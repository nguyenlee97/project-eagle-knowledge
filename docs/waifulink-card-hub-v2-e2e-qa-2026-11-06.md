# WaifuLink Card Hub v2.0 & StoryQuestEngine v2.0 — Kiến Trúc, Chuẩn Chữ Lớn / Chống Méo Tỷ Lệ & Nghiệm Thu E2E DirectX 9 (`1920x1080`)

- **Ngày hoàn tất:** `2026-11-06`
- **Agent / Hội thoại thực thi:** Antigravity (`ca10ae9a-a3de-4c0d-9af9-0496f9f686c5`)
- **Đích triển khai:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục staging & rollback:** `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-card-hub-v2-20261106\`
- **Phiếu công việc:** [`docs/project-eagle/work-items/2026-11-06-antigravity-waifulink-card-hub-v2.md`](work-items/2026-11-06-antigravity-waifulink-card-hub-v2.md)
- **Trạng thái nghiệm thu:** **`100% PASS`** (`Part A Offline 3/3 Suites PASS [5,508 HUD Keys CFont Clean]`, `Part B Live DirectX 9 1920x1080 13/13 Screenshots PASS`, `EagleLuaErrors.log = 0`, `eagle_doctor.py 11/11 PASS`)

---

## 1. Tóm Tắt Các Hạng Mục Đã Hoàn Tất

1. **Bộ `36` Texture DXT5 Riêng Cho `6 Nhân Vật × 3 Chế Độ` Trong `models/hud.txd` (`336` chunks, `10,629,456` bytes):**
   - **`18` Tranh Thẻ Minh Họa Dọc (`wl_cd_<char>_scen`, `wl_cd_<char>_roam`, `wl_cd_<char>_sq`):** Vẽ 100% bằng subagent `image-generator` nội bộ kèm ảnh tham chiếu gốc của từng nhân vật (`hutao`, `furina`, `citlali`, `columbina`, `kirara`, `vesna`), crop thông minh đúng chuẩn tỷ lệ hiển thị `6:7` (`216:252` virtual px, ưu tiên lấy trọn mũ/khuôn mặt/xe mui trần) trước khi đóng gói POT `512x512` DXT5 (`PSNR >= 31.57 dB`).
   - **`18` Icon Biểu Tượng Chế Độ Riêng (`wl_ic_<char>_scen`, `wl_ic_<char>_roam`, `wl_ic_<char>_sq`):** Thiết kế vector siêu nét `512x512 -> 128x128` nền alpha sạch mang biểu tượng riêng từng cô gái (Hoa Mận / Bướm Lửa / Cổng Wuwang cho Hu Tao; Vương Miện Giọt Nước / Mặt Nạ Opera cho Furina; Gối Itzpapa / Sao Gió Đêm cho Citlali; Đôi Cánh Trăng Bạc cho Columbina; Chân Mèo Hộp Giao Hàng cho Kirara; Kiếm Băng Hoa Tuyết cho Vesna).
   - **Bảo toàn tuyệt đối `300` chunk sẵn có trong `models/hud.txd`** byte-for-byte.

2. **Giao Diện `WaifuLink Card Hub v2.0` (`cleo/EagleWaifuCardHub.lua` + `hud.lua`, `1920x1080` Fullscreen, Chuột `144Hz` + Phím):**
   - **2 lối vào liền mạch:**
     - Trước cửa nhà bạn gái bấm **`[F9]`**: mở thẳng Card Hub của chủ nhà đó (`wh_can_switch = 0` khóa nhân vật để tránh lệch tọa độ xuất xe `575 Broadway`).
     - Trong **App #13 `WaifuLink` (`DATE & VISIT`)**: nút nổi bật **`OPEN GIRLFRIEND HUB (FULLSCREEN)`** cho phép bấm **`[Q] / [E]`** hoặc mũi tên `< / >` trên Header chuyển nhanh qua lại cả 6 cô gái (tự đổi bảng màu chủ đạo + nhạc nền vùng miền).
   - **Chuột cảm ứng `144Hz` an toàn tuyệt đối:** Tự vá `CPad::UpdateMouse` (`0x0053F509`: `F3 A5 -> 90 90`) khi mở Card Hub và khôi phục tức thời về `F3 A5` ngay khi đóng Hub hoặc bấm `START FREE-ROAM OUTING`. Đã bổ sung `or EaglePhoneState.wl_house_menu == "1"` vào toàn bộ `9` chốt chặn HUD gốc GTA SA để không bao giờ lọt `$50000`, icon nắm đấm hay tên khu vực đè lên Card Hub.
   - **4 màn hình chuyên biệt:**
     - **Thanh Header Xuyên Suốt:** Avatar `ep_ms_<char>`, Tên & Danh hiệu, `STAGE X / 5`, thanh `Affection (current / 1000)` + `CGs: M/15`, cụm nhạc nền trực tiếp **`BGM`** kèm nút **`[N] Next`** & **`[M] Mute`**, nút **`< Exit / < Hub`** và **`AI Chat`**.
     - **`HUB_CARDS`:** 3 thẻ minh họa lớn (`SCENARIO EPISODES` · `FREE-ROAM OUTING` · `STORY QUEST VN`) đặt cân đối cùng thông số tóm tắt và nút hành động.
     - **`PAGE_SCENARIO`:** Thanh tiến độ `Stage Scenario Pts` + `Core Gate (0/3)`, 6 tab (`STAGE 1..5` + `EXTRA CAMEOS`) + nút `+ AI ENCORE SCENARIO`, danh sách 6 dòng thoáng rộng kèm huy hiệu màu (`[CLEARED]`, `[AVAILABLE +35]`, `[CARRYOVER +35]`, `[LOCKED]`) và khung xem trước `16:9` Couple CG thực tế.
     - **`PAGE_FREEROAM`:** 2 thanh đo trực quan (`STAGE FREE-ROAM POINTS: X / 75 PTS` & `CURRENT STAGE THRESHOLD`), thống kê bền vững từ SQLite (`OUTINGS`, `S / A / B Ranks`, `Best Score`), thông tin xe `575 Broadway Convertible`, bộ chọn 4 điểm hẹn (`Auto Scenic` + `3 Date Spots` kèm khoảng cách thực tế) và nút `[SET GPS TO HER HOME]` / `[TELEPORT TO HER HOME]` / `[START FREE-ROAM OUTING]`.
     - **`PAGE_STORY_QUEST`:** Cột trái chọn chiến dịch (`#1 .. #N`, hỗ trợ nhiều Story Quest cho mỗi nhân vật; hiện thông báo lịch sự `Coming Soon` cho nhân vật chưa có gói truyện) + 3 tab con: **`1. OVERVIEW & PLAY`** (Poster điện ảnh `16:9`, Tên truyện, Phụ đề, Tóm tắt 5 dòng, Thanh `Scenes Explored` / `Clues Discovered`, Bộ sưu tập `5 Endings`), **`2. CAUSAL FLOWCHART 2D`**, và **`3. SAVE / LOAD SLOTS`**.

3. **Chuẩn Chữ Lớn Ngang Ngửa Story Quest & Khóa Tỷ Lệ Chống Méo Ảnh Toàn Hệ Thống (Phản Hồi Trực Tiếp Từ Người Dùng):**
   - **Nâng cấp cỡ chữ lớn đồng bộ:**
     - Trong **Scenario VN (`DrawWaifuLinkDatingHud`)**: tăng hộp thoại chính lên đúng cỡ chữ Story Quest (`0.192, 0.412` căn trái, `width=84` × `4` dòng) và tách 3 lựa chọn thành **3 thẻ nổi trên ảnh CG** (`0.168..0.172`, tự động xuống 2 dòng `width=78`) thay vì nhét chữ nhỏ vào đáy hộp thoại.
     - Trong **`WaifuLink Card Hub v2.0`**: toàn bộ chữ tiêu đề, danh sách tập, thông số Free-Roam, Sơ đồ 2D và bảng Save/Load được nâng lên dải `0.150..0.228 × 0.322..0.488` (loại bỏ hoàn toàn cỡ chữ nhỏ `0.118..0.132`).
     - Ngoài **HUD 3D (`DrawWaifuLinkRelationshipBar`, Doorstep `[F9]` & Outing Banner)**: mở rộng khung `topW = 536` và nâng cỡ chữ lên `0.152..0.165 × 0.326..0.354`.
   - **Triệt tiêu 100% lỗi kéo giãn "lùn béo / bẹo hình bẹo dạng":**
     - Tất cả 18 thẻ dọc được crop thông minh đúng chuẩn `6:7` từ ảnh gốc `848x1264` và luôn vẽ qua hàm khóa tỷ lệ `DrawWlCardArt` (kể cả ở cột trái trang Story Quest).
     - Hàm đóng gói động `_build_waifulink_cg_txd_bytes` trong `EagleCompanion.py` tự động crop thông minh `16:9` (`focus_y = 0.18` ưu tiên khuôn mặt trên ảnh selfie dọc `896x1200` như `hutao_selfie.png`) trước khi xuất `1024x512` `WLCG0.TXD` / `WLCG1.TXD`, kết hợp hàm vẽ khóa tỷ lệ `DrawWlCg16x9`.
     - Đã sửa luôn tỷ lệ hiển thị banner `4:1` (`ep_bn_waifu`, `ep_bn_contacts`) và wallpaper `1:2` (`wp_tex`) trên điện thoại EaglePhone.

4. **`StoryQuestEngine v2.0` (`eagle_story_quest.py`) & Chuẩn Poster Điện Ảnh Bắt Buộc Cho Mọi Gói Truyện:**
   - Hỗ trợ đa chiến dịch trên mỗi nhân vật (`STORY_QUEST_CAMPAIGNS` list hoặc `STORY_QUEST_CAMPAIGN` đơn lẻ, tương thích ngược 100% với Citlali & Furina v1.0).
   - Tự động nâng cấp schema SQLite không mất dữ liệu (`campaign_id`) + bảng `story_quest_save_slots` hỗ trợ **`7` Ô Lưu (`Slot 0 Auto-Save` + `Slots 1..6 Manual`)** lưu chính xác `(campaign_id, node_id, beat_idx, bond, insight, flags_json, history_json, cg_rel, saved_at)` hiển thị cả trong `Card Hub` lẫn phím `[S] / [L]` ngay trong VN.
   - Bộ giải tọa độ **Sơ Đồ Cây Nhân Quả 2D (`build_causal_graph_2d`)** tự động xếp cột `Ch.1 -> Ch.5 -> Endings` (`0` node đè nhau trên cả Hu Tao `33 cols / 49 nodes`, Citlali `33 cols / 49 nodes`, Furina `35 cols / 49 nodes`), vẽ đường nối vuông góc 2D phân biệt nhánh đã mở / chưa mở, hỗ trợ click xem chi tiết & **`TIME-JUMP HERE`**.
   - Bổ sung Poster điện ảnh `16:9` (`ui_assets/story_quest_cgs/hutao/hutao_sq1_poster.jpg`, `1376x768`) và `synopsis` cho Hu Tao Story Quest #1 (`"Where the Papilio Rests"`).

---

## 2. Quy Chuẩn Bắt Buộc Cho Mọi Gói Story Quest Mới Về Sau

Từ `StoryQuestEngine v2.0` (`06/11/2026`), mọi gói `eagle_story_quest_<char>.py` mới (hoặc chiến dịch `#2, #3...` trong `STORY_QUEST_CAMPAIGNS`) **bắt buộc khai báo đủ 4 trường metadata cấp chiến dịch** để tab `1. OVERVIEW & PLAY` hiển thị chuẩn giao diện điện ảnh trước khi bấm chơi:

```python
STORY_QUEST_CAMPAIGN = {
    "campaign_id": "<char>_sq1_<slug>",
    "char_id": "<char>",
    "title": "<Ten Truyen Chinh Thuc Clean CFont ASCII>",
    "subtitle": "<Phu De Van Hoc Clean CFont ASCII>",
    "poster_cg": "<char>_sq1_poster.jpg",  # 1376x768 (16:9) luu tai ui_assets/story_quest_cgs/<char>/, tao bang image-generator noi bo
    "synopsis": "<Doan tom tat cot truyen 200-300 ky tu Clean CFont ASCII khong tiet lo ket cuc>",
    ...
}
```

---

## 3. Danh Mục Tệp Runtime Đã Triển Khai & Hash SHA-256 (`manifest.json`)

- **Manifest đầy đủ (`44` tệp):** [`staging/project-eagle/waifulink-card-hub-v2-20261106/manifest.json`](../../staging/project-eagle/waifulink-card-hub-v2-20261106/manifest.json)
- **Script phục hồi có kiểm tra SHA-256:** [`staging/project-eagle/waifulink-card-hub-v2-20261106/rollback_card_hub_v2.py`](../../staging/project-eagle/waifulink-card-hub-v2-20261106/rollback_card_hub_v2.py)

| Tệp Runtime (`gameplay-lab`) | Trước (`SHA-256` đầu) | Sau (`SHA-256` đầu) | Kích thước mới |
|---|---|---|---|
| `models/hud.txd` | `521898168d0f...` | `a3b0e65db2a5...` | `10,629,456 B` (`336` chunks) |
| `cleo/EagleWaifuCardHub.lua` | *(mới)* | `f613480ae2e8...` | `53,867 B` |
| `hud.lua` | `01e5723f976f...` | `e2ed275becf6...` | `239,267 B` |
| `eagle_story_quest.py` | `deb27befbbab...` | `cdda19f46384...` | `131,617 B` |
| `eagle_story_quest_hutao.py` | `6e4647a2fdfa...` | `c3d7804ee6d7...` | `420,121 B` |
| `eagle_dating_sim.py` | `d0022d3e2864...` | `890a89e84f82...` | `312,880 B` |
| `EagleCompanion.py` | `f2ed04a9e2a1...` | `70bf57a6b6b0...` | `482,564 B` |
| `ui_assets/story_quest_cgs/hutao/hutao_sq1_poster.jpg` | *(mới)* | `2acfee107875...` | `379,113 B` (`1376x768`) |
| `ui_assets/waifulink_cards/wl_cd_*.png` + `wl_ic_*.png` (`36` tệp) | *(mới)* | *(xem `manifest.json`)* | `18` thẻ `512x512` + `18` icon `128x128` |

> **Cam kết không can thiệp chéo:** `eagle_story_quest_citlali.py` và `eagle_story_quest_furina.py` giữ nguyên 100% không chạm tới.

---

## 4. Kết Quả Kiểm Thử Toàn Diện (Part A Offline & Part B Live DirectX 9 `1920x1080`)

### 4.1. Part A — Kiểm Thử Logic & Binary Offline (`test_part_a_card_hub_and_sq_v2.py`)
- **Biên dịch & Texture Audit:** `336` chunks hợp lệ trong `hud.txd`, giải mã ngược toàn bộ `36` texture DXT5 (`wl_cd_*` `512x512` + `wl_ic_*` `128x128`) đạt `PSNR >= 31.57 dB`, poster `1376x768`.
- **Multi-Campaign, 2D Graph & 7 Save Slots:** Kiểm chứng đăng ký 2 chiến dịch song song cho 1 nhân vật, lưu/tải tròn vòng `Slot 0..6`, và giải đồ thị 2D `0` trùng ô trên Hu Tao (`33` cột), Citlali (`33` cột), Furina (`35` cột).
- **CFont ASCII Audit:** Quét `5,508` khóa xuất HUD qua toàn bộ 6 cô gái × 4 trang × các modal — **`0` ký tự vi phạm `0x20..0x7E`**.

### 4.2. Part B — Nghiệm Thu Trực Tiếp Trong `gta_pe.exe` DirectX 9 `1920x1080` (`run_part_b_card_hub_v2_qa.py`)
Toàn bộ 13 ảnh chụp màn hình thực tế tại [`staging/project-eagle/waifulink-card-hub-v2-20261106/qa_screenshots/`](../../staging/project-eagle/waifulink-card-hub-v2-20261106/qa_screenshots/) đã được kiểm tra trực tiếp bằng mắt:
- `01_doorstep_f9_hutao_hub_cards.png`: Mở `[F9]` trước cửa nhà Hu Tao (`[Doorstep Locked]`), 3 thẻ dọc chuẩn tỷ lệ `6:7`, chữ lớn rõ, ẩn sạch `$50000` & radar, chuột `144Hz` `0x9090` kích hoạt, nhạc Liyue phát tự động; đóng Hub trả ngay `0xF3A5`.
- `02_app13_waifulink_fullscreen_btn.png`: Nút đỏ nổi bật `OPEN GIRLFRIEND HUB (FULLSCREEN)` trong App #13 kèm banner `ep_bn_waifu` đúng tỷ lệ `4:1` sắc nét.
- `03_hub_switch_furina_cards.png` & `04_hub_switch_citlali_cards.png`: Chuyển nhanh sang Furina (xanh Sapphire + nhạc Fontaine) và Citlali (tím Lavender + nhạc Natlan), tranh thẻ chuẩn tỷ lệ 100%.
- `04b_hub_vesna_coming_soon.png`: Trang Story Quest của Vesna hiển thị khung `Coming Soon` lịch sự kèm tranh thẻ `6:7` cột trái đúng tỷ lệ.
- `05_page_scenario_hutao.png` & `05b_scenario_vn_launched.png`: Danh sách tập chữ lớn thoáng mắt + CG Couple `16:9`; bấm chạy vào Scenario VN hiển thị chữ thoại lớn chuẩn Story Quest (`0.192, 0.412`) và 3 thẻ lựa chọn nổi trên nền CG.
- `06_page_freeroam_hutao.png` & `06b_freeroam_driving_active.png`: Selfie Hu Tao được crop thông minh `16:9` không còn bị bẹt ngang; bấm `START FREE-ROAM OUTING` xuất xe `575 Broadway`, trả chuột `0xF3A5` tức thời và hiện thanh HUD hẹn hò chữ lớn trên đường phố.
- `07_page_story_quest_overview_poster.png`: Poster điện ảnh `16:9` Hu Tao & Aether bên đèn lồng Liyue + tiêu đề vàng cỡ lớn + tóm tắt cốt truyện + nút `[N] Next` / `[M] Mute` BGM hoạt động chuẩn xác.
- `08_page_story_quest_2d_flowchart.png` & `10_in_vn_2d_flowchart_modal.png`: Sơ đồ cây nhân quả 2D trực quan cả ngoài Card Hub lẫn phím `[J]` trong VN; bấm `TIME-JUMP HERE` nhảy thẳng vào đúng checkpoint.
- `09_in_vn_saveload_slots_modal.png` & `11_page_story_quest_saveload_tab.png`: Bảng `Auto-Save + 6 Manual Slots` có ảnh thu nhỏ CG `16:9` thực tế; tải lại `Slot 1` khôi phục chính xác `N04 beat 2 (Bond 2, Insight 2)`.
- **Kiểm toán sau QA:** `cleo/EagleLuaErrors.log` = `0` lỗi; CSDL `eagle_companion.db` & `waifulink.sqlite3` được khôi phục nguyên trạng sạch sẽ; `eagle_doctor.py --doctor` đạt **`11/11 PASS, 0 WARN, 0 FAIL`**; cả 2 khóa `game-write.lock` và `ingame-runtime.lock` đều `null`.
