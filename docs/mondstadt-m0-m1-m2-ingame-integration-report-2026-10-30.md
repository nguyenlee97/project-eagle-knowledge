# Báo cáo Tích hợp & Nghiệm thu In-Game Quần thể Mondstadt (`Sector M0 + Sector M1 + Sector M2`) — Project Eagle (`gameplay-lab`)

- **Ngày thực hiện**: `2026-10-30` (hoàn tất nghiệm thu `2026-10-31`)
- **Agent thực hiện**: `antigravity`
- **Phiếu công việc**: `docs/project-eagle/work-items/2026-10-30-mondstadt-m0-m1-m2-ingame-integration.md`
- **Đích triển khai**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & Backup**: `D:\GTA Archive\Staging\mondstadt-ingame-integration-2026-10-30\`
- **Script phục hồi khẩn cấp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\Rollback_Mondstadt_Integration.bat`
- **Trạng thái nghiệm thu tổng thể**: **`100% PASS` (`eagle_doctor.py` `11/11 PASS`, Route Crawlers `4/4` Suites / `12/12` Segments `PASS`, Enterable Interiors `7/7 PASS`, Contact Sheet Ngày `8/8 PASS` & Đêm `8/8 PASS`, Aether 6-Step Rig Test `6/6 PASS`)**

---

## 1. Tổng quan Kiến trúc & Định vị Thế giới (`MONDSTADT_GTA_ANCHOR`)

Toàn bộ quần thể Mondstadt (`Sector M0` Thành Mondstadt + `Sector M1` Vùng Hoang Dã & 24 Cụm Địa danh + `Sector M2` Bờ Đông, Bán đảo Đông-Nam, Đảo Musk Reef & Đại Cầu Vượt Biển Trung Tâm) đã được đóng gói sạch và tích hợp đồng bộ vào `gameplay-lab`:

- **Tâm định vị Thế giới (`MONDSTADT_GTA_ANCHOR`)**:
  - Tâm Thành Mondstadt (`ENU = 0, 0, 0`): **`(-6500.0, -3500.0, +59.5)`** trên vùng biển phía Tây (`West Continent`).
  - Công thức chuyển đổi tọa độ ngoài trời (`Area Code = 0`):
    $$X_{\text{gta}} = E - 6500.0,\quad Y_{\text{gta}} = N - 3500.0,\quad Z_{\text{gta}} = U + 59.5$$
  - Phạm vi bao phủ: $X_{\text{gta}} \in [-7268.0, -4452.0]$ (cùng Đại Cầu Vượt Biển Trung Tâm nối về bờ Tây Whetstone tại $X_{\text{gta}} = -2544.0, Y_{\text{gta}} = -2698.0$), $Y_{\text{gta}} \in [-4780.0, -2698.0]$, hoàn toàn tách biệt với đất liền San Andreas và các đảo custom hiện có.
- **Hệ thống 7 Nội thất Bước vào được (`INT-01..INT-07`)**:
  - Đặt tại **`Area Code = 1`, `Z = +1500.0m`**, kết nối hai chiều với cửa ngoài trời (`Area Code = 0`) qua các cặp marker `enex` trong `.IPL`.

| Gói Tích hợp (`CUSTOM\`) | Dải Model ID | Số đối tượng `.IDE` | Số thực thể `.IPL` (`inst` + `enex`) | Số mục `.COL3` (Tổng mặt va chạm) | Dung lượng `.IMG` |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **`mondstadt_m0_city.*`** (`Sector M0` Thành Mondstadt) | `6710..6726` | `17` (`9` Near + `8` LOD) | `17` `inst` | `9` mục (`130,361` faces) | `72.73 MB` |
| **`mondstadt_m1_wilds.*`** (`Sector M1` Phase 1 + Phase 2 + `INT-01..06`) | `6680..6701`, `6730..6859` | `150` (`84` Near + `66` LOD) | `219` `inst` + `12` `enex` | `84` mục (`65,114` faces) | `26.86 MB` |
| **`mondstadt_m2_east.*`** (`Sector M2` Bờ Đông + `Route 13..21` + Đại Cầu Vượt Biển + `INT-07`) | `11960..12152` | `191` (`107` Near + `84` LOD) | `248` `inst` + `2` `enex` | `107` mục (`76,598` faces) | `38.68 MB` |
| **TỔNG CỘNG** | **358 IDs** (`0` trùng lặp) | **358 models** | **484 `inst` + 14 `enex`** | **200 `.COL3` (`272,073` faces)** | **138.27 MB** |

> **Bảo toàn tuyệt đối `VegasN.ide`**: Dải `6863..6889` của `DATA\MAPS\vegas\VegasN.ide` hoàn toàn không bị chạm tới (`Sector M1` dừng ở `6859` và dùng `6680..6701` cho 16 Mob/NPC/Rương + 6 Nội thất `INT-01..INT-06`).

---

## 2. Kiểm toán Nhị phân `.COL3`, Ánh sáng Ngày/Đêm & Cờ Render (Bài học #10–#22)

1. **Chuẩn hóa `.COL3` (`200 / 200` mục đạt `100% PASS`)**:
   - Mọi entry `.COL3` đều có `body_sz >= 0x58 (88)` và `offsetVertices == 0x74 (116)` (`0` mục rỗng/LOD trong `.COL`).
   - Kích thước entry `.COL3` lớn nhất: **`56,540 B`** (`< 92,768 B` — dưới ngưỡng tràn signed 16-bit sector của `fastman92 Limit Adjuster`).
   - Bán kính đỉnh `int16 / 128.0`: cực đại **`220.00m`** (`< ±255.0m`, `0` đỉnh bị kẹp thầm). Toàn bộ các tuyến đường dài (`Route 18`, `Route 19`, `Route 21`) đã được chia đôi `Part A / Part B` an toàn.
   - Tệp `.col` được đặt đồng thời tại `CUSTOM\*.col` (nạp qua lệnh `COLFILE` trong `data\gta.dat`) **và** nhúng trực tiếp vào bên trong `CUSTOM\*.img` để `CStreaming` luôn tìm thấy dữ liệu va chạm.
2. **Ánh sáng mặt va chạm & Vertex Prelight Ngày/Đêm**:
   - Toàn bộ **`272,073 / 272,073` mặt `TColFace`** trong cả 3 tệp `.col` đều được đặt `light = 0xFF` (`day=15, night=15`), giúp nhân vật chính Aether, NPC và phương tiện đứng trên đất/đường Mondstadt luôn nhận đủ ánh sáng môi trường.
   - Toàn bộ `.DFF` đều bật `rpGEOMETRYPRELIT (0x08)` kèm chunk `ExtraVertColour (0x0253F2F9)` (Day RGBA ấm áp + Night RGBA dịu mắt + ấm cam quanh đèn đường/cửa sổ), `RpMaterial.color = (255, 255, 255, 255)` (`ambient = 1.0, diffuse = 1.0`).
   - Toàn bộ khối địa hình, mặt đường và công trình đặc trong `.IDE` dùng cờ `flags = 0` (**`0` đối tượng địa hình/đường bộ dùng cờ `4 (DRAW_LAST)`**), triệt tiêu hoàn toàn lỗi Z-buffer X-ray xuyên thấu.

---

## 3. Bản đồ Minimap 2D (`radar.img`), Nước Bơi được (`water.dat`), AI Path (`paths.img`) & GPS (`pecore_gps_graph.pegg`)

1. **Minimap 2D (`S&S\Cdimages\default\radar.img`)**:
   - Kết xuất **`44` mảnh `radar*.txd`** (`c = 33..39, r = 53..57` và `c = 40..42, r = 53..55`) theo kỹ thuật `2x` supersampling (`512×512 -> 256×256` Lanczos, nén `DXT1` qua `texconv.exe`).
   - Đóng gói chuẩn khung nhị phân `34,816 B` của `radar00.txd`:
     - `rw_version = 0x1803FFFF` tại cả 6 offset (`0x08, 0x14, 0x24, 0x30, 0x8098, 0x80A4`).
     - Tên texture nội bộ (`32` byte null-padded ASCII) tại **`0x3C..0x5C`**.
     - Header `DXT1` (`0x7C..0x90`: `rasterFormat=0x200`, `"DXT1"`, `256×256`, `depth=16`, `dataSize=0x8000`) và dữ liệu điểm ảnh `32,768 B` tại **`0x90..0x8090`**.
2. **Hệ thống Nước Bơi được (`data\water.dat`)**:
   - Tách ô đại dương phía Tây thành 3 ô bao ngoài và bổ sung 3 vùng nước Mondstadt không chồng lấn:
     - **Hồ Cider (`Cider Lake`)**: `[-6860..-6120] × [-3820..-3160]` tại **`Z_gta = +1.50m`** (`U = -58.0m`).
     - **Hồ Tinh Lạc (`Starfell Lake`)**: `[-6185..-6080] × [-3015..-2920]` tại **`Z_gta = +39.20m`** (`U = -20.3m`).
     - **Mặt biển Bờ Đông `M2` & Đảo Musk Reef**: `[-5420..-4400] × [-4780..-2732]` tại **`Z_gta = 0.00m`**.
3. **AI Giao thông & Người đi bộ (`S&S\Cdimages\default\paths.img`)**:
   - Biên dịch **`14` sector `FLA4`** (`1,039` nút xe cộ + `793` nút người đi bộ) phủ toàn bộ mạng lưới 21 tuyến đường `M0 + M1 + M2` và Đại Cầu Vượt Biển Trung Tâm nối vào nút gốc `node_id = 35` của `nodes14.dat` (Whetstone).
   - Tuân thủ đầy đủ quy tắc `FLA4`: `area_id` nhúng ở cả 5 bảng con (`nodes, navi, links, link_lengths, path_intersection_flags`), cờ `0x0800 (val1) / 0x0900 (val2)`, `speedLimit = 0`, và mọi sector trống đều có footer `b"EOF\x00"` tại offset `28 (0x1C)`.
4. **Đồ thị Dẫn đường GPS (`data\pecore_gps_graph.pegg`) & Menu Dịch chuyển (`EaglePhone / Companion`)**:
   - Mở rộng `data\pecore_gps_graph.pegg` thêm **`+1,038` nút** và **`+2,108` cạnh hai chiều** (`navi_idx = 0xFFFFFFFF`), nâng tổng đồ thị lên **`148,417` nút / `252,646` cạnh** (`28,199,440 B`).
   - Đăng ký **`57` tọa độ Dịch chuyển (`MONDSTADT_CAMPAIGN_POIS`)** vào `CURATED_GG_MAP_POIS` trong [eagle_gg_map_pois.py](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_gg_map_pois.py) và tái tạo `cleo\EagleMapIndex.cache` (`526` mounts, `0` missing).

---

## 4. Kết quả Nghiệm thu Offline & In-Game (`100% PASS`)

### 4.1. Kiểm tra Offline Pre-Flight (`eagle_doctor.py`)
- Kết quả chạy [eagle_doctor.py](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_doctor.py): **`11/11 PASS, 0 WARN, 0 FAIL` (`41ms`)** (báo cáo chi tiết tại [latest-doctor-report.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/latest-doctor-report.md)).

### 4.2. Kiểm tra Bot Route Crawler (`4/4` Suites — `12/12` Phân đoạn `PASS`)
Bộ kiểm thử tự động [eagle_ingame_tester.py](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ingame_tester.py) điều khiển nhân vật đi bộ/chạy thực tế qua 4 tuyến giáp ranh trọng yếu:

| Suite ID | Tuyến Kiểm thử | Số phân đoạn | Thời gian | Kết quả | Báo cáo Chi tiết |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **`MONDSTADT_M0_TO_M1_SEAM`** | Cầu đá Thành Mondstadt (`M0`) $\rightarrow$ Đàn bồ câu Timmie $\rightarrow$ Mố cầu `PAD-01` (`M0 <-> M1`) $\rightarrow$ `Route 01` (`M1`) | `3/3 PASS` | `4,622 ms` | **`PASS`** | [route-crawler-mondstadt-m0-to-m1-seam.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/route-crawler-mondstadt-m0-to-m1-seam.md) |
| **`MONDSTADT_M1_WINDRISE_WINERY`** | Đường chính `m1_road_r09` (`mw1_t07`) $\rightarrow$ Mép nối `mw1_t07 <-> mw1_t01` $\rightarrow$ Cổng Tửu Trang Dawn Winery (`M1-POI-15`) | `3/3 PASS` | `30,637 ms` | **`PASS`** | [route-crawler-mondstadt-m1-windrise-winery.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/route-crawler-mondstadt-m1-windrise-winery.md) |
| **`MONDSTADT_M1_TO_M2_SEAM`** | Đường `Route 16` (`mw1_t17`) $\rightarrow$ Ranh giới `Sector M1 <-> Sector M2` ($X = -5732\text{m}$) $\rightarrow$ Đèo Bờ biển Chim Ưng (`me2_t20`) | `3/3 PASS` | `35,110 ms` | **`PASS`** | [route-crawler-mondstadt-m1-to-m2-seam.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/route-crawler-mondstadt-m1-to-m2-seam.md) |
| **`MONDSTADT_R21_OCEAN_BRIDGE`** | Cầu Gỗ Vượt Biển `Route 21 Part A` (`me2_road_r21`) $\rightarrow$ Trạm nghỉ Giữa Biển (`me2_abyss_brg`) $\rightarrow$ `Route 21 Part B` (`me2_road_r21b`) | `3/3 PASS` | `17,892 ms` | **`PASS`** | [route-crawler-mondstadt-r21-ocean-bridge.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/route-crawler-mondstadt-r21-ocean-bridge.md) |

### 4.3. Kiểm tra 7 Nội thất Bước vào được (`INT-01..INT-07` @ `Area Code = 1, Z = +1500.0m`)
Toàn bộ 7 nội thất đều nạp đầy đủ `.DFF`, `.TXD` và `.COL3` trong RAM, mặt sàn hứng nhân vật đứng vững (`Vz = 0.000`):

| Mã Nội thất | Model ID & Tên `.DFF` | Tọa độ Sàn (`Area 1`) | Cặp `enex` | Mặt `.COL3` trong RAM | Trạng thái | Ảnh chụp Thực tế In-Game |
| :---: | :--- | :---: | :---: | :---: | :---: | :--- |
| **`INT-01`** | `6696` (`int_dawn_winery`) | `(-7000.0, -4000.0, 1500.40)` | `M1EXT01 <-> M1INT01` | `92 faces` | **`PASS`** | [mondstadt_int_01_int_dawn_winery.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_01_int_dawn_winery.png) |
| **`INT-02`** | `6697` (`int_angels_share`) | `(-6700.0, -4000.0, 1500.40)` | `M1EXT02 <-> M1INT02` | `92 faces` | **`PASS`** | [mondstadt_int_02_int_angels_share.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_02_int_angels_share.png) |
| **`INT-03`** | `6698` (`int_fav_cathedral`) | `(-6400.0, -3999.79, 1500.40)` | `M1EXT03 <-> M1INT03` | `92 faces` | **`PASS`** | [mondstadt_int_03_int_fav_cathedral.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_03_int_fav_cathedral.png) |
| **`INT-04`** | `6699` (`int_knights_hq`) | `(-6100.0, -3999.79, 1500.40)` | `M1EXT04 <-> M1INT04` | `92 faces` | **`PASS`** | [mondstadt_int_04_int_knights_hq.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_04_int_knights_hq.png) |
| **`INT-05`** | `6700` (`int_cats_tail`) | `(-7000.0, -3700.0, 1500.40)` | `M1EXT05 <-> M1INT05` | `92 faces` | **`PASS`** | [mondstadt_int_05_int_cats_tail.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_05_int_cats_tail.png) |
| **`INT-06`** | `6701` (`int_alchemy_lab`) | `(-6700.0, -3700.0, 1500.40)` | `M1EXT06 <-> M1INT06` | `92 faces` | **`PASS`** | [mondstadt_int_06_int_alchemy_lab.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_06_int_alchemy_lab.png) |
| **`INT-07`** | `12150` (`int_spiral_abys`) | `(-6400.0, -3700.0, 1501.00)` | `M2EXT07 <-> M2INT07` | `136 faces` | **`PASS`** | [mondstadt_int_07_int_spiral_abys.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/mondstadt_int_07_int_spiral_abys.png) |

### 4.4. Contact Sheet Hình ảnh & RAM Ban Ngày (`12:00`) & Ban Đêm (`22:00`) (`8/8 PASS`)
- **Ban Ngày (`12:00`)**: **`8/8 PASS` (`17,779 ms`, `0 anomalies`)** — [visual-inspection-mondstadt-day12.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/visual-inspection-mondstadt-day12.md) / [visual-inspection-mondstadt-day12.html](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/visual-inspection-mondstadt-day12.html).
- **Ban Đêm (`22:00`)**: **`8/8 PASS` (`17,382 ms`, `0 anomalies`)** — [visual-inspection-mondstadt-night22.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/visual-inspection-mondstadt-night22.md) / [visual-inspection-mondstadt-night22.html](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/visual-inspection-mondstadt-night22.html).

### 4.5. Kiểm tra 6 Bước Khung xương & Động tác Nhân vật chính Aether (`6/6 PASS`)
- Báo cáo chi tiết: [aether-rig-test-latest.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/aether-rig-test-latest.md) & ảnh chụp thực tế [aether-rig-verification-latest.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/aether-rig-verification-latest.png):
  - `01_CLUMP_AND_MODEL_RAM`: **`PASS`** (`ped_ptr=0x277BB020, model_id=0, m_pRwObject=0x47B1CF28, TXD_slot=45`)
  - `02_WALK_IMPULSE`: **`PASS`** (`Moved 0.55m smoothly | dz=-0.02m`)
  - `03_SPRINT_IMPULSE`: **`PASS`** (`Sprinted 1.10m | End Z=6.29m`)
  - `04_JUMP_AND_LAND_COL`: **`PASS`** (`Peak dZ=+3.01m, Landed Z=6.69m (Start Z=6.29m)`)
  - `05_WEAPON_AND_STATE`: **`PASS`** (`ActiveSlot=2, WeaponType=22, PedState=1, RwObject=0x47B1CF28`)
  - `06_CAMERA_AND_SCREENSHOT`: **`PASS`** (`Camera=OK, Screenshot=aether-rig-verification-latest.png`)

---

## 5. Bài học Kỹ thuật Mới Phát hiện & Đã Khắc phục Triệt để

1. **Độ lệch `+0xC00` giữa File Offset và Virtual Address (`.text`) trong `gta_pe.exe` & Kiểm tra Khởi tạo của `modloader.asi`**:
   - Trong `gta_pe.exe`, phân đoạn `.text` có `VirtualAddress = 0x1000` và `PointerToRawData = 0x400`, nên `VA = FileOffset + 0x400C00` (chênh `+0xC00` so với `0x400000`). Ngoài ra, `modloader.asi` kiểm tra `[0x00C920E8] == 0` trong `DllMain` (`gGameState == 0`). Việc cộng đúng `+0xC00` cho các địa chỉ vá nền (`0x00746081, 0x0053BC78, 0x00747FB6, 0x00747FDA, 0x0074805A`) và chỉ kích hoạt khi `gGameState >= 5` đã loại bỏ hoàn toàn lỗi crash `0x0074745B` và hộp thoại cảnh báo của `modloader.asi`.
2. **Cấu trúc Header Native Texture `DXT1` (`34,816 B`) trong `radar.img` (`0x3C` & `0x90`)**:
   - Trong `radar00.txd`, tên texture nội bộ (`32` byte) nằm tại **`0x3C..0x5C`**, header raster `DXT1` (`width=256, height=256, depth=16, dataSize=0x8000`) nằm tại **`0x7C..0x90`**, và `32,768 B` dữ liệu điểm ảnh `DXT1` bắt đầu tại **`0x90..0x8090`**. Ghi sai vào `0x28` / `0x78` sẽ ghi đè `dataSize = 0x8000` tại `0x8C`, khiến `CTxdStore::LoadTxd` lặp tải hoặc treo khi stream mảnh radar.
3. **Độ cao Tâm Khung xương `CPed` (`CMatrix.pos.z = ground_z + 1.05m`) trên Cầu Nhiều Tầng Va chạm**:
   - Trong GTA SA, `CMatrix.pos.z` của `CPed` nằm tại vùng hông/xương chậu (`+1.02m` phía trên lòng bàn chân). Với các công trình có 2 lớp mặt sàn `.COL` như cầu đá Mondstadt (`5.34m` mặt đường và `2.32m` vòm dưới), khi dịch chuyển cần đặt `z = ground_z + 1.05m` để bàn chân nhân vật đứng trên mặt đường thay vì lọt vào giữa hai lớp va chạm.
