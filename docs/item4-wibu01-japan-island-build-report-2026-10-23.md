# Báo Cáo Xây Dựng & Kiểm Toán Nhị Phân: Quần Đảo Đô Thị Nhật Bản Độc Lập Tại `WIBU-01` (`MKLAS` — Đầu Nam Cầu Cao Tốc #5)

- **Ngày hoàn tất:** 23/10/2026
- **Agent thực hiện:** Antigravity (`ccf7de5c-1bef-4e05-8b2b-ddc63edbe1e1`)
- **Hồ sơ khởi tạo gốc:** [item4-wibu01-japan-island-handover-and-prompt-2026-10-23.md](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/item4-wibu01-japan-island-handover-and-prompt-2026-10-23.md)
- **Thư mục Staging độc lập:** `D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\`
- **Trạng thái `gta sa gameplay-lab`:** **Chưa ghi đè (`0` file bị chạm)** — sẵn sàng cài đặt 1-Click sau khi nghiệm thu.
- **Kết quả Kiểm toán Nhị phân 5 bước (`audit_wibu01_package.py`):** **`ALL_5_AUDITS_PASSED` (`100% PASS`)**

---

## 1. Tổng Quan Kiến Trúc & Quy Hoạch Liên Hoàn Bắc → Nam (`WIBU-01`)

Quần đảo Đô thị Nhật Bản tại **`WIBU-01` (`MKLAS` — ngoài khơi Tây Nam Los Santos)** được hợp nhất từ **6 bộ mod GTA SA gốc** trong `D:\GTA Archive\Mod Donor Library\`:
1. **`Akihabara Electronic Town (#155560)`** (`75` models, `ID 11850..11924`)
2. **`Kerorin Capital 1.0 (#153898)`** (`49` models, `ID 11800..11848`)
3. **`Tháp TorreTokyo (012 Project Japan)`** (`4` models, `ID 3194..3197`)
4. **`Lâu Đài Nhật Bản (#101385)`** (`1` model, `ID 3198`)
5. **`Kawaiiboutique (#175652)`** (`1` model, `ID 3199`)
6. **`Cây Hoa Anh Đào Sakura (011 Project Japan)`** (`14` models, `ID 3200..3213`, `36` cá thể trồng dọc đại lộ)

### Phát hiện quan trọng qua kiểm thử 3D Blender & Giải pháp Liên hoàn Bắc → Nam

Khi dựng cảnh 3D lần đầu trong Blender 4.5 + DragonFF từ dữ liệu gốc của 2 khu đô thị:
- Trong **`Kerorin Capital 1.0`**, đại lộ 2 làn `kero14` bị **chặn kín ở đầu Bắc (`Y_orig = 465..525`)** bởi một tòa nhà xưởng công nghiệp lớn, trong khi **đầu Nam (`Y_orig = 320.22`)** mới là cổng đại lộ mở thông thoáng; ngoài ra mép cực Bắc của `kero01` (`Y_orig = 755.5`) còn có dãy núi giả và cầu treo trang trí.
- Ngược lại, trong **`Akihabara Electronic Town`**, đại lộ chính **`Chuo-dori` (`douro`)** là trục đường xuyên tâm mở thông cả hai đầu Bắc (`Y_aki = -2609.20`) và Nam (`Y_aki = -2818.90`), chỉ bị chặn tạm thời bởi 2 rào chắn công trường (`koujichu01`, `koujichu02`) và 2 đoạn đường dốc cụt (`douro02`, `douro03`).

Do đó, để người chơi lái xe từ **Cầu Cao Tốc #5** xuống đảo hoàn toàn thông suốt từ Bắc xuống Nam mà không đâm vào tường hay rơi xuống biển, cấu trúc tổng thể của **`WIBU-01`** được thiết kế thành **3 phân khu liên hoàn (`Y = -4551.250 -> -5420.0`)**:

| Phân khu (Bắc → Nam) | Tọa độ trục `Y` (World) | Cao độ mặt đường (`Z_surf`) | Cấu trúc & Điểm nhấn kiến trúc |
| :--- | :--- | :--- | :--- |
| **0. Điểm tiếp đất Nam Cầu Cao Tốc #5** | `Y = -4551.250` (`X = -1390.375`) | **`23.375 m`** | Nhịp cuối `gtw_road1A40` (`ID 58292`) của Cầu Cao Tốc #5 nối từ Sân bay LS (`LAX`) ra vùng biển `MKLAS`. |
| **1. Cửa ngõ Phía Bắc: Phố Điện Tử Akihabara & Quảng trường Tháp Tokyo** | `Y = -4551.250 -> -4760.950` (`209.7 m`) | **`23.375 m`** (`0.0 mm` lệch bậc!) | Độc lập tịnh tiến `(dX = -4274.885, dY = -1942.050, dZ = +10.585)`; lược bỏ 2 rào chắn `koujichu01/02` ở `.IPL` để mở thông hai đầu đại lộ `Chuo-dori` (`douro`); **Tháp Tokyo (`3194..3197`)** đặt vững chãi trên nền đảo bê tông phía Đông (`dodai02` tại `-1285.0, -4685.0, 32.35`). |
| **2. Đại lộ Hoa Anh Đào Trung tâm & Quảng trường Lâu Đài Nhật – Kawaii Plaza** | `Y = -4760.950 -> -4960.950` (`200.0 m`) | **`23.375 m`** (`0.0 mm` lệch bậc!) | Kê thêm 1 khối đế đảo bê tông cốt thép `dodai02` (`ID 11859`) tại `(-1425.0, -4860.95, 8.624)` (mặt sàn `Z = 23.144 m`) đỡ **5 nhịp đại lộ `gtw_road1A40`** (`X = -1390.375, Z_surf = 23.375 m`), hai bên là hàng cây **Sakura** cùng **Kawaiiboutique (`3199`)** & **Lâu Đài Nhật (`3198`)** tọa lạc trên thềm bê tông phía Tây nhìn thẳng ra đại lộ. |
| **3. Khu Đô thị Phía Nam: Thủ phủ Kerorin Capital (`ZERO`)** | `Y = -4960.950 -> -5420.0` (`460.0 m`) | **`23.375 m`** (`0.0 mm` lệch bậc!) | Xoay **`180°` quanh trục Z** (`q = (0, 0, 1, 0)`) quanh tâm cổng đại lộ `(391.975, 320.220, 9.219)` để đầu mở thông thoáng của đại lộ 2 làn `kero14` đón trực tiếp Đại lộ Hoa Anh Đào tại `(-1390.375, -4960.950, 23.375)` và dẫn sâu vào khu trung tâm thương mại – cảng biển phía Nam. |

---

## 2. Kết Quả Thực Thi Chi Tiết 5 Bước Kỹ Thuật

### Bước 1: Khớp Nối Cao Độ & Tọa Độ Mặt Đường Liền Khít Với Cầu Cao Tốc #5 (`0.0 mm` Step)

- **Phép biến đổi tọa độ Akihabara Electronic Town:**
  - Cổng Bắc đại lộ `Chuo-dori` (`douro` — `ID 11860`) trong hệ tọa độ gốc của mod có tâm làn đường tại `X_aki = 2884.510`, mép Bắc tại `Y_aki = -2609.200`, cao độ mặt nhựa đường `Z_surf_aki = 12.790 m` (tâm instance `Z_inst_aki = 11.630 m`).
  - Vector tịnh tiến chính xác:
    $$\Delta X = -1390.375 - 2884.510 = -4274.885\text{ m}$$
    $$\Delta Y = -4551.250 - (-2609.200) = -1942.050\text{ m}$$
    $$\Delta Z = 23.375 - 12.790 = +10.585\text{ m}$$
  - Độ lệch cao độ mặt đường tại mối nối Cầu Cao Tốc #5 `(-1390.375, -4551.250, 23.375)`: **`0.0 mm`**.
- **Phép biến đổi tọa độ Kerorin Capital (`ZERO`):**
  - Toàn bộ `49` mảnh của `Kerorin Capital` được xoay `180°` quanh trục Z trong mặt phẳng ngang và tịnh tiến về cổng Bắc Kerorin tại `(-1390.375, -4960.950, 23.375)`:
    $$X_{\text{new}} = -1390.375 - (X_{\text{orig}} - 391.975)$$
    $$Y_{\text{new}} = -4960.950 - (Y_{\text{orig}} - 320.220)$$
    $$Z_{\text{new}} = Z_{\text{orig}} + 14.156$$
    $$(q_x', q_y', q_z', q_w') = (-q_y, q_x, q_w, -q_z)$$
  - Độ lệch cao độ giữa nhịp cuối Đại lộ Hoa Anh Đào Trung tâm và mặt đường `kero14`: **`0.0 mm`**.

---

### Bước 2: Đóng Gói / Tối Ưu `.TXD` Chuẩn DXT1/DXT5 & Kiểm Toán `.COL3 < 92,768 Bytes`

#### 2.1. Tổng hợp 7 Archive `.TXD` Độc lập (Chuẩn RenderWare `0x1803FFFF` GTA SA PC)

| Tên file `.TXD` | Dung lượng | Số lượng Raster | Định dạng nén (`D3DFORMAT`) | Kiểm tra Power-of-Two (`POT`) | Mã băm `SHA-256` |
| :--- | ---: | ---: | :--- | :---: | :--- |
| **`akihabara_town.txd`** | **`52.15 MB`** (`54,683,944 B`) | **`844`** | `824` `DXT1` + `20` `DXT5` | `0` non-POT (`100% PASS`) | `05fcd5c69978d016cb6f918d85909f2fdb1e525f8d75c4c54b3fb529f985200f` |
| **`kero.txd`** | **`14.17 MB`** (`14,861,864 B`) | **`124`** | `95` `DXT1` + `29` `DXT5` | `0` non-POT (`100% PASS`) | `e3ba8f8228513f4088e3a01a336a8cdc639979281764d9354a4070a695ad652e` |
| **`wibu_sakura_trees.txd`** | **`6.11 MB`** (`6,402,344 B`) | **`34`** | `17` `DXT1` + `17` `DXT5` | `0` non-POT (`100% PASS`) | `9b60ce9a15d20c29fb40cedc88ed098b982184f827969a94431de8976e9b3d59` |
| **`kawaiiboutique_wibu.txd`** | **`2.67 MB`** (`2,804,776 B`) | **`24`** | `23` `DXT1` + `1` `DXT3` | `0` non-POT (`100% PASS`) | `7db4461e1b0640c8b43e8eba293dd4f9f39dd8b72110563c98fa0f2f2e42e1ce` |
| **`Abase.txd`** | **`2.17 MB`** (`2,274,820 B`) | **`6`** | `6` `DXT1` | `0` non-POT (`100% PASS`) | `3cd0a733e6be64891e156ac1dd4431a76f7bba745e8748c70fe2081ad6730f22` |
| **`jp_castle_wibu.txd`** | **`1.65 MB`** (`1,731,876 B`) | **`58`** | `53` `DXT1` + `4` `DXT3` + `1` `RGBA` | `0` non-POT (`100% PASS`) | `83f226e31de810442e9495933182b30293397df3fa79e476b4387eab3f1d6aed` |
| **`Abase3.txd`** | **`0.92 MB`** (`961,796 B`) | **`4`** | `4` `DXT1` | `0` non-POT (`100% PASS`) | `51410de0d39a87151962b2636903f22685d03fb7bbd3511b803371b9e4697e3d` |

- **Điểm nổi bật về tối ưu hóa `.TXD`:**
  1. **`akihabara_town.txd`**: Đóng gói toàn bộ `844` tên texture độc nhất mà `75` file `.dff` của Akihabara thực sự tham chiếu từ `860` file `.png` rời rạc, tự động chuẩn hóa mọi bức ảnh có kích thước lẻ (`non-Power-of-Two`) về lũy thừa của 2 gần nhất và nén phần cứng `BC1/DXT1` (opaque) hoặc `BC3/DXT5` (alpha biển hiệu/cây xanh).
  2. **`kero.txd`**: Nén lại toàn bộ `33` raster `RGBA32/BGRA32` không nén trong bản gốc xuống `DXT1/DXT5` (giới hạn `max_dim = 1024`), giúp dung lượng giảm từ **`34.99 MB` xuống còn `14.17 MB` (`-59.5%`)**, thấp hơn nhiều so với ngưỡng yêu cầu `< 25 MB`.
  3. **`jp_castle_wibu.txd`**: Tự động gom bổ sung `4` texture gốc (`comptwall26`, `gangwin4_LAe`, `gangwin5_LAe`, `tancolum1`) từ `contachou1_lae2.txd` và `1` texture nền bê tông (`ctmall02_64`) từ `gta3.img` để model `jp_castle_wibu` (`carlshou1_lae2.dff`) đạt **100% đủ texture độc lập**.
  4. **`wibu_sakura_trees.txd`**: Kết hợp toàn bộ `24` raster tán hoa anh đào từ `tree1.txd`..`tree3.txd` cùng `10` raster vỏ thân cây gỗ tự nhiên từ `gta_tree_boak.txd`, `gta_tree_palm.txd`, `gtatreeshi.txd`, `gtatreeshi7.txd`, `gta_proc_bush.txd` (`gta3.img`).

#### 2.2. Kiểm toán Giới hạn `.COL3 < 92,768 Bytes` (`fastman92limitAdjuster_GTASA.ini`)

- Toàn bộ **`144 / 144` khối `.COL3`** trong `models/col/wibu01_japan_island.col` (`4,086,744 bytes`) đã được kiểm tra kích thước từng entry đơn lẻ và tự động sinh hộp va chạm `COL3` chuẩn cho 2 model thiếu `.col` riêng (`kero47`, `kawaiiboutique_wibu`).
- **Khối `.COL3` lớn nhất:** `Abase2` (`TorreTokyo`) = **`87,292 bytes` `< 92,768 bytes`** (dư `5,476 bytes` an toàn dưới trần bộ nhớ tĩnh của `fastman92limitAdjuster`).

---

### Bước 3: Cấp Phát Dải ID Sạch, Chuẩn Hóa 100% Quaternion & Raycast Hàng Cây Hoa Anh Đào

| Nhóm công trình | Dải Model ID | Số lượng Model | Tên `.TXD` gắn kết | Đặc tả `.IDE` / `.IPL` |
| :--- | :---: | ---: | :--- | :--- |
| **`Kerorin Capital 1.0`** | **`11800..11848`** | `49` | `kero` | `46` `objs` + `3` `tobj` (`kero11`, `kero25`, `kero37` phát sáng ban đêm `19h–6h`). |
| **`Akihabara Electronic Town`** | **`11850..11924`** | `75` | `akihabara_town` | `62` `objs` + `13` `tobj` (biển quảng cáo neon Anime/Game bật sáng ban đêm). |
| **`Tháp TorreTokyo`** | **`3194..3197`** | `4` | `Abase`, `Abase3` | Đặt tại quảng trường phía Đông Akihabara `(-1285.0, -4685.0, 32.35)`, chuẩn hóa Quaternion từ `0.99985` về đúng `1.0000000`. |
| **`Lâu Đài Nhật Bản`** | **`3198`** | `1` | `jp_castle_wibu` | Đặt tại quảng trường phía Tây Đại lộ Trung tâm `(-1415.0, -4895.0, 26.722)`, mặt tiền quay hướng Đông nhìn ra đại lộ. |
| **`Kawaiiboutique`** | **`3199`** | `1` | `kawaiiboutique_wibu` | Đặt tại quảng trường phía Tây Đại lộ Trung tâm `(-1416.0, -4825.0, 29.152)`, mặt tiền quay hướng Đông nhìn ra đại lộ. |
| **`Cây Hoa Anh Đào Sakura`** | **`3200..3213`** | `14` | `wibu_sakura_trees` | `36` cá thể được bắn tia **Raycasting** từ `Z = +100.0 m` xuống trúng mặt vỉa hè `.COL` của Akihabara (`Z = 23.38 m`), Đại lộ Trung tâm (`Z = 23.375 m`) và Kerorin (`Z = 23.375 m`). |

- **Kiểm tra chuẩn hóa Quaternion (`0x005381D5`):** Toàn bộ **`176 / 176` dòng `inst`** trong `wibu01_japan_island.ipl` đều thỏa mãn $\left|\sqrt{q_x^2 + q_y^2 + q_z^2 + q_w^2} - 1.0\right| \le 10^{-6}$ (`0` trường hợp sai lệch).

---

### Bước 4: Đóng Gói `wibu01_japan_island.img`, Kiểm Toán Nhị Phân 5 Bước & Bộ 6 Ảnh Phối Cảnh 3D (Blender 4.5 + DragonFF)

#### 4.1. Bảng Tệp Tin Đầu Ra & Mã Băm `SHA-256` Trong Staging

| Tệp tin trong `D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\` | Kích thước | Chi tiết nội dung | Mã băm `SHA-256` |
| :--- | ---: | :--- | :--- |
| [`wibu01_japan_island.img`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/wibu01_japan_island.img) | `141,643,776 B` (`135.08 MB`) | Archive `VER2` chuẩn `2048-byte` sector, gồm **`152` entries** (`144` `.dff` + `7` `.txd` + `1` `.col`) | `30d3991cd44d8b8b5dbbd18d41f87e92de686c1a99fa918211e644ce685bc7d1` |
| [`models/col/wibu01_japan_island.col`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/models/col/wibu01_japan_island.col) | `4,086,744 B` (`3.90 MB`) | **`144` khối `COL3`**, khối lớn nhất `87,292 B` (`< 92,768 B`) | `9413f44fd88e2ea20a7c06117a407e0fe182efee36123f3427313e52fce38fa7` |
| [`data/maps/wibu01/wibu01_japan_island.ide`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/data/maps/wibu01/wibu01_japan_island.ide) | `5,983 B` | **`144` định nghĩa model** (`128` `objs` + `16` `tobj`), `0` trùng ID với `64,617` ID của Lab | `7c6b8e93441610817d84878d8ce4c94e3456ad437b788130c247d3ec3f1b83da` |
| [`data/maps/wibu01/wibu01_japan_island.ipl`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/data/maps/wibu01/wibu01_japan_island.ipl) | `18,987 B` | **`176` instances** (`140` công trình/mặt đường + `36` cây Hoa Anh Đào), `100%` Quaternion chuẩn | `9d8d28424aec639f44f5ad49317f3941964cb498a1e290e5d9eb4f5478cf3466` |
| [`audit_report.json`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/audit_report.json) / [`manifest.json`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/manifest.json) | `4,230 B` | Kết quả kiểm toán tự động 5 bước (`ALL_5_AUDITS_PASSED`, `1,792/1,792` DFF texture refs khớp `100%`) | — |

#### 4.2. Bộ 6 Ảnh Chụp Phối Cảnh 3D Thực Tế (Blender 4.5 + DragonFF — `1280×720` Cycles)

Toàn bộ `176` đối tượng `.IPL` của `WIBU-01` cùng các nhịp cuối của **Cầu Cao Tốc #5** đã được nạp trực tiếp từ `.DFF` + `.TXD` thực tế trong gói Staging vào **Blender 4.5 LTS + DragonFF** để kiểm tra trực quan từ 6 góc máy:

1. **Mối nối Điểm Tiếp Đất Nam Cầu Cao Tốc #5 & Đại lộ Akihabara (`0.0 mm` Step):**
   - File: [`docs/project-eagle/wibu01-3d-captures/01_bridge5_touchdown_seam.png`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/wibu01-3d-captures/01_bridge5_touchdown_seam.png)
   - Mặt đường 2 làn kẻ vạch vàng của Cầu Cao Tốc #5 nối phẳng tuyệt đối vào vạch qua đường (crosswalk) đầu Bắc đại lộ `Chuo-dori` của Akihabara tại `(-1390.375, -4551.250, 23.375)` kèm 2 hàng cây Hoa Anh Đào đón khách.
2. **Đại lộ Điện tử Akihabara (`Chuo-dori Electric Town`):**
   - File: [`docs/project-eagle/wibu01-3d-captures/02_akihabara_chuo_dori_electric_town.png`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/wibu01-3d-captures/02_akihabara_chuo_dori_electric_town.png)
   - Hẻm núi các tòa nhà thương mại Akihabara, cầu vượt đường sắt xanh lá `JR Sobu Line`, biển hiệu Anime/Game sắc nét từ `akihabara_town.txd` và hàng cây Sakura nở hồng hai bên vỉa hè.
3. **Quảng trường Tháp Tokyo (`TorreTokyo Plaza East`):**
   - File: [`docs/project-eagle/wibu01-3d-captures/03_tokyo_tower_plaza_east.png`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/wibu01-3d-captures/03_tokyo_tower_plaza_east.png)
   - Tháp Tokyo đỏ-trắng (`ID 3194..3197`) vươn cao trên nền đảo bê tông phía Đông (`dodai02`) phía sau khối phố Akihabara.
4. **Đại lộ Hoa Anh Đào Trung tâm, Kawaiiboutique & Lâu Đài Nhật Bản:**
   - File: [`docs/project-eagle/wibu01-3d-captures/04_japanese_castle_kawaii_plaza.png`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/wibu01-3d-captures/04_japanese_castle_kawaii_plaza.png)
   - Đại lộ trung tâm `gtw_road1A40` chạy trên khối đảo bê tông `dodai02` thứ hai (`Y = -4760.95 -> -4960.95`), bên phải là cửa hàng hồng **Kawaiiboutique (`3199`)** và **Lâu Đài Nhật Bản (`3198`)** rợp bóng hoa anh đào.
5. **Cổng Đại lộ Phía Nam đi vào Khu Đô thị Kerorin Capital (`ZERO`):**
   - File: [`docs/project-eagle/wibu01-3d-captures/05_kerorin_capital_skyline.png`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/wibu01-3d-captures/05_kerorin_capital_skyline.png)
   - Điểm chuyển tiếp phẳng `0.0 mm` tại `(-1390.375, -4960.950, 23.375)` từ Đại lộ Hoa Anh Đào Trung tâm đi thẳng vào đại lộ 2 làn `kero14` mở thông thoáng của **Kerorin Capital**.
6. **Toàn cảnh Quần Đảo Đô Thị Nhật Bản `WIBU-01` nhìn từ trên cao (`Full Island Aerial`):**
   - File: [`docs/project-eagle/wibu01-3d-captures/06_wibu01_full_island_aerial.png`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/wibu01-3d-captures/06_wibu01_full_island_aerial.png)
   - Cái nhìn tổng thể từ Cầu Cao Tốc #5 ở phía Bắc, xuyên qua Akihabara + Tháp Tokyo, qua Đại lộ Hoa Anh Đào + Lâu Đài Nhật + Kawaiiboutique, tới tận quần thể đô thị Kerorin Capital ở phía Nam.

---

### Bước 5: Script Cài Đặt 1-Click An Toàn & Phục Hồi Nguyên Trạng (`Rollback`)

Trong thư mục Staging `D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\` đã chuẩn bị sẵn bộ công cụ triển khai tự động tuân thủ nghiêm ngặt quy ước khóa ghi `docs/project-eagle/locks/game-write.lock`:

1. **Cài đặt vào `gta sa gameplay-lab`:**
   - Chạy [`D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\Install_Wibu01_Japan_Island.bat`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/Install_Wibu01_Japan_Island.bat) (hoặc `python Install_Wibu01_Japan_Island.py`).
   - Script sẽ tự động:
     - Kiểm tra và giữ khóa `docs/project-eagle/locks/game-write.lock`.
     - Sao lưu nguyên trạng `data/gta.dat` kèm mã băm `SHA-256` vào `backup_before_install/`.
     - Copy `wibu01_japan_island.img`, `models/col/wibu01_japan_island.col`, `models/txd/*.txd` (`7` file), `data/maps/wibu01/wibu01_japan_island.ide` và `data/maps/wibu01/wibu01_japan_island.ipl` vào `gta sa gameplay-lab`.
     - Đăng ký `IMG`, `COLFILE`, `IDE` và `IPL` của `WIBU-01` vào đúng phân đoạn trong `data/gta.dat`, rồi nhả khóa `game-write.lock`.
2. **Gỡ cài đặt / Khôi phục nguyên trạng (`Rollback`):**
   - Chạy [`D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\Rollback_Wibu01_Japan_Island.bat`](file:///D:/GTA%20Archive/Staging/wibu01-japan-island-2026-10-23/Rollback_Wibu01_Japan_Island.bat) (hoặc `python Rollback_Wibu01_Japan_Island.py`).
   - Khôi phục chính xác `data/gta.dat` (kiểm tra khớp `SHA-256` gốc) và dọn sạch toàn bộ các file của `WIBU-01` khỏi `gta sa gameplay-lab`.
