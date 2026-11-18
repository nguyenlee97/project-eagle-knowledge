# Master Prompt Khởi Đầu Hội Thoại Mới: Triển Khai Trọn Gói Nhân Vật #6 (Mảnh Ghép Cuối Cùng 6/6) — `WaifuLink Vesna Strivozha` (`char_id = "vesna"`, `ped_id = 49433`)

> Sao chép toàn bộ khối Markdown dưới đây và dán vào hội thoại mới của **Vesna Strivozha**:

```markdown
# NHIỆM VỤ: Triển Khai Trọn Gói WaifuLink v4.0 Cho Nhân Vật #6 (Hoàn Tất Dàn 6/6): Vesna Strivozha (`char_id = "vesna"`, `ped_id = 49433`) & Nghiệm Thu Thực Tế In-Game DirectX 9 (Kèm JP Voice)

Bạn phụ trách xây dựng hoàn chỉnh gói nội dung **WaifuLink v4.0** cho mảnh ghép cuối cùng (`6/6`) của dàn bạn gái Project Eagle: **Vesna Strivozha — Snowy Banquet's Sharp Blade, Commander of the Druzhna (`char_id = "vesna"`)** trong `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`, đạt chuẩn sản xuất và kiểm thử thực tế DirectX 9 ngang hàng 100% với 5 nhân vật đã nghiệm thu PASS (`hutao`, `furina`, `citlali`, `columbina`, `kirara`).

Luôn giao tiếp với người dùng bằng **tiếng Việt** (nội dung thoại/kịch bản trong game viết bằng **tiếng Anh** theo chuẩn WaifuLink v4.0).

---

## 1. QUY TẮC KHÓA AN TOÀN ĐA HỘI THOẠI & HẠ TẦNG CÓ SẴN (ĐỌC KỸ ĐẦU TIÊN!)

Trước khi bắt đầu, hãy đọc theo thứ tự:
1. `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
2. `C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py` (công cụ khóa kép nguyên tử duy nhất của toàn dự án)
3. `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-kirara-e2e-qa-2026-11-04.md` và `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-jp-voiceline-report-2026-11-04.md`
4. `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_kirara.py` (mẫu chuẩn mới nhất 30 kịch bản + 15 Milestones sạch 100% ký tự `CFont`), `eagle_waifulink_v4_pilot.py`, `eagle_dating_sim.py` và `eagle_waifulink_voice.py`.

### Hạ tầng 3D, UI & Giọng Nhật ĐÃ CÓ SẴN 100% cho Vesna (KHÔNG SỬA `peds.ide`, `custom_mods.img`, `hud.txd` hay `COMPONENTPEDS.img`!)
- **3D Custom Ped độc lập**: **`ped_id = 49433` (`model_name = "wl_vesna"`)** đã được đóng gói trong `CUSTOM/custom_mods.img` và đăng ký trong `data/peds.ide` (6 slot gốc `190..195` nay dành cho dàn bạn gái HSR/ZZZ, tuyệt đối không đụng vào!).
- **Mascot Avatar**: **`ep_ms_vesna`** đã có sẵn trong `models/hud.txd`.
- **Giọng lồng tiếng Nhật (`WaifuLink JP Voice Engine v1.0`)**: Bộ **`24` file `.wav` tiếng Nhật thật của Vesna (CV: Aya Endo — chất giọng nữ chỉ huy quý tộc tinh nghịch, sắc sảo)** chia đủ `8` nhóm cảm xúc đã được cài sẵn tại `data/project-eagle/dating-sim/voices/vesna/` và điều khiển tự động bởi `eagle_waifulink_voice.py`!
- **Màu xe mui trần hẹn hò**: Xe `575 Broadway` của Vesna đã có sẵn màu **`(6, 1)` (Golden Amber & Pearl White)** trong `start_freeroam_outing`.

### Kho Ảnh Tham Chiếu Gốc BẮT BUỘC Truyền Cho `image-generator` (CỰC KỲ QUAN TRỌNG!)
Vì **Vesna Strivozha** cùng dàn nhân vật Snezhnaya Version 7.1 (**Danica**, **The Tsaritsa**, **Odette**, **Vodyanitsa**) là nhân vật đặc biệt có thiết kế chuẩn riêng trong kho của người dùng, khi gọi subagent `image-generator` vẽ `135` ảnh CG, **BẮT BUỘC truyền đường dẫn ảnh gốc tham chiếu** để giữ đúng 100% khuôn mặt, kiểu tóc và trang phục:
- **Vesna Strivozha** (bắt buộc truyền ở MỌI ảnh `135/135`):
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-screens\implementation\references\images\vesna-official-directory.png`
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-screens\implementation\references\images\vesna-official-trailer.jpg`
  - `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\ui_assets\waifu_vesna.png`
- **Danica** (Royal Head Housemaid — tóc bob xanh teal, mắt cyan-hồng, băng đô hầu gái trắng ngà):
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-batches\EXC06-20261103\references\danica-reveal.jpg`
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-batches\EXC06-20261103\references\danica.webp`
- **The Tsaritsa** (Nữ Hoàng Băng Giá Snezhnaya):
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-screens\implementation\references\images\tsaritsa-official-trailer.jpg`
- **Odette** (tóc xanh búi ballet có lọn xoăn, mắt tím violet, phụ kiện tóc vàng):
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-batches\EXC06-20261103\references\odette-user-hair.png`
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-batches\EXC06-20261103\references\odette.webp`
- **Vodyanitsa** (tóc xanh teal dài, mắt xanh biển, đôi hoa trắng cài tóc):
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-batches\EXC06-20261103\references\vodyanitsa.webp`
- **Columbina**:
  - `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-screens\implementation\references\images\columbina-official-directory.png`

### Quy tắc Khóa Kép Bắt Buộc (`tools/eagle_coord_lock.py`)
- Đăng ký phiếu công việc tại `docs/project-eagle/work-items/2026-11-05-antigravity-waifulink-v4-vesna.md` và dùng thư mục staging riêng `staging/project-eagle/waifulink-vesna-qa-20261105/`.
- **Làm việc nặng 100% NGOÀI KHÓA**:
  - Viết module riêng `Project Eagle/gta sa gameplay-lab/eagle_waifulink_v4_vesna.py`, kết xuất toàn bộ **135 ảnh CG 16:9 độc lập (`1376×768`)** vào `data/project-eagle/dating-sim/media/vesna_*.jpg`, xuất trang preview `docs/project-eagle/vesna-30-scenarios-135cgs-full-preview.html`, và chạy kiểm thử Python logic **Part A** trên file SQLite tạm riêng (`staging/project-eagle/waifulink-vesna-qa-20261105/part_a_vesna.db`) **hoàn toàn ngoài khóa**.
- **Khi đấu nối vào `eagle_waifulink_v4_pilot.py` và `eagle_dating_sim.py`**:
  - Chiếm `game-write.lock` qua `EagleCoordLock("game-write", chat="<CONVERSATION_ID>", task="Wire Vesna v4.0 (6/6 Finale)", wait_sec=600)`.
  - **Đọc lại nội dung mới nhất trên đĩa ngay sau khi chiếm khóa**, thực hiện `edit_file` gọn chính xác, kiểm tra `py_compile`, rồi **nhả `game-write.lock` ngay lập tức**!
- **Khi chạy kiểm thử In-Game DirectX 9 (`gta_pe.exe` + `EagleCompanion.py` `:8765`)**:
  - **CẤM TUYỆT ĐỐI** chạy `taskkill /IM gta_pe.exe` hay xóa `data/eagle_companion.db` trước khi giữ `ingame-runtime.lock`!
  - Bọc toàn bộ kịch bản test in-game trong `with EagleCoordLock("ingame-runtime", chat="<CONVERSATION_ID>", task="Vesna Live D3D9 QA", wait_sec=900):`. Trong `finally:` bắt buộc tắt sạch `gta_pe.exe` + `EagleCompanion.py` và reset sạch `data/eagle_companion.db` + `cleo/EaglePhoneHUD.dat` (`open=0, ev_active=0`).

---

## 2. ĐẶC TẢ NỘI DUNG & KỸ THUẬT CHO VESNA STRIVOZHA (`char_id = "vesna"`)

1. **Hồ Sơ Nhân Vật, Tính Cách & Luật Sạch Ký Tự RenderWare `CFont`**:
   - **Vai người chơi**: **Traveler Aether** (tóc vàng tết bím, mắt vàng ấm, trang phục Nhà Lữ Hành trắng-vàng-nâu). Mọi sự kiện quá khứ (*Story Quest Version 7.1: 'Swords and Secrets' Parts I–VII* dẹp loạn kiếm linh gia tộc Strivozha và âm mưu quân sự Snezhnaya, cùng cuốn cẩm nang trứ danh *'How to Handle Druzhna Commander Vesna'* do Hầu gái trưởng Danica viết) đều đã trải qua cùng Aether.
   - **Tính cách đặc trưng**: Tổng Tư lệnh Druzhna (đội cận vệ hoàng gia tinh nhuệ của Băng Thần Tsaritsa), mang huyết thống Vila (tiên tuyết cổ đại) và thanh kiếm *Beyond the Chrysalis* + Anemo Stellar Linchpin. Trên chiến trường uy nghiêm sắc bén bất khả chiến bại, nhưng khi tan ca đi riêng với Aether lại cực kỳ rạng rỡ, mê tốc độ cao, thích bày trò trêu chọc ngọt ngào (lén bỏ lát chanh chua hoặc vẽ hình trái tim bằng kem dưới đáy tách trà của Aether khi Danica không để ý, giơ huy hiệu Tư lệnh Druzhna bảo kê miễn trừ ngoại giao cho xe của Aether!).
   - **Kênh suy nghĩ nội tâm (ASCII sạch cho HUD)**: `Vila Blade's Resonance` (đấu nối prefix `Vila Blade's Resonance: ` vào `build_hud_kv` trong `eagle_dating_sim.py` giống hệt 5 nhân vật trước!).
   - **LUẬT CHỐNG LỖI FONT TRONG `gta_pe.exe`**: Tuyệt đối **KHÔNG dùng dấu `~`, `|`, `*` hoặc emoji ngoài ASCII** trong lời thoại, `action_cue`, `inner_thought`, `label`, `player_text` của `eagle_waifulink_v4_vesna.py` (đồng thời làm sạch luôn vài dấu `~` cũ trong `starter_messages`/`hangout_choices`/`voice_style` của `vesna` ở `eagle_dating_sim.py`!). Giữ `mood` dài 1–2 từ viết hoa chữ cái đầu (`<= 16` ký tự, ví dụ `Confident`, `Playful Tease`, `Noble Warmth`, `Shy Devoted`).

2. **Sửa Lỗi Tọa Độ `home_coords` & `date_spots` Hiện Tại Của Vesna**:
   - **BUG HIỆN TẠI TRONG `eagle_dating_sim.py`**: Hiện `vesna` đang để `home_coords = [-1398.10, 2636.87, 54.70]` (bãi đỗ đồn cảnh sát nhỏ ở El Quebrados) VÀ `date_spots[0] = [-1398.10, 2636.87, 54.70]` (`0.0m` trùng khít cửa nhà!), trong khi `date_spots[2]` (`[2127.40, 2378.20, 10.82]`) lại văng xa tới **`3.54 km` xuyên sa mạc sang tận Las Venturas**!
   - **Cách xử lý**: Kiểm tra thực tế bằng `0x02CE` ground Z trong `gta_pe.exe` để đặt `home_coords` của Vesna tại một dinh thự quý tộc / tư dinh chỉ huy ven biển thật đẹp, sang trọng, **mặt đường nhựa rộng phẳng 100%, không dính con quay vàng EHI interior** — ví dụ khu biệt thự đồi biển **Paradiso / Calton Heights / Esplanade North ở Bắc San Fierro** hoặc khu cảng du thuyền **Bayside Marina** (không trùng với `hutao` Chinatown SF, `furina` Richman LS, `citlali` Verona Beach LS, `columbina` Prickle Pine LV, `kirara` Marina Canal LS), kèm **3 `date_spots` đường nhựa phẳng đẹp cách `home_coords` từ `450m – 1,400m`** (ví dụ: *Golden Gate Battery Point Overlook*, *Esplanade North Coastal Highway*, *Palisades Aristocratic Tea Promenade*) để xe mui trần `575 Broadway` màu Vàng Hổ Phách & Trắng Ngọc Trai `(6, 1)` lướt êm ái!

3. **Đủ 135 Ảnh CG 16:9 Độc Lập (`135/135` Unique SHA-256) tại `data/project-eagle/dating-sim/media/`**:
   - **15 Milestone CGs (`vesna_m01.jpg` .. `vesna_m15.jpg`)**: Mốc `[60, 125, 185, 250, 320, 385, 450, 520, 585, 650, 720, 785, 850, 925, 1000]`, tăng dần độ thân mật từ Stage 1 (chào kiểu Tư lệnh Druzhna, trò đùa lát chanh dưới đáy tách trà, tập kiếm *Vila Blade Dance*) -> Stage 3 (đua xe mui trần ven biển hoàng hôn, khoác áo choàng lông trắng cho Aether dưới tuyết đầu mùa) -> Stage 4–5 (xõa mái tóc bạch kim ánh vàng sau giờ tháo quân phục, đầm dạ hội Snezhnaya / trang phục nghỉ dưỡng suối nước nóng mùa đông sang trọng quyến rũ PG-13 / SFW, tuyệt đối cấm NSFW/nudity).
   - **80 Core Romance Scenario CGs (`vesna_s{1..5}_sc{1..4}_cg{1..4}.jpg`)**: `20` kịch bản hẹn hò cốt lõi (`4 kịch bản/Stage × 5 Stages × 4 cảnh/kịch bản`), luôn có mặt **cả Traveler Aether và Vesna** tương tác tình cảm sống động trong khung hình 16:9!
   - **40 Extra Snezhnaya & Genshin Cameo Scenario CGs (`vesna_s{1..5}_ex{1..2}_cg{1..4}.jpg`)**: `10` kịch bản khách mời đặc sắc (`2 kịch bản/Stage × 5 Stages × 4 cảnh/kịch bản`) có truyền đúng ảnh tham chiếu gốc của từng khách mời:
     - Stage 1: `ex1` (**Danica** — Hầu gái trưởng Danica bắt quả tang Vesna vẽ trái tim dưới tách trà của Aether và rút sổ tay *'How to Handle Commander Vesna'*), `ex2` (**Childe / Tartaglia** — giao đấu kiếm thuật hữu nghị tại thao trường tuyết trắng)
     - Stage 2: `ex1` (**Odette** — buổi thưởng trà chiều và vũ điệu băng tuyết trên sân thượng khách sạn ven biển), `ex2` (**Vodyanitsa** — đêm nhạc nhà hát ven hồ nơi Vodyanitsa mỉm cười nhìn Vesna bối rối trước lời khen của Aether)
     - Stage 3: `ex1` (**Columbina** — Vesna múa kiếm dưới ánh trăng trong tiếng ngân nga dịu dàng của Columbina bên cạnh Aether), `ex2` (**Arlecchino** — cuộc gặp gỡ ngoại giao sắc sảo tại sảnh tiệc Snezhnaya nơi Vesna công khai đứng về phía Aether)
     - Stage 4: `ex1` (**Danica & Odette** — hai người bạn thân giúp Vesna chọn đầm dạ hội riêng tư cho buổi hẹn tối với Aether), `ex2` (**The Tsaritsa** — Băng Thần Tsaritsa ban đặc ân nghỉ phép hoàng gia cho Nữ Tư lệnh trung thành và Nhà Lữ Hành)
     - Stage 5: `ex1` (**Danica, Odette & Vodyanitsa** — tiệc chúc phúc mùa xuân *'Vesna'* rực rỡ tại cung điện băng), `ex2` (**The Tsaritsa & Columbina** — lời chúc phúc dưới bầu trời cực quang phương Bắc cho lưỡi kiếm sắc nhất của Snezhnaya và ngôi sao của cô ấy).

4. **Hoàn Tất Đấu Nối `6/6` Vào `eagle_waifulink_v4_pilot.py` & `eagle_dating_sim.py`**:
   - Export `VESNA_15_MILESTONES`, `VESNA_20_SCENARIOS`, `VESNA_10_EXTRA_CAMEO_SCENARIOS`, `VESNA_ALL_30_SCENARIOS`, `VESNA_STAGE_CHAT_STARTERS` qua `eagle_waifulink_v4_pilot.py` (`get_scenarios_for_character("vesna", ...)`, `evaluate_vn_free_text_with_reask` reaction riêng cho `vesna`).
   - Trong `eagle_dating_sim.py`: cập nhật `_get_milestones_for_char`, `_get_stage_chat_starters_for_char`, `_get_cg_catalog`, `complete_freeroam_outing` (`elif cid == "vesna":` với S-Rank/A-Rank/B-Rank high-speed commander reactions & `Vila Blade's Resonance`), `generate_encore_scenario`, nâng `is_pilot_complete` lên đủ **`("hutao", "furina", "citlali", "columbina", "kirara", "vesna")`** (`6/6` hoàn chỉnh!), `avatar_url` (`/dating-media/vesna_m01.jpg`), `cg2_url` (`/dating-media/vesna_m07.jpg`), `VESNA` `FEW_SHOT_PERSONA_PACK` sạch dấu `~`/`*`, từ khóa L1/L2/L3 Memory (`Druzhna`, `Strivozha`, `Danica`, `Tsaritsa`, `Vila`, `Odette`, `Vodyanitsa`, `Chrysalis`, `Snezhnaya`), và prefix `Vila Blade's Resonance` trong `build_hud_kv`.

---

## 3. KIỂM THỬ E2E BẮT BUỘC (PART A OFFLINE + PART B LIVE DIRECTX 9 + JP VOICE + KIỂM TRA TỔNG ĐÀI 6/6 ROSTER)

1. **Part A (Offline Python Engine Test trên temp DB riêng trong `staging/project-eagle/waifulink-vesna-qa-20261105/`)**:
   - Xác minh đủ `135/135` ảnh `vesna_*.jpg` tồn tại, kích thước hợp lệ, `135` mã SHA-256 duy nhất, `0` ký tự `~`/`|`/`*` vi phạm `CFont`, VÀ kiểm tra tổng thể cả **6/6 nhân vật (`6 × 135 = 810` ảnh CG)** đều báo `is_pilot_complete == True`!
   - Kiểm tra 5 Stage (`0 -> 1000`), trần Chat `45/stage`, trần Free-Roam `75/stage`, cổng `199` Stage Gate (`3/4` Core Scenarios), Carryover không khóa cứng, 2-Strike Off-Topic Re-Ask & Anti-Stuck Bridge, và chat thật với `gpt-6-luna`.
2. **Part B (Live DirectX 9 `gta_pe.exe` dưới khóa `ingame-runtime.lock` & Kiểm Tra Ảnh Bằng Mắt Thật)**:
   - Mở game + Sidecar, chọn `Vesna` trên App 13 (`13.WaifuLink`), chụp và **dùng `read_file` kiểm tra bằng mắt thật** tối thiểu 8–10 ảnh `1920×1080`:
     1. App 13 hiển thị `Vesna Strivozha` + `ep_ms_vesna` + chat trực tiếp `[F6]` với `gpt-6-luna` không bị cắt chữ `...`.
     2. Tới `home_coords` thấy **3D Vesna (`ped_id = 49433`, `wl_vesna`)** đứng đón dưới nắng đẹp + Ambient Proximity HUD + `[F9]` House Visit Selector hiện ảnh `vesna_m01.jpg`.
     3. Fullscreen `16:9` Visual Novel + Translucent Footer ở `Scene 1/4` và `Scene 4/4` (`Vila Blade's Resonance` hiển thị trọn vẹn, `SCENARIO PASSED! +35 Affection` tự đóng sau `4.5s`).
     4. Fullscreen `16:9` Extra Cameo VN (có mặt Danica / Tsaritsa / Odette / Vodyanitsa đúng thiết kế tham chiếu gốc!).
     5. Free-Roam Outing chở **3D Vesna** ngồi ghế phụ xe mui trần không tựa đầu `575 Broadway` màu Vàng Hổ Phách & Trắng `(6, 1)` (chụp cả góc sau & góc kính trước `Q+E`), cập bến nhận điểm + rơi ảnh kỷ niệm `vesna_m02` Time-Apart khi tách xa `> 38m`.
     6. Thử thách xe cháy `< 250 HP` -> `EagleWaifuBridge.cs` sơ tán 3D Vesna ra cách `5.5m` ở `2000.0 HP` + xe nổ `0 HP` & người chơi `Wasted` mà 3D Vesna vẫn sống sót `2000.0/2000.0 HP`.
     7. **Kiểm tra `dating_sim.voice_telemetry` trong `/api/state`**: xác nhận giọng Nhật của Vesna (`char_id == "vesna"`, `CV: Aya Endo`) tự động phát thành công (`mci_ok == True`, `play_count` tăng lên) qua các bước gặp ngoài cửa nhà, xem VN và lái xe hẹn hò!
   - Kiểm tra `cleo/EagleLuaErrors.log` rỗng (`0` lỗi), chạy `eagle_doctor.py` đạt `11/11 PASS`, xuất báo cáo `docs/project-eagle/waifulink-vesna-e2e-qa-2026-11-05.md`, cập nhật `shared-agent-workflow.md` + `docs/project-eagle/README.md` ghi dấu mốc **Hoàn tất 100% dàn 6/6 bạn gái WaifuLink v4.0 (`810` CGs + `144` JP Voices)** và giải phóng sạch mọi khóa!
```
