# Báo Cáo Bàn Giao Kỹ Thuật: Sector M2 — Bờ Đông & Bán Đảo Đông-Nam Mondstadt (`mondstadt_east_m2`)

- **Ngày hoàn thành**: `2026-10-25`
- **Tác nhân thực hiện**: `Antigravity`
- **Trạng thái**: `completed_in_staging` (`0` ghi đè vào `Sector M0`, `Sector M1` hay `Project Eagle\gta sa gameplay-lab`)
- **Thư mục Staging độc lập**: [`D:\GTA Archive\Staging\teyvat-mondstadt-east-m2-2026-10-25\`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/)
- **Trình xem 3D WebGL Hợp nhất (`M0 + M1 + M2`)**: [`mondstadt-m2-east-coast-showcase-2026-10-25.html`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/mondstadt-m2-east-coast-showcase-2026-10-25.html) (`56.45 MB`, `sha256=a1507c6f1f2a7369dc6cd960c726e890880734927524ab14613641233b787001`)

---

## 1. Phạm Vi Địa Lý, Dữ Liệu HoyoMap CDN & Khớp Biên `0.00 mm` Với `Sector M1`

1. **Khung tọa độ `ENU` (so với tâm Thành Mondstadt `0, 0`)**:
   - **Khối chính Bờ Đông & Đảo Musk Reef (`40` mảnh `256m × 256m`, `me2_t00 .. me2_t39`)**: `dX_east ∈ [+768.0m .. +2,048.0m]` (`5` cột × `256m`), `dY_north ∈ [-1,280.0m .. +768.0m]` (`8` hàng × `256m`).
   - **Phần mở rộng Góc Đông-Nam ôm trọn 100% Hẻm Núi Dadaupa & Hồ Kiếm (`6` mảnh `me2_t40 .. me2_t45`)**: `dX_east ∈ [+240.0m .. +768.0m]`, `dY_north ∈ [-1,280.0m .. -768.0m]`.
   - **Hệ tọa độ GTA SA (`MONDSTADT_GTA_ANCHOR = -6500.0, -3500.0, +59.5`)**:
     - `dX_east = -z_obj - 783.0` → `X_gta = -z_obj - 7283.0`
     - `dY_north = -x_obj - 2275.0` → `Y_gta = -x_obj - 5775.0`
     - `dZ_up = y_obj - 263.0` → `Z_gta = y_obj - 203.5`
2. **4 Khối `HoyoMap CDN` (`Stages_BigWorld_{2_-2, 1_-2, 2_-3, 1_-3}`)**:
   - Đã tải bổ sung 2 khối bờ biển cực Đông `Stages_BigWorld_2_-3_Constant_HLOD_Lod0.obj` (`1,525` đỉnh, `2,915` mặt) và `Stages_BigWorld_1_-3_Constant_HLOD_Lod0.obj` (`2,220` đỉnh, `3,502` mặt) cùng `BigWorldTerrain_{2_-3, 1_-3}.bin_BaseMap.png` vào `D:\GTA Archive\Mod Donor Library\hoyomap-3d-cdn\mondstadt_blocks\`.
   - Khử sạch `2` token UV vô cực (`∞`) trong `1_-2` bằng `safe_float`; tính UV chiếu phẳng `generatePlanarUVs` trên toàn bộ Bounding Box `1024m × 1024m` của từng ô gốc trước khi cắt mảnh `256m` (Bài học #2 & #3).
3. **Khớp biên `0.00 mm` tuyệt đối với `Sector M1`**:
   - Toàn bộ `193` đỉnh trên đường biên Đông `dX_east = +768.0m` (`dY_north ∈ [-768.0m .. +768.0m]`) và `67` đỉnh trên đường biên Nam `dY_north = -768.0m` (`dX_east ∈ [+240.0m .. +768.0m]`) được khóa cứng vào độ cao `Z` thực tế của `Sector M1` (`mw1_t*`), đạt sai số **`0.0000 mm` (`0.00 mm`)** trên cả `.DFF` và `.COL3`.

---

## 2. Quy Hoạch 6 Cụm Địa Danh Chuẩn Genshin, 12 Tổ Hợp Điểm Nhấn & 8 Đạo Cụ Đặc Thù (`ID 11960 .. 12127`)

| Mã POI | Model ID (Near / LOD) | Tên Model (`<= 15` ký tự) | Tọa độ Tâm `ENU (E, N, U)` | Khu vực & Nội dung Công trình / Quái vật / Rương báu |
| :--- | :--- | :--- | :--- | :--- |
| **`M2-POI-01`** | `12060 / 12090` | `me2_starsnatch` / `lme2_starsnatch` | `[1048.0, 504.0, -4.0]` | **Khu vực 1 — Vách Đá Hái Sao (`Starsnatch Cliff`)**: Đài ngắm biển đá trắng, thảm hoa Cecilia, Đàn Phong Cầm (`MSR #551363`), Phong Thần Đồng (`MSR #606515`), đàn Tinh Điệp Phong & Rương Báu Hoa Lệ (`MSR #543924`). |
| **`M2-POI-02`** | `12061 / 12091` | `me2_twinds_e` / `lme2_twinds_e` | `[880.0, 224.0, -10.0]` | **Khu vực 2A — Đền Ngàn Gió Mở Rộng Phía Đông (`Thousand Winds Temple East`)**: Vòng ngoài đấu trường cổ đại nối liền `POI-12` của `M1`, hàng cột La Mã, Thủ Vệ Di Tích (`MSR #587707`) & Mắt Bão (`MSR #601779`). |
| **`M2-POI-03`** | `12062 / 12092` | `me2_midsummer` / `lme2_midsummer` | `[1016.0, 128.0, 14.0]` | **Khu vực 2B — Bí Cảnh Vườn Hoa Mùa Hè (`Midsummer Courtyard`)**: Cổng đá Bí Cảnh cổ đại, Điểm Dịch Chuyển (`MSR #543725`) & **Cổ Thụ Bí Cảnh Irminsul (`Aplaybox 6ujkqcr38uYz` / `MSR #607308`)**. |
| **`M2-POI-04`** | `12063 / 12093` | `me2_falcon_pr` / `lme2_falcon_pr` | `[1040.0, -192.0, -54.0]` | **Khu vực 3A — Bờ Biển Chim Ưng Bắc (`Falcon Coast Harbor & Lighthouse`)**: Ngọn hải đăng đá trắng cao `21.8m`, bến thuyền gỗ dài vươn ra biển & quán rượu gió biển. |
| **`M2-POI-05`** | `12064 / 12094` | `me2_falcon_cp` / `lme2_falcon_cp` | `[1080.0, -376.0, -53.5]` | **Khu vực 3B — Bờ Biển Chim Ưng Nam (`South Falcon Coast Hilichurl Camp`)**: Trại Hilichurl ven biển (`MSR #609416`, Tháp canh `#613586`, Nồi sừng `#613588`, Hàng rào `#613582`) & Rương báu. |
| **`M2-POI-06`** | `12065 / 12095` | `me2_sword_cem` / `lme2_sword_cem` | `[784.0, -760.0, -53.0]` | **Khu vực 4A — Hồ Kiếm Trung Tâm Hẻm Núi Dadaupa (`Sword Cemetery`)**: Đảo tròn giữa hồ, Đại Kiếm Bia Đá trung tâm, 24 thanh trọng kiếm cắm quanh hồ, **Vòng Phong Ấn 3 Tầng (`me2_seal_dome`)**, 3 cột phong ấn & **Rương Báu Hoa Lệ**. |
| **`M2-POI-07`** | `12066 / 12096` | `me2_tribe_ecl` / `lme2_tribe_ecl` | `[880.0, -616.0, -38.0]` | **Khu vực 4B — Đại Doanh Trại Bộ Tộc Nhật Thực (`Eclipse Tribe — Bắc Dadaupa`)**: Nhà Thủ Lĩnh Lớn (`MSR #609417`), Cụm lều (`#609416`), Tháp canh xoắn (`#613586`) & Đài Phong Ấn Bắc. |
| **`M2-POI-08`** | `12067 / 12097` | `me2_tribe_mty` / `lme2_tribe_mty` | `[968.0, -832.0, -34.0]` | **Khu vực 4C — Đại Doanh Trại Bộ Tộc Hảo Thịt (`Meaty Tribe — Đông Dadaupa`)**: **Đấu trường lôi đài gỗ tròn**, Nồi sừng khổng lồ (`MSR #613588`), Nhà Thủ Lĩnh (`#609417`) & Đài Phong Ấn Đông. |
| **`M2-POI-09`** | `12068 / 12098` | `me2_tribe_slp` / `lme2_tribe_slp` | `[536.0, -856.0, -40.0]` | **Khu vực 4D — Đại Doanh Trại Bộ Tộc Hảo Ngủ (`Sleeper Tribe — Tây Dadaupa`)**: Làng sàn gỗ ven hồ trong ô `1_-2`, Tháp canh 2 tầng (`MSR #613590`), Nhà Thủ Lĩnh (`#609417`) & Đài Phong Ấn Tây. |
| **`M2-POI-10`** | `12069 / 12099` | `me2_forsaken` / `lme2_forsaken` | `[608.0, -1064.0, -18.0]` | **Khu vực 4E — Bí Cảnh Hẻm Núi Quên (`Forsaken Rift Domain — Nam Dadaupa`)**: Cổng đá Bí Cảnh vách núi phía Nam, trụ đá băng cổ đại & **Cổ Thụ Bí Cảnh Irminsul**. |
| **`M2-POI-11`** | `12070 / 12100` | `me2_cape_oath` / `lme2_cape_oath` | `[1384.0, -808.0, 28.0]` | **Khu vực 5 — Đỉnh Mũi Đất Thề (`Cape Oath`)**: 3 Đài Tiên Linh (`me2_seelie_ct`), 3 Đài Nguyên Tố Phong (`me2_anemo_mon`), Điểm Dịch Chuyển & **Cổng Dịch Chuyển Lỗ Đen (`enex` `M2_ABYSS_IN`)** bay thẳng ra Đảo Musk Reef. |
| **`M2-POI-12`** | `12071 / 12101` | `me2_musk_abys` / `lme2_musk_abys` | `[1808.0, -712.0, -52.0]` | **Khu vực 6 — Đảo Rạn San Hô Musk & Cổng La Hoàn Thâm Uyên (`Musk Reef & Spiral Abyss`)**: **Cổng Xoắn Ốc La Hoàn Thâm Uyên (`Aplaybox kuyKJEK6eGLp`, `ID 12120`)**, hàng cột vòm cổ đại, bến tàu đảo & **Cổng Lỗ Đen khứ hồi (`enex` `M2_ABYSS_OUT`)** về Mũi Đất Thề. |

---

## 3. Kiểm Định 6 Chốt Chặn Kỹ Thuật & SHA-256 Deliverables

| Hạng mục Kiểm định | Kết quả Thực tế (`verify_m2.py` / `audit.json`) | Trạng thái |
| :--- | :--- | :--- |
| **1. Khớp biên `M1 <-> M2` (`0.00 mm`)** | `260/260` đỉnh biên (`193` Đông + `67` Nam) khớp tuyệt đối `0.0000 mm` | **PASS** |
| **2. Ngân sách ID & Độ dài tên (`<= 19` ký tự)** | `124` Model trong `11960 .. 12127` (thuộc `11960 .. 12159`), tên dài nhất `15` ký tự ASCII | **PASS** |
| **3. Binary `.DFF` (`0x1803FFFF`)** | `124` file `.DFF` (`648,315` đỉnh, `216,105` tam giác), có đủ `Day/Night Prelight` & `2dfx`, tọa độ cục bộ `<= 128.0m` | **PASS** |
| **4. Binary `.TXD` (`DXT1 Mipmapped`)** | `mondstadt_east_m2.txd` (`13` tex) & `lod_mondstadt_east_m2.txd` (`12` tex) nén `BC1_UNORM / DXT1` đủ mipmap | **PASS** |
| **5. Binary `.COL3` (`0x58` Header, Bài học #17)** | `62` mục `.COL3`, **`0` mục LOD trong `.COL3`**, `offsetVertices == 0x74 (116)`, mục lớn nhất `24,248 B < 92,768 B` | **PASS** |
| **6. `A* Walkability` & `Vehicle Driveability`** | `12/12` Điểm nhấn thuộc 6 Khu vực đạt `100% PASS` đi bộ & lái xe từ Cầu Mondstadt `(321.0, -93.1)` + `enex` Lỗ Đen 2 chiều | **PASS** |

### Bảng Băm SHA-256 Các Tệp Bàn Giao Chính
- [`mondstadt_east_m2.img`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/mondstadt_east_m2.img): `33,275,904 B` · `sha256=afd252ceff946e69341278bc67692d4b09fcf5a9dea2e571259add6b8ecc0084`
- [`mondstadt_east_m2.ide`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/mondstadt_east_m2.ide): `4,717 B` · `sha256=9b70ba59f44b347a6ca59fc01b603aedf0416993ac658d500c43672b405b978d`
- [`mondstadt_east_m2_west_continent.ipl`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/mondstadt_east_m2_west_continent.ipl): `11,536 B` · `sha256=4a111be05d66e23420fafc201a04469c071a3da5a7c70d2c5a2199a93d5a5aa7`
- [`mondstadt_east_m2_sandar_bay.ipl`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/mondstadt_east_m2_sandar_bay.ipl): `11,388 B` · `sha256=73818f1d85c614486a2537c3d2a916ad225c25ec43e50adc6ede7079de47a2d8`
- [`mondstadt_east_m2.col`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/models/col/mondstadt_east_m2.col): `1,099,024 B` · `sha256=7436cc49bfb878ed92a2e3436465b2362e53747fdefb53b9f38d9b5e6e4be349`
- [`mondstadt_east_m2.txd`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/models/txd/mondstadt_east_m2.txd): `570,272 B` · `sha256=7f26754d398a0be1f1c392ef2ce1ded77ee53c7dbc7041e80a5a279caece12ee`
- [`lod_mondstadt_east_m2.txd`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/models/txd/lod_mondstadt_east_m2.txd): `1,050,712 B` · `sha256=4c1f811ac1c65b8bf4d04efc69b6f2d64b108013fb06db089ef1953f26c7556e`
- [`audit.json`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/audit.json): `3,376 B` · `sha256=013099db81260098fe5360bdb6d7b29293baa8b13733621b2a8f18b92255fb15`
- [`walkability.json`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-east-m2-2026-10-25/walkability.json): `6,856 B` · `sha256=3e3fd9bd572ce1396d44263573fe615c05179bd9d433a0803fbcc4c0df8a934b`
- [`mondstadt-m2-east-coast-showcase-2026-10-25.html`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/mondstadt-m2-east-coast-showcase-2026-10-25.html): `59,193,031 B` · `sha256=a1507c6f1f2a7369dc6cd960c726e890880734927524ab14613641233b787001`
