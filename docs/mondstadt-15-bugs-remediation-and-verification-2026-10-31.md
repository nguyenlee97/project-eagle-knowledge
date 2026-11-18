# Báo Cáo Khắc Phục Toàn Diện 15 Lỗi In-Game & Nghiệm Thu Thực Tế Quần Thể Mondstadt (`Sector M0 + M1 + M2 + INT-01..07`)

- **Ngày thực hiện**: `2026-10-31`
- **Agent thực hiện**: `Antigravity` (`33fbbaf0-a9d8-4aff-94bf-3242e4a6d74a`)
- **Đích triển khai**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Staging riêng**: `D:\GTA Archive\Staging\mondstadt-ingame-integration-2026-10-30`
- **Work Item**: [`docs/project-eagle/work-items/2026-10-30-mondstadt-m0-m1-m2-ingame-integration.md`](work-items/2026-10-30-mondstadt-m0-m1-m2-ingame-integration.md)
- **Trạng thái nghiệm thu**: **`100% PASS`** (`Doctor 11/11 PASS`, `Route Crawlers 7/7 Suites [29/29 chặng PASS]`, `Terrace Jump-Down 3/3 PASS`, `Enterable Interiors 7/7 PASS`, `Contact Sheet Ngày/Đêm 8/8 PASS`, `Live City NPCs 43 spawned / 22 walking`, `Aether 6-Step Rig Test 6/6 PASS`).

---

## 1. Bảng Đối Chiếu 15 Lỗi Báo Cáo & Giải Pháp Kỹ Thuật Triệt Để

| # | Hạng mục lỗi người dùng báo cáo | Nguyên nhân gốc rễ (Root Cause) | Giải pháp kỹ thuật & File đã cập nhật | Trạng thái |
| :-: | :--- | :--- | :--- | :-: |
| **1** | Lục địa Mondstadt cấn vào cầu San Fierro (`Gant Bridge` / `Garver Bridge`) | Tâm cũ `(-4100, -2300, +60.5)` khiến cực Bắc tiến sát vùng San Fierro (`Y > -2400`) | Dịch chuyển toàn bộ quần thể `M0 + M1 + M2` về phía Tây Nam tới `NEW_ANCHOR = (-4350.0, -3000.0, +59.5)` (`DX = -250m, DY = -700m, DZ = -1.0m`), đảm bảo khoảng cách an toàn `> 500m` phía Nam San Fierro và phía Tây Whetstone | **PASS** |
| **2** | Cầu nối đất liền mang phong cách hiện đại lạc quẻ với kiến trúc Mondstadt | Cầu dây văng/thép hiện đại không hợp mỹ thuật thời trung cổ châu Âu của Mondstadt | Thiết kế & biên dịch mới **Đại Cầu Vòm Đá Gothic Hoàng Gia Mondstadt** dài `891.5m` gồm `10` nhịp (`IDs 12079..12088`, `me2_viaduct_01..10`, LOD `12109..12118`) nối từ Whetstone (`-2584.0, -2633.0, 9.05m`) tới Bờ Chim Ưng (`-3206.0, -3272.0, 12.96m`) với cổng tháp đôi Gothic, vòm cuốn đá, trụ chắn sóng và `.COL3` liền mạch | **PASS** |
| **3** | Minimap / Radar 2D lệch vị trí hoặc sai bảng màu gốc GTA SA | Các tile `radar*.txd` chưa khớp tọa độ dịch chuyển mới và bảng màu chuẩn GTA SA | Kết xuất mới `30` tile `radar*.txd` (`256×256 DXT1` supersampled từ `512×512`) vào `S&S\Cdimages\default\radar.img` theo đúng bảng màu bản đồ 2D GTA SA (`#7087AD` nước, `#91AF64` thảo nguyên, `#A5A096` khu phố, `#383838` mặt đường viền `#141414`, `#D6BA63` cầu vượt biển) | **PASS** |
| **4** | Thiếu icon chú thích địa danh trên bản đồ (`Legend Blips`) và NPC trong thành dùng skin lặp lại của Los Santos | Chưa có script đăng ký blip `CRadar::SetCoordBlip` và các NPC đứng quầy chưa lọc danh sách skin hiếm | Biên dịch `cleo\MondstadtLifeAndBlips.cs` (`3,247 B`) hiển thị icon bản đồ gốc (`0AA5` `CRadar::SetCoordBlip`) tại các địa danh/cửa hàng chính và triệu hồi `26` NPC đứng quầy (`100%` dùng skin anime/game hiếm, không trùng NPC đại trà ở Los Santos) + `71` node đi bộ `FLA4` trong `paths.img` | **PASS** |
| **5** | Bậc thang trong Thành Mondstadt (`M0`) bị khấc cao, phải nhảy mới lên được | Các bậc đá dốc đứng trong `6711..6714` vượt ngưỡng bước chân tự động của `CPed` | Bổ sung các dốc đá thoải (`stair ramps`) cả ở lưới hiển thị `.DFF` và lưới va chạm `.COL3` trong `6711, 6712, 6713, 6714`, giúp nhân vật chạy bộ mượt từ Cổng Chính -> Chợ Dưới -> Quảng Trường Đài Phun Nước -> Quảng Trường Tượng Phong Thần -> Đại Giáo Đường mà không cần nhảy | **PASS** |
| **6** | Timmie và đàn bồ câu đứng chắn giữa lòng cầu đá Mondstadt (`6716`) | Tọa độ cũ đặt Timmie và đàn bồ câu ngay tim đường xe/người chạy | Dịch chuyển Timmie (`model 167`, `(-4084.80, -3073.50, 5.99)`) và đàn bồ câu (`6716`, `md_island_bridge`) sang lề bộ hành sát lan can đá phía Bắc, giải phóng hoàn toàn lòng đường trung tâm | **PASS** |
| **7** | Tường vô hình chặn người chơi nhảy từ sân thượng/bậc thang xuống khu dưới | Một số mặt đứng biên trong `mondstadt_m0_city.col` nhô cao hơn mặt sàn tạo tường chắn vô hình | Loại bỏ toàn bộ mặt chắn vô hình nhô cao trên mép bậc thang/sân thượng của `6710..6714`; kiểm thử thực tế nhảy từ 3 tầng quảng trường/bậc thang xuống khu dưới (`JUMP_01..03`) đều vượt mép mượt mà (`drop_z = 4.03m..7.15m`) | **PASS** |
| **8** | Tường chắn kè đá và Tượng Phong Thần Barbatos (`6713`) bị sọc kéo giãn hoặc dính mảnh ngói đỏ li ti | Chiếu UV phẳng `XY` lên mặt đứng khiến `du ≈ 0, dv ≈ 0` (sọc đứng), còn ép `mat_id=0` lại gán nhầm atlas nhà/mái ngói `md_city_tex` | Trong [`fix_m0_city_and_bridge.py`](file:///d:/GTA%20Archive/Staging/mondstadt-ingame-integration-2026-10-30/fix_m0_city_and_bridge.py): giữ nguyên `mat_id` đá/cỏ (`1, 2, 3`), đồng nhất Tượng Barbatos (`6713`) về `mat_id = 2` (`md_stairs_stone` đá chạm khắc sáng màu), tách đỉnh theo `(mat_id, plane_ax)` và áp dụng **True 3D Triplanar World-Space UVs** (`XY` cho sàn, `YZ` cho tường Đông/Tây, `XZ` cho tường Bắc/Nam) | **PASS** |
| **9** | Màu cỏ ở vùng ngoại ô `M1` & `M2` bị xám/vàng úa khi nhìn gần | Texture cỏ gốc thiếu độ bão hòa xanh lục và prelight đỉnh bị kẹp xám | Tạo mới bộ texture thảo nguyên xanh ngọc lục bảo Mondstadt (`mw_grass_lush`, `mw_springvale`, `me2_grass_lush`, `RGB ~(78, 154, 52)` có hoa Cecilia trắng vàng) và bảo toàn sắc độ xanh trong prelight đỉnh (`patch_dff_vertex_colors_vibrant`) | **PASS** |
| **10** | Ánh sáng ban đêm ở Thành Mondstadt (`M0`) quá gắt hoặc lóa | Điểm sáng `2DFX` cũ có bán kính và cường độ corona quá lớn | Cân chỉnh toàn bộ đèn `2DFX` trong `6710..6716` về tông vàng ấm dịu (`RGB (255, 210, 135)`, `cor_size = 0.85..1.0`, `rd = 18..24m`) kết hợp `ExtraVertColour` (`NVCA`) ban đêm cân bằng | **PASS** |
| **11** | Một số đoạn đường/sườn đồi/vật thể ở `M1` & `M2` bị xuyên thấu (`.COL` thiếu mặt) | `.COL3` cũ dùng decimation thưa và thiếu mặt va chạm cho sạp hàng/xe kéo/đá/nội thất | Biên dịch lại toàn bộ `mondstadt_m0_city.col` (`8,580` faces), `mondstadt_m1_wilds.col` (`174,866` faces), `mondstadt_m2_east.col` (`131,773` faces) ở độ phủ `100%` (`stride=1`, `TColFace.light=0xFF`, giữ `100%` tam giác tầm người chơi `z <= 4.2m`) | **PASS** |
| **12** | Quái vật, Boss, Rương báu và cây cối bị lơ lửng hoặc nằm trên tán cây | Tọa độ `Z` nội suy chưa raycast trực tiếp lên mặt `.COL3` địa hình thực tế | Xây dựng `FastColRaycaster` (lưới không gian `32m`) bắn tia xuống mặt `.COL3` địa hình/mặt đường để hạ chính xác từng rương báu, quái vật, địa danh, điểm `ENEX` và loại bỏ các cây lơ lửng (`712, 713, 615, 617, 1226`) | **PASS** |
| **13** | Khe hở / khấc va chạm tại điểm tiếp giáp Cầu Đá `M0` (`6716`) và Đường `M1` (`6854`) | Cao độ mũi cầu Đông `6716` và đầu đường `m1_road_r01` (`6854`) tại `PAD-01 (-4029.0, -3093.1, 4.31)` chưa khâu liền | Khâu liền mạch mặt đường và `.COL3` giữa `6716` (`md_island_bridge`) và `6854` (`m1_road_r01`) qua `PAD-01`; kiểm thử `MONDSTADT_M0_TO_M1_SEAM` đạt `5/5 segments PASS` | **PASS** |
| **14** | 6 tòa nhà lớn (`INT-01..INT-06`) chưa vào được hoặc nội thất thiếu trần/tường kín | Cặp `ENEX` chưa đồng bộ tên hoặc nội thất thiếu hộp tường/trần hai mặt tại `Area Code = 1` | Nâng cấp 6 nội thất `6696..6701` (`int_dawn_winery`, `int_angels_share`, `int_fav_cathedral`, `int_knights_hq`, `int_cats_tail`, `int_alchemy_lab` tại `Area 1, Z = 1500.25m`) với tường/trần kín, `.COL3` sàn/bàn ghế đặc và cặp `ENEX` 2 chiều (`MD_WIN`, `MD_ANG`, `MD_CAT`, `MD_KNI`, `MD_TAI`, `MD_ALC`) | **PASS** |
| **15** | Cổng La Hoàn Thâm Cảnh (`Spiral Abyss` tại Rạn San Hô Musk) chưa có sảnh nội thất hoàn chỉnh hoặc bị cây/khe hở che | Bản chuyển đổi từ `spiral_abyss_interior_3d.glb` (`12150`, `int_spiral_abys`) có cụm cây 42k tam giác (`g[8..10]`) & bụi cây (`g[5]`) chắn giữa phòng và để hở vách phải nơi đặt cây | Biên dịch `12150` (`int_spiral_abys`) giữ `100%` độ chi tiết (`stride=1`) cho sảnh đấu trường, cột đá, vòng tròn Abyss, Rương Hiếm (`g[11]`) và Chìa Khóa Monolith (`m_cut`), loại bỏ cây chắn tầm nhìn (`g[5], g[8..10]`) và bổ sung vách đá hình trụ `360°` (`R = 20.6m`, `me2_stone_ruin`) + vòm sao Abyss (`me2_abyss_void`) đóng kín hoàn toàn sảnh tại `(-4250.0, -3200.0, 1500.0)` nối với cổng `MD_ABY` | **PASS** |

---

## 2. Kết Quả Kiểm Tra & Nghiệm Thu Thực Tế Trong Game (`gta_pe.exe`)

### 2.1. Kiểm tra Sức khỏe Hệ thống (`eagle_doctor.py`)
- **Kết quả**: **`11/11 PASS, 0 WARN, 0 FAIL`** (`46ms`).
- `03_GPS_GRAPH_PEGG`: `148,337` nodes, `252,486` directed edges (`28,186,640 B`).
- `04_MAP_MOUNTS_CACHE`: `526` mounts (`0 missing`).

### 2.2. Kiểm thử Chạy bộ Liên tục Qua 7 Tuyến Đường, Cầu & Bậc Thang (`Route Crawlers`: `7/7 Suites PASS` — `29/29 Chặng PASS`)

| # | Mã Tuyến (`Suite Code`) | Mô tả lộ trình kiểm thử | Số chặng PASS | Thời gian | Trạng thái |
| :-: | :--- | :--- | :-: | :-: | :-: |
| 1 | `MONDSTADT_GOTHIC_VIADUCT` | Đại Cầu Vòm Đá Gothic Hoàng Gia (`891m` Whetstone `<->` Falcon Coast, qua nhịp 1 & khe nối nhịp 1 `<->` 2) | `5/5` | `6,044 ms` | **`PASS`** |
| 2 | `MONDSTADT_M0_TO_M1_SEAM` | Cổng Chính Mondstadt -> Cầu Đá -> Chỗ Timmie & Bồ câu -> Khe nối `PAD-01` -> Đường dẫn `M1` | `5/5` | `6,446 ms` | **`PASS`** |
| 3 | `MONDSTADT_CITY_SHOPS_AND_STAIRS` | Cổng Thành -> Tiệm Rèn Wagner -> Hiệp Hội Nhà Mạo Hiểm -> Sạp Hoa/Quả -> Bậc Thang Chợ Dưới -> Good Hunter -> Đài Phun Nước & Giả Kim | `6/6` | `6,483 ms` | **`PASS`** |
| 4 | `MONDSTADT_CATHEDRAL_STAIRS` | Quảng Trường Tượng Phong Thần Barbatos -> Chân Cầu Thang Lớn -> Giữa Cầu Thang -> Đỉnh Cầu Thang -> Cửa Đại Giáo Đường Favonius | `4/4` | `4,370 ms` | **`PASS`** |
| 5 | `MONDSTADT_M1_WINDRISE_WINERY` | Đường Cao Nguyên Tửu Trang Dawn Winery -> Cổng Tửu Trang -> Sân Trong -> Cửa Chính Dinh Thự | `3/3` | `2,964 ms` | **`PASS`** |
| 6 | `MONDSTADT_M1_TO_M2_SEAM` | Đường Liên Vùng `Route 16` cắt qua ranh giới `Sector M1 <-> Sector M2` (`X = -3582m`) | `3/3` | `3,088 ms` | **`PASS`** |
| 7 | `MONDSTADT_R21_OCEAN_BRIDGE` | Cầu Gỗ Vượt Biển `Route 21` nối Mũi Hứa Hẹn (`Cape Oath`) -> Trạm Giữa Biển -> Rạn San Hô Musk | `3/3` | `2,634 ms` | **`PASS`** |

### 2.3. Kiểm thử Nhảy Từ Sân Thượng & Mép Bậc Thang Xuống Khu Dưới (`Bug #7` — `0` Tường Vô Hình: `3/3 PASS`)

| Mã bài kiểm thử | Điểm xuất phát (Tầng trên) | Điểm tiếp đất (Tầng dưới) | Quãng đường ngang (`moved`) | Độ hạ cao độ (`drop_z`) | Trạng thái |
| :--- | :--- | :--- | :-: | :-: | :-: |
| `JUMP_01_FOUNTAIN_TO_LOWER_MARKET` | Mép Đông Quảng trường Đài Phun Nước (`-4237.0, -3036.0, 12.60`) | Khu Chợ Dưới (`-4197.90, -3034.60, 7.53`) | `39.13m` | `-6.07m` | **`PASS`** |
| `JUMP_02_CATHEDRAL_STAIR_SIDE_DROP` | Mép bên Đại Cầu Thang Giáo Đường (`-4422.0, -2934.0, 51.50`) | Quảng trường Tượng Phong Thần (`-4407.32, -2978.04, 49.03`) | `46.43m` | `-4.03m` | **`PASS`** |
| `JUMP_03_CATHEDRAL_UPPER_TERRACE_DROP` | Lan can Sân Thượng Đại Giáo Đường (`-4435.0, -2944.0, 55.14`) | Quảng trường Tượng Phong Thần (`-4387.62, -2951.47, 48.99`) | `47.96m` | `-7.15m` | **`PASS`** |

### 2.4. Kiểm thử 7 Không Gian Nội Thất (`INT-01..INT-07` tại `Area Code = 1, Z = +1500.25m`: `7/7 PASS`)

| Mã Nội thất | Model ID & DFF | Tên công trình & Cặp cửa `ENEX` | Tọa độ thực tế sau tiếp đất | `Vz` | Số mặt `.COL3` | Ảnh chụp nghiệm thu in-game | Trạng thái |
| :-: | :--- | :--- | :--- | :-: | :-: | :--- | :-: |
| `INT-01` | `6696` (`int_dawn_winery`) | Đại Sảnh Tửu Trang Dawn Winery (`MD_WIN`) | `(-4850.0, -3500.0, 1501.05)` | `0.000` | `848 F` | [`mondstadt_int_01_int_dawn_winery.png`](crash-reports/bug-snapshots/mondstadt_int_01_int_dawn_winery.png) | **`PASS`** |
| `INT-02` | `6697` (`int_angels_share`) | Quán Rượu Angel's Share 2 Tầng (`MD_ANG`) | `(-4550.0, -3500.0, 1501.05)` | `0.000` | `832 F` | [`mondstadt_int_02_int_angels_share.png`](crash-reports/bug-snapshots/mondstadt_int_02_int_angels_share.png) | **`PASS`** |
| `INT-03` | `6698` (`int_fav_cathedral`) | Chính Điện Đại Giáo Đường Favonius (`MD_CAT`) | `(-4250.0, -3500.0, 1501.05)` | `0.000` | `1,004 F` | [`mondstadt_int_03_int_fav_cathedral.png`](crash-reports/bug-snapshots/mondstadt_int_03_int_fav_cathedral.png) | **`PASS`** |
| `INT-04` | `6699` (`int_knights_hq`) | Tổng Bộ Đội Kỵ Sĩ Favonius & Phòng Jean (`MD_KNI`) | `(-3950.0, -3500.0, 1501.05)` | `0.000` | `1,040 F` | [`mondstadt_int_04_int_knights_hq.png`](crash-reports/bug-snapshots/mondstadt_int_04_int_knights_hq.png) | **`PASS`** |
| `INT-05` | `6700` (`int_cats_tail`) | Quán Rượu Đuôi Mèo (`The Cat's Tail`, `MD_TAI`) | `(-4850.0, -3200.0, 1501.05)` | `0.000` | `860 F` | [`mondstadt_int_05_int_cats_tail.png`](crash-reports/bug-snapshots/mondstadt_int_05_int_cats_tail.png) | **`PASS`** |
| `INT-06` | `6701` (`int_alchemy_lab`) | Phòng Thí Nghiệm Giả Kim Thuật (`MD_ALC`) | `(-4550.0, -3200.0, 1501.05)` | `0.000` | `660 F` | [`mondstadt_int_06_int_alchemy_lab.png`](crash-reports/bug-snapshots/mondstadt_int_06_int_alchemy_lab.png) | **`PASS`** |
| `INT-07` | `12150` (`int_spiral_abys`) | Sảnh Đấu Trường La Hoàn Thâm Cảnh Tầng 12 (`MD_ABY`) | `(-4250.0, -3213.5, 1501.00)` | `0.000` | `1,816 F` | [`mondstadt_int_07_int_spiral_abys.png`](crash-reports/bug-snapshots/mondstadt_int_07_int_spiral_abys.png) | **`PASS`** |

### 2.5. Kiểm thử Thị Giác Ban Ngày (`12:00`) & Ban Đêm (`22:00`) (`MONDSTADT_TOUR`: `8/8 PASS` Ngày & `8/8 PASS` Đêm, `0` lỗi Streaming)
- Báo cáo chi tiết Ban Ngày (`12:00`): [`visual-inspection-mondstadt-day12.md`](crash-reports/visual-inspection-mondstadt-day12.md)
- Báo cáo chi tiết Ban Đêm (`22:00`): [`visual-inspection-mondstadt-night22.md`](crash-reports/visual-inspection-mondstadt-night22.md)
- Ảnh chụp các khu chợ, quầy rèn, Hiệp Hội Nhà Mạo Hiểm, sạp hoa/quả, Đài Phun Nước & Tiệm Giả Kim có NPC hoạt động:
  - [`mondstadt_npcs_blacksmith_and_guild.png`](crash-reports/bug-snapshots/mondstadt_npcs_blacksmith_and_guild.png)
  - [`mondstadt_npcs_fruit_flower_market.png`](crash-reports/bug-snapshots/mondstadt_npcs_fruit_flower_market.png)
  - [`mondstadt_npcs_fountain_alchemy_goodhunter.png`](crash-reports/bug-snapshots/mondstadt_npcs_fountain_alchemy_goodhunter.png)

### 2.6. Kiểm thử 6 Bước Rig & Chuyển Động Nhân Vật Chính Aether (`6/6 PASS`)
- Báo cáo: [`aether-rig-test-latest.md`](crash-reports/aether-rig-test-latest.md) (`6/6 PASS`, `2,598 ms`, kiểm tra tại Cầu Đá Mondstadt `(-4084.8, -3077.8, 6.00)`).

### 2.7. Tạo Dáng Linear Blend Skinning (LBS) Cho 11 Nhân Vật Nội Thất, Áo Choàng Venti & Đóng Kín Trần Vòm (`INT-01..INT-06`)
- **Uốn xương LBS trên Blender 5.0** ([`pose_mondstadt_chars_blender.py`](file:///D:/GTA%20Archive/Staging/mondstadt-ingame-integration-2026-10-30/pose_mondstadt_chars_blender.py)): Thay thế hoàn toàn dáng đứng cứng `T-pose`/`A-pose` bằng các tư thế tự nhiên, đặc trưng cho từng nhân vật (`Diluc` khoanh tay bartending, `Venti` gảy đàn/vẫy tay, `Kaeya` chống hông thư thái, `Barbara` chắp tay cầu nguyện, `Rosaria` khoanh tay nghiêng đầu, `Jean` đặt tay trước ngực chỉ huy, `Lisa` chống hông giữ pháp khí, `Diona` lắc bình pha chế, `Albedo` trầm tư nghiên cứu, `Sucrose` ôm sổ ghi chép, `Klee` vẫy tay vui vẻ), tính toán đầy đủ trọng số đa xương (`LBS`) bao gồm cả xương tay áo (`+Left/Right Sleeve1..3`), vạt áo choàng (`+Back/Front Cask1..2`), đuôi và các đốt ngón tay.
- **Xoay hướng mặt chuẩn về phía người chơi (`rot_deg = 0.0`)** ([`patch_interiors_int01_int06.py`](file:///D:/GTA%20Archive/Staging/mondstadt-ingame-integration-2026-10-30/patch_interiors_int01_int06.py)): Xoay toàn bộ `11` nhân vật nội thất và Tượng Phong Thần Barbatos (`MSR_604549` trong `INT-03`) hướng về phía Nam (`-Y`, đối diện cửa ra vào nơi người chơi bước vào) thay vì quay lưng vào cửa.
- **Sửa áo choàng trắng của Venti thành màu xanh lục bảo chuẩn Genshin (`#187E5E`)**: Xử lý vùng mask grayscale (`x < 374, y < 640`, `sat < 0.14`, `lum > 0.42`) trên texture gốc `Avatar_Boy_Loli_Venti_Tex_Body_Diffuse.png` (vốn được tô màu bằng shader trong Genshin Impact), bake màu xanh lục bảo `rgb(24, 126, 94)` đồng thời giữ nguyên hoa văn viền vàng kim (`sat >= 0.14`), đóng gói lại `char_venti_body` vào `CUSTOM\mondstadt_m1_wilds.txd` (xem ảnh kiểm chứng cận cảnh phía sau lưng Venti: [`mondstadt_int_02_venti_cape_back.png`](crash-reports/bug-snapshots/mondstadt_int_02_venti_cape_back.png)).
- **Đóng kín trần vòm & tường thu hồi Bắc/Nam (`nz < 0`) cho `INT-01..INT-06`**: Bổ sung mái vòm gỗ/đá nghiêng 2 mái có pháp tuyến hướng xuống trong phòng (`nz < 0`) cùng 2 mảng tường tam giác thu hồi (`gable walls`), triệt tiêu hoàn toàn hiện tượng lộ bầu trời xanh phía trên các phòng nội thất.

---

## 3. Danh Mục File Đã Triển Khai & Cách Phục Hồi (Rollback)

### Các file đã cập nhật trong `gameplay-lab`:
1. `CUSTOM\mondstadt_m0_city.{img,ide,ipl,col}`
2. `CUSTOM\mondstadt_m1_wilds.{img,ide,ipl,col}`
3. `CUSTOM\mondstadt_m2_east.{img,ide,ipl,col}`
4. `data\gta.dat` & `data\water.dat`
5. `S&S\Cdimages\default\radar.img` (`30` tile radar 2D vùng Mondstadt)
6. `S&S\Cdimages\default\paths.img` (`9` sector `FLA4`: `959` vehicle nodes + `71` town ped nodes)
7. `data\pecore_gps_graph.pegg`, `eagle_gg_map_pois.py`, `cleo\EagleMapIndex.cache`
8. `cleo\MondstadtLifeAndBlips.cs` (`3,247` bytes)

### Hướng dẫn phục hồi (Rollback):
- Bản sao lưu nguyên trạng trước khi triển khai được lưu tại `D:\GTA Archive\Staging\mondstadt-ingame-integration-2026-10-30\backups\`.
- Để phục hồi về trạng thái trước đợt nâng cấp, copy các file trong `backups\` đè lại vào `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\` và xóa `cleo\MondstadtLifeAndBlips.cs`.
