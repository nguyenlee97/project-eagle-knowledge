# Báo cáo tiếp nhận & đối chiếu kiến trúc Mondstadt Character Chat (`v0.3.3`)

- **Ngày tiếp nhận:** `2026-11-04` (Asia/Saigon)
- **Agent thực hiện:** Antigravity (`c71a77f9-97e6-4a68-aba6-9fb3b4acf926`)
- **Phiếu công việc:** [`../work-items/2026-11-04-antigravity-mondstadt-character-chat-onboarding.md`](../work-items/2026-11-04-antigravity-mondstadt-character-chat-onboarding.md)
- **Phạm vi:** Chỉ đọc hiểu mã nguồn, gói nội dung, hồ sơ bàn giao của Codex (`v0.1.0` -> `v0.3.3`) và đối chiếu với hiện trạng quần thể Mondstadt (`M0 + M1 + M2 + INT-01..07`) trong `gameplay-lab`. Không sửa source, DB hay runtime.

---

## 1. Tóm tắt kiến trúc `tools/eagle-character-chat` (`v0.3.3`) của Codex

1. **Ranh giới độc lập ngoài game (`Standalone Studio` cổng `8952`):**
   - Ngôn ngữ sản phẩm: **English-only** cho cả hội thoại, lựa chọn phóng tác và giao diện web (`static/index.html`, `static/app.js`).
   - Lưu trữ cục bộ tại `data/project-eagle/character-chat/conversations.sqlite3` (SQLite WAL + FTS5 `turn_search`, schema `v2`), hoàn toàn tách biệt với `paimon.sqlite3` và `eagle_companion.db`.
   - Cấu hình AI riêng không chứa khóa bí mật tại `data/project-eagle/character-chat/connection.json`: gọi trực tiếp OpenAI `gpt-6-luna` (`reasoning_effort: "low"`, `max_completion_tokens: 1200`, `timeout_seconds: 35`, biến môi trường user `EAGLE_CHARACTER_OPENAI_API_KEY`).

2. **Bốn lớp dữ liệu tách bạch (chống trộn lẫn canon – lời người chơi – nhận thức cá nhân):**
   - **World Snapshot & Entities (`content/world.json` + `content/cognition/world.json`):** Ghim mốc **`post-7.1`** (`profile.id = "post_71"`), Aether đã quen dàn nhân vật, định nghĩa rõ thực thể/alias, nền tảng vũ trụ học (Heavenly Principles, Four Shades, Archons/Authorities/Gnoses, Khaenri'ah, Irminsul, Descenders) và các đại sự kiện (Natlan: Mavuika/Capitano; Snezhnaya `7.1`: cuộc đối đầu Ronova cùng hệ quả chưa ngã ngũ).
   - **Character Cognition Dossier (`content/cognition/<char>.json`):** Tách riêng cho từng nhân vật gồm `identity` (`public_role` vs `true_role`), `values`, `voice`, `disclosure`, `limitations`, `baseline`, `biography` (có `sequence`), `shared_history` (hỗ trợ gate `requires_story` đối chiếu `completed_optional`), `relationships` (`subject/predicate/object` + `query_aliases` riêng theo nhân vật để `"your father"` của Diluc trỏ về Crepus chứ không nhầm gia đình Aether) và `awareness` (`known_since` + `disclosure: public | guarded | private_with_traveler`). Mọi bản ghi hồ sơ cá nhân bắt buộc `characters == [char_id]` để không rò sang nhân vật khác qua retrieval.
   - **Hai chế độ hội thoại (`content/characters/<char>.json` + `engine.py`):**
     - *Scripted / Adapted dialogue*: đồ thị trạng thái (`root` và các node con), `12` lựa chọn/nhân vật (`120` lựa chọn trên `10` hồ sơ), chạy được cả khi offline.
     - *Free AI chat*: lắp ráp ngữ cảnh có ngân sách cứng **`20,000` ký tự** (ưu tiên giữ nguyên `foundation` briefs + `question_anchors`, cắt giảm có thứ tự từ `extractive_summaries` -> `earlier_exchanges` -> `recent` -> `lore` -> `notes`), chặn câu hỏi vượt patch `> 7.1` (`cutoff_guard`), trích dẫn hội thoại cũ dưới dạng `transcript_only` (để AI tự sửa sai nếu lượt cũ lỡ suy diễn), và bắt buộc trả về JSON Schema nghiêm ngặt `{"evidence_plan": [{"record_id", "claim_type"}], "reply"}` được kiểm chứng cục bộ trong `grounding.py` (chỉ chấp nhận `record_id` thực sự được cấp trong lượt đó, tối đa `8` record, lời thoại tối đa `180` từ / `2,500` ký tự).
   - **Scoped Memory & Lifecycle (`store.py` + `memory.py`):**
     - Cách ly theo `profile -> playthrough -> branch -> character_id` (kể bí mật cho Venti thì Jean/Mona không biết).
     - Chu trình 2 pha `pending -> ready -> ack -> committed` (chỉ khi UI hiển thị xong và gọi `ack` thì lượt thoại mới vào lịch sử/FTS5, tiến node đồ thị và trích xuất memory; hủy/lỗi/mất kết nối không tạo ký ức ma).
     - Trích xuất tự động bảo thủ bằng regex câu đơn ngôi thứ nhất (`memory.py`: `name`, `nickname`, `preference`, `promise`, `plan`, `fact`, hỗ trợ `Actually, ...` / `Correction: ...` và `Remember: ...`), có thứ tự ưu tiên `manual_edit > manual > explicit > automatic`, luôn gắn nhãn `player_reported` (không bao giờ biến lời người chơi thành canon thế giới). Hỗ trợ `fork` theo `checkpoint`, `forget_turn` và `reset_character_memory`.

---

## 2. Đối chiếu Roster `v0.3.3` với hiện trạng Mondstadt In-Game (`gameplay-lab`)

| Nhóm | Nhân vật | Trạng thái trong `eagle-character-chat` (`v0.3.3`) | Hiện trạng model / vị trí trong `gameplay-lab` & `Skin Library` (`D:`) |
| :--- | :--- | :--- | :--- |
| **Đã có cả Chat Dossier lẫn vị trí Nội thất Mondstadt (`7`)** | **Venti, Jean, Diluc, Kaeya, Lisa, Klee, Barbara** | Đầy đủ `characters/*.json` (`12` choices/người) + `cognition/*.json` + kiểm thử `gpt-6-luna` | Đang đứng tạo dáng LBS hướng mặt ra cửa trong các nội thất `Area 1` (`INT-01` Dawn Winery: Diluc; `INT-02` Angel's Share: Venti, Kaeya; `INT-03` Cathedral: Barbara; `INT-04` Knights HQ: Jean, Lisa; `INT-06` Alchemy Lab: Klee) dưới dạng static posed mesh thuộc `int_*.dff`, đồng thời có sẵn cặp ped `.dff/.txd` đã kiểm hash trên `D:\GTA Archive\Skin Library`. |
| **Đã có Chat Dossier, chưa đặt vào Nội thất `INT-01..06` (`3`)** | **Mona, Noelle, Fischl (+ Oz)** | Đầy đủ hồ sơ `v0.3.0` / `v0.3.3` (Fischl đi kèm Oz chung scope memory, trả lời `Oz:` trước khi gọi trực tiếp) | Đã kiểm hash cặp ped `.dff/.txd` của Mona, Noelle, Fischl trên `D:`; riêng Oz đã được Codex tách & convert thành `oz_static.dff/.txd` (`3,390` tris, `DXT5` alpha) trong `staging/project-eagle/character-noelle-fischl-20261028/oz-assets/`, chưa đưa vào runtime game. |
| **Đang đứng trong Nội thất Mondstadt nhưng chưa có Chat Dossier (`4`)** | **Rosaria, Diona, Albedo, Sucrose** | Chưa có file trong `content/characters/` và `content/cognition/` (báo cáo `v0.3.3` ghi Sucrose là phần việc tiếp theo) | Đang hiện diện sẵn trong nội thất `gameplay-lab` (`INT-03` Cathedral: Rosaria; `INT-05` Cat's Tail: Diona + 6 mèo; `INT-06` Alchemy Lab: Albedo, Sucrose) và có cặp skin trong `Skin Library`. |

---

## 3. Các điểm kỹ thuật cần bảo toàn khi phát triển tiếp

1. **Bảo toàn dữ liệu & chuẩn kiểm duyệt của Codex:**
   - Mọi nhân vật mới thêm vào `eagle-character-chat` phải đăng ký trong `content/world.json` (`character_order`), có đủ cặp `content/characters/<id>.json` (`12` adapted choices có `source_ids` HTTPS hợp lệ) và `content/cognition/<id>.json` (`characters: ["<id>"]` tuyệt đối riêng tư, tách rõ `biography` ổn định với `shared_history` có cờ `requires_story`, tách `awareness` với `disclosure`), giữ tổng context `< 20,000` ký tự và vượt qua toàn bộ `unittest` (`97+` checks) + kiểm thử live `gpt-6-luna` trên DB synthetic riêng (không chạm `conversations.sqlite3` thật của người dùng).
2. **Nếu tích hợp vào In-Game (`gta sa gameplay-lab`):**
   - Tuân thủ khóa kép `tools/eagle_coord_lock.py` (`game-write` và `ingame-runtime`).
   - Tách `placement manager` / proximity trigger khỏi `Engine` chat; định danh ký ức luôn bám `branch_id + character_id`, không bám `ped_handle` hay `model_id`.
   - Lưu ý kiến trúc 2 hướng cho actor trong Mondstadt: (a) tương tác theo tọa độ anchor với các nhân vật LBS đã gắn sẵn trong `INT-01..06` hoặc (b) cấp `Custom Ped ID` riêng (tránh dùng lại `190..195` vì đã gán cho dàn HSR/ZZZ và đang có mặt trong `MondstadtLifeAndBlips.cs`) cho các điểm đứng ngoài trời `M0/M1` (như Mona, Noelle, Fischl + prop `oz_static`), kết nối qua giao thức phân trang an toàn (`Protocol v2` / Sidecar HTTP) + VN HUD và giữ cơ chế `ack` sau khi hiển thị trang thoại.
