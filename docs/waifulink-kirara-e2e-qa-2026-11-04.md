# Báo Cáo Triển Khai & Nghiệm Thu E2E In-Game DirectX 9 + JP Voice: Kirara (`char_id = "kirara"`, `ped_id = 49432`)

- **Ngày hoàn tất**: `2026-11-04` (`Asia/Saigon`)
- **Agent / Hội thoại**: Antigravity / `75da5edd-8ab3-45a1-80ce-457e2f92ea6f`
- **Phiếu công việc**: [`work-items/2026-11-04-antigravity-waifulink-v4-kirara.md`](work-items/2026-11-04-antigravity-waifulink-v4-kirara.md)
- **HTML Preview tương tác**: [`kirara-30-scenarios-135cgs-full-preview.html`](kirara-30-scenarios-135cgs-full-preview.html)
- **Target**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

---

## 1. Tóm tắt trung thực & Trạng thái bàn giao

- **Logic, kịch bản & nghiệm thu E2E (`Part A` + `Part B` DirectX 9 + `JP Voice` + `eagle_doctor`)**: **100% PASS**
  - **Part A (Offline Engine + Live `gpt-6-luna`)**: **`39/39` assertions PASS** trên SQLite cô lập `staging/project-eagle/waifulink-kirara-qa-20261104/part_a_kirara.db` (`Stage 1 -> Stage 5`, `80 -> 1,000 Affection`, mở khóa đủ `15/15` Milestones, L3 Deep Memory Recall `Simulanka` / `Phantom in Boots` / `Chiori`, Stage Carryover không khóa cứng, 2-Strike Off-Topic Re-Ask + Anti-Stuck Bridge, không hồi quy `hutao`, `furina`, `citlali`, `columbina`).
  - **Part B (Live DirectX 9 `gta_pe.exe` `1920×1080` + JP Voice)**: **`12/12` ảnh chụp màn hình PASS** (`01`, `02`, `03a`, `03`, `04`, `05`, `06`, `07a`, `07b`, `08`, `09`, `10` — đã kiểm tra trực quan từng ảnh bằng `read_file`, không cắt chữ `...`, không dính mã màu `CFont` `~`/`|`/`*`), `19` lượt phát giọng Nhật thật của Kirara (`CV: Sayumi Suzushiro`, `mci_ok = true`), `0` lỗi trong `cleo/EagleLuaErrors.log`, `0` crash.
  - **Health Check tổng thể**: `eagle_doctor.py` đạt **`11/11 PASS` (`0 WARN`, `0 FAIL`)**; giữ nguyên 100% gói Presentation `03/11` (`WibuMenu.asi`, `fronten2.txd`, `fronten3.txd`), `data/peds.ide`, `models/hud.txd`, `CUSTOM/custom_mods.img`, `COMPONENTPEDS.img` và `data/project-eagle/dating-sim/voices/kirara/*.wav`.
- **Bộ ảnh CG `16:9` hoàn chỉnh (`135 / 135` ảnh độc lập — `100%` SHA-256 duy nhất)**:
  - Đã kết xuất, chuẩn hóa `1376×768` (`16:9`) và kiểm chứng PIL + SHA-256 đủ **`135 / 135` ảnh CG độc lập (`135/135` mã băm SHA-256 duy nhất, `0` ảnh thiếu, `0` ảnh trùng lặp)** tại `data/project-eagle/dating-sim/media/kirara_*.jpg` (luôn truyền ảnh tham chiếu gốc `ui_assets/waifu_kirara.png`: thiếu nữ nekomata tóc vàng sáng nhuộm đuôi xanh bạc hà búi hai tai mèo cột nơ đen, mắt ngọc lục bảo, răng khểnh nhỏ, hai đuôi mèo xù tách đôi, bốt đệm thịt hồng, trang phục *Whirling Bloom* & *Phantom in Boots* cùng Traveler Aether; giữ nguyên `kirara_cg1.jpg` & `kirara_cg2.jpg` cũ).
  - Toàn bộ `135/135` ảnh được nhúng trực tiếp trong [`kirara-30-scenarios-135cgs-full-preview.html`](kirara-30-scenarios-135cgs-full-preview.html) (`337,745` bytes) và ghi nhận đầy đủ tại [`cg_manifest_status.json`](../../staging/project-eagle/waifulink-kirara-qa-20261104/cg_manifest_status.json).
  - **Cập nhật nâng cấp Native Ultra Đợt 1 (`2026-11-05`)**: Đã vẽ lại và thay thế thành công toàn bộ **`17/17` bức CG cameo** do người dùng chọn bằng `image-generator` nội bộ (`gemini-3.1-flash-image`, tuyệt đối không gọi API ngoài), nâng tỷ lệ ảnh Native Ultra lên **`64/135`** (cập nhật kèm thẻ lọc `✨ Vừa vẽ lại Đợt 1 (17)` và chống lưu cache trình duyệt trong [`kirara-cg-redo-selector.html`](kirara-cg-redo-selector.html)).

---

## 2. Kiến trúc Gói Nhân vật Kirara (`eagle_waifulink_v4_kirara.py`)

| Hạng mục | Chi tiết triển khai |
| :--- | :--- |
| **Định danh Runtime** | `char_id = "kirara"`, `ped_id = 49432`, `model_name = "wl_kirara"`, mascot `ep_ms_kirara` |
| **Module kịch bản độc lập** | `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_kirara.py` (`SHA-256: 1bbd5cd1...53fd`) |
| **15 Time-Apart Milestones** | `kirara_m01..m15` tại mốc `[60, 125, 185, 250, 320, 385, 450, 520, 585, 650, 720, 785, 850, 925, 1000]`, suy nghĩ nội tâm `Twin-Tail Nekomata Instinct:`, hành động `<= 64` ký tự và 3 lựa chọn phản hồi (`r1`, `r2`, `r3`) |
| **30 Kịch bản Visual Novel (`120` Scene CGs)** | `20` Core Couple Scenarios (`kirara_s1_sc1..s5_sc4`) + `10` Extra Genshin Cameo Scenarios (`kirara_s1_ex1..s5_ex2` có mặt **Chiori, Charlotte, Yae Miko, Lynette & Furina, Navia & Nilou, Yoimiya & Ayaka, Wanderer, Nahida, Yumemizuki Mizuki, Chiori & Yae Miko**); mỗi kịch bản gồm 3 Node × 3 Lựa chọn (`BEST`/`GOOD`/`AWKWARD`) + chuỗi 4 khung CG `16:9` (`1/4 Opening` -> `4/4 Couple Ending`) |
| **Chuẩn sạch `CFont` RenderWare** | `0` ký tự cấm (`~`, `|`, `*`, ngoài ASCII), `mood <= 16` ký tự, `action_cue <= 64` ký tự |
| **Giọng lồng tiếng Nhật (`JP Voice`)** | `WaifuLink JP Voice Engine v1.0` (`CV: Sayumi Suzushiro / 鈴代紗弓`), `24` file `.wav` chia `8` nhóm cảm xúc tại `data/project-eagle/dating-sim/voices/kirara/` |
| **Nhà riêng (`home_coords`)** | **Komaniya Express Marina Outpost, Marina LS**: `[632.00, -1586.00, 14.35]` (mặt nhựa thực tế `standing Z = 15.53m` tương ứng mặt đường `~14.48m`, rộng phẳng, `0` EHI cone, không trùng nhà 5 bạn gái khác) |
| **3 Điểm hẹn hò (`date_spots`)** | Cách nhà `480.7m – 859.5m` (nằm gọn trong chuẩn `450m – 1,400m`):<br>1. `Santa Maria Sunbeam Pier` (`[372.00, -1990.00, 7.83]`, cách nhà `480.7m`, live `standing Z = 4.13m`)<br>2. `Melrose Chioriya Boutique` (`[812.00, -1105.00, 25.78]`, cách nhà `513.4m`, live `standing Z = 16.77m`)<br>3. `Pershing Bento Fountain` (`[1479.00, -1732.00, 13.38]`, cách nhà `859.5m`, live `standing Z = 13.38m`) |
| **Xe hẹn hò Free-Roam** | Xe mui trần không tựa đầu **`575 Broadway`** sơn màu **Dendro Mint & Pearl White (`[86, 1]`)** |

---

## 3. Lỗi Tọa Độ Cũ Đã Khắc Phục & Tinh Chỉnh Hiển Thị HUD

1. **Sửa triệt để lỗi tọa độ `home_coords` trùng `date_spots[0]` (`0.0m`) ở sân đất Flint Range (`eagle_dating_sim.py`)**:
   - Trước khi sửa, `kirara` dùng `home_coords = [-377.40, -1438.69, 24.72]` trùng khít `0.0m` với `date_spots[0]` trên nền đất nông trại gồ ghề Flint Range, còn `date_spots[1]` văng xa `2.87 km` ra sát bờ nước Palomino Creek.
   - Đã chuyển `home_coords` sang phố kênh đào **Marina Canal LS** (`[632.00, -1586.00, 14.35]`) và 3 `date_spots` đường nhựa rộng phẳng tại Santa Maria (`480.7m`), Melrose (`513.4m`) và Pershing Square (`859.5m`), kiểm chứng trực tiếp Z mặt đường trong `gta_pe.exe`.
2. **Đấu nối đầy đủ nhánh persona Kirara trong `eagle_dating_sim.py` & `eagle_waifulink_v4_pilot.py`**:
   - Nối `KIRARA_15_MILESTONES`, `KIRARA_STAGE_CHAT_STARTERS`, `KIRARA_30_SCENARIOS`, ma trận 5 tầng `ARCHETYPE_5LAYER_MATRICES["kirara"]` (hồi ức 3.7 *Summoners' Summit*, *Cisoria Chapter* của Chiori, và 4.8 *Simulanka — Phantom in Boots*), tiền tố nội tâm `Twin-Tail Nekomata Instinct: `, lời thoại cứu hộ xe cháy / `Wasted` / `S`/`A`/`FAIL` riêng của Kirara, và rút gọn tên 3 điểm hẹn `<= 25` ký tự để thanh `GPS ROUTING:` góc dưới phải hiển thị trọn vẹn 100%.

---

## 4. Kết Quả Nghiệm Thu Part A & Part B Live DirectX 9 (`12/12` Ảnh Kiểm Mắt Thật + JP Voice)

- **Báo cáo JSON máy đọc**:
  - Part A: [`part_a_results.json`](../../staging/project-eagle/waifulink-kirara-qa-20261104/part_a_results.json) (`39/39 PASS`, `gpt-6-luna (OpenAI Live)`)
  - Part B: [`part_b_live_results.json`](../../staging/project-eagle/waifulink-kirara-qa-20261104/part_b_live_results.json) (`all_passed = true`, `play_count = 19`, `lua_errors = 0`)

### 4.1. Telemetry Giọng Nhật Thật (`WaifuLink JP Voice Engine v1.0`)
- **Seiyuu**: `Sayumi Suzushiro (鈴代紗弓)` — Backend `mci_mpegvideo`, `mci_ok = true` trên toàn bộ **`19` lượt phát** trong phiên live DirectX 9:
  - `greet_doorstep`: `1` lượt (chào đón trước trạm Marina Canal LS)
  - `vn_sweet_happy`: `6` lượt | `vn_tender_love`: `4` lượt (các cảnh Visual Novel `kirara_s1_sc1` & `kirara_s1_ex1`)
  - `outing_cruise`: `3` lượt (`outing_cruise_01.wav`, `02.wav`, `03.wav` khi khởi hành xe `575 Broadway`)
  - `outing_bump_rescue`: `3` lượt (`outing_bump_rescue_01.wav`, `02.wav`, `03.wav` khi va chạm hạ hạng, sơ tán xe cháy & nổ xe `Wasted`)
  - `outing_arrive_photo`: `2` lượt (`outing_arrive_photo_01.wav` khi cán đích điểm hẹn & `03.wav` khi nổ ảnh Time-Apart `kirara_m02.jpg`)

### 4.2. Bảng Kiểm Chứng Trực Quan 12 Ảnh Chụp DirectX 9 (`1920×1080`)

| STT | Tệp ảnh DirectX 9 (`1920×1080`) | Nội dung kiểm chứng trực quan (`read_file`) | Trạng thái |
| :--- | :--- | :--- | :---: |
| `01` | [`kirara_01_app13_f6_typing.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_01_app13_f6_typing.png) | App 13 WaifuLink của Kirara (`ep_ms_kirara`, `Love 80/1000`), chế độ gõ trực tiếp `[F6]`: `> brought grilled fish bento and chin scratches` rõ nét, không lỗi font. | **PASS** |
| `02` | [`kirara_02_app13_live_ai_reply.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_02_app13_live_ai_reply.png) | Phản hồi thật 2 lượt liên tiếp từ `gpt-6-luna` (`80 -> 86 -> 92/1000`), hiển thị biểu cảm `Delighted`, câu trả lời của Kirara và 3 gợi ý chat động mới. | **PASS** |
| `03a` | [`kirara_03a_doorstep_3d_ambient.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_03a_doorstep_3d_ambient.png) | 3D `wl_kirara` (`ped_id = 49432`, `2000.0 HP`, trang phục *Whirling Bloom*, hai đuôi mèo + nơ tai mèo) đứng trên mặt nhựa phẳng Marina Canal LS + Ambient HUD `[HOUSE VISIT] Near Kirara's Home (3m)`. | **PASS** |
| `03` | [`kirara_03_doorstep_3d_and_selector.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_03_doorstep_3d_and_selector.png) | 3D `wl_kirara` đứng trọn vẹn bên lề nắng trái cạnh bảng `[F9]` `HOUSE VISIT EVENT TRIGGER: Kirara (Komaniya Express Marina Outpost, Marina LS)` + ảnh preview `kirara_m01.jpg` và 5 lựa chọn không mất chữ. | **PASS** |
| `04` | [`kirara_04_vn_scene1_fullscreen.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_04_vn_scene1_fullscreen.png) | Fullscreen `16:9` Visual Novel `kirara_s1_sc1` (`1/4 OPENING CG`), Kirara chào kiểu bưu tá trao hộp quà nơ xanh bạc hà cho Aether bên kênh đào Marina + dòng nội tâm `Twin-Tail Nekomata Instinct` đầy đủ. | **PASS** |
| `05` | [`kirara_05_vn_scene4_ending.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_05_vn_scene4_ending.png) | Hoàn thành `4/4 COUPLE ENDING` (`SCENARIO PASSED! (+35 Affection)`, `92 -> 127`), hiện đếm ngược `Auto-closing overlay in 3.9s` và tự đóng mượt sau `4.5s`. | **PASS** |
| `06` | [`kirara_06_vn_extra_cameo.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_06_vn_extra_cameo.png) | Kịch bản Extra Genshin Cameo `kirara_s1_ex1` (`Cameo: Chiori`) hiển thị CG `16:9` Chiori kiểm tra đường may trang phục *Whirling Bloom* cùng Kirara và Aether tại Chioriya Boutique. | **PASS** |
| `07a` | [`kirara_07a_freeroam_rear_broadway.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_07a_freeroam_rear_broadway.png) | Góc cam sau xe mui trần `575 Broadway` màu xanh bạc hà - nội thất trắng (`[86, 1]`), vạch GPS xanh lá (`87 m`), HUD `S-RANK (+25)` và thanh `GPS ROUTING: Kirara Date: Pershing Bento Fountain (88m - E) [F10: Clear]` không cắt chữ. | **PASS** |
| `07b` | [`kirara_07b_freeroam_front_camera.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_07b_freeroam_front_camera.png) | Góc cam nhìn ngược đầu xe (`Q+E`) dưới nắng sớm `09:13` thấy rõ 3D `wl_kirara` ngồi ghế phụ cạnh Aether, không vướng tựa đầu hay vòng chọn radio. | **PASS** |
| `08` | [`kirara_08_arrival_and_m02_banner.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_08_arrival_and_m02_banner.png) | Cán đích Pershing Bento Fountain (`A-RANK +20`, `162 -> 182`), sau khi tạm biệt rời xe `>38m` và chờ `~11s`, tự động nổ banner `[ALERT] WAIFULINK PHOTO: KIRARA — M02: Sunlit Chin Scratches & Cat-Ear Ribbons` kèm ảnh `kirara_m02.jpg`. | **PASS** |
| `09` | [`kirara_09_burning_car_rescued_2000hp.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_09_burning_car_rescued_2000hp.png) | **Torture A**: Xe `575 Broadway` bốc cháy ngùn ngụt (`220 HP < 250`) — cầu CLEO lập tức sơ tán 3D `wl_kirara` đứng an toàn cách đám cháy ở **`2000.0 / 2000.0 HP`** (`rescue_count = 1`) dưới banner `[ALERT] KIRARA SAFE (2000 HP)`. | **PASS** |
| `10` | [`kirara_10_wasted_kirara_immortal_2000hp.png`](../../staging/project-eagle/waifulink-kirara-qa-20261104/live_screenshots/kirara_10_wasted_kirara_immortal_2000hp.png) | **Torture B**: Xe phát nổ `0 HP` + người chơi tử trận thật sự (`Wasted`, `player_hp = 0.0`, `state = 55`) — 3D `wl_kirara` (`model_idx = 49432`, `shm_ped_model = 49432`, `rescue_count = 2`, `heartbeat = 8736`) vẫn đứng nguyên vẹn ở **`2000.0 / 2000.0 HP`**. | **PASS** |

---

## 5. Bảng Hash SHA-256 & Hướng Dẫn Rollback An Toàn

### Manifest SHA-256 các tệp Runtime liên quan

| Tệp Runtime (`Project Eagle/gta sa gameplay-lab/`) | Trạng thái | SHA-256 hiện tại sau tích hợp |
| :--- | :---: | :--- |
| `eagle_waifulink_v4_kirara.py` | Tạo mới | `1bbd5cd1fc368deda39047c1d7f3798a9e6a342bd7b184d2be616c161f8153fd` |
| `eagle_waifulink_v4_pilot.py` | Sửa dùng chung | `bae0deeed7f7da7223543349c599dfc090684a88167ef49fdd620502b48d6397` |
| `eagle_dating_sim.py` | Sửa dùng chung | `835145bd2a2c73191cc77170a5478b04657f96929f7d835e50d8b1a8ecaa9d34` |

### Sao lưu & Phục hồi có kiểm tra khóa
- Bản sao lưu trước khi đấu nối được lưu tại `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-kirara-qa-20261104\backups\` (gồm `before_hashes.json`, `after_hashes.json`, `eagle_waifulink_v4_pilot.py.pre_kirara.bak`, `eagle_dating_sim.py.pre_kirara.bak`).
- **Quy trình rollback an toàn**: Không chép đè mù quáng file `.bak` nếu có hội thoại khác đã cập nhật sau đó; luôn chiếm `game-write.lock` qua `tools/eagle_coord_lock.py`, đối chiếu SHA-256 hiện tại trên đĩa với `after_hashes.json`, rồi gỡ riêng nhánh `char_id == "kirara"` trong `eagle_waifulink_v4_pilot.py` + `eagle_dating_sim.py` và xóa `eagle_waifulink_v4_kirara.py` (cùng 135 file `kirara_m*.jpg` / `kirara_s*.jpg`, giữ lại `kirara_cg1.jpg` & `kirara_cg2.jpg`).

---

## 6. Trạng Thái Hoàn Tất & Khóa Điều Phối

- **Trạng thái khóa (`tools/eagle_coord_lock.py status`)**:
  - `game-write`: `null` (đã giải phóng sạch)
  - `ingame-runtime`: `null` (đã tắt sạch `gta_pe.exe` & `EagleCompanion.py`, đã khôi phục sạch `eagle_companion.db` / `waifulink.sqlite3` và đồng bộ `EaglePhoneHUD.dat` về `open=0, ev_active=0`)
- **Trạng thái công việc**: **100% DONE** (`135/135` CGs `16:9` SHA-256 duy nhất, `Part A 39/39 PASS`, `Part B DirectX 9 12/12 PASS`, `JP Voice 19 plays OK`, `eagle_doctor 11/11 PASS`).
