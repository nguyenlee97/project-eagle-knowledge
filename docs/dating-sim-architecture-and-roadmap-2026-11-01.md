# Kiến Trúc & Lộ Trình Hệ Thống "Eagle Dating Sim" (Game Hẹn Hò AI Trong GTA Project Eagle)

- **Ngày lập thiết kế:** `01/11/2026` (`Asia/Saigon`)
- **Agent thực hiện:** Antigravity (`35d5cf80-28f1-43e1-8e77-f60ee3d570c3`)
- **Trạng thái:** Bản thiết kế kiến trúc, Gameplay & Roadmap (100% không tác động tiến trình `gta_pe.exe` đang chạy).
- **Tài liệu nền tảng:** Kế thừa từ [girlfriend-system-source-survey-2026-11-01.md](girlfriend-system-source-survey-2026-11-01.md).

---

## 1. Tầm Nhìn Tổng Thể: "Build Một Game Dating Sim Hoàn Chỉnh Bên Trong GTA"

Thay vì chắp vá hệ thống bạn gái năm 2004 của GTA San Andreas (vốn bị giới hạn ở 6 slot cố định, thoại băng đảng cũ của CJ, kiểm tra chỉ số Béo/Cơ bắp và dễ làm hỏng skin `AETHER`), mục tiêu mới là **đóng băng hoàn toàn hệ thống bạn gái gốc (`GFAGNT` / `MOB_GF`)** và xây dựng một **Engine Dating Sim độc lập ("WaifuLink / Eagle Dating Sim")** chạy song song với thế giới mở của Project Eagle:

1. **Khớp 100% với dàn nhân vật/skin người chơi đang sử dụng:** Không giới hạn ở 6 slot `190..195`. Hỗ trợ cả nhóm nhân vật đang gắn vào slot Bạn Gái (`Furina`, `Hu Tao`, `Citlali`, `Columbina`, `Kirara`, `Vesna`), nhóm nhân vật tại **Mondstadt (`M0–M2` / `INT-01..07`)** (`Jean`, `Lisa`, `Barbara`, `Noelle`, `Fischl`, `Mona`, `Rosaria`, `Sucrose`) và bất kỳ skin nữ nào được cài từ `Skin Library` (`numbered-skins/deployment/state.json`).
2. **Nhắn tin & Nhận ảnh qua điện thoại (`EaglePhone`):** Một ứng dụng nhắn tin/hẹn hò kiểu *Messenger / Line / Akasha Terminal* ngay trên `EaglePhone`, nơi các cô gái có thể chủ động nhắn tin, trò chuyện AI giữ ngữ cảnh, và **gửi hình ảnh (Selfie đời thường, ảnh chụp tại địa điểm trong game, ảnh trang phục, hoặc Special CG mở khóa theo độ thân mật)** lưu vào Album điện thoại.
3. **Trí nhớ dài hạn (Persistent Memory) & Tiến trình tình cảm nhiều tầng:** Mỗi nhân vật có bộ nhớ SQLite riêng, nhớ được sở thích của Aether, những nơi hai người từng đi qua, món quà từng tặng, bài nhạc từng nghe chung trên xe và lời hứa hẹn gặp.
4. **Hẹn hò thực tế ngoài thế giới mở (In-World Gameplay Loop):** Hẹn lịch qua tin nhắn $\rightarrow$ Đón bằng xe riêng hoặc đặt `EagleRide` (`App #12`) $\rightarrow$ Lái xe nghe `Custom Radio` $\rightarrow$ Đi dạo / vào quán rượu tại **Mondstadt (`M0–M2`)**, **Đảo Nhật Bản (`WIBU-01`)** hoặc nhà hàng San Andreas $\rightarrow$ Trò chuyện trực tiếp qua khung **Visual Novel HUD (`VNDialogue.lua`)** với biểu cảm nhân vật (Sprite/Portrait) và tặng quà/chụp ảnh kỷ niệm.

---

## 2. Gameplay Approach (Thiết Kế Trải Nghiệm Người Chơi)

### 2.1. Vòng Lặp Gameplay Chính (Core Dating Loop)

```
[1. Kết nối & Nhắn tin trên EaglePhone]
   Nhắn tin tự do (AI) • Nhận ảnh Selfie/paparazzi từ ẻm • Chốt lịch & địa điểm hẹn
         │
         ▼
[2. Đón Bạn Gái / Gặp Mặt Ngoài Đời (In-World)]
   Đi xe tới điểm hẹn hoặc gọi EagleRide • NPC spawn đúng skin Genshin + hoạt ảnh vẫy tay/hôn
         │
         ▼
[3. Hoạt Động Hẹn Hò Thế Giới Mở (Open-World Date Activities)]
   • Lái xe dạo phố + nghe Custom Radio (nhân vật bình luận bài hát/tốc độ lái)
   • Đi dạo ngắm cảnh (Mondstadt, Đại lộ Hoa Anh Đào WIBU-01, Bãi biển Santa Maria...)
   • Ăn uống / Uống trà / Nhậu tại Angel's Share, Cat's Tail, Good Hunter, Quán Nhật...
   • Tặng quà & Chụp ảnh chung (Photo Mode lưu vào Album kỷ niệm)
         │
         ▼
[4. Hội Thoại Visual Novel (VN HUD) & Sự Kiện Tình Cảm (Heart Events)]
   Mở giao diện Visual Novel ngay tại bàn ăn/điểm ngắm cảnh • Lựa chọn nhánh + Chat tự do
         │
         ▼
[5. Kết Thúc Buổi Hẹn & Dư Âm (After-Date Memory & Follow-up Photo)]
   Đưa về nhà • Ghi nhận Memory vào SQLite • 15 phút sau ẻm nhắn tin cảm ơn + gửi 1 tấm ảnh kỷ niệm!
```

### 2.2. Hệ Thống Chỉ Số & Cấp Độ Tình Cảm (Relationship Tiers)

Thay cho thanh `0..100%` đơn điệu của GTA SA, mỗi nhân vật có hồ sơ tình cảm riêng:
- **5 Cấp độ quan hệ (Relationship Stage):**
  1. `Lv.1 — Acquaintance (Người quen)`: Mới gặp hoặc mới kết bạn qua điện thoại. Trò chuyện lịch sự, gửi ảnh phong cảnh/đời thường cơ bản.
  2. `Lv.2 — Friend (Bạn thân)`: Bắt đầu chủ động nhắn tin hỏi thăm, rủ đi cà phê/ăn uống, gửi ảnh selfie đời thường.
  3. `Lv.3 — Crush (rung động)`: Mở khóa tương tác nắm tay, tặng hoa (`GUN_FLOWERS`), đi xe riêng ban đêm, lời thoại bắt đầu ngại ngùng/thả thính, gửi ảnh selfie góc cận / outfit mới.
  4. `Lv.4 — Lover (Người yêu)`: Mở khóa tương tác ôm/hôn (`kissing.ifp`), hẹn hò riêng tư tại nhà/khách sạn/Tửu trang, gọi điện/nhắn tin nhớ nhung, gửi ảnh Special CG lãng mạn.
  5. `Lv.5 — Soulmate / Oath (Tri kỷ)`: Mở khóa cốt truyện riêng (Personal Story Quest), phần thưởng đặc quyền cho Aether (buff chỉ số, xe riêng, hoặc gọi hỗ trợ chiến đấu/đi dạo bất cứ lúc nào).
- **Chỉ số cảm xúc động (Dynamic Mood & Trust):**
  - `Affection (0..1000)`: Điểm tình cảm tích lũy qua chat, tặng quà và đi hẹn hò.
  - `Mood (Vui vẻ / Hào hứng / Giận dỗi / Nhớ nhung)`: Thay đổi theo cách Aether trả lời tin nhắn, việc đến đúng giờ hay trễ hẹn, hoặc lái xe tông tường quá nhiều trong buổi hẹn.
  - `Jealousy Toggle (Tùy chọn Harem hoặc Chung thủy)`: Có công tắc trong Settings để người chơi chọn chế độ **Harem Hòa Bình** (không bị trừ điểm khi đi với người khác) hoặc **Drama/Thực Tế** (nếu đi hẹn hò với Hu Tao mà đi ngang qua Furina thì Furina sẽ nhắn tin tra hỏi kèm ảnh bắt quả tang!).

### 2.3. Tính Năng "Chat & Gửi Hình Qua Điện Thoại" (`WaifuGram / EagleChat`)

Đây là trái tim của trải nghiệm "game trong game" trên `EaglePhone`:
- **Tin nhắn chủ động (Proactive Messaging):**
  - Buổi sáng (`07:00–09:00` in-game): Nhân vật nhắn chúc buổi sáng kèm 1 tấm ảnh (ví dụ: Furina gửi ảnh bánh ngọt buổi sáng, Kirara gửi ảnh đang giao hàng, Hu Tao gửi ảnh trêu chọc).
  - Khi thời tiết đổi (Mưa / Hoàng hôn) hoặc Aether bước vào khu vực mới (ví dụ vừa tới Mondstadt): Nhân vật ở khu vực đó nhắn tin *"Em vừa thấy anh ở gần quảng trường Mondstadt phải không?"*.
- **Hệ thống Gửi Ảnh (Photo & CG Pack System):**
  - Mỗi nhân vật có một thư mục **Media Pack (`media/<char_id>/`)** được phân loại theo thẻ ngữ cảnh (`tags`):
    - `selfie_casual`: Ảnh selfie đời thường (phòng ngủ, quán trà, đi dạo).
    - `location_spot`: Ảnh gắn với địa danh (Mondstadt, biển, phố đêm Nhật Bản).
    - `mood_reaction`: Ảnh biểu cảm (vui, dỗi, ngại đỏ mặt, meme Genshin).
    - `special_cg_lv3 / lv4 / lv5`: Ảnh nghệ thuật / quyến rũ mở khóa khi đạt mốc tình cảm cao.
  - **Cơ chế AI chọn ảnh thông minh:** Khi LLM sinh câu trả lời trong JSON envelope, ngoài `reply_text` và `mood`, model có thể đính kèm `"attachment_tag": "selfie_casual"` hoặc người chơi có thể nhắn *"Gửi cho anh xem hình em đang làm gì đi"* $\rightarrow$ Engine tự chọn bức ảnh phù hợp nhất (ưu tiên ảnh chưa gửi) và hiển thị ngay trong khung chat `EaglePhone` + lưu vào ứng dụng **Gallery (Bộ sưu tập ảnh)**.
  - **Hỗ trợ cả HUD trong game & Web UI:**
    - Trên màn hình `EaglePhone` (cả bản Web/Tablet và bản in-game overlay): Hiển thị bong bóng chat có hình ảnh thu nhỏ, bấm vào phóng to Full HD.

---

## 3. Technical Approach (Giải Pháp Kỹ Thuật & Chống Xung Đột)

### 3.1. Chiến Lược "Tắt Sạch Không Đụng Bytecode" Đối Với Hệ Thống Bạn Gái Gốc (`main.scm`)

Một trong những rủi ro lớn nhất khi sửa `main.scm` là làm lệch offset khiến save game hoặc các thread khác (`CELLFON`, `STARTGM`) bị crash. Thay vì sửa file `main.scm`, ta dùng **Chiến lược Đóng Băng Runtime (Runtime Hibernation Bridge)** qua `EagleCompanion.py` hoặc 1 script CLEO5 nhỏ (`EagleDatingCore.cs`):

| Thành phần gốc GTA SA | Cách xử lý chống xung đột | Cơ chế kỹ thuật cụ thể |
| :--- | :--- | :--- |
| **Thread `GFAGNT` & `MOB_GF`** (`main.scm` @ `0x02375E`, `0x02D014`) | **Đóng băng sạch (Hibernate)** | Xóa bitmask `$406` (`$(1624) = 0`) trong RAM hoặc dừng script thread `gfagnt` / `mob_gf` bằng CLEO (`0459: TERMINATE_ALL_SCRIPTS_WITH_THIS_NAME 'gfagnt'`). Khi `gfagnt` dừng: không còn blip tim cũ xung đột, không có cuộc gọi đòi hẹn hò của Denise/Millie cũ, và không bao giờ kích hoạt `gf_meeting.scm` / `gf_date.scm`. |
| **Audio thoại GTA SA 2004 (`SPC_GA`)** | **Tắt hoàn toàn trong buổi hẹn** | Vì không gọi `gf_date.scm`, game sẽ không bao giờ phát giọng tiếng Anh đường phố của Denise/Millie khi đang đi với Citlali/Columbina. Có thể thay bằng giọng TTS/Voice sample Genshin của nhân vật. |
| **Cờ kiểm duyệt Hot Coffee (`$(4876)` @ `0x00A4AC6C`) & Model `*GRL2`** | **Đã tắt sẵn mặc định (`$(4876) = 1`) + Khóa cứng khi qua hệ thống mới** | Mặc định `GFINIT` (`0x023750`) gán `$(4876) = 1` (Censored ON), không có mod Hot Coffee nào bật `$(4876) = 0`. Nếu `$(4876) = 0`, `gf_sex.scm` (`0x1D8D`) sẽ gọi `023C: LOAD_SPECIAL_CHARACTER` nạp `GANGRL2..CROGRL2` (vẫn là model gốc GTA SA `~100 KB` trong `COMPONENTPEDS.img`), làm nhân vật nữ Genshin bị biến thành model 2004. Giữ `$(4876) = 1` và tắt `gfagnt` sẽ chặn 100% nguy cơ này. |
| **Nhân vật chính (Player = CJ)** | **Giữ nguyên CJ gốc (Đã bỏ hướng thay CJ = Aether)** | Người chơi giữ nguyên CJ gốc nên toàn bộ hệ thống quần áo, chỉ số và hoạt ảnh của CJ hoạt động bình thường, không cần lo lỗi `070D: BUILD_PLAYER_MODEL`. |
| **Xung đột Ped Slot (`190..195` và skin khác)** | **Quản lý Spawn Động (Dynamic Companion Spawner)** | Hệ thống mới tự động đọc `state.json` của `Skin Library` và danh sách ped trong `peds.ide` / `Mondstadt` để biết chính xác Model ID nào đang mang skin của nhân vật nào. Khi bắt đầu buổi hẹn, CLEO script `EagleDatingActor.cs` mới nạp (`0247: REQUEST_MODEL`) đúng Model ID đó, tạo Actor đi cùng Aether và giải phóng ngay khi kết thúc buổi hẹn. |

### 3.2. Kiến Trúc 4 Tầng (4-Layer Architecture)

```
┌────────────────────────────────────────────────────────────────────────────┐
│ TẦNG 1: GIAO DIỆN NGƯỜI CHƠI (UI LAYER)                                    │
│  • EaglePhone App "WaifuLink" (Chat, Danh bạ, Lịch hẹn, Gửi/Xem Ảnh, CG)   │
│  • In-Game VN HUD (VNDialogue.lua: Khung thoại Visual Novel + Portrait)    │
│  • In-Game Notification Banner (Tin nhắn/Ảnh mới báo góc màn hình)         │
└───────────────────────────────────┬────────────────────────────────────────┘
                                    │ HTTP / JSON Bridge
┌───────────────────────────────────▼────────────────────────────────────────┐
│ TẦNG 2: BỘ NÃO AI, TRÍ NHỚ & MEDIA ENGINE (PYTHON SIDECAR)                 │
│  • Nâng cấp từ `tools/eagle-character-chat` + `EagleCompanion.py`          │
│  • Character Registry: Tự động đồng bộ với Skin đang cài (`state.json`)    │
│  • SQLite Memory v3: Lưu lịch sử chat, kỷ niệm buổi hẹn, điểm Affection    │
│  • Photo/CG Selector: Chọn ảnh theo tag ngữ cảnh & cấp độ tình cảm         │
│  • Game Context Sensor: Đọc vị trí Aether, thời tiết, giờ, bài nhạc Radio  │
└───────────────────────────────────┬────────────────────────────────────────┘
                                    │ RAM Mailbox (`0xCAFE00`) & JSON IPC
┌───────────────────────────────────▼────────────────────────────────────────┐
│ TẦNG 3: ĐIỀU KHIỂN THẾ GIỚI MỞ & BUỔI HẸN (CLEO5 / LUA RUNTIME)            │
│  • `EagleDatingHibernator.cs`: Tắt `gfagnt`/`mob_gf` gốc an toàn           │
│  • `EagleDateDirector.cs`: Spawn bạn gái, đi theo Aether, lên xe, vào quán │
│  • Hoạt ảnh lãng mạn: Gọi `kissing.ifp`, `flowers.ifp`, `dancing.ifp`      │
│  • Tích hợp `EagleRide` (đặt xe đón cả hai) & `Custom Radio`               │
└───────────────────────────────────┬────────────────────────────────────────┘
                                    │
┌───────────────────────────────────▼────────────────────────────────────────┐
│ TẦNG 4: DỮ LIỆU THẾ GIỚI & BẢN ĐỒ (WORLD & MAP POIs)                       │
│  • Điểm hẹn tại Mondstadt (`M0–M2`, `INT-01..07`), Đảo Nhật (`WIBU-01`)    │
│  • 116 Nhà hàng/Quán Bar/Café & 79 Điểm ngắm cảnh từ `eagle_gg_map_pois.py`│
└────────────────────────────────────────────────────────────────────────────┘
```

### 3.3. Cơ Chế Đồng Bộ Nhân Vật Với Skin Đang Dùng (`Skin-to-Character Sync`)

Để hệ thống luôn khớp với những nhân vật bạn đang cài làm skin:
1. **File cấu hình trung tâm `data/project-eagle/dating-sim/roster.json`:**
   - Tự động đọc [state.json](file:///D:/GTA%20Archive/Skin%20Library/Project%20Eagle/numbered-skins/deployment/state.json) (ví dụ biết ngay slot `195` là **Citlali**, `194` là **Columbina**, `193` là **Furina**, `192` là **Hu Tao**, `191` là **Kirara**, `190` là **Vesna**) cộng với dàn nhân vật Mondstadt (`Jean`, `Lisa`, `Barbara`, `Noelle`, `Fischl`, `Mona`, `Rosaria`, `Sucrose`).
   - Khi bạn đổi skin mới qua **Skin Viewer** (ví dụ cài thêm *Raiden Shogun* hay *Navia* vào một slot ped), bạn chỉ cần bấm 1 nút **"Sync Active Skins"** (hoặc hệ thống tự phát hiện hash `state.json` thay đổi) để kích hoạt hồ sơ nhân vật đó trong danh bạ hẹn hò!
2. **Cấu trúc Hồ sơ 1 Nhân vật (Character Dating Pack):**
   - `profile.json`: Tên, danh hiệu, tính cách, cách xưng hô với Aether (ví dụ: *Anh/Em*, *Nhà Lữ Hành/Tôi*), khung giờ hay thức, địa điểm yêu thích (ví dụ: Lisa thích thư viện/quán trà, Hu Tao thích đi dạo ban đêm, Furina thích nhà hàng sang trọng/xem nhạc kịch), món quà yêu thích.
   - `cognition.json`: Kiến thức cốt truyện Genshin và mối quan hệ (kế thừa từ `tools/eagle-character-chat/content/cognition/`).
   - `photos/`: Bộ ảnh selfie, ảnh đời thường và ảnh CG theo từng mốc tình cảm (`Lv.1..Lv.5`).
   - `portraits/`: Bộ ảnh bán thân (2D Sprite với các biểu cảm: *Bình thường, Cười, Ngại đỏ mặt, Giận dỗi, Ngạc nhiên*) để hiện lên khung **Visual Novel HUD** khi nói chuyện trực tiếp.

---

## 4. Roadmap Triển Khai Theo Từng Giai Đoạn (Làm Dần, Chắc Chắn, Không Phá Game)

Lộ trình được chia thành **5 Phase từ nền tảng đến nâng cao** để mỗi Phase đều có sản phẩm chơi thử được ngay và không ảnh hưởng tới phần bạn đang test:

### Phase 0: Cô Lập Hệ Thống Cũ & Chuẩn Bị Khung Dữ Liệu (Safe Foundation)
- **Mục tiêu:** Chấm dứt hoàn toàn sự can thiệp của hệ thống bạn gái GTA SA 2004 mà không chạm vào `main.scm`, đồng thời tạo cấu trúc dữ liệu cho dàn nhân vật Genshin hiện tại.
- **Công việc:**
  1. Viết mô-đun tắt sạch thread `gfagnt` và `mob_gf` khi vào game + khóa bảo vệ model `AETHER` khỏi lệnh `070D: BUILD_PLAYER_MODEL`.
  2. Xây dựng `roster.json` đồng bộ tự động với 6 skin ở slot `190..195` (`Citlali`, `Columbina`, `Furina`, `Hu Tao`, `Kirara`, `Vesna`) và dàn nữ `Mondstadt` (`Jean`, `Lisa`, `Barbara`, `Noelle`, `Fischl`, `Mona`).
  3. Mở rộng schema SQLite của `eagle-character-chat` thêm bảng `dating_state` (`affection`, `stage`, `mood`, `unlocked_photos`, `scheduled_date`) và `episodic_memories` (nhật ký các buổi hẹn).

### Phase 1: Ứng Dụng "WaifuLink" Trên `EaglePhone` — Chat AI, Memory & Gửi Ảnh (Phone Dating Sim)
- **Mục tiêu:** Biến `EaglePhone` thành một chiếc điện thoại Dating Sim thực thụ — chưa cần spawn NPC phức tạp ngoài đường cũng đã có thể nhắn tin, xây dựng tình cảm và nhận ảnh từ các ẻm.
- **Công việc:**
  1. Thêm App mới **"WaifuLink (Hẹn Hò & Tin Nhắn)"** lên màn hình chính `EaglePhone` (gồm 4 tab: *Tin nhắn*, *Danh bạ & Hồ sơ tình cảm*, *Album Ảnh/CG*, *Lịch Hẹn*).
  2. Kết nối trực tiếp với engine LLM (`gpt-6-luna`) + hệ thống Memory: nhân vật nhớ mọi chi tiết người chơi kể và phản hồi đúng tính cách (hỗ trợ tiếng Việt tự nhiên hoặc tiếng Anh tùy chọn).
  3. **Xây dựng tính năng Gửi Hình & Album Ảnh:**
     - Tạo kho ảnh mẫu phân loại theo ngữ cảnh (`morning`, `selfie`, `outfit`, `food`, `night`, `flirt`, `cg_reward`) cho từng nhân vật.
     - Cho phép nhân vật gửi ảnh ngay trong luồng chat (khi đạt điều kiện tình cảm, khi chủ động nhắn tin sáng/tối, hoặc khi Aether nhắn xin ảnh).
     - Hiển thị thông báo (Toast Banner) trong game khi có tin nhắn/ảnh mới từ bạn gái.

### Phase 2: Đón Bạn Gái Ngoài Đời & Hẹn Hò Thế Giới Mở Cơ Bản (In-World Date Director)
- **Mục tiêu:** Chuyển từ "nhắn tin qua điện thoại" sang "gặp mặt trực tiếp trong thế giới GTA".
- **Công việc:**
  1. **Chốt kèo hẹn trong khung chat:** Khi Aether nhắn *"Tối nay đi chơi nhé"* hoặc bấm nút **"Rủ Đi Hẹn Hò"** trên App, nhân vật sẽ đồng ý và ghim điểm hẹn lên `GG Map` (hoặc đứng chờ ở nhà/Mondstadt).
  2. **Script điều phối buổi hẹn (`EagleDateDirector.cs`):**
     - Spawn đúng Model ID của nhân vật tại điểm hẹn với hoạt ảnh đứng chờ/vẫy tay.
     - Khi Aether tới gần: Tự động vào chế độ đồng hành (đi bộ cạnh nhau, tự lên ghế phụ xe Aether hoặc cùng lên xe công nghệ `EagleRide`).
     - Hỗ trợ các tương tác lãng mạn trực tiếp bằng phím tắt / Quick Menu: **Tặng hoa (`flowers.ifp`), Nắm tay đi dạo, Ôm/Hôn (`kissing.ifp`), Khiêu vũ (`dancing.ifp`)**.

### Phase 3: Giao Diện Visual Novel Trong Buổi Hẹn & Điểm Hẹn Trên Map Mới (VN HUD + Map Integration)
- **Mục tiêu:** Đưa trải nghiệm hẹn hò tại **Mondstadt (`M0–M2`)**, **Đảo Nhật Bản (`WIBU-01`)** và các nhà hàng/bãi biển lên chuẩn một game Visual Novel.
- **Công việc:**
  1. **Điểm hẹn chuyên biệt (Dating Hotspots) trên Map mới:**
     - Định nghĩa các bàn ngồi/điểm ngắm cảnh tại *Quán rượu Angel's Share (`INT-02`)*, *Quán trà Cat's Tail (`INT-07`)*, *Tửu trang Dawn Winery (`INT-06`)*, *Đại lộ Hoa Anh Đào (`WIBU-01`)* và các nhà hàng mở sẵn qua `EHI.ini`.
  2. **Chế độ "Table Talk / Scenic Date" với Visual Novel HUD:**
     - Khi tới điểm hẹn, camera chuyển sang góc điện ảnh hướng về phía bạn gái đang ngồi đối diện hoặc đứng tựa lan can ngắm cảnh.
     - Bật khung thoại **VN HUD** kèm **Ảnh chân dung biểu cảm (Character Sprite: Cười / Đỏ mặt / Ngạc nhiên)**, 3 lựa chọn trả lời nhanh + ô gõ chat tự do.
  3. **Cảm biến ngữ cảnh thời gian thực (Live Game Context):**
     - AI biết rõ hai người đang ngồi ở đâu, trời đang mưa hay hoàng hôn, Aether vừa lái xe êm ái hay phóng bạt mạng, và đang bật bài nhạc gì trên **Custom Radio** để đưa vào câu chuyện.
     - Cuối buổi hẹn, toàn bộ buổi đi chơi được tóm tắt thành 1 dòng **Ký ức buổi hẹn (Date Memory)** lưu vào SQLite, và 10 phút sau khi về nhà cô gái sẽ nhắn tin kèm 1 bức ảnh selfie kỷ niệm buổi đi chơi!

### Phase 4: Paimon Wingman, Sự Kiện Tình Cảm (Heart Events) & Chế Độ Chụp Ảnh Chung
- **Mục tiêu:** Hoàn thiện chiều sâu "Game trong Game" và kết nối tất cả các hệ thống lại với nhau.
- **Công việc:**
  1. **Paimon Agent làm "Quân sư tình cảm" (Wingman):** Paimon có thể bật mí hôm nay nhân vật nào đang có tâm trạng tốt, gợi ý món quà/địa điểm hợp gu từng cô gái, hoặc giúp Aether đặt trước bàn ăn và gọi xe `EagleRide`.
  2. **Cốt truyện riêng theo cấp độ (Heart Events Lv.1 $\rightarrow$ Lv.5):** Mỗi khi thăng cấp quan hệ (`Friend` $\rightarrow$ `Crush` $\rightarrow$ `Lover`), kích hoạt một kịch bản hẹn hò đặc biệt có cốt truyện riêng của nhân vật đó.
  3. **In-Game Date Photo Mode:** Cho phép Aether và bạn gái tạo dáng chụp ảnh chung tại các danh lam thắng cảnh trong game và lưu thẳng vào Album kỷ niệm trên `EaglePhone`.
