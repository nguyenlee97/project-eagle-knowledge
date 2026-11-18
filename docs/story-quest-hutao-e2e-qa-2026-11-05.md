# Báo Cáo Bàn Giao & Nghiệm Thu E2E: `Story Quest Engine v1.0` + Chiến Dịch Visual Novel 5 Chương Hu Tao (`"Where the Papilio Rests"`)

- **Ngày hoàn tất:** 2026-11-05
- **Agent / Hội thoại triển khai:** Antigravity (`8b77c600-9e8a-4800-a63d-1b995675e60a`)
- **Hội thoại điều phối gốc (Orchestrator):** `35d5cf80-28f1-43e1-8e77-f60ee3d570c3`
- **Phiếu công việc:** [`work-items/2026-11-05-antigravity-story-quest-hutao-implementation.md`](work-items/2026-11-05-antigravity-story-quest-hutao-implementation.md)
- **Kinh thánh cốt truyện & DAG nhân quả (`v2.1 APPROVED`):** [`story-quest-hutao-5ch-narrative-and-causal-bible-2026-11-05.md`](story-quest-hutao-5ch-narrative-and-causal-bible-2026-11-05.md)
- **Trình đọc HTML tương tác + Sơ đồ DAG + Gallery 42 CGs:** [`hutao-story-quest-5ch-full-preview.html`](hutao-story-quest-5ch-full-preview.html)
- **Đích cài đặt thực tế:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Trạng thái khóa (`tools/eagle_coord_lock.py status`):** `{"game-write": null, "ingame-runtime": null}` (đã giải phóng sạch cả 2 khóa)

---

## 1. Tổng Quan Kiến Trúc `Story Quest Engine v1.0` (Plug-and-Play 100% Độc Lập Nhân Vật)

`Story Quest Engine v1.0` ([`eagle_story_quest.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_story_quest.py)) là hệ thống **Pure Branching Visual Novel** tách biệt hoàn toàn với hệ thống `30` kịch bản ngắn `4`-CG và hoàn toàn **không có thanh gõ AI `[F6]`**:

1. **Cơ chế Cắm-là-Chạy (`Zero-Core-Edit Auto-Discovery`) cho 5 bạn gái tiếp theo (`furina`, `columbina`, `citlali`, `kirara`, `vesna`):**
   - Engine tự động quét mọi tệp khớp mẫu `eagle_story_quest_<char_id>.py` trong thư mục gốc `gameplay-lab` có export hằng số `STORY_QUEST_CAMPAIGN: dict`.
   - Khi triển khai nhân vật tiếp theo, subagent **chỉ cần thả đúng 2 thành phần độc lập** (không cần sửa `eagle_story_quest.py`, `EagleCompanion.py`, `eagle_dating_sim.py` hay `hud.lua`):
     - `Project Eagle/gta sa gameplay-lab/eagle_story_quest_<char_id>.py`
     - `Project Eagle/gta sa gameplay-lab/ui_assets/story_quest_cgs/<char_id>/*.jpg` (`1376x768`, `16:9`)
   - Thẻ mở chiến dịch trong **App #13 `WaifuLink` -> Tab `DATE & VISIT`** và dòng **`[6] Story Quest: <Title>`** tại **Menu Trước Cửa Nhà `[F9]`** sẽ tự động kích hoạt ngay cho nhân vật đó kèm màu chủ đề `theme_rgb` và icon `ep_ms_<char_id>`.
2. **State Machine, SQLite Auto-Save Từng Nhịp & Causal Flowchart Time-Jump (`waifulink.sqlite3`):**
   - Lưu tự động trên từng nhịp đọc (`beat_idx`) vào 3 bảng SQLite riêng (`story_quest_runs`, `story_quest_checkpoints`, `story_quest_unlocks`) trong `data/project-eagle/dating-sim/waifulink.sqlite3`.
   - Mọi Node và mọi Cổng lựa chọn (`Choice Gate`) đã đi qua đều lưu ảnh chụp trạng thái chính xác `(bond, insight, flags)` để người chơi nhấn **`[J]` (`Causal Flowchart & Checkpoint Time-Jump`)** nhảy ngược về bất kỳ phân cảnh/ngã rẽ nào mà không phải cày lại từ đầu.
3. **Trình Chiếu Fullscreen `16:9` DirectX 9 + Chuột Cảm Ứng 144Hz + Lồng Tiếng Nhật:**
   - Stream trực tiếp ảnh `1376x768` qua khe ping-pong `models/txd/WLCG0.TXD` & `WLCG1.TXD` (`Opcode 0x0391 -> 0x0390`) kèm màn mờ chuyển cảnh `220ms` (`EagleSqCgFadeClock`), không dùng cửa sổ ngoài và không gây reset thiết bị DirectX 9.
   - Bàn phím & chuột cảm ứng song song 100%: `Space` / `Enter` / `Click màn hình CG` qua nhịp tiếp theo; `[1-3]` hoặc click thẻ chọn phương án; `[B]` mở Nhật ký hội thoại & quyết định (`Backlog`); `[J]` mở Sơ đồ nhánh nhân quả (`Flowchart`, đổi từ `[M]` sang `[J]` để không đụng phím đổi chế độ radar `Map & Blips` của GTA SA, đồng thời gọi `Opcode(0x00BE)` xóa chữ GXT gốc); `[H]` ẩn toàn bộ UI ngắm tranh CG tràn viền `16:9`; `[Backspace]` lưu tự động và thoát về thế giới 3D (khôi phục nguyên vẹn `CPad::UpdateMouse = F3 A5`).
   - Tự động phát giọng lồng tiếng Nhật (`Rie Takahashi`) theo trường `voice_emotion` của từng beat qua `WaifuLink JP Voice Engine` (`mci_mpegvideo`).

---

## 2. Gói Chiến Dịch Thí Điểm 5 Chương Của Hu Tao (`char_id = "hutao"`, `ped_id = 49429`)

- **Tệp gói chiến dịch:** [`eagle_story_quest_hutao.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_story_quest_hutao.py) (`419,711` bytes)
- **Nhan đề:** `"Where the Papilio Rests"` *(Phụ đề: `"Where the Plum Blossom Crosses the Mist"`)*
- **Quy mô kịch bản văn học (Literary English, sạch 100% ASCII `CFont` `0x20..0x7E`):**
  - `5` Chương liên hoàn xuyên suốt `12` ngày cận Tết Hải Đăng (`44/44` Scene Nodes, `501` nhịp văn học & hội thoại viết tay, `0` lỗi ký tự `CFont`).
  - `22` Cổng lựa chọn cố định (`C01..C22`) + cơ chế cứu vớt tự động `N17` (`Second-Chance Plum Branch` kích hoạt chính xác cho `35` quỹ đạo `C(7,4)` đạt `(BOND, INSIGHT) == (10, 6)` khi lỡ chọn `C07_B`).
  - `11` Cờ nhân quả (`F01_COLD_PULSE` .. `F11_BUBU_HERBS`), `2` Cổng Kết Hợp Đa Chương (`C15_B_GATE1` & `C18_C_GATE2`) + Cổng Tế Đàn Tuyến A (`C11_A`) và `5` Kết thúc (`END_TRUE`, `END_GOOD`, `END_NEUTRAL`, `END_BAD_1`, `END_BAD_2`).
  - Dàn khách mời chuẩn cốt truyện Liyue: **Zhongli, Baizhu & Changsheng, Qiqi, Xiangling & Guoba, Xingqiu, Chongyun, Yanfei, Lan Yan, Xiao, Ningguang, Keqing, Paimon**.
- **Bộ `42/42` Ảnh CG `16:9` (`1376x768`, SHA-256 duy nhất):**
  - Toàn bộ `42` tấm tại `Project Eagle/gta sa gameplay-lab/ui_assets/story_quest_cgs/hutao/*.jpg` được tạo **100% bằng subagent `image-generator` nội bộ của Antigravity** (sau khi người dùng trực tiếp đối chiếu A/B 5 mẫu và chọn phong cách Visual Novel của Gemini; chỉ truyền ảnh tham chiếu nhân vật gốc HoYoverse + ảnh cảnh liền trước cho các cặp `Base -> Diff`, tuyệt đối không dùng ảnh từ đợt Scenario cũ).

---

## 3. Kết Quả Kiểm Chứng Offline (Part A) & Trực Tiếp Trong Game DirectX 9 (Part B)

### 3.1. Kiểm Chứng Toán Học DAG & Offline Engine (`Part A — 100% PASS`)
- [`verify_hutao_5ch_dag.py`](../../staging/project-eagle/story-quest-hutao-research-20261105/verify_hutao_5ch_dag.py): **Exit code `0`** — `44/44` node liên thông (`0` deadlock, `0` node mồ côi), `6,311` quỹ đạo Rational-Priority / `8,566` quỹ đạo Open-Choice, xác suất Markov tổng đúng `100.00%`, toàn bộ `11` cờ + `BOND` + `INSIGHT` đều có bằng chứng ablation khác `0`.
- [`test_part_a_story_quest.py`](../../staging/project-eagle/story-quest-hutao-impl-20261105/test_part_a_story_quest.py) (chạy độc lập trên `part_a.db` ngoài khóa): **Exit code `0`** — xác nhận auto-save từng beat, mở khóa đủ `5/5` kết thúc qua `Flowchart Jump`, cảm ứng `code=16`, giọng lồng tiếng Nhật và sạch `100%` bảng mã ASCII `CFont`.

### 3.2. Nghiệm Thu Trực Tiếp DirectX 9 `1920x1080` Dưới `ingame-runtime.lock` (`Part B — 11/11 Ảnh PASS`)
Chạy qua [`run_live_d3d9_qa.py`](../../staging/project-eagle/story-quest-hutao-impl-20261105/run_live_d3d9_qa.py) (telemetry lưu tại [`live_d3d9_qa_results.json`](../../staging/project-eagle/story-quest-hutao-impl-20261105/live_d3d9_qa_results.json)), toàn bộ `11/11` ảnh chụp màn hình thực tế `1920x1080` trong [`staging/project-eagle/story-quest-hutao-impl-20261105/qa_screenshots/`](../../staging/project-eagle/story-quest-hutao-impl-20261105/qa_screenshots/) đã được kiểm tra trực tiếp bằng mắt:

| # | Tệp ảnh DirectX 9 (`1920x1080`) | Hạng mục kiểm tra thực tế | Kết quả |
|---|---|---|---|
| `01` | `01_app13_waifulink_launcher.png` | App #13 `WaifuLink` (`DATE & VISIT`) hiển thị thẻ vàng-đỏ `Story Quest: Where the Papilio Rests (Endings 0/5 - Start Ch.1 - Pure VN)` | **PASS** |
| `02` | `02_doorstep_f9_menu.png` | Menu trước cửa nhà Hu Tao `[F9]` hiển thị dòng `[6] Story Quest: Where the Papilio Rests (5 Ch - Pure VN - Endings 0/5)` | **PASS** |
| `03` | `03_ch1_bamboo_mist_opening.png` | Nhấn phím `[6]` mở Chương 1 `N01` (`ch1_bamboo_mist_base.jpg`), đầy đủ suy nghĩ nội tâm không cắt chữ, không có thanh `[F6]` AI, click chuột trực tiếp trên tranh (`code=16, arg=1`) qua nhịp mượt | **PASS** |
| `04` | `04_ch1_bedside_wrist_diff_transition.png` | Chuyển cảnh liền mạch `Base -> Diff` (`ch1_parlor_bedside_wrist.jpg`) khi Aether giữ cổ tay phải lạnh buốt của Hu Tao + ghi nhận manh mối `Clues 1/11` | **PASS** |
| `05` | `05_choice_gate_preset_options.png` | Cổng lựa chọn `C01` (`N02`) hiển thị 2 thẻ phương án nổi sắc nét kèm nameplate `Hu Tao` (`ep_ms_hutao`) | **PASS** |
| `06` | `06_hide_ui_pure_cg.png` | Phím thực `[H]` ẩn toàn bộ UI để ngắm tranh CG `16:9` tràn màn hình (`[H / Click] Show UI`) | **PASS** |
| `07` | `07_backlog_overlay.png` | Phím thực `[B]` mở bảng `DIALOGUE & DECISION BACKLOG` phân màu rõ `[Narrator]`, `[Hu Tao]` và `[Decision]` | **PASS** |
| `08a` | `08a_flowchart_modal.png` | Phím thực `[J]` mở bảng `CAUSAL FLOWCHART & CHECKPOINT TIME-JUMP` hiển thị danh sách node/cổng kèm `Bond / Insight / Clues` (sạch 100% không dính chữ `Map & Blips`) | **PASS** |
| `08b` | `08b_combo_gate1_unlocked.png` | Cổng Kết Hợp Đa Chương #1 (`N25_B5_GATE1` cùng Zhongli trên cầu Liyue) mở khóa huy hiệu ngọc lục bảo `[COMBINATION UNLOCKED]` | **PASS** |
| `09` | `09_ending_true_twin_plums.png` | Hoàn tất Chương 5 đạt **`TRUE ENDING - Twin Plum Blossoms on the Living Shore`** (`end_true_twin_plums_kiss.jpg`) | **PASS** |
| `10` | `10_ending_bad1_umbrella.png` | Time-Jump qua Flowchart về `N17` -> rẽ nhánh Tuyến A ngập ngừng đạt **`BAD ENDING I - Polite Strangers Under a Black Umbrella`** (`Endings 2/5`) | **PASS** |

- **Lồng tiếng Nhật (`Rie Takahashi`):** `mci_ok = True`, phát mượt các nhóm cảm xúc (`vn_playful_tease`, `vn_sweet_happy`, `vn_tender_love`, `greet_doorstep`) qua `WaifuLink JP Voice Engine v1.0`.
- **Chuột cảm ứng & Khôi phục Gameplay:** `CPad::UpdateMouse` (`0x0053F509`) tự động vá `90 90` khi mở Story Quest và trả về đúng `f3 a5` ngay khi nhấn `[Backspace]` thoát ra gameplay 3D.
- **Sức khỏe Runtime & Dọn Dẹp:** `cleo/EagleLuaErrors.log` = **`0` lỗi**; `eagle_doctor.py --doctor` = **`11/11 PASS, 0 WARN, 0 FAIL`**; đã tắt sạch `gta_pe.exe` + `EagleCompanion.py`, xóa sạch dữ liệu lưu thử nghiệm trong `waifulink.sqlite3` / `eagle_companion.db` (kèm `-wal`/`-shm`) và reset `EaglePhoneHUD.dat` để người dùng vào chơi mới tinh từ đầu.

---

## 4. Danh Mục Tệp Đã Triển Khai, SHA-256 & Lệnh Rollback Có Guard

Toàn bộ bản sao lưu trước khi đấu nối và manifest băm SHA-256 được lưu tại [`staging/project-eagle/story-quest-hutao-impl-20261105/backup_before_wire/manifest.json`](../../staging/project-eagle/story-quest-hutao-impl-20261105/backup_before_wire/manifest.json):

### Tệp sửa đổi dưới `game-write.lock` (4 tệp)
| Tệp trong `gameplay-lab` | SHA-256 Trước (`before`) | SHA-256 Sau (`after`) |
|---|---|---|
| `EagleCompanion.py` | `465401e291ee8e80...` | `4ed217a31494084c...` |
| `eagle_dating_sim.py` | `2a36b1c448f52c8f...` | `23e2c150e06d3ace...` |
| `eagle_vn_ingame_overlay.py` | `72ecab6ad6110b15...` | `a0bc90f5d64d8453...` |
| `hud.lua` | `40d8ecb8871bc753...` | `c8772a9d2a77c18d...` |

### Tệp mới bổ sung (44 tệp)
- `eagle_story_quest.py` (`sha256=a8c5dca51e8adb7781edbbb2778b1deef5a256b2989a6fd200b17eedaec7c9a6`)
- `eagle_story_quest_hutao.py` (`sha256=6e4647a2fdfab0ca3000782c49f45f314880772ca8d528590f7c50e4852763e8`)
- `ui_assets/story_quest_cgs/hutao/*.jpg` (`42` tệp `1376x768` RGB `.jpg`, đủ `42/42` mã SHA-256 duy nhất trong `manifest.json`)

### Lệnh Rollback An Toàn Có Guard (chỉ gỡ phần Story Quest nếu cần, bảo toàn công việc của agent khác)
```powershell
python "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\story-quest-hutao-impl-20261105\backup_before_wire\rollback_story_quest_wire.py"
```
*(Script tự động giữ `game-write.lock`, kiểm tra chống trôi hash `after_hashes` trước khi khôi phục để không bao giờ ghi đè nhầm chỉnh sửa mới của hội thoại khác.)*
