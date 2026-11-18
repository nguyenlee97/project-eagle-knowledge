# Báo Cáo Hoàn Tất Tích Hợp Runtime & Nghiệm Thu Thực Tế In-Game DirectX 9 Cho Furina de Fontaine (`char_id = "furina"`, `ped_id = 49428`)

- **Ngày thực hiện**: `2026-11-04` (`Asia/Saigon`)
- **Agent / Hội thoại**: Antigravity (`469110bc-c460-48bf-87d4-02b11f2bca81`)
- **Phiếu công việc**: [`work-items/2026-11-04-antigravity-furina-ingame-integration-and-qa.md`](work-items/2026-11-04-antigravity-furina-ingame-integration-and-qa.md)
- **Target game**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & QA**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-furina-qa-20261104\`
- **Kết quả tổng thể**: **100% PASS** (`Part A 79/79 assertions + 135/135 unique CGs`, `Part B 12/12 ảnh DirectX 9 1920×1080 kiểm tra bằng mắt thật`, `EagleLuaErrors.log = 0`, `eagle_doctor.py = 11/11 PASS`, đã dọn sạch DB runtime & giải phóng mọi khóa).

---

## 1. Các Hạng Mục Đã Rà Soát & Khắc Phục Cho Furina

### 1.1. Tọa Độ Thực Địa `home_coords`, `date_spots` & Xe Mui Trần `575 Broadway` (`eagle_dating_sim.py`)
- **Tinh chỉnh `home_coords` & `date_spots` chuẩn địa hình Los Santos**:
  - Chuyển `home_coords` của Furina về **Richman Chateau Estate, Los Santos (`[720.00, -1314.50, 13.55]`)** — mặt tiền dinh thự sang trọng dọc đại lộ Vinewood/Richman phẳng rộng, `0` con quay EHI gây nhiễu, spawn **3D Furina (`ped_id = 49428`, `wl_furina`)** đứng đón tự nhiên tại `(721.20, -1315.70, 13.58)` với `2000.0 / 2000.0 HP` và `proof_flags = 0xBC (188)`.
  - Thiết lập bộ **3 `date_spots`** chuẩn phong cách ngôi sao nhạc kịch Fontaine tại Los Santos, cách nhà từ `455m – 799m` trên mặt đường nhựa rộng phẳng:
    1. `furina_patisserie` — **Rodeo Patisserie Boulevard**: `[275.00, -1410.00, 13.45]` (`455.1m` từ nhà).
    2. `furina_promenade` — **Verona Beach Ocean Promenade**: `[834.00, -1783.00, 13.45]` (`482.2m` từ nhà).
    3. `furina_beach` — **Santa Maria Sunset Pier**: `[373.20, -2034.00, 7.83]` (`798.7m` từ nhà).
- **Màu sơn riêng cho xe mui trần `575 Broadway`, Thoại Chấm Điểm Chuyến Đi & Mở Rộng Dòng Suy Nghĩ VN Footer**:
  - Trong `start_freeroam_outing` (`eagle_dating_sim.py` dòng `2794`), cấu hình `date_colors["furina"] = (79, 1)` (**Hydro Royal Blue & Pearl White**) trên xe mui trần không tựa đầu **`575 Broadway`**.
  - Trong `complete_freeroam_outing` (`eagle_dating_sim.py` dòng `2900–2935`), bổ sung đầy đủ lời thoại, cử chỉ giữ mũ chóp vương miện và dòng suy nghĩ `Salon Solitaire's Whisper` riêng cho Furina ở cả 5 trường hợp (`S-Rank`, `A-Rank`, va chạm `FAIL`, sơ tán khỏi xe cháy `vehicle_burning_waifu_rescued`, và người chơi `player_wasted`), tách biệt hoàn toàn khỏi câu thoại `"Wangsheng Parlor"` của Hu Tao.
  - Trong `build_hud_kv` (`eagle_dating_sim.py` dòng `4293–4329`), tự động gắn nhãn `Salon Solitaire's Whisper:` cho các kịch bản AI Encore của Furina và mở rộng độ dài dòng `wl_vn_thought` từ `raw_th[:132]` lên `textwrap.shorten(raw_th, width=196, placeholder="...")` (cùng `width=116` cho `wl_vn_c1..c3`) để hiển thị trọn vẹn 100% câu suy nghĩ nội tâm dài nhất (`189` ký tự) trong khung kính mờ `1850px` của `hud.lua` không bị cắt lửng.

### 1.2. Làm Sạch Ký Tự RenderWare `CFont` & Chuẩn Hóa `mood` (`eagle_waifulink_v4_furina.py`)
- Quét toàn bộ `15` Milestones (`FURINA_15_MILESTONES`), `30` Scenarios (`120` scenes trong `FURINA_20_SCENARIOS` + `FURINA_10_EXTRA_CAMEO_SCENARIOS`) và `FURINA_STAGE_CHAT_STARTERS` bằng `staging/project-eagle/waifulink-furina-qa-20261104/sanitize_furina_module.py`:
  - Loại bỏ triệt để các ký tự `~`, `|`, `*` gây lỗi mã màu/token trên `CFont` DirectX 9 và chuẩn hóa dấu gạch ngang sang ASCII an toàn.
  - Chuẩn hóa toàn bộ trường `mood` về `1–2` từ viết hoa chữ cái đầu (`<= 16` ký tự) và đảm bảo toàn bộ câu gợi ý Quick-Chat `[1]/[2]/[3]` cùng `proactive_action_cue` hiển thị trọn vẹn trên App 13 không bị cắt cụt.
- Giữ nguyên 100% `ped_id = 49428` (`wl_furina` trong `CUSTOM/custom_mods.img` + `data/peds.ide`), mascot `ep_ms_furina` trong `models/hud.txd`, `COMPONENTPEDS.img` (`190..195` HSR/ZZZ), gói Presentation `03/11` và các tích hợp song song (Citlali, Columbina, JP Voicelines).

---

## 2. Manifest Tệp Đã Thay Đổi, Hash SHA-256 & Lệnh Phục Hồi Có Guard

| Tệp | Trạng thái | Kích thước | SHA-256 Trước | SHA-256 Sau |
| :--- | :--- | ---: | :--- | :--- |
| `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_furina.py` | Đã cập nhật | `456,927 B` | `c017922a521d19c5dd9d2b348bf8a52b1511a0c4ba05a89d03988ec25465dcb8` | `81c0ddc36d4c982b385228d56841d64f1c7c530b1d606bad36b6a5496cf2671b` |
| `Project Eagle/gta sa gameplay-lab/eagle_dating_sim.py` | Đã cập nhật *(dưới `game-write.lock`, hợp nhất cùng các hội thoại song song)* | `248,923 B` | `43860add215c0ca3dcea86ed05c1b6dfbc447f38424783c38ffb3ec7ea05a595` | `3bbac7436487e4ae41920aec82d426c83ff5f491d63be7d0a55eaf1e3e0053e9` |
| `Project Eagle/gta sa gameplay-lab/CUSTOM/custom_mods.img` | Giữ nguyên (`wl_furina`) | `152,598,528 B` | `f5130730b6276d72404b382126458e06bb8704932b11c734870bc1d843aa3c9d` | `f5130730b6276d72404b382126458e06bb8704932b11c734870bc1d843aa3c9d` |
| `Project Eagle/gta sa gameplay-lab/data/peds.ide` | Giữ nguyên (`49428`) | `218,705 B` | `d0c6891d8b00a832756e58d4d863c2bd61a99a4dc6aeab15e8eb95215edcc46e` | `d0c6891d8b00a832756e58d4d863c2bd61a99a4dc6aeab15e8eb95215edcc46e` |
| `Project Eagle/gta sa gameplay-lab/models/hud.txd` | Giữ nguyên (`ep_ms_furina`) | `4,478,160 B` | `1fd202b0f7fa35b3ed01733bd6fe1a4a62d4256346d5c2e1744151589c13b84a` | `1fd202b0f7fa35b3ed01733bd6fe1a4a62d4256346d5c2e1744151589c13b84a` |

### Backup & Phục Hồi Có Guard (Bảo Toàn Feature Của Agent Khác)
- Bản sao lưu trước khi sửa nằm tại `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-furina-qa-20261104\backups\`:
  - `eagle_waifulink_v4_furina.py.bak` (`c017922a...`)
  - `eagle_dating_sim.py.bak` (`43860add...`)
- **Lưu ý quan trọng khi rollback**: Do `eagle_dating_sim.py` dùng chung với các hội thoại song song (Citlali, Columbina, JP Voicelines), **không chép đè nguyên file `eagle_dating_sim.py.bak`** nếu hash đã tiến thêm; chỉ khôi phục file riêng `eagle_waifulink_v4_furina.py` bằng guard hash dưới khóa `game-write.lock`:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py" acquire game-write --chat "rollback-furina" --task "Restore Furina module" --wait 600
  $target = "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_furina.py"
  $bak = "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-furina-qa-20261104\backups\eagle_waifulink_v4_furina.py.bak"
  if ((Get-FileHash $target -Algorithm SHA256).Hash.ToLower() -eq "81c0ddc36d4c982b385228d56841d64f1c7c530b1d606bad36b6a5496cf2671b") {
      Copy-Item $bak $target -Force
  } else { throw "Hash mismatch on eagle_waifulink_v4_furina.py — aborting rollback" }
  python "C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py" release game-write --chat "rollback-furina"
  ```

---

## 3. Kết Quả Kiểm Thử Hai Tầng (Part A Offline + Part B Live DirectX 9)

### 3.1. Part A — Deterministic & Live-AI Engine E2E (`run_furina_part_a_e2e.py`, 100% Ngoài Khóa)
- Chạy độc lập trên SQLite tạm `staging/project-eagle/waifulink-furina-qa-20261104/part_a_furina.db` sau chỉnh sửa cuối cùng của `eagle_dating_sim.py` -> **`79/79` assertions PASS (`100% GREEN`)** ([`furina_part_a_report.json`](../../staging/project-eagle/waifulink-furina-qa-20261104/furina_part_a_report.json)):
  - **Media & PIL Decode Audit**: Xác thực đủ `135/135` tệp `.jpg` (`furina_m01..m15.jpg`, `furina_s1_sc1_cg1..s5_sc4_cg4.jpg`, `furina_s1_ex1_cg1..s5_ex2_cg4.jpg`) đọc mở hợp lệ qua Pillow, không lỗi header, bảo toàn hồi quy `30` kịch bản của Hu Tao & Citlali.
  - **Ambient Doorstep & Selector**: Kiểm chứng đóng/mở banner `wl_house_near` ở `40m -> 5.5m -> Backspace -> 29m walk-away` trước Richman Chateau Estate cùng preview `furina_m01.jpg`.
  - **Live `gpt-6-luna` Multi-Turn Memory & Economy Caps**: Chat trực tiếp với `gpt-6-luna` trích xuất đúng L3 Fact Memory vào SQLite (*Pour la Justice cake / macarons & black tea*), trần Chat `45/stage`, trần Free-Roam `75/stage`, giữ ảnh `furina_m03` khi đang đi chung và tự bắn banner `WAIFULINK PHOTO: FURINA` sau `11.5s` rời xa, kẹp cổng `Stage 1 Gate` ở `199` trước khi hoàn thành `3/3` kịch bản VN, mở khóa `Stage 2 (234 -> 269 Carryover -> 304 Dynamic AI Encore)`.

### 3.2. Part B — Live DirectX 9 In-Game E2E (`run_furina_part_b_live_d3d9.py`, Dưới `ingame-runtime.lock`)
- Chạy trực tiếp trong `gta_pe.exe` (`1920×1080` DirectX 9) + `EagleCompanion.py` (`:8765`), đã đọc kiểm tra trực quan bằng mắt thật (`read_file`) toàn bộ **12 ảnh chụp PNG** trong `staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/` ([`furina_part_b_d3d9_report.json`](../../staging/project-eagle/waifulink-furina-qa-20261104/furina_part_b_d3d9_report.json) `all_passed: true`):
  1. **[`furina_01a_app13_f6_typing.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_01a_app13_f6_typing.png)** & **[`furina_01_app13_live_ai_chat.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_01_app13_live_ai_chat.png)**: Mở EaglePhone App 13 (`WAIFULINK v4.0: Furina`), hiển thị đúng avatar `ep_ms_furina`, thanh gõ phím trực tiếp `[F6]` (`strawberry macarons and tea`) và phản hồi live từ `gpt-6-luna` (`80 -> 86 -> 92/1000`) cùng 3 gợi ý Quick-Chat hiển thị sắc nét không cắt chữ.
  2. **[`furina_02a_doorstep_3d_ambient.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_02a_doorstep_3d_ambient.png)** & **[`furina_02_doorstep_3d_and_selector.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_02_doorstep_3d_and_selector.png)**: Tới trước thềm dinh thự Richman Chateau LS (`5m`) thấy rõ **3D Furina (`ped_id = 49428`, `wl_furina`, `2000.0 HP`)** đội mũ chóp vương miện Hydro đứng đón + banner `[HOUSE VISIT] Near Furina's Home (5m) - Press [F9] Event Selector`; bấm `[F9]` hiện bảng chọn 5 sự kiện kèm ảnh preview `furina_m01.jpg`.
  3. **[`furina_03_vn_fullscreen_scene1.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_03_vn_fullscreen_scene1.png)** & **[`furina_03_vn_fullscreen_scene4.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_03_vn_fullscreen_scene4.png)**: Trình chiếu Fullscreen `16:9` Visual Novel (`WLCG0/1.TXD`) cho `furina_s1_sc1` (*The Last 'Pour la Justice' Opera Cake*) từ `1/4 OPENING CG` tới `4/4 COUPLE ENDING`, khung kính mờ đáy màn hình hiển thị trọn vẹn dòng `(Salon Solitaire's Whisper: ...)`, nhận `+35 Affection` (`127/1000`, `Stage Gate: 1/3`) và đếm ngược tự đóng sau `4.5s`.
  4. **[`furina_04_vn_cameo_fontaine.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_04_vn_cameo_fontaine.png)**: Trình chiếu Fullscreen `16:9` kịch bản khách mời Fontaine (`furina_s1_ex1` — có mặt Iudex Neuvillette cùng Aether và Furina), dòng suy nghĩ nội tâm `Salon Solitaire's Whisper` hiển thị nguyên vẹn 100% không cắt chữ.
  5. **[`furina_05_freeroam_3d_broadway_rear.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_05_freeroam_3d_broadway_rear.png)**, **[`furina_05_freeroam_3d_broadway_front.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_05_freeroam_3d_broadway_front.png)** & **[`furina_05c_time_apart_m02_banner.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_05c_time_apart_m02_banner.png)**: Chở **3D Furina** ngồi ghế phụ xe mui trần **`575 Broadway` màu Xanh Hoàng Gia & Trắng Ngọc Trai (`[79, 1]`)** trên đường băng nhựa vạch sơn trắng LSIA, thấy rõ mũ vương miện Hydro của Furina ở cả góc đuổi sau và góc kính chắn gió trước (`Q+E`), chấm điểm từ `S-RANK (+25)` sang `A-RANK (+20)` (`147/1000`), và tự động bắn banner **`WAIFULINK PHOTO: FURINA` (`furina_m02.jpg`)** khi rời xa.
  6. **[`furina_06_burning_car_rescued_2000hp.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_06_burning_car_rescued_2000hp.png)** & **[`furina_06_wasted_immortal_2000hp.png`](../../staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/furina_06_wasted_immortal_2000hp.png)**: Khi capo xe `575 Broadway` bốc cháy dữ dội (`< 250 HP`), `EagleWaifuBridge.cs` lập tức sơ tán 3D Furina ra đứng an toàn bên phải tiền cảnh kèm banner `[ALERT] FURINA SAFE (2000 HP)` (`rescue_count = 1`, `live_hp = 2000.0`); khi xe nổ tung (`0 HP`) và người chơi bị **`Wasted` (`player_wasted_hp = 0.0`)**, **3D Furina vẫn sống sót nguyên vẹn 100% ở `2000.0 / 2000.0 HP`** (`rescue_count = 2`, `waifu_alive = true`).

### 3.3. Sức Khỏe Hệ Thống & Trạng Thái Sau Nghiệm Thu
- `cleo/EagleLuaErrors.log`: **Không phát sinh lỗi Lua** (`0` runtime errors).
- `eagle_doctor.py`: **`11/11 PASS, 0 WARN, 0 FAIL`** (`0` crash mới trong `ProjectEagle_crashes/`).
- Dọn dẹp sau test: Đã tắt sạch `gta_pe.exe` + `EagleCompanion.py`, xóa DB test tạm để trả `data/eagle_companion.db` về sạch, reset `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0, wl_vn_active=0, wl_house_menu=0, wl_house_near=0`), và giải phóng hoàn toàn cả hai khóa `game-write.lock` & `ingame-runtime.lock`.
