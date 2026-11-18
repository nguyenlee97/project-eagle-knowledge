# Báo Cáo Bàn Giao & Nghiệm Thu E2E: `Story Quest #1` (5 Chương Visual Novel) Cho Furina de Fontaine (`"Unscripted Encore"` — `v2.1.0` + `StoryQuestEngine v2.0` & `WaifuLink Card Hub v2.0`)

- **Ngày thực hiện & nghiệm thu hoàn tất:** 2026-11-06
- **Agent / Hội thoại triển khai:** Antigravity (`8e5d3ed7-64e4-486b-b230-0cbfe701122a`)
- **Hội thoại điều phối gốc (Orchestrator):** `35d5cf80-28f1-43e1-8e77-f60ee3d570c3`
- **Phiếu công việc:** [`work-items/2026-11-06-antigravity-story-quest-furina.md`](work-items/2026-11-06-antigravity-story-quest-furina.md)
- **Kinh thánh cốt truyện & DAG nhân quả (`v2.0 APPROVED — Round 2 100% PASS`):** [`story-quest-furina-5ch-narrative-and-causal-bible-2026-11-06.md`](story-quest-furina-5ch-narrative-and-causal-bible-2026-11-06.md)
- **Trình đọc HTML tương tác + Sơ đồ DAG + Gallery `45` CG:** [`furina-story-quest-5ch-full-preview.html`](furina-story-quest-5ch-full-preview.html) (`269,122` bytes)
- **Đích cài đặt thực tế:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Trạng thái khóa (`tools/eagle_coord_lock.py status`):** `{"game-write": null, "ingame-runtime": null}` (đã nhả sạch cả 2 khóa)

> [!TIP]
> **Hoàn tất 100% Bộ CG (`44/44` Story CGs + `1/1` Movie Poster = `45/45` tệp `1376x768` `.jpg` thật) & Nâng cấp `StoryQuestEngine v2.0`:**
> - Toàn bộ `45/45` hình ảnh đều được sinh **100% bằng subagent `image-generator` nội bộ của Antigravity** (tuân thủ tuyệt đối Luật Cứng Tạo Ảnh, truyền ảnh gốc HoYoverse `furina-official-directory.png` + `waifu_furina.png` + Base CG khóa góc máy, không dùng API ngoài, `0` chữ vẽ đè lên tranh, `45/45` mã SHA-256 duy nhất).
> - Đã bổ sung đầy đủ chuẩn Movie-Poster `StoryQuestEngine v2.0` trong [`eagle_story_quest_furina.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_story_quest_furina.py) (`518,093` bytes, `sha256=5909112918fa32f84475a3d9cfb34eef463186433101c6867833843c4de2e46b`) và nghiệm thu **PASS 100%** cả 3 tab của `PAGE_STORY_QUEST` trong `WaifuLink Card Hub v2.0`.

---

## 1. Kiến Trúc Zero-Core-Edit & Chuẩn Metadata `StoryQuestEngine v2.0`

Triển khai giữ nguyên **Zero-Core-Edit** (`0` dòng sửa đổi ngược lên `eagle_story_quest.py`, `EagleCompanion.py`, `eagle_dating_sim.py`, `hud.lua` hay `cleo/EagleWaifuCardHub.lua`):

1. **Metadata Movie-Poster & Tương thích Đa Chiến Dịch (`citlali`, `furina`, `hutao`):**
   - Tệp độc lập [`eagle_story_quest_furina.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_story_quest_furina.py) (`version = "2.1.0"`) export cả `STORY_QUEST_CAMPAIGN` và `STORY_QUEST_CAMPAIGNS = [STORY_QUEST_CAMPAIGN]`:
     - `"poster_cg": "ui_assets/story_quest_cgs/furina/furina_sq1_poster.jpg"` *(đồng bộ quy ước đường dẫn tương đối từ thư mục game như `eagle_story_quest_hutao.py` để `validate_campaign_pack(..., require_cgs_on_disk=True)` kiểm chứng trực tiếp trên đĩa đạt `errors = []`)*
     - `"title": "Unscripted Encore"` (`100%` ASCII `CFont` `0x20..0x7E`)
     - `"subtitle": "Scene 182,377 Beyond the Fountain of Tears"` (`100%` ASCII `CFont`)
     - `"synopsis"` (`251` ký tự, gói gọn thành đúng `4` dòng `wh_sq_syn1..4 <= 66` ký tự/dòng, không tiết lộ kết cục, `0` ký tự cấm `~ | *`, ngoặc cong hay em-dash):
       `"Past midnight by the Fountain of Lucine, five centuries of crystal tear-rime chill Furina's wrist and steal her sense of sweetness. Walk twelve Fontinalia days as her mortal co-star, gather hidden backstage clues, and brave the Solstice tide together."`
2. **Quy mô kịch bản & Hệ thống nhân quả (`v2.0` — `0% Dead Code`):**
   - `44/44` Scene Nodes (`N01..N44`) chia qua `5` Chương (`Ch1: 8`, `Ch2: 9`, `Ch3: 10`, `Ch4: 8`, `Ch5: 9`), **`573` nhịp văn học (Literary English)** sạch `100%` ASCII `CFont`.
   - `22` Cổng lựa chọn (`C01..C22`) + sự kiện tự động `N17` (`Second-Chance Sapphire Star Pin` trao `F07_SAPPHIRE_PIN` khi `BOND >= 11` & `INSIGHT >= 7`), `12` cờ nhân quả (`F01..F12`), `2` Cổng Kết Hợp Đa Chương (`C15_B_GATE1` & `C18_C_GATE2`), và `5` Kết thúc (`END_TRUE`, `END_GOOD`, `END_NEUTRAL` phân hoạch rời rạc `44A: 365 / 44B: 984 / 44C: 689`, `END_BAD_1`, `END_BAD_2`).

---

## 2. Kết Quả Kiểm Chứng Offline (`Part A`) & Nghiệm Thu Trực Tiếp DirectX 9 `1920x1080` (`Part B`)

### 2.1. Kiểm Chứng Offline Ngoài Khóa (`Part A — 100% PASS`)
- [`test_part_a_furina_sq_v2.py`](../../staging/project-eagle/story-quest-furina-impl-20261106/test_part_a_furina_sq_v2.py) (báo cáo JSON tại [`part_a_v2_verification_report.json`](../../staging/project-eagle/story-quest-furina-impl-20261106/part_a_v2_verification_report.json)):
  - `validate_campaign_pack(STORY_QUEST_CAMPAIGN, base_dir=GAME_ROOT, require_cgs_on_disk=True)` -> **`ok = True, errors = []`** (`44` nodes, `573` beats, **`45/45` tệp `.jpg` `1376x768` tồn tại thực tế với `45` SHA-256 duy nhất**).
  - Bố cục `build_causal_graph_2d("furina")`: `35` cột, `49` nút (`44` scene nodes + `5` ending badges), `50` cạnh nối nhân quả, **`0` cặp tọa độ `(col, lane)` đè nhau**, mọi `lane` nằm gọn trong `[0..4]`.
  - Lưu & tải `Manual Slot 1` trên SQLite tạm khôi phục chính xác `(node_id, beat_idx, bond, insight, flags, cg_rel)`; toàn bộ chuỗi `wh_*` / `sq_*` sạch `100%` `check_strict_cfont_string`.
- [`test_part_a_story_quest_furina.py`](../../staging/project-eagle/story-quest-furina-impl-20261106/test_part_a_story_quest_furina.py): **PASS** (`["citlali", "furina", "hutao"]` cùng hoạt động, mở khóa đủ `5/5` endings, `31` lượt voice trigger, cả 2 Micro-Guardrails PASS).

### 2.2. Nghiệm Thu In-Game DirectX 9 (`1920x1080`) Cả 3 Tab `WaifuLink Card Hub v2.0` (`Part B v2.0 — 5/5 Ảnh PASS`)
Thực thi qua [`run_live_card_hub_v2_furina_qa.py`](../../staging/project-eagle/story-quest-furina-impl-20261106/run_live_card_hub_v2_furina_qa.py) dưới `ingame-runtime.lock` (telemetry lưu tại [`qa_v2_live_results.json`](../../staging/project-eagle/story-quest-furina-impl-20261106/qa_v2_live_results.json)), kiểm tra trực tiếp bằng mắt toàn bộ ảnh tại [`qa_screenshots_v2/`](../../staging/project-eagle/story-quest-furina-impl-20261106/qa_screenshots_v2/):

| # | Tệp ảnh DirectX 9 (`1920x1080`) | Hạng mục nghiệm thu trên `PAGE_STORY_QUEST` (`WaifuLink Card Hub v2.0`) | Kết quả |
|---|---|---|---|
| `01` | `01_furina_sq_tab1_overview_poster.png` | **Tab `1. OVERVIEW & PLAY`:** Hiển thị sắc nét Poster điện ảnh `16:9` `furina_sq1_poster.jpg` (Sân khấu vàng Opera Epiclese + Đài phun nước Lucine dưới trăng), Title `Unscripted Encore`, Subtitle và `4` dòng `synopsis` cân đối, **không cắt chữ**, kèm nhạc nền Fontaine `Il Crepuscolo di Poisson` & `5` ô Ending | **PASS** |
| `02` | `02_furina_vn_seawall_pact_diff_cg.png` | Nhấn `START CHAPTER 1` chơi tới Cổng `C04` trên đê chắn sóng, hiển thị sắc nét tấm Diff CG mới vẽ `ch1_seawall_pact_diff.jpg` (`Bond 4 Insight 4 Clues 4/12`), lưu vào `Manual Slot 1` rồi đi tiếp sang Chương 2 (`N09`) | **PASS** |
| `03` | `03_furina_sq_tab2_causal_flowchart_2d.png` | **Tab `2. CAUSAL FLOWCHART 2D`:** Hiển thị `Columns 1-4 / 35` (`Progress: 20%`), các nút Chương 1 nối cạnh vàng **`0` node đè nhau**, nhấn `[TIME-JUMP HERE]` nhảy thẳng từ `N09` về đúng checkpoint `N02` | **PASS** |
| `04` | `04_furina_sq_tab3_saveload_slots.png` | **Tab `3. SAVE / LOAD SLOTS`:** Hiển thị tách biệt `AUTO-SAVE` (`Slot 0`) và `SAVE SLOT 1 - [CH1] Overlook Above the Terrestrial Sea` kèm ảnh thu nhỏ `16:9` `ch1_seawall_pact_diff.jpg` và các nút `[SAVE TO SLOT 1]` / `[LOAD SLOT]` / `[DELETE]` | **PASS** |
| `05` | `05_furina_slot1_restored_beat_and_cg.png` | Nhấn `[LOAD SLOT]` ở Tab 3 khôi phục chính xác từng trường dữ liệu: `N08` beat `0` (`[1/2]`), tranh `ch1_seawall_pact_diff.jpg`, `Bond 4`, `Insight 4`, `Clues 4/12` | **PASS** |

*(Cùng bộ `11/11` ảnh nghiệm thu VN đầy đủ các tính năng `[H]` Pure CG, `[B]` Backlog, `[J]` Flowchart Modal, Cổng Kết Hợp #1, `TRUE ENDING`, `BAD ENDING I` và giọng Nhật *CV: Inori Minase* tại [`qa_screenshots/`](../../staging/project-eagle/story-quest-furina-impl-20261106/qa_screenshots/).)*

- **Sức khỏe Hệ thống & Dọn Dẹp Sạch:** `CPad::UpdateMouse` (`0x0053F509`) khôi phục đúng `f3 a5`; `cleo/EagleLuaErrors.log` = **`0` lỗi**; `eagle_doctor.py` = **`11/11 PASS, 0 WARN, 0 FAIL`**; đã đóng sạch `gta_pe.exe` + `EagleCompanion.py`, khôi phục bản sạch `eagle_companion.db` / `waifulink.sqlite3` (`0` dòng test `char_id='furina'` trên mọi bảng kể cả `story_quest_save_slots`), reset `EaglePhoneHUD.dat` và nhả sạch cả 2 khóa.

---

## 3. Danh Mục Trọn Bộ `45/45` Tệp Ảnh `16:9` (`1376x768`) & Lệnh Rollback

Manifest băm SHA-256 đầy đủ (`pending_cgs = []`) nằm tại [`staging/project-eagle/story-quest-furina-impl-20261106/manifest.json`](../../staging/project-eagle/story-quest-furina-impl-20261106/manifest.json):
- **`1/1` Movie-Poster CG:** `ui_assets/story_quest_cgs/furina/furina_sq1_poster.jpg` (`351,454` bytes, `sha256=ed21dd8cce52d7908d3c11b450fb8609f23545e70dac0ba77c003efe8c63713d`).
- **`28/28` Base & Ending CGs:** Hoàn tất `100%`.
- **`16/16` Camera-Locked Diff CGs:** Hoàn tất `100%` (bao gồm cả `6` tấm vừa hoàn thiện: `ch1_seawall_pact_diff.jpg`, `ch2_opera_rime_cloth_diff.jpg`, `ch3a_footlights_vow_diff.jpg`, `ch4c_terrace_spill_diff.jpg`, `ch4c_terrace_close_avert_diff.jpg`, `ch5_royal_box_twin_plumes_diff.jpg`).

### Lệnh Rollback An Toàn Có Kiểm Tra SHA-256 (nếu cần gỡ riêng gói Furina `45` ảnh + module)
```powershell
python "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\story-quest-furina-impl-20261106\rollback_furina_sq1.py"
```
