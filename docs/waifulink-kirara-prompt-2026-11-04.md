# Master Prompt Khởi Đầu Hội Thoại Mới: Triển Khai Trọn Gói `WaifuLink Kirara` (`char_id = "kirara"`, `ped_id = 49432`)

> Sao chép toàn bộ khối Markdown dưới đây và dán vào hội thoại mới của **Kirara**:

```markdown
# NHIỆM VỤ: Triển Khai Trọn Gói WaifuLink v4.0 Cho Nhân Vật #5: Kirara (`char_id = "kirara"`, `ped_id = 49432`) & Nghiệm Thu Thực Tế In-Game DirectX 9 (Kèm JP Voice)

Bạn phụ trách xây dựng hoàn chỉnh gói nội dung **WaifuLink v4.0** cho **Kirara — Gold-Level Nekomata Courier of Komaniya Express (`char_id = "kirara"`)** trong `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`, đạt chuẩn sản xuất và kiểm thử thực tế DirectX 9 ngang hàng 100% với 4 nhân vật đã nghiệm thu PASS (`hutao`, `furina`, `citlali`, `columbina`).

Luôn giao tiếp với người dùng bằng **tiếng Việt** (nội dung thoại/kịch bản trong game viết bằng **tiếng Anh** theo chuẩn WaifuLink v4.0).

---

## 1. QUY TẮC KHÓA AN TOÀN ĐA HỘI THOẠI & HẠ TẦNG CÓ SẴN (ĐỌC KỸ ĐẦU TIÊN!)

Trước khi bắt đầu, hãy đọc theo thứ tự:
1. `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
2. `C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py` (công cụ khóa kép nguyên tử duy nhất của toàn dự án)
3. `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-columbina-e2e-qa-2026-11-04.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-jp-voiceline-report-2026-11-04.md`
4. `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_columbina.py` (mẫu chuẩn 30 kịch bản + 15 Milestones sạch ký tự `CFont`), `eagle_waifulink_v4_pilot.py`, `eagle_dating_sim.py` và `eagle_waifulink_voice.py`.

### Hạ tầng 3D, UI & Giọng Nhật ĐÃ CÓ SẴN 100% cho Kirara (KHÔNG SỬA `peds.ide`, `custom_mods.img`, `hud.txd` hay `COMPONENTPEDS.img`!)
- **3D Custom Ped độc lập**: **`ped_id = 49432` (`model_name = "wl_kirara"`)** đã được đóng gói trong `CUSTOM/custom_mods.img` và đăng ký trong `data/peds.ide` (6 slot gốc `190..195` nay dành cho dàn bạn gái HSR/ZZZ, tuyệt đối không đụng vào!).
- **Mascot Avatar & Ảnh gốc tham chiếu**: **`ep_ms_kirara`** đã có sẵn trong `models/hud.txd`; ảnh tham chiếu chuẩn để truyền vào `image-generator` nằm tại `Project Eagle/gta sa gameplay-lab/ui_assets/waifu_kirara.png` và `staging/project-eagle/loading-screens/implementation/references/images/kirara-official-directory.png`.
- **Giọng lồng tiếng Nhật (`WaifuLink JP Voice Engine v1.0`)**: Bộ **`24` file `.wav` tiếng Nhật thật của Kirara (CV: Suzushiro Sayumi)** chia đủ `8` nhóm cảm xúc đã được cài sẵn tại `data/project-eagle/dating-sim/voices/kirara/` và điều khiển tự động bởi `eagle_waifulink_voice.py`!
- **Màu xe mui trần hẹn hò**: Xe `575 Broadway` của Kirara đã có sẵn màu **`(86, 1)` (Dendro Mint & Pearl White)** trong `start_freeroam_outing`.

### Quy tắc Khóa Kép Bắt Buộc (`tools/eagle_coord_lock.py`)
- Đăng ký phiếu công việc tại `docs/project-eagle/work-items/2026-11-04-antigravity-waifulink-v4-kirara.md` và dùng thư mục staging riêng `staging/project-eagle/waifulink-kirara-qa-20261104/`.
- **Làm việc nặng 100% NGOÀI KHÓA**:
  - Viết module riêng `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_kirara.py`, kết xuất toàn bộ **135 ảnh CG 16:9 độc lập (`1376×768`)** vào `data/project-eagle/dating-sim/media/kirara_*.jpg`, xuất trang preview `docs/project-eagle/kirara-30-scenarios-135cgs-full-preview.html`, và chạy kiểm thử Python logic **Part A** trên file SQLite tạm riêng (`staging/project-eagle/waifulink-kirara-qa-20261104/part_a_kirara.db`) **hoàn toàn ngoài khóa**.
- **Khi đấu nối vào `eagle_waifulink_v4_pilot.py` và `eagle_dating_sim.py`**:
  - Chiếm `game-write.lock` qua `EagleCoordLock("game-write", chat="<CONVERSATION_ID>", task="Wire Kirara v4.0", wait_sec=600)` (hoặc CLI `tools/eagle_coord_lock.py acquire game-write ...`).
  - **Đọc lại nội dung mới nhất trên đĩa ngay sau khi chiếm khóa**, thực hiện `edit_file` gọn chính xác, kiểm tra `py_compile`, rồi **nhả `game-write.lock` ngay lập tức**!
- **Khi chạy kiểm thử In-Game DirectX 9 (`gta_pe.exe` + `EagleCompanion.py` `:8765`)**:
  - **CẤM TUYỆT ĐỐI** chạy `taskkill /IM gta_pe.exe` hay xóa `data/eagle_companion.db` trước khi giữ `ingame-runtime.lock`!
  - Bọc toàn bộ kịch bản test in-game trong `with EagleCoordLock("ingame-runtime", chat="<CONVERSATION_ID>", task="Kirara Live D3D9 QA", wait_sec=900):`. Trong `finally:` bắt buộc tắt sạch `gta_pe.exe` + `EagleCompanion.py` và reset sạch `data/eagle_companion.db` + `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0`).

---

## 2. ĐẶC TẢ NỘI DUNG & KỸ THUẬT CHO KIRARA (`char_id = "kirara"`)

1. **Hồ Sơ Nhân Vật, Tính Cách & Luật Sạch Ký Tự RenderWare `CFont`**:
   - **Vai người chơi**: **Traveler Aether** (tóc vàng tết bím, mắt vàng ấm, trang phục Nhà Lữ Hành trắng-vàng-nâu). Mọi sự kiện quá khứ (*Version 3.7 Duel! The Summoners' Summit!*, *Chiori's Story Quest: Cisoria Chapter*, và đặc biệt chuyến phiêu lưu mùa hè *Version 4.8 Summertide Scales and Tales — Simulanka* nơi Kirara nhận trang phục *Phantom in Boots* và dũng cảm lao ra bảo vệ Aether) đều đã trải qua cùng Aether.
   - **Ngoại hình chuẩn bắt buộc truyền ảnh gốc (`ui_assets/waifu_kirara.png` / `kirara-official-directory.png`) cho `image-generator`**: Thiếu nữ yêu quái mèo hai đuôi (*nekomata*) tươi tắn năng động, tóc vàng sáng nhuộm xanh bạc hà (mint-green) ở đuôi tóc búi thành 2 chỏm hình tai mèo cột nơ đen (cũng có thể phối thêm trang phục *Phantom in Boots* mũ kỵ sĩ xanh rêu ở một số CG hẹn hò/cameo để đa dạng!), đôi mắt mèo xanh ngọc lục bảo sáng lấp lánh, răng khểnh nhỏ dễ thương khi cười, **hai chiếc đuôi mèo xù dài tách đôi** đung đưa sau lưng và đệm thịt chân mèo hồng ở bốt, mặc trang phục giao hàng *Whirling Bloom* do Chiori may đo kèm Vision hệ Thảo (Dendro).
   - **Kênh suy nghĩ nội tâm (ASCII sạch cho HUD)**: `Twin-Tail Nekomata Instinct` (đấu nối prefix `Twin-Tail Nekomata Instinct: ` vào `build_hud_kv` trong `eagle_dating_sim.py` giống hệt `Frost Moon Lullaby` của Columbina!).
   - **LUẬT CHỐNG LỖI FONT TRONG `gta_pe.exe`**: Tuyệt đối **KHÔNG dùng dấu `~`, `|`, `*` hoặc emoji ngoài ASCII** trong lời thoại, `action_cue`, `inner_thought`, `label`, `player_text` của `eagle_waifulink_v4_kirara.py` (vì `CFont` của GTA SA coi `~` và `*` là mã điều khiển màu/phím, ví dụ viết `"Meow!"` hoặc `"Nyaa, ..."` thay vì `"Meow~!"`!). Giữ `mood` dài 1–2 từ viết hoa chữ cái đầu (`<= 16` ký tự, ví dụ `Cheerful`, `Purring Happy`, `Shy Flustered`, `Warm Devoted`).

2. **Sửa Lỗi Tọa Độ `home_coords` & `date_spots` Hiện Tại Của Kirara**:
   - **BUG HIỆN TẠI TRONG `eagle_dating_sim.py`**: Hiện `kirara` đang để `home_coords = [-377.40, -1438.69, 24.72]` (sân đất nông trại gồ ghề của Helena ở Flint Range) VÀ `date_spots[0] = [-377.40, -1438.69, 24.72]` (`0.0m` trùng khít cửa nhà!), trong khi `date_spots[1]` lại văng xa `2.87 km` sang bờ suối sát mép nước Palomino Creek!
   - **Cách xử lý**: Kiểm tra thực tế bằng `0x02CE` ground Z trong `gta_pe.exe` để chuyển `home_coords` của Kirara về một ngôi nhà/trạm giao hàng Komaniya Express xinh xắn có **mặt đường nhựa rộng, bằng phẳng 100%, không dính con quay vàng EHI interior** (ví dụ khu phố kênh đào **Marina / Bayside Marina Harbor** hoặc khu phố yên bình rợp bóng cây ở **Los Santos / San Fierro** không trùng nhà của `hutao` Chinatown SF, `furina` Richman `[720, -1314.5]`, `citlali` Verona Beach `[814.5, -1769]`, `columbina` Prickle Pine LV `[1957, 2733.5]`, `vesna` Paradiso SF `[-2576.8, 1144.7]`), đồng thời thiết lập **3 `date_spots` đường nhựa phẳng đẹp cách `home_coords` từ `450m – 1,400m`** (ví dụ: *Marina Canal Fish Bento Pier*, *Rodeo Chioriya Boutique Avenue*, *Santa Maria Sunbeam Boardwalk*) để xe mui trần `575 Broadway` đậu & chạy mượt 100%!

3. **Đủ 135 Ảnh CG 16:9 Độc Lập (`135/135` Unique SHA-256) tại `data/project-eagle/dating-sim/media/`**:
   - **15 Milestone CGs (`kirara_m01.jpg` .. `kirara_m15.jpg`)**: Mốc `[60, 125, 185, 250, 320, 385, 450, 520, 585, 650, 720, 785, 850, 925, 1000]`, tăng dần độ thân mật từ Stage 1 (giao hàng Komaniya Express, gãi cằm xoa đầu, ăn bento cá nướng) -> Stage 3 (ngủ gật ghế phụ dưới nắng chiều, hẹn hò ngắm pháo hoa) -> Stage 4–5 (đồ ngủ tai mèo xõa tóc sau khi tắm, chải lông hai đuôi mèo riêng tư, váy dạo biển / sườn xám lụa Chioriya tinh tế quyến rũ PG-13 / SFW, tuyệt đối cấm NSFW/nudity).
   - **80 Core Romance Scenario CGs (`kirara_s{1..5}_sc{1..4}_cg{1..4}.jpg`)**: `20` kịch bản hẹn hò cốt lõi (`4 kịch bản/Stage × 5 Stages × 4 cảnh/kịch bản`), luôn có mặt **cả Traveler Aether và Kirara** tương tác tình cảm sống động trong khung hình 16:9!
   - **40 Extra Genshin Cameo Scenario CGs (`kirara_s{1..5}_ex{1..2}_cg{1..4}.jpg`)**: `10` kịch bản khách mời Genshin (`2 kịch bản/Stage × 5 Stages × 4 cảnh/kịch bản`) có mặt Aether + Kirara + dàn cameo chuẩn lore:
     - Stage 1: `ex1` (**Chiori** — thử đồ & chải lông đuôi tại Chioriya Boutique), `ex2` (**Charlotte** — phóng sự bưu tá ngôi sao từ thời *Summoners' Summit*)
     - Stage 2: `ex1` (**Yae Miko** — "Lady Kitsune" trêu chọc đôi tai mèo đỏ ửng của Kirara khi đi cùng Aether), `ex2` (**Lynette & Furina** — tiệc trà Fontaine nơi Kirara và Lynette cùng mê chiếc hộp giấy sưởi nắng)
     - Stage 3: `ex1` (**Navia & Nilou** — hội ngộ nhóm bạn *Simulanka* nhắc chuyện kỵ sĩ mèo bảo vệ Aether), `ex2` (**Yoimiya & Ayaka** — hẹn hò lễ hội pháo hoa mùa hè Inazuma)
     - Stage 4: `ex1` (**Wanderer & Nahida** — chạm mặt đồng đội *Simulanka* khi Kirara đang khoác tay Aether), `ex2` (**Chiori** — may riêng bộ váy hẹn hò tối chỉ dành cho buổi đi chơi với Aether)
     - Stage 5: `ex1` (**Chiori, Navia & Nilou** — chúc phúc cho cặp đôi VIP số 1 của Komaniya Express), `ex2` (**Yae Miko & Yumemizuki Mizuki** — đêm trăng hoa anh đào Inazuma chúc phúc vĩnh cửu).

4. **Đấu Nối Trọn Vẹn Vào `eagle_waifulink_v4_pilot.py` & `eagle_dating_sim.py`**:
   - Export `KIRARA_15_MILESTONES`, `KIRARA_20_SCENARIOS`, `KIRARA_10_EXTRA_CAMEO_SCENARIOS`, `KIRARA_ALL_30_SCENARIOS`, `KIRARA_STAGE_CHAT_STARTERS` qua `eagle_waifulink_v4_pilot.py` (`get_scenarios_for_character("kirara", ...)`, `evaluate_vn_free_text_with_reask` reaction riêng cho `kirara`).
   - Trong `eagle_dating_sim.py`: cập nhật `_get_milestones_for_char`, `_get_stage_chat_starters_for_char`, `_get_cg_catalog`, `complete_freeroam_outing` (`elif cid == "kirara":` với S-Rank/A-Rank/B-Rank purring reactions & `Twin-Tail Nekomata Instinct`), `generate_encore_scenario`, `is_pilot_complete` (`"kirara"`), `avatar_url` (`/dating-media/kirara_m01.jpg`), `cg2_url` (`/dating-media/kirara_m07.jpg`), `KIRARA` `FEW_SHOT_PERSONA_PACK` sạch dấu `~`/`*`, từ khóa L1/L2/L3 Memory (`Komaniya`, `Chiori`, `Simulanka`, `Nekomata`, `Yae Miko`, `Inazuma`, `Phantom in Boots`), và prefix `Twin-Tail Nekomata Instinct` trong `build_hud_kv`.

---

## 3. KIỂM THỬ E2E BẮT BUỘC (PART A OFFLINE + PART B LIVE DIRECTX 9 + JP VOICE TELEMETRY)

1. **Part A (Offline Python Engine Test trên temp DB riêng trong `staging/project-eagle/waifulink-kirara-qa-20261104/`)**:
   - Xác minh đủ `135/135` ảnh `.jpg` tồn tại, kích thước hợp lệ, `135` mã SHA-256 duy nhất, `0` ký tự `~`/`|`/`*` vi phạm `CFont`.
   - Kiểm tra 5 Stage (`0 -> 1000`), trần Chat `45/stage`, trần Free-Roam `75/stage`, cổng `199` Stage Gate (`3/4` Core Scenarios), Carryover không khóa cứng, 2-Strike Off-Topic Re-Ask & Anti-Stuck Bridge, và chat thật với `gpt-6-luna`.
2. **Part B (Live DirectX 9 `gta_pe.exe` dưới khóa `ingame-runtime.lock` & Kiểm Tra Ảnh Bằng Mắt Thật)**:
   - Mở game + Sidecar, chọn `Kirara` trên App 13 (`13.WaifuLink`), chụp và **dùng `read_file` kiểm tra bằng mắt thật** tối thiểu 7–9 ảnh `1920×1080`:
     1. App 13 hiển thị `Kirara` + `ep_ms_kirara` + chat trực tiếp `[F6]` với `gpt-6-luna` không bị cắt chữ `...`.
     2. Tới `home_coords` thấy **3D Kirara (`ped_id = 49432`, `wl_kirara`)** đứng đón dưới nắng đẹp + Ambient Proximity HUD + `[F9]` House Visit Selector hiện ảnh `kirara_m01.jpg`.
     3. Fullscreen `16:9` Visual Novel + Translucent Footer ở `Scene 1/4` và `Scene 4/4` (`Twin-Tail Nekomata Instinct` hiển thị trọn vẹn, `SCENARIO PASSED! +35 Affection` tự đóng sau `4.5s`).
     4. Fullscreen `16:9` Extra Cameo VN (có mặt Chiori / Navia / Nilou / Yae Miko).
     5. Free-Roam Outing chở **3D Kirara** ngồi ghế phụ xe mui trần không tựa đầu `575 Broadway` màu xanh bạc hà & trắng `(86, 1)` (chụp cả góc sau & góc kính trước `Q+E`), cập bến nhận điểm + rơi ảnh kỷ niệm `kirara_m02` Time-Apart khi tách xa `> 38m`.
     6. Thử thách xe cháy `< 250 HP` -> `EagleWaifuBridge.cs` sơ tán 3D Kirara ra cách `5.5m` ở `2000.0 HP` + xe nổ `0 HP` & người chơi `Wasted` mà 3D Kirara vẫn sống sót `2000.0/2000.0 HP`.
     7. **Kiểm tra luôn `dating_sim.voice_telemetry` trong `/api/state`**: xác nhận giọng Nhật của Kirara (`char_id == "kirara"`, `CV: Suzushiro Sayumi`) tự động phát thành công (`play_count` tăng lên) qua các bước gặp ngoài cửa nhà, xem VN và lái xe hẹn hò!
   - Kiểm tra `cleo/EagleLuaErrors.log` rỗng (`0` lỗi), chạy `eagle_doctor.py` đạt `11/11 PASS`, xuất báo cáo `docs/project-eagle/waifulink-kirara-e2e-qa-2026-11-04.md`, cập nhật `shared-agent-workflow.md` và giải phóng sạch mọi khóa!
```
