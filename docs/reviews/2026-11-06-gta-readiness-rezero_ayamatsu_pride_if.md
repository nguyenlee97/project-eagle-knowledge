# Biên Bản Đánh Giá Sẵn Sàng Tích Hợp GTA (`GTA Readiness Review`) — `rezero_ayamatsu_pride_if`

- **Ngày kiểm định**: `2026-11-06` (cập nhật hoàn tất kiểm định: `2026-11-07T02:27:00+07:00`)
- **Đơn vị kiểm định**: Hội thoại 2 — *GTA Literature Integration Readiness & Technical Asset Reviewer* (`3609e7e6-b4a0-4b56-92ff-f978e80fa9a6`, chế độ **chỉ-đọc runtime game**)
- **Gói nội dung kiểm định**: `D:\Eagle Literature Studio\packages\rezero_ayamatsu_pride_if\`
- **Hội thoại sản xuất nguồn**: `bb0448a6-8995-48dd-a0db-c0337c57128d` (*Re Zero Ayamatsu Pride If Production*)
- **Đích tích hợp mục tiêu**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (`EagleLiteratureEngine` + `hud.lua` + `.TXD` Ping-Pong Slot + Win32 `mciSendStringW`)
- **Kết luận Tổng thể (`Verdict`)**: **`READY_FOR_INTEGRATION`** (`0` Blockers — Đạt tuyệt đối cả `4/4` GTA Readiness Gates)

---

## 1. Bảng Tóm Tắt Kết Quả 4 Cổng Kiểm Định (`4 GTA Readiness Gates`)

| Cổng Kiểm Định (`Gate`) | Hạng Mục Kiểm Tra Kỹ Thuật Trong Engine GTA | Chỉ Số Đo Lường Thực Tế | Trạng Thái |
| :--- | :--- | :--- | :---: |
| **Gate 1 — Schema & Hợp đồng `EagleLiteratureEngine`** | Cấu trúc `manifest.json` + `chapters/ch01..06.json`, tham chiếu `cg_id` / `bgm_id` / `speaker`, mã màu `nameplate_color_rgb`, đồng bộ Dual-Mode (`adv_cinema` & `nvl_book`) | `6` chương, `21` cảnh, `647` blocks (`640` prose + `7` breaks), `803` `vn_beats`, `15,866` từ (`verbatim_word_match_ratio = 1.0`). `50/50` CG & `8/8` BGM có dùng thực tế (`0` orphan). `100%` block khớp `cg_id`/`bgm_id` với beat đầu. | **PASS (`schema_ok = true`)** |
| **Gate 2 — Bảng Mã Chữ RenderWare `CFont` & Khung HUD `1920x1080`** | Quét ký tự điều khiển cấm của `CFont` (`~`, `|`, `*`, `{`, `}`, `@`, `\t`, ngoặc kép cong, gạch dài, `…`, non-ASCII ngoài `0x20..0x7E`) và kiểm tra tràn hộp phụ đề `4` dòng (`fw = 752.0`) | **`0` vi phạm `CFont`** trên toàn bộ `manifest` + `647` blocks + `803` beats. Độ dài beat: min `4`, TB `114.3`, **max `235` ký tự** (`<= 240`). **`0/803` beat vượt quá `4` dòng** ở độ rộng `66` cột. Nhãn `speaker` dài nhất `11` ký tự (`Townsperson`). | **PASS (`cfont_ok = true`)** |
| **Gate 3 — Raster DirectX 9 / `.TXD` & Duyệt Mắt `52/52` Ảnh (`read_file`)** | Kiểm tra header JPEG/Pillow, hệ màu RGB, cờ baseline (`progressive = False`), SHA-256 duy nhất, viền đen nội bộ, độ sáng màn chiếu và duyệt trực tiếp `52/52` ảnh bằng `read_file` | `poster.jpg` (`832x1248`, `2:3`), `banner_16x9.jpg` (`1376x768`, `16:9`) + `50/50` CG (`1376x768`, `16:9`) đều là **Baseline RGB JPEG**, `52/52` SHA-256 duy nhất, `0` viền đen letterbox, vùng mặt nằm gọn trong Safe Zone `y = 0.08..0.75`, chuyển cảnh `_base -> _diff` khóa góc máy hoàn hảo. | **PASS (`raster_txd_ok = true`, `visual_hud_ok = true`)** |
| **Gate 4 — Thử Nghiệm Phát Nhạc Thực Tế Win32 `mciSendStringW`** | Gọi trực tiếp `ctypes.windll.winmm.mciSendStringW` (`open ... type mpegvideo alias lit_bgm`, `status length`, `setaudio volume`, `play`, `status mode/position`, `close`) trên cả `8` file `.mp3` | **`8/8` track mở và phát thành công `100%`** (`rc = 0`, `mode = playing`, con trỏ `pos_ms` tịnh tiến ổn định). Toàn bộ `8` file là MP3 CBR `192 kbps`, `44.1 kHz`, Stereo, `0` ID3v2 cover-art tag, `nb_streams = 1`. | **PASS (`mci_audio_ok = true`)** |

---

## 2. Chi Tiết Kiểm Định Từng Cổng (`Technical Breakdown`)

### 2.1. Gate 1 — Schema, Tham Chiếu Tài Nguyên & Nhịp Đọc Dual-Mode (`EagleLiteratureEngine`)

1. **Định danh & Chế độ đọc**:
   - `schema_version`: `"eagle_lit_v1"`
   - `work_id`: `"rezero_ayamatsu_pride_if"`
   - `venue_type`: `"cinema"`
   - `default_read_mode`: `"adv_cinema"`
   - `supported_read_modes`: `["adv_cinema", "nvl_book"]`
2. **Thống kê cấu trúc `chapters/ch01.json .. ch06.json`**:

| Chương | File | Tiêu Đề Chương | Số Cảnh (`scenes`) | Tổng `blocks` (Prose / Break) | Tổng `vn_beats` | Số Từ (`word_count`) | Tổng `auto_hold_ms` (`1.0x`) |
| :---: | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Ch.01** | `chapters/ch01.json` | *Chapter 1: A Loop of Eighty-Seven Lives* | `5` | `135` (`133` / `2`) | `172` | `3,522` | `1,040,420 ms` (`17.34p`) |
| **Ch.02** | `chapters/ch02.json` | *Chapter 2: The Madman and the Finger* | `3` | `97` (`96` / `1`) | `124` | `2,535` | `751,950 ms` (`12.53p`) |
| **Ch.03** | `chapters/ch03.json` | *Chapter 3: The Spirit Knight and the Fallen Earl* | `3` | `102` (`100` / `2`) | `126` | `2,542` | `755,000 ms` (`12.58p`) |
| **Ch.04** | `chapters/ch04.json` | *Chapter 4: The Pyre of Greed* | `2` | `66` (`66` / `0`) | `84` | `1,720` | `508,820 ms` (`8.48p`) |
| **Ch.05** | `chapters/ch05.json` | *Chapter 5: The Broken Blue and the Accomplices* | `3` | `78` (`78` / `0`) | `94` | `1,843` | `560,670 ms` (`9.34p`) |
| **Ch.06** | `chapters/ch06.json` | *Chapter 6: The Hero Who Burned the World* | `5` | `169` (`167` / `2`) | `203` | `3,704` | `1,202,870 ms` (`20.05p`) |
| **TỔNG** | **6 files** | **Toàn bộ tác phẩm** | **`21`** | **`647` (`640` / `7`)** | **`803`** | **`15,866`** | **`4,819,730 ms` (`80.33p`)** |

3. **Kiểm định bảng phân vai (`cast`) & mã màu `nameplate_color_rgb`**:
   - Toàn bộ `18` nhân vật trong `manifest.cast` có mã màu `[R, G, B]` hợp lệ (`int` trong `[0..255]`).
   - Toàn bộ `803` `vn_beats` sử dụng `19` giá trị `speaker`: `Narrator` (`483` beats), `Subaru` (`150`), `Elsa` (`36`), `Petelgeuse` (`24`), `Reinhard` (`20`), `Emilia` (`18`), `Regulus` (`18`), `Meili` (`10`), `Felix` (`9`), `Thug` (`8`), `Otto` (`7`), `Julius` (`6`), `Guard` (`3`), `Puck` (`3`), `Felt` (`2`), `Townsperson` (`2`), `Witch` (`2`), `Roswaal` (`1`), `Guiltilaw` (`1`). Không có bất kỳ nhân vật lạ nào nằm ngoài danh mục (`0` unmapped speakers).
4. **Kiểm định đồng bộ Dual-Mode (`[V]` Toggle `adv_cinema` <-> `nvl_book`)**:
   - `100%` (`640/640`) prose block có `block.cg_id == block.vn_beats[0].cg_id` và `block.bgm_id == block.vn_beats[0].bgm_id`.
   - Khi người chơi bấm `[V]` chuyển qua lại giữa chế độ xem phim (`adv_cinema`) và chế độ đọc trang sách (`nvl_book`) hoặc khôi phục từ `bookmark`, hình nền CG và nhạc nền BGM luôn khớp tuyệt đối tại mọi vị trí đoạn văn.
   - Nhịp chuyển ảnh CG: `50` lần đổi CG trên `803` beats (trung bình `16.06` beats/CG, chuỗi giữ nguyên 1 CG dài nhất là `37` beats), đảm bảo bộ nạp kép `LITCG0.TXD` / `LITCG1.TXD` có dư thời gian prefetch mà không gây khựng khung hình.

---

### 2.2. Gate 2 — Bảng Mã Chữ RenderWare `CFont` & Khung Phụ Đề `1920x1080`

1. **An toàn `CFont` tuyệt đối (`0` lỗi)**:
   - Đã quét từng byte trên mọi trường chuỗi (`title`, `subtitle`, `authors`, `synopsis_short`, `chapter_title`, `scene_title`, `speaker`, `blocks[].text`, `vn_beats[].text`, `inner_thought`).
   - **Kết quả**: `0` ký tự ngoài khoảng ASCII in được `0x20..0x7E`, `0` dấu ngã `~` (tránh lỗi crash/đổi màu gãy chuỗi của `CFont::ParseToken`), `0` dấu `|`, `*`, `{`, `}`, `@`, `\t`, `\r`, `\n`.
2. **Độ khít khung HUD `1920x1080` (`DrawTextL` / `CFont::m_fWrapx`)**:
   - Với thông số hộp thoại Cinema (`fw = ScreenSize(752.0)`, lề chữ hai bên `ScreenSize(18.0)` -> vùng chữ thực tế `ScreenSize(716.0)`, cỡ chữ `scaleX = 0.192, scaleY = 0.412` tương đương `~66` ký tự/dòng, tối đa `4` dòng):
     - **Độ dài `vn_beat`**: ngắn nhất `4` ký tự, trung bình `114.3` ký tự, **dài nhất `235` ký tự** (`ch02` `b0094_0`, thấp hơn ngưỡng khuyến nghị `240` ký tự và thấp hơn xa trần cứng `280` ký tự).
     - **Phân bổ số dòng sau khi word-wrap ở `66` cột**:
       - `1` dòng: `162` beats (`20.17%`)
       - `2` dòng: `391` beats (`48.69%`)
       - `3` dòng: `191` beats (`23.79%`)
       - `4` dòng: `59` beats (`7.35%`)
       - **`>= 5` dòng (tràn khung): `0` beats (`0.00%`)**
     - **Độ dài nhãn tên `speaker`**: tối đa `11` ký tự (`"Townsperson"`, `"Petelgeuse"` `10` ký tự), nằm gọn hoàn toàn trong tab Nameplate rộng `ScreenSize(164.0)`.

---

### 2.3. Gate 3 — Tương Thích Raster DirectX 9 / `.TXD` & Duyệt Mắt `52/52` Ảnh (`read_file`)

#### A. Bảng Kiểm Kỹ Thuật Raster & Provenance

| Nhóm Tài Nguyên | Số Lượng File | Kích Thước (`W x H`) | Tỷ Lệ Khung | Định Dạng / Hệ Màu | Baseline JPEG (`progressive = False`) | Khoảng Dung Lượng | Khoảng Độ Sáng (`mean_luma`) | Trạng Thái Đóng Gói `.TXD` / D3DX9 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Poster Sảnh / Mặt Tiền** (`poster.jpg`) | `1` | `832 x 1248` | `2:3` (`0.6667`) | `JPEG / RGB` | Có (`100%`) | `278.5 KB` | `66.1` (`std = 56.2`) | **PASS** (Chuẩn khung Poster sảnh `2:3`) |
| **Banner Lịch Chiếu** (`banner_16x9.jpg`) | `1` | `1376 x 768` | `16:9` (`1.7917`) | `JPEG / RGB` | Có (`100%`) | `248.4 KB` | `68.2` (`std = 57.5`) | **PASS** (Chuẩn khung Marquee/UI `16:9`) |
| **Bộ CG Phim** (`cgs/cg_ch01..ch06_*.jpg`) | `50` | `1376 x 768` | `16:9` (`1.7917`) | `JPEG / RGB` | Có (`50/50`) | `161.3 KB .. 322.2 KB` (Tổng `12.66 MB`) | `24.1 .. 164.2` | **PASS** (Chuẩn nạp `LITCG0.TXD` / `LITCG1.TXD`) |

- **Tính toàn vẹn Hash & Provenance**:
  - `52/52` file ảnh có mã băm SHA-256 duy nhất (`0` ảnh trùng lặp hay placeholder), khớp `100%` với `manifest.json` và `cg_generation_manifest.json` (`total_items = 52`, `completed = 52`, `pending = 0`).
  - `0/52` ảnh bị viền đen letterbox/pillarbox bên trong khung `16:9`.

#### B. Kết Quả Duyệt Bằng Mắt Thật (`read_file`) Toàn Bộ `52/52` Ảnh Dưới Góc Nhìn HUD GTA `1920x1080`

Toàn bộ `52` file ảnh (`poster.jpg`, `banner_16x9.jpg` và `50` CG từ `ch01` đến `ch06`) đã được mở và kiểm tra trực tiếp bằng `read_file`:

1. **Poster (`poster.jpg`) & Banner (`banner_16x9.jpg`)**:
   - Đúng phong cách bìa Light Novel Shinichirou Otsuka kết hợp White Fox anime key visual.
   - Không có bất kỳ chữ giả, watermark hay logo rác nào; khi hiển thị trên bảng lịch chiếu rạp hoặc UI chọn phim trong GTA sẽ hoàn toàn sạch sẽ, rõ nét.
2. **Chương 1 (`10` CG — `cg_ch01_sc01_base` đến `cg_ch01_sc05_diff_slash`)**:
   - Tái hiện con hẻm thủ đô Lugunica, nhà kho của Felt/Rom và trận đụng độ Elsa & Reinhard.
   - Các cặp `_base -> _diff` (`sc01_base -> sc01_diff_vow`, `sc03_base -> sc03_diff_slaughter`, `sc04_base -> sc04_diff_emilia`, `sc05_base -> sc05_diff_reinhard -> sc05_diff_slash`) giữ nguyên góc máy và kiến trúc nền, chỉ thay đổi cử chỉ/biểu cảm/hiệu ứng kiếm khí. Khuôn mặt nhân vật nằm gọn trong vùng `y = 0.12..0.68`, hoàn toàn không bị hộp thoại `22%` đáy màn hình che khuất.
3. **Chương 2 (`8` CG — `cg_ch02_sc01_base` đến `cg_ch02_sc03_diff_dark_smile`)**:
   - Chuyển đổi mượt từ nụ cười tươi sáng của Emilia (`sc01_base -> sc01_diff_smile`) sang khu rừng băng và hang ổ Giáo phái Phù thủy với Petelgeuse (`sc02_base -> sc02_ice_base -> sc02_diff_cult`, `sc03_base -> sc03_diff_petelgeuse -> sc03_diff_dark_smile`). Ánh sáng trong hang tối có độ tương phản cao nhờ đuốc lửa và miasma tím, hiển thị rất rõ trên màn chiếu rạp.
4. **Chương 3 (`7` CG — `cg_ch03_sc01_base` đến `cg_ch03_sc03_diff_pawn`)**:
   - Cặp `sc01_base -> sc01_diff_spirit` (Julius & Hỏa Tinh Linh đỏ), `sc02_base -> sc02_diff_pout` (thuần phục Meili dưới ánh trăng), `sc03_roswaal_base` (Roswaal tuyệt vọng trong dinh thự) và `sc03_cell_base -> sc03_diff_pawn` (thu phục Otto trong ngục tối) đồng nhất thiết kế trang phục (áo khoác đen viền vàng của Subaru Pride IF) và khóa bố cục tuyệt đối.
5. **Chương 4 (`5` CG — `cg_ch04_sc01_base` đến `cg_ch04_sc02_diff_pyre`)**:
   - Trận đốt dinh thự của Tổng giám mục Tham lam Regulus Corneas: chuỗi `sc01_base -> sc01_diff_elsa_kick` và chuỗi 3 bước `sc02_base -> sc02_diff_elsa_join -> sc02_diff_pyre` giữ nguyên hàng đèn đường, cổng dinh thự bốc cháy và vị trí đứng của Subaru, tạo hiệu ứng chuyển động liên hoàn giống hệt hoạt cảnh Visual Novel thương mại.
6. **Chương 5 (`5` CG — `cg_ch05_sc01_base` đến `cg_ch05_sc03_diff_solace`)**:
   - Cặp `sc01_base -> sc01_diff_headpat` (Felix suy sụp bên cạnh Julius gục ngã trong quán rượu), `sc02_base` (Otto bước vào cửa quán rượu) và cặp `sc03_base -> sc03_diff_solace` (bức tranh 5 đồng phạm: Elsa, Meili, Subaru, Felix, Otto, Roswaal rồi chuyển sang các bóng mờ ký ức trong màn sương tím) có bố cục cân đối, sắc nét và giàu chiều sâu.
7. **Chương 6 (`15` CG — `cg_ch06_sc01_base` đến `cg_ch06_sc05_diff_eternal`)**:
   - Cao trào biển lửa thủ đô: `sc01_base` (tạm biệt Meili), chuỗi 3 ảnh đối đầu Reinhard (`sc01_reinhard_base -> sc01_diff_boast -> sc02_diff_tears`), cặp Elsa chặn Reinhard (`sc02_elsa_base -> sc02_diff_farewell`), cặp Ma thú Guiltilaw bị Puck đóng băng (`sc03_base -> sc03_diff_frozen`), chuỗi 4 ảnh Subaru gặp Emilia (`sc04_base -> sc04_diff_tracksuit -> sc04_diff_emilia_tears -> sc04_diff_pride`), cảnh kết trên tuyết (`sc04_finale_base`) và cặp Shadow Garden (`sc05_base -> sc05_diff_eternal`).
   - Đặc biệt, 2 ảnh tối nhất gói (`cg_ch06_sc05_base` với `mean_luma = 24.1` và `cg_ch06_sc05_diff_eternal` với `mean_luma = 29.0`) đã được kiểm tra kỹ bằng mắt: nền đen của Vườn Bóng Tối là chủ đích nghệ thuật, trong khi nhân vật Subaru mặc đồ thể thao trắng-cam và luồng sáng tím xoay quanh nổi bật hoàn toàn ở trung tâm khung hình (`std_luma = 31.6..33.8`), không hề bị mù chi tiết khi chiếu trong rạp.

---

### 2.4. Gate 4 — Kết Quả Thử Nghiệm Phát Nhạc Thực Tế Bằng Win32 `mciSendStringW`

Đã chạy script Python gọi trực tiếp `ctypes.windll.winmm.mciSendStringW` (mô phỏng chính xác kênh `lit_bgm` của GTA) trên toàn bộ `8/8` file `.mp3`:

| `bgm_id` | File Vật Lý (`bgm/*.mp3`) | Dung Lượng | Chuẩn Mã Hóa (`ffprobe`) | `open` (`rc`) | `status length` (`ms`) | `setaudio volume` (`base_mci_volume`) | `play` & `status mode` | `close` (`rc`) |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| `bgm_01_witch_call` | `bgm/bgm_01_witch_call.mp3` | `3,551.8 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `151,536 ms` (`2p31s`) | `220` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_02_takt_of_heroes` | `bgm/bgm_02_takt_of_heroes.mp3` | `3,646.9 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `155,598 ms` (`2p35s`) | `230` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_03_sloth_gong` | `bgm/bgm_03_sloth_gong.mp3` | `4,782.1 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `204,029 ms` (`3p24s`) | `215` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_04_elegy_for_rem` | `bgm/bgm_04_elegy_for_rem.mp3` | `5,693.9 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `242,939 ms` (`4p02s`) | `190` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_05_gray_tragedy` | `bgm/bgm_05_gray_tragedy.mp3` | `4,167.2 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `177,802 ms` (`2p57s`) | `205` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_06_chain_of_memories` | `bgm/bgm_06_chain_of_memories.mp3` | `6,349.1 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `270,890 ms` (`4p30s`) | `210` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_07_requiem_of_silence` | `bgm/bgm_07_requiem_of_silence.mp3` | `9,930.1 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `423,680 ms` (`7p03s`) | `240` (`rc = 0`) | `playing` (`pos > 0`) | `0` |
| `bgm_08_wish_stars` | `bgm/bgm_08_wish_stars.mp3` | `2,931.6 KB` | MP3 CBR `192kbps`, `44.1kHz`, `2ch`, `0` ID3 tags | `0` | `125,075 ms` (`2p05s`) | `185` (`rc = 0`) | `playing` (`pos > 0`) | `0` |

---

## 3. Lưu Ý Kỹ Thuật Quan Trọng Khi Đóng Gói (`Integration Notes` Cho Builder & Integrator)

Mặc dù gói `rezero_ayamatsu_pride_if` đạt chuẩn `100%` (`0` lỗi cần sửa ở phía Studio), **Hội thoại 1 (`Infrastructure Builder`)** và **Hội thoại 3 (`Game Integrator`)** cần lưu ý **3 điểm ánh xạ dữ liệu** sau để `EagleLiteratureEngine` nạp gói trơn tru ngay từ lần chạy đầu tiên:

1. **Tên khóa danh mục trong `manifest.json` (`cast` / `cg_catalog` / `bgm_catalog`)**:
   - Theo `GTA_EAGLE_LIT_CONTRACT_V1.md` Mục 3.1, file `manifest.json` xuất xưởng dùng tên khóa chính thức là:
     - `"cast"` (mảng `18` object nhân vật)
     - `"cg_catalog"` (dict `50` CG)
     - `"bgm_catalog"` (dict `8` BGM)
   - Trong `eagle_literature_engine.py`, bộ parser nên hỗ trợ đọc cả `"cast"` lẫn alias `"cast_registry"`, `"cg_catalog"` lẫn `"cg_registry"`, và `"bgm_catalog"` lẫn `"bgm_registry"`.
2. **Ánh xạ trường `"speaker"` trong `vn_beats[]` sang mã màu `nameplate_color_rgb`**:
   - Trong `chapters/ch01..06.json`, mỗi phần tử của `vn_beats[]` dùng khóa `"speaker"` chứa tên hiển thị (`display_name`, ví dụ `"Subaru"`, `"Elsa"`, `"Reinhard"`, `"Narrator"`).
   - Khi tra cứu màu Nameplate từ `manifest.cast`, `EagleLiteratureEngine` nên xây bảng tra cứu hai chiều theo cả `cast_entry["display_name"]` và `cast_entry["char_key"]`.
   - Với `"speaker": "Narrator"` (`483/803` beats dẫn chuyện), engine cần gán màu mặc định Slate-Silver `[226, 232, 240]` (hoặc ẩn tab Nameplate nếu thiết kế HUD chọn kiểu hộp dẫn chuyện thuần túy).
3. **Đề xuất danh sách Rạp Phim (`recommended_venues`) từ Bản Quy Hoạch 30 Địa Điểm**:
   - Vì `rezero_ayamatsu_pride_if` là phim Visual Novel hành động/bi kịch quy mô lớn (`6` chương, `50` CG IMAX `16:9`, `8` BGM giao hưởng, thời lượng `~65-80` phút), gói này phù hợp để lên lịch chiếu tại:
     - **6 Đại Rạp (`GRAND` IMAX Multiplex — Suất chiếu Tâm điểm Tuần / Featured Premiere)**:
       - `CIN-01` (*Vinewood Cathay Grand Theatre* — Los Santos)
       - `CIN-02` (*Sakura Multiplex IMAX* — North Chicago `INLAND-03A`)
       - `CIN-03` (*Akihabara TOHO Anime Cinema* — Japan Island `WIBU-01`)
       - `CIN-04` (*The Loop Historic Grand Theatre* — Downtown Chicago)
       - `CIN-11` (*Wichita Heartland Grand Multiplex* — Wichita)
       - `CIN-12` (*Cottonmouth Bayou Grand Movie Haus* — Cottonmouth)
     - **6 Rạp Nhỏ Hợp Gu Anime / Dark-Fantasy (`SMALL` Boutique)**:
       - `CIN-06` (*Queens Castro Art-House Cinema* — San Fierro)
       - `CIN-07` (*Chinatown Lantern Indie Cinema* — Las Venturas)
       - `CIN-08` (*Staunton Opera & Indie Film Hall* — Liberty City)
       - `CIN-09` (*Bullworth Classic Town Theatre* — Bullworth Town)
       - `CIN-10` (*Rose City Retro Cinema* — Rose City)
       - `CIN-15` (*Independence Liberty Screening Hall* — Independence City)
     - **2 Thư Viện Lưu Trữ Bản Đọc Dual-Mode (`nvl_book`)**:
       - `LIB-02` (*Kinokuniya 8F Light Novel Megastore* — Akihabara `WIBU-01`)
       - `LIB-06` (*Cider Lake Yae & Favonius Book Pavilion* — Mondstadt `M1` Hồ Cider)
