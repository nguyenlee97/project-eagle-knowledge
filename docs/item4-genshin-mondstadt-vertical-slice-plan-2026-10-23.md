# Hạng mục 4 — Kế Hoạch & Hồ Sơ Bàn Giao Khởi Tạo Hội Thoại Mới: Xây Dựng Bản Mod GTA SA **Thành Mondstadt (Genshin Impact Vertical Slice)** Từ Starting Point `HoyoMap 3D`

- **Ngày lập**: `2026-10-23`
- **Tác giả**: `Antigravity`
- **Mục tiêu hội thoại mới**: Thực thi **Hướng C (`Vertical Slice Prototype`)** — sử dụng dữ liệu 3D của **Thành Mondstadt (`Area_Mengde_City`)** đã tải sẵn trên ổ `D:\` làm `Starting Point` để chế tác, nâng cấp và biên dịch thành một **Bản Mod Map GTA San Andreas (`.dff`, `.txd`, `.col`, `.ide`, `.ipl`) chất lượng cao** dành cho `Project Eagle` (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`).
- **Tài liệu nền tảng liên quan**:
  - [Showcase HTML — Đại danh mục & Báo cáo giải phẫu Map/Building Anime](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/item4-public-anime-wibu-mods-showcase-2026-10-23.html)
  - [Báo cáo bóc tách Kỳ 3 & Kỳ 4 (`HoyoMap CDN` & Thế giới Anime)](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/item4-mod-decomposition-ky3-ky4-touge-anime-worlds-2026-10-23.md)
  - [Tài liệu tham chiếu Bộ công cụ AI Modding của Dryxio (`Ariane`, `GTA-Scout`)](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/dryxio-gta-ai-modding-toolkit-reference-2026-10-23.md)

---

## 1. Tài Nguyên Đầu Vào (`Starting Point`) Đã Có Sẵn Trên Ổ `D:\`

Thư mục lưu trữ vật lý: `D:\GTA Archive\Mod Donor Library\hoyomap-3d-cdn\`

| Tên File Trên Ổ `D:\` | Dung Lượng | Thông Số Hình Học Đã Đo Đạc | Vai Trò Trong Pipeline Xây Dựng Mondstadt |
| :--- | :--- | :--- | :--- |
| **`Area_Mengde_City_Constant_HLOD_Lod0.obj`** | `2.07 MB` | `17,158` đỉnh (`v`), `17,158` UV (`vt`), `10,277` mặt tam giác (`f`). Kích thước bao (`Bounding Box` hệ tọa độ Unity `Y-Up`): `X = [-137.73..135.77m]` (`rộng 273.50m`), `Z = [-187.14..187.34m]` (`dài 374.48m`), `Y = [-58.11..59.07m]` (`cao 117.18m`). | **Khung hình học 3D chính (`Base Geometry & Layout 1:1`)** của toàn bộ Thành Mondstadt (từ cổng thành, khu phố dưới, bậc thang, cối xay gió đến quảng trường Tượng Phong Thần Barbatos và Đại Giáo Đường Tây Phong). |
| **`Area_Mengde_City_Constant_HLOD_Lod1.obj`** | `0.41 MB` | `3,416` đỉnh (`v`), `4,200` mặt tam giác (`f`). | **Mô hình LOD nhìn từ xa (`Draw Distance 1500m`)** cho phép nhìn thấy toàn cảnh Thành Mondstadt từ ngoài khơi Vịnh Sandar (`WIBU-06`). |
| **`Stages_Texture_Area_Mengde_City_HLOD_Combined_Diffuse.png`** | `1.14 MB` | Ảnh `PNG` gộp (`Combined Diffuse Atlas`). | **Texture nền cho lớp LOD xa** và là bản đồ tham chiếu màu/UV để tách vùng vật liệu cận cảnh (`High-Res Tileable Material Remaster`). |
| **`all_hlod_manifest.json` & `android_manifest.json` & `overrides.json`** | `725 KB` | Tọa độ gốc của Mondstadt trong thế giới Teyvat: `pos = (2275.0, 263.0, -783.0)`, nằm tại ô lưới `BigWorld` `2_-1` / `-2_-1`. | Dùng để tải bổ sung **địa hình đảo đá & cầu đá cổng thành Mondstadt (`BigWorld TerrainMesh` & `Stages_BigWorld HLOD`)** từ `https://cdn.flatypus.me/genshin/game_data/` để ghép liền chân tường thành xuống mặt nước biển! |

---

## 2. Quy Hoạch Dải Model ID & Tọa Độ Đích Trong `Project Eagle` (`gta sa gameplay-lab`)

- **Dải Model ID Độc Quyền Đã Cấp Phát Sẵn**: **`6710 .. 6729` (`20` IDs)** nằm trong **Khối ID trống `6526..6862` (`337` IDs sạch `0%` xung đột)** của `Project Eagle`.
  - Cho phép chia Thành Mondstadt thành **tối đa `10` phân khu/khối kiến trúc cận cảnh (`6710..6719`)** + **`10` mô hình LOD/cảnh quan phụ trợ (`6720..6729`)** thay vì nhồi cả thành phố vào 1 file duy nhất!
- **Phân Khu Đặt Tọa Độ (`Target Zone`)**:
  - **Phương án 1 (Mặc định trong Quy hoạch `WIBU-06`)**: Bờ Bắc **Đại Vịnh Sandar** (`X ≈ 12500, Y ≈ -8500, Z ≈ 15.0`).
  - **Phương án 2 (Thuận tiện kiểm thử nhanh gần Los Santos)**: Đặt tại vùng biển/đảo trống phía Tây Nam Los Santos (`WIBU-01` / `WIBU-05`) hoặc tạo phím dịch chuyển nhanh để **Aether** bay tới kiểm tra ngay khi vào game.

---

## 3. Lộ Trình Kỹ Thuật 5 Bước ("Vertical Slice Pipeline") Cho Hội Thoại Mới

Khi bắt đầu hội thoại mới, Agent sẽ tiến hành tuần tự 5 bước kỹ thuật sau:

### Bước 1 — Tải Bổ Sung Đế Đảo & Cầu Đá Mondstadt + Phân Cụm Hình Học (`Spatial & Connected-Component Slicing`)
1. Quét `android_manifest.json` quanh tọa độ `(2275, 263, -783)` để tải thêm mảnh địa hình đảo Mondstadt & cầu đá dẫn vào cổng thành từ CDN `https://cdn.flatypus.me/genshin/game_data/`.
2. Chuyển hệ trục tọa độ từ **Unity (`X, Y-Up, Z`, Left-handed)** sang **GTA San Andreas RenderWare (`X, Y-Forward, Z-Up`, Right-handed)**:
   - Công thức biến đổi đỉnh: $(X_{\text{GTA}}, Y_{\text{GTA}}, Z_{\text{GTA}}) = (X_{\text{Unity}}, Z_{\text{Unity}}, Y_{\text{Unity}})$.
   - Đảo thứ tự đỉnh mặt tam giác (`f v1 v3 v2`) để pháp tuyến (`Normal`) hướng ra ngoài chuẩn 100%, và lật trục $V$ của UV ($V_{\text{GTA}} = 1.0 - V_{\text{Unity}}$) nếu cần khớp ảnh `.PNG`.
3. **Cắt (Slice) `Area_Mengde_City_Constant_HLOD_Lod0.obj` thành 5–6 cụm kiến trúc riêng biệt** (theo tọa độ độ cao/khu vực và `Connected Components`):
   - **Phân khu 1 (`ID 6710`)**: Cổng Thành Chính, Tường Thành Ngoài & Tháp Canh (`Main Gate & Outer Walls`).
   - **Phân khu 2 (`ID 6711`)**: Quảng Trường Đài Phun Nước & Khu Phố Thương Mại Thấp (`Lower Commercial District & Fountain Plaza`).
   - **Phân khu 3 (`ID 6712`)**: Khu Phố Trung Tầng, Trụ Sở Đội Kỵ Sĩ Tây Phong & Cối Xay Gió (`Middle District, Knights HQ & Windmills`).
   - **Phân khu 4 (`ID 6713`)**: Quảng Trường Cao & Tượng Phong Thần Barbatos (`Barbatos Statue Plaza & Grand Stairs`).
   - **Phân khu 5 (`ID 6714`)**: Đại Giáo Đường Tây Phong (`Favonius Cathedral`).
   - **Phân khu 6 (`ID 6715`)**: Đế Đảo Đá & Cầu Đá Dẫn Vào Thành (`Mondstadt Island Base & Stone Bridge`).

### Bước 2 — Nâng Cấp Độ Sắc Nét Texture Cận Cảnh (`Texture & Material Remastering`)
- Để khắc phục nhược điểm ảnh `Combined_Diffuse.png` (`1.14 MB`) bị mờ khi Aether đứng gần:
  1. Nâng cấp độ phân giải (`4x Upscale + Sharpen Detail`) cho atlas `Stages_Texture_Area_Mengde_City_HLOD_Combined_Diffuse.png` lên `4096×4096` (hoặc chia thành 4 sub-atlas `2048×2048` riêng cho từng phân khu để không bị giới hạn kích thước raster).
  2. Tách các mặt sàn đá lát đường, bậc cầu thang và mặt cỏ (dựa vào góc pháp tuyến mặt phẳng $N_z > 0.75$ và màu sắc vùng UV) để có thể gán thêm **Detail Texture / High-Res Cobblestone & Grass** sắc nét dưới chân nhân vật.

### Bước 3 — Sinh Dữ Liệu Va Chạm `.COL` Chuẩn Vật Liệu Bước Chân & Nướng Ánh Sáng Đỉnh (`Vertex Prelight Day/Night`)
1. **Biên dịch file `mondstadt_city.col` (`COL3`)**:
   - Mọi phân khu (`6710..6715`) có khối `.col` riêng với số mặt tam giác `< 4,000 faces / model` (cực nhẹ và an toàn tuyệt đối cho engine vật lý GTA SA).
   - Tự động phân loại `Surface Material ID` của GTA SA dựa theo độ dốc và màu sắc:
     - Mặt phẳng ngang màu xám/trắng $\rightarrow$ **Đá lát đường / Bậc thang (`PAVEMENT` / `STONE`)**;
     - Mặt phẳng ngang màu xanh lá $\rightarrow$ **Thảm cỏ (`GRASS`)**;
     - Mặt đứng $\rightarrow$ **Tường đá / Gỗ (`WALL` / `WOOD`)**.
2. **Nướng `Vertex Prelight` (Ngày & Đêm) trực tiếp vào `.DFF`**:
   - Tính toán `Ambient Occlusion` giả lập theo hướng pháp tuyến mặt trời ($L = \text{normalize}(0.4, 0.3, 0.85)$) và độ cao $Z$ để:
     - **Ban ngày (`Day Prelight`)**: Sáng trong trẻo kiểu Anime (`RGB ≈ 235..255` ở mặt đón nắng, `170..195` ở mặt khuất bóng).
     - **Ban đêm (`Night Prelight`)**: Ánh trăng xanh dịu (`RGB ≈ 75, 85, 110`) kết hợp màu vàng ấm (`RGB ≈ 240, 190, 110`) tại các vùng cửa sổ sáng đèn!

### Bước 4 — Bổ Sung Cảnh Quan Sống Động (`Prop & Vegetation Dressing`)
- Trên nền hình học đã cắt của Thành Mondstadt, đặt bổ sung các prop cận cảnh bằng `.IPL`:
  - Cây xanh, bồn hoa, bụi cỏ quanh thành;
  - Đèn đường cổ điển và hiệu ứng ánh sáng đêm `2dfx` tại cổng thành, quảng trường đài phun nước và lối lên Đại Giáo Đường.

### Bước 5 — Kiểm Tra Bằng `Dryxio/ariane` Hoặc Đóng Gói Staging Kiểm Thử Trong `gameplay-lab`
- Xuất trọn bộ `mondstadt_city.img` (`.dff`, `.txd`, `.col`) + `mondstadt_city.ide` (`ID 6710..6725`) + `mondstadt_city.ipl` trong thư mục staging riêng trước khi nạp thử nghiệm cho nhân vật **Aether** chạy bộ kiểm tra từng bậc cầu thang!
