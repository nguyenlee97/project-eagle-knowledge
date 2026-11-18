# Báo Cáo Hoàn Tất Tích Hợp Runtime & Nghiệm Thu Thực Tế In-Game DirectX 9 Cho Citlali (`char_id = "citlali"`, `ped_id = 49430`)

- **Ngày thực hiện**: `2026-11-04` (`Asia/Saigon`)
- **Agent / Hội thoại**: Antigravity (`493148af-f0f7-4d9f-9ec8-bf377df747df`)
- **Phiếu công việc**: [`work-items/2026-11-04-antigravity-citlali-ingame-integration-and-qa.md`](work-items/2026-11-04-antigravity-citlali-ingame-integration-and-qa.md)
- **Target game**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & QA**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-citlali-qa-20261104\`
- **Kết quả tổng thể**: **100% PASS** (`Part A 35/35 assertions + 135/135 unique CGs`, `Part B 6/6 nhóm ảnh DirectX 9 1920×1080`, `EagleLuaErrors.log = 0 bytes`, `eagle_doctor.py = 11/11 PASS`, đã dọn sạch DB runtime & giải phóng mọi khóa).

---

## 1. Các Hạng Mục Đã Rà Soát & Khắc Phục Cho Citlali

### 1.1. Tọa Độ Thực Địa `home_coords`, `date_spots` & Xe Mui Trần `575 Broadway` (`eagle_dating_sim.py`)
- **Sửa lỗi `home_coords` & `date_spots[0]` trùng `0.0m` ở hẻm hẹp Ganton**:
  - Trước khi sửa, `citlali` đặt `home_coords = [2401.96, -1723.22, 12.60]` ngay sát con quay EHI cửa nhà Denise gốc ở Ganton (hẻm cụt chật hẹp dễ kẹt xe mui trần `575 Broadway`) và `date_spots[0]` trùng khít `0.0m` với `home_coords` (vi phạm khoảng cách tối thiểu `> 80m` của Free-Roam Outing).
  - Đã chuyển `home_coords` sang **Citlali's Night-Wind Sanctuary, Verona Beach LS (`[814.50, -1769.00, 13.40]`)** — mặt tiền biệt thự biển màu hồng pastel ở Verona Beach có đại lộ nhựa 4 làn phẳng rộng ngay trước thềm, `0` marker EHI gây nhiễu, spawn **3D Citlali (`ped_id = 49430`, `wl_citlali`)** đứng đón tự nhiên tại `(815.70, -1770.20, 14.06)`.
  - Thiết lập mới bộ **3 `date_spots`** chuẩn tính cách Bà Ngoại Itztli cách nhà từ `510m – 1,170m` trên đường nhựa rộng phẳng ở Los Santos:
    1. `citlali_pier` — **Santa Maria Stargazing Pier**: `[369.60, -2028.50, 7.83]` (`~514m` từ nhà; cao độ mặt sàn gỗ cầu cảng `law_pier` thực tế `z = 7.83m`).
    2. `citlali_observatory` — **Verdant Bluffs Star Observatory**: `[1252.40, -2036.80, 59.80]` (`~514m` từ nhà).
    3. `citlali_glenpark` — **Glen Park Mystic Pond Boulevard**: `[1898.00, -1340.00, 13.54]` (`~1,165m` từ nhà).
- **Màu sơn riêng cho xe mui trần không tựa đầu `575 Broadway` & Thoại Chấm Điểm Chuyến Đi**:
  - Trong `start_freeroam_outing` (`eagle_dating_sim.py` dòng `2795`), cấu hình `date_colors["citlali"] = (126, 93)` (**Pastel Pink-Lavender & Night-Wind Turquoise**).
  - Trong `complete_freeroam_outing` (`eagle_dating_sim.py` dòng `2864–2900`), bổ sung đầy đủ lời thoại, cử chỉ ôm gối `Itzpapa`/`Citlalin` và dòng suy nghĩ `🔮 Obsidian Mirror's Telepathy` riêng cho Citlali ở mọi trường hợp (`S-Rank`, `A-Rank`, va chạm `FAIL`, sơ tán khỏi xe cháy `vehicle_burning_waifu_rescued`, và người chơi `player_wasted`), tách biệt hoàn toàn khỏi thoại của Hu Tao.
  - Chuẩn hóa hiển thị nhãn `Obsidian Mirror's Telepathy:` trong khung thoại kính mờ VN footer (`eagle_dating_sim.py` dòng `4289–4311`).

### 1.2. Làm Sạch Ký Tự RenderWare `CFont` & Độ Dài `mood` (`eagle_waifulink_v4_citlali.py`)
- Quét toàn bộ `15` Milestones (`CITLALI_15_MILESTONES`), `30` Scenarios (`120` scenes trong `CITLALI_20_SCENARIOS` + `CITLALI_10_EXTRA_CAMEO_SCENARIOS`) và `CITLALI_STAGE_CHAT_STARTERS` bằng `staging/project-eagle/waifulink-citlali-qa-20261104/sanitize_citlali_module.py`:
  - Loại bỏ toàn bộ các ký tự `~`, `|`, `*` gây lỗi mã điều khiển màu/phím trên `CFont` DirectX 9.
  - Rút gọn toàn bộ trường `mood` về chuẩn `1–2` từ viết hoa chữ cái đầu (`<= 16` ký tự) và đảm bảo các câu gợi ý Quick-Chat `[1]/[2]/[3]` hiển thị trọn vẹn trong App 13 không bị cắt cụt vô nghĩa.
- Bảo toàn tuyệt đối `ped_id = 49430` (`wl_citlali` trong `CUSTOM/custom_mods.img` + `data/peds.ide`), mascot `ep_ms_citlali` trong `models/hud.txd`, `COMPONENTPEDS.img` (`190..195` HSR/ZZZ), gói Presentation `03/11` và phần tích hợp JP Voicelines vừa được hội thoại bên cạnh bổ sung vào `EagleCompanion.py` / `eagle_dating_sim.py`.

---

## 2. Manifest Tệp Đã Thay Đổi, Hash SHA-256 & Lệnh Phục Hồi Có Guard

| Tệp | Trạng thái | Kích thước | SHA-256 Trước | SHA-256 Sau |
| :--- | :--- | ---: | :--- | :--- |
| `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_citlali.py` | Đã cập nhật | `212,947 B` | `c2be68da835beffb2d8f6b80fd20426639c43066ae6bc38bda4a37ecd1d2ee3a` | `98721c591c0e9f636a337c76d986106a4b86c8ac49895ef67e8f5c77c0414616` |
| `Project Eagle/gta sa gameplay-lab/eagle_dating_sim.py` | Đã cập nhật *(cùng các hội thoại song song dưới `game-write.lock`)* | `248,359 B` | `c85a6f4299d2871707f9534d58187b64a08001e38732b1225b2c31e9a7bd4173` | `900f7dacf1432b2754761a115d358135d72a989307a5fd0b8db47642b8b54de8` |
| `Project Eagle/gta sa gameplay-lab/CUSTOM/custom_mods.img` | Giữ nguyên (`wl_citlali`) | `152,598,528 B` | `f5130730b6276d72404b382126458e06bb8704932b11c734870bc1d843aa3c9d` | `f5130730b6276d72404b382126458e06bb8704932b11c734870bc1d843aa3c9d` |
| `Project Eagle/gta sa gameplay-lab/data/peds.ide` | Giữ nguyên (`49430`) | `218,705 B` | `d0c6891d8b00a832756e58d4d863c2bd61a99a4dc6aeab15e8eb95215edcc46e` | `d0c6891d8b00a832756e58d4d863c2bd61a99a4dc6aeab15e8eb95215edcc46e` |
| `Project Eagle/gta sa gameplay-lab/models/hud.txd` | Giữ nguyên (`ep_ms_citlali`) | `4,478,160 B` | `1fd202b0f7fa35b3ed01733bd6fe1a4a62d4256346d5c2e1744151589c13b84a` | `1fd202b0f7fa35b3ed01733bd6fe1a4a62d4256346d5c2e1744151589c13b84a` |

### Backup & Phục Hồi Có Guard (Bảo Toàn Feature Của Agent Khác)
- Bản sao lưu trước khi sửa nằm tại `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-citlali-qa-20261104\backups\`:
  - `eagle_waifulink_v4_citlali.py.bak` (`c2be68da...`)
  - `eagle_dating_sim.py.pre_citlali.bak` (`c85a6f42...`)
- **Lưu ý quan trọng khi rollback**: Do `eagle_dating_sim.py` sau thời điểm backup còn nhận thêm cập nhật từ các hội thoại song song (JP Voicelines `9999181a`, Furina, Columbina), **không chép đè nguyên file `eagle_dating_sim.py.pre_citlali.bak`** nếu hash hiện tại khác; chỉ khôi phục file riêng `eagle_waifulink_v4_citlali.py` bằng guard hash dưới khóa `game-write.lock`:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py" acquire game-write --chat "rollback-citlali" --task "Restore Citlali module" --wait 600
  $target = "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_citlali.py"
  $bak = "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-citlali-qa-20261104\backups\eagle_waifulink_v4_citlali.py.bak"
  if ((Get-FileHash $target -Algorithm SHA256).Hash.ToLower() -eq "98721c591c0e9f636a337c76d986106a4b86c8ac49895ef67e8f5c77c0414616") {
      Copy-Item $bak $target -Force
  } else { throw "Hash mismatch on eagle_waifulink_v4_citlali.py — aborting rollback" }
  python "C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py" release game-write --chat "rollback-citlali"
  ```

---

## 3. Kết Quả Kiểm Thử Hai Tầng (Part A Offline + Part B Live DirectX 9)

### 3.1. Part A — Deterministic & Live-AI Engine E2E (`run_citlali_engine_e2e.py`, 100% Ngoài Khóa)
- Chạy độc lập trên SQLite tạm `staging/project-eagle/waifulink-citlali-qa-20261104/part_a_citlali.db` -> **`35/35` assertions PASS** (`part_a_results.json`):
  - **Media & SHA-256 Audit**: Đủ `135/135` tệp `.jpg` (`citlali_m01..m15.jpg`, `citlali_s1_sc1_cg1..s5_sc4_cg4.jpg`, `citlali_s1_ex1_cg1..s5_ex2_cg4.jpg`) tồn tại tại `data/project-eagle/dating-sim/media/`, `135` mã SHA-256 hoàn toàn duy nhất (`0%` trùng lặp).
  - **CFont Text Hygiene**: `0` ký tự cấm (`~`, `|`, `*` lỗi token), toàn bộ `mood <= 16` ký tự.
  - **3-Pillar Stage Economy & Carryover**: Khởi tạo mở sẵn `citlali_m01` + 3 `reaction_choices`; trần Chat `45/stage`, trần Free-Roam Outing `75/stage`, cổng `Stage Gate` kẹp đúng ở `199` khi chưa đủ `3/4` Core Scenarios và đột phá lên `Stage 2 (304/1000)` ngay khi hoàn thành kịch bản thứ 3; kịch bản Stage 1 chưa chơi vẫn mở được qua **Non-Hardlocked Stage Carryover** ở Stage 2; cơ chế **2-Strike Off-Topic Re-Ask + Anti-Stuck Bridge** và chat trực tiếp với **`gpt-6-luna` (OpenAI Live)** hoạt động chính xác 100%.

### 3.2. Part B — Live DirectX 9 In-Game E2E (`run_citlali_live_ingame_e2e.py`, Dưới `ingame-runtime.lock`)
- Chạy trực tiếp trong `gta_pe.exe` (`1920×1080` DirectX 9) + `EagleCompanion.py` (`:8765`), đã đọc kiểm tra trực quan bằng mắt thật (`read_file`) toàn bộ ảnh chụp trong `staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/` (`part_b_live_results.json` `all_passed: true`):
  1. **[`citlali_01_app13_live_ai_chat.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_01_app13_live_ai_chat.png)**: Mở EaglePhone App 13 (`WAIFULINK v4.0: Citlali`), hiển thị đúng avatar `ep_ms_citlali`, gõ `[F6]` chat trực tiếp với `gpt-6-luna` (`86/1000`) + bấm `[1]` Turn-2 (`92/1000`), lời thoại nhiều dòng và 3 câu gợi ý hiển thị đầy đủ không cắt chữ.
  2. **[`citlali_02_doorstep_3d_and_selector.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_02_doorstep_3d_and_selector.png)** *(kèm ảnh đơn [`citlali_02a_doorstep_3d_ambient.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_02a_doorstep_3d_ambient.png) & [`citlali_02b_selector_m01.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_02b_selector_m01.png))*: Tới trước cửa biệt thự Verona Beach LS (`6m`) thấy rõ **3D Citlali (`ped_id = 49430`, `wl_citlali`, `2000.0 HP`)** đứng đón + banner `[HOUSE VISIT] Near Citlali's Home (6m) - Press [F9] Event Selector`; bấm `[F9]` hiện bảng chọn 5 sự kiện kèm ảnh preview `citlali_m01.jpg`.
  3. **[`citlali_03_vn_fullscreen_scene1_and_4.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_03_vn_fullscreen_scene1_and_4.png)** *(kèm ảnh đơn [`citlali_03a_vn_fullscreen_scene1.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_03a_vn_fullscreen_scene1.png) & [`citlali_03b_vn_fullscreen_scene4.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_03b_vn_fullscreen_scene4.png))*: Trình chiếu Fullscreen `16:9` Visual Novel (`WLCG0/1.TXD`) cho `citlali_s1_sc1` (*Caught Reading Inazuman Romance Novels!*) ở `Scene 1/4` và `Scene 4/4` với khung thoại kính mờ đáy màn hình, `ep_ms_citlali`, dòng chữ tím `(Obsidian Mirror's Telepathy: ...)`, nhận `+35 Affection` (`127/1000`, `Stage Gate: 1/3`) và đếm ngược tự đóng sau `4.5s`.
  4. **[`citlali_04_vn_cameo_natlan.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_04_vn_cameo_natlan.png)**: Trình chiếu Fullscreen `16:9` kịch bản khách mời Natlan (`citlali_s1_ex2` — có mặt Kachina, Mualani, Kinich & Ajaw cùng Aether và Citlali).
  5. **[`citlali_05_freeroam_3d_broadway_rear_and_front.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_05_freeroam_3d_broadway_rear_and_front.png)** *(kèm ảnh đơn [`citlali_05a_freeroam_3d_broadway_rear.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_05a_freeroam_3d_broadway_rear.png), [`citlali_05b_freeroam_3d_broadway_front.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_05b_freeroam_3d_broadway_front.png), [`citlali_05c_time_apart_m02_drop.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_05c_time_apart_m02_drop.png))*: Chở **3D Citlali** ngồi ghế phụ xe mui trần không tựa đầu **`575 Broadway` màu hồng pastel - xanh ngọc (`[126, 93]`)**, thấy rõ Citlali ngồi cạnh người lái qua góc kính chắn gió trước (`Q+E`), chỉ đường GPS xanh lá (`503 m`) tới Santa Maria Stargazing Pier, hạ bậc từ `S-RANK (+25)` sang `A-RANK (+20)` khi va chạm nhẹ, cập bến cộng `+20` (`147/1000`), và tự động bắn thông báo ảnh kỷ niệm **`citlali_m02.jpg`** khi rời xa `> 38m`.
  6. **[`citlali_06_burning_car_and_wasted_immortal.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_06_burning_car_and_wasted_immortal.png)** *(kèm ảnh đơn [`citlali_06a_burning_car_rescued_2000hp.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_06a_burning_car_rescued_2000hp.png) & [`citlali_06b_wasted_immortal_2000hp.png`](../../staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/citlali_06b_wasted_immortal_2000hp.png))*: Khi xe `575 Broadway` bốc cháy (`< 250 HP`), `EagleWaifuBridge.cs` lập tức sơ tán 3D Citlali ra cách xa an toàn kèm banner `[ALERT] CITLALI SAFE (2000 HP)` (`rescue_count = 1`, `live_hp = 2000.0`); khi xe phát nổ (`0 HP`) và người chơi bị **`Wasted` (`player_hp = 0.0`)**, **3D Citlali vẫn sống sót nguyên vẹn 100% ở `2000.0 / 2000.0 HP`** (`rescue_count = 2`, `waifu_alive = true`).

### 3.3. Sức Khỏe Hệ Thống & Trạng Thái Sau Nghiệm Thu
- `cleo/EagleLuaErrors.log`: **`0` lỗi** (`0 bytes`).
- `eagle_doctor.py`: **`11/11 PASS, 0 WARN, 0 FAIL`** (`0` crash mới trong `ProjectEagle_crashes/`).
- Dọn dẹp sau test: Đã tắt sạch tiến trình test của phiên Citlali, khôi phục sạch `data/eagle_companion.db` & `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0`), và giải phóng hoàn toàn cả hai khóa `game-write.lock` & `ingame-runtime.lock` cho các hội thoại song song.
