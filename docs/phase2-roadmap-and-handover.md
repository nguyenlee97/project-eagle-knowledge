# Kế Hoạch Phase 2 & Tài Liệu Bàn Giao Ngữ Cảnh (Handover Plan)

> **Phối hợp hai bên agent:** mọi feature mới tích hợp vào gameplay-lab theo [knowledge và quy ước phối hợp chung](shared-agent-workflow.md); đăng ký phạm vi và giữ khóa trước khi ghi runtime/metadata deployment dùng chung.

> **Bàn giao mới nhất 22/10/2026 — chỉ chơi/build gameplay-lab.** Bản clean, Library và staging/backup skin đã được chuyển vật lý sang D, giữ junction C để tương thích. Skin Viewer đã nhận ownership lab theo baseline/hash merge; các luồng menu/loading/radio cũng nhắm lab. Đọc [báo cáo chuyển ổ và đổi đích build](storage-migration-and-lab-handover-2026-10-22.md) trước khi tiếp tục; không dùng bản clean lưu trữ hoặc lịch sử build/rollback clean làm đích mới.

> **Cập nhật 22/10/2026 — đã merge nội dung Wibu vào lab.** Loading/splash, main menu và NPC sửa rig mới nhất đã được đưa từ clean sang gameplay-lab. Aether/radio, các bản vá engine, Sidecar/EaglePhone và gameplay lab được giữ; đủ 37 file cài kiểm hash, 2.789 file được bảo vệ và 10 junction không đổi. Bản hợp nhất chưa được agent thử trong game. Đọc [báo cáo merge, launcher và rollback](merge-clean-to-gameplay-lab-2026-10-22.md) trước khi tiếp tục Phase 2; phần dưới ghi lịch sử MVP và roadmap.

> **Mục đích**: Tài liệu này đóng gói toàn bộ trạng thái hiện tại của **Phase 1 MVP** trong `gta sa gameplay-lab` và kế hoạch chi tiết cho **Phase 2 (4 hạng mục tiếp theo)** để khi khởi tạo hội thoại mới, Agent mới có thể đọc 1 file duy nhất này và bắt tay vào làm ngay mà không tốn context khảo sát lại từ đầu.

---

## I. Trạng Thái Hiện Tại (Bàn Giao Từ Phase 1 MVP)

### 1. Môi trường & Đường dẫn (Đã hợp nhất sau Merge & Chuyển ổ ngày 22/10/2026)
- **Bản chơi & đích tích hợp feature mới duy nhất (Unified Gameplay Lab)**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **File khởi động chuẩn**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\Start_Eagle_Lab_With_Sidecar.bat`
- **Thư mục Staging & Scripts quản lý Gameplay Lab**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc`
- **Bản Clean cũ (ĐÃ LƯU TRỮ TRÊN Ổ D — KHÔNG DÙNG LÀM ĐÍCH BUILD/CÀI MOD)**: `D:\GTA Archive\Project Eagle\gta sa clean\gta sa clean` (đường dẫn `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean` hiện là NTFS junction trỏ sang ổ D).
- **Kho Skin vật lý & Staging/Backup Skin**: `D:\GTA Archive\Skin Library`, `D:\GTA Archive\Skin Staging`, `D:\GTA Archive\Skin Backups` (các đường dẫn cũ trên C được giữ bằng NTFS junction).
- **Khóa ghi điều phối chung giữa Codex & Antigravity**: `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\coordination\game-write.lock` (theo [`shared-agent-workflow.md`](shared-agent-workflow.md)).

### 2. Các gói Mod & Bản vá Engine đã tích hợp ổn định
1. **Bản vá Engine & Plugin cốt lõi**:
   - Đã vá lỗi vòng lặp vô tận `CPathFind::DoPathSearch` (`VA 0x00451A00` / file offset `0x00050E00` trong `gta_pe.exe`) khi gặp node đường bất đối xứng (`NODES1890.DAT`).
   - Đã vá `cleo\CLEO+.cleo` v1.2.0 tương thích 100% với `fastman92limitAdjuster.asi` (FLA 7.7).
2. **Nhóm A (`install_group_a_mods.py` / `rollback_group_a_mods.py` / `backups/group_a_manifest.json`)**:
   - Kiến trúc cửa hàng thật, nội thất mở rộng (`EHI.IPL`, `INTERIOR_DOORS.IPL`, `FORTCARSON_INTERIORS.IPL`), sự kiện đường phố (`Busy Pedestrians`, `Random Events`, `Ambient Taxi`, `Street Art`, `Commercial Mod`), vũ khí & âm thanh (`Immersive Weapons Pack`), góc nhìn thứ nhất (`UltimateFP`).
   - Đã sửa ID ped bị thiếu (`208`/`265` $\rightarrow$ `71`/`253`) trong `cleo\Busy Pedestrians.ini` (chống crash khi hồi sinh ở bệnh viện).
   - Đã gỡ bỏ hoàn toàn `cleo\gasoline.cs` & `models\txd\gasoline.txd` (tắt tính năng hết xăng gây bất tiện khi lái xe, giữ nguyên kiến trúc cây xăng và phím `J`/`L` bật/tắt máy xe của `on_off_engine.cs`).
3. **Nhóm B1 (`install_group_b1_mods.py` / `rollback_group_b1_mods.py` / `backups/group_b1_manifest.json`)**:
   - `CUSTOM\GROUP_B1_TEXTURES.IMG` (`283` file texture cửa hàng & biển quảng cáo thập niên 90 tại LS/SF/LV, không đụng tới NPC skin và không đè Nhóm A) + `New Official Loading Themes`.
4. **Nhóm B3 (`install_group_b3_mods.py` / `rollback_group_b3_mods.py` / `backups/group_b3_manifest.json`)**:
   - `CUSTOM\GROUP_B3_ASSETS.IMG` (`GasStation.ifp`, `PedEventsMod.ifp`, `StreetCL.ifp`).
   - 7 script CLEO đã gia cố **Zero-Shift On-Demand Streaming Trampoline** (`@LoadAssetsSub` tự nạp lại model/IFP ngay khi vào bán kính 100m): `ML_Constructions.cs`, `ML_Fisher.cs`, `ML_GasWorker.cs`, `ML_Homeless.cs`, `ML_LifeInSF.cs`, `ML_Mechanic.cs`, `ML_DinerInterior.cs`.

### 3. Kiến trúc Sidecar & Điện thoại hiện tại (`EagleCompanion.py` + `hud.lua`)
- **Sidecar Python**: `EagleCompanion.py` + `eagle_historical_data.py` + `eagle_phone_ui.py` (đồng bộ trực tiếp RAM với `gta_pe.exe` qua `ADDR_PLAYER_PED_PTR = 0x00B7CD98`, `ADDR_PLAYER_MONEY = 0x00B7CE50`, `ADDR_EAGLE_MAILBOX = 0x00CAFE00` và ghi state sang `cleo/EaglePhoneState_0.lua` / `EaglePhoneState_1.lua`).
- **Renderer trong game**: `SanViveLuaHudSA.asi` thực thi `hud.lua` (bản gốc trong staging là `hud_eaglephone.lua`).
- **Phát hiện kỹ thuật quan trọng cho Phase 2**:
  - `SanViveLuaHudSA.asi` có sẵn binding C++ `sol2` cho **`TxdStore.GetFileById`**, **`TxdFile:FindTexture`**, **`Sprite.UseTexture(rwTexture)`**, **`Sprite.RenderOneXLUSprite(...)`**, **`Sprite2d.DrawSprite`**, **`Sprite2d.DrawShape`**, **`Sprite2d.DrawLine`**, **`Sprite2d.DrawRect`**.
  - Điều này cho phép nạp trực tiếp file `.txd` chứa **hình ảnh Anime, Icon ứng dụng, Banner, Avatar, Khung UI** vào game và vẽ lên màn hình điện thoại!

---

## II. Kế Hoạch Triển Khai Phase 2 (Theo Thứ Tự Ưu Tiên)

### Hạng mục 1: Hệ thống Báo Bug & Chẩn Đoán Tọa Độ Map (In-Game Bug Reporter & Auto-Inspector) — ✅ ĐÃ HOÀN TẤT (`EaglePhone OS v4.6`)
**Vấn đề thực tế**: Map của Project Eagle (và các vùng mở rộng) đôi khi có nhà thiếu sàn (bước vào rơi tự do), tường tàng hình chặn đường, hoặc mất mặt đường (đi qua rơi xuống void).

**Trạng thái triển khai (`eagle_map_inspector.py` + `EagleCompanion.py` + `hud.lua` + `eagle_phone_ui.py`)**:
1. **Phím tắt toàn cục & App 8 (`8.BUG`) trên In-Game HUD + Web UI**:
   - **Phím `F11` (Instant Bug Report & Auto-Inspector)**: Hoạt động mọi lúc (kể cả khi đang đóng điện thoại). Tự động thu thập tọa độ hiện tại, lịch sử 5 giây trước khi rơi (`-5s, -3s, -2s, -1s, 0s`), quét vật thể `.ipl`/`.ide`/`.img`/`.col` trong bán kính `15m`, lưu báo cáo chuẩn hóa và **tự động cứu hộ về vị trí an toàn `-3s` nếu phát hiện nhân vật đang rơi tự do (`vz < -0.20` hoặc `Z < -3.0m`)**.
   - **Phím `F12` (Instant Safe Recall / Cứu Hộ Nhanh)**: Dịch chuyển tức thì nhân vật (và cả xe nếu đang lái) về vị trí mặt đất an toàn `3 giây trước khi rơi` (hoặc `Lùi lại 5m thoát kẹt tường vô hình` / `Nâng cao +4.5m`), đồng thời **triệt tiêu toàn bộ vector vận tốc rơi & xoay (`+0x44`, `+0x50`)** để không bị mất máu khi tiếp đất.
   - **App 8 (`8.BUG`)**: Tích hợp đầy đủ trên cả HUD trong game (`hud.lua`) lẫn Web Smartphone (`http://127.0.0.1:8765`).
2. **Engine Chẩn Đoán Map Tự Động (`eagle_map_inspector.py` + `cleo/EagleMapIndex.cache`)**:
   - Đánh chỉ mục toàn bộ **`59,491` IDE models**, **`83,878` Text IPL `inst`**, **`62,839` Binary Stream IPL `inst` (`bnry` bên trong `.img`)**, **`41,815` COL collision models (`COLL`/`COL2`/`COL3`/`COL4` với số lượng `faces`/`boxes`/`spheres`)** và **`1,099` cửa `ENEX`**.
   - Thời gian nạp cache chỉ `~0.85s` và truy vấn không gian 2 tầng (`50m` + `200m` coarse grid cho vật thể lớn) chỉ mất **`~4ms`**.
   - Tự động gắn cờ chẩn đoán (`MISSING_COL_ENTRY`, `EMPTY_COL_0_FACES`, `MISSING_DFF_IN_IMG`, `MISSING_TXD_IN_IMG`, `INTERIOR_MISMATCH`, `INVISIBLE_WALL_COLLIDER`) và xuất báo cáo ra `docs/project-eagle/map-bug-reports.md` & `docs/project-eagle/map-bug-reports.json` kèm mẫu copy-paste gửi Discord Project Eagle.

---

### Hạng mục 2: Đại Tu Giao Diện Điện Thoại (EaglePhone OS v5.0 — Homescreen Icons, Sub-Pages, Anime Vibe & Visual UI) — ✅ ĐÃ HOÀN TẤT (`EaglePhone OS v5.0`)
**Vấn đề thực tế**: Điện thoại cũ hiển thị dạng 7–8 tab chữ dày đặc, thiếu tính trực quan của một chiếc smartphone hiện đại và thiếu chất Anime/Wibu.

**Trạng thái triển khai (`build_eaglephone_txd.py` + `models/hud.txd` + `EagleCompanion.py` + `hud.lua` + `eagle_phone_ui.py`)**:
1. **22 Anime/Genshin Textures (`.txd` & `.png`) nạp trực tiếp vào RenderWare**:
   - Đóng gói 22 texture 32-bit BGRA (`D3DFMT_A8R8G8B8 = 0x15`, `rwRASTERFORMAT8888 = 0x500`) vào `models/hud.txd` (có backup gốc tại `staging/project-eagle/gameplay-lab-poc/backups/hud.txd.bak`), `CUSTOM/EAGLEPHONE_UI.TXD`, `models/txd/EAGLEUI.TXD` và `ui_assets/*.png`:
     - **3 Hình nền Anime (`256x512`)**: `ep_wp_furina` (Furina Hydro Neon), `ep_wp_raiden` (Raiden Electro Violet), `ep_wp_hutao` (Hu Tao Crimson Night).
     - **4 Mascot Chibi/Cutout (`128x128`)**: `ep_ms_furina`, `ep_ms_hutao`, `ep_ms_keqing`, `ep_ms_raiden`.
     - **9 App Icons bo góc (`64x64`)**: `ep_ic_life`, `ep_ic_stck`, `ep_ic_cryp`, `ep_ic_bet`, `ep_ic_loto`, `ep_ic_news`, `ep_ic_port`, `ep_ic_bug`, `ep_ic_set`.
     - **6 Visual Cards & Banners (`256x64`)**: `ep_cd_atm`, `ep_cd_meal`, `ep_bn_pol`, `ep_bn_fin`, `ep_bn_wibu`, `ep_bn_spt`.
   - Trong `hud.lua`, cơ chế `RefreshEagleTextures()` duyệt vòng liên kết `RwLLLink` của `RwTexDictionary` từ `0x00BAB1FC` (`CHud::Sprites[0]`) kết hợp `Hud.GetFistTexture()` để lấy `sol2` `RwTexture*` userdata cho toàn bộ 22 texture `ep_*` và vẽ bằng `Sprite.UseTexture` + `Sprite.RenderOneXLUSprite`.
2. **Kiến trúc Điều hướng Đa Tầng (`Home Screen 0` $\leftrightarrow$ `Apps 1..9` $\leftrightarrow$ `Sub-page`)**:
   - **Màn hình Chính (`phone_app = 0`)**: Hình nền Anime全màn hình, Widget Thời tiết/Tài sản/Mascot ở trên, và **Lưới 3x3 Icon Ứng Dụng (`1..9`)** điều hướng 4 chiều bằng `I/K/J/L`, mở App bằng `F9`/`Enter` (hoặc phím `1..9`), quay lui đa tầng bằng `Backspace`/`F8` (`Sub-page -> Bảng chính -> Home Screen 0`) hoặc phím `0`.
   - **Tách Sub-page, Bảng kẻ ô 4 cột (`DrawTableRow4`), Visual Cards & Gauge Bars**:
     - *App 1 (Đời Sống & Ngân Hàng)*: Tách `Trang 1: Sinh Hoạt & Nhà Hàng` (`ep_cd_meal` + 3 thanh Gauge Máu/Độ No/Năng Lượng) và `Trang 2: Thẻ ATM Platinum & Tín Dụng` (`ep_cd_atm`).
     - *App 2 (Cổ Phiếu/Vàng) & App 3 (Crypto)*: Tách `Trang 1: Bảng Điện Market Watch 4 Cột` (`Mã | Giá | %24h | Đang Giữ` có kẻ sọc Zebra) $\leftrightarrow$ bấm `F9`/`Enter` vào mã bất kỳ mở `Trang 2: Biểu Đồ Nến & Đặt Lệnh Spot/Futures`.
     - *App 4 (Thể Thao)*: Tách `Trang 1: Bảng Kèo Scoreboard 4 Cột` (`Giờ | Cặp Đấu | 1-X-2 | Tài/Xỉu`) + 5 ô tỷ lệ cược trực quan và `Trang 2: Bảng Xếp Hạng Giải Đấu`.
     - *App 5 (Xổ Số)*: Hộp **Vé Cào 3x3 Ô (`DrawScratchGrid3x3`)** trực quan + dãy bóng số XSKT 16:30 & Vietlott 18:00.
     - *App 6 (Báo Ngày EagleTimes)*: 4 trang chuyên mục (`Thế Giới`, `Phố Wall & Vàng`, `Crypto & Wibu`, `Thể Thao`) kèm ảnh bìa `ep_bn_*` tương ứng.
     - *App 7 (Danh Mục Chung)*: Thanh **Asset Allocation Gauge Bar** (`Tiền/Bank`, `Cổ Phiếu/Vàng`, `Crypto`, `Futures/Bet`) + Bảng 4 cột cho từng nhóm tài sản.
     - *App 8 (Báo Bug Map & Auto-Inspector)*: Tích hợp vào Lưới 3x3 Home (`ep_ic_bug`), chia `Trang 1: Radar Tọa Độ, Vệt 5s & Cứu Hộ F12` và `Trang 2: Bảng 4 Cột Nghi Phạm .IPL/.COL`.
     - *App 9 (Cài Đặt & Giao Diện Anime)*: Đổi trực tiếp Hình nền (`Furina` / `Raiden` / `Hu Tao`), Mascot (`Furina` / `Hu Tao` / `Keqing` / `Raiden`) và Chủ đề Neon (`Cyan` / `Purple` / `Crimson` / `Gold`).

> **Cập nhật 22/10/2026**: Xem báo cáo kiểm toán thực tế đầy đủ nhất (byte-diff của `gta_pe.exe`/`PECore.asi`/`CLEO+.cleo`, 14 file khác biệt giữa `clean` và `lab`, 10 NTFS junctions, vị trí backup/rollback và ma trận kiểm thử in-game) tại **[`gameplay-lab-current-status-2026-10-22.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/gameplay-lab-current-status-2026-10-22.md)**.

---

### Hạng mục 3: Nâng Cấp Toàn Diện Báo Ngày `EagleTimes` Bằng Subagents (Sống Lại Kỷ Nguyên 2010–2025) — ✅ ĐÃ TRIỂN KHAI (`eagle_news_archive_2010_2025.py`)
**Vấn đề trước đây**: Mỗi ngày chỉ có rất ít sự kiện cố định hoặc lặp lại theo năm, đọc nhanh chán và chưa gợi lại được cảm giác hoài niệm sống động của từng giai đoạn 2010–2025.

**Trạng thái triển khai (`eagle_news_archive_2010_2025.py` — `1,781,548 B`, hơn 18.700 dòng)**:
1. **Đã biên tập hoàn chỉnh bộ cơ sở dữ liệu 16 năm (`2010–2025`) qua 4 Subagents (`2010–2013`, `2014–2017`, `2018–2021`, `2022–2025`)**:
   - **6 chuyên mục tích hợp vào App 6 (`6.Báo Ngày`)**:
     1. 🌍 **Thế Giới & Thời Sự**: Các cột mốc lịch sử có thật theo đúng dòng thời gian.
     2. 💻 **Công Nghệ & Đời Sống Số**: Yahoo! 360/Messenger, iPhone 4, Nokia Lumia, Flappy Bird (2014), Pokémon GO (2016), trào lưu quán Net, Facebook đời đầu, YouTube, TikTok, ChatGPT...
     3. 🎮 **Game & Văn Hóa Anime / Wibu**: Liên Minh Huyền Thoại, Dota 2, GTA V (2013), Sword Art Online (2012), Attack on Titan (2013), Your Name (2016), Demon Slayer (2019), **Genshin Impact ra mắt (28/09/2020)** và các bản cập nhật Inazuma/Sumeru/Fontaine/Natlan...
     4. 📈 **Kinh Tế, Vàng & Phố Wall**: Diễn biến khớp với giá cổ phiếu/vàng trong game.
     5. 🪙 **Crypto & Blockchain**: Từ thời đào Bitcoin bằng CPU, Mt.Gox, Halving, ICO 2017, DeFi/NFT 2021 đến ETF 2024.
     6. ⚽ **Thể Thao Đỉnh Cao**: Cúp C1, Ngoại Hạng Anh, World Cup, Euro, Quả Bóng Vàng Messi - Ronaldo qua từng năm.
2. **Trạng thái kiểm thử**: Đã tích hợp vào `EagleCompanion.py`, `hud.lua`, `eagle_phone_ui.py` và kiểm tra nạp module/UI; chưa kiểm thử chơi qua toàn bộ 16 năm trong game.

---

### Hạng mục 5 (Làm trước Hạng mục 4, tích hợp vào EaglePhone): Ứng dụng `GG Map` (GTA Genshin Map) & Chỉ Đường GPS Tự Động — ✅ ĐÃ TRIỂN KHAI (`App 10` / `eagle_gg_map_pois.py`)
**Mục tiêu**: Tạo ứng dụng bản đồ điểm đến **GG Map (GTA Genshin Map)** ngay trong `EaglePhone` (`App 10`, icon `ep_ic_ggmap`), tổng hợp **631 địa điểm POI** thuộc 10 danh mục khắp bản đồ Project Eagle.

**Trạng thái triển khai (`eagle_gg_map_pois.py` + `EagleCompanion.py` + `hud.lua` + `eagle_phone_ui.py`)**:
1. **Cơ chế Cắm Mốc Chỉ Đường Tự Động (Native `T` Waypoint & GPS Route)**:
   - Giải quyết tương thích với Fastman92 Limit Adjuster 7.7 (`Radar traces = 3000`): Đọc động con trỏ mảng `CRadar::ms_RadarTrace` đã được FLA dời về địa chỉ lệnh `0x005838B2` (số lượng tối đa tại `0x0058384E`), ghi trực tiếp `sRadarTrace` (sprite `41 = RADAR_SPRITE_WAYPOINT`) và cập nhật handle vào `FrontEndMenuManager.m_nTargetBlipIndex` (`0x00BA6774`).
   - **Bản vá RAM động cho `PECore.asi` (`_ensure_pecore_onfoot_gps_patch`)**: Vá 6 bytes tại `pecore_base + 0x000D0743` (`8B 81 8C 05 00 00` $\rightarrow$ `EB 45 90 90 90 90`) để `PECore.asi` vẽ đường dẫn GPS trên radar ngay cả khi nhân vật đang đi bộ.
   - **Sửa lỗi Desktop ảo cho luồng đọc phím (`_ensure_interactive_desktop`)**: Gọi `OpenInputDesktop` + `SetThreadDesktop` để `GetForegroundWindow()` và `GetAsyncKeyState()` luôn nhận phím ngay cả khi `EagleCompanion.py` được khởi chạy từ terminal sandbox.
   - **Trạng thái kiểm thử**: Người dùng đã test hiển thị danh sách địa điểm trong game; bản sửa địa chỉ FLA `0x005838B2` + patch RAM `PECore.asi` + `_ensure_interactive_desktop` đã được xác minh trên tiến trình game đang chạy qua ProcessBridge, chờ người dùng xác nhận nghiệm thu cuối trong game.
2. **10 Danh Mục Điểm Đến (`631 POIs` trong `eagle_gg_map_pois.py`, tự động sắp xếp từ gần đến xa theo vị trí người chơi)**:
   - `1. Tất Cả (ALL - 631)`, `2. Thắng Cảnh & Địa Danh (LANDMARKS - 79)`, `3. Trung Tâm Giao Thông (TRANSIT - 28)`, `4. Ẩm Thực & Giải Trí (FOOD_CLUB - 116)`, `5. Casino & Cá Cược (CASINO_BET - 24)`, `6. Mua Sắm & Làm Đẹp (SHOPS_STYLE - 135)`, `7. Vũ Khí & Độ Xe (GUN_GARAGE - 40)`, `8. Gym & Trường Đua (GYM_STADIUM - 12)`, `9. Nhà Riêng & Nội Thất (SAFEHOUSE_INT - 185)`, `10. Thế Giới Wibu/Anime (WIBU_WORLD - 12)`.

---

### Hạng mục 4 (Thực hiện sau khi hoàn tất Merge): "Project Wibu / Genshin Urban"
**Tầm nhìn**: Biến thế giới thành thị của Project Eagle thành một **Thế giới Anime / Genshin Impact hiện đại** theo từng bước an toàn, có kiểm soát và có rollback riêng cho từng lớp:
1. **Giai đoạn 4.1 — Wibu hóa Biển Quảng Cáo (Billboards) & Màn hình LED đô thị** (`GROUP_B1_TEXTURES.IMG`).
2. **Giai đoạn 4.2 — Thảm thực vật & Bầu trời / Màu sắc Tươi Sáng (Cel-Shaded / Anime Daylight Vibe)**.
3. **Giai đoạn 4.3 — Kiến trúc Nhật Bản & Khu phố / Map Bí Mật (Secret Anime Maps)**.
4. **Giai đoạn 4.4 — Nhân vật chính Aether (Full Rig & Animation) + Dàn NPC Anime/Game + Radio Custom**.

---

## III. Trạng Thái Sau Merge & Quy Ước Phối Hợp Chung (`22/10/2026`)

1. **Đã hoàn tất Merge (`gta sa clean` $\rightarrow$ `gta sa gameplay-lab`) & Chuyển lưu trữ sang ổ D**:
   - **37 file** từ `clean` (gồm `PECore.asi` có splash Project Wibu, `modloader/WibuWorldLoading/txd/loadscs.txd`, `modloader/modloader.img`, 32 file `WibuMenu.asi` + `.wibu-menu-install-state.json` mới cho lab, và `S&S/Cdimages/default/COMPONENTPEDS.img` `12,782,344,192 B` đã sửa 7 DFF rig 32/32 RW 3.6.0.3) đã được tích hợp vào `gta sa gameplay-lab`.
   - **2.789 file** riêng của `gameplay-lab` và **10 NTFS junctions** ở thư mục gốc Lab được bảo toàn nguyên vẹn 100%.
   - Backup của transaction merge đặt tại `D:\GTA Archive\Project Eagle Merges\clean-to-lab-2026-10-22` (kiểm tra/khôi phục qua `staging\project-eagle\merge-clean-to-lab-2026-10-22\Check_Rollback.bat` và `Rollback_Merge.bat`).
   - Chi tiết xem tại:
     - **[`merge-clean-to-gameplay-lab-2026-10-22.md`](merge-clean-to-gameplay-lab-2026-10-22.md)** (Hồ sơ transaction merge 37 file & rollback).
     - **[`storage-migration-and-lab-handover-2026-10-22.md`](storage-migration-and-lab-handover-2026-10-22.md)** (Hồ sơ chuyển 19 cây thư mục sang ổ D, đổi đích Skin Viewer / Radio Studio / WibuMenu sang Lab, và policy mirror 11 member ped trùng giữa `GROUP_A_MODS.IMG` và `COMPONENTPEDS.img`).
     - **[`gameplay-lab-current-status-2026-10-22.md`](gameplay-lab-current-status-2026-10-22.md)** (Hồ sơ kỹ thuật byte-diff của `gta_pe.exe`, `PECore.asi`, `CLEO+.cleo`, loader, 10 junctions và ma trận kiểm thử trước merge).
2. **Quy ước làm việc chung giữa Codex và Antigravity ([`shared-agent-workflow.md`](shared-agent-workflow.md))**:
   - Đọc [`AGENTS.md`](../../AGENTS.md), [`GEMINI.md`](../../GEMINI.md), [`shared-agent-workflow.md`](shared-agent-workflow.md) và các phiếu trong [`work-items/`](work-items/README.md) trước khi bắt đầu.
   - Đăng ký phạm vi bằng phiếu `docs/project-eagle/work-items/<YYYY-MM-DD>-<agent>-<task-id>.md`.
   - Khi ghi vào runtime `gta sa gameplay-lab`, metadata deployment chung hoặc chạy rollback, bắt buộc chiếm khóa thư mục độc quyền `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\coordination\game-write.lock` kèm `owner.json`, kiểm lại hash thực tế ngay trước khi ghi và nhả khóa sau khi cập nhật bàn giao.



