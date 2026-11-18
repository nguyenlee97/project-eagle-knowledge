# Eagle World Texture & Landmark Studio (`tools/world-texture-studio`) — Báo Cáo Triển Khai & Hướng Dẫn Sử Dụng

- **Ngày hoàn thành**: 24/10/2026
- **Agent thực hiện**: Antigravity (`f700a3ad-8aae-437a-8b96-ef20a9a45cbe`)
- **Đích tích hợp duy nhất**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục công cụ**: [`tools/world-texture-studio/`](../../tools/world-texture-studio/)
- **Phiếu công việc**: [`docs/project-eagle/work-items/2026-10-24-antigravity-world-texture-studio.md`](work-items/2026-10-24-antigravity-world-texture-studio.md)
- **Báo cáo khảo sát nền tảng**: [`docs/project-eagle/world-texture-billboard-mural-monument-survey-2026-10-24.md`](world-texture-billboard-mural-monument-survey-2026-10-24.md)

---

## 1. Tổng Quan Kiến Trúc Công Cụ

**Eagle World Texture & Landmark Studio** là công cụ chuyên dụng (tương tự `skin-viewer` và `eagle-radio-studio`) giúp quản lý, xem trước 2D/3D, chuyển đổi (convert) và đóng gói mod bề mặt công trình Wibu cho `gta sa gameplay-lab` mà không gây ảnh hưởng tới tốc độ nạp `CStreaming` hay hiệu năng khung hình.

Công cụ tách bạch rõ ràng **2 luồng kỹ thuật bản chất khác nhau** trong RenderWare:
1. **Luồng Bề Mặt 2D (`CAT1..CAT4` — Chỉ sửa `.TXD`, giữ nguyên 100% khung 3D `.DFF` gốc)**:
   - Áp dụng cho **Biển quảng cáo lớn (`CAT1_BILLBOARDS`)**, **Tranh tường / Graffiti / Banner dọc (`CAT2_MURALS_BANNERS_GRAFFITI`)**, **Màn hình LED / Bảng đèn Neon / Casino (`CAT3_NEON_LED_SCREENS_CASINOS`)**, và **Poster / Nhà chờ xe buýt / Mặt tiền cửa hàng / Máy bán nước (`CAT4_POSTERS_SHOPS_TRANSIT_VENDING`)**.
   - Công cụ đọc cả cặp `.DFF` + `.TXD` để **đo tỷ lệ khung hình học 3D thực tế ngoài đời (`effective_tex_aspect_wh`)** nhằm tự động bù giãn UV (chống méo mặt nhân vật khi ảnh trong `.TXD` lưu vuông `1:1` nhưng khung biển ngoài đời là `2:1` ngang hoặc `5:8` đứng), đồng thời cho phép **xoay xem trước trực tiếp trên mô hình 3D (`.DFF`) bằng Three.js WebGL** ngay trong trình duyệt.
2. **Luồng Tượng Đài & Biểu Tượng 3D (`CAT5_MONUMENTS` — Thay cả mô hình 3D `.DFF` + `.TXD`)**:
   - Áp dụng riêng cho `93` mô hình Tượng đài (`missliberty`, `sphinx01`, `atrium`, `big_cock`, `pirateship01`, `disney`...).
   - Cho phép chọn bất kỳ nhân vật anime nào từ kho **`Skin Library`** (`1,638` skins) hoặc tải lên cặp `.DFF` + `.TXD` mới $\rightarrow$ tự động gỡ bỏ `Skin PLG` / `HAnim PLG` xương động, xoay trục chuẩn Z-up, khớp chiều cao & tâm chân đế theo khung bao (`Bounding Box`) của tượng gốc, tạo **Bệ Đá Bát Giác 2 Tầng**, phủ chất liệu tượng (`Đá Cẩm Thạch Trắng`, `Vàng 24K`, `Đồng Cổ`, `Ngọc Bích`, hoặc giữ màu `Anime Figure`) và nướng màu đỉnh Ngày/Đêm (`PRELIT`).

---

## 2. Chi Tiết 4 Bộ Converter Bề Mặt 2D Chuyên Biệt (`core/converters.py`)

| Chế độ Converter | Hạng mục áp dụng | Tính năng kỹ thuật cốt lõi |
| :--- | :--- | :--- |
| **Converter A — Billboard Dual-Sync** | `CAT1_BILLBOARDS` (`121` `.TXD` Near + `100` `.TXD` LOD) | • **Tự động bù tỷ lệ UV khung 3D**: Khắc phục triệt để tình trạng `38.9%` raster biển quảng cáo lưu vuông `256×256` (`1:1`) nhưng gắn lên khung sắt `2:1`.<br>• **Nén chuẩn `DXT1` + Mipmaps** (`512×256` / `512×512` / `1024×512`) bằng `texconv.exe` (kèm bộ nén NumPy nội bộ), giúp **giảm `75% – 85%` dung lượng** so với các file biển quảng cáo `1024×512` `DXT3` đang phình trong `GROUP_B1_TEXTURES.IMG`.<br>• **Đồng bộ Kép `Near + LOD` (`auto_sync_lod`)**: Tự động dò tìm raster tương ứng trong file `*_lod.txd` cặp đôi, thu nhỏ ảnh mới xuống đúng cỡ LOD (`64×32` / `64×64` `DXT1`) và lưu vào Staging cùng lúc. |
| **Converter B — Mural, Graffiti & Tall Banner** | `CAT2_MURALS_BANNERS_GRAFFITI` (`171` `.TXD`) | • **Chế độ `mural_wall_blend`**: Trích xuất lớp vân nổi tần số cao (gạch/vữa/bê tông) từ chính bức ảnh tường gốc trong game và hòa trộn (`0%–45%`, mặc định `18%`) lên tranh anime mới để bức tranh nhìn như được sơn trực tiếp lên gạch thật.<br>• **Chế độ `graffiti_alpha`**: Giữ kênh Alpha mượt (hoặc tự động tách nền màu đơn sắc ở góc ảnh) và ép chuẩn nén **`DXT5` + Mipmaps** cho các vết sơn `tags_la*.txd`.<br>• **Chế độ `tall_banner`**: Khớp tỷ lệ phướn treo dọc (`1:2`, `1:4`) kèm hiệu ứng đổ bóng nếp gấp vải lượn sóng. |
| **Converter C — Neon, LED & Sub-Region Atlas** | `CAT3_NEON_LED_SCREENS_CASINOS` (`109` `.TXD`) | • **Thay vùng con trên Atlas (`Sub-Region / UV Island Patch`)**: Tự động phát hiện các ô tọa độ `UV` con từ `.DFF` để chỉ thay đúng 1 ô màn hình/logo trên tấm Atlas mà giữ nguyên toàn bộ các chữ đèn Neon khác nằm chung bức ảnh.<br>• **Hiệu ứng `LED Scanline & Vibrance`**: Thêm lưới điểm ảnh LED ngang/dọc và tăng độ rực màu ban đêm (`tobj`). |
| **Converter D — Poster, Bus Stop & Vending** | `CAT4_POSTERS_SHOPS_TRANSIT_VENDING` (`1,111` `.TXD`) | • **Khử giãn UV nhà chờ xe buýt**: Tự động đo khung kính đứng (`5:8` trên `bustopm.dff`) để ảnh poster đứng không bị bẹp ngang khi lưu vào raster vuông `256×256` (`CJ_BS_MENU5`).<br>• **Giữ khung viền / nút bấm máy bán nước (`preserve_border_pct`)**: Giữ nguyên phần viền kim loại, khe nhét tiền, nút bấm ở rìa ảnh gốc và chỉ lồng poster mới vào lòng khung.<br>• **Hiệu ứng mặt kính (`glass_sheen_strength`)**: Tạo vệt phản quang chéo nhẹ như nằm sau lớp kính lồng đèn. |

---

## 3. Cơ Chế Staging, Đồng Bộ Đa Archive `.IMG` & Rollback Bit-for-Bit (`core/deployer.py`)

- **Staging độc lập (`tools/world-texture-studio/data/staging/`)**:
  - Mọi thao tác Convert 2D hoặc Đúc Tượng 3D đều ghi vào `data/staging/txds/` và `data/staging/statues/` trước, cập nhật `staging_manifest.json` và cho phép kiểm tra trực quan trên Web (cả so sánh 2D Trước/Sau lẫn xoay mô hình 3D).
- **Deploy an toàn có giữ khóa `game-write.lock`**:
  - Kiểm tra tiến trình `gta_sa.exe` / `gta_pe.exe` đã đóng.
  - Tạo độc quyền thư mục khóa `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\coordination\game-write.lock` kèm `owner.json`.
  - Đồng bộ member đã sửa vào **tất cả các kho `.IMG` đang mount chứa member đó** (ví dụ cập nhật đồng thời cả bản trong `CUSTOM\GROUP_B1_TEXTURES.IMG` và bản trong `S&S\CDimages\andreas\GTA3_2.img`).
  - Trích lưu chính xác vùng sector gốc (`orig_offset_sectors`, `orig_sectors`), `32-byte directory entry` gốc và `orig_file_size` vào `data/backups/<tx_id>/`.
- **Rollback Bit-for-Bit trong 1 giây**:
  - Khôi phục đúng vùng sector gốc, trả lại `32-byte directory entry` và cắt `truncate(orig_file_size)`, đảm bảo mã băm `SHA-256` của file `.IMG` trở về **trùng khớp 100% từng bit** như trước khi Deploy.

---

## 4. Cách Khởi Chạy & Kiểm Thử

1. **Khởi chạy giao diện Web Studio (Port `8950`)**:
   - Nhấp đúp vào [`tools/world-texture-studio/Start_World_Texture_Studio.bat`](../../tools/world-texture-studio/Start_World_Texture_Studio.bat) hoặc chạy:
     ```powershell
     python tools\world-texture-studio\app.py
     ```
   - Mở trình duyệt tại: `http://127.0.0.1:8950`
2. **Chạy bộ kiểm thử tự động (`pytest`)**:
   ```powershell
   python -m pytest tools\world-texture-studio\tests\test_world_texture_studio.py -v
   ```
