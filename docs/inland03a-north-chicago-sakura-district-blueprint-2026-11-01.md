# Bản Thiết Kế Kỹ Thuật & Quy Hoạch Thi Công Phương Án 1 (`INLAND-03A` Bắc Chicago — Khu Đô Thị Học Viện, Đời Thường Nhật Bản & Đại Lộ Hoa Anh Đào)

- **Ngày lập**: `01/11/2026`
- **Hội thoại lập kế hoạch**: `3aacdf8b-d651-49fd-bb78-b3aba265fc6b`
- **Target tích hợp duy nhất**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Vùng đất lắp đặt**: **`INLAND-03A` (Phố Ma 2D Bắc Chicago)** — Khung tọa độ `X = [5630 .. 6980], Y = [10028 .. 11260]`, diện tích `1.28 km × 1.23 km = 1.57 km²`, độ cao chuẩn mặt đường `Z = 14.50m` (`ΔZ = 0.00m` tại cả 5 mối hàn đại lộ Bắc Chicago).
- **Trạng thái**: **Đã chốt thiết kế (`Approved for Implementation`)** — Sẵn sàng cho hội thoại thi công mới.

---

## 1. Tài Liệu Hình Ảnh & Bằng Chứng Khảo Sát Đã Lưu Trên Đĩa

1. **Bản đồ quy hoạch tổng thể & 5 mối hàn đại lộ (`Poster 1`)**:
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\evidence\inland03a_master_urban_and_road_plan.png`
2. **Bộ sưu tập 20 Map mới, Building mới & Object mới 100% chưa dùng trên Đảo Wibu / Mondstadt (`Poster 2`)**:
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\evidence\inland03a_new_buildings_and_objects_showcase.png`
   - 4 ảnh cắt riêng từng phân khu (`Zone A..D`): `docs\project-eagle\evidence\inland03a_zone_a_academy_preview.png` .. `inland03a_zone_d_modern_mansion_preview.png`
3. **Thiết kế mặt cắt đường xá mới 28m & Kịch bản di chuyển thực tế (`Poster 3`)**:
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\evidence\inland03a_road_design_and_movement_blueprint.png`
4. **Bằng chứng chụp in-game xác nhận vùng `INLAND-03A` trống `0% 3D`**:
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\evidence\inland03_chicago_bullworth_proof_grid.png`
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\evidence\inland_zones_and_donor_maps_scale_blueprint.png`

---

## 2. Dải ID Model & Cấu Trúc File Độc Lập Cho `INLAND-03A`

- **Dải Model ID trống hoàn toàn đã kiểm chứng trong `gameplay-lab`**:
  - Dải ưu tiên: **`12200 .. 12599` (`400` ID trống liên tiếp, nằm trong khối trống `12153 .. 12799` — hoàn toàn tách biệt với `WIBU-01` `3194..11958` và `Mondstadt` `6680..6881`, `11960..12152`)**.
  - Dự phòng nếu cần thêm: **`15100 .. 15499`** (nằm trong khối trống `15065 .. 15999`).
- **Tổ chức file runtime đề xuất (Độc lập, không chạm vào file của `WIBU-01` hay `Mondstadt`)**:
  - `CUSTOM\inland03a_sakura_chicago.ide`
  - `CUSTOM\inland03a_sakura_chicago.ipl`
  - `CUSTOM\inland03a_sakura_chicago.col`
  - `CUSTOM\inland03a_sakura_chicago.img` (hoặc đóng gói vào `MODELS\MODS\eagle_merged_mods.img` kèm đăng ký `gta.dat`)
  - Staging riêng trên ổ D: `D:\GTA Archive\Staging\inland03a-sakura-chicago-2026-11-01\`

---

## 3. Tọa Độ Chính Xác Của 5 Mối Hàn Đại Lộ 3D Bắc Chicago (`Z = 14.3m .. 14.5m`)

Toàn bộ 5 trục đường dọc Bắc – Nam của khu đô thị mới bắt đầu trực tiếp từ 5 đầu đường nhựa 3D có sẵn ở biên giới phía Bắc Chicago (`S&S\maps\mw\nmile.ipl`), **không xây cầu vượt biển**:

| Mã Mối Hàn | Tọa Độ Đầu Đường Cũ `(X, Y, Z)` | Model Đường Cũ (`nmile.ipl`) | Trục Đại Lộ Mới Nối Tiếp Lên Phía Bắc (`Z = 14.50m`) |
| :--- | :---: | :--- | :--- |
| **`WELD-1`** *(Tây)* | `(5822.7, 10027.9, 14.50)` | `mwGenRd4lna` *(4 làn)* | **Trục Dọc 1 (`Academy West Ave`)**: `X = 5822.7`, chạy từ `Y = 10027.9` lên `Y = 11120.0` |
| **`WELD-2`** *(Trung–Tây)* | `(6105.8, 10027.9, 14.50)` | `mwGenRd4lna` *(4 làn)* | **Trục Dọc 2 (`Nobita & Ramen Ave`)**: `X = 6105.8`, chạy từ `Y = 10027.9` lên `Y = 11120.0` |
| **`WELD-3`** *(Trục Chính)* | `(6319.2, 10193.3, 14.50)` | `mwGenRd4lna` *(4 làn)* | **ĐẠI LỘ CHÍNH (`Sakura Central Blvd`)**: `X = 6319.2`, rộng `28m` (có dải phân cách hoa anh đào giữa đường), từ `Y = 10193.3` lên `Y = 11180.0` |
| **`WELD-4`** *(Trung–Đông)* | `(6473.6, 10027.9, 14.50)` & `(6542.6, 10180.8, 14.30)` | `mwWideCrossRd4sx4` & `wb_road70` | **Trục Dọc 4 (`Otaku & Showroom Ave`)**: Nối từ `(6473.6, 10027.9)` lên `(6510.0, 10200.0)` rồi chạy thẳng lên `Y = 11120.0` |
| **`WELD-5`** *(Đông Ven Vịnh)* | `(6728.4, 10537.4, 14.50)` & `(6818.0, 10575.3, 14.50)` | `nMile_cst_road61` & `mwWideCrossRd2sx4` | **Trục Dọc 5 (`Lakeside Villa Drive`)**: Nối từ `(6728.4, 10537.4)` chạy dọc bờ vịnh lên `Y = 11120.0` |

### 4 Đại lộ ngang (`East–West Cross Streets` tại `Z = 14.50m`)
1. **`Cross-1 (South Border Connector, Y = 10200.0)`**: `X = 5640 .. 6695` — Nối ngang đầu 4 trục dọc ngay sát biên Bắc Chicago.
2. **`Cross-2 (Campus & Concert Promenade, Y = 10480.0)`**: `X = 5640 .. 6770` — Đại lộ hoa anh đào ngang qua Trường Cấp 3, Quán Ichiraku Ramen và Quảng trường Sân khấu Miku.
3. **`Cross-3 (Sakura Commercial Blvd, Y = 10750.0)`**: `X = 5640 .. 6880` — Đại lộ ngang nối Trụ sở Avengers HQ, Starbucks, Walmart/IKEA, Car Showroom và Đồi Biệt Thự.
4. **`Cross-4 (North Ring & Rest Park Way, Y = 11080.0)`**: `X = 5760 .. 6850` — Vành đai phía Bắc nối vào Trạm dừng nghỉ cao tốc `Truck & Bus Rest Park`.

---

## 4. Danh Mục 20 Công Trình & Gói Tài Nguyên Mới (`100% Chưa Dùng`) Từ `D:\GTA Archive\Mod Donor Library`

### Phân khu A — Học Viện & Thể Thao Anime (`X = 5630 .. 6045, Y = 10060 .. 10725`)
- **`A1` — Trường Cấp 3 `Escuela High School`** (`X=[5848..6035], Y=[10235..10445]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky4-anime-worlds\Escuela_Interior_117570\gta3.img\school.dff` + `escuela_objetos.col` (`70.0m × 20.6m × 38.8m`).
- **`A2` — Khu Nội Thất Lớp Học & Phòng Hiệu Trưởng** (`X=[5645..5798], Y=[10235..10445]`):
  - Nguồn: `classroom.dff`, `DirectorOfi.dff`, `interior3.dff`, `interior4.dff` trong cùng gói `Escuela_Interior_117570`.
- **`A3` — Sân Bóng Đá Học Đường & CLB Anime (`Anime Scene Map`)** (`X=[5848..6035], Y=[10515..10715]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky4-anime-worlds\Anime_Scene_Map_165621` (`Cancha.dff`, `CasaCampo.dff`, `Anime.dff`, `Nagato_Yander1..4.dff`, `79.5m × 154.4m × 23.3m`).
- **`A4` — Sân Trượt Băng Nghệ Thuật (`Figure Skating Rink`)** (`X=[5645..5798], Y=[10515..10715]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky6-world-filling-assets\gtainside-scenic-packs\GI_193661_figure-skating-v-0-3-for-pc`.

### Phân khu B — Phố Đời Thường Nhật Bản & Ẩm Thực Ramen (`X = 6065 .. 6295, Y = 10060 .. 10725`)
- **`B1` — Khu Phố Nhà Nobita & Doraemon** (`X=[6130..6292], Y=[10345..10455]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky4-anime-worlds\Nobita_House_78710\Nobita's House\data\maps\ie\ie1.dff`, `ie2.dff`, `ie.txd`, `ie1.col`, `ie2.col`.
- **`B2` — Sân Bãi Ống Cống & Công Viên Khu Phố Nobita** (`X=[6130..6292], Y=[10225..10335]`):
  - Nguồn: `test.dff`, `test.col`, `test.txd`, `fujyou_kino.dff`, `setti_Kino.dff` trong gói `Nobita_House_78710`.
- **`B3` — Quán Mì `Ichiraku Ramen`** (`X=[6130..6292], Y=[10515..10615]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky4-anime-worlds\Ichiraku_Ramen_86716\RAMEN\gta3.img\stripbar_lae.dff` + `lae2_4.col`.
- **`B4` — Phố Xe Đẩy Mì Đêm & Kiosk Ẩm Thực** (`X=[6130..6292], Y=[10625..10720]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky5-internet-multiverse\GI_176183_food-carts-and-kiosks-like-g` (`Food_cars\noodlecart_prop.dff`, `chillidogcart.dff`, `Beach-KiosksGTA V\beachhut01_law.dff`).

### Phân khu C — Phố Otaku & Quảng Trường 3 Sân Khấu Concert Miku (`X = 6340 .. 6695, Y = 10210 .. 10725`)
- **`C1` — Tổ Hợp Tòa Nhà Thương Mại `Little Akihabara V1 & V2`** (`X=[6350..6485], Y=[10230..10445]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\Little_Akihabara_V1_155181` & `Little_Akihabara_V2_221340` (`lanblokb2.txd` + khối nhà LAn).
- **`C2` — Dãy Phố Cửa Hiệu Nhật `OtakuShoppu & Japanese Building V1/V2`** (`X=[6535..6685], Y=[10230..10445]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\Japanese_Building_V1_159896` & `V2_175652` (`sunrise09_lawn.txd` + props).
- **`C3` — Quảng Trường Sân Khấu 3D `Hatsune Miku Project DIVA: Puzzle Stage`** (`X=[6350..6490], Y=[10515..10715]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky4-anime-worlds\PDFT_Puzzle_Stage_193789` (`10` DFFs + `10` COLs, `169.5m × 179.0m × 39.8m`).
- **`C4` — Sân Khấu `Romeo & Cinderella` + `World Is Mine` + `Miku Neon Signs`** (`X=[6535..6695], Y=[10515..10715]`):
  - Nguồn: `ky4-anime-worlds\Romeo_Cinderella_Stage_195825` (`3` DFFs), `World_Is_Mine_Stage_186849` (`2` DFFs) và `ky2-urban-buildings\Miku_Sign_180718` (`4` DFFs).

### Phân khu D — Đại Lộ Thương Mại, Showroom & Đồi Biệt Thự Ven Vịnh (`X = 5710 .. 6975, Y = 10620 .. 11260`)
- **`D1` — Trụ Sở Công Nghệ `Avengers Facility Headquarters`** (`X=[5848..6065], Y=[10790..11035]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky5-internet-multiverse\GI_137628_avengers-facility-for-pc\Avengers Facility Pc\Add It In Gta3.img\Abase1.dff` + `abase.col` (`96.3m × 107.9m × 36.5m`).
- **`D2` — Cửa Hàng Cafe `Starbucks Building`** (`X=[6130..6285], Y=[10790..10910]`):
  - Nguồn: `D:\GTA Archive\Mod Donor Library\ky5-internet-multiverse\GI_159350_starbucks-building-mod`.
- **`D3` — Đại Siêu Thị `Walmart Supermarket` & `IKEA Megastore`** (`X=[6350..6490], Y=[10790..11035]`):
  - Nguồn: `ky5-internet-multiverse\GI_48878_walmart-supermarket` & `GI_8759_ikea-mod-v1-0`.
- **`D4` — `Car Showroom` & Biệt Thự Hiện Đại `Modern Mansion`** (`X=[6535..6735], Y=[10790..11035]`):
  - Nguồn: `ky5-internet-multiverse\GI_150767_car-showroom-and-buying-cars\New Folder (2)\New Folder (2)\vgswrehse18.dff` + `GI_127449_modern-mansion` (`Base.dff`, `Garage_Furniture.dff`, `Lower_Furniture.dff`, `Outside_Furniture.dff`, `Upper_Furniture.dff`, `Glass.dff`).
- **`D5` — Đồi Biệt Thự Ven Vịnh `Villa F 1.1` & `New Mansion Villa`** (`X=[6795..6945], Y=[10620..11035]`):
  - Nguồn: `ky5-internet-multiverse\GI_167239_villa-f-1-1-mansion-for-andr` (`VillaF.dff`) & `GI_193945_new-mansion-villa-for-gta-sa` (`LABIGSAVEHOUse.dff`).
- **`D6` — Tháp Biểu Tượng `Tallest Tower`** (`X=[6130..6285], Y=[10925..11045]`):
  - Nguồn: `ky6-world-filling-assets\gtainside-scenic-packs\GI_129128_tallest-tower-in-la`.
- **`D7` — Trạm Dừng Nghỉ Cao Tốc `Truck & Bus Rest Park`** (`X=[6110..6390], Y=[11105..11235]`):
  - Nguồn: `ky6-world-filling-assets\gtainside-scenic-packs\GI_133149_truck-and-bus-rest-park-for-` (`102.8m × 114.4m`).
- **`D8` — Công Viên Rừng Thông, Khu Cắm Trại & Hải Đăng Ven Vịnh** (`X=[6785..6975], Y=[11060..11260]`):
  - Nguồn: `GI_27339_forest-mod-v2` + `GI_52962_camping-area-mod-v1-0` + `GI_212020_lighthouse-santa-maria-beach`.

---

## 5. Quy Trình Thi Công & Nghiệm Thu Bắt Buộc Trong Hội Thoại Mới

1. **Bước 1 — Đăng ký Work-Item & Staging riêng**:
   - Tạo phiếu `docs/project-eagle/work-items/2026-11-01-antigravity-inland03a-sakura-chicago-district.md`.
   - Khởi tạo thư mục staging `D:\GTA Archive\Staging\inland03a-sakura-chicago-2026-11-01\`.
2. **Bước 2 — Xây dựng Tấm nền (`Foundation Pads`) & Lưới đường 5×4 (`Z = 14.50m`)**:
   - Tạo mặt nền đất/cỏ/vỉa hè phẳng tại `Z = 14.40m` và lưới đường nhựa 5 dọc × 4 ngang tại `Z = 14.50m` khớp chính xác `ΔZ = 0.00m` với 5 đầu đường `WELD-1..5` của Bắc Chicago.
   - Đảm bảo mọi mặt đường & tấm nền **không đặt cờ `DRAW_LAST (4)`** và có đầy đủ mesh va chạm `.col` hai mặt hoặc pháp tuyến hướng lên (`nz > 0`).
3. **Bước 3 — Đóng gói 20 Tổ hợp Công trình (`IDs 12200 .. 12599`)**:
   - Chuẩn hóa `.dff`, `.txd` (nén DXT1/DXT5 hợp lệ, kiểm tra mipmap/alpha), `.col` (`COL3` có đầy đủ bounding sphere/box và triangle collision) và tạo `.ide` + `.ipl` cho toàn bộ 4 phân khu `A, B, C, D`.
4. **Bước 4 — Đấu nối Đồ thị GPS (`pecore_gps_graph.pegg`), Radar 2D & `EagleRide` POIs**:
   - Thêm 20 nút giao thông (`Nodes`) và 28 đoạn đường (`Edges`) nối trực tiếp vào 5 nút biên Bắc Chicago trong `data\pecore_gps_graph.pegg`.
   - Cập nhật các tile radar 2D tương ứng của khu vực `X=[5500..7000], Y=[10000..11300]` trong `radar.img` để minimap hiển thị đúng lưới đường 5×4 và 20 công trình mới.
5. **Bước 5 — Nghiệm thu Thực tế In-Game (`gta_pe.exe`) & Đóng Game Sau Khi Test**:
   - Chạy kiểm tra `Doctor`, `Route Crawler` lái xe thực tế từ Bắc Chicago qua cả 5 mối hàn `WELD-1..5` vào từng phân khu `A, B, C, D`, kiểm tra đi bộ của Aether và chụp bộ ảnh Contact Sheet nghiệm thu.
   - **Lưu ý bắt buộc**: Sau khi hoàn tất chụp ảnh/test in-game, phải **tắt `gta_pe.exe` ngay lập tức** theo đúng yêu cầu của người dùng.
