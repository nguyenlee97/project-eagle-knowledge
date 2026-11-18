# Báo Cáo Trạng Thái Thực Tế `gta sa gameplay-lab` & Hồ Sơ Kỹ Thuật Phục Vụ Merge

> **Presentation hiện tại03/11/2026:** [178ảnh, loading2s/menu4s, nhạc auto-next, true intro bypass đã được user test PASS](presentation-current-state.md). Snapshot22/10 bên dưới không đại diện phiên bản menu/loading hiện tại.

> **Snapshot trước merge lúc 04:20, đã được thay thế về trạng thái hiện tại.** Merge đã hoàn tất ngày 22/10/2026, gồm cả main menu mới và archive NPC đã sửa định dạng/rig. 37 file cài được kiểm hash; 2.789 file lab ngoài phạm vi merge và 10 junction giữ nguyên. Xem [báo cáo sau merge](merge-clean-to-gameplay-lab-2026-10-22.md) để biết file hiện tại, backup và rollback. Các số đếm, điều kiện chờ sửa NPC và hướng dẫn copy bên dưới được giữ làm lịch sử, không áp dụng lại vào lab đã merge.

> Clean và kho skin hiện lưu vật lý trên D; các đường C cũ là junction. Gameplay-lab là đích chơi/build duy nhất. Xem [bàn giao chuyển ổ và workflow lab](storage-migration-and-lab-handover-2026-10-22.md) để biết đường dẫn và kiểm tra mới nhất.

- **Ngày cập nhật**: `22/10/2026` (04:20 AM, Asia/Saigon)
- **Thư mục Lab đang hoạt động**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Clean đối chiếu**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`
- **Thư mục Staging của Lab**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc`
- **Mục đích tài liệu**: Cung cấp trạng thái thực tế trên đĩa (ground-truth), chi tiết byte-level của mọi bản vá nhị phân (`gta_pe.exe`, `PECore.asi`, `CLEO+.cleo`), cấu hình loader, phụ thuộc đường dẫn/junction, vị trí backup/rollback và phân định rõ phần đã kiểm thử trong game vs chưa kiểm thử — giúp người dùng và Agent phụ trách merge hai bản (`gta sa clean` $\leftrightarrow$ `gta sa gameplay-lab`) nắm toàn bộ ngữ cảnh mà không bỏ sót bất kỳ thay đổi nào.

---

## I. Đối Chiếu Toàn Cục Auf-Disk Giữa `gta sa gameplay-lab` Và `gta sa clean`

Kết quả quét đối chiếu SHA-256 toàn bộ cây thư mục giữa hai bản cài lúc `04:18 AM 22/10/2026`:
- **Tổng số file trong `gta sa clean`**: `1,721` files
- **Tổng số file trong `gta sa gameplay-lab`**: `3,482` files
- **Số file chung đường dẫn**: `1,714` files (trong đó **`1,696` files giống hệt nhau 100% về byte/SHA-256**, bao gồm toàn bộ `AETHER.dff`/`AETHER.txd` trong `modloader\RZL-Skin`, `data\radio.dat`, `S&S\ZON\radio.zon`, `models\txd\radio.txd` và 14 file âm thanh `audio\PE\RADIO\*`).
- **Số file chỉ có bên `gta sa clean`**: **`7` files**:
  1. `modloader\WibuWorldLoading\txd\loadscs.txd` (`37,181,768 B`, SHA-256 `7a3e0899f94908ef...` — bộ 14 poster anime 2D Wibu World).
  2. `secrets.local.json` (`121 B`).
  3. `5` file crash log trong `ProjectEagle_crashes\` (`2026-10-14_18-37-06.log`, `2026-10-14_19-47-46.log`, `2026-10-22_00-16-50.log`, `2026-10-22_04-06-47.log`, `2026-10-22_04-06-56.log`).
- **Số file chỉ có bên `gta sa gameplay-lab`**: **`1,768` files** (gồm hệ thống `EagleCompanion`/`EaglePhone OS v5.0`, `GG Map`, `EagleTimes 2010–2025`, `Auto-Inspector`, `CLEO+`, `UltimateFP`, và các gói mod Nhóm A, B1, B3).

### Bảng 14 File Non-Log Duy Nhất Khác Biệt Giữa 2 Bản (Trong 1,714 File Chung)

*(Ngoài 4 file log runtime `cleo.log`, `fastman92limitAdjuster.log`, `modloader\modloader.log`, `PECore.log`, chỉ có đúng **14 file** dưới đây khác nhau giữa 2 bản)*:

| STT | Đường dẫn tương đối | Bản `gta sa clean` (Size / SHA-256 đầu) | Bản `gta sa gameplay-lab` (Size / SHA-256 đầu) | Bản nào đang giữ thay đổi gì? (Hướng xử lý khi Merge) |
|---:|---|---|---|---|
| 1 | `gta_pe.exe` | `14,383,616 B` (`f115b49c5ac3a8fc`) | `14,383,616 B` (`ddf6456c9a1173b1`) | **Lab**: Đã vá lỗi treo vòng lặp vô tận `CPathFind::DoPathSearch` + đổi Window Title `GTA: Eagle Lab` + chuỗi `\GTA PE Lab Files`. 👉 **Giữ bản Lab**. |
| 2 | `gta_sa.exe` | `14,383,616 B` (`7c5a7661b2e01d64`) | `14,383,616 B` (`770170fe897eb23f`) | **Lab**: Bản sao của `gta_pe.exe` đã vá isolation strings. 👉 **Giữ bản Lab**. |
| 3 | `PECore.asi` | `3,151,360 B` (`4c3b891061d773b0`) | `2,977,792 B` (`a81c69ef38b8de8f`) | **Clean**: Đã thay PNG splash Hu Tao (`RCDATA 10/200/1033`) + chuỗi `"Project Wibu is loading"` tại RVA `0x1D0A58`. Section `.text`/`.data` 2 bản giống nhau 100%; riêng **Lab** có thêm patch RAM động lúc chạy (`+0x000D0743`) từ `EagleCompanion.py`. 👉 **Dùng bản `PECore.asi` của Clean đưa sang Lab** (vì RVA `.text` không đổi nên patch RAM `+0x000D0743` của Lab vẫn khớp 100%). |
| 4 | `S&S\Cdimages\default\COMPONENTPEDS.img` | `12,782,338,048 B` (~11.90 GiB) | `444,977,152 B` (~424.36 MiB) | **Clean**: Chứa dàn skin NPC mới build từ Skin Library (đang xử lý lỗi DFF RW 3.3 của Evelyn Chevalier & Tsukishiro Yanagi). **Lab**: Bản gốc + 3 skin cảnh sát/SWAT/quân đội pilot. 👉 **Sau khi fix xong DFF RW 3.3 bên Clean, đưa sang Lab**. |
| 5 | `modloader\modloader.img` | `39,579,648 B` (`08cf57f2a91db14c`) | `2,396,160 B` (`382eb164aff6bf6c`) | **Clean**: Chứa 3 mục (`AETHER.dff`, `AETHER.txd`, và `loadscs.txd` 37.18 MB). **Lab**: Chỉ chứa 2 mục (`AETHER.dff`, `AETHER.txd`). 👉 **Chép cả `modloader\WibuWorldLoading\txd\loadscs.txd` và `modloader\modloader.img` từ Clean sang Lab**. |
| 6 | `data\default.dat` | `1,117 B` (`46893011f9be62cf`) | `1,212 B` (`dbb63801e574f500`) | **Lab**: Thêm 3 dòng mount `IMG CUSTOM\GROUP_A_MODS.IMG`, `GROUP_B1_TEXTURES.IMG`, `GROUP_B3_ASSETS.IMG` ở đầu file. 👉 **Giữ bản Lab**. |
| 7 | `data\gta.dat` | `23,664 B` (`bc5767dd9b7af9bc`) | `23,752 B` (`7c00712e4185c79e`) | **Lab**: Thêm 3 dòng mount `IPL CUSTOM\EHI.IPL`, `INTERIOR_DOORS.IPL`, `FORTCARSON_INTERIORS.IPL`. 👉 **Giữ bản Lab**. |
| 8 | `fastman92limitAdjuster_GTASA.ini` | `17,994 B` (`56b31a20bbf8e7c0`) | `17,994 B` (`15e1f52251f274b0`) | **Lab**: Nâng giới hạn `Entry exits` (dòng 118) từ `1000` lên `2500` để chứa thêm cửa nội thất EHI. 👉 **Giữ bản Lab**. |
| 9 | `hud.lua` | `21,414 B` (`0a02e906ce7b3f62`) | `90,712 B` (`2fea5b68bd585ef3`) | **Lab**: Giao diện in-game `EaglePhone OS v5.0` (10 ứng dụng, 23 texture Anime `ep_*`, GG Map, Bug Reporter). 👉 **Giữ bản Lab**. |
| 10 | `models\hud.txd` | `1,573,968 B` (`467cc14fc19ec12d`) | `4,034,640 B` (`e511ca72bd81e874`) | **Lab**: Giữ nguyên toàn bộ texture HUD gốc + đóng gói thêm 23 texture 32-bit BGRA `ep_*` cho EaglePhone v5.0. 👉 **Giữ bản Lab**. |
| 11 | `custom\custom_mods.ipl` | `83,524 B` (`0a4fa2eb6b5149e8`) | `84,054 B` (`79d2fccab86b7407`) | **Lab**: Thêm 5 tấm sàn collision `lacW_conc51` và 1 cửa `cc_malldoor1` vá lỗi rơi xuyên sàn tại Casino, Mall và căn hộ Nhà báo Carcer City. 👉 **Giữ bản Lab**. |
| 12 | `S&S\Interior\ccn_enex.IPL` | `3,295 B` (`2f1c2e1e74f0cc5a`) | `3,591 B` (`839642023a40922c`) | **Lab**: Sửa tọa độ/liên kết nội thất các cổng `ENEX` tại Carcer City (Casino `CC-cas` $\rightarrow$ `CASINO2`, Mall $\rightarrow$ `CLOTHGP`/`CSEXL`, Căn hộ Nhà báo `CC-jour` $\rightarrow$ `SVSFSM`). 👉 **Giữ bản Lab**. |
| 13 | `data\maps\country\countn2.ide` | `35,439 B` (`aa29bd7e83ebd7d2`) | `35,547 B` (`d6aa529316b2967f`) | **Lab**: Thêm flag `2097156` cho 27 object ngoại ô/sa mạc (phục vụ nội thất mở rộng Nhóm A). 👉 **Giữ bản Lab**. |
| 14 | `data\maps\country\counxref.ide` | `8,493 B` (`0afc45d5f6a0892d`) | `8,575 B` (`e40935b4c469517c`) | **Lab**: Thêm flag `2097156` cho 15 object ngoại ô (phục vụ nội thất mở rộng Nhóm A). 👉 **Giữ bản Lab**. |

---

## II. Các File Đã Sửa/Thêm, Tính Năng Đang Dùng Và Lỗi Còn Tồn Tại

### 1. Danh mục các file đã thêm/sửa trong `gta sa gameplay-lab`

#### A. Thư mục gốc (`gta sa gameplay-lab\`)
- [`Start_Eagle_Lab_With_Sidecar.bat`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/Start_Eagle_Lab_With_Sidecar.bat) (`541 B`): Script khởi chạy chuẩn (bật daemon `EagleCompanion.py`, mở Web UI Smartphone ở cổng `8765`, và chạy `gta_pe.exe`).
- [`EagleCompanion.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/EagleCompanion.py) (`220,995 B`): Tiến trình Sidecar Python 64-bit (`EaglePhone OS v5.0`). Bao gồm `GTAProcessBridge` đọc/ghi RAM mỗi `100ms`, máy chủ HTTP `127.0.0.1:8765`, xử lý phím tắt toàn cục (`F7`, `F11`, `F12`, `I/K/J/L`, `F9`, `Backspace`), vá RAM động `PECore.asi` để vẽ GPS khi đi bộ, và ghi state kép ra `cleo\EaglePhoneState_0.lua` / `_1.lua`.
- [`hud.lua`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/hud.lua) & [`hud_eaglephone.lua`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/hud_eaglephone.lua) (`90,712 B`): Script Lua thực thi bởi `SanViveLuaHudSA.asi`, vẽ màn hình Smartphone DirectX 9 ngay góc dưới bên phải trong game, nạp 23 texture Anime `ep_*` từ `models\hud.txd`.
- [`eagle_phone_ui.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_phone_ui.py) (`97,862 B`): Giao diện Web Smartphone/Tablet (`http://127.0.0.1:8765`) điều khiển bằng chuột, đồng bộ thời gian thực với HUD trong game.
- [`eagle_gg_map_pois.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_gg_map_pois.py) (`235,769 B`) & `world_pois.json` (`45,596 B`): Cơ sở dữ liệu **631 địa điểm POI** chia làm 10 danh mục khắp các bang của Project Eagle phục vụ ứng dụng **GG Map**.
- [`eagle_news_archive_2010_2025.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_news_archive_2010_2025.py) (`1,781,548 B` — hơn 18.700 dòng): Kho dữ liệu báo ngày hoài niệm **EagleTimes (2010–2025)** gồm 6 chuyên mục (Thế giới, Công nghệ/Đời sống mạng VN, Game/Wibu/Genshin, Phố Wall & Vàng, Crypto, Thể thao).
- [`eagle_map_inspector.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_map_inspector.py) (`49,075 B`): Engine chẩn đoán lỗi map tự động, lưu lịch sử tọa độ 5 giây trước khi rơi và xuất báo cáo ra [`docs\project-eagle\map-bug-reports.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/map-bug-reports.md).
- [`eagle_historical_data.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_historical_data.py) (`36,666 B`): Dữ liệu lịch sử giá Cổ phiếu/Vàng (2010–2020), Crypto (2017–2021), Lịch thi đấu & Tỷ lệ kèo 5 giải thể thao (`EagleBet`) và Xổ số (`EagleLotto`).
- [`build_eaglephone_txd.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/build_eaglephone_txd.py) (`20,807 B`) & thư mục `ui_assets\` (`24 files`): Bộ công cụ và ảnh nguồn PNG tạo 23 texture Anime `ep_*` cho `models\hud.txd` và `CUSTOM\EAGLEPHONE_UI.TXD`.
- `UltimFPC.SA.asi` (`2,248,192 B`), `imgui.ufpsa.ini` (`1,792 B`), `data.dat` (`1,672 B`): Plugin góc nhìn thứ nhất **Ultimate First Person (UltimateFP)** thuộc Nhóm A.
- `CLEO+.cleo` (`661,288 B`, đặt ở cả root và `cleo\CLEO+.cleo`): Plugin CLEO+ v1.2.0 đã vá tương thích với Fastman92 Limit Adjuster 7.7.

#### B. Thư mục `cleo\`, `CUSTOM\`, `modloader\`, `data\`, `S&S\`
- **`CUSTOM\`**:
  - `GROUP_A_MODS.IMG` (`433,260,544 B` = 413.19 MB): Chứa toàn bộ model/texture/collision của các gói mod Nhóm A (Enterable Hidden Interiors, Fort Carson Interiors, Commercial Mod, Street Art, Immersive Weapons...).
  - `GROUP_B1_TEXTURES.IMG` (`325,634,048 B` = 310.55 MB): Chứa 283 file `.txd` cửa hàng, biển hiệu và bảng quảng cáo thập niên 90 tại LS/SF/LV (đã lọc bỏ hoàn toàn mọi file đụng tới NPC skin).
  - `GROUP_B3_ASSETS.IMG` (`1,994,752 B` = 1.90 MB): Chứa 3 file animation `GasStation.ifp`, `PedEventsMod.ifp`, `StreetCL.ifp`.
  - `EAGLEPHONE_UI.TXD` (`2,460,672 B`): Bản đóng gói độc lập của 23 texture Anime `ep_*`.
  - `EHI.IPL`, `INTERIOR_DOORS.IPL`, `FORTCARSON_INTERIORS.IPL`: Các file IPL nội thất mở rộng được mount trong `data\gta.dat`.
  - `custom_mods.ipl`: Đã bổ sung 5 tấm sàn collision `lacW_conc51` (`ID 152915`) và 1 cửa `cc_malldoor1` (`ID 150275`) tại Carcer City.
- **`cleo\`** (887 files thêm mới):
  - [`EagleLifePoC.cs`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/cleo/EagleLifePoC.cs) (`156 B`): Script CLEO thuần 100% opcode chuẩn GTA SA, chỉ thực hiện gắn 4 icon radar/map tại Carcer City (Casino `icon 25`, Căn hộ Nhà báo `icon 31`, 2 tiệm quần áo khu Mall `icon 45`) rồi tự kết thúc thread (`0A93`).
  - `EagleMapIndex.cache` (`25,929,967 B`): Chỉ mục không gian đã biên dịch sẵn của `59,491` IDE models, `83,878` Text IPL inst, `62,839` Binary Stream IPL inst, `41,815` COL models và `1,099` cửa ENEX.
  - `EaglePhoneState_0.lua`, `EaglePhoneState_1.lua`, `EaglePhoneHUD.dat`, `EagleLifeState.ini`: Các file đồng bộ trạng thái giữa `EagleCompanion.py` và `hud.lua`.
  - 7 script đời sống Nhóm B3 đã gia cố **Zero-Shift On-Demand Streaming Trampoline** (`@LoadAssetsSub`): `ML_Constructions.cs`, `ML_Fisher.cs`, `ML_GasWorker.cs`, `ML_Homeless.cs`, `ML_LifeInSF.cs`, `ML_Mechanic.cs`, `ML_DinerInterior.cs`.
  - Hệ thống script Nhóm A: `EHI_Repatched.cs`, `on_off_engine.cs` (đã đổi phím tắt sang `J`/`L`), `Busy Pedestrians` (kèm `Busy Pedestrians.ini` đã sửa ID ped `208`/`265` $\rightarrow$ `71`/`253`), `Random Events`, `Ambient Taxi`, `Commercial Mod`, `Street Art`. *(Lưu ý: `cleo\gasoline.cs` và `models\txd\gasoline.txd` đã được gỡ bỏ hoàn toàn theo yêu cầu người dùng).*
- **`modloader\`**:
  - `GroupA_Audio\`: Chứa `GENRL` âm thanh súng đạn của `Immersive Weapons Pack`.
  - `GroupB1_LoadingThemes\`: Nhạc nền màn hình chờ thập niên 90 (`Bank_076`).
  - `RZL-Skin\`: Chứa `AETHER.dff` (`1,080,699 B`) và `AETHER.txd` (`1,312,067 B`) giống hệt bên `gta sa clean`.
- **Radio Custom (đã đồng bộ 100% ở cả `gta sa gameplay-lab` và `gta sa clean`)**:
  - `data\radio.dat` (`8,619 B`), `S&S\ZON\radio.zon` (`1,092 B` — đã khâu kín khe hở 150m giữa 8 bang về 0m Dead-Zone + vùng `RAD_global` `Region=9`), `models\txd\radio.txd` (`23,079,976 B`) và 14 file âm thanh trong `audio\PE\RADIO\` (`1.707 GB`, 13 đài hoạt động + 1 file phụ).

---

### 2. Các lỗi đã xử lý vs Lỗi/Vấn đề còn tồn tại

#### A. Các lỗi đã xử lý dứt điểm trong `gta sa gameplay-lab`
1. **Crash lúc khởi động tại `0x00000000` (`MODELS\FRONTEN2.TXD`)** $\rightarrow$ Đã sửa bằng cách dịch hook `CGame::Process` trong `CLEO+.cleo` từ `0x0053BF4E` về `0x0053BF49` để tránh bị FLA 7.7 ghi đè 5 byte NOP.
2. **Crash tại `0x40B30872` (`cleo\GlazedOfficeLift.s`)** $\rightarrow$ Đã sửa bằng cách dời 2 hook `CObject::Create` trong `CLEO+.cleo` vượt qua lệnh JMP 5 byte của FLA 7.7 (`0x005A1FA3` $\rightarrow$ `0x005A1FBC` và `0x005A2018` $\rightarrow$ `0x005A2031`).
3. **Đơ/treo cứng game giữa chừng do vòng lặp vô tận tìm đường (`CPathFind::DoPathSearch`)** $\rightarrow$ Đã vá nhị phân vĩnh viễn tại `0x00050E0A..0x00050F13` (`VA 0x00451A0A..0x00451B13`) trong `gta_pe.exe`.
4. **Crash khi chết và hồi sinh tại bệnh viện (`0x654BAC79 in $fastman92limitAdjuster.asi`, `cleo\PostMan.qa`)** $\rightarrow$ Đã sửa ID ped không tồn tại `208`/`265` trong `cleo\Busy Pedestrians.ini` thành `71`/`253`.
5. **Crash `0x00465F3F` (`eaglife` / `EagleLifePoC.cs`) khi thêm blip Casino** $\rightarrow$ Đã dọn bỏ đoạn bytecode `0x3200` dư tham số từ bản v3.0 trong `build_eagle_life_poc.py` và biên dịch lại `EagleLifePoC.cs` (`156 B`) thuần opcode chuẩn.
6. **Crash khi nạp texture Anime v5.0 trong `SanViveLuaHudSA.asi`** $\rightarrow$ Đã sửa hàm `RefreshEagleTextures()` trong `hud.lua` duyệt danh sách liên kết `RwLLLink` của `RwTexDictionary` từ `0x00BAB1FC` (`CHud::Sprites[0]`) để lấy đúng userdata `RwTexture*`.
7. **Rơi xuyên sàn tại Casino Carcer City (`BUG-004`) và Mall Carcer City** $\rightarrow$ Đã sửa `S&S\Interior\ccn_enex.IPL` và lót sàn collision trong `CUSTOM\custom_mods.ipl` (người dùng đã test và xác nhận hoạt động tốt).

#### B. Các lỗi / vấn đề còn tồn tại hiện nay
1. **Lỗi chọn địa điểm trên `GG Map` chưa được người dùng nghiệm thu lại trong game sau bản vá cuối**:
   - Ở lần test trước (tối 16/10), người dùng báo chọn địa điểm trên `GG Map` không hiện dấu mốc đỏ và sau đó EaglePhone bị liệt phím tắt khi agent khởi động lại daemon từ sandbox.
   - Agent đã sửa cả 2 nguyên nhân gốc trong [`EagleCompanion.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/EagleCompanion.py):
     1. Cập nhật địa chỉ đọc con trỏ mảng `CRadar::ms_RadarTrace` sau khi FLA 7.7 patch (`ADDR_FLA_TRACE_BASE_PATCH = 0x005838B2`, giới hạn `3000` tại `0x0058384E`) và vá RAM `PECore.asi + 0x000D0743` (`EB 45 90 90 90 90`) để vẽ đường GPS cả khi đang đi bộ.
     2. Thêm `_ensure_interactive_desktop()` (`OpenInputDesktop` + `SetThreadDesktop`) để luồng đọc phím không bị kẹt trong desktop ảo khi chạy từ terminal.
   - **Trạng thái**: Đã xác nhận qua ProcessBridge trên tiến trình đang chạy lúc đó, và có log chạy ngắn lúc `00:05 – 00:08 ngày 22/10/2026`, nhưng **chưa có phản hồi xác nhận chính thức từ người dùng** về đường kẻ GPS trên minimap.
2. **Mũi tên vàng `ENEX` vào căn hộ Nhà báo Carcer City (`BUG-003` / `BUG-005` tại `10582.6, 9899.64, 19.6`) chưa được người dùng test lại sau khi gắn**:
   - Ban đầu agent chỉ gắn cánh cửa tĩnh `cc_malldoor1` để che lỗ thủng mặt tiền nên người dùng hỏi *"cái cửa bạn gắn vào không đi vô được thì mình sẽ vô toà nhà đó như thế nào?"*.
   - Agent đã bổ sung cổng `ENEX` `CC-jour` tại `(10582.6, 9899.64, 19.6)` trong `S&S\Interior\ccn_enex.IPL` nối vào nội thất căn hộ `"SVSFSM"` và gắn blip ngôi nhà xanh (`icon 31`), nhưng người dùng chưa phản hồi kết quả bước vào cửa này.
3. **Các điểm khuyết collision rải rác khác của bản đồ mở rộng Project Eagle (ví dụ `BUG-002` tại `10794.84, 10255.07, 24.34` ở Carcer City)**:
   - Một số ô đất/vỉa hè của map Carcer City gốc bị hở mặt collision; người chơi hiện dùng phím `F11` (ghi nhận tọa độ) và `F12` (cứu hộ tức thì về 3 giây trước khi rơi) để xử lý khi bắt gặp.
4. **Lỗi crash lúc đóng game (`LdrShutdownProcess` tại `std.data.dll + 0x0016F6DD`)**:
   - Ghi nhận trong `ProjectEagle_crashes\2026-10-22_00-08-16.log`: chỉ xảy ra ở thời điểm Windows giải phóng DLL khi người chơi bấm thoát game (`Quit Game`), hoàn toàn không xảy ra trong khi đang chơi.
5. **Cảnh báo nhỏ trong `cleo.log`**:
   - `Loading of audiostream 'audio\pe\radio\static.mp3' failed. Error code: 8`: File tiếng rè chuyển đài `static.mp3` không có trong thư mục `audio\pe\radio\`, không ảnh hưởng đến việc phát 13 đài `.ogg` của RadioEx.
6. **Lỗi bên `gta sa clean` cần xử lý trước khi chép `COMPONENTPEDS.img` sang `gameplay-lab`**:
   - Hai skin Zenless Zone Zero (**Evelyn Chevalier** và **Tsukishiro Yanagi**) có header DFF RenderWare `3.3` làm crash game khi load/New Game bên `gta sa clean` (ghi nhận trong `ProjectEagle_crashes\2026-10-22_04-06-47.log` và `04-06-56.log`). Cần hoàn tất nâng version RW header lên $\ge 3.4$ (hoặc loại khỏi bản build `COMPONENTPEDS.img`) trước khi chép `COMPONENTPEDS.img` sang `gta sa gameplay-lab`.

---

## III. Chi Tiết Các Bản Vá Nhị Phân (`gta_pe.exe`, `PECore.asi`, `CLEO+.cleo`) Và Cấu Hình Loader

### 1. Bản vá trong `gta_pe.exe` và `gta_sa.exe`
- **File đích**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\gta_pe.exe` (`14,383,616 B`)
  - SHA-256 gốc (`clean` / `baseline`): `F115B49C5AC3A8FCEDB00EE216730B2A6F573AFE4908B2AC328A9CC2B9D0DCB3`
  - SHA-256 sau khi vá Isolation (`gta_sa.exe` hiện tại trong lab): `770170FE897EB23F339D608A1C9918D7740D2990B3434D43FAB02152C00EF7E6`
  - SHA-256 sau khi vá Isolation + `CPathFind::DoPathSearch` (`gta_pe.exe` hiện tại trong lab): `DDF6456C9A1173B179DB3CA67ACEF3F59E1A6FC8DDAA15737F5153BA545BD684`

#### Bảng Byte-Diff Chính Xác Của `gta_pe.exe`
| Nhóm bản vá | File Offset | Virtual Address (VA) | Độ dài | Bytes Gốc (`clean`) | Bytes Đã Vá (`gameplay-lab`) | Ý nghĩa kỹ thuật |
|---|---|---|---|---|---|---|
| **Isolation: User Files** | `0x00472FA8` | `0x00873BA8` | 28 B | `\GTA PE User Files\0...` | `\GTA PE Lab Files\0...` | Đổi chuỗi thư mục User Files trong `.rdata` của exe (lưu ý: `PECore.asi` vẫn hook về `Documents\Project Eagle User Files`, xem mục IV.2). |
| **Isolation: Window Title** | `0x0046BB88` | `0x0086C788` | 20 B | `GTA: Project Eagle\0\0` | `GTA: Eagle Lab\0\0\0\0\0\0` | Đổi tiêu đề cửa sổ game thành `GTA: Eagle Lab`. |
| **`CPathFind::DoPathSearch` (1/6)** | `0x00050E0A` | `0x00451A0A` | 6 B | `8D 9B 00 00 00 00` | `8B 6C 24 10 90 90` | Nạp `ebp = [esp+10h]` trước vòng lặp duyệt node đường. |
| **`CPathFind::DoPathSearch` (2/6)** | `0x00050E1F` | `0x00451A1F` | 6 B | `0F 86 E7 00 00 00` | `0F 86 F4 00 00 00` | Điều chỉnh đích nhảy `jbe` tới đoạn kiểm tra cờ thoát an toàn (`0x00451B19`). |
| **`CPathFind::DoPathSearch` (3/6)** | `0x00050E7E` | `0x00451A7E` | 8 B | `3B DF 8B 7C 24 3C 75 71` | `2B DF 8B 7C 24 3C EB 2E` | Thay `cmp ebx, edi; jne` bằng bộ đếm bước lùi `sub ebx, edi; jmp` tới trampoline kiểm tra giới hạn. |
| **`CPathFind::DoPathSearch` (4/6)** | `0x00050EB4` | `0x00451AB4` | 12 B | `8D A4 24 00 00 00 00 EB 03 8D 49 00` | `43 83 FB 02 77 3D EB CA 90 90 90 90` | `inc ebx; cmp ebx, 2; ja +0x3D; jmp -0x36`: Chặn đứng vòng lặp vô tận khi gặp cặp node đường bất đối xứng (`NODES1890.DAT`). |
| **`CPathFind::DoPathSearch` (5/6)** | `0x00050F08` | `0x00451B08` | 4 B | `8B 6C 24 10` | `84 F6 74 0D` | `test dh, dh; jz +0x0D`: Thoát sớm nếu không tìm thấy nhánh hợp lệ. |
| **`CPathFind::DoPathSearch` (6/6)** | `0x00050F13` | `0x00451B13` | 6 B | `0F 8C F7 FE FF FF` | `0F 8C F1 FE FF FF` | Điều chỉnh offset nhảy vòng lặp `jl` khớp với vị trí `0x00451A0A`. |

---

### 2. Trạng thái & Bản vá trong `PECore.asi` (Auf-Disk vs Runtime RAM)
- **So sánh file `PECore.asi` trên đĩa**:
  - Bản `gta sa gameplay-lab\PECore.asi`: `2,977,792 B`, SHA-256 `A81C69EF38B8DE8FC9CECEC2C1A38AF3DB6DA0A68D34C4BF4F3A175D0A65FFF7` (bản gốc ngày `01/07/2026`).
  - Bản `gta sa clean\PECore.asi`: `3,151,360 B`, SHA-256 `4C3B891061D773B095C52B4CD87A1C1FC1A5FBFD40533AF707046D929B861560` (bản đã cập nhật splash Wibu World ngày `14/10/2026`).
  - **Kết quả đối chiếu section**: Toàn bộ mã thực thi `.text`, `.data`, imports, exports và entry point của `PECore.asi` ở hai bản **giống hệt nhau 100%**. Bản `clean` chỉ khác ở:
    1. Chuỗi caption tại RVA `0x001D0A58` (`.rdata`): `"Project Eagle is loading"` $\rightarrow$ `"Project Wibu is loading\0"`.
    2. Section `.rsrc`: Thay resource `RCDATA` (Type `10`, Name `200`, Lang `1033`) bằng ảnh PNG 640×640 RGBA của Project Wibu (Hu Tao silhouette).
- **Bản vá RAM động (Runtime Memory Patch) trên `PECore.asi` trong `gta sa gameplay-lab`**:
  - Khi `EagleCompanion.py` chạy, hàm `_ensure_pecore_onfoot_gps_patch()` tự động tìm base address của module `PECore.asi` trong tiến trình `gta_pe.exe` và vá **6 bytes tại RVA `+0x000D0743`**:
    - **Bytes gốc**: `8B 81 8C 05 00 00` (`mov eax, [ecx+0x58C]` — kiểm tra con trỏ xe hiện tại của người chơi; nếu `NULL` tức đang đi bộ thì bỏ qua việc vẽ đường GPS).
    - **Bytes sau khi vá RAM**: `EB 45 90 90 90 90` (`jmp +0x45; nop*4` — nhảy qua khối kiểm tra phương tiện để `PECore.asi` luôn tính toán và vẽ vệt đường chỉ dẫn GPS trên radar ngay cả khi Aether đang đi bộ).
  - **Tương thích khi Merge**: Vì RVA `+0x000D0743` thuộc section `.text` không hề thay đổi trong bản `PECore.asi` của `gta sa clean`, **việc chép `PECore.asi` từ `clean` sang `gameplay-lab` sẽ giữ được cả màn hình splash Project Wibu lẫn tính năng vẽ GPS khi đi bộ của Lab**.

---

### 3. Bản vá trong `cleo\CLEO+.cleo` (Tương thích Fastman92 Limit Adjuster 7.7)
- **File đích**: `gta sa gameplay-lab\cleo\CLEO+.cleo` (và bản sao tại `gta sa gameplay-lab\CLEO+.cleo`), kích thước `661,288 B`.
- **SHA-256 gốc (CLEO+ v1.2.0 upstream)**: `FF4D164F13F2C6BE32D28C93C713EE4C7EE44065FE70EC972CF0B483CF5F642D`
- **SHA-256 sau khi vá**: `FA263672D0FEE89F102402B06E953E95A61ECC52B02D7DA350DD71F6D9150319`

| Vị trí vá | File Offset | Bytes Gốc | Bytes Đã Vá | Giải thích kỹ thuật |
|---|---|---|---|---|
| **1. `CGame::Process` Hook** | `0x0001C939` | `B9 4E BF 53 00` (`0x0053BF4E`) | `B9 49 BF 53 00` (`0x0053BF49`) | FLA 7.7 ghi đè 5 byte NOP tại `0x0053BF4E`. Lùi điểm đặt hook về `0x0053BF49` (`call Cickle::Update`) giúp cả FLA và CLEO+ cùng chạy. |
| **2. Null-Pointer Thunk Guard** | `0x00025B26` | `FF E0 CC CC CC CC CC` | `85 C0 74 02 FF E0 C3` | Thêm `test eax, eax; jz +2; jmp eax; ret` trong `injector::function_hooker` để tránh crash `0xC0000005` nếu con trỏ hàm gốc bị rỗng. |
| **3. `CObject::Create` Hook 1** | `0x000354B9` | `B9 A3 1F 5A 00` (`0x005A1FA3`) | `B9 BC 1F 5A 00` (`0x005A1FBC`) | Tránh lệnh `JMP` 5 byte của FLA 7.7 tại `0x005A1FA1` khi mở rộng giới hạn Object lên 70,000. |
| **4. `CObject::Create` Hook 2** | `0x00035FB9` | `B9 18 20 5A 00` (`0x005A2018`) | `B9 31 20 5A 00` (`0x005A2031`) | Tránh lệnh `JMP` 5 byte của FLA 7.7 tại `0x005A2016`. |

---

### 4. Bản vá Bytecode CLEO (`ML_*.cs` & `on_off_engine.cs`)
1. **`cleo\on_off_engine.cs`**:
   - Tại offset `0x4A`: đổi mã phím `0xBE` (dấu chấm `.`) thành `0x4A` (phím `J` bật/tắt động cơ xe, phím `L` bật/tắt đèn xe).
2. **`cleo\ML_Constructions.cs`, `ML_Fisher.cs`, `ML_GasWorker.cs`, `ML_Homeless.cs`, `ML_LifeInSF.cs`, `ML_Mechanic.cs`**:
   - Áp dụng kỹ thuật **Zero-Shift On-Demand Streaming Trampoline**: Giữ nguyên 100% độ dài và vị trí các nhãn nhảy cũ, chỉ thay lệnh `004D: goto_if_false` (7 bytes) ngay sau kiểm tra bán kính `00FE: locate_char_any_means_3d` bằng lệnh nhảy `0002: goto` tới đoạn mã `@LoadAssetsSub` nối thêm ở cuối file (EOF).
   - `@LoadAssetsSub` tự động gọi `0247: request_model`, `04ED: request_animation`, `038B: load_all_models_now` trước khi spawn NPC/sự kiện, chống crash khi streaming model bị thu hồi.
3. **`cleo\ML_DinerInterior.cs`**:
   - Cắt bỏ `17,540 bytes` bảng debug symbol `VAR` thừa ở cuối file `Diner.csa`, giữ lại đúng `28 bytes` bytecode thực thi sạch.

---

### 5. Cấu hình Loader & Thứ tự Mount
1. **`modloader\modloader.ini`**:
   - `Profile = Default`, `IgnoreAllMods = false`, `ExcludeAllMods = false`.
   - Trong kiến trúc của Project Eagle, plugin `gta3.std.stream` của ModLoader không dùng để stream đè các archive lớn của `S&S\`; thay vào đó ModLoader nạp `modloader\modloader.img` (được khai báo trong `data\default.dat`), âm thanh (`GroupA_Audio`, `GroupB1_LoadingThemes` qua `gta3.std.bank`) và texture hiệu ứng/màn hình chờ (`WibuWorldLoading\txd\loadscs.txd` qua `gta3.std.fx`).
   - **Lưu ý quan trọng về `modloader\modloader.img`**:
     - Trong `gta sa gameplay-lab\modloader\modloader.img` (`2,396,160 B`): hiện chỉ chứa 2 entry `AETHER.dff` và `AETHER.txd`.
     - Trong `gta sa clean\modloader\modloader.img` (`39,579,648 B`): chứa 3 entry `AETHER.dff`, `AETHER.txd` và `loadscs.txd` (`37,183,488 B`).
2. **`data\default.dat`** (trong `gta sa gameplay-lab`):
   - Đã chèn 3 dòng mount IMG ở ngay đầu file (trước `CUSTOM\CUSTOM_MODS.IMG` và `MODLOADER\MODLOADER.IMG`):
     ```text
     IMG CUSTOM\GROUP_A_MODS.IMG
     IMG CUSTOM\GROUP_B1_TEXTURES.IMG
     IMG CUSTOM\GROUP_B3_ASSETS.IMG
     ```
3. **`data\gta.dat`** (trong `gta sa gameplay-lab`):
   - Đã chèn 3 dòng mount IPL ngay sau `IPL CUSTOM\CUSTOM_MODS.ipl`:
     ```text
     IPL CUSTOM\EHI.IPL
     IPL CUSTOM\INTERIOR_DOORS.IPL
     IPL CUSTOM\FORTCARSON_INTERIORS.IPL
     ```
4. **`fastman92limitAdjuster_GTASA.ini`** (trong `gta sa gameplay-lab`):
   - Dòng 118: `Entry exits = 2500` (bản `clean` là `1000`).
   - `Radar traces = 3000`: FLA 7.7 cấp phát lại mảng `CRadar::ms_RadarTrace` và ghi địa chỉ mảng mới vào lệnh assembly tại `0x005838B2` (được `EagleCompanion.py` đọc động để cắm mốc GPS `GG Map`).
5. **`SanViveLuaHudSA.asi`**:
   - Nạp và thực thi trực tiếp `hud.lua` ở thư mục gốc của game; cung cấp binding C++ `sol2` (`Sprite.UseTexture`, `Sprite.RenderOneXLUSprite`, `Sprite2d.DrawRect`, `Sprite2d.DrawLine`, `Memory.GetInt`...).

---

## IV. Cách Khởi Động, Phụ Thuộc Đường Dẫn Và Vị Trí Backup/Rollback

### 1. Cách khởi động chuẩn
Chạy trực tiếp file batch tại thư mục gốc của Lab:
```text
C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\Start_Eagle_Lab_With_Sidecar.bat
```
File `.bat` này thực hiện tuần tự:
1. `cd /d "%~dp0"` (đưa working directory về đúng thư mục `gta sa gameplay-lab`).
2. Khởi chạy ngầm tiến trình `python EagleCompanion.py` (cửa sổ thu nhỏ `EaglePhone Sidecar`).
3. Đợi 2 giây rồi mở giao diện Web Smartphone (`http://127.0.0.1:8765`) bằng Microsoft Edge ở chế độ `--app` kích thước `450x890`.
4. Khởi chạy `gta_pe.exe`.

---

### 2. Phụ thuộc đường dẫn (Path Dependencies & NTFS Junctions) — CỰC KỲ QUAN TRỌNG KHI MERGE / ĐỔI TÊN THƯ MỤC

1. **10 NTFS Directory Junctions ngay tại thư mục gốc `gta sa gameplay-lab\`**:
   Do một số script CLEO trong Nhóm A (`Busy Pedestrians`, `Random Events`, `Commercial Mod`, `Street Art`) truy cập tài nguyên theo đường dẫn tương đối từ thư mục gốc trong khi CLEO 5 đặt thư mục làm việc tại `cleo\`, trình cài đặt `install_group_a_mods.py` đã tạo **10 NTFS Junctions** ở thư mục gốc trỏ vào `cleo\`:
   - `gta sa gameplay-lab\Art Sound` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\Art Sound`
   - `gta sa gameplay-lab\GM` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\GM`
   - `gta sa gameplay-lab\M` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\M`
   - `gta sa gameplay-lab\ModelsQ` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\ModelsQ`
   - `gta sa gameplay-lab\ModelsQa` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\ModelsQa`
   - `gta sa gameplay-lab\ModelsQWD` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\ModelsQWD`
   - `gta sa gameplay-lab\QA` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\QA`
   - `gta sa gameplay-lab\Sound` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\Sound`
   - `gta sa gameplay-lab\SQ` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\SQ`
   - `gta sa gameplay-lab\V` $\rightarrow$ `\\?\C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\cleo\V`
   > ⚠️ **Lưu ý sống còn**: NTFS Junction lưu đường dẫn đích tuyệt đối. Nếu giữ nguyên đường dẫn `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` thì không cần làm gì cả. Nhưng nếu sau này đổi tên hoặc di chuyển thư mục `gta sa gameplay-lab` sang đường dẫn khác, **phải tạo lại 10 junction này** trỏ vào `<thư_mục_mới>\cleo\<Tên>` (hoặc copy thật các thư mục đó ra root).

2. **2 NTFS Directory Junctions của công cụ `Eagle Radio Studio`**:
   - `C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio\data\backups` $\rightarrow$ `D:\GTA Archive\Eagle Radio Studio\backups`
   - `C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio\data\cache` $\rightarrow$ `D:\GTA Archive\Eagle Radio Studio\cache`
   - Cần giữ ổ `D:` kết nối khi mở Eagle Radio Studio (`Start_Eagle_Radio_Studio.bat`).

3. **Đường dẫn thư mục Save Game thực tế (`Documents\Project Eagle User Files`)**:
   - Mặc dù `gta_pe.exe` của Lab đã được vá chuỗi `\GTA PE Lab Files` tại `0x00472FA8`, module `SaveSideloader` trong `PECore.asi` hook hàm khởi tạo thư mục người dùng và luôn điều hướng về:
     ```text
     C:\Users\LENOVO\Documents\Project Eagle User Files
     ```
   - Đây là nơi lưu `GTAPEsf1..8.b`, `PECoreSaveData1..8.dat`, `RepairGTASaveExtender1..8.dat` và `gta_pe.set` cho cả `clean` và `gameplay-lab`.
   - Trong khi đó, dữ liệu tài khoản ngân hàng, danh mục cổ phiếu/crypto, vé số và cài đặt giao diện của `EaglePhone OS v5.0` được lưu hoàn toàn độc lập bên trong thư mục lab tại:
     - `gta sa gameplay-lab\cleo\EaglePhoneHUD.dat`
     - `gta sa gameplay-lab\cleo\EaglePhoneState_0.lua` & `EaglePhoneState_1.lua`
     - `gta sa gameplay-lab\cleo\EagleLifeState.ini`

4. **Các script Python trong Lab (`EagleCompanion.py`, `eagle_map_inspector.py`, `eagle_phone_ui.py`)**:
   - Sử dụng 100% đường dẫn tương đối qua `Path(__file__).resolve().parent`.
   - Riêng `eagle_map_inspector.py` xuất báo cáo bug map ra `self.game_dir.parent.parent / "docs" / "project-eagle"` (tức `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\map-bug-reports.md` & `.json`).
   - File `Rollback_EagleLife_PoC.bat` có 1 đường dẫn tuyệt đối trỏ về `C:\Users\LENOVO\Desktop\GTA\backups\project-eagle\gameplay-lab-baseline\hud.lua`.

---

### 3. Sổ cái toàn bộ vị trí Backup và Script Rollback

| Hạng mục / Tầng | Vị trí chứa file Backup & Manifest | Script Rollback / Khôi phục | Phạm vi bảo vệ |
|---|---|---|---|
| **Baseline gốc của Lab** | `C:\Users\LENOVO\Desktop\GTA\backups\project-eagle\gameplay-lab-baseline\`<br>(`gta_pe.exe` gốc, `gta_sa.exe` gốc, `hud.lua` gốc `21,414 B`) | `gta sa gameplay-lab\Rollback_EagleLife_PoC.bat` | Khôi phục `gta_pe.exe`, `gta_sa.exe`, `hud.lua` về trạng thái nguyên bản trước khi lập Lab. |
| **Texture HUD gốc (`models\hud.txd`)** | `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\backups\hud.txd.bak` (`1,573,968 B`, SHA-256 `467cc14fc19ec12d...`) | Copy đè `hud.txd.bak` về `gta sa gameplay-lab\models\hud.txd` | Khôi phục `models\hud.txd` trước khi nhúng 23 texture Anime `ep_*` của EaglePhone v5.0. |
| **Gói Mod Nhóm A (Interiors, Busy Peds, Weapons, UltimateFP)** | `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\backups\group_a_backup\`<br>& `group_a_manifest.json` | `python C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\rollback_group_a_mods.py` | Gỡ sạch 976 file Nhóm A, 10 junctions và trả lại 7 file gốc (`default.dat`, `gta.dat`, `countn2.ide`, `counxref.ide`, `fastman92limitAdjuster_GTASA.ini`, `gta_pe.exe`, `Picture.dff`). |
| **Gói Mod Nhóm B1 (283 Textures 90s + Loading Themes + Patch `CPathFind`)** | `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\backups\group_b1_backup\`<br>& `group_b1_manifest.json` | `python C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\rollback_group_b1_mods.py` | Gỡ `CUSTOM\GROUP_B1_TEXTURES.IMG`, `modloader\GroupB1_LoadingThemes` và trả lại `data\default.dat` trước B1. |
| **Gói Mod Nhóm B3 (3 IFPs + 7 CLEO `ML_*.cs` Trampoline)** | `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\backups\group_b3_backup\`<br>& `group_b3_manifest.json` | `python C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\gameplay-lab-poc\rollback_group_b3_mods.py` | Gỡ `CUSTOM\GROUP_B3_ASSETS.IMG`, 7 file `cleo\ML_*.cs` và trả lại `data\default.dat` trước B3. |
| **Bản vá Map Carcer City (`ccn_enex.IPL` & `custom_mods.ipl`)** | `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\map-bug-fixes-backup\`<br>(`ccn_enex.IPL.bak`, `custom_mods.ipl.bak`) | Copy 2 file `.bak` về `S&S\Interior\ccn_enex.IPL` và `CUSTOM\custom_mods.ipl` | Khôi phục trạng thái IPL trước khi vá lỗi rơi sàn Casino, Mall và căn hộ Nhà báo Carcer City. |
| **Loading Screen Wibu World & `PECore.asi` (bên `clean`)** | `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-screens\implementation\pecore\backup\PECore-source.asi` & `backup\LOADSCS.original.txd` | `staging\project-eagle\loading-screens\implementation\scripts\rollback_wibu.ps1` | Khôi phục `PECore.asi` và `loadscs.txd` có kiểm tra guard hash. |
| **Radio Studio Snapshots (7 bản Lab + 6 bản Main)** | `C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio\data\backups\` (junction tới `D:\GTA Archive\Eagle Radio Studio\backups`) | Khôi phục trực tiếp trên giao diện Web `Eagle Radio Studio` (`:8790`) | Khôi phục `data\radio.dat`, `S&S\ZON\radio.zon`, `models\txd\radio.txd` và `audio\PE\RADIO\`. |

---

## V. Phân Định Rõ: Phần Đã Test Trong Game vs Phần Chưa Test

Tuân thủ quy tắc tách bạch bằng chứng trong `AGENTS.md`, bảng dưới đây phân loại chính xác từng thành phần theo 3 mức độ: **(1) Đã được người dùng mở game test và xác nhận**, **(2) Đã chạy trong tiến trình game / kiểm tra qua ProcessBridge & log runtime**, và **(3) Chưa được nghiệm thu thực tế trong game**:

### 1. Đã được người dùng kiểm thử thực tế trong game (User Tested In-Game)
- **Khởi động & Vận hành chung qua `Start_Eagle_Lab_With_Sidecar.bat`**: Đã mở chơi nhiều phiên từ 14/10 đến 22/10/2026 (phiên gần nhất ghi nhận trong log là `22/10/2026 00:05:17 – 00:08:32`).
- **Bản vá chống treo `CPathFind::DoPathSearch` trong `gta_pe.exe` và `CLEO+.cleo`**: Đã được người dùng xác nhận trực tiếp lúc đang chơi (*"what have you done, the game unstuck itself without im doing anything"*, *"oke giờ thì game đang chạy ổn"*).
- **Gói Mod Nhóm A, Nhóm B1, Nhóm B3**:
  - Đã test dạo phố, sự kiện đường phố, nội thất mở rộng.
  - Đã test chết và hồi sinh tại bệnh viện sau khi sửa ID ped `71`/`253` trong `Busy Pedestrians.ini` (xác nhận hết crash).
  - Đã test lái xe sau khi gỡ `gasoline.cs` (xác nhận không còn bị hết xăng giữa đường;総 thể MVP được người dùng xác nhận: *"oke tôi test ổn, phase mvp cho tới giờ là tạm ổn"*).
- **Hệ thống Điện thoại `EaglePhone OS` (In-Game HUD `hud.lua` & Web UI `:8765`)**:
  - Đã test đồng bộ tiền mặt & máu thời gian thực (sau khi sửa lỗi nhấp nháy bằng cơ chế đệm kép `EaglePhoneState_0/1.lua`).
  - Đã test giao diện Anime Home Screen v5.0 (hình nền Furina/Raiden/Hu Tao, mascot chibi, lưới icon ứng dụng).
  - Đã test App Chứng khoán/Crypto, Cá cược thể thao `EagleBet`, và Xổ số `EagleLotto` (đã tách riêng trang XSKT 16:30 và Vietlott 6/45, 6/55 18:00 theo phản hồi sau khi test của người dùng).
- **Hệ thống Báo Bug Map (`F11`) & Cứu hộ tức thì (`F12`)**:
  - Người dùng đã trực tiếp dùng `F11` trong game để log `BUG-002`, `BUG-003`, `BUG-004`, `BUG-005` tại Carcer City.
- **Bản vá sàn và cửa vào Casino Carcer City (`BUG-004`)**:
  - Người dùng đã tự vào lại Casino trong game và xác nhận: *"casino fix ngon luôn"*.
- **Hệ thống 13 Đài Radio Custom (`RadioEx` + `S&S\ZON\radio.zon` khâu kín 0m Dead-Zone + `RAD_global`)**:
  - Người dùng đã test lái xe nghe thử ở Los Santos và Carcer City, phát hiện lỗi mất tiếng ở ranh giới bang và file nhạc lỗi `Surging Reminiscence.mp3`; sau khi vá `radio.zon` và thay file nhạc, bộ 13 đài đã được build đồng bộ vào cả 2 bản.

### 2. Đã xác minh qua ProcessBridge / Log Runtime nhưng chờ người dùng xác nhận lại trong game
- **Tính năng cắm mốc đỏ Waypoint (`T`) & vẽ đường GPS của ứng dụng `10.GG Map`**:
  - Người dùng đã mở `GG Map` trong game và xác nhận danh sách địa điểm hiển thị ổn (*"danh sách địa điểm hiển thị khá là oke"*), nhưng ở lần thử đầu tiên bấm chọn địa điểm chưa lên đường GPS (do FLA 7.7 dời con trỏ `ms_RadarTrace` sang `0x005838B2` và `PECore.asi` chặn vẽ GPS khi đi bộ) và sau đó bị kẹt phím do desktop ảo của terminal sandbox.
  - Agent đã sửa cả 3 điểm (`0x005838B2`, patch RAM `PECore.asi + 0x000D0743`, và `_ensure_interactive_desktop()`) rồi kiểm tra trực tiếp trên tiến trình `PID 22916` đang mở của người dùng. Tuy nhiên người dùng chưa gửi phản hồi nghiệm thu cuối cùng cho thao tác dẫn đường GPS sau khi sửa.
- **4 Icon bản đồ mới tại Carcer City (`EagleLifePoC.cs` 156B) & Cổng `ENEX` vào căn hộ Nhà báo (`BUG-003` / `BUG-005`)**:
  - Trong phiên chạy lúc `00:05:17 ngày 22/10/2026`, `cleo.log` xác nhận `EagleLifePoC.cs` (156B) đã nạp và thực thi sạch sẽ không còn lỗi crash `0x00465F3F`. Tuy nhiên chưa có phản hồi của người dùng xác nhận đã bước thử vào mũi tên vàng `CC-jour` (nội thất `"SVSFSM"`) trước cửa căn hộ Nhà báo.

### 3. Mới kiểm tra bằng Script / Offline (Chưa kiểm thử sâu trong game)
- **Kho tin tức `EagleTimes 2010–2025` (`eagle_news_archive_2010_2025.py` — 18.700+ dòng)**:
  - Đã kiểm tra nạp module Python, cấu trúc dữ liệu 16 năm × 6 chuyên mục và hiển thị trên UI, nhưng người dùng chưa chơi qua nhiều ngày/năm trong game để đọc thử toàn bộ các giai đoạn.
- **Độ ổn định dài hạn của 7 script Nhóm B3 (`ML_*.cs` với `@LoadAssetsSub` trampoline)**:
  - Đã xác nhận nạp sạch qua `cleo.log` trong các phiên mở game, nhưng chưa có bài kiểm thử di chuyển tốc độ cao liên tục qua cả 7 điểm sự kiện ở LS/SF trong một phiên chơi kéo dài.

---

## VI. Hướng Dẫn Kỹ Thuật Cho Agent Thực Hiện Merge (`gta sa clean` $\rightarrow$ `gta sa gameplay-lab`)

Như đã phân tích ở Mục I, **`gta sa gameplay-lab` chứa toàn bộ bản vá nhị phân (`gta_pe.exe`, `CLEO+.cleo`), cấu hình loader (`default.dat`, `gta.dat`, `fastman92limitAdjuster_GTASA.ini`), 10 NTFS junctions và 1,768 file hệ thống gameplay**, trong khi **`gta sa clean` chỉ có đúng 3 thành phần nội dung mới cần đưa sang Lab**:

1. **Bước 1 — Đưa Loading Screen & Startup Splash Project Wibu từ `clean` sang `gameplay-lab`**:
   - Copy `modloader\WibuWorldLoading\txd\loadscs.txd` (`37,181,768 B`) từ `clean` sang `gta sa gameplay-lab\modloader\WibuWorldLoading\txd\loadscs.txd`.
   - Copy `modloader\modloader.img` (`39,579,648 B` — đã có sẵn cả `AETHER.dff`, `AETHER.txd` và `loadscs.txd`) từ `clean` sang `gta sa gameplay-lab\modloader\modloader.img` (sao lưu bản 2.40 MB cũ của Lab trước khi ghi đè).
   - Copy `PECore.asi` (`3,151,360 B`, SHA-256 `4C3B891061D773B0...`) từ `clean` sang `gta sa gameplay-lab\PECore.asi` (sao lưu bản `2,977,792 B` của Lab trước khi ghi đè). *Do section `.text` của 2 bản `PECore.asi` giống hệt nhau 100%, bản vá RAM động tại RVA `+0x000D0743` của `EagleCompanion.py` hoàn toàn tương thích.*
2. **Bước 2 — Đưa dàn Skin NPC (`COMPONENTPEDS.img`) từ `clean` sang `gameplay-lab`**:
   - **Điều kiện tiên quyết**: Phải sửa xong lỗi DFF RenderWare 3.3 của 2 skin **Evelyn Chevalier** và **Tsukishiro Yanagi** bên `clean` (đảm bảo `clean` vào New Game / Load Game không còn crash như log `04:06:47` & `04:06:56`).
   - Sau khi `COMPONENTPEDS.img` bên `clean` đã ổn định, copy (hoặc hardlink/di chuyển để tiết kiệm 11.9 GiB ổ C) sang `gta sa gameplay-lab\S&S\Cdimages\default\COMPONENTPEDS.img`.
   - *Lưu ý*: Các gói mod Nhóm A, B1, B3 trong `gameplay-lab` hoàn toàn không chứa bất kỳ model ped nào và `peds.ide` giữa 2 bản giống hệt nhau 100% (`95,709 B`), nên không có bất kỳ xung đột ID hay texture nào với `COMPONENTPEDS.img`.
3. **Bước 3 — Tuyệt đối KHÔNG ghi đè 11 file cấu hình/binary riêng của `gameplay-lab`**:
   - Không được lấy bản của `clean` đè lên các file sau trong `gameplay-lab`:
     1. `gta_pe.exe` & `gta_sa.exe`
     2. `cleo\CLEO+.cleo` & `CLEO+.cleo`
     3. `data\default.dat`
     4. `data\gta.dat`
     5. `fastman92limitAdjuster_GTASA.ini`
     6. `hud.lua`
     7. `models\hud.txd`
     8. `custom\custom_mods.ipl`
     9. `S&S\Interior\ccn_enex.IPL`
     10. `data\maps\country\countn2.ide` & `counxref.ide`
     11. 10 NTFS Directory Junctions tại thư mục gốc của `gta sa gameplay-lab`.
