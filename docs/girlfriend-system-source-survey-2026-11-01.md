# Báo Cáo Khảo Sát Source: Hệ Thống Bạn Gái (Girlfriend / Dating System) & Khả Năng Tích Hợp AI / Map Mới Trên Project Eagle

- **Ngày khảo sát:** `01/11/2026` (`Asia/Saigon`)
- **Agent thực hiện:** Antigravity (`35d5cf80-28f1-43e1-8e77-f60ee3d570c3`)
- **Phạm vi:** Chỉ đọc (`Read-Only`) 100% trên đĩa cứng (`0` tác động tới tiến trình `gta_pe.exe` đang chạy, `0` ghi file runtime, không chiếm khóa `game-write.lock`).
- **Đích khảo sát:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`, `D:\GTA Archive\Skin Library`, `tools/eagle-character-chat`, `tools/eagle-dialogue`, và `staging/project-eagle/npc-dialogue-integration-research-20261022`.

---

## 1. Kết Luận Tóm Tắt

**Game gốc `Project Eagle (gta sa gameplay-lab)` CÓ hỗ trợ đầy đủ 100% hệ thống Bạn Gái (Girlfriend / Dating System) ngay trong source bytecode và tài nguyên thực tế.**

Không những giữ nguyên toàn bộ các luồng điều khiển hẹn hò của GTA San Andreas (`GFINIT`, `GFAGNT`, `MOB_GF`, `CELLFON`, `gf_meeting.scm`, `gf_date.scm`, `gf_sex.scm`), đội ngũ phát triển Project Eagle còn **chủ động vá script khởi tạo Freeroam (`STARTGM` và `MAIN`)** để mở khóa sẵn **Denise** và **Millie** ngay từ khi bắt đầu New Game (vì bản Freeroam đã lược bỏ nhiệm vụ cốt truyện), đồng thời mở sẵn cổng điều kiện cốt truyện cho **Helena**. Đặc biệt, trên bản `gameplay-lab` hiện tại, cả **6 slot Bạn Gái (`Ped IDs 190..195`) đã được cài sẵn 6 skin nhân vật nữ Genshin Impact** (`Vesna`, `Kirara`, `Hu Tao`, `Furina`, `Columbina`, `Citlali`).

---

## 2. Bằng Chứng Khảo Sát Chi Tiết Từng Tầng Trong `gta sa gameplay-lab`

### 2.1. Tầng Kịch Bản Bytecode (`data\script\main.scm` & `data\script\script.img`)

Đã giải mã trực tiếp `data\script\main.scm` (`4,849,743 bytes`, `187` luồng `03A4`) và `data\script\script.img` (`749,568 bytes`, `89` script ngoại vi):

| Thành phần | Vị trí / Kích thước | Trạng thái trong `gameplay-lab` | Chi tiết kỹ thuật & Offset thực tế |
| :--- | :--- | :--- | :--- |
| **Khởi chạy từ `MAIN`** | `main.scm` @ `0x013869` (`79977`) | **Đang BẬT (Active)** | Gọi `00D7: LAUNCH_MISSION 143985` (`GFINIT`), kèm `166294` (`CELLFON`) tại `0x01388C` và `187953` (`STARTGM`) tại `0x013893`. |
| **Thread `GFINIT`** | `main.scm` @ `0x023271` (`143985..145246`) | **Đang BẬT (Active)** | Khởi tạo toàn bộ cấu trúc dữ liệu của 6 bạn gái: điểm tình cảm ban đầu (`$359..$364` / `1436..1456`), bitmask sở thích lái xe/khu vực (`$377..$382` / `1508..1528`), khung giờ có mặt ở nhà (`$383..$388` / `1532..1552`), tạo 7 object cửa/tủ đồ tại nhà 6 bạn gái (`-51..-56`), gán cờ censor cà phê `$(4876) = 1` và khởi chạy `004F: START_NEW_SCRIPT 145246` (`GFAGNT`). |
| **Thread `GFAGNT`** | `main.scm` @ `0x02375E` (`145246..159050`) | **Đang BẬT (Active)** | Vòng lặp ngầm quản lý toàn bộ trạng thái 6 bạn gái: kiểm tra thành phố hiện tại của người chơi (`0842: GET_CITY_PLAYER_IS_IN`), bật/tắt blip trái tim (`Sprite 21`), kiểm tra khung giờ rảnh, nạp model `190..195` (`0247: REQUEST_MODEL`), kích hoạt quà thưởng (xe riêng tại `50%`, trang phục & đặc quyền tại `100%`), và gọi `gf_meeting.scm` / `gf_date.scm`. |
| **Bản vá Freeroam trong `STARTGM` & `MAIN`** | `main.scm` @ `0x02DE58`, `0x02DE5F`, `0x013073` | **Đã vá sẵn cho Eagle** | - `0x02DE58`: `08BA: SET_GLOBAL_VAR_BIT_CONST $(1624), 0` $\rightarrow$ Mở khóa sẵn **Denise (`GF #0`)** ngay khi vào game.<br>- `0x02DE5F`: `08BA: SET_GLOBAL_VAR_BIT_CONST $(1624), 5` $\rightarrow$ Mở khóa sẵn **Millie (`GF #5`)** ngay khi vào game.<br>- `0x013073`: `0004: SET_VAR_INT $(1832), 2` $\rightarrow$ Mở khóa cổng điều kiện cốt truyện (`2 <= $(1832)` tại `0x023C32`) để gặp **Helena (`GF #2`)**. |
| **Thread `MOB_GF` & `CELLFON`** | `main.scm` @ `0x02D014` (`184340`) & `0x028996` (`166294`) | **Đang BẬT (Active)** | Quản lý các cuộc gọi điện thoại từ bạn gái khi người chơi lâu không đến thăm (`mode = 1`) hoặc khi bị bắt gặp đi với cô gái khác (`mode = 2`, trừ điểm tình cảm). |
| **`gf_meeting.scm` (Script `24`)** | `script.img` (`8,192 B`, `GFMEET`) | **Có đủ & được `GFAGNT` gọi** | Kịch bản làm quen lần đầu cho 4 bạn gái ngoài thế giới: **Michelle** (`192`), **Helena** (`191`), **Barbara** (`190`), **Katie** (`193`). Kiểm tra chỉ số `Sex Appeal` (`Stat 25`), `Fat` (`Stat 21`), `Muscle` (`Stat 23`) và khởi tạo `Stat 252..257`. |
| **`gf_date.scm` (Script `25`)** | `script.img` (`34,816 B`, `GFDATE`) | **Có đủ & được `GFAGNT` gọi** | Kịch bản hẹn hò chính: Đi ăn (`FDREST1`, `REST2`, `DINER1`, `DINER2`, `TSDINER`), Đi uống (`BAR1`, `BAR2`, `UFOBAR`), Đi nhảy Club (`dance.scm` `18,432 B`), Đi dạo bằng xe (`Driving Date`), Hôn (`KISSING`), Tặng quà (`GIFT_GIVE`/`GIFT_GET`), và mời vào nhà uống cà phê cuối buổi hẹn. |
| **`gf_sex.scm` (Script `26`)** | `script.img` (`14,336 B`, `GFSEX`) | **Có đủ & được `gf_date` gọi** | Kịch bản "Uống cà phê" cuối buổi hẹn (mặc định ở chế độ Censored `$(4876) = 1` quay camera bên ngoài nhà). |

---

### 2.2. Danh Sách 6 Bạn Gái, Tọa Độ, Khung Giờ & Skin Genshin Đang Cài Trong `gameplay-lab`

Đối chiếu giữa `main.scm` (`GFINIT`/`GFAGNT`), `data\peds.ide` (dòng `228..233`), `D:\GTA Archive\Skin Library\Project Eagle\numbered-skins\deployment\state.json`, `catalog.json` và `S&S\Cdimages\default\COMPONENTPEDS.img`:

| GF Index | Tên gốc (`peds.ide` Voice) | Ped ID & Model | Skin Genshin đang cài (`COMPONENTPEDS.img`) | Trạng thái mở khóa đầu game | Tọa độ gặp lần đầu (`gf_meeting.scm`) | Tọa độ nhà hẹn hò (`GFAGNT` Blip Tim) | Khung giờ rảnh (`$383..$388`) | Đặc quyền & Xe thưởng (`50%` / `100%`) |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`0`** | **Denise Robinson** (`VOICE_GFD_DENISE`) | `195` (`GANGRL3`) | **Citlali** (`Skin #1423`, `2.55 MB` DFF / `50.33 MB` TXD) | **Đã mở sẵn** (`Bit 0` của `$(1624)`) | *(Không cần — mở sẵn từ đầu)* | `(2401.96, -1723.22, 12.60)` — Ganton, Los Santos (`City 1`) | `16:00 – 06:00` | Xe **Green Hustler** (`50%`), Trang phục Pimp (`100%`) |
| **`1`** | **Michelle Cannes** (`VOICE_GFD_MICHELLE`) | `192` (`MECGRL3`) | **Hu Tao (`HuTao CSL2`)** (`Skin #687`, `1.71 MB` DFF / `16.08 MB` TXD) | Gặp tại Trường lái xe SF (`Bit 1`) | `(-2027.58, -118.70, 1034.00)` — Nội thất Driving School, Doherty SF | `(-1799.50, 1195.50, 24.11)` — Downtown, San Fierro (`City 2`) | `00:00 – 12:00` | Sơn sửa xe miễn phí tại garage `MICHDR`, Xe **Monster** (`50%`), Đồ Racing (`100%`) |
| **`2`** | **Helena Wankstein** (`VOICE_GFD_HELENA`) | `191` (`GUNGRL3`) | **Kirara (`A74 Kirara`)** (`Skin #1726`, `1.63 MB` DFF / `4.68 MB` TXD) | Gặp tại Blueberry (`$(1832)=2` đã mở sẵn) | `(257.67, -154.75, 4.08)` — Ban công tập bắn Ammu-Nation Blueberry | `(-377.40, -1438.69, 24.72)` — Trang trại Flint Range (`City 0`) | `08:00 – 12:00` & `14:00 – 02:00` | Kho vũ khí trong nhà kho (`Pistol, Chainsaw, Molotov, Flamethrower`), Xe **Bandito** (`50%`), Đồ Rural (`100%`) |
| **`3`** | **Barbara Schternvart** (`VOICE_GFD_BARBARA`) | `190` (`COPGRL3`) | **Vesna** (`Skin #54`, `4.33 MB` DFF / `29.71 MB` TXD) | Gặp tại El Quebrados (`Bit 3`) | `(-1410.10, 2648.73, 54.69)` — Bãi đỗ xe Đồn Cảnh sát El Quebrados | `(-1398.10, 2636.87, 54.70)` — El Quebrados, Tierra Robada (`City 0`) | `16:00 – 06:00` | Bị bắt không mất vũ khí/tiền (`SWITCH_ARREST_PENALTIES 0`), Xe **Ranger** (`50%`), Đồ Cop (`100%`) |
| **`4`** | **Katie Zhan** (`VOICE_GFD_KATIE`) | `193` (`NURGRL3`) | **Furina (`A74 Furina`)** (`Skin #322`, `1.83 MB` DFF / `2.84 MB` TXD) | Gặp tại Sân golf Avispa SF (`Bit 4`) | `(-2291.71, -233.02, 41.72)` — Bụi cây sườn đồi Avispa Country Club SF | `(-2576.81, 1144.74, 54.74)` — Juniper Hollow, San Fierro (`City 2`) | `12:00 – 00:00` | Nhập viện không mất vũ khí/tiền (`SWITCH_DEATH_PENALTIES 0`), Xe **White Romero** (`50%`), Đồ Medic (`100%`) |
| **`5`** | **Millie Perkins** (`VOICE_GFD_MILLIE`) | `194` (`CROGRL3`) | **Columbina** (`Skin #3380`, `4.43 MB` DFF / `3.67 MB` TXD) | **Đã mở sẵn** (`Bit 5` của `$(1624)`) | *(Không cần — mở sẵn từ đầu)* | `(2035.36, 2732.41, 9.82)` — Prickle Pine, Las Venturas (`City 3`) | `12:00 – 22:00` | Xe **Pink Club** (`50%`), Đồ Gimp (`100%`) |

> **Lưu ý về file archive:** Cả 6 cặp `.dff`/`.txd` (`copgrl3..gangrl3`) chỉ nằm trong `S&S\Cdimages\default\COMPONENTPEDS.img`, không nằm trong danh sách 11 file trùng với `CUSTOM\GROUP_A_MODS.IMG`. Riêng các model phụ `copgrl1..gangrl1` và `copgrl2..gangrl2` (chỉ được nạp qua `023C: LOAD_SPECIAL_CHARACTER` nếu bật mã debug `UNCENSORED` trong `gf_sex.scm`) vẫn đang giữ model gốc GTA SA (`~100 KB`).

---

### 2.3. Tầng Hoạt Ảnh (`.ifp`), Vật Phẩm Quà Tặng, Nội Thất Hẹn Hò (`ENEX`) & Âm Thanh

1. **Hoạt ảnh (`.ifp` trong `anim\anim.img`)**:
   - Có đủ **8/8** bộ animation phục vụ hẹn hò:
     - `kissing.ifp` (`176,128 B`): `PLAYA_KISS_01..03`, `GRLFRD_KISS_01..03`, `GIFT_GIVE`, `GIFT_GET`, `GF_StreetArgue_02`.
     - `dancing.ifp` (`122,880 B`): Hoạt ảnh nhảy đôi trong Club.
     - `park.ifp` (`22,528 B`): Hoạt ảnh múa Thái Cực Quyền (`TAI_CHI_IN/LOOP/OUT`) của Katie/Furina lúc gặp lần đầu.
     - `flowers.ifp` (`8,192 B`) & `dildo.ifp` (`65,536 B`): Hoạt ảnh cầm và tặng bó hoa / quà.
     - `blowjobz.ifp` (`163,840 B`), `sex.ifp` (`253,952 B`), `snm.ifp` (`204,800 B`).
2. **Vật phẩm quà tặng (`data\default.ide`) & Script sự kiện đường phố (`cleo\`)**:
   - Đầy đủ ID vũ khí/quà tặng: `325` (`GUN_FLOWERS` — Bó hoa tươi), `321..324` (`GUN_DILDO1/2`, `GUN_VIBE1/2`), `326` (`GUN_CANE`).
   - Trong `cleo\`, gói Nhóm A đã có sẵn 2 script sự kiện môi trường liên quan:
     - `cleo\Date Kiss.qa` (`KISSPKQ` — `14,976 B`): Tạo các cặp đôi NPC đứng trò chuyện, tặng quà và hôn nhau trên phố bằng `KISSING`.
     - `cleo\Flowers Seller.qa` (`FLOWRQA` — `11,897 B`): Tạo NPC bán hoa dạo ngoài phố.
3. **Nội thất nhà hàng, quán bar, vũ trường & phòng bạn gái (`ENEX` / `.IPL`)**:
   - Quét toàn bộ `.IPL` ghi nhận **126 điểm `ENEX`** thuộc hệ thống hẹn hò (`FDREST1`, `REST2`, `DINER1`, `DINER2`, `TSDINER`, `BAR1`, `BAR2`, `UFOBAR`, `LASTRIP`, `STRIP2`).
   - Đặc biệt, bản mod **Extended Hidden Interiors (`custom\EHI.IPL` + `cleo\EHI.ini` + `cleo\DatingInteriors.s`)** đang cài trong `gameplay-lab` đã bật cấu hình `[RESTAURANTS]` (`Diner1 = 1`, `Diner2 = 1`, `SecretValley = 1`, `WorldOfCoq = 1`, `WelcomePump = 1`), giúp các nhà hàng hẹn hò vốn bị khóa ngoài giờ hẹn nay có thể bước vào tự do mọi lúc.
4. **Chỉ số (`data\statdisp.dat`) & Âm thanh (`audio\SFX\SPC_GA`)**:
   - Các chỉ số `Stat 252..257` (tiến độ tình cảm 6 bạn gái), `Stat 65`, `Stat 184` (số bạn gái đang hẹn hò), `Stat 186`, `Stat 189` đều hoạt động nguyên vẹn.
   - Ngân hàng âm thanh `audio\SFX\SPC_GA` (`1,103,880,528 B` — `1.10 GB`) và `audio\SFX\SCRIPT` (`319.68 MB`) còn nguyên vẹn.

---

## 3. Khảo Sát Các Hệ Thống Phụ Trợ Hiện Có Trong Workspace (Chatbot, Paimon, EaglePhone, Map Mới)

Ngoài cơ chế hẹn hò gốc của GTA SA, workspace hiện đã có sẵn 4 nền tảng hiện đại có thể kết nối trực tiếp để nâng cấp tính năng Bạn Gái:

| Hệ thống trong Workspace | File nguồn chính | Hiện trạng hỗ trợ | Tiềm năng kết nối với tính năng Bạn Gái |
| :--- | :--- | :--- | :--- |
| **1. Character Chat Studio v0.3.3** | `tools/eagle-character-chat/` (`engine.py`, `memory.py`, `store.py`, `content/cognition/*.json`) | Đã có **10 nhân vật Genshin** (`Venti`, `Jean`, `Diluc`, `Mona`, `Kaeya`, `Lisa`, `Klee`, `Barbara`, `Noelle`, `Fischl–Oz`), dùng model `gpt-6-luna`, có hồ sơ nhận thức (`cognition`), quan hệ (`relationships`), lịch sử chung với Aether (`shared_history`) và bộ nhớ SQLite bền vững. | Hiện mới chạy trên Web Studio (`http://127.0.0.1:8952`), chưa nối vào in-game NPC hay thanh tiến độ bạn gái. Có thể dùng làm **bộ não hội thoại & ký ức hẹn hò** cho dàn nhân vật nữ Genshin. |
| **2. Paimon Agent & VN HUD (`eagle-dialogue`)** | `tools/eagle-dialogue/` (`bridge/paimon.py`, `hud/paimon_hud.lua`, `runtime/eagle_dialogue/phone_tools.py`, `cleo/EaglePaimonBridge.cs`, `cleo/EagleDialogueBridge.cs`) | Đã cài vào `gameplay-lab` (App 11 trên EaglePhone + khung thoại Visual Novel xanh đêm/viền vàng trong game + 3 câu gợi ý + gõ phím tự do + điều khiển EaglePhone qua tool). | Đã chứng minh hoàn chỉnh đường truyền **CLEO5 Bridge $\leftrightarrow$ Sidecar Python $\leftrightarrow$ Lua VN HUD trong game**. Có thể tái sử dụng cùng kiến trúc khung thoại VN HUD này để trò chuyện trực tiếp khi đang đi hẹn hò với bạn gái! |
| **3. EaglePhone OS v5.0 & EagleRide (App #12)** | `EagleCompanion.py`, `hud.lua`, `eagle_phone_ui.py`, `eagle_gg_map_pois.py`, `eagle_ride_engine.py` | Đã có 12 ứng dụng, `715` địa điểm `GG Map` (gồm `116` nhà hàng/quán bar/club, `79` danh lam thắng cảnh, `63` điểm Mondstadt, `WIBU-01` Nhật Bản) và dịch vụ đặt xe công nghệ `EagleRide` (`Uber / Xanh SM / Grab / Be`). | Chưa có App "Bạn Gái / Hẹn Hò" (Dating/Contacts) trên EaglePhone. Có thể đọc/ghi trực tiếp biến toàn cục SCM của `GFAGNT` từ `EagleCompanion.py` để xem độ thân mật, nhắn tin rủ đi chơi, gọi xe `EagleRide` đón bạn gái hoặc hẹn gặp tại các POI trên `GG Map`. |
| **4. Nguồn tham khảo Upstream (`ai-companion`)** | `staging/project-eagle/npc-dialogue-integration-research-20261022/upstream/ai-companion/` (`llm_brain.py`, `memory_db.py`, `ped_demographics.py`, `stage1_test[fs][mem].js`) | Có sẵn thiết kế mẫu cho `persona_girlfriend`, `trust_score (0.0..1.0)`, ghi nhận sự kiện lãng mạn (`record_memory(..., "romance", ...)`) và các action emote (`flirt`, `kiss`, `cuddle`, `dance` gọi `Grlfrd_Kiss_01` / `KISSING`). | Có thể tham khảo tập hành động (`emote` / `kiss` / `flirt` / `follow_player`) để tích hợp có kiểm soát vào CLEO5 adapter của Eagle. |
| **5. Quần thể Map Mới (`Mondstadt M0/M1/M2` & `WIBU-01`)** | `cleo/MondstadtLifeAndBlips.cs`, `INT-01..INT-07` (`Area Code 1`), `CUSTOM/wibu01_japan_island.*` | Trong 7 nội thất Mondstadt (`INT-01..06`) đã đặt sẵn **11 nhân vật Playable Mondstadt** đã uốn xương LBS (`Jean`, `Lisa`, `Barbara`, `Rosaria`, `Sucrose`, `Diona`, `Klee`, `Venti`, `Diluc`, `Kaeya`, `Albedo`). | Các nhân vật nữ tại Mondstadt hiện là model/ped đứng tạo dáng tĩnh trong nội thất, chưa gắn kịch bản hẹn hò hoặc hội thoại trực tiếp. |

---

## 4. Các Điểm Nghẽn / Giới Hạn Của Hệ Thống Bạn Gái Gốc Khi Chơi Trên Project Eagle

Dù hệ thống bạn gái gốc đang chạy đầy đủ trong `main.scm`, khảo sát source chỉ ra **5 điểm hạn chế lớn** nếu người dùng muốn trải nghiệm hẹn hò chất lượng cao với Aether:

1. **Bị khóa cứng vào 4 vùng địa lý cũ của GTA SA (`0842: GET_CITY_PLAYER_IS_IN`)**:
   - Tại `main.scm` offset `0x0239D2`, `GFAGNT` kiểm tra `0842: GET_CITY_PLAYER_IS_IN` (`0` = Quê/Sa mạc, `1` = Los Santos, `2` = San Fierro, `3` = Las Venturas) mới cho phép hiển thị blip và bắt đầu buổi hẹn.
   - Khi đi hẹn hò (`gf_date.scm`), bạn gái chỉ nhận diện các điểm ăn uống/nhảy múa cố định của San Andreas, chưa nhận diện các điểm hẹn lãng mạn tại **Thành Mondstadt (`Quán rượu Angel's Share INT-02`, `Nhà hàng Good Hunter`, `Đài phun nước Quảng trường`, `Phong Khởi Địa`)**, **Đảo Nhật Bản `WIBU-01` (`Akihabara`, `Đại lộ Hoa Anh Đào`, `Tháp Tokyo`)** hay **Vice City / Liberty City**.
2. **Nguy cơ lỗi ngoại hình Aether khi nhận thưởng quần áo `100%` (`087B` + `070D`)**:
   - Khi tình cảm đạt `100%`, `gf_date.scm` gọi `087B: GIVE_PLAYER_CLOTHES_OUTSIDE_SHOP` và `070D: BUILD_PLAYER_MODEL` để thưởng bộ đồ CJ (`Pimp`, `Racing`, `Cop`, `Medic`, `Rural`, `Gimp`). Với người chơi đang dùng skin toàn thân `AETHER` qua `RZL-Skin` (`F2`), lệnh `BUILD_PLAYER_MODEL` có nguy cơ rebuild lại mesh CJ gốc hoặc gây xung đột hiển thị.
3. **Phụ thuộc chỉ số CJ cổ điển (`Fat`, `Muscle`, `Sex Appeal`)**:
   - `gf_meeting.scm` (offset `3974..4199`) kiểm tra `Stat 21 (Fat)` và `Stat 23 (Muscle)` theo gu thẩm mỹ băng đảng năm 2004 (ví dụ: Barbara thích CJ mập `Fat >= 50%`, Helena thích CJ gầy ít cơ bắp, Katie thích CJ cơ bắp `Muscle >= 75%`), không hợp với nhân vật chính **Aether** (luôn giữ một vóc dáng chuẩn Genshin).
4. **Cơ chế bắt đầu buổi hẹn còn thủ công và thiếu chiều sâu hội thoại**:
   - Người chơi phải tự canh đúng khung giờ (`$383..$388`), tự lái xe đến tận cửa nhà ở LS/SF/LV/Sa mạc và bước vào vòng tròn đỏ; trong buổi hẹn chỉ hiện vài dòng subtitle ngắn lặp đi lặp lại (`GF_0036..GF_0075`), không có trò chuyện AI, không nhắn tin hẹn trước qua điện thoại và không lưu lại kỷ niệm buổi hẹn.
5. **Danh tính nhân vật chưa đồng bộ giữa Skin, Voice và Lore**:
   - Dù 6 slot `190..195` đã mang ngoại hình **Furina, Hu Tao, Citlali, Columbina, Kirara, Vesna**, nhưng tên hiển thị trên HUD/Stats và giọng lồng tiếng (`SPC_GA`) vẫn là **Katie, Michelle, Denise, Millie, Helena, Barbara** của GTA SA 2004.

---

## 5. Đề Xuất Lộ Trình Cải Thiện Tính Năng Bạn Gái (Song Song Với Map, NPC Chatbot & Paimon Agent)

Khi người dùng kết thúc phiên test hiện tại và sẵn sàng triển khai, tính năng Bạn Gái có thể được nâng cấp theo **3 giai đoạn mô-đun hóa** (hoàn toàn tương thích với `EaglePhone`, `Paimon Agent`, `Character Chat` và `Mondstadt / WIBU-01`):

### Giai đoạn 1 — Cầu nối Quản lý Bạn Gái trên `EaglePhone` & Vá Tương Thích Aether (Nhanh, An Toàn, Không Sửa `main.scm`)
- **Đọc/ghi trực tiếp RAM của `GFAGNT` từ `EagleCompanion.py`**:
  - Đọc/điều chỉnh trực tiếp biến toàn cục SCM `$406` (`1624` — bitmask mở khóa 6 bạn gái), `$359..$364` (`1436..1456` — điểm tình cảm `0..100%`) và `Stat 252..257`.
  - Cho phép **mở khóa ngay cả 6 bạn gái Genshin (`Furina`, `Hu Tao`, `Citlali`, `Columbina`, `Kirara`, `Vesna`)** mà không bị chặn bởi chỉ số `Fat`/`Muscle` của CJ.
  - Đổi tên hiển thị trên `EaglePhone` đúng theo nhân vật Genshin đang cài (`Citlali`, `Hu Tao`, `Kirara`, `Vesna`, `Furina`, `Columbina`) kèm khung giờ rảnh, vị trí blip và nút **Đặt mốc GPS (`GG Map`) / Đặt xe `EagleRide` tới đón bạn gái**.
  - Thêm guard bảo vệ skin `AETHER` để không bị `070D: BUILD_PLAYER_MODEL` ghi đè khi đạt `100%` tình cảm.

### Giai đoạn 2 — Hẹn Hò Thông Minh Có Hội Thoại AI (Nối `Character Chat Studio` + `VN HUD` của `eagle-dialogue`)
- **Nhắn tin & Hẹn gặp qua EaglePhone**:
  - Tích hợp danh bạ Bạn Gái / Waifu Genshin (gồm cả 6 bạn gái trong game `Furina`, `Hu Tao`, `Citlali`, `Columbina`, `Kirara` lẫn dàn nhân vật nữ trong `Character Chat Studio` như `Jean`, `Lisa`, `Barbara`, `Noelle`, `Fischl`, `Mona`) vào hệ thống chat AI (`gpt-6-luna`).
- **Trò chuyện trực tiếp trong buổi hẹn bằng khung `VN HUD` (giống Paimon)**:
  - Khi đang đi dạo phố, ngồi trên xe hoặc vào nhà hàng/quán rượu cùng bạn gái, mở khung thoại `VN HUD` để trò chuyện bằng tiếng Anh/Việt có ngữ cảnh thực tế (vị trí đang đứng, thời tiết, chiếc xe đang đi, nhà hàng đang ăn).
  - Kết quả buổi hẹn và nội dung trò chuyện được ghi nhận thành **Kỷ niệm thật (`shared_memories`)** trong SQLite và cộng trực tiếp vào thanh tiến độ tình cảm (`Affection / Trust`).

### Giai đoạn 3 — Mở Rộng Điểm Hẹn Hò Sang Map Mới (`Mondstadt M0–M2`, `Đảo Nhật Bản WIBU-01` & `715 POIs`)
- **Cho phép hẹn hò tại các địa danh Anime/Genshin mới**:
  - Đón bạn gái (hoặc gặp trực tiếp `Jean`, `Lisa`, `Barbara`, `Noelle`, `Fischl`, `Mona`, `Furina`, `Hu Tao` tại **Mondstadt / Đảo Nhật Bản `WIBU-01`**) đi dạo **Đại lộ Hoa Anh Đào Akihabara**, ngắm cảnh trên **Tượng Phong Thần Barbatos / Phong Khởi Địa**, uống rượu tại **Tửu trang Dawn Winery (`INT-06`) / Quán rượu Angel's Share (`INT-02`)**, hoặc đi chung xe **EagleRide (`App #12`)**.
- **Tích hợp với Paimon Agent (`App #11`)**:
  - Paimon đóng vai trò "Quân sư tình cảm" (Wingman): nhắc lịch hẹn sắp tới, gợi ý địa điểm hẹn hò trên `GG Map` hợp gu từng nhân vật, hoặc đặt sẵn xe `EagleRide` / mua hoa giúp Aether.
