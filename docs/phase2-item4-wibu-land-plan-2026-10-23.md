# Đại Từ Điển Bản Đồ Thế Giới (World Atlas), 6 Cầu Cao Tốc 3D & Quy Hoạch 8 Vùng Đất Wibu (`gta sa gameplay-lab`)

- **Ngày cập nhật**: `2026-10-23`
- **Bản đồ tương tác (Interactive HTML Atlas có nhúng sẵn 16 Ảnh Chụp Phối Cảnh 3D Thực Tế)**:
  - [`map-mismatch-interactive-atlas-2026-10-23.html`](map-mismatch-interactive-atlas-2026-10-23.html) / [`project-eagle-world-atlas-v1.html`](project-eagle-world-atlas-v1.html)
- **Thư mục 16 ảnh phối cảnh 3D thực tế (`1280×720` Cycles — kết xuất từ `.DFF`/`.TXD`/`.IPL` & `pecore_gps_graph.pegg`)**:
  - [`docs/project-eagle/atlas-3d-captures/`](atlas-3d-captures/)
- **Hồ sơ bàn giao thi công Cầu 3D & GPS**:
  - [`work-items/2026-10-23-antigravity-island-bridges-and-gps-unification.md`](work-items/2026-10-23-antigravity-island-bridges-and-gps-unification.md)

---

## 1. Bức Tranh Toàn Cảnh: Đối Chiếu 4 Lớp Dữ Liệu Thực Tế Của `gta sa gameplay-lab`

Khi đối chiếu trực tiếp **4 lớp dữ liệu thực tế** của `gta sa gameplay-lab`:
1. **Ảnh Bản Đồ 2D Pause Map (`ProperRadarSA.txd` & `S&S/Cdimages/default/radar.img` — `9,216` ô `500m × 500m`)**
2. **Thế Giới 3D Thực Tế (`.IPL` / `.IDE` / `.COL` — `147,231` vật thể đặt trên bản đồ sau khi bắc thêm 6 Cầu Cao Tốc 3D `+508` instance và khử `722` bản sao trùng khít `BUG-005`)**
3. **Đồ Thị Đường Bộ GPS (`data/pecore_gps_graph.pegg` — `147,307` node giao thông, `254,380` cạnh có hướng, `151,679` CLink; cụm Lục địa chính `Comp #0` đạt `142,743` node = `>99.6%` toàn bộ node đường bộ mặt đất)**
4. **Danh Bạ `631` Địa Điểm `GG Map` (`eagle_gg_map_pois.py`) & `1,640` Phân Vùng (`S&S/ZON/map.zon` & `info.zon`)**

Chúng ta thu được thống kê chính xác trên từng ô lưới `500m × 500m` của toàn lục địa (`X = [-6000 .. +19000], Y = [-12000 .. +16000]`):

| Phân loại Ô `500m × 500m` | Số lượng Ô | Diện tích ($\text{km}^2$) | Ý nghĩa thực tế & Hệ quả khi chơi / mod |
|---|---:|---:|---|
| 🟢 **Đô Thị 3D Mật Độ Cao (`MATCHED_DENSE`)** | `377` | **`94.25 km²`** | Có cả bản đồ 2D lẫn `>= 80` vật thể 3D/ô (`San Andreas`, `Liberty City`, `Carcer City`, `Vice City`, `Cottonmouth`...). **Không nên nhồi thêm map/tòa nhà Wibu nặng vào đây** để tránh tràn bộ nhớ `CStreaming`; chỉ nên thay texture biển quảng cáo (Giai đoạn 4.1). |
| 🩵 **Ngoại Ô & Đường Trường 3D (`MATCHED_SPARSE`)** | `620` | **`155.00 km²`** | Có cả 2D và `1..79` vật thể 3D/ô (đường cao tốc liên bang, đèo núi, thị trấn nhỏ). Có thể đặt trạm dừng nghỉ, cổng chào Torii hoặc nút giao rẽ vào khu Wibu mới. |
| 🟠 **Ốc Đảo 3D Bị Cô Lập Trước Đây (`ISOLATED_3D_ISLAND`)** | `61` | **`15.25 km²`** | Các thành phố/đảo 3D (`Chicago/Sears Tower`, `Bullworth`, `Dublin/Upstate NE`, `Pera Loca`) trước đây bị ngăn cách với Lục địa chính bởi khoảng trống `0.98 km – 2.82 km` $\rightarrow$ **Nay đã được nối thông 100% bằng 6 Cây Cầu Cao Tốc 3D (`BR-1`..`BR-5`) & `pecore_gps_graph.pegg`!** |
| 🔴 **Đất Ma 2D + Có Sẵn Node GPS Nhưng `0%` 3D (`PHANTOM_2D_WITH_GPS`)** | `54` | **`13.50 km²`** | **Vị trí VÀNG số 1 cho Hạng mục 4**: Trên bản đồ 2D đã vẽ sẵn đường phố/đảo **VÀ** trong `pecore_gps_graph.pegg` đã có sẵn hàng ngàn node đường bộ (`MKLAS` Tây Nam LS, bờ Tây Cottonmouth...), nhưng **thế giới 3D có `0` vật thể**! |
| 🟠 **Vẽ Đường Phố 2D Nhưng `0%` 3D (`PHANTOM_2D_ROADS`)** | `214` | **`53.50 km²`** | Bản đồ 2D đã vẽ sẵn mạng lưới đường xá, quốc lộ, thị trấn nhưng chưa dựng bất kỳ model 3D nào. |
| 🟡 **Vẽ Đất Trống 2D Nhưng `0%` 3D (`PHANTOM_2D_LAND`)** | `179` | **`44.75 km²`** | Bản đồ 2D vẽ đất liền/đồi núi nhưng trong 3D chỉ là mặt nước biển trống. |
| 🟣 **Có Công Trình 3D Trên Biển 2D (`HIDDEN_3D_ON_WATER`)** | `28` | **`7.00 km²`** | Có cầu vượt biển, đảo nhỏ hoặc khu bí mật trong 3D (`.IPL`), nhưng trên Pause Map 2D vẫn hiển thị là màu nước biển. |

---

## 2. Phối Cảnh 3D Thực Tế: 6 Cây Cầu Cao Tốc 3D Đã Thi Công (`CUSTOM_MODS.ipl` + `pecore_gps_graph.pegg`)

Toàn bộ 6 cây cầu cao tốc dưới đây được dựng từ các nhịp mặt đường cao tốc đúc sẵn có `.COL` 10 mặt phẳng chuẩn xác (`58292 gtw_road1A40`, `58291 gtw_road1A30`, `59893 gtw_road1A10` kèm LOD tầm nhìn `1500m`) trong `CUSTOM\CUSTOM_MODS.ipl` và đấu nối trực tiếp chuỗi node GPS + CLink trong `data\pecore_gps_graph.pegg`. Hình ảnh dưới đây được kết xuất trực tiếp bằng **Blender 4.5 Cycles + DragonFF + PyRenderWare** từ các file `.DFF`, `.TXD`, `.IPL` và dải lụa GPS `.PEGG` (màu cyan phát sáng):

| Mã cầu | Tuyến kết nối | Node đầu (Mainland) | Node cuối (Đảo) | Chiều dài 2D | Số nhịp 3D (`+LOD`) | Số node GPS trên cầu |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **Bridge 1 (`BR-1`)** | **Carcer West $\leftrightarrow$ Chicago / Windy Bay (`Comp #97`)** | `133126` `(8786.8, 9625.4, 41.9)` | `137973` `(7115.2, 9811.8, 17.0)` | `1,681.86m` | `43` (`+43 LOD`) | `24` |
| **Bridge 2 (`BR-2`)** | **Carcer East $\leftrightarrow$ Bullworth South (`Comp #104`)** | `143171` `(11363.0, 10502.6, 19.5)` | `144304` `(14023.6, 11433.2, 0.8)` | `2,818.69m` | `73` (`+73 LOD`) | `39` |
| **Bridge 3A (`BR-3A`)** | **Bullworth NE/SE $\leftrightarrow$ Dublin NW (`Comp #103`)** | `144302` `(14043.9, 11436.4, 0.8)` | `144473` `(15338.5, 11397.5, 3.2)` | `1,295.21m` | `34..43` (`+LOD`) | `19` |
| **Bridge 3B (`BR-3B`)** | **Upstate Liberty NE $\leftrightarrow$ Dublin SW (`Comp #103`)** | `141224` `(15977.9, 9958.0, 140.8)` | `143470` `(16559.9, 10747.9, 22.0)` | `981.14m` | `26` (`+26 LOD`) | `15` |
| **Bridge 4 (`BR-4`)** | **LS Ocean Docks $\leftrightarrow$ Đảo Pera Loca (`Comp #19`)** | `21682` `(2326.0, -2663.0, 12.0)` | `15652` `(1589.1, -3839.8, 6.0)` | `1,388.43m` | `36..67` (`+LOD`) | `20` |
| **Bridge 5 (`BR-5`)** | **Nam Whetstone $\leftrightarrow$ Đảo Ma MKLAS / Sanak SW (`Comp #11`)** | `20584` `(-1387.0, -2932.0, 45.0)` | `12371` `(-1390.4, -4551.2, 23.4)` | `1,619.25m` | `42..51` (`+LOD`) | `23` |

### 2.1. `BR-1`: Cầu Cao Tốc #1 — Tây Carcer City $\leftrightarrow$ Chicago / Windy Bay (`1.68 km`)
![Bridge 1: Carcer West to Chicago Windy Bay](atlas-3d-captures/br1_carcer_chicago.png)
*Phối cảnh 3D thực tế tại `(7350, 9785, 17)`: Mặt cầu cao tốc 3D kèm dải lụa GPS cyan tiếp đất trực tiếp vào bờ Đông Chicago / Windy Bay và quần thể nhà chọc trời Sears Tower.*

### 2.2. `BR-2`: Cầu Cao Tốc #2 — Đông Carcer City $\leftrightarrow$ Nam Thị Trấn Bullworth (`2.82 km`)
![Bridge 2: Carcer East to Bullworth South](atlas-3d-captures/br2_carcer_bullworth.png)
*Phối cảnh 3D thực tế tại `(11420, 10522, 19.4)`: Đầu cầu phía Tây kết nối trực tiếp vào đại lộ ven sông Đông Carcer City và cụm cao ốc trung tâm.*

### 2.3. `BR-3A`: Cầu Cao Tốc #3A — Đông Bắc Bullworth $\leftrightarrow$ Tây Bắc Đảo Dublin (`1.30 km`)
![Bridge 3A: Bullworth NE to Dublin NW](atlas-3d-captures/br3a_bullworth_dublin.png)
*Phối cảnh 3D thực tế tại `(15868, 12397, 21.6)`: Nhịp cầu vượt eo biển phương Bắc nối từ Bullworth sang sườn đồi xanh của Đảo Dublin (`S&S\Dublin`).*

### 2.4. `BR-3B`: Cầu Cao Tốc #3B — Đông Bắc Upstate Liberty $\leftrightarrow$ Tây Nam Đảo Dublin (`981m`)
![Bridge 3B: Upstate Liberty NE to Dublin SW](atlas-3d-captures/br3b_upstate_dublin.png)
*Phối cảnh 3D thực tế tại `(16380, 10500, 35)`: Nhịp cầu dốc 26 đốt (với `|rx|, |ry| > 0.052` vượt ngưỡng phẳng hóa `0x005381D5` của `gta_pe.exe`) leo từ bờ đảo Dublin (`Z=22m`) lên đỉnh đèo Upstate Liberty (`Z=138m`).*

### 2.5. `BR-4`: Cầu Cao Tốc #4 — Cảng Los Santos (Ocean Docks) $\leftrightarrow$ Đảo Pera Loca (`1.39 km`)
![Bridge 4: Los Santos Ocean Docks to Pera Loca Island](atlas-3d-captures/br4_ls_peraloca.png)
*Phối cảnh 3D thực tế tại `(2746, -3947, 21.2)`: Nhịp cầu vượt biển phương Nam nối thẳng từ Ocean Docks (Los Santos) ra bờ biển rặng dừa của đảo Pera Loca (`WIBU-05`).*

### 2.6. `BR-5`: Cầu Cao Tốc #5 — Nam Whetstone / Angel Pine $\leftrightarrow$ Cửa Ngõ Đảo Ma MKLAS (`1.62 km`)
![Bridge 5: Whetstone Angel Pine to MKLAS WIBU-01](atlas-3d-captures/br5_whetstone_mklas.png)
*Phối cảnh 3D thực tế tại `(-1389.8, -3250, 23.3)`: Đầu cầu phía Bắc xuyên qua hẻm núi rừng thông Whetstone / Angel Pine vươn thẳng về phía Nam ra vùng biển `WIBU-01`.*

---

## 3. Phối Cảnh 3D Thực Tế: Quy Hoạch 8 Vùng Đất Trống & Đảo Mở Rộng Cho Hạng Mục 4 (`WIBU-01` $\rightarrow$ `WIBU-08`)

| Mã Khu | Tên Khu Quy Hoạch & Vị Trí | Khung Tọa Độ `X` / `Y` | Diện Tích | Điểm Đấu Nối Đường 3D (`Mainland` $\leftrightarrow$ `Target`) | Hiện Trạng 2D / GPS / 3D & Ý Tưởng Xây Dựng Hạng Mục 4 |
|---|---|---|---:|---|---|
| **🔥 `WIBU-01`** *(Ưu tiên #1)* | **Đảo Đô Thị Ma `MKLAS` (Tây Nam Los Santos)** | `X=[-2800..200]`<br>`Y=[-6300..-4300]` | **`5.75 km²`** (`23` ô) | Whetstone `(-1387, -2932, 45.0)` $\leftrightarrow$ Đảo MKLAS `(-1390, -4551, 23.4)` *(Đã bắc Cầu #5 `1.62 km`)* | • **2D**: `100%` (`23/23` ô) đã vẽ sẵn đảo & mạng lưới đại lộ.<br>• **GPS**: **Có sẵn `2,106` node đường bộ (`Comp #11`, `2,095` đoạn đường)** trong `.pegg`!<br>• **3D**: **`0` vật thể**.<br>• **Quy hoạch**: Đặt nguyên **Thành Phố Đảo Wibu / Fontaine / Akihabara / Thành Mondstadt** vào đây — tận dụng ngay Cầu #5 và `2,106` node GPS có sẵn! |
| **🌉 `WIBU-02`** *(Ưu tiên #2)* | **Mặt Tiền Đô Thị & Vịnh Gió Chicago (`Windy Bay`)** | `X=[5200..8900]`<br>`Y=[8200..10900]` | **`5.50 km²`** (`22` ô) | Tây Carcer `(8786.8, 9625.4, 41.9)` $\leftrightarrow$ Đông Chicago `(7115.2, 9811.8, 17.0)` *(Đã bắc Cầu #1 `1.68 km`)* | • **3D & GPS**: Quần thể nhà chọc trời Chicago (`Sears Tower`, `617` model 3D, `1,548` node GPS) đã được Cầu #1 nối thông vào Lục địa chính.<br>• **Quy hoạch**: Biến khu mặt tiền bến du thuyền Windy Bay và dải ven cầu thành **Khu Phố Đêm Anime / Gacha Urban District (Sixth Street ZZZ / Kamurocho)**. |
| **🏫 `WIBU-03`** *(Ưu tiên #3)* | **Thị Trấn Bullworth & Vùng Biển Trống Đông Học Viện** | `X=[13300..16600]`<br>`Y=[9850..12700]` | **`6.25 km²`** (`25` ô) | Đông Carcer `(11363, 10502.6, 19.5)` $\leftrightarrow$ Nam Bullworth `(14023.6, 11433.2, 0.8)` *(Đã bắc Cầu #2 `2.82 km`)* | • **3D**: Nửa Tây thị trấn Bullworth đã có 3D hoàn chỉnh, nhưng **nửa Đông Học viện (`X = 14200..15000`, nơi có 2 POI `GG Map` bị rơi tự do)** có **`0` vật thể 3D**!<br>• **Quy hoạch**: Đặt **Map Trường Học Anime / Tracen Academy (Uma Musume) / Akademi High School** vào `(14456, 12162)`. |
| **⛩️ `WIBU-04`** | **Quần Đảo Dublin (`S&S\Dublin`) & Thung Lũng Đông Bắc** | `X=[15300..17450]`<br>`Y=[10700..13250]` | **`3.00 km²`** (`12` ô) | Đã nối qua **Cầu #3A** (`Bullworth ↔ Dublin NW`) và **Cầu #3B** (`Upstate NE ↔ Dublin SW`) | • **3D & GPS**: Đã có khu phố cổ châu Âu và đồi cỏ xanh (`2,248` node GPS) nối thông 2 đầu.<br>• **Quy hoạch**: Mở rộng thành **Khu Phố Cổ Mondstadt / Liyue / Đền Sakura** trên các sườn đồi trống của đảo Dublin. |
| **🏝️ `WIBU-05`** | **Quần Đảo Nhiệt Đới Pera Loca (Nam Los Santos)** | `X=[1100..2800]`<br>`Y=[-5300..-2650]` | **`1.75 km²`** (`7` ô) | Cảng Ocean Docks LS `(2326, -2663, 12)` $\leftrightarrow$ Đảo Pera Loca `(1589, -3840, 6)` *(Đã bắc Cầu #4 `1.39 km`)* | • **3D & GPS**: Đảo Pera Loca (`123` node GPS, `130` vật thể 3D) đã được nối thông với Los Santos qua Cầu #4.<br>• **Quy hoạch**: Tổ hợp **Resort Bãi Biển Mùa Hè / Quần Đảo Golden Apple Archipelago / Đảo Quy Lão Kame** ngay sát Nam Los Santos. |
| **🌊 `WIBU-06`** | **Đại Vùng Vịnh `SANDAR` (Giữa Peachtree – Cottonmouth)** | `X=[3000..9500]`<br>`Y=[-8000..-1500]` | **`37.50 km²`** (`150` ô) | Nam Peachtree `(3600, -1800, 18.0)` $\leftrightarrow$ Tây Cottonmouth `(9750, -5200, 15.0)` | • **Quy hoạch**: Quỹ đất dự trữ `37.5 km²` (`0` vật thể 3D) ở phía Nam, nơi đặt mặt bằng chính của **Thành Mondstadt Vertical Slice (`6200, -3200, 59.5`)**! |
| **⛰️ `WIBU-07`** | **Đại Bình Nguyên Bắc Cheyenne / Minwall (`RDREG02`)** | `X=[-3500..3500]`<br>`Y=[8500..13500]` | **`31.50 km²`** (`126` ô) | Bắc Lincoln `(-1200, 8400, 42.0)` $\leftrightarrow$ Bình nguyên `(0, 10200, 50.0)` | • **Quy hoạch**: Quỹ đất `31.5 km²` (`0` vật thể 3D) lý tưởng để đặt các **Map Đèo Đua Xe Touge (`Mt. Akina`, `Shomaru Touge`)** mà không ảnh hưởng FPS đô thị. |
| **🔧 `WIBU-08`** | **69 Điểm Hở Node GPS Vi Mô (`Micro-Gap Stitches`)** | Toàn bản đồ `S&S` | *Hở `1.6m – 30.0m`* | `Anneland`, `Abyssal Canyon`, `Starfish`, `Carcer N`, `Chicago SW`... | • **Trạng thái**: **ĐÃ HÀN THÔNG MẠCH 100%** trong `data/pecore_gps_graph.pegg`, giải cứu `2,844+` node đường bộ! |

### 3.1. `WIBU-01`: Cửa Ngõ Đảo Ma `MKLAS` & Mạng Lưới `2,106` Node GPS Có Sẵn Trên Biển
![WIBU-01: MKLAS Ghost GPS Grid and Bridge 5 Touchdown](atlas-3d-captures/wibu01_mklas_gateway.png)
*Phối cảnh 3D thực tế tại `(-1400, -4900, 23.3)`: Nhịp cuối của Cầu Cao Tốc #5 (phía dưới giữa ảnh) nối trực tiếp vào **mạng lưới `2,095` đoạn đường bộ GPS màu cyan phát sáng (`Comp #11` — `2,106` node)** đã được thiết kế sẵn đầy đủ đại lộ, vòng xoay và ô phố trên mặt biển nhưng có `0` vật thể 3D!*

### 3.2. `WIBU-02`: Mặt Tiền Đô Thị & Bến Du Thuyền Chicago / Windy Bay (`Sears Tower`)
![WIBU-02: Chicago Windy Bay Waterfront](atlas-3d-captures/wibu02_chicago_windybay.png)
*Phối cảnh 3D thực tế tại `(6488, 9344, 18)`: Toàn cảnh bờ vịnh Windy Bay, cầu cảng, kè đá và cụm nhà chọc trời Downtown Chicago (đã nối liền mạch với Tây Carcer qua Cầu #1).*

### 3.3. `WIBU-03`: Thị Trấn Bullworth & Khoảng Trống Biển Đông Học Viện (`X > 14200`)
![WIBU-03: Bullworth Town and East Academy Sea Gap](atlas-3d-captures/wibu03_bullworth_academy.png)
*Phối cảnh 3D thực tế tại `(14029, 12064, 18)`: Nửa bên trái là khu thị trấn Bullworth & tháp đồng hồ đã có 3D hoàn chỉnh; nửa bên phải là vùng nước trống `0` vật thể 3D nơi đặt Học viện Anime (`14456, 12162`).*

### 3.4. `WIBU-04`: Quần Đảo Dublin (`S&S\Dublin`)
![WIBU-04: Dublin Island](atlas-3d-captures/wibu04_dublin_island.png)
*Phối cảnh 3D thực tế tại `(16850, 11450, 24)`: Các dãy phố gạch đỏ châu Âu và đồi cỏ xanh trên đảo Dublin, kết nối 2 đầu bởi Cầu #3A và Cầu #3B.*

### 3.5. `WIBU-05`: Đảo Nhiệt Đới Pera Loca (Nam Los Santos)
![WIBU-05: Pera Loca Tropical Island](atlas-3d-captures/wibu05_peraloca_island.png)
*Phối cảnh 3D thực tế tại `(1606, -3867, 12)`: Ngọn hải đăng, rặng dừa nhiệt đới, cầu tàu và bãi biển trên đảo Pera Loca ở phía Nam Los Santos.*

---

## 4. Phối Cảnh 3D Thực Tế: 3 Đại Đô Thị Trọng Điểm & 2 Khu Vực Đã Vá Triệt Để Bug Bản Đồ (`BUG-005`..`BUG-008`)

### 4.1. Los Santos — Downtown & Quảng Trường Pershing Square (`CITY-LS`)
![Los Santos Downtown 3D Capture](atlas-3d-captures/city_ls_downtown.png)
*Phối cảnh 3D thực tế tại `(1480, -1650, 25)`: Trung tâm Los Santos với tháp US Bank Tower, trụ sở LSPD và quảng trường Pershing Square (`MATCHED_DENSE`).*

### 4.2. San Fierro — Khu Doherty, Wang Cars & Cầu Garver Bridge (`CITY-SF`)
![San Fierro Doherty 3D Capture](atlas-3d-captures/city_sf_doherty.png)
*Phối cảnh 3D thực tế tại `(-1980, 260, 35)`: Khu đô thị Doherty, showroom Wang Cars và nhịp cầu dây văng Garver Bridge / cầu sắt Kincaid.*

### 4.3. Las Venturas — Đại Lộ Sòng Bạc The Strip (`CITY-LV`)
![Las Venturas Strip 3D Capture](atlas-3d-captures/city_lv_strip.png)
*Phối cảnh 3D thực tế tại `(2140, 1380, 22)`: Đại lộ The Strip với kim tự tháp Camel's Toe, tháp Obelisk và lâu đài Come-A-Lot.*

### 4.4. Biên Giới Carcer City — Đèo Keystone (`BUG-006` & `BUG-005` Đã Vá)
![BUG-006 Carcer Keystone Border 3D Capture](atlas-3d-captures/bug006_carcer_keystone.png)
*Phối cảnh 3D thực tế tại `(11092.8, 8207.6, 20.0)`: Hành lang đèo Keystone nối Carcer City sau khi liên kết đủ 11 file `.COL` bị thiếu (`274` model `ks_border`), dọn sạch `722` bản sao `.IPL` trùng khít (`BUG-005`) và hàn thông mạch dải lụa GPS cyan.*

### 4.5. Hành Lang Liberty City — Staunton Island & Upstate (`BUG-007` Đã Vá)
![BUG-007 Liberty City Staunton Corridor 3D Capture](atlas-3d-captures/bug007_liberty_staunton.png)
*Phối cảnh 3D thực tế tại `(14750, 7950, 22.0)`: Sân vận động Liberty City, khu phố Staunton Island, cầu vòm và đồi Upstate kèm mạng lưới dải lụa GPS cyan đã thông mạch liên bang.*
