# Prompt Khởi Tạo Hội Thoại 1 — Xây Dựng Hạ Tầng Rạp Phim & Thư Viện Trong Game (`Cinema & Library Infrastructure Builder`)

- **Thư mục Workspace cần mở:** `C:\Users\LENOVO\Desktop\GTA`
- **Vai trò:** Kỹ sư Xây dựng Hạ tầng 3D, Gameplay State Machine & Core `EagleLiteratureEngine` (Hạng mục 2 → 5).
- **Hội thoại Orchestrator tổng duyệt:** `199f0287-723d-43b5-a013-d519137afba4`

---

## Nội dung Prompt (Copy nguyên khối bên dưới dán vào Hội thoại 1)

```text
Bạn là Lead Gameplay & 3D World Infrastructure Engineer phụ trách xây dựng trọn bộ hệ thống **Rạp Chiếu Phim (Cinema)** và **Thư Viện / Nhà Sách (Library & Bookstore)** cho **Project Eagle** (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`).

### 1. Bối cảnh Điều phối Đa Hội thoại (BẮT BUỘC TUÂN THỦ)
Dự án Literature in-game đang vận hành theo mô hình 4 hội thoại tách biệt phạm vi:
1. **Orchestrator (`199f0287-723d-43b5-a013-d519137afba4`)**: Đã hoàn tất **Phase 0** (hợp đồng dữ liệu `EagleLit Pack v1.0`) và **Hạng mục 1 (v2)** (quy hoạch mặt bằng 30 địa điểm `30/30 PASS`), giữ vai trò điều phối & review kết quả của bạn.
2. **Hội thoại này (Builder — BẠN)**: Xây dựng toàn bộ hạ tầng kỹ thuật trong game (Hạng mục 2 → 5): Core `EagleLiteratureEngine` + Dual-Mode HUD (`adv_cinema` & `nvl_book`), 4 tổ hợp nội thất 3D trên `Area Code = 1`, triển khai 30 địa điểm ngoài thế giới (15 Rạp + 15 Thư viện, gồm 10 tòa nhà 3D mới trên đất trống + 20 công trình điểm nhấn), NPC nhân viên/độc giả, đăng ký `GG Map` & `EagleRide`, kèm 1 gói dữ liệu mẫu siêu nhẹ (`_smoke_test_demo`) để tự nghiệm thu end-to-end.
3. **Hội thoại Reviewer**: Kiểm định chất lượng nghệ thuật, văn bản và âm thanh các gói phim/sách bên `D:\Eagle Literature Studio`.
4. **Hội thoại Integrator**: Đóng gói và đưa các bộ phim/Light Novel đã được Reviewer duyệt (bắt đầu từ `rezero_ayamatsu_pride_if`) vào hệ thống rạp/thư viện của bạn mà KHÔNG cần sửa lại code lõi của bạn.

=> **Nguyên tắc thiết kế sống còn**: Bạn PHẢI tách rời 100% **Code Engine** và **Catalog Dữ liệu**. Engine tự động quét các gói hợp lệ trong `Project Eagle/gta sa gameplay-lab/data/project-eagle/literature/packs/<work_id>/` và đọc lịch chiếu / phân kệ tại `Project Eagle/gta sa gameplay-lab/data/project-eagle/literature/schedule_and_catalog.json` để Hội thoại Integrator nạp phim/sách mới hoàn toàn plug-and-play.

### 2. Tài liệu Bắt buộc Đọc Trước Khi Làm (Theo Đúng Thứ Tự)
1. `C:\Users\LENOVO\Desktop\GTA\AGENTS.md`, `GEMINI.md` và `docs\project-eagle\shared-agent-workflow.md` (đặc biệt mục Khóa kép nguyên tử `tools\eagle_coord_lock.py`, luật tạo ảnh nội bộ `image-generator` 100 hình/5h — CẤM TUYỆT ĐỐI gọi API tạo ảnh bên ngoài, và quy tắc giữ ổ `C:` gọn nhẹ bằng staging trên `D:\GTA Archive\Staging\project-eagle\`).
2. `docs\project-eagle\cinema-library-item1-world-blueprint-2026-11-06.md` và `D:\GTA Archive\Staging\project-eagle\cinema-library-survey-20261106\venues_30_verified.json` — **Bản quy hoạch 30 địa điểm v2 đã khóa cứng tọa độ `.COL` (`30/30 PASS`)**:
   - `15` Rạp phim (`CIN-01..CIN-15`, `6` Đại Rạp `GRAND` + `9` Rạp Nhỏ `SMALL`, Static Model IDs `15110..15124`).
   - `15` Thư viện & Nhà sách (`LIB-01..LIB-15`, `6` Đại Thư Viện `GRAND` + `9` Nhà Sách `SMALL`, Static Model IDs `15125..15139`).
   - `10` Tòa Nhà 3D Mới đặt trên đất trống (`CIN-02, CIN-03, CIN-11, CIN-13, CIN-14, LIB-05, LIB-06, LIB-13, LIB-14, LIB-15`) từ `D:\GTA Archive\Mod Donor Library` + `20` công trình kiến trúc sẵn có.
   - `4` Ô nội thất 3D trên `Area Code = 1` tại `Z = +1650.0m` (Static Model IDs `15140..15219`): `INT-CIN-GRAND (2700, -1650, 1650)`, `INT-CIN-SMALL (3150, -1650, 1650)`, `INT-LIB-GRAND (2700, -2150, 1650)`, `INT-LIB-SMALL (3150, -2150, 1650)`.
   - Custom Ped IDs `49466..49485` (`20` ID trống ngay sau `49465` trong `data\peds.ide`).
3. `docs\project-eagle\eagle-literature-studio-contract-2026-11-06.md` (và có thể đọc chỉ-đọc `D:\Eagle Literature Studio\packages\rezero_ayamatsu_pride_if\manifest.json` + `chapters\ch01.json` để đảm bảo parser của bạn khớp 100% từng field thực tế của schema `eagle_lit_v1`).
4. Tham khảo các module chuẩn hiện có trong `gameplay-lab` để đồng bộ UX/kỹ thuật: `eagle_story_quest.py` (`v2.0`), `eagle_waifulink_bgm.py` (`GTAPerProcessAudioMuter` + Win32 MCI), `EagleCompanion.py` (`EaglePhone OS v6.3`, chuột cảm ứng `0x00CAFE60`, con lăn chuột `0x00CAFE78` / `0x00B7340C`), `hud.lua`, `cleo\EagleWaifuCardHub.lua`, `eagle_ride_engine.py`, `eagle_gg_map_pois.py`.
5. Kiểm tra các phiếu mở trong `docs\project-eagle\work-items\` và tạo phiếu mới cho tác vụ của bạn trước khi viết code.

### 3. Các Hạng mục Kỹ thuật Cần Xây dựng & Nghiệm thu (Hạng mục 2 → 5)

#### Hạng mục 2: Core `EagleLiteratureEngine` & Giao diện Trình chiếu Dual-Mode (`eagle_literature_engine.py` + Lua HUD riêng)
- **Tối ưu chống xung đột file dùng chung**: Viết toàn bộ logic vào module riêng `eagle_literature_engine.py` và script vẽ HUD riêng `cleo\EagleLiteratureHud.lua` (hoặc hook mỏng tối thiểu vào `EagleCompanion.py` / `hud.lua` dưới `game-write.lock` sau khi đọc bản mới nhất trên đĩa).
- **Double-Buffer CG Loader (`models\txd\LITCG0.TXD` & `LITCG1.TXD`)**: Nạp mượt không khựng hình các bức CG `16:9` từ gói nội dung, khóa cứng tỷ lệ hiển thị `16:9` (tuyệt đối không kéo bẹt ảnh trên màn hình `1920×1080`).
- **Chế độ `adv_cinema` (Xem phim tại Rạp)**:
  - Khung hình điện ảnh `16:9` sắc nét + dải phụ đề kính mờ dưới đáy cỡ chữ lớn dễ đọc chuẩn `1920×1080` + thẻ tên nhân vật theo `nameplate_color_rgb`.
  - Điều khiển: Bấm tiếp (`Space` / `Enter` / `LMB`), **Auto-Play `[A]`** (có 3 tốc độ Chậm / Vừa / Nhanh, tự cộng thời gian theo số từ của beat), ẩn UI ngắm CG `[H]`, mở Backlog `[B]`, đổi nhanh sang chế độ sách `[V]` (nếu gói hỗ trợ cả 2 mode), thoát `[Backspace]` / `[Esc]`. Không có lựa chọn rẽ nhánh, không voice nhân vật.
- **Chế độ `nvl_book` (Đọc Light Novel tại Thư viện / Tủ sách `EaglePhone`)**:
  - Giao diện đọc sách nền tối dịu mắt (khung CG minh họa `16:9` tự động cập nhật theo đoạn + trang văn bản nhiều đoạn rõ nét), cuộn trang mượt bằng con lăn chuột (`0x00CAFE78`) / phím lên xuống / nút cảm ứng, mục lục nhảy chương, và **tự động lưu `bookmark` tới đúng `chapter_id` + `block_id`/`beat_id` đang đọc dở** vào `data\project-eagle\literature\eagle_lit_save.json`.
- **Âm thanh Nhạc nền (`alias lit_bgm`)**: Phát nhạc nền instrumental từ `bgm/` của gói qua Win32 MCI độc lập với `wl_bgm`/`sq_bgm`/Radio xe hơi, tự động lặp mượt khi hết bài, tự động tạm dừng khi vào Pause Menu (`0x00BA67A4`), và dùng `GTAPerProcessAudioMuter` mute tiếng ồn GTA khi đang mở HUD trình chiếu (bắt buộc khôi phục âm thanh 100% trong `finally:` / khi đóng HUD).

#### Hạng mục 3 & 4: 4 Nội Thất 3D (`Area Code = 1`), 30 Công Trình Thế Giới, Lịch Chiếu & Kệ Sách
- **4 Tổ hợp Nội thất 3D (`Z = +1650.0m`, `Area Code = 1`, IDs `15140..15219`)**:
  - Dựng bằng Blender 5.0 (`.DFF` prelight dịu mắt + `.TXD` + `.COL3` chuẩn không lọt sàn, trần/tường kín):
    1. `INT-CIN-GRAND` `(2700, -1650, 1650)`: Sảnh lớn (Quầy vé Box Office, Quầy Bắp & Nước, 5 khung Poster tuần phát sáng, bàn chờ Lounge) nối thông bằng hành lang/cửa sang Phòng chiếu IMAX bậc thang `60` ghế + màn bạc lớn + `6` cặp ghế đôi Waifu + cửa `EXIT` xanh.
    2. `INT-CIN-SMALL` `(3150, -1650, 1650)`: Sảnh gỗ/Art-Deco ấm cúng (Quầy vé kiêm bắp nước, 2 khung Poster) + Phòng chiếu Boutique `24` ghế + `4` cặp ghế đôi + cửa `EXIT`.
    3. `INT-LIB-GRAND` `(2700, -2150, 1650)`: Đại thư viện 2 tầng vòm cao (Quầy thủ thư thuê/mua sách, dãy kệ cao, tầng lửng, `24` bàn đèn đọc sách + `6` bàn đôi).
    4. `INT-LIB-SMALL` `(3150, -2150, 1650)`: Nhà sách & Book-Cafe gỗ ấm (Quầy thu ngân/cà phê, kệ sách chủ đề, `10` bàn đọc + `3` bàn đôi cạnh cửa sổ).
- **Luồng Trạng thái Thực tế (BẮT BUỘC ĐÚNG 100% YÊU CẦU NGƯỜI DÙNG)**:
  - **Rạp phim**: Ngoài đường bấm `[E]` vào **Sảnh rạp** -> Mua vé chọn phim (Đại Rạp chiếu `4–5` phim/tuần vé `$25`, Rạp Nhỏ chiếu `2` phim/tuần vé `$10–$12`; mỗi phim có `5` suất/ngày `09:00, 13:00, 17:00, 20:30, 23:30`, cho phép vào sớm/trễ linh hoạt **`±60` phút giờ game**, nếu lỡ quá xa cho đổi miễn phí sang suất kế tiếp; có mua thêm Bắp + Nước) -> Đi tới cửa **Phòng chiếu** bấm `[E]` bước vào trong phòng chiếu -> Đi bộ tới đúng ghế ngồi bấm `[E]` để bắt đầu xem phim (mở HUD `adv_cinema`) -> **Khi xem hết phim HOẶC bấm thoát giữa chừng: chỉ tắt HUD, nhân vật Aether VẪN Ở TRONG PHÒNG CHIẾU 3D** -> Phải tự đi bộ ra cửa `EXIT` của phòng chiếu để trở ra **Sảnh rạp** -> Đi bộ từ Sảnh rạp ra cửa chính để về lại đúng tọa độ ngoài đường của thành phố/quốc lộ lúc vào.
  - **Thư viện / Nhà sách**: Ngoài đường `[E]` vào **Thư viện** -> Tới quầy thuê sách đọc tại chỗ (`$4–$8` trong 7 ngày game) hoặc mua sở hữu vĩnh viễn (`$20–$60`, lưu vào tủ sách cá nhân đọc được cả trên `EaglePhone`) -> Đi bộ tìm **Bàn đọc sách** bấm `[E]` ngồi xuống mở HUD `nvl_book` -> Đóng HUD vẫn đứng cạnh bàn trong Thư viện -> Đi bộ ra cửa chính về lại ngoài đường.
- **Triển khai 30 Địa điểm Ngoài Thế giới (`CUSTOM\cinema_library_world.{ide,ipl,col,img}`, IDs `15110..15139`)**:
  - Đặt chính xác `10` Tòa Nhà 3D Mới trên đất trống theo `venues_30_verified.json` — **bắt buộc tính cao độ theo đáy mesh thực tế `Z_IPL = Z_ground - min_z - 0.05` và chạy gộp vật liệu `numMaterials <= 136`**, không dùng backdrop rỗng.
  - Đặt bảng hiệu / hộp đèn Poster tuần trước cửa `20` công trình điểm nhấn có sẵn (nếu retexture biển hiệu gốc thì đặt trong `modloader\EagleLiteratureSignage\` tách biệt 100% với archive `S&S` gốc để rollback 1 chạm).
  - Đăng ký NPC nhân viên bán vé, bắp nước, thủ thư, độc giả (`Ped IDs 49466..49485` chọn từ các skin `normal` sạch chưa gán trong `D:\GTA Archive\Skin Library`) spawn động bên trong nội thất.

#### Hạng mục 5: Đấu nối Hệ sinh thái, Chừa Mấu nối Waifu & Nghiệm thu Kép
- Đăng ký đủ `30` địa điểm (tên, phân hạng, vùng, tọa độ cửa & `dropoff_pos`) vào **`GG Map`** (`eagle_gg_map_pois.py`) và **`EagleRide v2.0`** (`eagle_ride_engine.py`) để người chơi tìm kiếm và đặt xe công nghệ chở tới tận cửa.
- Giữ nguyên cấu trúc dữ liệu `waifu_hooks` (`dropoff_coords`, `couple_seat_pool`, `post_date_lobby_chat_anchor`) trong metadata địa điểm & nội thất để sau này nối tính năng dắt Waifu đi xem phim không phải sửa 3D.
- Tạo 1 gói dữ liệu kiểm thử nội bộ siêu nhẹ (`data\project-eagle\literature\packs\_smoke_test_demo\`, 1 chương ngắn 6 beats + 2 ảnh test phẳng/sạch tạo bằng Python Pillow không tốn quota AI + 1 file âm thanh MCI sạch) để test trọn vòng mua vé -> vào phòng chiếu -> xem HUD -> thoát ra sảnh -> ra đường và thuê sách -> ngồi bàn đọc -> lưu bookmark.

### 4. Kỷ luật Phối hợp, Khóa Kép & Bàn giao cho Orchestrator
- Dùng staging riêng tại `D:\GTA Archive\Staging\project-eagle\cinema-library-builder-20261106\`.
- Mọi thao tác sửa file runtime/archive dùng chung phải giữ khóa `EagleCoordLock("game-write", ...)` trong thời gian ngắn nhất, kiểm tra hash trước/sau và tạo script rollback có guard (`rollback_cinema_library_infra.py`).
- Mọi phiên bật `gta_pe.exe` + `EagleCompanion.py` để test **Part B (DirectX 9 `1920×1080`)** phải nằm trong `EagleCoordLock("ingame-runtime", ...)` và dọn sạch tiến trình trong `finally:`.
- Chụp bộ ảnh nghiệm thu DirectX 9 thực tế (bên ngoài tòa nhà 3D mới ở miền Trung & thành phố, sảnh rạp, mua vé/bắp nước, phòng chiếu ghế ngồi, HUD `adv_cinema`, thư viện, bàn đọc HUD `nvl_book`, thoát ra sảnh & ra đường), kiểm tra bằng mắt thật từng ảnh (`read_file`), xác nhận `EagleLuaErrors.log = 0` và `eagle_doctor 11/11 PASS`.
- Khi hoàn tất, cập nhật phiếu `docs\project-eagle\work-items\` sang trạng thái `done` và viết báo cáo bàn giao chi tiết tại `docs\project-eagle\cinema-library-infrastructure-handover-2026-11-06.md` (ghi rõ schema `schedule_and_catalog.json`, đường dẫn thả pack và lệnh kiểm tra) để **Orchestrator (`199f0287-723d-43b5-a013-d519137afba4`)** review và cho Hội thoại Integrator nạp phim/sách thật.
```
