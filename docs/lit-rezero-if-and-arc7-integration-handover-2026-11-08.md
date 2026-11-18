# Báo Cáo Bàn Giao Tích Hợp Đợt Phát Hành Literature Đầu Tiên: 6 Phim *Re:Zero IF* (`cinema`) & Đại Tuyển Tập Sách *Re:Zero Arc 7 — 116 Chương* (`library`)

- **Ngày thực hiện**: `2026-11-08`
- **Kỹ sư phụ trách**: **Literature Content Release & In-Game Integration Engineer** (`a68843e2-d192-4fdd-8d1a-076fde2236c6`)
- **Hội thoại Điều phối Tổng (Orchestrator)**: `199f0287-723d-43b5-a013-d519137afba4`
- **Hội thoại Hạ tầng (Infrastructure Builder)**: `498055f0-8746-457d-8717-9588d8e8ce28`
- **Hội thoại Kiểm định (Pack Reviewer)**: `3609e7e6-b4a0-4b56-92ff-f978e80fa9a6`
- **Đích vận hành**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & Sao lưu**: `D:\GTA Archive\Staging\project-eagle\lit-pack-integrator\`
- **Phiếu công việc**: [`docs/project-eagle/work-items/2026-11-08-antigravity-lit-integrate-rezero-if-and-arc7.md`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/work-items/2026-11-08-antigravity-lit-integrate-rezero-if-and-arc7.md) (`status: done`)

---

## 1. Tóm tắt Kết quả Thực hiện (Executive Summary)

1. **Thực thi nghiêm ngặt Quy tắc Cổng Chặn (`Gatekeeper Rules`)**:
   - Đã tích hợp chính xác **7 gói nội dung đạt chứng chỉ `READY_FOR_INTEGRATION`** từ `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\literature\certifications\*.cert.json` (`157` chương, `47,185` prose blocks, `50,442` VN beats, `938,951` từ, `716` CG `1376×768`, `14` covers, `57` BGM).
   - Tự động loại trừ gói thứ 8 đang sản xuất dở dang `rezero_arc8_wn` ở cả tầng CLI triển khai ([`tools/deploy_literature_pack.py`](file:///c:/Users/LENOVO/Desktop/GTA/tools/deploy_literature_pack.py)) lẫn tầng quét runtime trong [`eagle_literature_engine.py`](file:///c:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_literature_engine.py).
2. **Đồng bộ 100% Ánh xạ Schema Studio trong `eagle_literature_engine.py` & `cleo/EagleLiteratureHud.lua`**:
   - Cập nhật `LiteraturePack.get_indexed_chapter()` đọc đầy đủ các khóa chuẩn của Studio (`location_label`, `bgm`/`default_bgm_id`/`bgm_id`, `initial_cg`/`default_cg_id`/`cg_id`, `nvl_paragraph`/`book_text`/`text`, truyền `bgm_id` xuống từng beat và lọc bỏ các block `kind == "scene_break"` rỗng).
   - Lập chỉ mục `self.cast` không phân biệt hoa/thường theo cả `char_key.lower()` và `display_name.lower()`; ẩn nhãn người nói khi `speaker.lower() == "narrator"` để câu dẫn chuyện không bị gắn tiền tố `NARRATOR:`.
   - Bổ sung `.replace("{", "[").replace("}", "]")` vào `clean_cfont_ascii()` để khử sạch 3 dấu `}` đánh máy trong `rezero_rem_sloth_if`.
   - Mở rộng chế độ đọc sách `nvl_book` cho phép đoạn văn hiện tại (`p_off == 0`) wrap tối đa `14` dòng trước khi điền các đoạn kế tiếp vào phần dòng trống còn lại; nâng cấp modal Mục lục `[T]` (`TOC`) thành cửa sổ trượt `8` chương (`CH X-Y OF 116`) hỗ trợ nhảy tới bất kỳ chương nào trong `116` chương của `rezero_arc7_wn` và nâng cấp quầy vé/thư viện (`MODAL_TICKET_COUNTER` / `MODAL_LIBRARY_COUNTER`) thành cửa sổ trượt `5` mục.
3. **Xây dựng CLI Tích hợp Tự động [`tools/deploy_literature_pack.py`](file:///c:/Users/LENOVO/Desktop/GTA/tools/deploy_literature_pack.py) & Lịch chiếu/Kệ sách 30 Địa điểm**:
   - Hỗ trợ đầy đủ các lệnh `list`, `verify`, `stage`, `apply`, `remove`, `rollback`.
   - Liên kết không tốn dung lượng ổ `C:` bằng NTFS Directory Junction tại `Project Eagle\gta sa gameplay-lab\data\project-eagle\literature\packs\<work_id>` trỏ thẳng sang `D:\Eagle Literature Studio\packages\<work_id>`.
   - Cập nhật [`schedule_and_catalog.json`](file:///c:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/data/project-eagle/literature/schedule_and_catalog.json) phủ kín toàn bộ **15 Rạp Phim (`CIN-01..15`)** và **15 Thư Viện / Nhà Sách (`LIB-01..15`)**, kèm đầy đủ `waifu_discussion_hooks` cho cả 6 nhân vật (`hutao`, `furina`, `citlali`, `columbina`, `kirara`, `vesna`).
4. **Nghiệm thu Kép (Part A Offline 100% + Part B Live DirectX 9 `1920×1080` In-Game QA)**:
   - **Part A Offline (`verify_part_a_offline.py`)**: Quét toàn bộ `157` chương, `47,185` đoạn văn và `50,442` beats của 7 gói: `0` lỗi fallback bìa, `0` lỗi thiếu BGM, `0` lỗi ngoặc `{}`, `0` lỗi tiền tố `NARRATOR:`.
   - **Part B Live DirectX 9 `1920×1080` (`run_part_b_live_d3d9_qa.py`)**: Chụp và kiểm định trực tiếp 14 ảnh thực tế trong game dưới khóa `EagleCoordLock("ingame-runtime")`, `EagleLuaErrors.log = 0`, `eagle_doctor.py 11/11 PASS`.

---

## 2. Bảng Phân Bổ 7 Gói Đã Cấp Chứng Chỉ Trên 30 Địa Điểm

| STT | Mã gói (`work_id`) | Phân loại | Số chương | Số CG (`1376×768`) | Số BGM | Phân bổ tại 15 Rạp (`CIN-01..15`) & 15 Thư viện (`LIB-01..15`) |
| :--- | :--- | :--- | :---: | :---: | :---: | :--- |
| 1 | `rezero_ayamatsu_pride_if` | `cinema` + `library` archive | `6` | `50` | `8` | Chiếu tại cả 6 Đại Rạp (`CIN-01..04, 11, 12`) + Rạp nhỏ (`CIN-08, 09, 13, 14`); lưu trữ đọc sách tại `LIB-01, 02, 06, 09, 12` |
| 2 | `rezero_rem_sloth_if` | `cinema` + `library` archive | `9` | `44` | `8` | Chiếu tại cả 6 Đại Rạp + Rạp nhỏ (`CIN-05, 06, 07, 10, 15`); lưu trữ đọc sách tại `LIB-02, 03, 05, 06, 07, 11, 15` |
| 3 | `rezero_kasaneru_greed_if` | `cinema` + `library` archive | `6` | `42` | `8` | Chiếu tại cả 6 Đại Rạp + Rạp nhỏ (`CIN-06, 07, 08, 13, 15`); lưu trữ đọc sách tại `LIB-01, 02, 04, 06, 08, 13` |
| 4 | `rezero_butterfly_lust_if` | `cinema` + `library` archive | `8` | `28` | `6` | Chiếu tại cả 6 Đại Rạp + Rạp nhỏ (`CIN-05, 06, 10, 14, 15`); lưu trữ đọc sách tại `LIB-02, 03, 05, 06, 10, 14` |
| 5 | `rezero_oboreru_wrath_if` | `cinema` + `library` archive | `6` | `36` | `8` | Chiếu tại cả 6 Đại Rạp + Rạp nhỏ (`CIN-07, 08, 09, 13`); lưu trữ đọc sách tại `LIB-02, 06, 07, 09, 11, 12` |
| 6 | `rezero_tsugihagu_gluttony_if` | `cinema` + `library` archive | `6` | `42` | `8` | Chiếu tại cả 6 Đại Rạp + Rạp nhỏ (`CIN-05, 09, 10, 14`); lưu trữ đọc sách tại `LIB-02, 04, 06, 08, 10, 13, 14, 15` |
| 7 | `rezero_arc7_wn` | **Flagship `library`** | **`116`** | **`474`** | **`11`** | **Sách Tâm Điểm (#1 Flagship Light Novel)** tại toàn bộ **15/15 Thư viện & Nhà sách (`LIB-01..15`)** (Thuê 7 ngày `$5–$8`, Mua vĩnh viễn vào `EaglePhone` `$35`) |

---

## 3. Bằng Chứng Nghiệm Thu Thực Tế Trong Game (`1920×1080` DirectX 9 Screenshots)

Toàn bộ 14 ảnh chụp màn hình DirectX 9 (`1920×1080`) và báo cáo JSON chi tiết được lưu tại:
- Báo cáo JSON: [`D:\GTA Archive\Staging\project-eagle\lit-pack-integrator\part_b_live_d3d9_report.json`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/part_b_live_d3d9_report.json)
- Thư mục ảnh: `D:\GTA Archive\Staging\project-eagle\lit-pack-integrator\qa_screenshots\`

| Mã ảnh | Đường dẫn file | Nội dung kiểm định & kết quả |
| :---: | :--- | :--- |
| `01` | [`01_cin01_ticket_counter_rezero_if_1to5.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/01_cin01_ticket_counter_rezero_if_1to5.png) | Quầy vé Đại Rạp Vinewood (`CIN-01` -> `INT-CIN-GRAND`) hiển thị các phim *Re:Zero IF* (`Pride`, `Sloth`, `Greed`, `Wrath`, `Gluttony`), banner `16:9` nét căng, giá vé `$25`, combo bắp nước `$10` và 5 suất chiếu `09:00..23:30`. |
| `02` | [`02_cin01_ticket_counter_scroll_6th_lust_if.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/02_cin01_ticket_counter_scroll_6th_lust_if.png) | Cuộn cửa sổ trượt tại quầy vé xuống phim thứ 6 `>> 6/7. Re:Zero: Lust IF [8Ch]` kèm banner `16:9` hoàng cung Lugunica. |
| `03` | [`03_adv_cinema_pride_if_ch1_base_cg.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/03_adv_cinema_pride_if_ch1_base_cg.png) | Công chiếu phim #1 *Re:Zero: Pride IF* (`[CH 1/6] Royal Capital Lugunica -- Loot House`) ở chế độ `adv_cinema`: CG gốc `cg_ch01_sc01_base` (`16:9`), thẻ tên `Subaru` màu cam và BGM `Call of the Witch`. |
| `04` | [`04_adv_cinema_pride_if_ch1_diff_vow.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/04_adv_cinema_pride_if_ch1_diff_vow.png) | Chuyển cảnh sang biến thể `cg_ch01_sc01_diff_vow` (ánh kiếm đỏ của Elsa phía sau Subaru) qua cơ chế Double-Buffer TXD (`LITCG0.TXD` <-> `LITCG1.TXD`) không giật hình; câu dẫn chuyện không bị gắn nhãn `NARRATOR:`. |
| `05` | [`05_adv_cinema_sloth_if_rem_route.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/05_adv_cinema_sloth_if_rem_route.png) | Công chiếu phim #2 *Re:Zero: Sloth IF (Rem Route)* (`[CH 1/9] Western Border Highway -- Liger Passenger Carriage`): CG `16:9` Halibel, Rem và Subaru trên xe ngựa + BGM `Chain of Memories`. |
| `06` | [`06_adv_cinema_greed_if_echidna_route.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/06_adv_cinema_greed_if_echidna_route.png) | Công chiếu phim #3 *Re:Zero: Greed IF* (`[CH 1/6] New Roswaal Mansion -- Subaru's Bedroom & Washroom`): CG `16:9` Subaru soi gương + `BGM: Wish of the Stars` + `AUTO [A]: SLOW 1.0x`. |
| `07` | [`07_auditorium_after_hud_close_at_exit_door.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/07_auditorium_after_hud_close_at_exit_door.png) | **Kiểm tra bắt buộc**: Bấm `[Bksp]` đóng HUD xem phim, Aether vẫn đứng nguyên tại hàng ghế trong khán phòng 3D (`state == "CINEMA_AUDITORIUM"`, `Area Code = 1`, `POPCORN+SODA ACTIVE`) trước khi tự đi bộ qua cửa `EXIT` ra sảnh và ra phố. |
| `08` | [`08_lib02_counter_flagship_rezero_arc7_and_if_archive.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/08_lib02_counter_flagship_rezero_arc7_and_if_archive.png) | Quầy Thư viện Đại Thư Viện Kinokuniya Akihabara (`LIB-02` -> `INT-LIB-GRAND`) hiển thị sách tâm điểm `>> 1/8. Re:Zero Arc 7: Land of Wolves [116Ch]` (`CHAPTERS: 116 - ILLUSTRATIONS: 474`) cùng 6 bộ IF lưu trữ. |
| `09` | [`09_nvl_book_arc7_ch1_16x9_illustration_and_prose.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/09_nvl_book_arc7_ch1_16x9_illustration_and_prose.png) | Ngồi bàn đọc mở *Re:Zero Arc 7* ở chế độ `nvl_book`: cột trái hiển thị minh họa `16:9` (`cg_ch001_sc01_base` — Emilia, Ram, Beatrice tại Tháp Canh Pleiades), cột phải hiển thị trọn vẹn nhiều đoạn văn dài không bị cắt cụt. |
| `10` | [`10_nvl_book_arc7_toc_sliding_window_ch82_of_116.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/10_nvl_book_arc7_toc_sliding_window_ch82_of_116.png) | Bấm `[T]` mở Mục lục (`TABLE OF CONTENTS`) với cửa sổ trượt `CH 78-85 OF 116`, nhảy trực tiếp tới `>> [5] Ch.82: Chapter 76: Chance Meetings at the Imperial Capital`. |
| `11` | [`11_nvl_book_arc7_ch82_great_disaster_cg_and_prose.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/11_nvl_book_arc7_ch82_great_disaster_cg_and_prose.png) | Đọc Chương 82 (`PAGE 57/279`, `PROGRESS: 70.0%`) với minh họa `cg_ch082_sc01_diff_wheelchair_corridor` (Katya ngồi xe lăn trò chuyện cùng Rem tại Thủ đô Lupgana) và `BGM: Longing for Sunbeams`. |
| `12` | [`12_arc7_ch82_toggled_to_adv_cinema_mode.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/12_arc7_ch82_toggled_to_adv_cinema_mode.png) | Bấm `[V]` chuyển đổi tức thì giữa `nvl_book <-> adv_cinema` ngay tại Chương 82 của *Re:Zero Arc 7* mà không mất vị trí đoạn đang đọc. |
| `13` | [`13_library_hall_after_book_close_at_reading_table.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/13_library_hall_after_book_close_at_reading_table.png) | **Kiểm tra bắt buộc**: Bấm `[Bksp]` gấp sách, tự động lưu `bookmark` ở Chương 82 (`ch=81, blk=56`) và Aether vẫn đứng ngay cạnh bàn đọc trong đại sảnh thư viện 2 tầng (`state == "LIBRARY_HALL"`, `Area Code = 1`). |
| `14` | [`14_eaglephone_bookshelf_arc7_ch82_bookmark_resumed.png`](file:///D:/GTA%20Archive/Staging/project-eagle/lit-pack-integrator/qa_screenshots/14_eaglephone_bookshelf_arc7_ch82_bookmark_resumed.png) | Sau khi rời thư viện ra phố (`Area Code = 0`), mở tủ sách cá nhân trên `EaglePhone` (`open_phone_bookshelf`) và khôi phục chính xác `PAGE 57/279 (70.0%)` của Chương 82 *Re:Zero Arc 7*. |

---

## 4. Manifest SHA-256 & Hướng Dẫn Rollback An Toàn

### Bảng SHA-256 Trước & Sau Tích Hợp

| File | SHA-256 Trước Khi Apply | SHA-256 Sau Khi Apply |
| :--- | :--- | :--- |
| [`data/project-eagle/literature/schedule_and_catalog.json`](file:///c:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/data/project-eagle/literature/schedule_and_catalog.json) | `6abbb3fe4b593959a51308abeced72240558a4f1a357e00bf85f9ac4aab13a90` | `3be41ecfea88f2acec1f822efb9d60ce58f1a845df0a7e1bfa132e81a380d23c` |
| [`eagle_literature_engine.py`](file:///c:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_literature_engine.py) | `63770ef4b23234dbd73696ac9ad003051a77f80cc67ce0e8701fbda07d783bbc` | `5dbd792ef3bf6e2985c3bc93025d52d2b5c296240702df662f89fec5e5196e1e` |
| [`cleo/EagleLiteratureHud.lua`](file:///c:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/cleo/EagleLiteratureHud.lua) | `7efab738b15d2eccacb1c2c722b1cfe44a7ea6e05d39f8d1d16e5ff10b0f3b81` | `a9655cc4a62908f8359cfdeb583da3472625bb363a4f973d8d5252b4a3d3f867` |

### Các Lệnh Vận Hành & Rollback

- **Kiểm tra danh sách gói & trạng thái chứng chỉ Gatekeeper**:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py" list
  ```
- **Kiểm định Pre-Flight các gói chứng chỉ `READY_FOR_INTEGRATION`**:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py" verify --all-certified
  ```
- **Triển khai / Cập nhật lịch chiếu & kệ sách vào `gameplay-lab`**:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py" apply --all-certified
  ```
- **Rollback nguyên trạng về trước đợt phát hành 2026-11-08 (dưới khóa `game-write`)**:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py" rollback
  # Hoặc chạy trực tiếp script độc lập:
  python "D:\GTA Archive\Staging\project-eagle\lit-pack-integrator\rollback_lit_packs_20261108.py"
  ```
