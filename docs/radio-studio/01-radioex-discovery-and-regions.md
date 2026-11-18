# 01. Khảo Sát Kỹ Thuật Thực Tế: `RadioEx` & `ZoneEx` trên Project Eagle v1.3

- **Ngày cập nhật:** 14/10/2026
- **Đối tượng phân tích:**
  - [`PECore.asi`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/PECore.asi) (`2,977,792` bytes, SHA-256 `A81C69EF...`, ImageBase `0x10000000`, build `Jun 15 2026`)
  - [`bass.dll`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/bass.dll) (`147,528` bytes, v2.4.17)
  - [`data\radio.dat`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/data/radio.dat) (`5,398` bytes, 7 sections, 63 active stations + 2 commented stations)
  - [`S&S\ZON\radio.zon`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/S&S/ZON/radio.zon) (`892` bytes, 7 type-5 zones)
  - [`models\txd\radio.txd`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/models/txd/radio.txd) (`19,670,440` bytes, RenderWare D3D9 TexDict chứa 75 textures `256x256` 32-bit BGRA)

---

## 1. Giải Đáp 8 Câu Hỏi Discovery Bằng Bằng Chứng Binary & Config

### Câu 1: `RadioEx` đọc file nào, khi nào? Cơ chế nạp lại, cache hay yêu cầu restart?
- **Bằng chứng tĩnh (`[STATIC-BIN]`):**
  - Trong `RadioEx_Patch` (`VA 0x100F8560`), `PECore.asi` đăng ký 5 lambda sự kiện:
    1. `0x100F8C70` (`initGameEvent`): Gọi `RadioEx::Init` (`VA 0x100F4670`) và vá hàm `CHud::DrawRadioStation` (`0x4E9E50`) nếu `UseVisualRadioSprites = true`.
    2. `0x100F8D70` (`reInitGameEvent`): Reset trạng thái stream khi New Game / Load Game (không đọc lại `radio.dat`).
    3. `0x100F8ED0` (`processScriptsEvent`): Gọi `RadioEx::Update` (`VA 0x100F7670`) mỗi frame.
    4. `0x100F8EE0` (`drawHudEvent`): Gọi `RadioEx::DrawCustomRadioHud` (`VA 0x100F42A0`) và vẽ sprite đài SA gốc.
    5. `0x100F90A0` (`shutdownEngineEvent`): Giải phóng toàn bộ stream BASS và TXD slot khi thoát game.
  - Hàm `RadioEx::LoadConfig` (`VA 0x100F4AA0`) đọc `data\radio.dat` bằng `std::ifstream` và **chỉ có đúng 1 điểm gọi duy nhất** trong toàn bộ binary (`0x100F46C0` bên trong `RadioEx::Init`).
- **Kết luận cho Adapter:**
  - Không có cơ chế hot-reload hay file watcher cho `data\radio.dat` hoặc `models\txd\radio.txd`.
  - Mọi thay đổi cấu hình kênh/vùng hoặc thêm bài mới **bắt buộc phải khởi động lại game** để có hiệu lực.

---

### Câu 2: Station audio thực sự được resolve từ đâu? Vì sao baseline chưa thấy file? Thiếu audio tác động thế nào?
- **Bằng chứng tĩnh & khảo sát ổ đĩa (`[STATIC-BIN]` + `[CONFIG-DATA]`):**
  - Khi người chơi lái xe bước vào một vùng radio mới, `RadioEx::OnEnterRegion` (`VA 0x100F6D10`) gọi `RadioEx::LoadRegionStreams` (`VA 0x100F68A0`).
  - Tại `0x100F6A66`, đường dẫn `AudioFile` được kiểm tra bằng `std::filesystem::exists` **tương đối so với thư mục gốc của game** (working directory).
  - Rà soát toàn bộ workspace xác nhận thư mục `AUDIO\PE\RADIO\` **không có mặt** trong bản phân phối `gta sa clean` lẫn `ProjectEagle_Release`.
  - **Tác động khi thiếu file audio:**
    - Nếu `std::filesystem::exists` trả về `false`, `PECore.asi` ghi `[W] [RadioEx] Audio file not found: <path>` (`0x100F6AC9`) và giữ `station.m_StreamHandle = 0` (`[station + 0x4C]`).
    - Kênh thiếu audio **không bị xóa khỏi vòng chọn đài** và **không gây crash**. Khi người chơi chuyển tới kênh đó, game phát tiếng sôi chuyển đài (nếu có `audio\pe\radio\static.mp3`), sau đó phát sự im lặng.
  - **File `audio\pe\radio\static.mp3`:**
    - Được nạp tại `0x100F4714` (hoặc lazy-load tại `0x100F7420`). Bản gốc đang thiếu file này nên `PECore.log` báo `[W] [RadioEx] Failed to load static sound from audio\pe\radio\static.mp3`. **Eagle Radio Studio** tự động bổ sung `audio\pe\radio\static.mp3` để hiệu ứng chuyển đài hoạt động trọn vẹn.

---

### Câu 3: Codec/container, sample rate, duration, loop/seek và giới hạn cấu trúc dữ liệu?
- **Bằng chứng tĩnh (`[STATIC-BIN]`):**
  - `RadioEx` tạo stream qua CLEO opcode `0x0AAC` (`BASS_StreamCreateFile(FALSE, path, 0, 0, BASS_SAMPLE_LOOP)`), bật loop qua `0x0AC0`, chỉnh âm lượng qua `0x0ABC`, và đăng ký 3 custom CLEO opcodes trong `OpcodeMgr::Init` (`0x10132070`):
    - `0x3210`: `BASS_ChannelGetPosition` + `BASS_ChannelBytes2Seconds`
    - `0x3211`: `BASS_ChannelSeconds2Bytes` + `BASS_ChannelSetPosition`
    - `0x3212`: `BASS_ChannelGetLength` + `BASS_ChannelBytes2Seconds`
  - Bản `bass.dll` v2.4.17 đi kèm hỗ trợ trực tiếp **OGG Vorbis (`.ogg`), MP3 (`.mp3`), WAV (`.wav`), AIFF**, nhưng **không hỗ trợ trực tiếp FLAC/M4A/AAC/Opus** nếu thiếu plugin ngoài. Do đó, pipeline của **Eagle Radio Studio** nhận đầu vào đa định dạng (`MP3, WAV, OGG, FLAC, M4A, AAC, OPUS`) và biên dịch thống nhất ra **OGG Vorbis (`44100 Hz`, Stereo `2ch`, `-q:a 5`)**.
  - **Duration (`0x100F6B42`):** Nếu `Duration <= 0` trong `radio.dat`, `RadioEx` tự gọi opcode `0x3212` để đo độ dài thực tế của stream.
  - **Giới hạn cấu trúc:**
    - `m_Regions` (`0x1026F0E0`) là `std::unordered_map<int, RegionConfig>` (struct `68` bytes).
    - `m_Stations` (`[region + 0x34]`) là `std::vector<StationConfig>` (struct `88` bytes). Không có giới hạn mảng tĩnh về số vùng hay số kênh mỗi vùng.
    - **Ràng buộc bộ đọc CSV (`0x100F54A8`):** Dòng `Station=` được tách bằng `std::getline(ss, token, ',')` không có cơ chế escape $\rightarrow$ **Tên kênh và đường dẫn tuyệt đối không được chứa dấu phẩy `,`**, và đường dẫn file audio phải là ASCII thuần (do `BASS_StreamCreateFile` gọi với `unicode = FALSE`).

---

### Câu 4: Một station nhận nhiều file hay một stream? Có shuffle runtime, metadata bài hay virtual position không?
- **Bằng chứng tĩnh (`[STATIC-BIN]`):**
  - Mỗi `StationConfig` (`88` bytes) chỉ lưu duy nhất 1 chuỗi `m_AudioFile` (`+0x18`) và 1 `m_StreamHandle` (`+0x4C`). Hoàn toàn **không có** cơ chế danh sách nhiều file con hay hiển thị tên bài hát đang phát (now-playing metadata) trong engine.
  - **Cơ chế Đồng Hồ Phát Sóng Ảo (`m_VirtualPosition` tại `+0x50`):**
    - Trong `RadioEx::Update` (`0x100F7B50`–`0x100F7BF4`), mỗi frame engine tính `dt` (giây) và duyệt qua **tất cả các kênh của tất cả các vùng**:
      - Nếu kênh đang phát: đồng bộ `m_VirtualPosition = GetAudioStreamPosition(handle)` (`0x3210`).
      - Nếu kênh không phát: cộng `m_VirtualPosition += dt` và chia lấy dư cho `m_Duration`.
    - Khi người chơi vặn đài tới kênh đó (`0x100F80DE`), `RadioEx` gọi `SetAudioStreamPosition(handle, m_VirtualPosition)` (`0x3211`) để phát tiếp đúng vị trí thời gian thực như một đài phát thanh đang phát sóng liên tục.

---

### Câu 5: Cơ chế chọn Region theo Zone/Player/Vehicle và xử lý vùng San Andreas / chồng lấn?
- **Bằng chứng tĩnh (`[STATIC-BIN]`):**
  - `ZoneEx::Init` (`0x1012F260`) hook `CTheZones::CreateZone` (`0x5B4B2E` $\rightarrow$ `0x1012ED20`) và lưu mọi zone có `type == 5` từ `S&S\ZON\radio.zon` vào `std::vector<RadioZone>` tại `0x1026F17C`.
  - Trong `ZoneEx::GetRadioRegion` (`VA 0x1012F1C0`):
    - Kiểm tra tọa độ `(x, y, z)` của xe/người chơi với từng hộp `[minX..maxX, minY..maxY, minZ..maxZ]`.
    - **Xử lý chồng lấn (`0x1012F226..0x1012F23A`):** Tính diện tích 2D `area = (maxX - minX) * (maxY - minY)` và chọn zone có **diện tích 2D nhỏ nhất** (`area < bestArea`).
    - Nếu không thuộc hộp nào trong `radio.zon`, trả về `-1` (`0xFFFFFFFF`).
  - **Phát hiện quyết định về vùng San Andreas (`0x100F77A2..0x100F7868`):**
    - Trong `RadioEx::Update`, engine gọi `ZoneEx::GetRadioRegion(&pos)` **TRƯỚC** (`0x100F77A2`).
    - Nếu `radioRegionId != -1` và tìm thấy `radioRegionId` trong `m_Regions` (`data\radio.dat`), tại `0x100F7817..0x100F7826` code gán `hasCustomRegion = true`, nhảy qua (`jmp 0x100f7868`) và đặt `inSA = false` (`xor dl, dl`)!
    - Chỉ khi `radioRegionId == -1` (không có zone trong `radio.zon`), engine mới kiểm tra `GetMapCityRegion()` (`0x10142260`) để bật 11 đài GTA SA gốc (`inSA = true`).
    - **Ý nghĩa:** Mặc định `S&S\ZON\radio.zon` chỉ khai báo 7 vùng (ID `1, 3, 4, 5, 6, 7, 8`, bỏ trống ID `2`) nên San Andreas (`[-3000..3000, -3000..3000]`) dùng 11 đài gốc. Nhờ luồng ưu tiên ở `0x100F77A2`, **Eagle Radio Studio** cung cấp tùy chọn bật/tắt **`San Andreas (Region 2)`**: khi bật, tool thêm `RAD_sanandreas` (`Region=2`) vào `radio.zon` và `[SanAndreas]` vào `radio.dat` để phát kênh custom ngay tại Los Santos / San Fierro / Las Venturas; khi tắt, San Andreas giữ nguyên 11 đài gốc!

---

### Câu 6: Dùng chung một Station/Audio cho nhiều Region?
- **Bằng chứng tĩnh (`[STATIC-BIN]`):**
  - Nhiều section `[Region]` trong `data\radio.dat` có thể trỏ tới **cùng một đường dẫn `AudioFile`** (ví dụ `AUDIO\PE\RADIO\CUSTOM\ST_SHARED.OGG`). Tool chỉ cần build **1 file `.OGG` duy nhất** trên đĩa.
  - Khi lái xe qua ranh giới hai vùng cùng có kênh đó, vì `m_VirtualPosition` của cả hai bản ghi trong `m_Regions` đều được cộng `dt` như nhau mỗi frame (`0x100F7B50`), khi sang vùng mới và chọn kênh đó, nhạc tiếp tục phát tại đúng vị trí thời gian tương ứng.

---

### Câu 7: Hiển thị Tên / Sprite (`models\txd\radio.txd`) và Fallback?
- **Bằng chứng tĩnh (`[STATIC-BIN]`):**
  - Danh sách trong Pause Menu (`PrintRadioStationList` `0x5746F0` $\rightarrow$ `0x100F0480`) và hàm `GetRadioStationName` (`0x507000` $\rightarrow$ `0x100F0250`) luôn trả về chuỗi `station.m_Name`.
  - Hiển thị trên HUD chính giữa phía trên màn hình (`RadioEx::DrawCustomRadioHud` tại `VA 0x100F42A0`):
    - Nếu `UseVisualRadioSprites = true` (mặc định trong `PECore.ini`): vẽ texture `256x256` có tên `SpriteName` nạp từ `MODELS\TXD\<TxdName>.txd` (`models\txd\radio.txd`). Nếu `SpriteName` không tìm thấy trong `radio.txd` (`texPtr == NULL` tại `0x100F4401`), hàm thoát ngay (`je 0x100f4629`) — không bị crash hay ô trắng, nhưng không vẽ chữ thay thế trên HUD.
    - Nếu `UseVisualRadioSprites = false`: nhánh `0x100F44BD` vẽ trực tiếp chữ `station.m_Name` bằng font GTA SA (`FontStyle 2`, màu vàng cam `0x90, 0x62, 0x10`).
  - **Giải pháp toàn diện trong Eagle Radio Studio:**
    1. Trích xuất toàn bộ **75 sprite có sẵn** trong `models\txd\radio.txd` ra PNG để người dùng chọn trực quan trong UI (không cần sửa `radio.txd`).
    2. Hỗ trợ **Tự tạo Logo HUD 256×256 (`Auto-Badge`)** theo tên kênh hoặc **Tải ảnh PNG/JPG riêng**, tự động đóng gói chunk RenderWare D3D9 `0x15` (`D3DFMT_A8R8G8B8`, `256x256`) vào `models\txd\radio.txd` để chế độ `UseVisualRadioSprites = true` hiển thị logo sắc nét cho mọi kênh mới!
    3. Cung cấp công tắc bật/tắt `UseVisualRadioSprites` trong `PECore.ini` ở phần Cài đặt nâng cao.

---

### Câu 8: Khả năng hỗ trợ của ModLoader?
- Trong `modloader\.data\plugins\plugins.ini:14`, `gta3.std.stream=0` đang tắt. Đồng thời, `PECore.asi` mở `data\radio.dat` bằng `std::ifstream` và `bass.dll` mở file `.OGG` bằng `CreateFileA` nội bộ.
- Do đó, **ghi trực tiếp vào thư mục gốc của target (`data\radio.dat`, `AUDIO\PE\RADIO\CUSTOM\*.OGG`, `models\txd\radio.txd`, `S&S\ZON\radio.zon`) thông qua hệ thống Staging + SHA-256 Backup/Restore nguyên tử của tool** là phương án tin cậy tuyệt đối.
