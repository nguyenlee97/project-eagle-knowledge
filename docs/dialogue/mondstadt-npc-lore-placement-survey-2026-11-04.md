# Khảo sát Lore Genshin & Tọa độ Thực tế (`M0/M1/INT`) Đặt 10 NPC Mondstadt Character Chat

- **Ngày khảo sát**: `2026-11-04`
- **Agent thực hiện**: `Antigravity` (`c71a77f9-97e6-4a68-aba6-9fb3b4acf926`)
- **Target runtime**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Nguyên tắc thiết kế từ người dùng**: Đặt vị trí hợp lý theo lore Genshin Impact, **ưu tiên ngoài trời và không đặt trong nhà quá nhiều**, đồng bộ với cơ chế gặp trực tiếp mở khóa Danh bạ điện thoại (Social Link / Confidant) và Persona HUD 6 biểu cảm.
- **Phạm vi tác động ở bước này**: Chỉ đọc (`0` chỉnh sửa runtime, archive hay DB).

---

## 1. Tổng quan Tỷ lệ Phân bổ: **8 Ngoài Trời (`80%`) — 2 Trong Nhà (`20%`)**

Qua đối chiếu đồng thời **(a)** thói quen sinh hoạt & Nhiệm vụ Truyền thuyết/Đồng hành trong Genshin Impact, **(b)** lời chào mở đầu (`greeting`) + cây hội thoại (`nodes`) trong `tools/eagle-character-chat/content/characters/*.json`, và **(c)** phép bắn tia mặt sàn `.COL3` (`FastColRaycaster`, kiểm tra độ phẳng bán kính `1.6m` và khoảng không trên đầu `2.6m`) trên `mondstadt_m0_city.col` & `mondstadt_m1_wilds.col`:

- **Ngoài trời Ngoại ô `Sector M1` (`3` NPC)**: **Venti**, **Diluc**, **Klee** — đặt tại 3 thắng cảnh biểu tượng nhất ngoài thành (Đại Thụ Phong Khởi Địa, Sân Vườn Nho Tửu Trang Dawn Winery, Bờ Hồ Sao Rơi), giúp chuyến lái xe/dạo bộ quanh ngoại ô Mondstadt luôn có điểm gặp gỡ sống động.
- **Ngoài trời Nội thành `Sector M0` (`5` NPC)**: **Fischl (+ Oz)**, **Mona**, **Kaeya**, **Noelle**, **Barbara** — rải đều theo trục cao độ từ Phố Chợ tầng dưới (`Z ≈ 6.6m`) -> Khu Dân Cư Nam -> Quảng trường Đài Phun Nước (`Z = 12.6m`) -> Sân trước Trụ sở Kỵ Sĩ (`Z = 58.1m`) -> Tiền sảnh Sân thượng Đại Giáo Đường (`Z = 56.8m`), không dồn cục tại một điểm.
- **Trong nhà `INT-04` (`Area 1`, chỉ `2` NPC)**: **Jean** và **Lisa** — hai nhân vật duy nhất gắn chặt với bàn làm việc Quyền Đội Trưởng và Thư viện Đội Kỵ Sĩ (đặc biệt lời chào cứng của Lisa trong `lisa.json` là *"Come in and settle down; the books can wait a moment"*, bắt buộc ngữ cảnh trong thư viện). Cả hai nằm chung trong đúng 1 cửa `MD_KNI` ngay sau lưng sân tập của Noelle, đứng cách nhau `6.3m` (văn phòng vs cánh kệ sách) để không chồng vùng tương tác.

---

## 2. Bảng Quy hoạch Chi tiết 10 Nhân vật Mondstadt

| # | Nhân vật | Khu vực | Vị trí cụ thể | Tọa độ `(X, Y, Z)` & `Heading` | Độ lệch sàn `1.6m` | Căn cứ Lore Genshin & Khớp lời thoại `eagle-character-chat` |
| :-: | :--- | :---: | :--- | :--- | :-: | :--- |
| 1 | **Venti** (`venti`) | Ngoài trời `M1` | Dưới tán Đại Thụ Vennessa — Phong Khởi Địa (`Windrise`) | `(-3813.0, -3324.0, 31.14)`, `Hdg 180°`, `Area 0` | `0.000m` | Điểm hẹn biểu tượng cuối Chương Mở Đầu & *Carmen Dei*; nơi Venti đón gió gảy đàn và có thể trò chuyện riêng tư về Barbatos/Dvalin. Khớp `greeting`: *"The wind brought me a tune, but I think it was waiting for an audience."* *(Dự phòng nếu muốn gặp trong thành: Quảng trường Tượng Barbatos `-4380.0, -2950.0, 48.00`)*. |
| 2 | **Diluc** (`diluc`) | Ngoài trời `M1` | Sân đá trước Dinh thự & Vườn nho Tửu Trang Dawn Winery | `(-4808.0, -3567.0, 24.06)`, `Hdg 135°`, `Area 0` | `0.041m` | Ban ngày Lão gia Diluc trực tiếp giám sát Tửu Trang Ragnvindr ngoài khuôn viên vườn nho (*Hidden Strife*, *Of Ballads and Brews*). Khớp `root` choice: *"How are things at the winery?" -> "The winery is operating as it should. There is always something to oversee..."* |
| 3 | **Klee** (`klee`) | Ngoài trời `M1` | Bãi cỏ bờ Hồ Sao Rơi cạnh Thần Tượng (`Starfell Lake`) | `(-3880.0, -2545.0, 48.71)`, `Hdg 270°`, `Area 0` | `0.000m` | Hễ rời phòng giam là Klee chạy ra thiên nhiên (Hồ Sao Rơi / Rừng Thì Thầm) ôm Dodoco thám hiểm và ngắm cá (*Trifolium Chapter*). Đặt ngoài bờ hồ hợp tính cách hiếu động của Klee hơn hẳn trong phòng kín. |
| 4 | **Fischl & Oz** (`fischl`) | Ngoài trời `M0` | Sân đá cạnh Quầy Hiệp Hội Nhà Mạo Hiểm Katheryne | `(-4188.0, -3046.0, 6.56)`, `Hdg 150°`, `Area 0` *(Oz lơ lửng ngang vai phải)* | `0.005m` | Điều tra viên chính thức của Hiệp Hội Nhà Mạo Hiểm Mondstadt (*Unreconciled Stars*). Khớp `root` choice: *"How is your work with the Adventurers' Guild going?"* Mesh `oz_static.{dff,txd}` đặt lệch `(+0.55m ngang, +1.35m cao)` bù chóp cánh dưới. |
| 5 | **Mona** (`mona`) | Ngoài trời `M0` | Đầu ngõ Khu Dân Cư Nam — trước Nhà Chiêm Tinh phong ấn Thủy | `(-4213.0, -3055.0, 6.65)`, `Hdg 0°`, `Area 0` | `0.000m` | Cuối *Astrolabos Act I*, Mona thuê căn nhà của ông Goth ở khu dân cư phía Nam phố chợ; trong Genshin gốc nhà này không mở cửa trong mà luôn trò chuyện với Mona ngay ngoài thềm. Khớp `city_talk`: *"A little quiet is valuable, and so is having daily necessities within reach."* |
| 6 | **Kaeya** (`kaeya`) | Ngoài trời `M0` | Quảng trường Đài Phun Nước & lối lên Good Hunter | `(-4242.0, -3028.5, 12.60)`, `Hdg 160°`, `Area 0` | `0.000m` | Ban ngày Đội trưởng Kỵ binh thường dạo quanh quảng trường trung tâm & Good Hunter nắm tin tức cư dân (*Pavo Ocellus*, Hangout *Act I*). Vừa đúng chất tình báo phong lưu, vừa không nhốt thêm người trong quán rượu. |
| 7 | **Noelle** (`noelle`) | Ngoài trời `M0` | Sân đá / Bãi tập trước cửa Trụ Sở Đội Kỵ Sĩ Tây Phong | `(-4364.5, -3025.5, 58.10)`, `Hdg 45°`, `Area 0` | `0.000m` | Trong *Hangout Act I & II*, Noelle luôn quét dọn khuôn viên và luyện trọng kiếm ngoài sân tập Trụ sở Kỵ Sĩ. Đứng ngay sân nắng trước cửa `MD_KNI` tạo nhịp dẫn tự nhiên trước khi bước vào gặp Jean & Lisa. |
| 8 | **Barbara** (`barbara`) | Ngoài trời `M0` *(hoặc `INT-03`)* | Tiền sảnh Sân thượng Đại Giáo Đường Tây Phong (`Cathedral Forecourt`) | `(-4444.5, -2937.0, 56.77)`, `Hdg 255°`, `Area 0` | `0.000m` | Đón nắng gió trên đỉnh Đại Cầu Thang trước cửa Giáo Đường, nơi cô tập hát khích lệ cư dân (bên trong `INT-03` vẫn còn Tu nữ Rosaria trực). *(Tuỳ chọn phụ: đặt trong `INT-03` `(-4250.0, -3494.5, 1500.52)` cạnh bàn thờ Đàn Thiên Không nếu muốn tỉ lệ `7 Ngoài : 3 Trong`)*. |
| 9 | **Jean** (`jean`) | Trong nhà `INT-04` | Bàn chỉ huy Văn phòng Quyền Đội Trưởng (`MD_KNI`) | `(-3952.2, -3494.8, 1500.52)`, `Hdg 180°`, `Area 1` | `0.000m` | Hình ảnh đặc trưng nhất của Jean trong mọi nhiệm vụ Mondstadt là giải quyết công văn tại phòng làm việc Đội Trưởng. Khớp `greeting`: *"I have a little time to spare, so please tell me what is on your mind."* |
| 10 | **Lisa** (`lisa`) | Trong nhà `INT-04` | Cánh Đông Kệ sách & Bàn trà Thư viện Đội Kỵ Sĩ (`MD_KNI`) | `(-3946.2, -3496.5, 1500.52)`, `Hdg 210°`, `Area 1` | `0.000m` | Thủ thư coi giữ kho sách và thưởng trà trong nhà; lời chào cứng trong `lisa.json` (*"Come in and settle down; the books can wait a moment"*) đòi hỏi bối cảnh bên trong thư viện. Cách Jean `6.3m` nên vùng tương tác `2.5m` tách biệt hoàn toàn. |

---

## 3. Kiểm toán Chống Trùng lặp Nhân vật (`Zero-Clone Audit`)

Khảo sát thực tế file runtime hiện tại phát hiện **2 nguồn gây phân thân (duplicate NPC)** nếu không xử lý đồng bộ khi triển khai:

1. **Tượng nhân vật gắn cứng trong mesh nội thất `.dff` (`CUSTOM\mondstadt_m1_wilds.img` tạo bởi `patch_interiors_int01_int06.py`)**:
   - Hiện tại 6 phòng `INT-01..06` đang gắn tĩnh 11 nhân vật vào `.dff` căn phòng:
     - `INT-01` Dawn Winery: **Diluc** (`MSR_328746`) -> **Cần gỡ mesh tĩnh** khi đưa Diluc ra sân vườn nho `M1`.
     - `INT-02` Angel's Share: **Venti** (`MSR_328741`), **Kaeya** (`MSR_328743`) -> **Cần gỡ cả 2 mesh tĩnh** khi đưa Venti ra Windrise và Kaeya ra Đài Phun Nước.
     - `INT-03` Favonius Cathedral: **Barbara** (`MSR_328747`), Rosaria (`MSR_514444`) -> **Gỡ mesh tĩnh Barbara** (giữ nguyên **Rosaria** làm NPC trang trí trong Giáo đường!).
     - `INT-04` Knights HQ: **Jean** (`MSR_328744`), **Lisa** (`MSR_328745`) -> **Gỡ 2 mesh tĩnh** để thay bằng 2 `CPed` sống có idle animation, quay mặt về phía Aether và tương tác hội thoại trực tiếp.
     - `INT-05` Cat's Tail: Diona + 6 mèo -> **Giữ nguyên 100%**.
     - `INT-06` Alchemy Lab: Albedo (`MSR_525577`), Sucrose (`MSR_538867`), **Klee** (`MSR_536287`) -> **Chỉ gỡ mesh tĩnh Klee**, giữ nguyên **Albedo & Sucrose** trong phòng thí nghiệm!
2. **Xung đột ID skin ẩn trong `cleo\MondstadtLifeAndBlips.cs` + `COMPONENTPEDS.img`**:
   - Đối chiếu `numbered-skins/catalog.json` & `reviews.json` phát hiện: ở dòng `985` của `build_mondstadt_radar_water_paths_gps_blips_npcs.py`, NPC đứng bán hoa **Flora** tại `(-4207.0, -3048.0, 6.47)` đang dùng `Ped ID 211`, mà `Ped ID 211` trong `COMPONENTPEDS.img` hiện tại lại mang skin **Kaeya (`kaeya__bfed033d655f.dff`)**! Ngoài ra `Ped ID 274` đi dạo ở sân Giáo đường đang mang skin **Hu Tao**.
   - **Giải pháp triệt để khi thi công**:
     - Cấp dải **Custom Ped ID độc lập `49434..49443`** (`mc_venti`, `mc_jean`, `mc_diluc`, `mc_mona`, `mc_kaeya`, `mc_lisa`, `mc_klee`, `mc_barbara`, `mc_noelle`, `mc_fischl`) trong `CUSTOM\custom_mods.img` + `data\peds.ide` (theo đúng chuẩn `49428..49433` của WaifuLink).
     - Đổi model của Flora trong `MondstadtLifeAndBlips.cs` khỏi `211` sang skin thiếu nữ thường dân để trong thành Mondstadt tuyệt đối không có bản sao Kaeya đứng bán hoa.

---

## 4. Kiến trúc 4 Hạng mục Tích hợp Sẵn sàng Thi công (Sau khi Chốt Vị trí)

1. **Map Placement & Proximity Encounter (`cleo/EagleMondstadtChatBridge.cs` + `CUSTOM/custom_mods.img`)**:
   - Stream động các NPC theo bán kính hysteresis (`140m` ngoài trời `Area 0`, hoặc theo `Area 1` cho `INT-04`), kèm prop `oz_static` đi theo Fischl và điểm đánh dấu nhẹ khi lại gần `< 2.6m`.
   - Khi bấm phím tương tác (ví dụ `[E]` / `[Y]` khi đứng gần `< 2.6m`): NPC xoay mặt nhìn thẳng vào Aether (`TASK_TURN_CHAR_TO_FACE_CHAR`), mở khóa vĩnh viễn liên hệ trong Danh bạ điện thoại (`Social Link Unlocked!`) và bật Persona HUD.
2. **Persona-Style Dialogue UI & 6-Expression Bust-up Sprites (`hud.lua` + `MCSP0/MCSP1.TXD`)**:
   - Giao diện vát chéo sắc nét phong cách *Persona 3 Reload / Persona 5 Royal* bằng `Sprite2d.DrawShape` + hộp thoại góc nghiêng, danh sách lựa chọn (`1..4`), phím `[F6]` gõ chat tự do với `gpt-6-luna` (nhờ hook bàn phím chống thoát xe/IME có sẵn trong `EagleCompanion.py`).
   - Kết xuất sẵn bộ **`6` sprite bán thân nền trong suốt (`512×512 BGRA8888`) cho mỗi nhân vật** (`neutral`, `happy`, `serious`, `surprised`, `sad_worried`, `smug_teasing` + trạng thái `oz` phát biểu cho Fischl = `61` sprite) nạp qua 2 slot ping-pong `models/txd/MCSP0.TXD` & `MCSP1.TXD`, tự động đổi biểu cảm theo ngữ cảnh câu trả lời.
3. **Engine & Memory Bridge (`eagle_mondstadt_chat_bridge.py`)**:
   - Tái sử dụng trực tiếp `Engine`, `Store`, `grounding` và SQLite `conversations.sqlite3` của Codex (`tools/eagle-character-chat`, bảo toàn `97/97` unit tests), truyền rõ kênh giao tiếp (`in_person` khi đứng nói chuyện trực tiếp trên map vs `phone_text` khi nhắn tin từ xa qua điện thoại) và thực thi chuẩn quy trình `ack(turn_id)` sau khi hiển thị.
4. **App #14 `Contacts` (`Danh Bạ`) trên EaglePhone (`hud.lua` + `eagle_phone_ui.py`)**:
   - Đặt tại ô trống **Hàng 5 Cột 2** trên lưới `5×3` của EaglePhone (cạnh App #13 `WaifuLink`), gom chung danh bạ liên lạc từ xa cho cả **6 Waifu** (mở sẵn từ đầu, nối sang luồng chat WaifuLink) và **10 NPC Mondstadt** (hiện trạng thái `Chưa gặp / Locked` với gợi ý khu vực trên map cho tới khi gặp trực tiếp lần đầu để mở khóa nhắn tin mọi lúc mọi nơi).
