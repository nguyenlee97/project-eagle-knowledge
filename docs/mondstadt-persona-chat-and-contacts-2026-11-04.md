# Tích hợp 10 Nhân vật Mondstadt (3D Map + Persona Dialogue HUD + 61 CG Biểu Cảm) & App #14 Danh Bạ (`Contacts`) trên `gameplay-lab`

- **Ngày hoàn thành**: `2026-11-04`
- **Agent thực hiện**: Antigravity (`c71a77f9-97e6-4a68-aba6-9fb3b4acf926`)
- **Trạng thái**: `done` (**Part A `6/6` PASS**, **Part B DirectX 9 `1920×1080` `9/9` ảnh PASS**, `0` Lua errors, đã khôi phục save mở khóa về `0/10` sạch cho người chơi, đã nhả sạch cả 2 khóa `game-write` & `ingame-runtime`)
- **Target duy nhất**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Staging & Backup**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\mondstadt-persona-chat-20261104\`
- **Phiếu công việc**: [`work-items/2026-11-04-antigravity-mondstadt-persona-chat-ingame-integration.md`](work-items/2026-11-04-antigravity-mondstadt-persona-chat-ingame-integration.md)
- **Tài nguyên bảo toàn 100%**: Không đụng gói Presentation `03/11` (`WibuMenu.asi`, `fronten2.txd`, `fronten3.txd`), không đụng `clean` trên ổ `D:`, không đụng `eagle_waifulink_v4_*.py` / `eagle_dating_sim.py` của các gói WaifuLink.

---

## 1. Kiến trúc tổng thể & 4 trụ cột tính năng

1. **10 NPC Mondstadt 3D sống động trên bản đồ (`Ped IDs 49434..49443`) + Quạ Lôi Oz 3D bay lơ lửng (`Object ID 6702`)**:
   - Đóng gói 10 model riêng (`mc_venti` .. `mc_fischl`) vào `CUSTOM/custom_mods.img` (đã tối ưu DXT1/DXT5 `<= 512px` kèm mipmap) và đăng ký `49434..49443` trong `data/peds.ide`.
   - Đóng gói `oz_static.{dff,txd}` + `COL3` (`Object ID 6702`) vào `CUSTOM/mondstadt_m1_wilds.{ide,col,img}`; Oz bay lơ lửng theo sóng tam giác `±0.09m` ngay cạnh vai phải Fischl ở Hiệp Hội Nhà Mạo Hiểm.
   - Dọn sạch các sub-mesh tượng nhân vật tĩnh nướng cứng trong 5 nội thất Mondstadt (`int_knights_hq.dff`, `int_angels_share.dff`, `int_fav_cathedral.dff`, `int_dawn_winery.dff`, `int_alchemy_lab.dff`) và cập nhật `cleo/MondstadtLifeAndBlips.cs` (gỡ bản sao Kaeya `Ped 211` ở sạp hoa Flora & Hu Tao `Ped 274`) để đảm bảo **0 nhân bản trùng lặp** trên toàn cõi Mondstadt.
2. **Cầu CLEO 60 FPS `cleo/EagleMondstadtChatBridge.cs` (`MCHT` @ `0x00CAFE40` / `0x00CAFE44`)**:
   - Stream/despawn thông minh theo khoảng cách `140m` / `175m` và kiểm tra khớp `area_code` (`0` ngoài trời `M0/M1`, `1` trong nội thất `INT-04`).
   - Bất tử `2000.0 HP` + khóa vị trí cho 10 NPC.
   - Phát hiện cạnh lên phím vật lý `[E]` trong bán kính `3.15m`, xoay ma trận `CMatrix` để Traveler Aether và NPC hướng mặt trực diện vào nhau, cắt góc máy **3D Two-Shot nửa trái màn hình (`X_norm ≈ 0.19..0.45`)**, và chạy **animation cử chỉ trò chuyện hai chiều** (`IDLE_chat`, `endchat_01..03`, `factalk`, `XPRESSscratch`) cho cả Aether lẫn NPC theo từng lượt thoại.
3. **Persona 3 Reload / Persona 5 Dialogue HUD + 61 Sprite Biểu Cảm `512×512` (`hud.lua` + `MCSP0/MCSP1.TXD`)**:
   - Nửa phải màn hình (`X_norm ≈ 0.52..0.99`) hiển thị CG bán thân nền trong suốt `512×512` BGRA8888 (`1,048,744` bytes) nạp động qua cơ chế ping-pong `models/txd/MCSP0.TXD` & `MCSP1.TXD` trên `TXD slot 95` (đã guard tránh xung đột với `WLCG0/1` của WaifuLink).
   - Bộ **61 sprite trong suốt** gồm `6` biểu cảm cho mỗi nhân vật (`neutral`, `happy`, `serious`, `surprised`, `sad_worried`, `smug_teasing`) cộng thêm sprite riêng **`oz`** (`Oz - Night Raven Familiar`) tự động bật lên cùng bảng tên `Oz` mỗi khi Oz dịch lời cho Fischl.
   - Tích hợp trực tiếp với `tools/eagle-character-chat` (`gpt-6-luna` qua `http://127.0.0.1:8317/v1` + SQLite `conversations.sqlite3`): hỗ trợ chọn nhanh `[1..4]` hoặc bấm **`[F6]` gõ chat tự do trực tiếp trong game**.
4. **App #14 Danh Bạ & Nhắn Tin Từ Xa (`14.Contacts` trên EaglePhone `5×3`)**:
   - Hợp nhất **16 liên hệ** (`3` tab `1.All (16)` / `2.Mondstadt (10)` / `3.Waifus (6)`):
     - **6 Waifu (`Hu Tao`, `Furina`, `Citlali`, `Columbina`, `Kirara`, `Vesna`)**: Mở khóa sẵn (`[OPEN]`), bấm `[F9]` chuyển thẳng sang `App #13 WaifuLink` của đúng nhân vật đó.
     - **10 Nhân vật Mondstadt**: Khởi đầu ở trạng thái **`[LOCK]`**. Khi chưa gặp ngoài đời, bấm `[F9]` hoặc `[F10]` sẽ **cắm mốc đỏ GPS** dẫn đường tới đúng vị trí đứng trên bản đồ (riêng Jean & Lisa trong nội thất `INT-04` sẽ dẫn đường tới cửa chính Trụ sở Kỵ Sĩ Đội Tây Phong `(-4374.0, -3018.0, 59.70)`).
     - Ngay lần đầu gặp trực tiếp và bấm `[E]` trò chuyện trên bản đồ, nhân vật được **mở khóa vĩnh viễn (`[OPEN]`)** trong Danh Bạ kèm thông báo `NEW SOCIAL LINK UNLOCKED`, cho phép nhắn tin từ xa (`Remote DM` qua `[1..3]` hoặc `[F6]`) **dùng chung chính xác cùng một bộ nhớ hội thoại SQLite** với các cuộc gặp trực tiếp (nhắn tin qua điện thoại không cắt camera 3D).

---

## 2. Bảng định danh & Tọa độ 10 Nhân vật Mondstadt + Oz

| STT | `char_id` | Tên hiển thị | `ped_id` / `obj_id` | Model (`.img`) | Khu vực (`area`) | Tọa độ `(X, Y, Z, Heading)` | Ghi chú định vị / GPS |
|---:|---|---|---:|---|---:|---|---|
| 0 | `venti` | Venti | `49434` | `mc_venti` (`custom_mods.img`) | `0` (`M1`) | `(-3813.0, -3324.0, 31.14, 180°)` | Gốc Đại Thụ Phong Khởi (`Windrise Great Oak`) |
| 1 | `jean` | Jean | `49435` | `mc_jean` (`custom_mods.img`) | `1` (`INT-04`) | `(-3952.2, -3494.8, 1500.52, 180°)` | Văn phòng Đội trưởng (`outdoor_gps`: `-4374.0, -3018.0, 59.70`) |
| 2 | `diluc` | Diluc | `49436` | `mc_diluc` (`custom_mods.img`) | `0` (`M1`) | `(-4808.0, -3567.0, 24.06, 135°)` | Sân trước Tửu Trang Dawn (`Dawn Winery Forecourt`) |
| 3 | `mona` | Mona | `49437` | `mc_mona` (`custom_mods.img`) | `0` (`M0`) | `(-4213.0, -3055.0, 6.65, 0°)` | Trước nhà Chiêm Tinh Nam Mondstadt (`Astrologist House`) |
| 4 | `kaeya` | Kaeya | `49438` | `mc_kaeya` (`custom_mods.img`) | `0` (`M0`) | `(-4242.0, -3028.5, 12.60, 160°)` | Quảng trường Đài Phun Nước / Good Hunter |
| 5 | `lisa` | Lisa | `49439` | `mc_lisa` (`custom_mods.img`) | `1` (`INT-04`) | `(-3946.2, -3496.5, 1500.52, 210°)` | Thư viện Kỵ Sĩ Đoàn (`outdoor_gps`: `-4374.0, -3018.0, 59.70`) |
| 6 | `klee` | Klee | `49440` | `mc_klee` (`custom_mods.img`) | `0` (`M1`) | `(-3880.0, -2545.0, 48.71, 270°)` | Bờ Hồ Sao Rơi (`Starfell Lake Statue Shore`) |
| 7 | `barbara` | Barbara | `49441` | `mc_barbara` (`custom_mods.img`) | `0` (`M0`) | `(-4444.5, -2937.0, 56.77, 255°)` | Sân thượng Đại Giáo Đường Tây Phong (`Cathedral Forecourt`) |
| 8 | `noelle` | Noelle | `49442` | `mc_noelle` (`custom_mods.img`) | `0` (`M0`) | `(-4364.5, -3025.5, 58.10, 45°)` | Sân tập Trụ sở Kỵ Sĩ Đoàn (`Knights HQ Courtyard`) |
| 9 | `fischl` | Fischl | `49443` | `mc_fischl` (`custom_mods.img`) | `0` (`M0`) | `(-4188.0, -3046.0, 6.56, 150°)` | Quảng trường Hiệp Hội Nhà Mạo Hiểm (đi kèm Oz 3D) |
| — | `oz` | Oz (Familiar) | `6702` (`CObject`) | `oz_static` (`mondstadt_m1_wilds.img`) | `0` (`M0`) | Bay lơ lửng cạnh vai phải Fischl | Kèm `COL3` `oz_static` trong `mondstadt_m1_wilds.col` |

---

## 3. Phím điều khiển trong game

- **Gặp gỡ trực tiếp trên bản đồ Mondstadt**:
  - Đứng cách NPC `<= 3.15m`: hiện thẻ nổi Persona `[E] TALK TO <NAME>` kèm avatar.
  - **`[E]`**: Bắt đầu cuộc gặp 3D Two-Shot + Persona CG HUD (mở khóa nhân vật vào `App #14` nếu là lần đầu).
  - **`[1] / [2] / [3] / [4]`** (hoặc `I/K` + `F9/Enter`): Chọn câu thoại gợi ý.
  - **`[F6]`**: Mở thanh gõ tin nhắn/thoại tự do trực tiếp bằng bàn phím -> `Enter` gửi cho `gpt-6-luna` (`Esc` hủy gõ).
  - **`[Backspace]` / `[F8]` / `[Tab]`**: Chào tạm biệt, trả lại góc camera và điều khiển cho Aether.
- **Điện thoại EaglePhone (`[F7]`) -> Ô `14.Contacts`**:
  - **`[J] / [L]`**: Chuyển giữa 3 tab `1.All (16)`, `2.Mondstadt (10)`, `3.Waifus (6)`.
  - **`[I] / [K]`**: Cuộn danh sách liên hệ.
  - **`[F9]` / `[Enter]`**:
    - Nếu liên hệ đang **`[LOCK]`**: Cắm mốc đỏ GPS tới vị trí nhân vật (hoặc cửa chính tòa nhà nếu ở trong nội thất).
    - Nếu là **Mondstadt `[OPEN]`**: Mở khung **Remote DM** nhắn tin từ xa (`[1..3]` chọn nhanh, `[F6]` gõ phím tự do, `[F10]` cắm GPS, `[Backspace]` quay lại danh sách).
    - Nếu là **Waifu `[OPEN]`**: Chuyển thẳng sang `App #13 WaifuLink` của nhân vật đó.

---

## 4. Kết quả kiểm thử & Bằng chứng nghiệm thu

### Part A — Kiểm thử Offline ngoài khóa (`staging/project-eagle/mondstadt-persona-chat-20261104/test_part_a_offline.py`)
- **`6/6` bài kiểm thử đạt 100% (`2.06s`)**:
  1. Kiểm tra đủ `61` sprite `512×512` alpha sạch + định dạng RenderWare D3D9 `MCSP0/1.TXD` (`1,048,744` bytes).
  2. Kiểm tra `20` file ped (`mc_*.dff/.txd`), `oz_static.{dff,txd}`, `5` file nội thất đã gỡ tượng tĩnh, `hud_candidate.txd`, `EAGLEPHONE_UI_candidate.TXD` và bytecode CLEO.
  3. Kiểm chứng toán học chiếu phối cảnh camera 3D Two-Shot cho cả `10/10` vị trí đứng (Aether và NPC luôn nằm gọn ở nửa trái `x_norm ∈ [0.12, 0.49]`, không che CG bên phải).
  4. Kiểm chứng bộ phân loại biểu cảm `classify_expression_and_anim` (bao gồm phát hiện Oz dịch lời -> `sprite_key = "oz"`) và bộ lọc `sanitize_cfont_text` an toàn 100% với `CFont`.
  5. Kiểm thử luồng E2E trên SQLite tạm: khóa ban đầu -> gặp mặt mở khóa -> lưu hội thoại SQLite -> nhắn tin từ xa trong `App #14` đọc đúng trí nhớ chung.
  6. Kiểm tra `py_compile` toàn bộ file Python và cân bằng cú pháp `hud.lua`.

### Part B — Nghiệm thu trực tiếp DirectX 9 `1920×1080` trong `gta_pe.exe` (`part_b_live_results.json`)
- Chạy dưới khóa `EagleCoordLock("ingame-runtime")`, đạt **PASS 100% (`112.9s`, `EagleLuaErrors.log = 0`)**, đã kiểm tra trực quan từng bức ảnh chụp thật:
  1. `qa_screenshots/01_venti_windrise_proximity_prompt.png`: Venti (`49434`, handle `3585`) dưới gốc Đại Thụ Phong Khởi nắng đẹp + thẻ nhắc `[E] TALK TO VENTI (2.1m) (New Encounter!)`.
  2. `qa_screenshots/02_venti_persona_hud_encounter.png`: Bấm `[E]` cắt camera Two-Shot nửa trái (Aether & Venti đối diện cử chỉ tay sống động) + toast `NEW SOCIAL LINK UNLOCKED: VENTI` + CG `512×512` Venti sắc nét bên phải + khung thoại đa giác Persona bên dưới.
  3. `qa_screenshots/03_venti_live_luna_expression_switch.png`: Chat tự do live với `gpt-6-luna` (*"Dandelion Wine, bright as the sun..."*) tự động đổi sang sprite Venti `happy` (`Warm / Happy`, `mc_sp_ver: 1 -> 3`).
  4. `qa_screenshots/04a_fischl_and_3d_oz_encounter.png`: Tại Hiệp Hội Nhà Mạo Hiểm (`M0`), Fischl (`49443`, handle `10753`) đứng cùng **Quạ Lôi Oz 3D (`6702`, `oz_handle=50945`)** bay lơ lửng ngay cạnh vai + giao diện Persona tím Electro.
  5. `qa_screenshots/04b_fischl_oz_portrait_reply.png`: Khi `gpt-6-luna` để Oz dịch lời (*`Oz: What Mein Fraulein means is...`*), bảng tên đổi sang `Oz` và CG `512×512` bên phải đổi trực tiếp sang chân dung **`Oz - Night Raven Familiar`**.
  6. `qa_screenshots/05_jean_knights_hq_indoor_dedup.png`: Bên trong Văn phòng Kỵ Sĩ Đoàn `INT-04` (`Area 1`, `Z=1500.52`), tượng tĩnh cũ đã biến mất hoàn toàn, chỉ còn Jean (`49435`, handle `8194`) & Lisa (`49439`, handle `8450`) sống động (`spawned_mask=34`, Oz & NPC ngoài trời tự ẩn `oz_handle=0`).
  7. `qa_screenshots/06a_eaglephone_home_app14_tile.png`: Màn hình chính EaglePhone hiển thị nút tròn **`14.Contacts`**.
  8. `qa_screenshots/06b_app14_contacts_directory.png`: Danh bạ `App #14` tab `2.Mondstadt` hiển thị `Venti [OPEN]`, `Jean [OPEN]`, `Diluc [LOCK] 778m` kèm cắm mốc đỏ GPS dẫn đường tới Tửu Trang Dawn.
  9. `qa_screenshots/06c_app14_remote_dm_venti.png`: Nhắn tin từ xa (`Remote DM`) với Venti ngay trên điện thoại, nối tiếp mạch hội thoại trước đó mà không cắt camera 3D.
- Sau khi chụp nghiệm thu xong, khối `finally` của script QA đã khôi phục trạng thái mở khóa của người chơi về nguyên bản `0/10` Mondstadt (`6/16` tổng cộng) để người dùng tự trải nghiệm mở khóa từ đầu khi vào game.

---

## 5. Manifest SHA-256 (Before / After) & Quy trình Rollback nguyên trạng

Toàn bộ bản sao trước khi sửa (`backups/`) và bảng đối chiếu SHA-256 đầy đủ nằm tại:
- [`staging/project-eagle/mondstadt-persona-chat-20261104/manifest_before_after.json`](../../staging/project-eagle/mondstadt-persona-chat-20261104/manifest_before_after.json)

| Tài nguyên trong `gameplay-lab` | Loại | SHA-256 Trước (`pristine`) | SHA-256 Sau (`applied`) |
|---|---|---|---|
| `EagleCompanion.py` | Sửa | `6373811a593bb534...` | `bd58f3f46f8a85d3...` |
| `hud.lua` | Sửa | `e0fbdf84dc0086d1...` | `03e83dd4e1e723a5...` |
| `eagle_phone_ui.py` | Sửa | `725b66f1b23ac3ee...` | `701f0e2f30991c96...` |
| `data/peds.ide` | Sửa | `d0c6891d8b00a832...` | `026e05f04eb6e8cb...` |
| `CUSTOM/mondstadt_m1_wilds.ide` | Sửa | `b7496e635125e3a5...` | `4cfffc87042b203c...` |
| `CUSTOM/custom_mods.img` | Sửa (`+20` entries) | `f5130730b6276d72...` | `cf90f81f3948f650...` |
| `CUSTOM/mondstadt_m1_wilds.img` | Sửa (`6` replaced, `+2` added) | `4177ee5b2aab8f0d...` | `ec5419af59db3847...` |
| `CUSTOM/mondstadt_m1_wilds.col` | Sửa (`+oz_static COL3`) | `b751fe2720f5e2c9...` | `446d290175615088...` |
| `cleo/MondstadtLifeAndBlips.cs` | Sửa | `72c282c90cf05668...` | `51547798dd151250...` |
| `models/hud.txd` | Sửa (`+12` icons) | `1fd202b0f7fa35b3...` | `79babd373cce40a6...` |
| `custom/EAGLEPHONE_UI.TXD` & `models/txd/EAGLEUI.TXD` | Sửa | `a3c3a41bc28ddf93...` | `6063e1114bfdd73a...` |
| `eagle_mondstadt_chat_bridge.py` | Thêm mới | — | `f10cc89f6cc1411f...` |
| `cleo/EagleMondstadtChatBridge.cs` | Thêm mới | — | `838ad8fab7fd3859...` |
| `models/txd/MCSP0.TXD` & `MCSP1.TXD` | Thêm mới (buffer động) | — | Ping-pong runtime `1,048,744 B` |
| `ui_assets/ep_ic_contacts.png`, `ep_bn_contacts.png`, `ep_mc_*.png` (`13` file) | Thêm mới | — | Xem `manifest_before_after.json` |

### Lệnh Rollback Bit-for-Bit (có giữ khóa `game-write.lock` & kiểm tra game đã đóng)
```powershell
python -X utf8 "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\mondstadt-persona-chat-20261104\rollback_mondstadt_persona_chat.py"
```
*(Lưu ý: Nếu các hội thoại WaifuLink / EaglePhone OS v6.0 sau thời điểm `15:10 UTC 04/11` có sửa tiếp `EagleCompanion.py`, `hud.lua` hoặc `eagle_phone_ui.py`, cần đọc hash thực tế trước khi chạy rollback tổng để không ghi đè thay đổi mới của agent khác.)*

---

## 6. Bản cập nhật theo phản hồi người dùng (`23:46 04/11/2026`): Sửa triệt để lỗi thủng nền 61 Sprite & Nâng Cỡ Chữ Lớn

1. **Nguyên nhân gốc & Cách sửa lỗi thủng/trong suốt trên Venti và các nhân vật tóc/áo tối màu (`build_sprites_and_ui_tex.py`)**:
   - **Nguyên nhân**: Các sprite sheet gốc (`1264×848`) dùng nền xanh đen `#061127` (`RGB ≈ [6, 17, 39]`, nhiễu biên 99th-percentile chỉ `<= 5.4` đơn vị RGB). Ngưỡng cũ (`tol_hard = 26.0`, `tol_soft = 46.0`, `hole_tol = 15.0`) quá rộng nên tràn qua nét vẽ viền anime đen (`dist ≈ 15..28`) và xóa nhầm mảng tóc xanh đen của Venti (`[10, 24, 50]`, `dist ≈ 13.6`), nơ tóc đen của Jean, kẹp dơi/ruy-băng của Fischl, áo sơ-mi đen của Diluc và bịt mắt của Kaeya.
   - **Cách sửa**: Thay bằng bộ tách silhouette chính xác (`tol_hard = 8.2` + hàng rào gradient viền `<= 7.5` + lọc khe hở khép kín ở vai tóc hai bím có kiểm tra chu vi da + ép cứng **`alpha = 255` đặc 100%** cho toàn bộ pixel bên trong nhân vật, chỉ khử răng cưa `1px` ngoài viền). Đã bổ sung kiểm tra tự động `0` lỗ thủng trong `test_part_a_offline.py` (`test_01`) và bảng kiểm chứng nền hồng neon `sprites_magenta_audit.png` / `venti_6_fullres_audit.png`.
2. **Tăng mạnh cỡ chữ & Mở rộng khung hiển thị (`hud.lua` + `eagle_mondstadt_chat_bridge.py`, tương thích 100% `EaglePhone OS v6.0 + Touchscreen`)**:
   - **Persona In-Person HUD (`DrawMondstadtPersonaHud`)**: Tăng khung đa giác lên `770 × 198` (`~1856 × 477 px` trên `1080p`); lời thoại chính `mc_l1..4` nâng từ `0.138, 0.298` lên **`0.312, 0.664` (`+126%`)**; bảng tên nhân vật `0.330, 0.700` (`+104%`); thanh lựa chọn `[1..4]` `0.252, 0.536` (`+97%`); tự động dời thẻ `MONDSTADT SOCIAL LINK` góc trái trên xuống dưới khi có banner sự kiện `ev_active == "1"`.
   - **Thẻ nhắc tiếp cận `[E] TALK TO ...`**: Tăng khung lên `468 × 46`, cỡ chữ chính nâng từ `0.142, 0.304` lên **`0.272, 0.578` (`+91%`)**.
   - **App #14 Danh Bạ (`Contacts` & `Remote DM`)**: Nâng tên liên hệ lên **`0.198, 0.420`**, chức danh/khoảng cách đầy đủ không cắt chữ lên **`0.162, 0.345`**, và nội dung bong bóng tin nhắn `Remote DM` nâng từ `0.108, 0.234` lên **`0.192, 0.408` (`+78%`, wrap `52` ký tự/dòng hiển thị trọn vẹn câu trả lời)**.
   - **Lọc sạch ký tự xuống dòng kép `\n`** từ LLM trong `sanitize_cfont_text` và tinh chỉnh bộ phân loại biểu cảm cho lời ca vui tươi.
3. **Manifest cập nhật (`staging/project-eagle/mondstadt-persona-chat-20261104/manifest_followup_20261104.json`)**:
   - `hud.lua`: `fb822da92df51707...` (merge trực tiếp trên `EaglePhone OS v6.0` `cd23edb54a2ea906...`)
   - `eagle_mondstadt_chat_bridge.py`: `cae381281060bce7...`
   - `models/hud.txd` (`296` textures): `f2f6474e10d6915c...`
   - `custom/EAGLEPHONE_UI.TXD` & `models/txd/EAGLEUI.TXD` (`50` textures): `8622d3329a2b8b93...`
   - Kiểm chứng lại đạt **Part A `6/6` PASS** và **Part B DirectX 9 `1920×1080` PASS (`110.5s`, `0` Lua errors)**.
