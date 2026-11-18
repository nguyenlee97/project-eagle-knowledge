# Mondstadt Character Batch 1 (`Sucrose`, `Diona`, `Amber`, `Eula`) & Giao thức `MCHT v2` (`30` NPC) — Báo Cáo Bàn Giao & Nghiệm Thu E2E

- **Ngày hoàn tất**: `2026-11-05` (`Asia/Saigon`, `UTC+7`)
- **Agent thực hiện**: Antigravity (`b0ff0420-2761-414d-86c7-2c9c95d13029`)
- **Trạng thái**: **`100% COMPLETED & VERIFIED (Offline Part A + Live gpt-6-luna + Live DirectX 9 1920×1080 Part B + Rollback Bit-for-Bit)`**
- **Đích tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục staging & backup**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\mondstadt-batch1-sucrose-diona-amber-eula-20261105\`
- **Phiếu điều phối**: `docs/project-eagle/work-items/2026-11-05-antigravity-mondstadt-batch1-sucrose-diona-amber-eula.md`

---

## 1. Tóm tắt Kết quả Bàn giao

1. **Mở rộng Hệ thống Character Brain `tools/eagle-character-chat` (`v0.3.4`, `10 -> 14` nhân vật Mondstadt, `120 -> 168` lựa chọn `adapted`)**:
   - Hoàn tất 4 hồ sơ nghiên cứu nguồn 4 bậc (`58` nguồn HTTPS) tại `staging/.../research/{sucrose,diona,amber,eula}.md`.
   - Bổ sung 4 cặp hồ sơ nhận thức 5 tầng (`schema_version: 1`) tại `content/characters/{sucrose,diona,amber,eula}.json` và `content/cognition/{sucrose,diona,amber,eula}.json`; cập nhật `content/world.json`, `content/cognition/world.json`, `tests/test_roster.py`, `tests/test_grounding.py`, `README.md`.
   - Kiểm thử unit suite: **`Ran 98 tests — OK`**; `node --check static/app.js`: **PASS**.
   - Đánh giá Live `gpt-6-luna` tuần tự trên SQLite tạm (`staging/.../live_eval/results.json`): **`20/20` lượt hội thoại thật PASS** (`0` rò rỉ thân phận `Barbatos` / `Darknight Hero`, `100%` tôn trọng cờ `requires_story`, `100%` đính chính tiền đề sai đúng giọng nhân vật, `100%` nhớ sở thích 2 lượt).
2. **Nâng cấp dứt điểm Cầu Bộ nhớ Chung CLEO `MCHT v2` (`768` byte, trần `30` NPC)**:
   - Biên dịch và triển khai `cleo/EagleMondstadtChatBridge.cs` (`15,285` B, `1,906` lệnh, `sha256=89c90a80ca8c...`): cấp phát `0AC8` `768` byte, đóng dấu `shm_version = 2` tại `shm+220`, `npc_capacity = 30` tại `shm+224`, mảng `ped_handles[0..29]` tại `shm+256..375` và `ped_ptrs[0..29]` tại `shm+384..503` (giữ tương thích 100% vùng `0..127` & `212..219`, không bao giờ đè lên `suppress_prompts` hay `python_heartbeat`).
   - Xác nhận trực tiếp trong `gta_pe.exe` ở `60 FPS`: `shm_ptr = 0x4213e070`, `shm_version = 2`, `npc_capacity = 30`.
3. **Đóng gói 4 Custom Ped 3D (`49444..49447`) & Khử nhân bản nội thất (`Zero-Clone`)**:
   - Đóng gói `mc_sucrose`, `mc_diona`, `mc_amber`, `mc_eula` (`.dff` + `.txd`, đủ `32` xương `Skin PLG` + `HAnim PLG`, toàn bộ raster nén `DXT1/DXT5 <= 512px`, vá bổ sung raster băng đô đỏ `HM_B_Headset` cho Amber) vào `CUSTOM/custom_mods.img` (`153 -> 161` entries) và khai báo `49444..49447` trong `data/peds.ide`.
   - Gỡ riêng tượng tĩnh **Diona (`AID #539022`)** khỏi `INT-05` `int_cats_tail.dff` trong `CUSTOM/mondstadt_m1_wilds.img`, **bảo toàn nguyên vẹn cả `6/6` chú mèo tĩnh Mondstadt (`AID #606769`)**.
   - Gỡ riêng tượng tĩnh **Sucrose (`AID #538867`)** khỏi `INT-06` `int_alchemy_lab.dff`, **bảo toàn nguyên vẹn Albedo (`AID #525577`)**.
4. **Kết xuất `24` Sprite Biểu Cảm `512×512` Đặc `100%` (`0` Lỗ Thủng Alpha) + `4` Icon Danh Bạ `ep_mc_*`**:
   - Dùng duy nhất subagent nội bộ `image-generator` của Antigravity sinh 4 bảng biểu cảm `3×2` (`sucrose`, `diona`, `amber`, `eula`), tách nền flood-fill có khóa đặc nội vùng `alpha = 255` sau bước lấy mẫu `LANCZOS` nâng tổng kho sprite Mondstadt từ **`61 -> 85` file** tại `data/project-eagle/character-chat/sprites/`.
   - Kiểm toán trực quan trên nền hồng `#FF00FF` (`staging/.../batch1_sprites_magenta_audit.png`) và kiểm định toán học trong `test_08`: **`85/85` sprite đạt `0` lỗ thủng nội vùng và `0` pixel bán trong suốt nội vùng**.
   - Đóng gói `ep_mc_sucrose`, `ep_mc_diona`, `ep_mc_amber`, `ep_mc_eula` (`128×128`) vào `models/hud.txd` (`300` textures), `custom/EAGLEPHONE_UI.TXD` và `models/txd/EAGLEUI.TXD` (`54` textures).
5. **Mở rộng `App #14 Contacts` (`16 -> 20` Liên hệ) trên nền `EaglePhone OS v6.3`**:
   - Nâng cấp phẫu thuật `eagle_mondstadt_chat_bridge.py`, `EagleCompanion.py`, `eagle_phone_ui.py` và `hud.lua`: hiển thị `All (20)` / `Mondstadt (14)` / `Waifus (6)`, bảo toàn `100%` tính năng cuộn bong bóng lịch sử DM `v6.3` (`Up / Dn / End` + thanh cuộn), cỡ chữ lớn (`0.312×0.664`) và hạ nhẹ trục nhìn camera Two-Shot nội thất cho mẫu nhí Katzlein `diona` (`cam_z = nz + 1.22`, `look_z = nz + 0.92`) để trọn khuôn mặt, mũ và tai mèo hiển thị rõ phía trên hộp thoại.
6. **Nghiệm thu E2E (`Part A` + `Rollback` + `Part B` DirectX 9 `1920×1080` + `Doctor`)**:
   - `test_part_a_offline.py` (chế độ nghiêm ngặt đủ `85/85` sprite, chạy sau chỉnh sửa cuối): **`8/8` nhóm PASS (`58.79s`)**.
   - `rollback_batch1.py`: Đã chạy thử nghiệm thực tế, khôi phục khớp `100%` SHA-256 bit-for-bit của cả 11 file gốc và dọn sạch 4 file thêm mới trước khi `apply_batch1.py` triển khai bản chốt.
   - `run_part_b_live_ingame_qa.py` (`1920×1080` DirectX 9 dưới `ingame-runtime.lock`): **`9/9` ảnh chụp trực tiếp trong game kiểm tra bằng mắt thật PASS** (`104.3s`), `EagleLuaErrors.log = 0`, `eagle_doctor.py` đạt **`11/11 PASS` (`0` cảnh báo, `0` crash)**.
   - Đã khôi phục nguyên trạng `data/project-eagle/character-chat/conversations.sqlite3` và dọn sạch `ingame_contacts_state.json`; giải phóng sạch cả hai khóa (`game-write = null`, `ingame-runtime = null`).

---

## 2. Thiết kế Giao thức `MCHT v2` (`768` Byte — Trần `30` NPC)

| Offset (Byte) | Kiểu | Trường dữ liệu | Ghi chú |
| :--- | :--- | :--- | :--- |
| `0..63` | `int32` / `float` | Header `v1/v2` (`magic=0x4D434854`, `cmd_seq`, ..., `heartbeat` @ `68`, `area_vis` @ `72`, `near_idx` @ `76`, `near_dist` @ `80`, `e_seq` @ `84`, `conv_act` @ `88`, `active_npc` @ `92`, `oz_handle` @ `96`, `spawned_mask` @ `112`) | Tương thích 100% với `MCHT v1`; `spawned_mask` dùng bit `0..29` cho tối đa `30` NPC. |
| `128..207` | `int32[10]` + `uint32[10]` | Legacy `v1` `ped_handles[0..9]` & `ped_ptrs[0..9]` | Đồng bộ song song cho `idx < 10`. |
| `212..219` | `uint32[2]` | `suppress_prompts` (`212`), `python_heartbeat` (`216`) | Python ghi mỗi nhịp bridge. |
| **`220..223`** | `int32` | **`shm_version = 2`** | Cờ nhận diện phiên bản `MCHT v2`. |
| **`224..227`** | `int32` | **`npc_capacity = 30`** | Trần cố định `30` NPC cho các batch tiếp theo (`idx 14..29`). |
| **`256..375`** | `int32[30]` | **`ped_handles[0..29]` (`v2`)** | Mảng 30 handle SCM không đụng độ vùng `212..227`. |
| **`384..503`** | `uint32[30]` | **`ped_ptrs[0..29]` (`v2`)** | Mảng 30 con trỏ `CPed*`. |
| `504..767` | `uint8[264]` | Vùng đệm dự phòng `v2` | Khởi tạo `0`. |

---

## 3. Bảng Tọa độ, Custom Ped `49444..49447` & Minh chứng Ảnh Chụp Trực Tiếp DirectX 9 (`1920×1080`)

| `idx` | Nhân vật | `Ped ID` / Model | Khu vực & Tọa độ (`X, Y, Z, hdg, area`) | Ảnh nghiệm thu DirectX 9 (`staging/project-eagle/mondstadt-batch1-sucrose-diona-amber-eula-20261105/qa_screenshots/`) |
| :---: | :--- | :--- | :--- | :--- |
| `10` | **Sucrose** | `49444` / `mc_sucrose` (`16,840V / 32B`) | Quầy Giả Kim Quảng trường trên `M0`: `(-4232.0, -3014.0, 12.60, 180.0, area=0)` + gỡ `#538867` trong `INT-06` (giữ Albedo `#525577`) | `03_sucrose_alchemy_terrace_encounter.png`, `03b_int06_alchemy_lab_albedo_zero_sucrose_clone.png` |
| `11` | **Diona** | `49445` / `mc_diona` (`13,792V / 32B`) | Quầy pha chế `INT-05` Cat's Tail: `(-4850.0, -3198.0, 1500.27, 180.0, area=1)`, `outdoor_gps=(-4152.0, -3064.0, 6.75)` + gỡ `#539022` (giữ `6/6` mèo `#606769`) | `04a_diona_cats_tail_prompt_6cats.png`, `04_diona_cats_tail_indoor_6cats.png` |
| `12` | **Amber** | `49446` / `mc_amber` (`12,483V / 32B`, `+HM_B_Headset`) | Cầu Đá Cổng Chính Mondstadt `M0`: `(-4143.0, -3059.5, 6.76, 255.0, area=0)` | `01_amber_main_gate_bridge_prompt.png`, `02_amber_persona_encounter_and_luna.png` |
| `13` | **Eula** | `49447` / `mc_eula` (`18,858V / 32B`) | Mũi đá tuần tra Hồ Sao Rơi `M1`: `(-3852.0, -2562.0, 48.71, 180.0, area=0)` (cách Klee `32.8m`) | `05_eula_starfell_lake_patrol.png` |
| — | **App #14** | `Contacts (20)` | Danh bạ `All (20)` / `Mondstadt (14)` / `Waifus (6)` + GPS cửa quán + DM cuộn `v6.3` dùng chung SQLite | `06a_app14_contacts_20_directory.png`, `06b_app14_remote_dm_shared_memory.png` |

---

## 4. Bảng SHA-256 Trước / Sau Triển Khai & Lệnh Phục Hồi (`Rollback`)

Chi tiết đầy đủ lưu tại `staging/project-eagle/mondstadt-batch1-sucrose-diona-amber-eula-20261105/manifest_before_after.json`:

| File trong `gameplay-lab` | `pristine_sha256` (Trước) | `after_sha256` (Sau) |
| :--- | :--- | :--- |
| `eagle_mondstadt_chat_bridge.py` | `945586e998c9b292...` | `cae275882321faa7...` |
| `EagleCompanion.py` | `92ad19beb48dba65...` | `d77c996330d46238...` |
| `eagle_phone_ui.py` | `701f0e2f30991c96...` | `d3563a6ad1c81d25...` |
| `hud.lua` | `0aa3f5a2202675b6...` | `d95879b12717219c...` |
| `data/peds.ide` | `026e05f04eb6e8cb...` | `1c066f329392e6fb...` |
| `cleo/EagleMondstadtChatBridge.cs` | `838ad8fab7fd3859...` | `89c90a80ca8c3e86...` |
| `CUSTOM/custom_mods.img` | `cf90f81f3948f650...` | `bea912134412a43c...` |
| `CUSTOM/mondstadt_m1_wilds.img` | `ec5419af59db3847...` | `635648fad0a5795a...` |
| `models/hud.txd` | `f2f6474e10d6915c...` | `521898168d0f7083...` |
| `custom/EAGLEPHONE_UI.TXD` & `models/txd/EAGLEUI.TXD` | `8622d3329a2b8b93...` | `b0f8c83d885d0076...` |

- **Lệnh hoàn tác an toàn có guard SHA-256** (chỉ thực hiện khi game đóng và giữ `game-write.lock`):
  ```powershell
  C:\Python310\python.exe "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\mondstadt-batch1-sucrose-diona-amber-eula-20261105\rollback_batch1.py"
  ```
