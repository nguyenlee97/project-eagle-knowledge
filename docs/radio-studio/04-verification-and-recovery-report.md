# 04 — Báo Cáo Nghiệm Thu, Failure-Mode & Phục Hồi (Verification & Recovery Report)

Tài liệu này ghi nhận kết quả kiểm thử tự động từ đầu đến cuối (End-to-End), kết quả kiểm tra các tình huống lỗi (Failure-Mode), bằng chứng bảo toàn dữ liệu giữa **Gameplay Lab** và **Game Chính**, mã băm SHA-256 trước/sau khi cài đặt, và hướng dẫn kiểm tra thực tế trong game.

---

## 1. Phân tách rõ: Kiểm thử tự động (Đã thực hiện) vs. Kiểm thử nghe trong game (Dành cho người dùng)

Theo nguyên tắc minh bạch kỹ thuật:
- **Đã thực hiện và xác minh tự động trên máy (`7/7 PASS`)**:
  - Phân tích mã máy `PECore.asi` (`0x100F4670..0x100F8200`, `0x1012F0B0..0x1012F290`) và `bass.dll` (`v2.4.17`).
  - Kiểm thử bộ đọc/ghi AST bảo toàn byte-for-byte cho `data\radio.dat` (giữ nguyên cả kiểu xuống dòng hỗn hợp `CRLF`/`LF` của file gốc), `S&S\ZON\radio.zon` và `PECore.ini`.
  - Kiểm thử pipeline `ffmpeg`/`ffprobe` với 4 định dạng đầu vào (`MP3`, `FLAC`, `WAV`, `OGG`), kiểm tra Incremental Rebuild Cache (chỉ chuẩn hóa lại track thay đổi) và kiểm tra phát hiện file nhạc nguồn bị xóa/đổi tên.
  - Kiểm thử trích xuất 75 sprite gốc và đóng gói thêm 3 sprite `ERS_*` (`256x256` `D3DFMT_A8R8G8B8`) vào `models\txd\radio.txd`.
  - Kiểm thử cơ chế **Transactional Rollback** khi giả lập lỗi giữa chừng trong lúc Apply, cơ chế **1-Click Restore Backup**, và cơ chế **Surgical Uninstall** (`uninstall_tool_stations_only`).
  - Áp dụng bộ 3 kênh mẫu (`[Test Asset]`) vào **Gameplay Lab** (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`), giữ nguyên 100% **Game Chính** (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`).
- **Chưa tự mở cửa sổ game 3D để nghe trực tiếp (Cần người dùng nghiệm thu trong game)**:
  - Việc khởi chạy `gta_sa.exe` trong môi trường đồ họa DirectX 9, lên xe và xoay bánh xe radio là bước nghiệm thu trải nghiệm người dùng cuối trên **Gameplay Lab** (xem hướng dẫn chi tiết tại **Mục 6** bên dưới).

---

## 2. Kết quả bộ kiểm thử tự động (`tests/test_end_to_end.py`)

Chạy bằng lệnh:

```powershell
python -m pytest tests/test_end_to_end.py -v
```

| Mã bài test | Nội dung kiểm thử | Kết quả |
|---|---|---|
| `test_01_target_independence_and_preservation` | Xác minh `gameplay-lab` và `gta sa clean` là hai bản cài độc lập vật lý (`st_nlink == 1`, `st_ino` khác nhau hoàn toàn trên `radio.dat`, `radio.zon`, `PECore.ini`, `models\txd\radio.txd`). Xác minh đầy đủ các tài nguyên bảo toàn: Aether (`AETHER.dff/txd`), NPC (`COMPONENTPEDS.img`), `EagleCompanion.py`, `EagleLifePoC.cs`. | **PASSED** |
| `test_02_lossless_config_parser_and_sanitization` | Kiểm tra AST parser đọc đúng 7 vùng / 63 kênh active + 2 kênh `#Station=` bị comment (`Tatar Radio`, `Retro Plus`). Kiểm tra khử dấu phẩy `,` và chuyển tiếng Việt có dấu sang ASCII an toàn cho font GTA SA. Kiểm tra thêm/bỏ `[SanAndreas]` (`Region=2`) và `RAD_sanandreas` trong `radio.zon`. | **PASSED** |
| `test_03_txd_parser_badge_generator_and_sprite_injection` | Kiểm tra đọc RenderWare TXD (`0x16`), trích xuất 75 sprite sang PNG, sinh logo `Auto-Badge` `256x256` và bơm sprite `ERS_TEST01` vào bản sao `radio.txd` rồi gỡ bỏ về đúng 75 sprite gốc. | **PASSED** |
| `test_04_multi_format_audio_pipeline_and_incremental_cache` | Sinh 4 file nhạc mẫu ở 4 định dạng (`MP3`, `FLAC`, `WAV`, `OGG`). Biên dịch thành stream `.OGG` (`44100 Hz`, Stereo), kiểm tra `track_manifest` (`start_sec`, `end_sec`). Kiểm tra build lần 2 đạt `100% cache hit`, và khi chỉ đổi thứ tự track thì không phải giải mã lại bất kỳ track nào (`reencoded_tracks == 0`). | **PASSED** |
| `test_05_full_lab_apply_verification_and_restore` | Kiểm tra trọn vẹn chu trình `Staging Preview` -> `Apply` vào `gameplay-lab` -> Xác minh `radio.dat`, `radio.zon`, `radio.txd` (78 sprites), 3 file `.OGG` trong `AUDIO\PE\RADIO\CUSTOM\` và `audio\pe\radio\static.mp3` -> `Restore Backup` -> Xác minh SHA-256 khớp tuyệt đối với bản gốc. | **PASSED** |
| `test_06_failure_modes_and_transactional_rollback` | Kiểm tra 3 tình huống lỗi: (1) File nhạc nguồn bị xóa/đổi tên sau khi từng nạp cache -> hệ thống phát hiện ngay và chặn Apply (không dùng cache cũ âm thầm); (2) File nhạc hỏng (corrupt bytes) -> báo lỗi rõ ràng; (3) Giả lập lỗi giữa chừng khi đang Apply (`simulate_mid_apply_failure=True`) -> tự động Rollback tức thì toàn bộ file về đúng SHA-256 trước khi bấm Apply. | **PASSED** |
| `test_07_fastapi_endpoints_integration` | Kiểm tra toàn bộ REST API của `app.py` (`/api/status`, `/api/sprites`, `/api/regions/lookup`, `/api/stations`, `/api/build`, `/api/deploy/preview`, `/api/audio/stream/...`). | **PASSED** |

---

## 3. Bằng chứng bảo toàn dữ liệu (SHA-256 Baseline & Post-Apply)

### 3.1. Các file hệ thống Radio trước và sau khi cài đặt trên Gameplay Lab

| Đường dẫn tương đối | Kích thước gốc | Mã băm SHA-256 gốc (Baseline & Game Chính hiện tại) | Mã băm SHA-256 trên Gameplay Lab sau khi Apply 3 kênh mẫu |
|---|---|---|---|
| `data\radio.dat` | `5,398` bytes | `82682172b58707375923fed221ecf5723a5db75db2c265e927101a7d79828c4c` | `9a2cb164f345a6950e37578f17679f48cd0a56c70a41d6cce0ac4e9033f33116` |
| `S&S\ZON\radio.zon` | `892` bytes | `0275a3dee4b540844646b4fb780f4e4517b5e600dcdad829467db02b9a6942ba` | `04c2d5551f030787d3cce94d0e7fa0fcd536f24b73c29e3ff094080922f5c233` |
| `PECore.ini` | `7,400` bytes | `31489780cd21d25671f44cbd53bd1e05a5bebb557cba1330ac3508fc409887bc` | `d7c33d38baf83e2506b47f0efa59392415b558fc1c4cafc12830a463c175aca1` |
| `models\txd\radio.txd` | `19,929,212` bytes | `963d3ab73ced90f9fea65940ea21d055ad0c26ed67fca4cc76afbb20be9d817e` | `2237162a8a9d127f1ef15ab9f6bbd6663daf9f770b4fab3fbdafe0b31b39fb03` |

- **Bản sao lưu tự động (Pre-Apply Backup ID)**: `bk_20261014_113021_1582` tại `tools\eagle-radio-studio\data\backups\lab\bk_20261014_113021_1582\` lưu trữ nguyên bản byte-for-byte toàn bộ 4 file trên.

### 3.2. Trạng thái bảo toàn trên Game Chính (`gta sa clean\gta sa clean`)

- **Game Chính hoàn toàn không bị chỉnh sửa**: Toàn bộ 4 file trên tại `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean` giữ nguyên mã băm SHA-256 gốc ở cột Baseline.
- Các bản mod hiện có được xác minh nguyên vẹn:
  - `modloader\RZL-Skin\AETHER.dff` & `modloader\RZL-Skin\AETHER.txd` (Nhân vật chính Aether)
  - `S&S\Cdimages\default\COMPONENTPEDS.img` (Bộ NPC cảnh sát/SWAT/quân đội)
  - `PECore.asi`, `bass.dll`, `EagleCompanion.py`, `cleo\EagleLifePoC.cs`

---

## 4. Trạng thái hiện tại trên Gameplay Lab sau khi cài đặt bộ Demo 3 kênh

Để bạn có thể vào thử nghiệm ngay hoặc xem trực tiếp trên giao diện **Eagle Radio Studio**, bộ dự án mẫu gồm **3 kênh (`[Test Asset]`)** đã được biên dịch và cài đặt sẵn vào **Gameplay Lab** (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`):

1. **Teyvat Starlight FM** (`st_shared_anime`):
   - **Loại kênh**: Kênh dùng chung nhiều vùng (**Shared Station**).
   - **Vùng phủ sóng**: San Andreas (`Region=2`), Liberty (`Region=5`), Leonida / Vice City (`Region=7`), Cheyenne (`Region=1`), Praire (`Region=4`).
   - **Playlist mẫu**: 2 bài (`[Test] Teyvat Starlight (Anime J-Pop Demo)` MP3 + `[Test] Mondstadt Breeze (FLAC Lossless Demo)` FLAC — tổng thời lượng `15.0s`).
   - **File xuất trong Lab**: `AUDIO\PE\RADIO\CUSTOM\ST_SHARED_ANIME.OGG` + Sprite `ERS_ST_SHARED_ANIME` trong `models\txd\radio.txd`.
2. **Vice Neon CityPop 84** (`st_vice_only`):
   - **Loại kênh**: Kênh độc quyền theo vùng đô thị biển (**Region-Exclusive**).
   - **Vùng phủ sóng**: Leonida / Vice City (`Region=7`).
   - **Playlist mẫu**: 1 bài (`[Test] Vice Bay Sunset (City Pop WAV Demo)` WAV — thời lượng `7.5s`).
   - **File xuất trong Lab**: `AUDIO\PE\RADIO\CUSTOM\ST_VICE_ONLY.OGG` + Sprite `ERS_ST_VICE_ONLY` trong `models\txd\radio.txd`.
3. **Liberty Midnight OST** (`st_liberty_only`):
   - **Loại kênh**: Kênh theo cụm vùng Đông Bắc & Cao nguyên.
   - **Vùng phủ sóng**: Liberty (`Region=5`), Cordillera (`Region=3`), Neijas (`Region=6`).
   - **Playlist mẫu**: 1 bài (`[Test] Liberty Nocturne (Instrumental OST Demo)` OGG — thời lượng `8.5s`).
   - **File xuất trong Lab**: `AUDIO\PE\RADIO\CUSTOM\ST_LIBERTY_ONLY.OGG` + Sprite `ERS_ST_LIBERTY_ONLY` trong `models\txd\radio.txd`.

Ngoài ra:
- File tiếng nhiễu chuyển đài `audio\pe\radio\static.mp3` đã được bổ sung vào `gameplay-lab` để khắc phục cảnh báo `Failed to load static sound` trong `PECore.log`.
- Vùng `RAD_sanandreas` (`Region=2`) và section `[SanAndreas]` đã được bật trên `gameplay-lab` để bạn có thể nghe thử ngay tại Los Santos / San Fierro / Las Venturas mà không cần dịch chuyển sang bang khác.

---

## 5. Cách Khôi Phục (Restore / Rollback) Về Nguyên Bản Chỉ Với 1 Cú Nhấp

Bạn có 2 cách khôi phục bất kỳ lúc nào:

1. **Trên giao diện Eagle Radio Studio**:
   - Mở tab **4. Kiểm Tra, Cài Đặt & Sao Lưu**.
   - Trong bảng **Lịch Sử Bản Sao Lưu (Backup Snapshots)**, nhấn nút **Khôi phục bản này** ở bản chụp đầu tiên (trước khi cài đặt) -> Toàn bộ `data\radio.dat`, `S&S\ZON\radio.zon`, `PECore.ini`, `models\txd\radio.txd` sẽ trở về đúng byte-for-byte SHA-256 gốc và thư mục `AUDIO\PE\RADIO\CUSTOM\` sẽ được dọn sạch.
   - Hoặc nhấn nút **Gỡ riêng kênh của Tool (Giữ nguyên file gốc)** để chỉ gỡ các dòng `AUDIO\PE\RADIO\CUSTOM\*`, vùng `RAD_sanandreas` và các sprite `ERS_*`.
2. **Bằng dòng lệnh Python (nếu không mở UI)**:
   ```powershell
   cd "C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio"
   python -c "from pathlib import Path; from app import deploy_mgr; from core.deployer import KNOWN_TARGETS; print(deploy_mgr.restore_backup(Path(KNOWN_TARGETS['lab']['path'])))"
   ```

---

## 6. Hướng dẫn nghiệm thu thực tế trong game trên Gameplay Lab

Để kiểm tra trực tiếp trong game:

1. **Thay nhạc thật của bạn (Tùy chọn)**:
   - Mở **Eagle Radio Studio** (`Start_Eagle_Radio_Studio.bat` hoặc `http://127.0.0.1:8790`).
   - Chọn các kênh hoặc tạo kênh mới, nhấn **Chọn file từ máy...** (hoặc kéo thả file nhạc `.mp3`, `.flac`, `.wav`, `.ogg` của bạn vào), nhấn **Biên dịch tất cả kênh** rồi nhấn **Áp dụng (Apply) vào Gameplay Lab**.
2. **Khởi động bản Gameplay Lab**:
   - Chạy `gta_sa.exe` trong thư mục `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (lưu ý đóng game nếu game đang mở trước khi bấm Apply vì `RadioEx` chỉ đọc `data\radio.dat` một lần lúc khởi tạo game).
3. **Kiểm tra tại San Andreas (Los Santos / San Fierro / Las Venturas)**:
   - Lên bất kỳ xe ô tô / xe máy nào.
   - Cuộn con lăn chuột (hoặc phím chuyển đài radio): bạn sẽ thấy kênh **Teyvat Anime Wave [Test Asset]** cùng logo `Auto-Badge` sắc nét trên HUD và nghe thấy âm thanh phát liên tục.
4. **Kiểm tra sự khác biệt lineup theo vùng (Region Lineup)**:
   - Dịch chuyển (qua MapTeleporter hoặc lái xe) sang **Vice City / Leonida** (`Region=7`): cuộn đài sẽ thấy cả **Teyvat Anime Wave** và **Vice Neon CityPop**.
   - Dịch chuyển sang **Cordillera** (`Region=3`) hoặc **Neijas** (`Region=6`): cuộn đài sẽ thấy kênh độc quyền **Frontier Nocturne OST**.
5. **Kiểm tra `PECore.log`**:
   - Mở `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\PECore.log`: xác nhận dòng `[I] [RadioEx] Loaded radio configuration` và không còn lỗi thiếu `static.mp3`.
