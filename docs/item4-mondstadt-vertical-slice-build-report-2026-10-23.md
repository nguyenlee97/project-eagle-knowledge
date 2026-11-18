# Báo Cáo Thi Công & Kiểm Toán Nhị Phân: Bản Mod Map Thành Mondstadt (Genshin Impact Vertical Slice — Hướng C)

**Ngày hoàn thành:** 23/10/2026  
**Phạm vi thực hiện:** Строительство / Biên dịch hoàn chỉnh gói Mod Map GTA San Andreas cho **Thành Mondstadt (Genshin Impact Vertical Slice — Hướng C)** trong vùng staging độc lập trên ổ `D:\` (`D:\GTA Archive\Staging\mondstadt-vertical-slice-2026-10-23\`) theo đúng lộ trình 5 bước của [Kế hoạch Xây dựng Thành Mondstadt](item4-genshin-mondstadt-vertical-slice-plan-2026-10-23.md), sử dụng dải Model ID độc quyền **`6710..6725`** (thuộc dải `6710..6729` đã cấp phát cho `Project Eagle`).  
**Trạng thái Runtime:** Bản `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` được **giữ nguyên 100%**, chưa ghi đè bất kỳ file runtime nào trước khi người dùng duyệt gói staging.

---

## 1. Tóm Tắt Kết Quả Thực Hiện Theo 5 Bước Kỹ Thuật

### Bước 1: Thu Thập Đế Đảo & Cầu Đá Từ `HoyoMap 3D CDN`, Chuyển Hệ Trục Tọa Độ (`Y-Up` $\rightarrow$ `Z-Up`) & Cắt 6 Phân Khu Kiến Trúc (`ID 6710..6715` + LOD `6720..6725`)

1. **Tải bổ sung khối địa hình xung quanh đảo Mondstadt từ `https://cdn.flatypus.me/genshin/game_data/`** (lưu tại [`D:\GTA Archive\Mod Donor Library\hoyomap-3d-cdn\mondstadt_blocks\`](file:///D:/GTA%20Archive/Mod%20Donor%20Library/hoyomap-3d-cdn/mondstadt_blocks)):
   - `Stages_BigWorld_2_-1_Constant_HLOD_Lod0.obj` (`972,691` bytes, `15,151` đỉnh, `9,108` mặt tam giác) & `Lod1.obj` (`117,607` bytes) kèm `BigWorldTerrain_2_-1_BaseMap.png` (`256×256`, `67,828` bytes): chứa chính xác **đế đảo đá vôi Mondstadt (`Mondstadt Island Cliff Base`)**, bờ cỏ quanh tường thành và đường đê cổng Bắc.
   - `Stages_BigWorld_2_-2_Constant_HLOD_Lod0.obj` (`1,333,328` bytes) kèm `BigWorldTerrain_2_-2_BaseMap.png`: chứa **mố cầu bờ đối diện hồ Cider Lake** tại tọa độ địa phương `X ≈ +93.14m, Y ≈ -320.95m, Z ≈ -55.38m`.
   - `Area_Mengde_City_Constant_HLOD_Lod2.obj` (`152,337` bytes) và các ô lân cận `1_-1`, `1_-2`, `-1_-1`, `-2_-1`.
2. **Phát hiện & xử lý đồng bộ hệ tọa độ giữa `Lod0`, `Lod1` và `Stages_BigWorld`**:
   - `Area_Mengde_City_Constant_HLOD_Lod0.obj` nằm ở tọa độ cục bộ quanh `(0, 0, 0)` (tương ứng tâm Teyvat `X_obj = -2275.0, Y_obj = 263.0, Z_obj = -783.0`).
   - Ngược lại, `Area_Mengde_City_Constant_HLOD_Lod1.obj` (`3,416` đỉnh, `4,200` mặt tam giác) và `Stages_BigWorld_2_-1` nằm ở **hệ tọa độ toàn cục Teyvat** (`X_obj ∈ [-2412.73, -2139.23], Y_obj ∈ [204.89, 322.07], Z_obj ∈ [-970.14, -595.66]`), đồng thời `Lod1.obj` nguyên bản không chứa dòng `vt` (UV).
   - Pipeline [`build_mondstadt_vertical_slice.py`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/build_mondstadt_vertical_slice.py) tự động tịnh tiến `offset_unity = (+2275.0, -263.0, +783.0)` trước khi ánh xạ trục `(X_gta = -X_local, Y_gta = -Z_local, Z_gta = Y_local)`, giúp `Lod1` và đế đảo `Stages_BigWorld_2_-1` khớp khít `0.00 mm` với tường thành `Lod0`, đồng thời chiếu (`spatial UV projection`) tọa độ UV từ `Lod0` sang `Lod1`.
   - Cắt lọc bỏ `45` mặt tam giác địa hình đồi thô (`coarse terrain proxy`) của `Stages_BigWorld_2_-1` nằm lọt bên trong chu vi tường thành để không đâm xuyên qua mặt đường đá lát của thành phố.
3. **Tái tạo 3D Cầu Đá Vòm Đa Nhịp (`156m`) & Cánh Quạt Cối Xay Gió (`Windmill Sails`)**:
   - Trong dữ liệu tĩnh HLOD của Unity, **Cầu Đá Chính Mondstadt** (dài `156.2m`, rộng `14.0m`, nối từ mố cổng chính `(49.62, -163.50, -52.95)` tới mố bờ nam `(93.14, -321.00, -55.38)`) và **cánh quạt gỗ của 2 Cối Xay Gió** là dynamic props riêng lẻ.
   - Pipeline đã dựng bổ sung hình học 3D chuẩn xác cho **Cầu Đá 7 Nhịp Vòm** (mặt đường đá lát, lan can đá có trụ đỡ, vòm cầu và trụ đá cắm xuống lòng hồ Cider Lake) tích hợp vào phân khu `ID 6715` (`md_island_bridge`), cùng **2 bộ cánh quạt gỗ 4 cánh** gắn vào đúng trục tháp cối xay gió tại `(-50.8, -56.9, -15.5)` và `(24.2, -12.7, -5.8)` thuộc phân khu `ID 6712` (`md_city_mid_knights`).
4. **Cắt thành 6 Phân Khu Kiến Trúc (`ID 6710..6715`) & 6 LOD Tầm Xa (`ID 6720..6725`)**:
   - Mỗi phân khu được dịch về tâm riêng (`Local Bounding Center Pivot = (0, 0, 0)`) để tối ưu hóa độ chính xác số thực 16-bit của `COL3` và bán kính `Bounding Sphere` của RenderWare:

| Model ID (Near) | Tên Model (`.dff` / `.col`) | LOD ID (Far) | Tên LOD (`.dff`) | Số Đỉnh (Near) | Số Mặt Tam Giác (Near) | Mặt `COL3` (`FaceGroups`) | Bán Kính `Sphere` | Tâm Pivot Cục Bộ `(X, Y, Z)` |
| :--- | :--- | :--- | :--- | ---: | ---: | ---: | ---: | :--- |
| **`6710`** | `md_city_gate_walls` | **`6720`** | `lod_md_gate_walls` | `5,858` | `3,454` | `3,454` (`72` FG) | `130.89 m` | `(11.112, -77.143, -36.738)` |
| **`6711`** | `md_city_lower_plaza` | **`6721`** | `lod_md_lower_plaza` | `4,451` | `2,622` | `2,622` (`55` FG) | `110.85 m` | `(23.849, -104.318, -33.974)` |
| **`6712`** | `md_city_mid_knights` | **`6722`** | `lod_md_mid_knights` | `3,577` | `2,153` | `2,153` (`45` FG) | `120.60 m` | `(-3.233, -14.370, -12.032)` |
| **`6713`** | `md_city_barbatos_plaza` | **`6723`** | `lod_md_barbatos` | `1,889` | `1,271` | `1,269` (`27` FG) | `80.38 m` | `(-48.623, 29.489, -17.343)` |
| **`6714`** | `md_city_cathedral` | **`6724`** | `lod_md_cathedral` | `2,091` | `1,089` | `1,089` (`23` FG) | `96.10 m` | `(-73.276, 119.780, 10.532)` |
| **`6715`** | `md_island_bridge` | **`6725`** | `lod_md_island_bridge` | `1,865` | `1,253` | `1,253` (`27` FG) | `341.97 m` | `(2.989, -69.927, -42.940)` |
| **Tổng** | **6 Phân khu cận cảnh** | **Tổng** | **6 Phân khu LOD** | **`19,731`** | **`11,842`** | **`11,840` (`249` FG)** | — | — |

---

### Bước 2: Nâng Cấp Độ Sắc Nét Texture Cận Cảnh & Tách Vật Liệu Mặt Đường / Cầu Thang / Thảm Cỏ (`.TXD`)

1. **Remaster & Tách Kênh Vật Liệu (`Material Splitting`)**:
   - Từ `Area_Mengde_City_Constant_HLOD_Combined_Diffuse.png` (`512×512`) và `BigWorldTerrain_2_-1_BaseMap.png` (`256×256`), thuật toán nội suy Bicubic kết hợp Unsharp Mask và tổng hợp hạt chi tiết tần số cao (`High-Frequency Procedural Micro-Detail Overlay`: mạch gạch đá vôi, vân đá cuội lát đường, rãnh bậc thang và sợi cỏ xanh) đã nâng cấp lên bộ 6 texture cận cảnh chuẩn `1024×1024` / `512×512` (lưu tại [`textures_remastered/`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/textures_remastered)):
     - `md_city_atlas` (`1024×1024`): Tường gạch khung gỗ Tudor, mái ngói đỏ cam/xanh lam, đại giáo đường Favonius và tượng Phong Thần Barbatos.
     - `md_road_cobble` (`1024×1024`): Mặt đường đá lát quảng trường và phố đi bộ (tăng cường vân khe gạch đá cuội chống nhòe khi camera đặt sát sau lưng Aether).
     - `md_stairs_stone` (`1024×1024`): Bậc cầu thang đá dẫn lên Hiệp Sĩ Đoàn và Đại Giáo Đường.
     - `md_lawn_grass` (`1024×1024`): Thảm cỏ bồn hoa nội đô.
     - `md_island_cliff` (`1024×1024`): Vách đá vôi và bờ cỏ đảo Mondstadt giữa hồ Cider.
     - `md_bridge_stone` (`512×512`): Vật liệu đá lát và thành cầu vòm cổng chính.
2. **Đóng gói 2 Từ Điển Texture RenderWare `.TXD` (`0x1803FFFF` — GTA SA PC)**:
   - [`mondstadt_city.txd`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/models/txd/mondstadt_city.txd) (`22,020,904` bytes, `6` rasters `D3DFMT_A8R8G8B8`, Filter `FILTERLINEARMIPLINEAR`, Anisotropy `16x`).
   - [`lod_mondstadt.txd`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/models/txd/lod_mondstadt.txd) (`2,097,448` bytes, `2` rasters `512×512`: `md_lod_atlas`, `md_island_lod`).

---

### Bước 3: Biên Dịch `.DFF` (Nướng Vertex Prelight Ngày/Đêm + `2dfx`) & `.COL` (`COL3` Phân Loại Vật Liệu Bước Chân)

1. **Biên dịch 12 File `.DFF` (`RenderWare 3.6.0.3` / `0x1803FFFF`)**:
   - Cấu trúc nhị phân khớp chuẩn `gta_pe.exe`: `Clump (0x10)` $\rightarrow$ `FrameList (0x0E)` $\rightarrow$ `GeometryList (0x1A)` $\rightarrow$ `Geometry (0x0F)` (cờ `0x0001007E`: `TRISTRIP=0, POSITIONS, TEXTURED, PRELIT, NORMALS, LIGHT, MODULATE`, thứ tự index tam giác `<HHHH` `v2, v1, mat_id, v3`) $\rightarrow$ `MaterialList (0x08)` $\rightarrow$ `BinMeshPLG (0x050E)` $\rightarrow$ `ExtraVertColour (0x0253F2F9)` $\rightarrow$ `2dfx (0x0253F2F8)` $\rightarrow$ `Atomic (0x14)`.
   - **Vertex Prelight Ban Ngày (`Day Prelight`)**: Nướng trực tiếp ánh sáng mặt trời hướng Đông-Nam kết hợp bóng đổ khe hẹp (`Height + Concavity Ambient Occlusion`), giúp chân tường, gầm mái hiên và hốc cửa có chiều sâu 3D tự nhiên.
   - **Vertex Prelight Ban Đêm (`ExtraVertColour` `0x0253F2F9`)**: Header 4-byte (`uint32 = 1`) kèm mảng màu RGBA ban đêm (`rgb(42, 52, 82)` dịu mát trên tường đá/mái ngói, kết hợp ánh sáng vàng cam ấm `rgb(255, 205, 125)` hắt ra từ các ô cửa sổ quán rượu/nhà dân và hào quang xanh ngọc `Anemo` `rgb(110, 245, 210)` quanh chân tượng Barbatos).
   - **Đèn Đêm `2dfx` (`0x0253F2F8`)**: Gắn tổng cộng **`30` nguồn sáng điểm `2dfx` (`CORONA_ONLY` / `SHOW_ALWAYS_AT_NIGHT`, cấu trúc chuẩn `100 bytes/light`)** dọc theo cầu đá, cổng chính, quảng trường đài phun nước, trụ sở Hiệp Sĩ Đoàn, tượng Phong Thần và Đại Giáo Đường.
2. **Biên dịch Archive Va Chạm [`mondstadt_city.col`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/models/col/mondstadt_city.col) (`COL3`, `161,108` bytes, 6 phân khu)**:
   - Mỗi phân khu đều có `num_faces < 3,500` (thấp hơn rất nhiều so với ngưỡng an toàn `15,000` mặt của GTA SA), có bảng `FaceGroups` (`28 bytes/nhóm`, tối đa `50` tam giác/nhóm) để bộ giải va chạm của GTA SA truy vấn `AABB` siêu tốc.
   - Tự động phân loại **Surface Material ID** theo độ dốc pháp tuyến `n_z` và sắc độ màu gốc để kích hoạt đúng âm thanh bước chân & hiệu ứng bụi/vết lốp cho Aether:
     - `SURF_PAVEMENT (4)`: **`2,077` mặt** đường đá lát, cầu đá, hành lang và bậc thang (`n_z > 0.65`).
     - `SURF_GRASS_SHORT_LUSH (9)`: **`642` mặt** bồn cỏ nội đô và triền cỏ xanh đảo Mondstadt.
     - `SURF_ROCK_CLIFF (36)`: **`315` mặt** vách đá vôi dựng đứng quanh chân đảo.
     - `SURF_ROOF_SHINGLE (43)`: **`745` mặt** mái ngói nghiêng của các ngôi nhà.
     - `SURF_CONCRETE (5)`: **`8,061` mặt** tường thành đá, tháp canh, cột trụ và lan can.

---

### Bước 4: Khởi Tạo `.IDE` / `.IPL` (Raycasting Cây Xanh & Đèn Đường + Quaternions Chuẩn Hóa)

1. **Định nghĩa vật thể [`mondstadt_city.ide`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/data/maps/mondstadt/mondstadt_city.ide)**:
   - Khai báo `6` model cận cảnh (`6710..6715`, `DrawDistance = 295.0 < 300.0` để kích hoạt `.COL` vật lý và liên kết LOD) và `6` model LOD tầm xa (`6720..6725`, `DrawDistance = 1500.0`).
2. **Định vị không gian `.IPL` (hỗ trợ 2 phương án tọa độ sẵn sàng nạp vào game)**:
   - **Phương án 1 (Mặc định khuyến nghị — `WIBU-06` Vịnh Bắc Sandar / Đông Bắc Bản Đồ)**: [`mondstadt_city.ipl`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/data/maps/mondstadt/mondstadt_city.ipl) đặt tâm đảo Mondstadt tại **`(6200.0, -3200.0, 59.5)`**, nơi mặt hồ Cider khớp với mực nước biển `Z = 0.0m`, quảng trường cổng thành ở `Z ≈ +9.0m` và đỉnh Đại Giáo Đường ở `Z ≈ +123.0m`.
   - **Phương án 2 (Tùy chọn gần bờ Los Santos — `WIBU-05` Vịnh Nam LS)**: [`mondstadt_city_ls_bay.ipl`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/data/maps/mondstadt/mondstadt_city_ls_bay.ipl) đặt tâm đảo tại **`(550.0, -3650.0, 59.5)`** ngay phía Nam bãi biển Los Santos.
   - Cả 2 file `.IPL` đều liên kết chính xác từng cặp `Near Model (6710..6715)` với `LOD Index (6..11)` tương ứng, kèm **`23` prop cảnh quan** (cây xanh `620`, `700`, `712` và cột đèn cổ điển `1223`) được bắn tia `Raycasting` thẳng xuống bề mặt tam giác `Lod0` để lấy độ cao `Z` chính xác tới từng milimét. Toàn bộ `35` dòng `inst` đều đạt chuẩn hóa Quaternion `|qx² + qy² + qz² + qw² - 1.0| = 0.000000 < 0.02` (vượt qua kiểm tra `0x005381D5` của `gta_pe.exe`).

---

### Bước 5: Đóng Gói `mondstadt_city.img` (`VER2`) & Kiểm Toán Nhị Phân Offline + Kết Xuất 4 Ảnh Preview 3D

1. **Đóng gói [`mondstadt_city.img`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/mondstadt_city.img)**:
   - Chuẩn `VER2` (`25,651,200` bytes / `24.46 MB`), chứa đầy đủ **`15` file thành viên** (`6` near `.dff`, `6` LOD `.dff`, `2` `.txd`, `1` `.col`), căn lề sector `2048 bytes`.
2. **Kiểm toán nhị phân tự động (`5/5 PASS`)**:
   - `TXD_BINARY_HEADER`: `PASS` (`root=0x16, size=22020892, ver=0x1803ffff, textures=6`).
   - `COL3_ARCHIVE_INTEGRITY`: `PASS` (`entries=6, max_faces=3454 (<4000), exact_eof=True`).
   - `DFF_12_MODELS_AND_PRELIGHT_CHUNKS`: `PASS` (Cả 12 file `.dff` có đầy đủ `Clump`, `FrameList`, `Geometry 0x1007E`, `BinMeshPLG`, `ExtraVertColour`, `2dfx`, `Atomic`).
   - `IPL_QUATERNIONS_AND_LOD_LINKS`: `PASS` (`total_instances=35, bad_quats=0, near_lod_pairs=6`).
   - `IMG_VER2_ARCHIVE`: `PASS` (`magic=VER2, files=15, total_bytes=25651200`).
3. **4 Ảnh Preview 3D Kết Xuất Trực Tiếp Từ Các File `.DFF` + `.TXD` + `.COL` Đã Biên Dịch**:
   - [Toàn cảnh Ban Ngày (`preview_day_overview.png`)](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/previews/preview_day_overview.png)
   - [Toàn cảnh Ban Đêm + Đèn `2dfx` (`preview_night_prelight.png`)](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/previews/preview_night_prelight.png)
   - [Bản đồ Phân loại Vật liệu Va chạm `COL3` (`preview_col_materials.png`)](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/previews/preview_col_materials.png)
   - [Cận cảnh Cầu Đá 7 Nhịp Vòm, Cổng Chính & Cối Xay Gió (`preview_bridge_and_gate.png`)](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/previews/preview_bridge_and_gate.png)

---

## 2. Danh Mục File & Mã Băm `SHA-256` Trong Vùng Staging (`D:\`)

Thư mục gốc Staging: [`D:\GTA Archive\Staging\mondstadt-vertical-slice-2026-10-23\`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23)

| Thành Phần | Đường Dẫn File | Kích Thước (Bytes) | Mã Băm `SHA-256` |
| :--- | :--- | ---: | :--- |
| **IMG Archive (`VER2`)** | [`mondstadt_city.img`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/mondstadt_city.img) | `25,651,200` | `103195321F23D83EC4B898C3C7DB6B02554667D9021F242D437766A228644D45` |
| **IDE Definitions** | [`data/maps/mondstadt/mondstadt_city.ide`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/data/maps/mondstadt/mondstadt_city.ide) | `1,004` | `0F0495D50FA1F5AB98B1AD4A959D7184791622039B215B67367AE5965CD7E003` |
| **IPL (`WIBU-06` Sandar Bay)** | [`data/maps/mondstadt/mondstadt_city.ipl`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/data/maps/mondstadt/mondstadt_city.ipl) | `2,331` | `7126335E3B31FC47D64F282B8989F12C5A3B52F381845DA78475FCE0A5404E67` |
| **IPL (`WIBU-05` South LS Bay)** | [`data/maps/mondstadt/mondstadt_city_ls_bay.ipl`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/data/maps/mondstadt/mondstadt_city_ls_bay.ipl) | `2,315` | `F53CEB5AD2A768F72C21CDD3F6FA9B1C90209D455C18455657DBB4EB579EC165` |
| **COL3 Collision Archive** | [`models/col/mondstadt_city.col`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/models/col/mondstadt_city.col) | `161,108` | `C4FA4BBCAA15C78ED3A8AEE98707CBCEBB312FAA2AEBC2D5E8AB1F9FAD55EA64` |
| **Near Texture Dictionary** | [`models/txd/mondstadt_city.txd`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/models/txd/mondstadt_city.txd) | `22,020,904` | `4914EEF96D0156D5E55B4BFF6BC7E0FB8BACCA01479E532392EF9CB099C6C7E0` |
| **LOD Texture Dictionary** | [`models/txd/lod_mondstadt.txd`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/models/txd/lod_mondstadt.txd) | `2,097,448` | `5D1C68540D95DD1647CC8C2CEB212E239681CC9DE568F84F03848639E0EB8E18` |
| **Manifest & Audit JSON** | [`manifest.json`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/manifest.json) | `14,724` | — |
| **Script Biên Dịch Nguồn** | [`build_mondstadt_vertical_slice.py`](file:///D:/GTA%20Archive/Staging/mondstadt-vertical-slice-2026-10-23/build_mondstadt_vertical_slice.py) | `84,962` | — |

---

## 3. Hướng Dẫn Nạp Thử Nghiệm Vào `gta sa gameplay-lab` (Khi Có Lệnh Triển Khai)

Khi người dùng muốn nạp gói **Thành Mondstadt (Vertical Slice)** từ staging vào `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`:

1. **Cách 1 — Qua ModLoader (Khuyến nghị để bật/tắt không chạm vào file gốc)**:
   - Tạo thư mục `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\modloader\MondstadtVerticalSlice\`.
   - Copy `models\dff\*.dff`, `models\txd\*.txd`, `models\col\mondstadt_city.col` và `data\maps\mondstadt\mondstadt_city.ide` + `mondstadt_city.ipl` vào thư mục đó.
2. **Cách 2 — Qua `gta.dat` của Project Eagle**:
   - Copy `mondstadt_city.img` vào `models\mondstadt_city.img` và thư mục `data\maps\mondstadt\` vào `data\maps\mondstadt\`.
   - Thêm 3 dòng vào `data\gta.dat`:
     ```text
     IMG MODELS\MONDSTADT_CITY.IMG
     IDE DATA\MAPS\MONDSTADT\MONDSTADT_CITY.IDE
     IPL DATA\MAPS\MONDSTADT\MONDSTADT_CITY.IPL
     ```
3. **Tọa độ Teleport để Aether dịch chuyển tới ngay trước Cầu Đá Cổng Chính Mondstadt**:
   - Tại vịnh Bắc Sandar (`WIBU-06`, file `mondstadt_city.ipl`):
     - **Đầu Cầu Đá Mondstadt**: `X = 6293.0, Y = -3520.0, Z = 6.5`
     - **Quảng Trường Đài Phun Nước (Cổng Thành)**: `X = 6235.0, Y = -3325.0, Z = 10.5`
     - **Quảng Trường Tượng Phong Thần Barbatos**: `X = 6155.0, Y = -3190.0, Z = 43.5`
   - Tại vịnh Nam Los Santos (`WIBU-05`, nếu dùng file `mondstadt_city_ls_bay.ipl`):
     - **Đầu Cầu Đá Mondstadt**: `X = 643.0, Y = -3970.0, Z = 6.5`
     - **Quảng Trường Đài Phun Nước (Cổng Thành)**: `X = 585.0, Y = -3775.0, Z = 10.5`
     - **Quảng Trường Tượng Phong Thần Barbatos**: `X = 505.0, Y = -3640.0, Z = 43.5`
