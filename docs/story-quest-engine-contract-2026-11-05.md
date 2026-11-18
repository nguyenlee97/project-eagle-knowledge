# Hợp Đồng Kỹ Thuật `Story Quest Engine v1.0` (Plug-and-Play Multi-Character Visual Novel Architecture)

- **Ngày ban hành:** `2026-11-05`
- **Hội thoại điều phối (Orchestrator):** `35d5cf80-28f1-43e1-8e77-f60ee3d570c3`
- **Đích runtime:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

## 1. Triết Lý Thiết Kế (Chống Xung Đột Khi Chạy Song Song Nhiều Hội Thoại Nhân Vật)

Tính năng **Story Quest** được xây dựng một lần ở hội thoại Pilot (**Hu Tao — `char_id = "hutao"`**) theo kiến trúc **Core Engine tách rời hoàn toàn khỏi Character Campaign Pack**:

1. **Core Engine dùng chung (chỉ xây ở Pilot Hu Tao, các nhân vật sau KHÔNG cần sửa):**
   - `Project Eagle/gta sa gameplay-lab/eagle_story_quest.py`:
     - Tự động dò tìm gói cốt truyện của từng nhân vật bằng `importlib.import_module(f"eagle_story_quest_{char_id}")` (quét các file `eagle_story_quest_*.py` trong thư mục `gameplay-lab`).
     - Quản lý đồ thị nhân quả DAG (`nodes`, `beats`, `preset_choices`, `combination_gates`, `endings`), đánh giá biểu thức điều kiện an toàn (không dùng `eval` thô), Auto-Save từng beat/lựa chọn, Backlog (`last 120 beats`), và **Interactive Flowchart Jump** (nhảy lại bất kỳ node/cổng lựa chọn nào đã mở khóa với đúng snapshot `flags/bond/insight` lúc tới node đó để khám phá đủ 5 Endings mà không cần chơi lại từ đầu).
   - `EagleCompanion.py`, `eagle_dating_sim.py`, `hud.lua`:
     - Giao tiếp qua API thống nhất `/api/story_quest/*` và bộ khóa HUD `sq_*` trong `EaglePhoneHUD.dat` / `build_hud_kv`.
     - Hiển thị trên cả **App 13 (`WaifuLink` -> nút/tab `Story Quest`)** lẫn **House Visit `[F9]` (`Story Quest Campaign`)**.

2. **Gói Nội Dung Độc Lập Của Từng Nhân Vật (Mỗi hội thoại Worker chỉ ghi vào đúng 2 đường dẫn riêng biệt):**
   - Module kịch bản Python: `Project Eagle/gta sa gameplay-lab/eagle_story_quest_<char_id>.py` (ví dụ: `eagle_story_quest_hutao.py`, `eagle_story_quest_furina.py`, `eagle_story_quest_columbina.py`, `eagle_story_quest_citlali.py`, `eagle_story_quest_kirara.py`, `eagle_story_quest_vesna.py`).
   - Thư mục CG riêng: `Project Eagle/gta sa gameplay-lab/ui_assets/story_quest_cgs/<char_id>/*.jpg` (`16:9`, chuẩn `1376x768`).
   - Nhờ `_sync_dynamic_waifulink_cg_txd` trong `EagleCompanion.py` ưu tiên giải mã `self.base_dir / Path(rel_clean)`, chỉ cần truyền `cg_rel_url = "ui_assets/story_quest_cgs/<char_id>/<cg_file>.jpg"` là DirectX 9 `WLCG0.TXD` / `WLCG1.TXD` tự động nạp mượt mà không đụng chạm thư mục `dating-sim/media/`!

---

## 2. Chuẩn Dữ Liệu Module `eagle_story_quest_<char_id>.py`

Mỗi file `eagle_story_quest_<char_id>.py` bắt buộc export biến `STORY_QUEST_CAMPAIGN: dict` theo cấu trúc chuẩn:

```python
STORY_QUEST_CAMPAIGN = {
    "char_id": "hutao",
    "ped_id": 49429,
    "display_name": "Hu Tao",
    "campaign_id": "hutao_sq_v1_papilio_rests",
    "title": "Where the Papilio Rests",
    "subtitle": "A Five-Chapter Visual Novel of Life, Ash, and Starlight",
    "poster_cg": "ui_assets/story_quest_cgs/hutao/hutao_sq1_poster.jpg",  # BẮT BUỘC (v2.0): Ảnh Movie-Poster 16:9 (1376x768) hiển thị ở Card Hub v2.0 PAGE_STORY_QUEST!
    "synopsis": "Beneath Liyue's lantern glow, an unsealed Border flare drains the warmth from Wangsheng's 77th Director...",  # BẮT BUỘC (v2.0): Tóm tắt hấp dẫn sạch 100% ASCII CFont (220-340 ký tự)
    "version": "2.0.0",
    "theme_rgb": [225, 49, 75],

# Cuối file bắt buộc export thêm danh sách đa chiến dịch cho StoryQuestEngine v2.0:
# STORY_QUEST_CAMPAIGNS = [STORY_QUEST_CAMPAIGN]
    "chapters": [
        {"chapter_id": "CH1", "index": 1, "title": "Incense for the Living", "entry_node": "N01"},
        # ... CH2..CH5
    ],
    "initial_state": {
        "bond": 0,
        "insight": 0,
        "flags": [],
    },
    "flag_catalog": {
        "F01_COLD_PULSE": {
            "title": "Cold Wrist Pulse",
            "clue_hint": "Hu Tao's fingertips were freezing despite a cloudless afternoon.",
        },
        # ... Mọi cờ đều phải có mô tả hiển thị trên Clue/Memory Strip
    },
    "endings": {
        "END_TRUE": {"rank": "TRUE ENDING", "title": "Spring Tea at Wangsheng", "tone": "radiant"},
        "END_GOOD": {"rank": "GOOD ENDING", "title": "Lanterns Over Yujing Terrace", "tone": "warm"},
        "END_NEUTRAL": {"rank": "BITTERSWEET ENDING", "title": "The Butterfly Beyond the Mist", "tone": "melancholy"},
        "END_BAD_1": {"rank": "BAD ENDING I", "title": "Director's Courteous Smile", "tone": "cold"},
        "END_BAD_2": {"rank": "BAD ENDING II", "title": "Ashes at Wuwang Gate", "tone": "tragic"},
    },
    "nodes": {
        "N01": {
            "node_id": "N01",
            "chapter_id": "CH1",
            "title": "Coffin Promo by the Harbor",
            "day_label": "Day 1 - Late Afternoon",
            "location": "Liyue Harbor - Chihu Rock",
            "beats": [
                {
                    "beat_id": "N01_B01",
                    "speaker": "Narrator",          # "Narrator" | "Aether" | "Hu Tao" | cameo name
                    "text": "Warm autumn sunlight spills across the flagstones of Chihu Rock...",
                    "inner_thought": "",            # Optional inner monologue / resonance line
                    "cg": "ui_assets/story_quest_cgs/hutao/ch1_harbor_base.jpg",
                    "voice_emotion": "",            # Optional: maps to eagle_waifulink_voice.py emotion bucket when speaker == heroine
                    "sfx_cue": "ambient_harbor",    # Optional metadata cue
                },
                # ... 10-20 literary beats per scene node
            ],
            # Hoặc chuyển thẳng/theo điều kiện (`routing`), hoặc mở lựa chọn (`choice`):
            "choice": {
                "choice_id": "C01",
                "prompt": "She extends her hand with a theatrical flourish, waiting for your answer.",
                "options": [
                    {
                        "opt_id": "A",
                        "label": "Play along with her two-for-one coffin pitch to make her laugh.",
                        "effects": {"bond": 1, "insight": 0, "add_flags": []},
                        "next_node": "N02",
                    },
                    {
                        "opt_id": "B",
                        "label": "Catch her wrist gently and ask why her fingers are ice-cold.",
                        "effects": {"bond": 1, "insight": 1, "add_flags": ["F01_COLD_PULSE"]},
                        "next_node": "N02",
                    },
                ],
            },
            "routing": [
                # Dùng cho các node không có choice hoặc các cổng Combination Gate:
                # {"when": {"min_insight": 5, "all_flags": ["F03_WUWANG_LORE"], "any_flags": ["F01_COLD_PULSE", "F08_ASH_COUGH_SEEN"]}, "next_node": "N29"},
                # {"default": True, "next_node": "N37_BAD2"}
            ],
            "ending_id": None,  # Chỉ đặt khác None tại các node kết thúc
        }
    },
}
```

---

## 3. Quy Tắc Bắt Buộc Về Văn Phong, RenderWare `CFont`, CG & DirectX 9

1. **Luật Sạch Ký Tự RenderWare `CFont` (`gta_pe.exe`)**:
   - Tuyệt đối **KHÔNG** dùng ký tự `~` (GTA hiểu nhầm là mã đổi màu chữ và crash/ẩn chuỗi), `|`, `*`, dấu ngoặc kép cong Unicode (`“ ” ‘ ’`), gạch ngang dài Unicode (`—` -> đổi thành `--`), hoặc dấu ba chấm một ký tự (`…` -> đổi thành `...`). Toàn bộ chuỗi hiển thị HUD phải là **ASCII chuẩn sạch 100%**.
2. **Chiến Lược CG `Base Scene + Pose/Expression Diff` (Đồng Bộ Tuyệt Đối Với Văn Bản)**:
   - Không khóa cứng số lượng CG ở con số cố định nhỏ. Mỗi bối cảnh quan trọng có **1 Base CG (`16:9`, `1376x768`)**, và khi cảm xúc/hành động của nhân vật trong cảnh đổi nhịp (tinh nghịch -> sững sờ -> ho ra tàn lửa -> quay mặt giấu nước mắt -> mỉm cười thật lòng), tạo các bản **Expression/Pose Diff CG** bằng cách truyền chính file **Base CG** + ảnh tham chiếu nhân vật gốc vào subagent `image-generator` nội bộ.
   - **TUÂN THỦ TUYỆT ĐỐI LUẬT CỨNG TẠO ẢNH (`AGENTS.md` / `GEMINI.md`):** Chỉ được dùng subagent `image-generator` nội bộ của Antigravity (`100` hình / cửa sổ trượt `5 tiếng`). Nghiêm cấm gọi bất kỳ API tạo ảnh bên ngoài nào. Nếu chạm trần `429 RESOURCE_EXHAUSTED`, dừng ngay bước vẽ ảnh, giữ nguyên các CG đã vẽ đạt chuẩn và báo rõ số ảnh còn thiếu + thời gian hồi quota.
3. **Ràng Buộc DirectX 9 Một Slot Script TXD (`hud.lua` `0x0391 / 0x0390`)**:
   - `hud.lua` giải phóng TXD cũ (`0x0391`) trước khi nạp `WLCG0/WLCG1` mới (`0x0390`). Khi chuyển giữa hai CG khác nhau, vẽ màn mờ chuyển cảnh nhẹ (`Sprite2d.DrawRect` alpha fade `~180–220ms`) để không nháy khung hình và tuyệt đối không giữ 2 con trỏ `EagleActiveWlCgTex` cùng lúc.
4. **Trải Nghiệm Thuần Visual Novel Trong Story Quest Mode**:
   - **TẮT hoàn toàn thanh nhập AI `[F6]`** khi đang trong chế độ `Story Quest` (100% lựa chọn có sẵn `1..3`).
   - Phím điều khiển chuẩn trong `hud.lua`:
     - `[SPACE]` / `[ENTER]` / Click: Sang beat văn bản tiếp theo.
     - `[1]` / `[2]` / `[3]`: Chọn nhánh khi đến Choice Gate.
     - `[B]`: Bật/tắt Backlog (đọc lại các câu thoại vừa qua).
     - `[M]`: Bật/tắt Flowchart / Chapter Checkpoint Jump (nhảy về bất kỳ cảnh/lựa chọn nào đã mở khóa kèm trạng thái cờ lúc đó).
     - `[H]`: Ẩn/hiện hộp thoại để ngắm trọn vẹn bức CG `16:9`.
     - `[BACKSPACE]` / `[ESC]`: Auto-Save tiến độ hiện tại và thoát êm về điện thoại / thế giới 3D (lần sau bấm `Continue Story Quest` sẽ vào lại đúng beat đang đọc dở!).
5. **Tự Động Kiểm Chứng Đồ Thị (Zero-Deadlock Gate)**:
   - Mọi module `eagle_story_quest_<char_id>.py` trước khi đưa vào game phải qua bộ kiểm tra đồ thị vét cạn xác nhận: `0` node mồ côi, `0` deadlock, mọi cờ đều có nơi gài và nơi trả kết quả, mọi cổng Combination Gate đều hoạt động, đủ tất cả Endings đều có đường đi hợp lệ, `100%` đường dẫn ảnh `cg` tồn tại trên đĩa và `0` ký tự vi phạm `CFont`.
