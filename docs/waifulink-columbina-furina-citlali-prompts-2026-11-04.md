# Bộ 3 Master Prompts Triển Khai & Tích Hợp Song Song: `Columbina`, `Furina`, `Citlali` (2026-11-04)

Tài liệu này chứa **3 bản Copy-Paste Prompt hoàn chỉnh, độc lập 100%** để dán trực tiếp vào 3 hội thoại riêng biệt:
1. **PROMPT 1**: Triển khai mới trọn gói **WaifuLink v4.0 — Columbina (`columbina`, `ped_id = 49431`)** (`135` CGs + module Python + tích hợp runtime + E2E QA In-Game).
2. **PROMPT 2**: Tích hợp hoàn chỉnh & Nghiệm thu In-Game cho **Furina de Fontaine (`furina`, `ped_id = 49428`)** (dành cho hội thoại của Furina).
3. **PROMPT 3**: Tích hợp hoàn chỉnh & Nghiệm thu In-Game cho **Citlali — Granny Itztli (`citlali`, `ped_id = 49430`)** (dành cho hội thoại của Citlali).

> [!IMPORTANT]
> Cả 3 bản Prompt đều đã được nhúng sẵn:
> - **Bảng Custom Ped ID 3D độc lập mới (`49428..49433` trong `CUSTOM/custom_mods.img` + `data/peds.ide`)** và **Mascot Avatar `ep_ms_<char_id>` đã build sẵn trong `models/hud.txd`** (tách biệt hoàn toàn khỏi 6 cô bạn gái gốc GTA SA `190..195` nay đã đổi sang dàn HSR/ZZZ).
> - **Quy tắc Khóa Kép Bắt Buộc (`game-write.lock` + `ingame-runtime.lock` qua `tools/eagle_coord_lock.py`)** để 3–4 hội thoại chạy song song không bao giờ ghi đè file hay giết nhầm phiên `gta_pe.exe` của nhau.

---

## PROMPT 1 — Dán Vào Hội Thoại Mới Để Triển Khai `WaifuLink Columbina`

```markdown
# NHIỆM VỤ: Triển Khai Trọn Gói WaifuLink v4.0 Cho Nhân Vật #4: Columbina (`char_id = "columbina"`, `ped_id = 49431`) & Nghiệm Thu Thực Tế In-Game

Bạn phụ trách xây dựng hoàn chỉnh gói nội dung **WaifuLink v4.0** cho **Columbina Hyposelenia — Kuutar / Damselette (`char_id = "columbina"`)** trong `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`, đạt chuẩn sản xuất và kiểm thử DirectX 9 thực tế y hệt **Hu Tao (`hutao`)**, **Furina (`furina`)** và **Citlali (`citlali`)**.

Luôn giao tiếp với người dùng bằng **tiếng Việt** (nội dung thoại/kịch bản trong game viết bằng **tiếng Anh** theo chuẩn WaifuLink v4.0).

---

## 1. QUY TẮC KHÓA AN TOÀN ĐA HỘI THOẠI (BẮT BUỘC TUÂN THỦ 100%)

Hiện có 3–4 hội thoại đang chạy song song trên cùng workspace. Trước khi làm bất cứ việc gì, hãy đọc:
1. `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
2. `C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py`
3. `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-hutao-e2e-qa-and-app13-2026-11-03.md`
4. `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_citlali.py` (mẫu chuẩn 30 kịch bản + 15 Milestones) và `eagle_dating_sim.py`
5. `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-hutao-qa-20261103\verify_chat_freeroam_immortal_waifu.py` & `verify_vn_fullscreen_footer.py` (mẫu script test DirectX 9).

- **Đăng ký phiếu công việc**: `docs/project-eagle/work-items/2026-11-04-antigravity-waifulink-v4-columbina.md`.
- **Hạ tầng 3D & UI đã được chuẩn bị sẵn cho Columbina (KHÔNG CẦN SỬA `peds.ide`, `custom_mods.img` hay `hud.txd`!)**:
  - Model 3D riêng của Columbina đã được đăng ký sẵn ở **`ped_id = 49431` (`model_name = "wl_columbina"`)** trong `CUSTOM/custom_mods.img` và `data/peds.ide`! (Không dùng slot `194 CROGRL3` cũ vì `190..195` nay dành cho 6 bạn gái HSR/ZZZ).
  - Avatar mascot **`ep_ms_columbina`** đã có sẵn trong `models/hud.txd`, và ảnh tham chiếu gốc nằm tại `Project Eagle/gta sa gameplay-lab/ui_assets/waifu_columbina.png` (cùng `staging/project-eagle/loading-screens/implementation/references/images/columbina-official-directory.png`).
- **Làm việc nặng 100% NGOÀI KHÓA**:
  - Viết module riêng `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_columbina.py`, kết xuất toàn bộ **135 ảnh CG 16:9 độc lập** vào `data/project-eagle/dating-sim/media/columbina_*.jpg`, tạo trang HTML preview `docs/project-eagle/columbina-30-scenarios-135cgs-full-preview.html`, và chạy kiểm thử Python logic **Part A** trên file SQLite tạm riêng (`staging/project-eagle/waifulink-columbina-qa-20261104/part_a_columbina.db`) **hoàn toàn ngoài khóa**.
- **Khi sửa `eagle_waifulink_v4_pilot.py` và `eagle_dating_sim.py`**:
  - Chiếm `game-write.lock` qua `python "C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py" acquire game-write --chat "<CONVERSATION_ID>" --task "Wire Columbina v4.0" --wait 600`.
  - **Đọc lại file mới nhất trên đĩa ngay sau khi chiếm khóa**, thực hiện `edit_file` gọn chính xác, kiểm tra `py_compile`, rồi `release game-write` ngay lập tức!
- **Khi chạy kiểm thử In-Game DirectX 9 (`gta_pe.exe` + `EagleCompanion.py` `:8765`)**:
  - **CẤM TUYỆT ĐỐI** gọi `taskkill /IM gta_pe.exe` hay xóa `data/eagle_companion.db` trước khi giữ `ingame-runtime.lock`!
  - Bọc toàn bộ kịch bản test in-game trong `with EagleCoordLock("ingame-runtime", chat="<CONVERSATION_ID>", task="Columbina Live D3D9 QA", wait_sec=900):`. Trong `finally:` bắt buộc tắt sạch `gta_pe.exe` + `EagleCompanion.py` và reset sạch `data/eagle_companion.db` + `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0`).

---

## 2. ĐẶC TẢ NỘI DUNG & KỸ THUẬT CHO COLUMBINA (`char_id = "columbina"`)

1. **Hồ Sơ Nhân Vật & Quy Tắc Ký Tự RenderWare `CFont` (CỰC KỲ QUAN TRỌNG)**:
   - **Vai người chơi**: **Traveler Aether** (tóc vàng tết bím, mắt vàng ấm, trang phục Nhà Lữ Hành trắng-vàng-nâu). Mọi sự kiện quá khứ (*A Winter Night's Lazzo*, *Nod-Krai Archon Quests: An Elegy of Dust and Lamplight & Voyage to the Frost Moon*, tái sinh thành *Kuutar — New Moon*) đều đã trải qua cùng Aether.
   - **Ngoại hình chuẩn bắt buộc truyền ảnh gốc (`ui_assets/waifu_columbina.png`) cho `image-generator`**: Tóc đen dài chấm thắt lưng ánh tím hồng (magenta), làn da trắng ánh trăng, mạng che mắt ren trắng mắt cáo kèm **6 cánh chim bồ câu Seraphim trắng** sau đầu (ở Stage 4–5 khi ở riêng bên Aether có thể khẽ nâng mạng ren hé mở đôi mắt sáng dịu dàng nhìn Aether).
   - **Kênh suy nghĩ nội tâm**: `🕊️ Frost Moon Lullaby`.
   - **LUẬT CHỐNG LỖI FONT TRONG `gta_pe.exe`**: Trong toàn bộ lời thoại, `action_cue`, `label`, `player_text` của `eagle_waifulink_v4_columbina.py`, **hạn chế dùng dấu `~`, `|`, `*` ở giữa câu** (vì `CFont` của GTA SA coi `~` và `*` là mã điều khiển màu/phím, còn `|` hiển thị thành `°`; `hud.lua` đã có bộ lọc nhưng viết sạch ASCII + câu gọn rõ ngay từ nguồn sẽ đẹp nhất!). Giữ `mood` dài 1–2 từ viết hoa chữ cái đầu (`<= 16` ký tự, ví dụ `Serene`, `Warm Dreamy`, `Shy Tender`).

2. **Kiểm Tra & Chuẩn Hóa Tọa Độ `home_coords` & `date_spots` Của Columbina**:
   - **CẢNH BÁO BUG HIỆN TẠI TRONG `eagle_dating_sim.py`**: Hiện `columbina` đang có `home_coords = [2035.36, 2732.41, 9.82]` (Prickle Pine, Las Venturas) VÀ `date_spots[0] = [2035.36, 2732.41, 9.82]` (`0.0m` cách cửa nhà -> sẽ vi phạm điều kiện cách nhà `> 80m` của Free-Roam Outing!).
   - Hãy đổi `date_spots` của Columbina thành **3 địa điểm đường nhựa bằng phẳng, rộng rãi tại Las Venturas / Bayside cách `home_coords` từ `450m – 1,800m`** (ví dụ: *The Visage Marble Fountain Promenade*, *Pirates in Men's Pants Lagoon Bridge*, *Emerald Isle / Roca Escalante Starlight Boulevard*), đảm bảo không đè lên con quay vàng EHI interior và xe mui trần `575 Broadway` đậu phẳng 100% không nghiêng lật!

3. **Đủ 135 Ảnh CG 16:9 Độc Lập (`135/135` Unique SHA-256) tại `data/project-eagle/dating-sim/media/`**:
   - **15 Milestone CGs (`columbina_m01.jpg` .. `columbina_m15.jpg`)**: Mốc `[60, 125, 185, 250, 320, 385, 450, 520, 585, 650, 720, 785, 850, 925, 1000]`, tăng dần độ thân mật từ Stage 1 (dịu dàng đời thường) tới Stage 5 (lãng mạn quyến rũ PG-13 / SFW tinh tế, tuyệt đối cấm NSFW/nudity).
   - **80 Core Romance Scenario CGs (`columbina_s{1..5}_sc{1..4}_cg{1..4}.jpg`)**: `20` kịch bản hẹn hò cốt lõi (`4 kịch bản/Stage × 5 Stages × 4 cảnh/kịch bản`), luôn có mặt **cả Traveler Aether và Columbina** tương tác tình cảm trong khung hình 16:9!
   - **40 Extra Genshin Cameo Scenario CGs (`columbina_s{1..5}_ex{1..2}_cg{1..4}.jpg`)**: `10` kịch bản khách mời Genshin (`2 kịch bản/Stage × 5 Stages × 4 cảnh/kịch bản`) có mặt Aether + Columbina + dàn cameo chuẩn lore:
     - Stage 1: `ex1` (**Childe / Tartaglia**), `ex2` (**Wanderer**)
     - Stage 2: `ex1` (**Arlecchino**), `ex2` (**Lyney, Lynette & Freminet**)
     - Stage 3: `ex1` (**Sandrone**), `ex2` (**Venti & Zhongli**)
     - Stage 4: `ex1` (**Childe — bắt gặp nắm tay dưới tuyết**), `ex2` (**Arlecchino — tiệc trà trăng đỏ chấp thuận**)
     - Stage 5: `ex1` (**Arlecchino, Childe, Lyney & Lynette chúc phúc**), `ex2` (**Frost Moon & Seelie Benediction dưới cực quang**).

4. **Đấu Nối Đầy Đủ Vào `eagle_waifulink_v4_pilot.py` & `eagle_dating_sim.py`**:
   - Đăng ký `COLUMBINA_15_MILESTONES`, `COLUMBINA_20_SCENARIOS`, `COLUMBINA_10_EXTRA_CAMEO_SCENARIOS`, `COLUMBINA_STAGE_CHAT_STARTERS` vào:
     - `get_scenarios_for_character("columbina", ...)` trong `eagle_waifulink_v4_pilot.py`
     - `_get_milestones_for_char`, `_get_stage_chat_starters_for_char`, `_get_cg_catalog`, `generate_encore_scenario`, `is_pilot_complete` (`"columbina"`), `avatar_url` (`/dating-media/columbina_m01.jpg`), `cg2_url` (`/dating-media/columbina_m07.jpg`), màu xe `575 Broadway` trắng bạc ánh hồng cho Columbina trong `start_freeroam_outing`, và từ khóa L1/L2/L3 Memory (`Nod-Krai`, `Kuutar`, `Frost Moon`, `Damselette`, `Arlecchino`, `Childe`).

---

## 3. KIỂM THỬ E2E BẮT BUỘC (PART A OFFLINE + PART B LIVE DIRECTX 9 SCREENSHOTS)

1. **Part A (Offline Python Engine Test trên temp DB riêng trong `staging/project-eagle/waifulink-columbina-qa-20261104/`)**:
   - Kiểm tra đủ `135/135` ảnh `.jpg` tồn tại, kích thước hợp lệ, `135` mã SHA-256 duy nhất.
   - Kiểm tra 5 Stage (`0 -> 1000`), trần Chat `45/stage`, trần Free-Roam `75/stage`, cổng `199` Stage Gate (`3/4` Core Scenarios), Carryover không khóa cứng, 2-Strike Off-Topic Re-Ask & Anti-Stuck Bridge, và chat thật với `gpt-6-luna`.
2. **Part B (Live DirectX 9 `gta_pe.exe` dưới khóa `ingame-runtime.lock`)**:
   - Mở game + Sidecar, chọn `Columbina` trên App 13 (`13.WaifuLink`), chụp và **đọc kiểm tra bằng mắt thật (`read_file` ảnh PNG)** tối thiểu 7 ảnh `1920×1080`:
     1. App 13 hiển thị `Columbina` + `ep_ms_columbina` + chat trực tiếp `[F6]` với `gpt-6-luna` không bị cắt chữ `...`.
     2. Tới trước cửa biệt thự Prickle Pine LV thấy **3D Columbina (`ped_id = 49431`, `wl_columbina`)** đứng đón + Ambient Proximity HUD + `[F9]` House Visit Selector hiển thị CG `columbina_m01.jpg`.
     3. Fullscreen `16:9` Visual Novel + Translucent Footer ở `Scene 1/4` và `Scene 4/4` (`SCENARIO PASSED! +35 Affection` tự đóng sau `4.5s`).
     4. Fullscreen `16:9` Extra Cameo VN (có mặt khách mời Harbingers/Archons).
     5. Free-Roam Outing chở **3D Columbina** ngồi ghế phụ xe mui trần không tựa đầu `575 Broadway` (chụp góc sau & góc kính lái trước `Q+E`), cập bến nhận điểm + rơi ảnh kỷ niệm `columbina_m02` khi tách xa.
     6. Thử thách xe cháy `< 250 HP` -> `EagleWaifuBridge.cs` sơ tán 3D Columbina ra cách `5.5m` ở `2000.0 HP` + xe nổ `0 HP` & người chơi `Wasted` mà 3D Columbina vẫn sống sót `2000.0/2000.0 HP`.
   - Kiểm tra `cleo/EagleLuaErrors.log` rỗng (`0` lỗi), `eagle_doctor.py` `11/11 PASS`, cập nhật báo cáo bàn giao và giải phóng sạch mọi khóa!
```

---

## PROMPT 2 — Dán Vào Hội Thoại Của `Furina` Để Hoàn Tất Tích Hợp & Nghiệm Thu In-Game

```markdown
# NHIỆM VỤ: Hoàn Tất Tích Hợp Runtime & Nghiệm Thu Thực Tế In-Game DirectX 9 Cho Furina (`char_id = "furina"`, `ped_id = 49428`)

Gói nội dung `eagle_waifulink_v4_furina.py` và bộ `135` ảnh CG (`data/project-eagle/dating-sim/media/furina_*.jpg`) đã được tạo trước đó, nhưng sau ngày `01/11`, hạ tầng **WaifuLink v4.0** trên `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` đã có **4 nâng cấp kiến trúc lớn** (đã nghiệm thu 100% trên Hu Tao ngày `03–04/11/2026`). Nhiệm vụ của bạn là rà soát, đồng bộ toàn diện **Furina** lên chuẩn mới nhất và chạy kiểm thử thực tế DirectX 9 trong `gta_pe.exe` chụp ảnh nghiệm thu bằng mắt thật!

Luôn giao tiếp với người dùng bằng **tiếng Việt**.

---

## 1. QUY TẮC KHÓA AN TOÀN ĐA HỘI THOẠI (3–4 CONVERSATIONS ĐANG CHẠY CÙNG LÚC!)

1. Đọc ngay từ đầu:
   - `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
   - `C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py`
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-hutao-e2e-qa-and-app13-2026-11-03.md` (Báo cáo chi tiết toàn bộ 13 lỗi runtime + Fullscreen 16:9 VN + `575 Broadway` + `EagleWaifuBridge.cs` `2000 HP`)
   - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-hutao-qa-20261103\verify_chat_freeroam_immortal_waifu.py` & `verify_vn_fullscreen_footer.py` (mẫu test runner DirectX 9).
2. Tạo phiếu công việc `docs/project-eagle/work-items/2026-11-04-antigravity-furina-ingame-integration-and-qa.md` và thư mục staging riêng `staging/project-eagle/waifulink-furina-qa-20261104/`.
3. **Thông tin Model 3D mới cực kỳ quan trọng**:
   - 6 slot bạn gái gốc GTA SA (`190..195`) nay đã được đổi sang dàn nhân vật HSR/ZZZ. Model 3D riêng của **Furina** đã được tách sang Custom Ped ID độc lập **`ped_id = 49428` (`model_name = "wl_furina"`)** trong `CUSTOM/custom_mods.img` và `data/peds.ide`! Avatar **`ep_ms_furina`** cũng đã có sẵn trong `models/hud.txd`. Tuyệt đối không sửa ngược `ped_id` của Furina về `193` và không đụng `COMPONENTPEDS.img` hay gói presentation `03/11`!
4. **Quy tắc 2 Khóa Bắt Buộc (`tools/eagle_coord_lock.py`)**:
   - Chạy kiểm tra script/text audit và Part A Python E2E trên file SQLite tạm riêng (`staging/project-eagle/waifulink-furina-qa-20261104/part_a_furina.db`) **100% NGOÀI KHÓA**.
   - Khi sửa `eagle_waifulink_v4_furina.py` (file riêng của bạn) không cần khóa; nhưng khi sửa `eagle_dating_sim.py` hoặc `EagleCompanion.py`, **bắt buộc chiếm `game-write.lock`**, **đọc lại nội dung mới nhất trên đĩa ngay trước khi `edit_file`**, kiểm tra `py_compile`, rồi **nhả `game-write.lock` ngay lập tức**.
   - Khi mở `gta_pe.exe` + `EagleCompanion.py` (`:8765`) để chạy Part B In-Game DirectX 9 QA: **CẤM TUYỆT ĐỐI** gọi `taskkill /IM gta_pe.exe` hay xóa `data/eagle_companion.db` khi chưa giữ `ingame-runtime.lock`! Bắt buộc bọc toàn bộ bài test in-game trong:
     ```python
     with EagleCoordLock("ingame-runtime", chat="<CONVERSATION_ID>", task="Furina Live D3D9 QA", wait_sec=900):
         ...
     ```
     Và trong khối `finally:` phải tắt sạch `gta_pe.exe` + `EagleCompanion.py`, xóa DB test về mặc định và sync sạch `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0`).

---

## 2. DANH SÁCH 5 HẠNG MỤC CẦN RÀ SOÁT & FIX CHO FURINA

1. **Rà soát & Chuẩn Hóa Tọa Độ Thực Địa `home_coords` & `date_spots` của Furina trong `eagle_dating_sim.py`**:
   - **Vấn đề hiện tại**: `home_coords` của Furina đang đặt ở đồi dốc Richman LS (`[321.5, -1180.2, 80.9]`), trong khi `date_spots[0]` (`[-2576.81, 1144.74, 54.74]`) và `date_spots[1]` (`[-1726.20, 1362.40, 7.18]`) lại văng sang tận **San Fierro** cách gần `4 km`! Ngoài ra mặt đường dốc ở Richman dễ làm xe mui trần `575 Broadway` bị nghiêng khi warp.
   - **Cách xử lý**: Kiểm tra thực tế trong `gta_pe.exe` (dùng `0x02CE` ground Z / matrix phẳng) để tinh chỉnh `home_coords` của Furina tại vị trí sân/đường bằng phẳng đẹp ngay trước biệt thự sang trọng ở Richman / Rodeo / Mulholland LS (không dính con quay vàng EHI interior!) VÀ cập nhật cả **3 `date_spots` của Furina về khu vực Los Santos / Santa Maria Lighthouse / Verona Beach Promenade / Rodeo Patisserie Boulevard** cách `home_coords` từ `450m – 1,600m` trên mặt đường nhựa rộng phẳng!
   - Cấu hình màu sơn xe `575 Broadway` riêng cho Furina trong `start_freeroam_outing` (ví dụ xanh dương Fontaine & trắng ngọc trai).

2. **Quét Sạch Ký Tự Dễ Lỗi RenderWare `CFont` & Độ Dài Dòng Trong `eagle_waifulink_v4_furina.py`**:
   - Kiểm tra toàn bộ `15` Milestones, `30` Scenarios (`120` scenes) và `FURINA_STAGE_CHAT_STARTERS`: loại bỏ các ký tự `~`, `|`, `*` thừa hoặc emoji không cần thiết trong các trường hiển thị lên HUD DirectX 9 (`proactive_action_cue`, `mood`, `label`, `player_text`), đảm bảo `mood` gọn 1–2 từ (`<= 16` ký tự) và không câu Quick-Chat nào bị cắt lửng vô nghĩa.

3. **Kiểm Tra Đấu Nối Khởi Tạo DB `m01`, Time-Apart Photo Drops & L1/L2/L3 Memory**:
   - Đảm bảo khi chọn `Furina` trên App 13 (`J/L` ở dòng 1 App 13 hoặc `/api/dating/select`), Furina có sẵn mốc khởi đầu chuẩn v4.0 (`furina_m01` mở khóa, 3 `reaction_choices` của `m01` hiện lên `[1]/[2]/[3]`), Time-Apart Milestone Photo Drop tự nổ `furina_m02` kèm ảnh preview 16:9 khi đạt `>= 125` Affection và cách xa `> 38m` sau `10s`, và `Dynamic AI Encore` hiển thị đúng CG của Furina.

4. **Chạy Part A (Deterministic Engine E2E trên Temp DB)**:
   - Kiểm tra toàn bộ 30 kịch bản (`135/135` file `.jpg` tồn tại & hash duy nhất), Stage Gate `199 -> 200` (`3/4` Core Scenarios), Carryover VN, trần Chat `45` / Free-Roam `75`, 2-Strike Off-Topic Re-Ask + Anti-Stuck Bridge, và live `gpt-6-luna` chat.

5. **Chạy Part B (Live DirectX 9 `gta_pe.exe` E2E dưới `ingame-runtime.lock` & Kiểm Tra Ảnh Bằng Mắt Thật)**:
   - Chụp và dùng `read_file` kiểm tra trực quan từng bức ảnh `1920×1080` trong `staging/project-eagle/waifulink-furina-qa-20261104/live_screenshots/`:
     1. `furina_01_app13_live_ai_chat.png`: Mở EaglePhone App 13 chuyển sang **Furina** (`ep_ms_furina` hiển thị đúng góc phải), gõ `[F6]` chat thật với `gpt-6-luna` + bấm `[1]` Turn-2, xác nhận lời thoại nhiều dòng & 3 gợi ý không bị cắt chữ `...`.
     2. `furina_02_doorstep_3d_and_selector.png`: Tới `home_coords` thấy **3D Furina (`ped_id = 49428`, `wl_furina`)** đứng đón ngoài đời thực + Ambient Proximity HUD + `[F9]` House Visit Selector hiện ảnh `furina_m01.jpg`.
     3. `furina_03_vn_fullscreen_scene1_and_4.png` (2 ảnh Scene `1/4` & Scene `4/4`): Fullscreen `16:9` Visual Novel (`1024×512` `WLCG0/1.TXD`) + khung thoại kính mờ trong suốt ở đáy ảnh + tên `Furina` + `ep_ms_furina` + tự đóng sau `4.5s`.
     4. `furina_04_vn_cameo_fontaine.png`: Fullscreen `16:9` Extra Cameo VN (có mặt Neuvillette / Navia / Clorinde / Charlotte).
     5. `furina_05_freeroam_3d_broadway_rear_and_front.png` (2 ảnh góc sau & góc kính trước `Q+E`): Chở **3D Furina** trên xe mui trần không tựa đầu `575 Broadway` dưới nắng đẹp, thấy rõ mặt & mũ/trang phục Fontaine của Furina ngồi bên cạnh nhân vật chính, lộ trình GPS tới điểm hẹn LS, chấm hạng va chạm & rơi ảnh kỷ niệm `furina_m02` Time-Apart!
     6. `furina_06_burning_car_and_wasted_immortal.png` (2 ảnh Torture A & B): Xe cháy `< 250 HP` -> `EagleWaifuBridge.cs` sơ tán 3D Furina cách `5.5m` ở `2000.0 HP` (`[ALERT] FURINA SAFE` / Waifu Safe); xe nổ `0 HP` + người chơi `Wasted` (`player_hp = 0.0`) mà **3D Furina vẫn sống sót 100% nguyên vẹn ở `2000.0/2000.0 HP`**, `0` lỗi Lua, `0` crash!
   - Cập nhật phiếu công việc & báo cáo `docs/project-eagle/waifulink-furina-ingame-qa-2026-11-04.md`, chạy `eagle_doctor.py` xác nhận `11/11 PASS` và nhả sạch mọi khóa.
```

---

## PROMPT 3 — Dán Vào Hội Thoại Của `Citlali` Để Hoàn Tất Tích Hợp & Nghiệm Thu In-Game

```markdown
# NHIỆM VỤ: Hoàn Tất Tích Hợp Runtime & Nghiệm Thu Thực Tế In-Game DirectX 9 Cho Citlali (`char_id = "citlali"`, `ped_id = 49430`)

Gói nội dung `eagle_waifulink_v4_citlali.py` và bộ `135` ảnh CG (`data/project-eagle/dating-sim/media/citlali_*.jpg`) đã được tạo ngày `02/11`, nhưng sau đó ngày `03–04/11/2026` hệ thống **WaifuLink v4.0** trên `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` đã được nâng cấp toàn diện (Fullscreen 16:9 Translucent Footer VN, App 13 6-line uncut `[F6]` live AI chat, chở 3D Waifu trên xe mui trần không tựa đầu `575 Broadway`, và cầu CLEO bất tử 3 lớp `cleo/EagleWaifuBridge.cs` `2000 HP`). Nhiệm vụ của bạn là rà soát, sửa các lỗi tọa độ/tích hợp còn tồn đọng của **Citlali**, và chạy nghiệm thu thực tế DirectX 9 trong `gta_pe.exe` có kiểm tra ảnh chụp bằng mắt thật!

Luôn giao tiếp với người dùng bằng **tiếng Việt**.

---

## 1. QUY TẮC KHÓA AN TOÀN ĐA HỘI THOẠI (3–4 CONVERSATIONS ĐANG CHẠY CÙNG LÚC!)

1. Đọc ngay từ đầu:
   - `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
   - `C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py`
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-hutao-e2e-qa-and-app13-2026-11-03.md`
   - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-hutao-qa-20261103\verify_chat_freeroam_immortal_waifu.py` & `verify_vn_fullscreen_footer.py`.
2. Tạo phiếu công việc `docs/project-eagle/work-items/2026-11-04-antigravity-citlali-ingame-integration-and-qa.md` và thư mục staging riêng `staging/project-eagle/waifulink-citlali-qa-20261104/`.
3. **Thông tin Model 3D & Mascot mới cực kỳ quan trọng**:
   - 6 slot bạn gái gốc GTA SA (`190..195`) nay đã được đổi sang dàn HSR/ZZZ. Model 3D riêng của **Citlali** đã được tách sang Custom Ped ID độc lập **`ped_id = 49430` (`model_name = "wl_citlali"`)** trong `CUSTOM/custom_mods.img` và `data/peds.ide`, đồng thời avatar **`ep_ms_citlali`** đã được đóng gói sẵn trong `models/hud.txd`! Tuyệt đối không đổi ngược `ped_id` về `195` và không đụng `COMPONENTPEDS.img` hay gói presentation `03/11`!
4. **Quy tắc 2 Khóa Bắt Buộc (`tools/eagle_coord_lock.py`)**:
   - Thực hiện audit văn bản và chạy Part A Python E2E trên file SQLite tạm riêng (`staging/project-eagle/waifulink-citlali-qa-20261104/part_a_citlali.db`) **100% NGOÀI KHÓA**.
   - Khi sửa `eagle_dating_sim.py` hoặc `EagleCompanion.py`, **bắt buộc chiếm `game-write.lock`**, **đọc lại nội dung mới nhất trên đĩa ngay trước khi `edit_file`**, kiểm tra `py_compile`, rồi **nhả `game-write.lock` ngay lập tức**.
   - Khi mở `gta_pe.exe` + `EagleCompanion.py` (`:8765`) chạy Part B In-Game DirectX 9 QA: **CẤM TUYỆT ĐỐI** gọi `taskkill /IM gta_pe.exe` hay xóa `data/eagle_companion.db` khi chưa giữ `ingame-runtime.lock`! Bắt buộc bọc toàn bộ bài test in-game trong:
     ```python
     with EagleCoordLock("ingame-runtime", chat="<CONVERSATION_ID>", task="Citlali Live D3D9 QA", wait_sec=900):
         ...
     ```
     Và trong khối `finally:` phải tắt sạch `gta_pe.exe` + `EagleCompanion.py`, xóa DB test về mặc định và sync sạch `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0`).

---

## 2. DANH SÁCH 5 HẠNG MỤC CẦN RÀ SOÁT & FIX CHO CITLALI

1. **Sửa Lỗi Tọa Độ `date_spots[0]` Trùng `home_coords` & Kiểm Tra Thực Địa Cho Citlali trong `eagle_dating_sim.py`**:
   - **BUG ĐÃ PHÁT HIỆN**: Hiện trong `ROSTER_6_GIRLFRIENDS`, `citlali` đang có `home_coords = [2401.96, -1723.22, 12.60]` (Ganton LS) VÀ `date_spots[0] = {"id": "citlali_home", "coords": [2401.96, -1723.22, 12.60]}` (`0.0m` cách cửa nhà!).
   - **Cách xử lý**: Thay `date_spots[0]` sang một địa điểm hẹn hò hợp tính cách Bà Ngoại Itztli cách nhà `500m – 1,500m` trên mặt đường nhựa rộng phẳng ở Los Santos (ví dụ *Santa Maria Stargazing Pier*, *Glen Park Mystic Pond Boulevard*, cùng *Verdant Bluffs Star Observatory* & *Verona Beach Sunset Pier*), đồng thời kiểm tra `home_coords` trong game đảm bảo không dính con quay vàng EHI interior của nhà Denise gốc (nếu sát cửa nhà Denise ở Ganton có marker hoặc hẻm hẹp dễ kẹt xe `575 Broadway`, hãy dịch `home_coords` sang căn biệt thự biển yên tĩnh Santa Maria / Verona Beach hoặc mặt đường rộng sạch ngay gần đó!).
   - Cấu hình màu sơn xe `575 Broadway` riêng cho Citlali trong `start_freeroam_outing` (tím pastel / xanh ngọc Night-Wind).

2. **Quét Sạch Ký Tự Dễ Lỗi RenderWare `CFont` & Độ Dài Dòng Trong `eagle_waifulink_v4_citlali.py`**:
   - Kiểm tra toàn bộ `15` Milestones, `30` Scenarios (`120` scenes) và `CITLALI_STAGE_CHAT_STARTERS`: loại bỏ các ký tự `~`, `|`, `*` gây lỗi token trong `CFont`, đảm bảo `mood` gọn 1–2 từ (`<= 16` ký tự) và không lựa chọn Quick-Chat nào bị cắt cụt.

3. **Kiểm Tra Đấu Nối Khởi Tạo DB `m01`, Time-Apart Photo Drops & Telepathy Inner-Thought**:
   - Đảm bảo khi chuyển sang `Citlali` trên App 13 (`J/L` dòng 1 App 13 hoặc `/api/dating/select`), Citlali có sẵn `citlali_m01` + 3 `reaction_choices` chuẩn v4.0, hiển thị đúng `🔮 Obsidian Mirror's Telepathy` trong VN footer, và tự động đẩy thông báo ảnh kỷ niệm `citlali_m02` kèm ảnh CG preview sau `10s` ở xa (`> 38m`) khi đạt `>= 125` Affection.

4. **Chạy Part A (Deterministic Engine E2E trên Temp DB)**:
   - Xác minh đủ `135/135` ảnh `.jpg` tồn tại & hash duy nhất, kinh tế 3 trụ cột (`45` chat cap, `75` outing cap, `3/4` Stage Gate clamp ở `199`), Carryover VN, 2-Strike Off-Topic Re-Ask + Anti-Stuck Bridge, và live `gpt-6-luna` chat.

5. **Chạy Part B (Live DirectX 9 `gta_pe.exe` E2E dưới `ingame-runtime.lock` & Kiểm Tra Ảnh Bằng Mắt Thật)**:
   - Chụp và dùng `read_file` kiểm tra trực quan từng bức ảnh `1920×1080` trong `staging/project-eagle/waifulink-citlali-qa-20261104/live_screenshots/`:
     1. `citlali_01_app13_live_ai_chat.png`: Mở EaglePhone App 13 chọn **Citlali** (`ep_ms_citlali` hiển thị đúng góc phải), gõ `[F6]` chat trực tiếp với `gpt-6-luna` + bấm `[1]` Turn-2, lời thoại nhiều dòng & 3 câu gợi ý không bị cắt chữ `...`.
     2. `citlali_02_doorstep_3d_and_selector.png`: Tới `home_coords` thấy **3D Citlali (`ped_id = 49430`, `wl_citlali`)** đứng đón ngoài map + Ambient Proximity HUD + `[F9]` House Visit Selector hiện ảnh `citlali_m01.jpg`.
     3. `citlali_03_vn_fullscreen_scene1_and_4.png` (2 ảnh Scene `1/4` & Scene `4/4`): Fullscreen `16:9` Visual Novel (`1024×512` `WLCG0/1.TXD`) + khung thoại kính mờ trong suốt ở đáy ảnh + tên `Citlali` + `ep_ms_citlali` + tự đóng sau `4.5s`.
     4. `citlali_04_vn_cameo_natlan.png`: Fullscreen `16:9` Extra Cameo VN (có mặt Ororon / Mavuika / Xilonen / Mualani / Kachina).
     5. `citlali_05_freeroam_3d_broadway_rear_and_front.png` (2 ảnh góc sau & góc kính trước `Q+E`): Chở **3D Citlali** ngồi ghế phụ xe mui trần không tựa đầu `575 Broadway` dưới nắng đẹp, thấy rõ mái tóc hồng-xanh ngọc của Citlali ngồi bên cạnh nhân vật chính, lộ trình GPS, chấm hạng va chạm & rơi ảnh kỷ niệm `citlali_m02` Time-Apart!
     6. `citlali_06_burning_car_and_wasted_immortal.png` (2 ảnh Torture A & B): Xe cháy `< 250 HP` -> `EagleWaifuBridge.cs` sơ tán 3D Citlali cách `5.5m` ở `2000.0 HP`; xe nổ `0 HP` + người chơi `Wasted` (`player_hp = 0.0`) mà **3D Citlali vẫn sống sót 100% nguyên vẹn ở `2000.0/2000.0 HP`**, `0` lỗi Lua, `0` crash!
   - Cập nhật phiếu công việc & báo cáo `docs/project-eagle/waifulink-citlali-ingame-qa-2026-11-04.md`, chạy `eagle_doctor.py` xác nhận `11/11 PASS` và nhả sạch mọi khóa.
```
