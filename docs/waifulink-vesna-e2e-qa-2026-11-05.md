# Báo Cáo Triển Khai & Nghiệm Thu E2E In-Game DirectX 9 + JP Voice: Vesna Strivozha (`char_id = "vesna"`, `ped_id = 49433` — Hoàn Tất Dàn 6/6)

- **Ngày hoàn tất**: `2026-11-05` (`Asia/Saigon`)
- **Agent / Hội thoại**: Antigravity / `42c2a1f1-4470-495c-a8f8-7e7b2c24fb68`
- **Phiếu công việc**: [`work-items/2026-11-05-antigravity-waifulink-v4-vesna.md`](work-items/2026-11-05-antigravity-waifulink-v4-vesna.md)
- **HTML Preview tương tác**: [`vesna-30-scenarios-135cgs-full-preview.html`](vesna-30-scenarios-135cgs-full-preview.html)
- **Target**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

---

## 1. Tóm tắt trung thực & Trạng thái bàn giao

- **Logic, kịch bản, hoàn tất dàn `6/6` & nghiệm thu E2E (`Part A` + `Part B` DirectX 9 + `JP Voice` + `eagle_doctor`)**: **100% PASS**
  - **Part A (Offline Engine + Live `gpt-6-luna` + Toàn dàn `6/6`)**: **`41/41` assertions PASS** trên SQLite cô lập `staging/project-eagle/waifulink-vesna-qa-20261105/part_a_vesna.db` (`Stage 1 -> Stage 5`, `80 -> 1,000 Affection`, mở khóa đủ `15/15` Milestones của Vesna, L3 Deep Memory Recall `Swords and Secrets` / `Danica` / `The Tsaritsa` kích hoạt `8` mục ký ức sâu, Stage Carryover không khóa cứng, 2-Strike Off-Topic Re-Ask + Anti-Stuck Bridge `+10`, Dynamic AI Encore `+1 Gate`, xác nhận toàn bộ **`6/6` nhân vật** `hutao`, `furina`, `citlali`, `columbina`, `kirara`, `vesna` đều đạt `is_pilot_complete == True` với `30` kịch bản và tổng `90` Milestones).
  - **Part B (Live DirectX 9 `gta_pe.exe` `1920×1080` + JP Voice)**: **`13/13` ảnh chụp màn hình PASS** (`01`, `02`, `03a`, `03`, `04`, `05`, `06a`, `06b`, `07a`, `07b`, `08`, `09`, `10` — đã kiểm tra trực quan từng ảnh bằng `read_file`, không cắt chữ `...`, không dính mã màu `CFont` `~`/`|`/`*`), **`20/20` lượt phát giọng Nhật thật của Vesna (`CV: Aya Endo / 遠藤綾`, `mci_ok = true`) trải đủ `8/8` nhóm cảm xúc**, `0` lỗi trong `cleo/EagleLuaErrors.log`, `0` crash (tương thích trơn tru trên `EaglePhone OS v6.2`).
  - **Health Check tổng thể**: `eagle_doctor.py` đạt **`11/11 PASS` (`0 WARN`, `0 FAIL`)**; giữ nguyên 100% gói Presentation `03/11` (`WibuMenu.asi`, `fronten2.txd`, `fronten3.txd`), `data/peds.ide`, `models/hud.txd`, `CUSTOM/custom_mods.img`, `COMPONENTPEDS.img` và `data/project-eagle/dating-sim/voices/vesna/*.wav`.
- **Bộ ảnh CG `16:9` hoàn chỉnh của Vesna (`135 / 135` ảnh độc lập — `100%` SHA-256 duy nhất)**:
  - Đã kết xuất bằng subagent `image-generator` nội bộ (luôn truyền đủ 3 ảnh gốc tham chiếu Snezhnaya 7.1, tuân thủ tuyệt đối Luật Cứng — hoàn thành `80` ảnh trước mốc quota và tự động chạy tiếp `55` ảnh còn lại ngay khi hồi quota lúc `05:41` sáng `05/11/2026` `UTC+7`), chuẩn hóa `1376×768` (`16:9`) và kiểm chứng PIL + SHA-256 đủ **`135 / 135` ảnh CG độc lập (`135/135` mã băm SHA-256 duy nhất, `0` ảnh thiếu, `0` ảnh trùng lặp)** tại `data/project-eagle/dating-sim/media/vesna_*.jpg` (giữ nguyên `vesna_cg1.jpg` & `vesna_cg2.jpg` cũ):
    - **`15 / 15` Milestone CGs (`vesna_m01..vesna_m15`)**: **Đủ `100%`**.
    - **`80 / 80` Core Couple CGs (`vesna_s{1..5}_sc{1..4}_cg{1..4}`)**: **Đủ `100%`**.
    - **`40 / 40` Extra Snezhnaya & Genshin Cameo CGs (`vesna_s{1..5}_ex{1..2}_cg{1..4}`)**: **Đủ `100%`** (**Danica**, **Tartaglia/Childe**, **Odette**, **Vodyanitsa**, **Columbina**, **Arlecchino**, **The Tsaritsa**).
  - Toàn bộ `135/135` ảnh được nhúng trực tiếp trong [`vesna-30-scenarios-135cgs-full-preview.html`](vesna-30-scenarios-135cgs-full-preview.html) (`334,790` bytes, `0` ô chờ) và ghi nhận đầy đủ tại [`cg_manifest_status.json`](../../staging/project-eagle/waifulink-vesna-qa-20261105/cg_manifest_status.json).

---

## 2. Kiến trúc Gói Nhân vật Vesna (`eagle_waifulink_v4_vesna.py`) & Bảng Tổng Hợp Dàn 6/6

### 2.1. Đặc tả kỹ thuật Vesna Strivozha (`#6/6`)

| Hạng mục | Chi tiết triển khai |
| :--- | :--- |
| **Định danh Runtime** | `char_id = "vesna"`, `ped_id = 49433`, `model_name = "wl_vesna"`, mascot `ep_ms_vesna` |
| **Module kịch bản độc lập** | `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_vesna.py` (`SHA-256: 867348b7...e2ab`) |
| **15 Time-Apart Milestones** | `vesna_m01..m15` tại mốc `[60, 125, 185, 250, 320, 385, 450, 520, 585, 650, 720, 785, 850, 925, 1000]`, suy nghĩ nội tâm `Vila Blade's Resonance:`, hành động `<= 64` ký tự và 3 lựa chọn phản hồi (`r1`, `r2`, `r3`) |
| **30 Kịch bản Visual Novel (`120` Scene CGs)** | `20` Core Couple Scenarios (`vesna_s1_sc1..s5_sc4`) + `10` Extra Snezhnaya & Genshin Cameo Scenarios (`vesna_s1_ex1..s5_ex2` có mặt **Danica, Tartaglia, Odette, Vodyanitsa, Columbina, Arlecchino, Danica & Odette, The Tsaritsa, Danica & Vodyanitsa, The Tsaritsa & Royal Court**); mỗi kịch bản gồm 3 Node × 3 Lựa chọn (`BEST`/`GOOD`/`AWKWARD`) + chuỗi 4 khung CG `16:9` (`1/4 Opening` -> `4/4 Couple Ending`) |
| **Chuẩn sạch `CFont` RenderWare** | `0` ký tự cấm (`~`, `|`, `*`, ngoài ASCII), `mood <= 16` ký tự, `action_cue <= 64` ký tự |
| **Giọng lồng tiếng Nhật (`JP Voice`)** | `WaifuLink JP Voice Engine v1.0` (`CV: Aya Endo / 遠藤綾`), `24` file `.wav` chia `8` nhóm cảm xúc tại `data/project-eagle/dating-sim/voices/vesna/` |
| **Nhà riêng (`home_coords`)** | **Palisades Bayfront Villa, San Fierro**: `[-2824.00, 924.00, 43.10]` (mặt nhựa thực tế `live standing Z = 43.91m`, độ dốc `0.00%`, `0` EHI cone, nhìn thẳng cầu Gant Bridge & vịnh San Fierro, tách biệt hoàn toàn với 5 bạn gái khác) |
| **3 Điểm hẹn hò (`date_spots`)** | Cách nhà `531.1m – 1,066.0m` (nằm gọn trong chuẩn `450m – 1,400m`):<br>1. `Battery Point Bayview` (`[-2542.00, 1374.00, 6.20]`, cách nhà `531.1m`, `live standing Z = 7.04m`)<br>2. `Calton Heights Manor` (`[-2067.00, 1076.00, 54.65]`, cách nhà `772.1m`, `live standing Z = 55.57m`)<br>3. `Esplanade North Coast` (`[-1854.88, 1368.00, 6.30]`, cách nhà `1,066.0m`, `live standing Z = 7.04m`) |
| **Xe hẹn hò Free-Roam** | Xe mui trần không tựa đầu **`575 Broadway`** sơn màu **Golden Amber & Pearl White (`[6, 1]`)** |

### 2.2. Bảng Hoàn Tất Toàn Dàn Bạn Gái WaifuLink v4.0 (`6 / 6`)

| # | `char_id` | Nhân vật | `ped_id` (`model_name`) | Mascot HUD | Khu vực nhà riêng | Màu xe `575 Broadway` | Seiyuu (`24` `.wav`) | Kịch bản / Milestones |
| :-: | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| `1` | `hutao` | Hu Tao | `49428` (`wl_hutao`) | `ep_ms_hutao` | Chinatown, San Fierro | Crimson & Dark (`[3, 0]`) | Rie Takahashi | `30` / `15` (`PASS`) |
| `2` | `furina` | Furina de Fontaine | `49429` (`wl_furina`) | `ep_ms_furina` | Richman Hills, Los Santos | Royal Blue & White (`[79, 1]`) | Inori Minase | `30` / `15` (`PASS`) |
| `3` | `citlali` | Citlali | `49430` (`wl_citlali`) | `ep_ms_citlali` | Verona Beach, Los Santos | Opal Pink & Ice (`[126, 1]`) | Asami Seto | `30` / `15` (`PASS`) |
| `4` | `columbina` | Columbina | `49431` (`wl_columbina`) | `ep_ms_columbina` | Prickle Pine, Las Venturas | Pearl White & Rose (`[1, 126]`) | Lynn | `30` / `15` (`PASS`) |
| `5` | `kirara` | Kirara | `49432` (`wl_kirara`) | `ep_ms_kirara` | Marina Canal, Los Santos | Dendro Mint & White (`[86, 1]`) | Sayumi Suzushiro | `30` / `15` (`PASS`) |
| `6` | `vesna` | Vesna Strivozha | `49433` (`wl_vesna`) | `ep_ms_vesna` | Palisades Bayfront, North SF | Golden Amber & White (`[6, 1]`) | Aya Endo | `30` / `15` (`PASS`) |

---

## 3. Lỗi Tọa Độ Cũ Đã Khắc Phục & Làm Sạch `CFont`

1. **Sửa triệt để lỗi tọa độ `home_coords` trùng `date_spots[0]` (`0.0m`) ở El Quebrados và điểm hẹn văng `3.54 km` sang Las Venturas (`eagle_dating_sim.py`)**:
   - Trước khi sửa, `vesna` để `home_coords = [-1398.10, 2636.87, 54.70]` (sân đồn cảnh sát thị trấn nhỏ El Quebrados) trùng `0.0m` với `date_spots[0]`, còn `date_spots[2]` (`[2127.40, 2378.20, 10.82]`) văng xa `3.54 km` xuyên sa mạc sang Las Venturas.
   - Đã chuyển `home_coords` về biệt thự ven biển **Palisades Bayfront Villa, Bắc San Fierro** (`[-2824.00, 924.00, 43.10]`) cùng 3 điểm hẹn cung đường ven vịnh Bắc San Fierro phẳng đẹp tại **Battery Point Bayview** (`531.1m`), **Calton Heights Manor** (`772.1m`) và **Esplanade North Coast** (`1,066.0m`), đo trực tiếp `live standing Z` trong `gta_pe.exe`.
2. **Đấu nối đầy đủ `6/6` nhân vật và làm sạch ký tự `~` cũ**:
   - Nối `VESNA_15_MILESTONES`, `VESNA_STAGE_CHAT_STARTERS`, `VESNA_30_SCENARIOS`, ma trận 5 tầng `ARCHETYPE_5LAYER_MATRICES["vesna"]` (hồi ức Version 7.1 *Swords and Secrets* Parts I–VII, thanh kiếm *Beyond the Chrysalis*, cẩm nang của Hầu gái trưởng Danica và triều đình Tsaritsa), tiền tố nội tâm `Vila Blade's Resonance: `, lời thoại cứu hộ xe cháy / `Wasted` / `S`/`A`/`FAIL` riêng của Vesna, đồng thời loại bỏ sạch các dấu `~` cũ trong `starter_messages`, `hangout_choices`, `voice_style` của `vesna`.

---

## 4. Kết Quả Nghiệm Thu Part A & Part B Live DirectX 9 (`13/13` Ảnh Kiểm Mắt Thật + JP Voice)

- **Báo cáo JSON máy đọc**:
  - Part A: [`part_a_results.json`](../../staging/project-eagle/waifulink-vesna-qa-20261105/part_a_results.json) (`41/41 PASS`, `gpt-6-luna` Live + kiểm đủ `6/6` roster)
  - Part B: [`part_b_live_results.json`](../../staging/project-eagle/waifulink-vesna-qa-20261105/part_b_live_results.json) (`all_passed = true`, `play_count = 20`, `lua_errors = 0`)

### 4.1. Telemetry Giọng Nhật Thật (`WaifuLink JP Voice Engine v1.0`)
- **Seiyuu**: `Aya Endo (遠藤綾)` — Backend `mci_mpegvideo`, `mci_ok = true` trên toàn bộ **`20 / 20` lượt phát** phủ kín **`8 / 8` nhóm cảm xúc** trong phiên live DirectX 9:
  - `greet_doorstep`: `1` lượt | `vn_sweet_happy`: `2` lượt | `vn_shy_blush`: `1` lượt | `vn_playful_tease`: `2` lượt | `vn_tender_love`: `6` lượt
  - `outing_cruise`: `3` lượt (`outing_cruise_01.wav`, `02.wav`, `03.wav` khi dạo phố trên `575 Broadway`)
  - `outing_bump_rescue`: `3` lượt (`outing_bump_rescue_01.wav`, `02.wav`, `03.wav` khi va chạm, sơ tán xe cháy `220 HP` & nổ xe `Wasted`)
  - `outing_arrive_photo`: `2` lượt (`outing_arrive_photo_01.wav` khi cán đích Battery Point & `03.wav` khi nổ ảnh Time-Apart `vesna_m02.jpg`)

### 4.2. Bảng Kiểm Chứng Trực Quan 13 Ảnh Chụp DirectX 9 (`1920×1080`)

| STT | Tệp ảnh DirectX 9 (`1920×1080`) | Nội dung kiểm chứng trực quan (`read_file`) | Trạng thái |
| :--- | :--- | :--- | :---: |
| `01` | [`vesna_01_app13_f6_typing.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_01_app13_f6_typing.png) | App 13 WaifuLink của Vesna trên EaglePhone OS v6.2 (`ep_ms_vesna`, `80/1000`), chế độ gõ `[F6]`: `> brought northland honey tea for my commander` rõ nét trước cầu Gant Bridge. | **PASS** |
| `02` | [`vesna_02_app13_live_ai_reply.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_02_app13_live_ai_reply.png) | Phản hồi thật 2 lượt liên tiếp từ `gpt-6-luna` (`80 -> 86 -> 92/1000`), không cắt chữ `...`, kèm 3 gợi ý chat động mới chuẩn giọng Tư lệnh Druzhna. | **PASS** |
| `03a` | [`vesna_03a_doorstep_3d_ambient.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_03a_doorstep_3d_ambient.png) | 3D `wl_vesna` (`ped_id = 49433`, `2000.0 HP`, đôi cánh tiên tuyết Vila óng ánh) đứng trên mặt nhựa phẳng Palisades Bayfront Villa (`10:17` sáng) + Ambient HUD `[HOUSE VISIT] Near Vesna's Home (4m)`. | **PASS** |
| `03` | [`vesna_03_doorstep_3d_and_selector.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_03_doorstep_3d_and_selector.png) | 3D `wl_vesna` đứng rõ bên trái cạnh bảng `[F9]` `HOUSE VISIT EVENT TRIGGER: Vesna (Palisades Bayfront Villa, San Fierro)` + ảnh preview `vesna_m01.jpg` và 5 lựa chọn không cụt chữ. | **PASS** |
| `04` | [`vesna_04_vn_scene1_fullscreen.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_04_vn_scene1_fullscreen.png) | Fullscreen `16:9` Visual Novel `vesna_s1_sc1` (`1/4 OPENING CG`: `Royal Salute & Secret Cream-Heart Tea` với cầu Gant Bridge phía sau Aether & Vesna) + dòng nội tâm `Vila Blade's Resonance` đầy đủ. | **PASS** |
| `05` | [`vesna_05_vn_scene4_ending.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_05_vn_scene4_ending.png) | Hoàn thành `4/4 COUPLE ENDING` (`SCENARIO PASSED! (+35 Affection)`, `92 -> 127`, `Stage Gate: 1/3`), hiện đếm ngược và tự động đóng mượt sau `4.5s` không cần bấm phím. | **PASS** |
| `06a` | [`vesna_06a_vn_cameo_danica.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_06a_vn_cameo_danica.png) | Extra Cameo VN `vesna_s1_ex1` (**Danica** — tóc bob xanh teal, đồng phục Hầu gái trưởng trắng ngà-teal — rót trà bên cuốn cẩm nang quản lý Tư lệnh khiến Vesna đỏ mặt cạnh Aether). | **PASS** |
| `06b` | [`vesna_06b_vn_cameo_tsaritsa.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_06b_vn_cameo_tsaritsa.png) | Extra Cameo VN `vesna_s4_ex2` (**The Tsaritsa** ngự trên ngai băng pha lê Zapolyarny Palace ban chỉ dụ cho Vesna và Aether). | **PASS** |
| `07a` | [`vesna_07a_freeroam_rear_broadway.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_07a_freeroam_rear_broadway.png) | Góc cam sau xe mui trần `575 Broadway` màu vàng hổ phách - trắng ngọc trai (`[6, 1]`), 3D `wl_vesna` ngồi ghế phụ hướng về Gant Bridge, HUD `S-RANK (+25)` & thanh `GPS ROUTING` hiển thị trọn vẹn. | **PASS** |
| `07b` | [`vesna_07b_freeroam_front_camera.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_07b_freeroam_front_camera.png) | Góc cam nhìn ngược đầu xe (`Q+E`) dưới nắng chiều vàng `16:59` thấy rõ khuôn mặt và trang phục 3D `wl_vesna` ngồi cạnh Aether, không bị tựa đầu hay vòng radio che khuất. | **PASS** |
| `08` | [`vesna_08_arrival_and_m02_banner.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_08_arrival_and_m02_banner.png) | Cán đích `Battery Point Bayview` (`A-RANK +20`, `162 -> 182`), đi bộ rời xa `>38m` và chờ `>10s`, tự động nổ banner `[ALERT] WAIFULINK PHOTO: VESNA — M02: Secret Cream Heart & Tart Lemon Prank` kèm ảnh `vesna_m02.jpg`. | **PASS** |
| `09` | [`vesna_09_burning_car_rescued_2000hp.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_09_burning_car_rescued_2000hp.png) | **Torture A**: Xe `575 Broadway` bốc cháy ngùn ngụt (`220 HP < 250`) — cầu CLEO lập tức sơ tán 3D `wl_vesna` đứng an toàn cách đám cháy `5.5m` ở **`2000.0 / 2000.0 HP`** (`rescue_count = 1`) dưới banner `[ALERT] VESNA SAFE (2000 HP)`. | **PASS** |
| `10` | [`vesna_10_wasted_vesna_immortal_2000hp.png`](../../staging/project-eagle/waifulink-vesna-qa-20261105/live_screenshots/vesna_10_wasted_vesna_immortal_2000hp.png) | **Torture B**: Xe phát nổ `0 HP` + người chơi tử trận thật sự (`Wasted`, `player_hp = 0.0`, `state = 55`) — 3D `wl_vesna` (`model_idx = 49433`, `shm_ped_model = 49433`, `rescue_count = 2`, `heartbeat = 7262`) vẫn đứng nguyên vẹn ở **`2000.0 / 2000.0 HP`**. | **PASS** |

---

## 5. Xác Thực Toàn Bộ `135 / 135` Ảnh CG `16:9` (`1376×768`) & HTML Preview

- **Trạng thái hiện tại (`cg_manifest_status.json`)**: **`135 / 135` ảnh đã cài đặt (`135` mã băm SHA-256 duy nhất, `missing_count = 0`)**:
  - `15/15` Milestones (`vesna_m01..vesna_m15`)
  - `80/80` Core Couple CGs (`vesna_s{1..5}_sc{1..4}_cg{1..4}`) — hoàn tất nốt `55` ảnh ngay sau mốc hồi quota `05:40:34` sáng `05/11/2026` (`UTC+7`) và đã kiểm tra trực quan mẫu từng Stage bằng `read_file`
  - `40/40` Extra Snezhnaya & Genshin Cameo CGs (`vesna_s{1..5}_ex{1..2}_cg{1..4}`)
- **Trang HTML Preview đầy đủ**: [`vesna-30-scenarios-135cgs-full-preview.html`](vesna-30-scenarios-135cgs-full-preview.html) (`334,790` bytes, hiển thị đủ `135/135` ảnh CG thực tế).

---

## 6. Bảng Hash SHA-256 & Hướng Dẫn Rollback An Toàn

### Manifest SHA-256 các tệp Runtime liên quan

| Tệp Runtime (`Project Eagle/gta sa gameplay-lab/`) | Trạng thái | SHA-256 trước tích hợp | SHA-256 hiện tại sau tích hợp |
| :--- | :---: | :--- | :--- |
| `eagle_waifulink_v4_vesna.py` | Tạo mới | *(chưa tồn tại)* | `867348b796104e285824a15594c7c28b417a28a6ca8b0e725762b5d58b2fe2ab` |
| `eagle_waifulink_v4_pilot.py` | Sửa dùng chung | `bae0deeed7f7da7223543349c599dfc090684a88167ef49fdd620502b48d6397` | `ea84b8107ee4828b830206f6740f11ff9fec779e668fdd072daa43fae483373f` |
| `eagle_dating_sim.py` | Sửa dùng chung | `835145bd2a2c73191cc77170a5478b04657f96929f7d835e50d8b1a8ecaa9d34` | `2a36b1c448f52c8f09c0a82cbeb5fc8b5735882584cea7bdb7e143b12bbb36e2` |

### Sao lưu & Phục hồi có kiểm tra khóa
- Bản sao lưu trước khi đấu nối được lưu tại `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-vesna-qa-20261105\backups\` (gồm `before_hashes.json`, `after_hashes.json`, `eagle_waifulink_v4_pilot.py.pre_vesna.bak`, `eagle_dating_sim.py.pre_vesna.bak`).
- **Quy trình rollback an toàn**: Không chép đè mù quáng file `.bak` nếu có hội thoại khác đã cập nhật sau đó; luôn chiếm `game-write.lock` qua `tools/eagle_coord_lock.py`, đối chiếu SHA-256 hiện tại trên đĩa với `after_hashes.json`, rồi gỡ riêng nhánh `char_id == "vesna"` trong `eagle_waifulink_v4_pilot.py` + `eagle_dating_sim.py` và xóa `eagle_waifulink_v4_vesna.py` (cùng 135 file `vesna_m*.jpg` / `vesna_s*.jpg`, giữ lại `vesna_cg1.jpg` & `vesna_cg2.jpg`).

---

## 7. Trạng Thái Hoàn Tất & Khóa Điều Phối

- **Trạng thái khóa (`tools/eagle_coord_lock.py status`)**:
  - `game-write`: `null` (đã giải phóng sạch)
  - `ingame-runtime`: `null` (đã tắt sạch `gta_pe.exe` & `EagleCompanion.py`, đã khôi phục sạch `eagle_companion.db` / `waifulink.sqlite3` và đồng bộ `EaglePhoneHUD.dat` về `open=0, ev_active=0`)
- **Trạng thái công việc**: **100% DONE** (`135/135` CGs `16:9` SHA-256 duy nhất, hoàn tất toàn bộ dàn `6/6` bạn gái, `Part A 41/41 PASS`, `Part B DirectX 9 13/13 PASS`, `JP Voice 20 plays 8/8 buckets OK`, `eagle_doctor 11/11 PASS`).
