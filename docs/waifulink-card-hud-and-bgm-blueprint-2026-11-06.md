# Bản Thiết Kế Kiến Trúc: `WaifuLink Card Hub v2.0` (Thẻ Minh Hoạ 3 Chế Độ & Đa Story Quest) + `Genshin BGM Engine` (`st_g02`)

- **Ngày lập:** `2026-11-06`
- **Hội thoại Orchestrator:** `35d5cf80-28f1-43e1-8e77-f60ee3d570c3`
- **Đích tích hợp:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

Tài liệu này lưu trữ quy chuẩn kiến trúc trên đĩa để các hội thoại Worker (BGM Research, HUD Card Redesign, và các Story Quest nhân vật tiếp theo) tham chiếu thống nhất.

## 1. Kiến Trúc `WaifuLink Card Hub v2.0` (`hud.lua` + `models/hud.txd` + `eagle_dating_sim.py` + `eagle_story_quest.py`)

### 1.1. Quy ước Texture Thẻ Minh Hoạ & Icon Chế Độ Theo Nhân Vật Trong `models/hud.txd`
Mỗi nhân vật trong dàn 6 bạn gái (`hutao`, `furina`, `citlali`, `columbina`, `kirara`, `vesna`) có bộ 3 thẻ minh hoạ dọc (`256x384` hoặc `256x256` DXT5) và icon chế độ riêng đóng gói sẵn trong `models/hud.txd`:
- `wl_cd_<char>_scen`: Thẻ minh hoạ chế độ **Scenario** riêng của `<char>`
- `wl_cd_<char>_roam`: Thẻ minh hoạ chế độ **Free Roam** riêng của `<char>`
- `wl_cd_<char>_sq`: Thẻ minh hoạ chế độ **Story Quest** riêng của `<char>`

Khe động `models/txd/WLCG0.TXD` & `WLCG1.TXD` (`1024x512`) được dùng để stream trực tiếp ảnh preview `16:9` của mục đang trỏ (Scenario CG1, ảnh kỷ niệm Free Roam, ảnh bìa Story Quest hoặc ảnh chụp của Save Slot đang chọn).

### 1.2. Cấu Trúc 4 Màn Hình (`1920x1080` Mouse `144Hz` + Keyboard)
1. **Màn hình gốc (`HUB_CARDS`)**:
   - Header: Avatar `ep_ms_<char>`, Tên & Danh hiệu, Huy hiệu `Stage 1..5`, Thanh tổng tình cảm `♥`, và thanh trạng thái nhạc nền `♪ BGM` (nút bật/tắt/đổi bài).
   - 3 Thẻ Lớn đặt ngang có viền phát sáng theo `DEFAULT_THEME_COLORS[char_id]`: **Scenario**, **Free Roam**, **Story Quest**.
2. **Trang con `PAGE_SCENARIO`**:
   - Hiển thị rõ `Current Stage`, `Affection Progress`, điều kiện mở cổng `Core Scenarios Passed (X/3)`.
   - Bộ lọc `Stage 1..5` + `Extra Cameos`, danh sách `30` kịch bản có nhãn trạng thái (`CLEARED`, `NEW`, `CARRYOVER`, `LOCKED`), khung preview `16:9` bên phải và nút `PLAY SCENARIO`.
3. **Trang con `PAGE_FREEROAM`**:
   - Hiển thị rõ **Điểm Free Roam đã đạt trong Stage hiện tại so với trần Stage (`stage_roam_pts / 75`)** VÀ **Tổng điểm tình cảm hiện tại so với ngưỡng lên Stage kế tiếp (`affection / next_threshold`)**.
   - Thống kê tổng số chuyến đi, số lần đạt hạng `S / A / B`, số ảnh kỷ niệm đã mở (`X / 15`), chọn `Date Spot 1..3` và nút `START OUTING`.
4. **Trang con `PAGE_STORY_QUEST` (`StoryQuestEngine v2.0` Multi-Campaign)**:
   - Hỗ trợ **nhiều hơn 1 Story Quest trên mỗi nhân vật**:
     - `eagle_story_quest.py` nạp đồng thời `STORY_QUEST_CAMPAIGNS: list[dict]` và `STORY_QUEST_CAMPAIGN: dict` từ mọi file `eagle_story_quest_<char>*.py`, định danh bằng `(char_id, campaign_id)`.
     - Bổ sung bảng `story_quest_save_slots` (`slot_idx = 0` Auto-Save + `slot_idx = 1..6` Manual Save Slots) lưu kèm `cg_rel`, `chapter_id`, `node_id`, `beat_idx`, `bond`, `insight`, `flags_json`, `backlog_json`, `saved_at`.
   - Gồm danh sách chọn Story Quest bên trái + 3 chế độ xem bên phải:
     1. `OVERVIEW`: Tiến độ `%` Node đã mở, Manh mối (`Clues`), `Endings Unlocked (X/5)`, nút `Continue / New Game`.
     2. `CAUSAL FLOWCHART 2D`: Sơ đồ cây nhân quả vẽ bằng các khối Node & đường nối theo 5 cột Chương (`Ch.1..Ch.5`), cho phép click nhảy thời gian (`Time-Jump`) kèm snapshot cờ.
     3. `SAVE / LOAD`: Quản lý `Auto-Save` + `6` ô lưu thủ công kèm ảnh preview `16:9` (truy cập được cả trong lúc đang chơi VN qua phím `[S]` / `[L]`).

---

## 2. Kiến Trúc Nhạc Nền `WaifuLink Genshin BGM Engine` (`eagle_waifulink_bgm.py`)

- **Nguồn nhạc ưu tiên số 1**: Đài **`st_g02` (`Night-Wind Resonance FM` — Genshin Global Citlali, `80` bài)** trong `tools/eagle-radio-studio/data/project.json` (kết hợp bổ sung có chọn lọc từ `st_g01`, `st_g03`, `st_g04` và kho cache Genshin trên `D:/GTA Archive/Eagle Radio Studio/cache` nếu cần bài chuyên biệt theo vùng Liyue/Fontaine/Natlan/Inazuma/Snezhnaya).
- **Cơ chế phát song song không xung đột giọng nói**:
  - Sử dụng luồng Win32 `winmm.dll -> mciSendStringW` riêng với định danh `alias wl_bgm` (tách biệt hoàn toàn với `alias wl_voice` trong `eagle_waifulink_voice.py`).
  - Âm lượng chuẩn khi đọc chữ: `220 / 1000`.
  - **Auto-Ducking**: Khi `wl_voice` đang phát câu thoại tiếng Nhật, hạ mượt `wl_bgm` xuống `90 / 1000` và nâng lại `220 / 1000` sau khi thoại kết thúc `300ms`.
  - Tự động tắt `wl_bgm` khi bước vào chế độ lái xe **Free Roam** hoặc thoát hẳn về gameplay GTA 3D để không chồng chéo với RadioEx trên xe.


---

## 3. Trạng Thái Triển Khai & Chuẩn Bắt Buộc `Movie-Poster Metadata` Cho Mọi Gói Story Quest (`06/11/2026` — DONE)

- **Đã triển khai và nghiệm thu `100% PASS` trong `gameplay-lab`** bởi hội thoại `ca10ae9a-a3de-4c0d-9af9-0496f9f686c5`:
  - `models/hud.txd` (`10,629,456 B`, `336` chunks, đóng gói `18` thẻ `wl_cd_<char>_*` `512x512` chuẩn tỷ lệ hiển thị `6:7` + `18` icon biểu tượng `wl_ic_<char>_*` `128x128` nền trong suốt).
  - `cleo/EagleWaifuCardHub.lua` + `hud.lua` + `eagle_story_quest.py` (`v2.0`) + `eagle_dating_sim.py` + `EagleCompanion.py` + `eagle_story_quest_hutao.py` + `ui_assets/story_quest_cgs/hutao/hutao_sq1_poster.jpg` (`1376x768`).
  - Chi tiết báo cáo QA E2E DirectX 9 `1920x1080` (`13/13` ảnh chụp thực tế) xem tại [`waifulink-card-hub-v2-e2e-qa-2026-11-06.md`](waifulink-card-hub-v2-e2e-qa-2026-11-06.md).
- **QUY CHUẨN BẮT BUỘC CHO MỌI GÓI STORY QUEST VỀ SAU (`Citlali`, `Furina`, `Columbina`, `Kirara`, `Vesna` & Chiến Dịch `#2, #3...`):**
  - Mọi dict chiến dịch trong `STORY_QUEST_CAMPAIGN` hoặc `STORY_QUEST_CAMPAIGNS` **bắt buộc phải có đủ 4 trường giới thiệu bên ngoài** trước khi người chơi bấm bắt đầu:
    1. `"title"`: Tên chính thức của Story Quest (tiếng Anh sạch `CFont` `0x20..0x7E`).
    2. `"subtitle"`: Phụ đề văn học ngắn gọn (tiếng Anh sạch `CFont` `0x20..0x7E`).
    3. `"poster_cg"`: Tên file ảnh bìa ngang điện ảnh `16:9` (`1376x768`, ví dụ `"<char>_sq1_poster.jpg"`, lưu trong `ui_assets/story_quest_cgs/<char>/`, **chỉ tạo bằng subagent `image-generator` nội bộ** có truyền ảnh tham chiếu gốc của nhân vật & Aether).
    4. `"synopsis"`: Đoạn tóm tắt cốt truyện hấp dẫn không spoil kết cục (`200–300` ký tự tiếng Anh sạch `CFont` `0x20..0x7E`, tự động wrap `5` dòng trên tab `1. OVERVIEW & PLAY`).
