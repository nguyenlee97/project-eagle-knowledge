# Master Prompt Khởi Tạo & Tích Hợp Batch Nhân Vật Mondstadt Trên Antigravity (Chuẩn Tái Sử Dụng Cho Mọi Batch Tiếp Theo — Áp Dụng Ngay Cho Batch 1: `Sucrose`, `Diona`, `Amber`, `Eula`)

> **Cách dùng**: Copy toàn bộ khối nội dung dưới đường kẻ `---` bên dưới và dán thẳng vào một cuộc hội thoại Antigravity mới để thực thi trọn gói từ nghiên cứu Lore -> xây dựng Brain/Chatbot -> chuẩn bị/tạo & test Model 3D + Animation + Sprite -> mở rộng Bridge `MCHT v2` -> tích hợp `gameplay-lab` -> kiểm thử Offline & Live DirectX 9 trong game.
> Khi sang **Batch 2, Batch 3...**, chỉ cần cập nhật **Mục 1 (Danh sách nhân vật mục tiêu, ID, Skin & Tọa độ dự kiến)**, giữ nguyên toàn bộ quy chuẩn kỹ thuật từ **Mục 2 đến Mục 9**.

---

Bạn là agent kỹ thuật chính trên **Antigravity** phụ trách phát triển trọn gói hệ thống **Character Brain + Chatbot + 3D Ped/Animation + 2D Persona Expressions + In-Game Integration & QA** cho **Project Eagle (`gta sa gameplay-lab`)**, kế thừa toàn bộ tiêu chuẩn kỹ thuật của cả Codex và Antigravity trước đây.

Nhiệm vụ của hội thoại này là phát triển hoàn chỉnh, tích hợp và kiểm thử end-to-end (Offline + Live DirectX 9 trong game) cho **Batch 4 nhân vật Mondstadt mới**: **`Sucrose`, `Diona`, `Amber`, `Eula`** (nâng tổng nhân vật Mondstadt từ `10 -> 14`, tổng liên hệ `App #14 Contacts` từ `16 -> 20`), đồng thời **nâng cấp dứt điểm giao thức bộ nhớ chung CLEO `MCHT` từ trần `10` NPC lên `30` NPC (`MCHT v2`)** để mở đường cố định cho mọi batch nhân vật tiếp theo.

---

## 1. Phạm vi Batch hiện tại & Bảng thông số đầu vào (`Batch 1: NPC #11..#14`)

- **Đích tích hợp duy nhất**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Các hệ thống CẤM tự ý sửa đổi/ảnh hưởng**:
  - Bản lưu trữ `clean` trên ổ `D:\GTA Archive\Project Eagle\gta sa clean\gta sa clean`.
  - Gói Presentation đã nghiệm thu ngày `03/11` (`WibuMenu.asi`, `fronten2.txd`, `fronten3.txd` — xem `docs/project-eagle/presentation-current-state.md`).
  - Hệ thống trợ lý Paimon (persona, DB, provider riêng) và ứng dụng hẹn hò `App #13 WaifuLink` (`eagle_waifulink_v4_*.py`, `eagle_dating_sim.py`, `WLCG0.TXD`, `WLCG1.TXD`, peds `49428..49433`).
  - Nền tảng `EaglePhone OS v6.0 + Touchscreen` và bộ cỡ chữ lớn vừa nghiệm thu trên `hud.lua` (chỉ mở rộng danh sách/bộ đếm nhân vật một cách phẫu thuật, kiểm tra hash trước khi ghi).
- **4 Nhân vật mục tiêu trong Batch này**:
  1. **`sucrose`** (`Sucrose` — `idx = 10`, Custom `Ped ID = 49444`, model stem `mc_sucrose`):
     - **Skin sẵn có trong kho (`D:\GTA Archive\Skin Library\Project Eagle\numbered-skins\catalog.json`)**: `Sucrose__ca0ffa6c91af.dff` + `Sucrose__ca0ffa6c91af.txd` (`id=1942`) hoặc bản TXD tối ưu `Sucrose__txd_d01190b2c248ecb3.txd` (`id=3532`).
     - **Khử nhân bản nội thất (`Zero-Clone`)**: Đang có tượng mesh tĩnh `AID "538867"` nướng cứng trong `INT-06` Phòng Thí Nghiệm Giả Kim (`int_alchemy_lab.dff`) -> **bắt buộc gỡ riêng `#538867`, giữ nguyên Albedo `#525577`** chờ batch sau.
     - **Định hướng vị trí hợp lore**: Quầy Giả Kim ngoài trời tại Quảng trường Thành Mondstadt (`Sector M0`, `area = 0`, tách xa Kaeya/Mona/Fischl `>= 8m`) hoặc bên trong `INT-06` Phòng Giả Kim (nếu đặt trong nhà phải kèm `outdoor_gps` tại cửa chính tòa nhà).
  2. **`diona`** (`Diona` — `idx = 11`, Custom `Ped ID = 49445`, model stem `mc_diona`):
     - **Skin sẵn có trong kho**: `Diona__23d26599a51c.dff` + `Diona__23d26599a51c.txd` (`id=1487`).
     - **Khử nhân bản nội thất (`Zero-Clone`)**: Đang có tượng mesh tĩnh `AID "539022"` nướng cứng trong `INT-05` Quán Rượu Cat's Tail (`int_cats_tail.dff`) -> **bắt buộc gỡ riêng `#539022`, giữ nguyên toàn bộ 6 chú mèo tĩnh** trong quán làm đạo cụ sinh động!
     - **Định hướng vị trí hợp lore**: Hiên/cửa trước Quán Rượu Đuôi Mèo Cat's Tail (`Sector M0`, `area = 0`) hoặc bên trong quầy pha chế `INT-05` Cat's Tail (nếu đặt trong `INT-05`, xác minh chính xác `GET_AREA_VISIBLE` thực tế của `INT-05` và khai báo `outdoor_gps` tại cửa quán Cat's Tail).
  3. **`amber`** (`Amber` — `idx = 12`, Custom `Ped ID = 49446`, model stem `mc_amber`):
     - **Skin sẵn có trong kho**: Đối chiếu 2 bản `Amber__dc4e7f7ef596.{dff,txd}` (`id=2535`) và `Amber__08f55bcbb55b.{dff,txd}` (`id=2141` / `3556` — chỉ bị cờ dung lượng do TXD gốc > 10 MiB, sau khi nén DXT1/DXT5 `<= 512px` sẽ rất nhẹ), chọn bản có mặt, tỉ lệ cơ thể và rig xương đẹp nhất.
     - **Định hướng vị trí hợp lore**: Ngoài trời tại **Cổng Chính Thành Mondstadt / Đầu Cầu Đá dẫn vào thành (`Sector M0`, `area = 0`)** — khớp biểu tượng Kỵ Sĩ Trinh Thám đầu tiên đón Traveler đến Mondstadt (`0` xung đột mesh nội thất).
  4. **`eula`** (`Eula` — `idx = 13`, Custom `Ped ID = 49447`, model stem `mc_eula`):
     - **Skin sẵn có trong kho**: Đối chiếu `Eula__dbdf9c9de670.{dff,txd}` (`id=196`, đã chấm `rating: like`), `Eula SL__647ec8d2a133.{dff,txd}` (`id=450`, FadXploit 2.0) và `Eula__0910037b9e6b.{dff,txd}` (`id=1968`), chọn bản đẹp và rig sạch nhất.
     - **Định hướng vị trí hợp lore**: Ngoài trời tại **Đường tuần tra Bờ Hồ Sao Rơi / Mũi đá hướng Long Tích (`Sector M1`, `area = 0`, tách xa vị trí Klee)** hoặc sân thoáng gần **Good Hunter (`Sector M0`, `area = 0`)** (`0` xung đột mesh nội thất).

---

## 2. Bước 0 — Đọc Tài liệu Nền tảng, Đăng ký Phạm vi & Kỷ luật Khóa Kép

Trước khi thực hiện bất kỳ chỉnh sửa nào, bắt buộc đọc đầy đủ các file chuẩn sau:
1. `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `C:\Users\LENOVO\Desktop\GTA\GEMINI.md`
2. `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
3. `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\dialogue\character-system-full-handoff-2026-11-04.md` (kiến trúc toàn diện của Character System do Codex bàn giao)
4. `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\mondstadt-persona-chat-and-contacts-2026-11-04.md` (kiến trúc tích hợp 3D + Persona HUD + 61 Sprite không thủng alpha + Cỡ chữ lớn + App #14 Contacts)
5. `C:\Users\LENOVO\Desktop\GTA\tools\eagle-character-chat\README.md`, cộng với 1 cặp nhân vật mẫu (`content/characters/noelle.json` + `content/cognition/noelle.json` và `fischl.json`)
6. Tham chiếu bộ script thi công chuẩn ở `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\mondstadt-persona-chat-20261104\` (`build_world_assets_and_bridge.py`, `build_sprites_and_ui_tex.py`, `apply_sprite_and_font_upgrade.py`, `test_part_a_offline.py`, `run_part_b_live_ingame_qa.py`).

**Quy tắc điều phối & Khóa (`C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py`)**:
- Tạo phiếu công việc mới tại `docs/project-eagle/work-items/` và tạo thư mục staging độc lập cho batch này: `staging/project-eagle/mondstadt-batch1-sucrose-diona-amber-eula-<YYYYMMDD>/`.
- Kiểm tra `C:\Python310\python.exe tools\eagle_coord_lock.py status`.
- **100% công việc nghiên cứu lore, viết brain JSON, chạy unit test SQLite tạm, nén `.dff/.txd`, tách nền sprite `512x512`, biên dịch CLEO `.cs` phải làm trong staging ngoài khóa.**
- Chỉ giữ khóa `game-write` trong vài giây khi ghi/patch vào `gameplay-lab` (kiểm tra lại SHA-256 của file đích ngay trước lúc ghi để không đè lên thay đổi của agent khác).
- Chỉ giữ khóa `ingame-runtime` khi khởi chạy `gta_pe.exe` để test trực tiếp trong game (Part B), và nhả sạch cả 2 khóa ngay khi hoàn tất.
- Lưu ý môi trường Windows PowerShell 5.1: không dùng toán tử `&&` của bash; luôn cấu hình `sys.stdout.reconfigure(encoding="utf-8")` trong script Python và tránh import `scipy` trên `C:\Python310` (do lệch ABI với `numpy 2.2.6`, dùng thuần `PIL` + `numpy` + `collections.deque`).

---

## 3. Giai đoạn 1 — Nghiên cứu Lore & Thu thập Dữ liệu Nhân vật (`4-Tier Source Ladder`)

- **Phối hợp Subagent trên Antigravity**: Dùng `invoke_subagent` (`TypeName="research"` hoặc `"self"`, `Model="inherit"`) giao khảo sát độc lập cho từng nhân vật, xuất hồ sơ nguồn vào `staging/.../research/<char_id>.md`. Tuyệt đối không để nhiều subagent cùng sửa chung một file; agent chính tự rà soát chéo và tổng hợp.
- **Thang nguồn chuẩn 4 bậc (bắt buộc tuân thủ)**:
  1. **Bậc 1 — Văn bản chính thức trong game (Độ tin cậy cao nhất)**: Character Profile (`Character Details`, `Character Story 1..5`, `Vision`), toàn bộ `Voice-Overs` (`About Us`, `About <Character>`, sở thích/món ăn, sinh nhật, bậc đột phá), thoại `Serenitea Pot / Companion` & bộ nội thất yêu thích, transcript nhiệm vụ Ma Thần / Truyền Thuyết / Đồng Hành (Hangout) / Sự kiện, Character Demo & Collected Miscellany.
  2. **Bậc 2 — Kho transcript cộng đồng (Genshin Impact Wiki `/Profile`, `/Voice-Overs`, `/Companion`, trang thoại quest)**: Chỉ lấy phần **nguyên văn văn bản/lời thoại trong game**, tách biệt rõ với phần tóm tắt diễn giải của biên tập viên wiki.
  3. **Bậc 3 — Phân tích thứ cấp (`moriasmoday.com`, bài phân tích lore)**: Chỉ dùng làm đầu mối đối chiếu chiều sâu tính cách/quan hệ; mọi chi tiết đưa vào brain phải truy ngược được về nguồn Bậc 1/Bậc 2. Nếu trang web lỗi/không truy cập được hoặc chỉ là suy đoán của fan, phải ghi nhận trung thực chứ không bịa nguồn hoặc biến giả thuyết thành canon.
  4. **Bậc 4 — Video gameplay có timestamp cụ thể**: Dùng bổ khuyết khi transcript chữ bị thiếu cảnh.
- **Các chốt tính cách & ranh giới cốt truyện bắt buộc cho 4 nhân vật**:
  - **`sucrose`**: Trợ lý của Albedo tại Đội Kỵ Sĩ Tây Phong, chuyên ngành Giả Kim Sinh Học (*Bio-Alchemy* — cải tạo giống cây/ngọt hoa với ước mơ tạo ra khu vườn thần tiên thu nhỏ từ lời hứa tuổi thơ với hai người bạn cũ đã chia xa). Rụt rè trong giao tiếp đời thường nhưng cực kỳ say sưa, khúc chiết và kiên định khi nói về thí nghiệm, mẫu vật và giả kim; luôn gọi kính trọng `"Mr. Albedo"`, làm việc cùng Timaeus, quý mến Klee và kết bạn chân thành với Collei (*Windblume's Breath* — lưu ý đây là sự kiện giới hạn, không mặc định Aether nhớ từng chi tiết nếu chưa gợi mở). Tránh biến Sucrose thành nhân vật một màu chỉ biết lắp bắp xin lỗi.
  - **`diona`**: Pha chế trưởng quán Cat's Tail xuất thân Thanh Tuyền Trấn (*Springvale*), con gái thợ săn Draff, mang dòng máu Kätzlein (tai và đuôi mèo thật, ghét bị véo tai/đuôi hoặc bị coi như thú cưng). Ghét cay ghét đắng rượu cồn vì cha cô cứ uống say là đánh mất hình ảnh người cha đáng ngưỡng mộ thời thơ ấu -> thề pha ra ly rượu dở nhất thế gian để sập tiệm ngành rượu Mondstadt (đơn phương coi Diluc / Dawn Winery là đối thủ không đội trời chung, dù không hề biết Diluc cũng ghét rượu và càng không biết Diluc là Darknight Hero!), nhưng lại mang **lời chúc phúc của Tinh Linh Nước suối Thanh Tuyền (*Spring Fairy*)** từ bé khiến bất cứ ly cocktail nào cô pha cũng ngon tuyệt đỉnh. Các cảnh đi tìm mèo / hái nguyên liệu pha chế cùng Aether trong **Hangout Act I (*The Cat and the Cocktail*)** bắt buộc gắn cờ `requires_story: "diona_hangout"`.
  - **`amber`**: Kỵ Sĩ Trinh Thám (*Outrider*) duy nhất còn trụ lại Đội Kỵ Sĩ Tây Phong sau khi ông nội cô (người gốc Liyue sáng lập đội Outrider) đột ngột rời đi; vô địch bay lượn Mondstadt, tác giả búp bê nổ *Baron Bunny*. Là người đầu tiên gặp gỡ và cấp Phong Chi Dực cho Traveler Aether ở **Prologue Act I** (lịch sử canon cốt lõi đã xảy ra trong mốc `post_71`!). Với **Story Quest *Lepus Chapter: Act I*** (thi lấy bằng bay & bắt tên trộm "Raptor"), gắn cổng `requires_story: "amber_story_act1"` hoặc tách rõ phần quen biết Prologue với chi tiết nhiệm vụ riêng. Quan hệ bạn thân cực kỳ gắn bó với Eula, thân thiết với Collei, Jean, Kaeya, Klee, Noelle.
  - **`eula`**: Đội Trưởng Đội Du Kích (*Captain of the Reconnaissance Company* / *Spindrift Knight*) thuộc Đội Kỵ Sĩ Tây Phong, hậu duệ gia tộc quý tộc cũ Lawrence bị cư dân Mondstadt mang nặng thành kiến nhưng tự mình đứng về phía Mondstadt tự do. Câu cửa miệng `"vengeance"` / `"mark my words"` là tấm khiên tự trọng pha chút hài hước khô khan để hóa giải sự thù địch của đám đông và ghi nhớ từng ân tình nhỏ nhất (từ Amber, Jean, Yanfei, đầu bếp Sara, Traveler) để trả ơn gấp bội, tuyệt đối không phải ác ý thật. Gắn cờ `requires_story: "eula_story_act1"` cho cảnh tập nghi thức quý tộc Lawrence và phá âm mưu chú Schubert cùng Aether (*Aphros Delos Chapter: Act I*); cẩn trọng với các sự kiện giới hạn ở Dragonspine / Veluriyam Mirage.

---

## 4. Giai đoạn 2 — Xây dựng Brain 5 Lớp & Grounding trong `tools/eagle-character-chat`

Toàn bộ dữ liệu hội thoại dùng **`English-only`** và đặt trong mốc thế giới **`post_71`** (`v0.3.3+`):

1. **Tạo `tools/eagle-character-chat/content/characters/<id>.json` (`sucrose`, `diona`, `amber`, `eula`)**:
   - Đúng `schema_version: 1` với `id`, `name`, `title`, `tagline`, `persona`, `knowledge_policy`, `greeting`, `source_ids`, và cây `nodes` gồm `root` + 3 nhánh con = **đúng `12` lựa chọn `choices`** mỗi nhân vật (`"content_kind": "adapted"`, gắn `source_ids` đầy đủ).
   - **Cấm chép nguyên văn thoại Serenitea Pot hay quest game**: `greeting` và `12` câu `reply` phải được biên soạn mới (`adapted`) tự nhiên, đúng giọng nhân vật và khớp chính xác với bối cảnh vị trí đứng dự kiến trên bản đồ Mondstadt.
2. **Tạo `tools/eagle-character-chat/content/cognition/<id>.json` (`sucrose`, `diona`, `amber`, `eula`)**:
   - Đầy đủ `identity` (`public_role`, `true_role`), `values`, `voice`, `disclosure`, `limitations`, `source_ids`, và 5 mảng nhận thức tách biệt:
     - `baseline` & `biography`: Nhân thân, nghề nghiệp, lịch sử cá nhân và Vision có sẵn độc lập trước khi trò chuyện; việc RAG không khớp chi tiết sâu chỉ làm thu hẹp mức độ chắc chắn/chi tiết, không bao giờ gây mất trí nhớ căn cốt.
     - `shared_history`: Phân tách rõ tiền đề quen biết `post_71` (hoặc Prologue canon của Amber) với các nhiệm vụ tùy chọn cần cờ `"requires_story"` (`"diona_hangout"`, `"amber_story_act1"`, `"eula_story_act1"`, v.v.). Các biến cố lớn ở các quốc gia khác sau Mondstadt chỉ là tin tức được nghe kể (`reported`), không phải ký ức tận mắt chứng kiến (`eyewitness`).
     - `relationships`: Khai báo đầy đủ `entity_ids`, `relationship` (`subject`, `predicate`, `object`) và `query_aliases` kết nối chặt giữa 14 nhân vật Mondstadt.
     - `awareness`: Ghi rõ `known_since` và mức `disclosure` (`"public" | "guarded" | "private_with_traveler"`).
   - **QUY TẮC CÔ LẬP BÍ MẬT TUYỆT ĐỐI**: Mọi record cá nhân BẮT BUỘC đặt `"characters": ["<id>"]` (cấm dùng `"*"` cho thông tin riêng!). Cả `Sucrose`, `Diona`, `Amber`, `Eula` đều **KHÔNG biết Venti là Barbatos** và **KHÔNG biết Diluc là Darknight Hero**.
3. **Cập nhật `content/world.json` & `content/cognition/world.json` (và hồ sơ liên đới nếu cần)**:
   - Mở rộng `character_order` trong `content/world.json` lên 14 nhân vật, bổ sung `sources` và các bản ghi công khai.
   - Bổ sung thực thể & bí danh (`entities`, `query_aliases`) trong `content/cognition/world.json` cho `sucrose`, `diona`, `amber`, `eula` cùng các nhân vật/địa danh liên quan (`albedo`, `timaeus`, `draff`, `cats_tail`, `springvale`, `lawrence_clan`, `mika`, `collei`...) để câu hỏi chéo giữa cả 14 nhân vật truy xuất chính xác.
4. **Bảo toàn cơ chế Grounding `20,000` ký tự & Memory SQLite v2**:
   - Giữ nguyên ngân sách `20,000` ký tự (`grounding.py`), phong bì JSON `{"evidence_plan":[{"record_id":"...","claim_type":"..."}],"reply":"..."}` (`<= 8` `record_id` hợp lệ trong lượt, `<= 180` từ / `2,500` ký tự), cơ chế kiểm chứng nguồn gốc cục bộ (không tốn cuộc gọi API phụ), thuộc tính `player_reported` cho lời người chơi kể và chế độ `transcript_only` cho câu trả lời AI cũ.
   - Viết thêm unit test trong `tools/eagle-character-chat/tests/` kiểm tra schema 14 nhân vật, cách ly bí mật Barbatos/Darknight Hero, cờ `requires_story` và truy xuất chéo.

---

## 5. Giai đoạn 3 — Chuẩn bị/Tạo Model 3D, Kiểm thử Model & Animation, và Tạo 24 Sprite `512×512`

### 5.1. Chọn lọc / Chuyển đổi Model 3D (`.dff/.txd`) & Kiểm thử Rig Xương Offline
- Trích xuất 4 cặp ped từ `D:\GTA Archive\Skin Library\Project Eagle\numbered-skins\catalog.json` sang staging dưới tên chuẩn `mc_sucrose.{dff,txd}` (`49444`), `mc_diona.{dff,txd}` (`49445`), `mc_amber.{dff,txd}` (`49446`), `mc_eula.{dff,txd}` (`49447`).
- **Quy chuẩn chung nếu gặp nhân vật/đạo cụ chưa có sẵn model GTA SA trong kho (áp dụng cho mọi batch)**:
  - **Với NPC `CPed` sống**: Tìm nguồn mod GTA SA ped đã rig sẵn xương chuẩn (`Clump 0x10` + `HAnim PLG 0x11E` + `Skin PLG 0x116`). Nếu phải convert từ PMX/FBX/DAE qua Blender + DragonFF (`staging/project-eagle/dryxio-tools/DragonFF-master`), bắt buộc map đúng cây xương Biped GTA SA (`Root`, `Pelvis`, `Spine`, `Spine1`, `Neck`, `Head`, `L/R Clavicle/UpperArm/Forearm/Hand`, `L/R Thigh/Calf/Foot`), chuẩn hóa tổng weight `= 1.0` (tối đa 4 xương/đỉnh) và xuất chuẩn RenderWare GTA SA (`0x1803FFFF`).
  - **Với đạo cụ/familiar đi kèm dạng `CObject` tĩnh** (như `oz_static.{dff,txd}` ở `staging/project-eagle/character-noelle-fischl-20261028/oz-assets/`): **CẤM** giảm mặt bằng bước nhảy `conv_tris[::step]` hay gộp đỉnh thô `round(..., 2)` làm rách lưới; giữ nguyên `DXT5` + mipmap cho vật liệu có alpha và đóng kèm `COL3`.
- **Tối ưu & Kiểm định kỹ thuật `.dff/.txd` trước khi nạp archive**:
  - Cắt gọn chunk RenderWare chuẩn (`0x10` cho `.dff`, `0x16` cho `.txd`), nén mọi raster `> 512px` hoặc chưa nén về **DXT1 (không alpha) / DXT5 (có alpha) `<= 512px` có đầy đủ mipmap** qua `optimize_skin_txd`.
  - Viết bài test đọc ngược kiểm chứng từng model: hợp lệ cấu trúc `Clump` + `Skin PLG` + `HAnim PLG`, **100% tên texture trong Material của `.dff` đều có mặt trong `.txd`** (chống lỗi trắng xóa texture trong game), không có đỉnh `NaN/Inf`, chiều cao bounding box hợp lệ (`~1.45m–1.95m` theo trục `Z-up`).

### 5.2. Sinh 24 Sprite Biểu cảm `512×512` Không Thủng Alpha + 4 Icon Danh bạ
- **LUẬT CỨNG TẠO ẢNH (KHÔNG NGOẠI LỆ)**: **CHỈ ĐƯỢC PHÉP dùng subagent `image-generator` nội bộ của Antigravity** (hạn mức `100` hình / cửa sổ trượt `5 tiếng`). **CẤM TUYỆT ĐỐI** gọi bất kỳ API tạo ảnh bên ngoài nào (OpenAI `gpt-image-*`, `dall-e-*`, Replicate, Stability...). Để tiết kiệm tối đa quota, hãy yêu cầu `image-generator` sinh **1 tấm Expression Sheet 6 ô (`3×2`) độ phân giải cao trên nền xanh lá thuần `#00FF00` tương phản mạnh với trang phục** cho mỗi nhân vật (chỉ tốn 4 lượt ảnh cho cả batch; lưu ý trang phục Sucrose có tông xanh nhạt nên chỉ định rõ nền `#00FF00` neon tách biệt hoặc `#0047AB` / chroma không trùng màu tóc/áo để biên cắt sạch 100%!). Nếu chạm `429 RESOURCE_EXHAUSTED`, dừng bước tạo ảnh ngay và báo cáo trung thực.
- Xuất đủ **6 biểu cảm `512×512` RGBA cho mỗi nhân vật** vào `data/project-eagle/character-chat/sprites/`:
  `<id>_neutral.png`, `<id>_happy.png`, `<id>_serious.png`, `<id>_surprised.png`, `<id>_sad_worried.png`, `<id>_smug_teasing.png` (nâng tổng kho sprite từ `61` -> `85` file).
- **Thuật toán tách nền chống thủng lỗ trong suốt (Bắt buộc áp dụng từ `build_sprites_and_ui_tex.py`)**:
  - **CẤM** lọc màu chroma toàn cục ngưỡng rộng (sẽ xuyên qua nét viền đen làm thủng tóc xanh đen của Eula, mũ/kính của Sucrose, nơ của Amber!).
  - Chỉ dùng **Flood-Fill từ biên ngoài với ngưỡng chặt (`tol_hard = 8.2`) + rào cản đạo hàm màu (`gradient <= 7.5`) dừng ngay trước nét mực đen anime**, khử rìa `1–2px` ngoài biên và **ép cứng `alpha = 255` đặc hoàn toàn cho mọi điểm ảnh nằm bên trong đường bao nhân vật**.
  - Bắt buộc ghép cả 24 sprite mới lên bảng kiểm định nền hồng neon `#FF00FF` và dùng `read_file` kiểm tra trực quan từng ô để đảm bảo **0 lỗ thủng hồng bên trong nhân vật, 0 viền rác ngoài rìa, không bị cắt mất tai mèo Diona hay mũ/nơ của Sucrose/Amber**.
- Tạo thêm 4 icon danh bạ vuông bo góc `ep_mc_sucrose`, `ep_mc_diona`, `ep_mc_amber`, `ep_mc_eula` (`64×64` DXT5) để đóng vào `models/hud.txd` (`flags=0x01`), `CUSTOM/EAGLEPHONE_UI.TXD` và `models/txd/EAGLEUI.TXD`.

---

## 6. Giai đoạn 4 — Kiểm thử Chatbot Offline & Live Rate-Limited Evaluation

1. **Kiểm thử Offline (trên SQLite tạm, 0 tốn API)**:
   - Chạy `C:\Python310\python.exe -m unittest discover -s tools\eagle-character-chat\tests -v` và `node --check tools\eagle-character-chat\static\app.js` đạt `100% PASS`.
   - **CẤM TUYỆT ĐỐI** khởi tạo `Store` test vào file thật `data/project-eagle/character-chat/conversations.sqlite3` của người chơi (luôn dùng file SQLite tạm trong `staging/` hoặc `tempfile`).
2. **Kiểm thử Live hành vi với `gpt-6-luna` (Tuân thủ kỷ luật Rate Limit)**:
   - Dùng cấu hình `data/project-eagle/character-chat/connection.json` (OpenAI direct `https://api.openai.com/v1`, model `gpt-6-luna`, đọc khóa từ `EAGLE_CHARACTER_OPENAI_API_KEY` — **TUYỆT ĐỐI KHÔNG in/log/lưu giá trị khóa API ở bất kỳ đâu**).
   - Chạy đánh giá tuần tự trên DB tạm: **tối đa 1 request đang bay**, **nghỉ `>= 11.0s–12.5s` giữa hai lượt gọi**, kiểm tra header rate-limit, **không auto-retry**, **không gọi thêm model trả phí để chấm điểm** (kiểm tra `evidence_plan` cục bộ + tự đọc xét duyệt câu trả lời), dừng ngay nếu gặp `429`.
   - Sát hạch đủ 5 tình huống cho mỗi nhân vật trong 4 nhân vật mới: (a) chào hỏi & công việc thường ngày đúng cá tính, (b) hỏi dò bí mật Venti=Barbatos / Diluc=Darknight Hero -> không rò rỉ, (c) hỏi kỷ niệm Hangout / Story Quest tùy chọn khi chưa bật cờ -> từ chối nhận vơ lịch sự, (d) người chơi cố tình gài thông tin sai canon -> nhân vật giữ vững nhận thức đúng trong vai (`player_reported`), (e) nhớ lại thông tin người chơi vừa chia sẻ sau nhiều lượt.

---

## 7. Giai đoạn 5 — Nâng cấp Cầu CLEO `MCHT v2` (`30` NPC) + Tích hợp Bản đồ & Điện thoại

### 7.1. Mở rộng Khối Shared Memory `MCHT` trước nhân vật thứ 11 (`Bắt buộc thực hiện đầu tiên khi tích hợp`)
- Trong bản cũ, `cleo/EagleMondstadtChatBridge.cs` (`0x00CAFE40` = `'MCHT'`, `0x00CAFE44` = `shm_ptr`, biên dịch bằng `tools/eagle-dialogue/bridge/assembler.py` — **đây là bytecode CLEO GTA SA, không phải C#!**) chỉ cấp `ALLOCATE_MEMORY` `256` byte cho `10` NPC (`idx 0..9`): `ped_handles` ở `128..167` và `ped_ptrs` ở `168..207`. Nếu ghi `idx = 10` vào offset cũ sẽ đè hỏng `ped_ptr[0]`!
- **Thiết kế `MCHT v2` chuẩn hóa cho `30` NPC (`idx 0..29`, khối `768` byte)**:
  - Nâng `ALLOCATE_MEMORY` (`0x0AC8`) lên **`768` byte** và xóa trắng về `0` khi khởi tạo.
  - Giữ nguyên vùng header/command/camera ở `0..127` và `player_hdg / npc_hdg` ở `212 / 216`; ghi `shm_version = 2` tại offset `220` và `npc_capacity = 30` tại offset `224`.
  - Dời mảng `ped_handles[0..29]` sang **`256 + idx*4` (`256..375`)** và mảng `ped_ptrs[0..29]` sang **`384 + idx*4` (`384..503`)**.
  - Thanh ghi cục bộ CLEO `15@` (`spawned_mask`) quản lý gọn các bit `0..29` (không chạm bit dấu 31), và vòng quét NPC tiếp tục dùng các biến tạm `16@..27@` sẵn có nên không vượt giới hạn `32` biến cục bộ (`0@..31@`) của CLEO.
  - Cập nhật đồng bộ cả trình sinh bytecode CLEO lẫn `eagle_mondstadt_chat_bridge.py` (kiểm tra khớp `shm_version == 2`).

### 7.2. Quy hoạch Tọa độ `.COL3`, Khử Nhân bản (`Zero-Clone`) & Đồng bộ UI
- **Kiểm chứng vật lý `.COL3` & Camera 3D Two-Shot**:
  - Dùng `FastColRaycaster` kiểm tra từng vị trí của `Sucrose`, `Diona`, `Amber`, `Eula`: độ phẳng mặt sàn bán kính `1.6m <= 0.05m`, khoảng trống trên đầu `>= 2.6m`, cách mọi NPC khác `>= 6.0m`, và phép chiếu ma trận camera Two-Shot giữ Aether + NPC nằm gọn ở nửa trái màn hình (`x_norm ∈ [0.12, 0.49]`), nhường trọn nửa phải (`0.52..0.99`) cho CG `512×512`.
- **Khử nhân bản (`Zero-Clone`)**:
  - Biên dịch lại nội thất Mondstadt (`patch_interiors_int01_int06.py` trong pipeline `build_world_assets_and_bridge.py`) với `removed_aids` bổ sung `"538867"` (Sucrose trong `INT-06`, giữ Albedo `"525577"`) và `"539022"` (Diona trong `INT-05`, giữ nguyên 6 chú mèo tĩnh), rồi đóng gói vào `CUSTOM/mondstadt_m1_wilds.img`.
  - Đăng ký `49444..49447` vào `data/peds.ide` và nạp `mc_sucrose/diona/amber/eula.{dff,txd}` vào `CUSTOM/custom_mods.img`.
- **Đồng bộ `eagle_mondstadt_chat_bridge.py`, `EagleCompanion.py`, `eagle_phone_ui.py` & `hud.lua`**:
  - Mở rộng bảng nhân vật Mondstadt lên `14` người (kèm luật phân loại biểu cảm `classify_expression_and_anim` hợp cá tính từng nhân vật và bộ lọc `sanitize_cfont_text` có `.replace("\\n", " ")`).
  - Chuyển bộ đếm danh bạ `App #14 Contacts` sang tính động theo danh sách (hoặc cập nhật chính xác thành **`14 Mondstadt / 20 All`**: `1.All (20)`, `2.Mondstadt (14)`, `3.Waifus (6)` trong cả `HOME_APPS_EN/VI`, `eagle_phone_ui.py` và `hud.lua`).
  - **Bảo toàn tuyệt đối** giao diện cảm ứng `EaglePhone OS v6.0` và cỡ chữ lớn đã nghiệm thu (`0.312×0.664` thoại chính Persona, `0.272×0.578` thẻ nổi `[E] TALK TO`, `0.192×0.408` tin nhắn DM trong `App #14`).

---

## 8. Giai đoạn 6 — Kiểm thử 2 Tầng (`Part A Offline` + `Part B Live DirectX 9 In-Game`)

### Part A — Kiểm thử Tự động Offline (Ngoài khóa, bắt buộc PASS 100% trước khi apply)
Viết và chạy `test_part_a_offline.py` trong thư mục staging của batch để xác nhận:
1. Đủ `85` sprite `512×512` đạt `alpha = 255` bên trong bóng nhân vật, `0` lỗ thủng nền, và nạp thử `MCSP0/1.TXD` đúng chuẩn BGRA8888 (`1,048,744` bytes).
2. Toàn bộ file `.dff/.txd` của 4 nhân vật mới có đầy đủ xương `Skin PLG` + `HAnim PLG`, khớp 100% tên texture material, không vỡ chunk; nội thất `INT-05` & `INT-06` đã gỡ đúng mesh Sucrose/Diona mà vẫn giữ Albedo + 6 mèo; 3 file TXD giao diện chứa đủ `14` icon `ep_mc_*`.
3. Kiểm chứng không chồng lấn địa chỉ bộ nhớ trên toàn dải `idx 0..29` của khối `768` byte `MCHT v2` và kiểm chứng toán học góc camera Two-Shot cho đủ `14/14` NPC.
4. Full suite `tools/eagle-character-chat/tests` PASS + luồng E2E giả lập trên **SQLite tạm** (`[LOCK]` -> gặp trực tiếp mở khóa -> lưu hội thoại -> `Remote DM` trong `App #14` đọc chung bộ nhớ).
5. `py_compile` toàn bộ Python script và cân bằng cú pháp `hud.lua`.

### Part B — Nghiệm thu Trực tiếp Trong Game (`gta_pe.exe` `1920×1080` dưới khóa `ingame-runtime`)
1. Sao lưu nguyên trạng `ingame_contacts_state.json` của người chơi trước khi test; giữ khóa `game-write` ngắn gọn để apply (kèm manifest SHA-256 before/after + script rollback một lệnh), nhả `game-write` rồi lấy khóa `ingame-runtime`.
2. Khởi chạy game và sidecar, điều khiển Aether đến gặp trực tiếp cả **4 nhân vật mới (`Sucrose`, `Diona`, `Amber`, `Eula`)** cộng tối thiểu **1–2 nhân vật cũ (`Venti` `idx=0`, `Fischl + Oz` `idx=9`)** để chứng minh `MCHT v2` chạy mượt trên cả dải cũ và mới.
3. Chụp ảnh màn hình DirectX 9 `1920×1080` ở từng điểm kiểm tra và **bắt buộc mở đọc trực tiếp từng ảnh bằng `read_file`** để xác nhận bằng mắt thật:
   - **3D Model & Animation**: Nhân vật đứng đúng cao độ mặt sàn, không trắng texture, không biến dạng khung xương, không còn tượng tĩnh trùng lặp trong `INT-05`/`INT-06`; khi nhấn `[E]`, Aether và NPC quay mặt trực diện vào nhau (`CMatrix`) và diễn hoạt tự nhiên các động tác hội thoại (`IDLE_chat`, `factalk`, `endchat_01..03`, `XPRESSscratch`).
   - **Persona HUD & Sprite**: Khung Two-Shot nửa trái thoáng đẹp, CG bán thân nửa phải sắc nét không thủng nền trong suốt, chữ lớn rõ ràng dễ đọc, đổi biểu cảm mượt mà.
   - **Live Chatbot & App #14 Contacts (`20` liên hệ)**: Nhắn thử câu thoại tự do `[F6]` nhận phản hồi `gpt-6-luna` chuẩn vai diễn (nghỉ đủ cooldown), mở khóa `NEW SOCIAL LINK UNLOCKED`, kiểm tra `App #14 Contacts` hiển thị đúng `20` liên hệ (`14` Mondstadt + `6` Waifus), cắm GPS khi `[LOCK]` và nhắn `Remote DM` khi `[OPEN]` giữ liền mạch trí nhớ hội thoại.
4. Xác nhận `moonloader.log` và log sidecar/bridge có **`0` lỗi Lua / Python exception**.

---

## 9. Hoàn tất, Khôi phục Trạng thái Sạch & Bàn giao

- Khôi phục lại `ingame_contacts_state.json` về đúng trạng thái trước QA của người chơi (để 4 nhân vật mới ở trạng thái `[LOCK]` sạch sẵn sàng cho người chơi tự đi gặp mở khóa trong trải nghiệm thật, đồng thời không làm bẩn `conversations.sqlite3`).
- Nhả sạch cả hai khóa `ingame-runtime` và `game-write`, kiểm tra lại bằng `python tools\eagle_coord_lock.py status`.
- Ghi báo cáo nghiệm thu đầy đủ tại `docs/project-eagle/`, cập nhật phiếu công việc sang `done` và bổ sung tóm tắt bàn giao vào `docs/project-eagle/shared-agent-workflow.md`.
