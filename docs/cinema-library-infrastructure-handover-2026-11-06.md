# Báo Cáo Bàn Giao Hạ Tầng Rạp Chiếu Phim (Cinema) & Thư Viện / Nhà Sách (Library & Bookstore) — Project Eagle (06–07/11/2026)

- **Hội thoại thực hiện (Builder):** `498055f0-8746-457d-8717-9588d8e8ce28` (`antigravity`)
- **Hội thoại điều phối (Orchestrator):** `199f0287-723d-43b5-a013-d519137afba4`
- **Phiếu công việc:** [`docs/project-eagle/work-items/2026-11-06-antigravity-cinema-library-builder-items2to5.md`](work-items/2026-11-06-antigravity-cinema-library-builder-items2to5.md) (`status: done`)
- **Đích triển khai:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & Backup:** `D:\GTA Archive\Staging\project-eagle\cinema-library-builder-20261106\`

---

## 1. Tóm Tắt Kiến Trúc & Nguyên Tắc Tách Rời Dữ Liệu 100% (Plug-and-Play Cho Integrator)

Toàn bộ hạ tầng kỹ thuật từ **Hạng mục 2 → 5** đã được xây dựng, triển khai vào `gameplay-lab` và nghiệm thu **Part A (Offline)** + **Part B (Live DirectX 9 `1920×1080`)** đạt **100% PASS**:

1. **Tách rời 100% Code Engine và Catalog Dữ liệu (`EagleLit Pack v1.0`)**:
   - [`eagle_literature_engine.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_literature_engine.py) tự động quét các gói nội dung hợp lệ có `manifest.json` (`schema_version: "eagle_lit_v1"`) theo thứ tự ưu tiên:
     1. `Project Eagle/gta sa gameplay-lab/data/project-eagle/literature/packs/<work_id>/`
     2. `Project Eagle/gta sa gameplay-lab/ui_assets/literature_packs/<work_id>/`
     3. `D:\Eagle Literature Studio\packages\<work_id>\`
   - Lịch chiếu rạp (`cinema_schedules`) và phân kệ thư viện (`library_shelves`) được đọc động từ [`data/project-eagle/literature/schedule_and_catalog.json`](../../Project%20Eagle/gta%20sa%20gameplay-lab/data/project-eagle/literature/schedule_and_catalog.json). Khi **Hội thoại Integrator** thêm gói phim/sách mới vào `data/project-eagle/literature/packs/<work_id>/` (hoặc cập nhật `schedule_and_catalog.json`), Engine tự động đưa tác phẩm lên toàn bộ `15` Rạp phim và `15` Thư viện/Nhà sách mà **không cần sửa bất kỳ dòng code Python hay Lua nào**.

2. **Giao Diện Trình Chiếu Dual-Mode (`adv_cinema` & `nvl_book`) & Double-Buffer CG (`16:9` Khóa Cứng)**:
   - Module Lua độc lập [`cleo/EagleLiteratureHud.lua`](../../Project%20Eagle/gta%20sa%20gameplay-lab/cleo/EagleLiteratureHud.lua) được nạp động từ [`hud.lua`](../../Project%20Eagle/gta%20sa%20gameplay-lab/hud.lua).
   - **Double-Buffer TXD (`models/txd/LITCG0.TXD` & `LITCG1.TXD`)**: Chuyển đổi ảnh `.jpg`/`.png` từ gói nội dung sang `RW 0x16 / 0x15 DXT1 (512×256)` với tên texture `"ep_lit_cg"`, luân phiên 2 slot `cg_slot = 0 / 1` kèm `cg_ver` tăng dần để đổi cảnh mượt không giật khung hình, khóa cứng tỷ lệ `16:9` (`1300×731` trong `adv_cinema`, `800×450` trong `nvl_book`) trên màn hình `1920×1080`.
   - **Chế độ `adv_cinema` (Xem phim tại Rạp)**: Khung hình `16:9` viền vàng kim, dải phụ đề kính mờ dưới đáy, thẻ tên nhân vật đổi màu theo `nameplate_color_rgb`, điều khiển `[Space/Enter/LMB]` qua beat, `[Up/Left]` lùi beat, `[A]` Auto-Play 3 tốc độ (`SLOW 1.0x`, `MID 1.4x`, `FAST 2.0x` tự cộng thời gian theo số từ của beat), `[H]` ẩn UI ngắm CG, `[B]` Backlog lịch sử thoại, `[T]` nhảy chương, `[V]` chuyển nhanh sang chế độ sách, `[Backspace]` rời ghế.
   - **Chế độ `nvl_book` (Đọc Light Novel tại Thư viện / Tủ sách `EaglePhone`)**: Giao diện 2 cột nền tối dịu mắt (khung minh họa `16:9` + thẻ thông tin chương bên trái, trang sách nhiều đoạn văn bên phải), cuộn trang mượt bằng con lăn chuột (`0x00CAFE78`), phím lên/xuống hoặc cảm ứng (`0x00CAFE60`), mục lục nhảy chương `[T]`, và **tự động lưu `bookmark` (`chapter_id`, `chapter_index`, `block_idx`, `block_id`, `beat_idx`, `beat_id`, `progress_pct`)** vào [`data/project-eagle/literature/eagle_lit_save.json`](../../Project%20Eagle/gta%20sa%20gameplay-lab/data/project-eagle/literature/eagle_lit_save.json).
   - **Âm thanh Nhạc nền (`alias lit_bgm`)**: Phát nhạc nền instrumental từ `bgm/` của gói qua Win32 MCI riêng biệt (`alias lit_bgm`), tự động lặp khi hết bài, tự động tạm dừng khi vào Pause Menu (`0x00BA67A4 != 0`), và dùng `GTAPerProcessAudioMuter` tắt tiếng ồn GTA khi mở HUD trình chiếu (khôi phục 100% âm thanh GTA khi đóng HUD / trong `finally:`).

3. **Luồng Trạng Thái Thực Tế 3D Theo Từng Phòng (Bắt Buộc Đúng Thiết Kế)**:
   - **Rạp Chiếu Phim (`CIN-01..CIN-15`)**:
     `Ngoài đường [E]` -> Bước vào **Sảnh rạp 3D (`CINEMA_LOBBY`)** -> Tới **Quầy vé (`TICKET_COUNTER`)** mua vé (`$25` Đại Rạp / `$12` Rạp Nhỏ, `5` suất/ngày `09:00, 13:00, 17:00, 20:30, 23:30`, linh hoạt **`±60` phút giờ game**, đổi miễn phí `$0` sang suất kế tiếp nếu trễ) & **Quầy Bắp Nước (`POPCORN_COUNTER`)** -> Đi bộ tới **Cửa Phòng Chiếu (`AUDITORIUM_ENTRY`)** bấm `[E]` kiểm tra vé -> Bước vào **Phòng Chiếu 3D (`CINEMA_AUDITORIUM`)** -> Đi bộ tới **Ghế ngồi (`AUDITORIUM_SEAT`)** bấm `[E]` mở HUD `adv_cinema` -> **Khi xem hết phim HOẶC bấm `[Backspace]` thoát giữa chừng: chỉ đóng HUD, nhân vật Aether VẪN ĐỨNG TẠI GHẾ TRONG PHÒNG CHIẾU 3D (`state == "CINEMA_AUDITORIUM"`, `Area Code = 1`)** -> Đi bộ ra cửa `EXIT` xanh (`AUDITORIUM_EXIT`) bấm `[E]` trở ra **Sảnh rạp (`CINEMA_LOBBY`)** -> Đi bộ ra cửa chính (`LOBBY_EXIT`) bấm `[E]` về lại đúng tọa độ ngoài đường (`return_xyz`, `Area Code = 0`).
   - **Thư Viện & Nhà Sách (`LIB-01..LIB-15`)**:
     `Ngoài đường [E]` -> Bước vào **Thư viện 3D (`LIBRARY_HALL`)** -> Tới **Quầy Thủ Thư (`LIBRARIAN_COUNTER`)** thuê sách 7 ngày (`$5` / `$4`) hoặc mua vĩnh viễn (`$45` / `$35`, tự động lưu vào `owned_books` đọc mọi lúc trên **Tủ sách cá nhân `EaglePhone`** bằng phím `[B]` tại Home Screen) -> Đi bộ tới **Bàn đọc sách (`READING_TABLE`)** bấm `[E]` mở HUD `nvl_book` -> Đóng HUD lưu `bookmark` và giữ Aether đứng cạnh bàn đọc trong Thư viện -> Đi bộ ra cửa chính (`LIBRARY_EXIT`) bấm `[E]` về lại ngoài đường.

---

## 2. Dải ID Đã Khóa & Tài Nguyên 3D Đã Triển Khai

| Hạng mục | Dải ID / Đường dẫn | Chi tiết kỹ thuật |
| :--- | :--- | :--- |
| **30 Địa điểm Thế giới** | Static IDs `15110..15139` | `15` Rạp phim (`CIN-01..CIN-15`, `15110..15124`) + `15` Thư viện/Nhà sách (`LIB-01..LIB-15`, `15125..15139`) từ `venues_30_verified.json`. Gồm **10 Tòa nhà 3D mới trên đất trống** (`CIN-02, CIN-03, CIN-11, CIN-13, CIN-14, LIB-05, LIB-06, LIB-13, LIB-14, LIB-15`) và **20 Cổng vòm/Biển hiệu/Poster 3D điểm nhấn**. |
| **4 Tổ hợp Nội thất 3D (`Area Code = 1`, `Z = +1650.0m`)** | Static IDs `15140..15201` | `15140` (`int_cin_grand`, LOD `15160`) tại `(2700, -1650, 1650)`; `15141` (`int_cin_small`, LOD `15161`) tại `(3150, -1650, 1650)`; `15180` (`int_lib_grand`, LOD `15200`) tại `(2700, -2150, 1650)`; `15181` (`int_lib_small`, LOD `15201`) tại `(3150, -2150, 1650)`. |
| **20 Custom Peds Nhân viên & Độc giả** | Ped IDs `49466..49485` | `lit_ped_01..lit_ped_20` đăng ký trong [`data/peds.ide`](../../Project%20Eagle/gta%20sa%20gameplay-lab/data/peds.ide) và đóng gói `.dff`/`.txd` vào `CUSTOM/cinema_library_world.img`. |
| **Archive Thế giới & Nội thất** | `CUSTOM\cinema_library_world.{ide,ipl,col,img}` | `112.50 MB` (`85` entries `.dff`/`.txd`), `38` IDE definitions, `34` IPL instances (`lodIndex = -1`), `34` COL3 collision models, đăng ký trong [`data/gta.dat`](../../Project%20Eagle/gta%20sa%20gameplay-lab/data/gta.dat). |
| **CLEO Native Bridge (`60 FPS`)** | `cleo\EagleLiteratureBridge.cs` | `1813` bytes, ký hiệu `ELIT` (`0x454C4954`) tại `0x00CAFE50` & con trỏ shared block tại `0x00CAFE54`, thực thi dịch chuyển `04E4` + `04BB` + `0860` + `00A1` + `0173` + `0373`, vẽ corona `024F` và spawn/cleanup NPC nội thất (`009A` / `009B`). |
| **GG Map & EagleRide** | `lit_poi_cin_01..15`, `lit_poi_lib_01..15` | Đã đăng ký toàn bộ `30` địa điểm vào [`eagle_gg_map_pois.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_gg_map_pois.py) (`CURATED_GG_MAP_POIS` + `_POI_EN_BY_ID`) và [`eagle_ride_engine.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ride_engine.py) (`DEFAULT_UNLOCKED_POIS`). |

---

## 3. Kết Quả Nghiệm Thu Kép (Part A Offline + Part B Live DirectX 9 `1920×1080`)

### 3.1. Part A — Kiểm Tra Offline (`verify_part_a_offline.py` & `eagle_doctor.py`)
- **Kiểm tra cấu trúc `.IMG` / `.IDE` / `.IPL` / `.COL3`**: `85` entries trong `cinema_library_world.img`, `38` IDE definitions, `34` IPL instances (`lodIndex = -1`), `34` COL3 models kín sàn/trần/tường, `20` Custom Peds `49466..49485` hợp lệ.
- **Kiểm tra `eagle_doctor.py`**: **`11/11 PASS, 0 WARN, 0 FAIL`** (`0` lỗi Lua trong `EagleLuaErrors.log`, `535` map mounts OK).

### 3.2. Part B — Kiểm Tra Live In-Game DirectX 9 `1920×1080` (`run_part_b_live_d3d9_qa.py`)
- Báo cáo JSON: `D:\GTA Archive\Staging\project-eagle\cinema-library-builder-20261106\part_b_live_d3d9_report.json` (`"passed": true`, `"lua_errors": 0`).
- Bộ `12/12` ảnh chụp `1920×1080` đã kiểm tra trực quan tại `D:\GTA Archive\Staging\project-eagle\cinema-library-builder-20261106\qa_screenshots\`:
  1. `01_outdoor_cin01_vinewood_cathay.png`: Ngoài đường `CIN-01` (`Vinewood Cathay Grand Theatre`) kèm cổng vòm 3D và prompt `[E]`.
  2. `02_outdoor_cin02_new_3d_building_sakura_imax.png`: Tòa nhà 3D mới trên đất trống `CIN-02` (`Sakura Multiplex IMAX`) kèm corona và prompt `[E]`.
  3. `03_int_cin_grand_lobby_and_custom_npcs.png`: Bên trong Sảnh Đại Rạp `INT-CIN-GRAND` (`Area Code = 1`, `Z = +1650.05m`) với biển `BOX OFFICE / TICKETS & POPCORN` và dàn Custom NPCs.
  4. `04_int_cin_grand_ticket_counter_modal.png`: Giao diện Quầy vé Box Office hiển thị poster `16:9`, danh sách 5 phim tuần và 5 suất chiếu `09:00 [13:00] 17:00 20:30 23:30 (OPEN NOW (+/-60m))`.
  5. `05_int_cin_grand_imax_auditorium_seats.png`: Bên trong Phòng chiếu IMAX bậc thang 60 ghế (`INT-CIN-GRAND`), màn chiếu lớn `16:9` và prompt `[E] Sit at IMAX Panorama Row E -> Start Movie Screening`.
  6. `06_adv_cinema_hud_16x9_rezero_pride_if.png`: Trình chiếu `adv_cinema` `1920×1080` với khung CG `16:9` sắc nét, dải phụ đề kính mờ dưới đáy và thẻ tên nhân vật.
  7. `07_adv_cinema_backlog_and_autoplay.png`: Trình chiếu `adv_cinema` bật `AUTO [A]: SLOW 1.0x` và bảng `DIALOGUE & NARRATION BACKLOG`.
  8. `08_auditorium_after_hud_close_at_exit_door.png`: Xác nhận sau khi đóng HUD `adv_cinema`, nhân vật Aether **vẫn đứng trong Phòng chiếu 3D** trước cửa `EXIT` xanh trước khi đi bộ ra Sảnh rạp và về lại đường phố `CIN-01` (`Area Code = 0`).
  9. `09_outdoor_lib06_new_3d_building_yae_pavilion.png`: Tòa nhà 3D mới trên đất trống `LIB-06` (`Cider Lake Yae & Favonius Book Pavilion`) kèm prompt `[E]`.
  10. `10_int_lib_grand_hall_and_librarian_modal.png`: Đại Thư Viện 2 tầng `INT-LIB-GRAND` và giao diện Quầy Thủ Thư (`[ENTER] RENT 7 DAYS: $5 - [P] BUY FOREVER (EAGLEPHONE): $45 - [C] COFFEE: $4`).
  11. `11_nvl_book_hud_16x9_multi_paragraph.png`: Chế độ đọc sách `nvl_book` `1920×1080` tại bàn đọc sách (khung minh họa `16:9` bên trái, trang văn bản nhiều đoạn bên phải, cuộn trang bằng con lăn chuột `0x00CAFE78` tới `PAGE 6/139`, `BOOKMARK AUTO-SAVED`).
  12. `12_eaglephone_bookshelf_bookmark_resume_and_toc.png`: Mở **Tủ sách cá nhân `EaglePhone`** ngoài đường phố, tự động khôi phục đúng `bookmark` (`block_idx = 5`, `PAGE 6/139`) và mở bảng `TABLE OF CONTENTS (PRESS [1-8] TO JUMP)`.

---

## 4. Hướng Dẫn Dành Cho Hội Thoại Integrator & Lệnh Rollback

### 4.1. Cách Hội Thoại Integrator Nạp Phim / Light Novel Mới (Không Cần Sửa Code)
1. Đặt gói tác phẩm chuẩn `eagle_lit_v1` vào:
   `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\data\project-eagle\literature\packs\<work_id>\`
2. (Tùy chọn) Thêm `<work_id>` vào danh sách phim chiếu của rạp hoặc kệ sách thư viện trong:
   `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\data\project-eagle\literature\schedule_and_catalog.json`
   *(Nếu chưa khai báo trong `schedule_and_catalog.json`, `EagleLiteratureEngine` vẫn tự động phân phối gói mới vào lịch chiếu và kệ sách của cả 30 địa điểm).*

### 4.2. Lệnh Rollback Nguyên Tử
Nếu cần hoàn tác toàn bộ đợt triển khai hạ tầng Rạp Chiếu Phim & Thư Viện về trạng thái trước khi cài đặt:
```powershell
python "D:\GTA Archive\Staging\project-eagle\cinema-library-builder-20261106\rollback_cinema_library_infra.py"
```
