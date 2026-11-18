# Quy Hoạch Tổng Thể Phase 2 Cho Ngoại Ô Mondstadt (`Sector M1`): Địa Danh Chuẩn Genshin, Mở Rộng Đường Chính & Đường Nhánh, Cầu Đường, Lấp Đầy Thế Giới & Tối Ưu Hóa (`DXT1` + Ngân Sách ID `< 65.535`)

- **Ngày lập & cập nhật**: `2026-10-24`
- **Hội thoại Phụ trách Chính (`Phase 2 Lead`)**: [`327d7afd-8da6-4eec-ac19-02d7dfebb8b1`](conversation://327d7afd-8da6-4eec-ac19-02d7dfebb8b1)
- **Hội thoại Bàn giao nền địa hình Phase 1 (`Completed`)**: [`a5424577-8251-4efa-b2d5-cb54893080c1`](conversation://a5424577-8251-4efa-b2d5-cb54893080c1) ([`mondstadt-wilds-m1-build-and-inspection-2026-10-23.md`](mondstadt-wilds-m1-build-and-inspection-2026-10-23.md))
- **Phiếu công việc Phase 2**: [`work-items/2026-10-24-antigravity-mondstadt-m1-phase2-beautification-and-canonical-pois.md`](work-items/2026-10-24-antigravity-mondstadt-m1-phase2-beautification-and-canonical-pois.md)
- **Các công cụ xem trực quan trên trình duyệt**:
  1. [Bản đồ Đối chiếu 1:1 Địa lý Chuẩn Genshin vs. `Sector M1` (`[-768m .. +768m]`)](mondstadt-m1-canonical-geography-and-thematic-plan-2026-10-24.html)
  2. [Đại Danh Mục 39 Bộ Tài Nguyên Lấp Đầy Bản Đồ & Kiến Trúc Mondstadt Chính Hãng](mondstadt-m1-asset-catalog-and-options-2026-10-24.html)
  3. [Trình Xem 3D WebGL Toàn Cảnh `M0 + M1 + Landmarks` (`WASD` Walk/Drive + GPS + Dvalin Bay + Timmie & Bồ Câu + Sói Bắc Phong Andrius + 15 Rương Báu)](mondstadt-m1-landmarks-showcase-2026-10-24.html)
  4. [Báo Cáo Kiểm Định Trực Quan 52 Model Đã Kéo Từ The Models Resource & Convert Sang `.DFF + .TXD` (`DXT1`)](mondstadt-models-resource-conversion-audit-2026-10-24.html)

---

## 1. Bàn Giao Trạng Thái Hiện Tại & Phạm Vi Phụ Trách Của Phase 2

Sau khi Hội thoại #1 (`a5424577-8251-4efa-b2d5-cb54893080c1`) hoàn tất 100% phần làm mượt địa hình `36` ô `256m × 256m` (`IDs 6730..6801`, `83/83 Binary PASS`, `17/17 A* Walkability PASS`, `38/38 Vehicle Driveability PASS`), **Hội thoại `327d7afd-8da6-4eec-ac19-02d7dfebb8b1` chính thức tiếp nhận toàn bộ quyền điều phối và thi công Phase 2 của `Sector M1`** với 3 mục tiêu cốt lõi do người dùng chỉ đạo:

1. **Định vị Địa danh theo Bản đồ Genshin Chuẩn + Kết hợp Đa Vũ Trụ hợp lý**:
   - Không đặt công trình của vùng khác (Liyue, Inazuma, Fontaine, Sumeru) vào Mondstadt.
   - Các địa danh có tên tuổi nằm trong `Sector M1` (`Thanh Tuyền`, `Tửu Trang Dawn Winery`, `Phong Khởi Địa`, `Rừng Thì Thầm`, `Hồ Sao Rơi`, `Phong Nguyên Bản`, `Lang Lãnh / Đấu trường Sói Andrius`, `Hẻm Núi Minh Quán`, `Chân núi tuyết Dragonspine`) phải có công trình/cảnh quan/quái vật **liên quan trực tiếp** tới địa danh đó.
   - Các khoảng trống ven đường, bờ hồ, sườn đồi được lấp đầy sáng tạo bằng cầu đường, bến thuyền, hải đăng, đồi đá `250m`, vách đá, hang động, cụm rừng thông/anh đào gộp sẵn, nhà gỗ, túp lều, trang trại và các điểm nhấn Đa Vũ Trụ (`7-Eleven`, `Showroom`, `Biệt thự Đèo`, `Lâu đài cổ`, `Đảo Kame House`, `Capsule Corp`).
2. **Hoàn thiện Hệ thống Đường Chính & Đường Nhỏ / Cầu Đường Chuẩn Bản Đồ Genshin**:
   - Bên cạnh 6 tuyến đường ô tô đã mở ở Phase 1 (`Route_01..06`), bổ sung **6 tuyến đường chính/nhánh còn thiếu so với bản đồ Genshin chuẩn (`Route_07..12`)** kèm hệ thống **Cầu vòm đá qua suối, Cầu vượt hẻm núi và Cầu gỗ dạo hồ** để kết nối tới mọi địa danh chính trong `Sector M1`.
3. **Nén Tối Đa (`DXT1` + Giảm Đa Giác) & Quản Lý Chặt Ngân Sách Model ID (`< 65.535`)**:
   - Mọi model từ Genshin (`The Models Resource`) và game khác phải qua pipeline nén 4 tầng (giảm `95%–98%` dung lượng) và tiết kiệm tối đa Model ID thông qua tái sử dụng ID có sẵn của `Project Eagle`, `Multi-Instancing` trong `.IPL` và `Pre-Merged Composite Clusters`.

---

## 2. Bản Đồ Đối Chiếu 1:1 Giữa Map Mondstadt Chính Thức Và Khung `Sector M1` (`ENU [-768m .. +768m]`)

![Bản Đồ Đối Chiếu Địa Lý Chuẩn Genshin Impact vs Sector M1](atlas-3d-captures/m1_genshin_canonical_map_analysis.png)

Khung **`Sector M1` (`1.536m × 1.536m`, `E ∈ [-768m .. +768m]`, `N ∈ [-768m .. +768m]`, gồm `6×6 = 36` ô `mw1_r0_c0..r5_c5`)** bao phủ toàn bộ vùng trung tâm Mondstadt:

| Khu Vực Địa Lý (Theo Map Genshin) | Ô Lưới `Sector M1` (`256m × 256m`) | Tọa Độ `ENU (E, N)` | Trạng Thái Trong `M1` | Quy Hoạch Công Trình, Cảnh Quan & Quái Vật Liên Quan |
| :--- | :---: | :---: | :---: | :--- |
| **1. Ngã 3 Đầu Cầu Mondstadt (`Bridgehead`)** | `r2_c4` (`ID 6746`) | `(+321 .. +372, -96)` | **Trong `M1` (`PAD-01`)** | • **Genshin**: Lều/Quầy Hiệp Hội Mạo Hiểm (`Katheryne`, `Cyrus`), Bàn Giả Kim (`#532651`), Sạp Trái Cây (`#611671`), Trụ Dịch Chuyển (`#543725`).<br>• **Đa Vũ Trụ**: Trạm dừng **7-Eleven Konbini** sáng đèn đêm. |
| **2. Rừng Thì Thầm (`Whispering Woods`)** | `r3_c4`, `r3_c5`, `r4_c4` (`ID 6752, 6753, 6758`) | `(+450 .. +600, +140)` | **Trong `M1` (`PAD-02`)** | • **Genshin**: **Doanh trại lớn của Hilichurl** (Nhà thủ lĩnh `#609417`, 2 Tháp canh `#613586/#613590`, Hàng rào Totem, Nồi sừng) + **Hilichurl, Mitachurl, Slime Phong (`#587816`)** ẩn dưới các cụm rừng thông gộp sẵn (`cwyforest`). |
| **3. Hồ Sao Rơi (`Starfell Lake`) & Núi Vọng Phong** | `r4_c5`, `r5_c4`, `r5_c5` (`ID 6759, 6764, 6765`) | `(+480 .. +680, +320 .. +620)` | **Trong `M1`** | • **Genshin**: Hồ nước có đảo nhỏ giữa hồ, Cầu gỗ bắc ra đảo, Đài đá Tượng Thần, **Rương Báu Cao Cấp (`#543924`)**, đàn **Slime Phong** và Chòi gỗ vọng cảnh trên đỉnh Bắc (`+260, +620`). |
| **4. Đấu Trường Phong Nguyên Bản (`Anemo Hypostasis`) & Đỉnh Đèo Đông** | `r2_c5`, `r3_c5` (`ID 6747, 6753`) | `(+610 .. +660, -40 .. +200)` | **Trong `M1` (`PAD-08`)** | • **Genshin**: Vòng tròn cổ đại + **Thủ Vệ Di Tích Ruin Guard (`#587707`)** + **Mắt Bão (`#601779`)** + Cột đá di tích (`stonepillar1`) nhìn sang hướng Đền Ngàn Gió.<br>• **Đa Vũ Trụ**: Đài quan sát / Tháp truyền hình (`Torre Tokyo`) trên đỉnh đèo Đông. |
| **5. Phong Khởi Địa (`Windrise`) & Cây Đại Thụ** | `r1_c4`, `r1_c5` (`ID 6740, 6741`) | `(+520 .. +680, -220 .. -360)` | **Trong `M1` (`PAD-07`)** | • **Genshin**: **Đại Thụ Phong Khởi Địa (`SymbolOfMondstadtsHero.dae` `#607308` / `Area_FQD`)** bên dòng suối + **Cầu vòm đá (`ce_archbridge`)** qua suối + Đàn Slime Phong.<br>• **Đa Vũ Trụ**: Khu Biệt thự nghỉ dưỡng (`PAD-07`) trên triền đồi nhìn xuống Đại Thụ. |
| **6. Thị Trấn Thanh Tuyền (`Springvale` & Hồ Thanh Tuyền)** | `r1_c3`, `r0_c3` (`ID 6739, 6733`) | `(+115 .. +180, -450 .. -550)` | **Trong `M1` (`PAD-04`)** | • **Chuẩn 100% Genshin**: **Cối Xay Gió Thanh Tuyền (`#609418`)** + **3 Nhà Thôn Quê Thanh Tuyền (`#611347`, `#612565`, `#610632`)** + Chợ Sạp Rau Quả/Sạp Hoa + Lều Thợ Săn + **Heo Rừng (`Boar #605628`)** + Cầu gỗ & Bến thuyền Hồ Thanh Tuyền. |
| **7. Đỉnh Đồi Nam Giáp Chân Núi Tuyết (`Snow-Covered Path` / `Cecilia Garden`)** | `r0_c2`, `r0_c3`, `r0_c4` (`ID 6732..6734`) | `(+160, -640)` | **Trong `M1` (`PAD-09`)** | • **Liên quan Genshin**: Cửa ngõ lên vùng núi cổ & Bí cảnh Cecilia — đặt **Pháo Đài Đá Cổ (`El Castillo Medieval Keep`)** + **Cửa Hang Động (`lcc_cm_caveent01`)** + **Ruin Guard (`#587707`)** & Rương Báu. |
| **8. Tửu Trang Dawn Winery (`Dawn Winery Manor` & Đồi Tượng Thần)** | `r1_c1`, `r0_c1`, `r1_c2` (`ID 6737, 6731, 6738`) | `(-364 .. -490, -420 .. -600)` | **Trong `M1` (`PAD-06`)** | • **Chuẩn 100% Genshin**: **Dinh Thự Tửu Trang Dawn Winery (`#609576` / `Area_HYWC`)** + **Giàn Nho (`Lush Grapevine #613642`)** + **Đồng Ruộng Rào Gỗ & Nhà Kho Đỏ (`ce_farmland01`, `ky_barn`)** trải rộng khắp thung lũng Tây-Nam. |
| **9. Lang Lãnh (`Wolvendom`) & Đấu Trường Sói Bắc Phong (`Andrius`)** | `r1_c0`, `r2_c0`, `r2_c1`, `r3_c1` (`ID 6736, 6742, 6743, 6749`) | `(-560 .. -660, -280 .. +180)` | **Trong `M1` (`PAD-10`)** | • **Liên quan Genshin**: Vòng tròn **Đấu trường Sói Bắc Phong (`Andrius`)** tại `(-600, -280)`, rừng thông rậm (`cwyforest`), vách đá hẻm núi (`lcc_cliff`), hang động, và trên đỉnh đồi `PAD-10` đặt **Lâu Đài Cổ (`Japanese/Medieval Castle`)** nhìn xuống toàn cảnh Lang Lãnh & Hồ Cider. |
| **10. Hẻm Núi Minh Quán (`Brightcrown Canyon`)** | `r4_c0`, `r4_c1`, `r5_c0`, `r5_c1` (`ID 6754, 6755, 6760, 6761`) | `(-350 .. -650, +350 .. +650)` | **Trong `M1`** | • **Liên quan Genshin**: Hẻm núi đá cổ dẫn về phía Phế Tích Phong Long — đặt **Cầu Vượt Hẻm Núi (`cocanyonbridge`)**, **Đồi Đá 250m (`hill250x250rocky1`)**, **Cột Đá Cổ** và **Doanh trại Hilichurl tiền đồn**. |
| **11. Lòng Hồ Cider, Bờ Hồ & Bầu Trời (`Cider Lake` & `SKY-11`)** | `r2_c2..c3`, `r3_c2..c3`, `SKY-11` | `(-250 .. +376, -280 .. +250, Z=+95m)` | **Trong `M1` (`PAD-03`, `PAD-05`, `SKY-11`)** | • **Trên bầu trời `SKY-11`**: **Phong Ma Long Dvalin chính hãng (`#328740`)** bay lượn trên bầu trời Hồ Cider.<br>• **Ven bờ hồ (`PAD-03`, `PAD-05`)**: **Đảo Kame House**, **8 Bến thuyền gỗ (`sp_pier`)**, **Ngọn hải đăng (`sp_lighthouse`)**, **Showroom Siêu Xe Kính**, **Quán Diner & Trạm Xăng ven đường**. |

---

## 3. Quy Hoạch Hệ Thống Đường Xá Phase 2: 6 Tuyến Hiện Có + 6 Tuyến Đường Chính/Nhánh & Cầu Đường Bổ Sung Theo Map Genshin

Để mạng lưới giao thông vừa chạy mượt cho ô tô, vừa khớp với **hệ thống đường dẫn tới các địa danh chính trên bản đồ Genshin chuẩn**:

### 3.1. 6 Tuyến Đường Ô Tô Đã Hoàn Thành Ở Phase 1 (`Route_01 .. Route_06`)
1. **`Route_01` (`Route_M1_Ring`)**: Vành đai `360°` quanh bờ Hồ Cider (`rộng 12m`).
2. **`Route_02` (`Route_Whispering_Woods`)**: Nhánh Đông-Bắc xuyên Rừng Thì Thầm (`PAD-02`) lên Đỉnh Núi Bắc (`rộng 11m`).
3. **`Route_03` (`Route_Springvale_Highway`)**: Đại lộ phía Nam nối `PAD-03` $\rightarrow$ Thị trấn Thanh Tuyền (`PAD-04`) $\rightarrow$ Đồi Tây Thanh Tuyền (`PAD-06`) $\rightarrow$ Bờ Nam Hồ Cider (`PAD-05`) (`rộng 12m`).
4. **`Route_04` (`Route_East_Touge`)**: Đường đèo phía Đông nối `PAD-03` $\rightarrow$ Lưng đèo Phong Khởi (`PAD-07`) $\rightarrow$ Đỉnh Đèo Đông (`PAD-08`) (`rộng 11m`).
5. **`Route_05` (`Route_South_Touge`)**: Đường đèo phía Nam nối Thanh Tuyền (`PAD-04`) $\rightarrow$ Đỉnh Đồi Nam giáp Tuyết Sơn (`PAD-09`) (`rộng 11m`).
6. **`Route_06` (`Route_West_Peak_Overlook`)**: Đường đèo phía Tây nối bờ Tây Hồ Cider $\rightarrow$ Đỉnh Đồi Lang Lãnh (`PAD-10`) (`rộng 11m`).

### 3.2. 6 Tuyến Đường Chính, Đường Nhánh Nhỏ & Cầu Đường Cần Bổ Sung Ở Phase 2 (`Route_07 .. Route_12`)
7. **`Route_07_Starfell_Lake` (Đường Chính Đông-Bắc lên Hồ Sao Rơi — `rộng 9m–10m`)**:
   - Tách từ `Route_Whispering_Woods` tại `PAD-02 (520, +140)` chạy thẳng lên **Hồ Sao Rơi (`Starfell Lake`, `(640, +320)`)**, kèm **Cầu gỗ (`ni_woodbridge`)** bắc ra đảo Tượng Thần giữa hồ.
8. **`Route_08_Windrise_Great_Tree_&_Stream_Bridge` (Đường Chính Đông-Nam qua Đại Thụ Phong Khởi Địa + Cầu Đá Qua Suối — `rộng 10m`)**:
   - Nối từ ngã ba Nam Cầu Mondstadt `(376, -210)` và Thanh Tuyền `(180, -450)` băng qua dòng suối bằng **Cầu Vòm Đá Cổ Điển (`ce_archbridge`)** dẫn thẳng tới gốc **Đại Thụ Phong Khởi Địa (`(615, -345)`)** rồi nối vào đèo Đông `PAD-07`.
9. **`Route_09_Dawn_Winery_Manor_Loop` (Đường Chính Tây-Nam xuống Dinh Thự Tửu Trang Dawn Winery — `rộng 10m`)**:
   - Kéo dài từ `PAD-06 (-364, -420)` xuống **Dinh thự Tửu Trang Dawn Winery (`(-490, -600)`)**, tạo vòng xuyến quanh các luống vườn nho và trang trại trước khi nối lại bờ hồ Tây-Nam.
10. **`Route_10_Wolvendom_Andrius_Trail` (Đường Hẻm Núi Tây vào Đấu Trường Sói Bắc Phong Andrius — `rộng 8m–9m`)**:
    - Con đường mòn đá xuyên rừng **Lang Lãnh (`Wolvendom`)** nối từ ngã ba Bắc Dawn Winery `(-364, -300)` và bờ Tây Hồ Cider `(-344, -64)` dẫn thẳng vào cửa **Đấu trường Sói Bắc Phong (`(-600, -280)`)**.
11. **`Route_11_Brightcrown_Canyon_Bridge_Trail` (Đường Nhánh Tây-Bắc xuyên Hẻm Núi Minh Quán + Cầu Vượt Hẻm Núi — `rộng 8m–9m`)**:
    - Từ Đồi Tây `PAD-10 (-560, +180)` dẫn lên phía Bắc băng qua khe vực bằng **Cầu Vượt Hẻm Núi (`cocanyonbridge`)** tới khu di tích **Hẻm Núi Minh Quán (`(-480, +500)`)** rồi nối về vành đai Bắc Hồ Cider.
12. **`Route_12_Springvale_Pond_&_Lakeside_Piers` (Hệ Thống Đường Nhỏ Ven Hồ Thanh Tuyền & 8 Bến Thuyền Hồ Cider — `rộng 6m–8m`)**:
    - Đường dạo lát đá/gỗ vòng quanh **Hồ Thanh Tuyền (`(160, -550)`)** có cầu gỗ nhỏ (`lcc_golfbridge`) và các nhánh rẽ ngắn dẫn xuống **8 Bến thuyền gỗ (`sp_pier`, `por_woodpier`) & Ngọn hải đăng (`sp_lighthouse`)** quanh Hồ Cider.

---

## 4. Chuẩn Nén 4 Tầng & Bảng Phân Bổ Ngân Sách Model ID (`< 65.535`)

### 4.1. Chuẩn Nén 4 Tầng Bắt Buộc (`Giảm 95% – 98% Dung Lượng`)
1. **Loại bỏ kênh PBR thừa & `ShadowMesh`**: Cắt bỏ 100% ảnh `_Normal`, `_Height`, `_SMBE`, `_Lightmap`, `_AO` và lưới bóng đổ `ShadowMesh` trong file `.dae`/`.obj`; gỡ xương (`Skinning Bones`) của quái vật/NPC tĩnh.
2. **Nén `DXT1 Mipmapped` `256×256` & Dùng Chung Atlas**: Mỗi texture `_Diffuse` nén `DXT1` chỉ nặng **`43 KB`**; dùng chung atlas `Area_MdBuild` cho toàn bộ nhà dân Mondstadt/Thanh Tuyền, `Area_MdProps_Gadget01` cho toàn bộ sạp hàng/đèn đường, và `Area_Common_Build_Hili_House_Cluster_01` cho toàn bộ 7 công trình trại Hilichurl.
3. **Giảm bậc đa giác (`Decimation`)**: Mỗi prop/nhà lẻ `<= 5.000 tris`; mỗi tổ hợp gộp nguyên cụm (`Composite POI`) `<= 14.500 tris` (`< 65.535` đỉnh `uint16`).
4. **Lưới `.COL3` tối giản**: `<= 2.280 faces` (`25–38 KB << 92.768 B`), kiểm tra cứng `span < ±240.0m` (không kẹp thầm `int16/128`), mặt đường/sàn phẳng `nz >= 0.707`.

### 4.2. Bảng Phân Bổ Model ID Cụm Mondstadt (`Khối Trống 6526 .. 6862 < 65.535`)

| Dải Model ID | Phân Khu / Gói Tài Nguyên | Số Lượng ID | Quy Tắc Sử Dụng & Tiết Kiệm ID |
| :---: | :--- | :---: | :--- |
| **`0 ID mới`** | **90 Vật Thể Môi Trường Của `Project Eagle`** (`ce_archbridge`, `cocanyonbridge`, `sp_pier`, `sp_lighthouse`, `hill250x250rocky1`, `lcc_cm_cave01`, `lcc_cliff`, `cwyforest001..006`, `lcc_treepatch`, `cw2_logcabins`, `lcc_hikinghut`, `ce_farmland01`, `ky_barn`, `ulp_windmill`, `rcdiner`...) | **`0 IDs`** | Đã có sẵn định nghĩa `.IDE` trong `Project Eagle`! Chỉ cần đặt tọa độ `inst` trong `.IPL` — có thể rải **300–500 vật thể** khắp `Sector M1` mà **không tốn thêm bất kỳ Model ID nào**. |
| **`6710 .. 6726`** | **`Sector M0` — Thành Mondstadt (`mondstadt_city`)** | `17 IDs` | Đã khóa cố định (`Read-Only`). |
| **`6730 .. 6765`** | **`Sector M1` — 36 Mảnh Địa Hình & Đường Bộ Cận Cảnh (`mw1_t00..35`)** | `36 IDs` | Nền địa hình + 12 tuyến đường + 10 bãi đất nền (`DrawDistance = 295m`, có `.COL3`). |
| **`6766 .. 6801`** | **`Sector M1` — 36 Mảnh Địa Hình & Đường Bộ LOD (`lmw1_t00..35`)** | `36 IDs` | LOD tầm xa (`DrawDistance = 1500m`). |
| **`6802 .. 6825`** *(Near)*<br>**`6830 .. 6853`** *(LOD)* | **24 Tổ Hợp Điểm Nhấn & Rồng Dvalin (`POI-01 .. POI-24`)** | `48 IDs` | Gộp nguyên cụm (`Pre-Merged Clusters`): Ngã 3 Đầu Cầu (`6802`), Quảng trường Rừng Thì Thầm (`6803`), Bến Hồ Đông (`6804`), Thị trấn Thanh Tuyền (`6805`), Đảo Kame House (`6806`), Tây Thanh Tuyền (`6807`), Lưng Đèo Phong Khởi (`6808`), Đỉnh Đèo Đông (`6809`), Pháo Đài Đỉnh Nam (`6810`), Lâu Đài Đồi Tây (`6811`), **Rồng Phong Ma Dvalin bay lượn (`6812`)**, **Đền Ngàn Gió (`6813`, hạ khớp mặt đất `Z = -25.4m`, chân móng `9.5m`)**, **Đại Thụ Phong Khởi Địa (`6814`)**, **Hồ Sao Rơi (`6815`)**, **Tửu Trang Dawn Winery (`6816`)**, **Đấu Trường Sói Bắc Phong (`6817`)**, **Hẻm Núi Minh Quán (`6818`)**, **Đỉnh Vọng Phong (`6819`)**, **Hồ Thanh Tuyền (`6820`)**, **Bến Tây Hồ Cider (`6821`)**, **Bến Bắc Hồ Cider (`6822`)**, **Rừng Nam (`6823`)**, **Rừng Đông (`6824`)**, **Cao Nguyên Tây-Bắc (`6825`)**. |
| **`6854 .. 6859`** *(Roads)*<br>**`6680 .. 6695`** *(Objects)*<br>**`2900 .. 2909`** *(Custom Peds)* | **Đường Chính/Nhánh, Quái Vật/NPC Tuần Tra & 5 Loại Rương Báu (`Multi-Instance & Interactive Pack`)** | `22 Obj IDs`<br>`+ 10 Ped IDs` | • **6 Tuyến Đường Chính & Đường Nhánh (`6854 .. 6859`)**: `rd_starfell`, `rd_windrise`, `rd_winery_lp`, `rd_wolvendom`, `rd_brcrown`, `rd_spring_pr`.<br>• **Quái vật & Động vật hoang dã (`Obj 6680 .. 6687` / `Ped 2900 .. 2907`)**: Slime Phong (`6680`/`6681`, `#587816`), Hilichurl (`6682`, `#584572`), Mitachurl (`6683`, `#584645`), Phù Thủy Hilichurl Phong (`6684`, `#585038`), Thủ Vệ Di Tích (`6685`, `#587707`), Mắt Bão (`6686`, `#601779`), Heo Rừng (`6687`, `#605628`).<br>• **Timmie & Đàn Chim Bồ Câu Trên Cầu Mondstadt (`Ped 2908` / `Obj 6688` `gi_timmie_npc` `#596302` + `Obj 6689` `sc_pigeon` `#606466`)**: Đặt tại cầu đá chính dẫn vào thành Mondstadt (`E = +265.2, N = -74.6, U = -52.12m`) cùng 10 con bồ câu & 2 chim sẻ mổ thóc dưới chân.<br>• **Sói Bắc Phong Andrius / Lupus Boreas (`Ped 2909` / `Obj 6690` `gi_andrius_boss` `#540934`)**: Đi tuần tra vòng tròn (`bán kính 13.5m`) bên trong Đấu Trường Sói Bắc Phong (`POI-16`, `E = -541.5, N = -175.0, U = -31.25m`).<br>• **5 Loại Rương Báu Genshin (`Obj 6691 .. 6695`, `#543920..#543924`)**: Đặt **15 rương (`CHEST_01..CHEST_15`)** rải rác trong thành, gần địa danh và ngoài rừng; khi lại gần (`<= 6.8m`) thưởng tiền 1 lần duy nhất: Rương Thường (`6691`, `+$100`), Rương Tinh Điêu (`6692`, `+$250`), Rương Quý Giá (`6693`, `+$500`), Rương Kỳ Dị (`6694`, `+$750`), Rương Hiếm/Hoa Lệ (`6695`, `+$1.000`). |

---

## 5. Sổ Tay Kinh Nghiệm Convert Skin & Model `.DAE` Sang GTA `.DFF + .TXD` (Chuẩn Bề Mặt Kín 100% — `0` Lỗ Thủng)

> [!IMPORTANT]
> Tài liệu chuyên sâu đầy đủ về quy trình convert Skin & Model 3D đã được tổng hợp tại: [`skin-and-3d-model-conversion-lessons-2026-10-25.md`](skin-and-3d-model-conversion-lessons-2026-10-25.md) và kiểm định trực quan 97/97 mục tại [`mondstadt-models-resource-conversion-audit-2026-10-24.html`](mondstadt-models-resource-conversion-audit-2026-10-24.html).

Qua kiểm định toàn bộ **91 gói model (`.dae`)** từ `models.spriters-resource.com` cùng **11 nhân vật Playable Mondstadt** trong [`parse_collada_dae.py`](file:///C:/Users/LENOVO/.gemini/antigravity/brain/327d7afd-8da6-4eec-ac19-02d7dfebb8b1/scratch/parse_collada_dae.py) và [`build_m1_multiverse_landmarks.py`](file:///D:/GTA%20Archive/Staging/mondstadt-m1-multiverse-landmarks-2026-10-24/build_m1_multiverse_landmarks.py), đã thiết lập **6 quy tắc bắt buộc**:

1. **Ưu tiên số 1 — Dùng trực tiếp Skin `.DFF` + `.TXD` có sẵn trong `D:\GTA Archive\Skin Library` trước khi convert từ `.DAE`**:
   - Toàn bộ 11 nhân vật Playable của Mondstadt (`Diluc #328746`, `Venti #328741`, `Kaeya #328743`, `Jean #328744`, `Lisa #328745`, `Barbara #328747`, `Rosaria #514444`, `Diona #539022`, `Albedo #525577`, `Sucrose #538867`, `Klee #536287`) đã có sẵn skin GTA SA chuẩn trong `Skin Library\Project Eagle\numbered-skins\raw`.
   - Nạp trực tiếp từ `.DFF` (`mat_split`) + `.TXD` có sẵn, chuẩn hóa tư thế trục đứng (`Z_UP` / `Y_UP` / `X_UP`) và lọc bỏ các sub-material phủ mắt trong suốt (`alpha_mean < 80`). Chỉ những model chưa có trong `Skin Library` mới convert từ `.dae` / `.fbx` / `.pmx`.
2. **Tuyệt đối CẤM cắt giảm tam giác bằng bước nhảy `max_tris` (`conv_tris[::step]`)**:
   - Việc giới hạn `max_tris = 8500` (hoặc `2800` trong nội thất) bằng cách lấy mẫu bước nhảy làm xóa mất 55%–89% mặt tam giác trên các model lớn (`Playable Char`, `Statue of Marble and Brass #604549`, `Lupus Boreas #540934`, `Stormterror Dvalin #328740`), gây hiện tượng thủng lỗ chỗ khắp bề mặt. Bắt buộc **giữ 100% mặt tam giác gốc (`0` lỗ thủng)**.
3. **Độ chính xác hàn đỉnh `round(p, 4)` (`0.1 mm`) & Không tách đỉnh theo `face_normal`**:
   - Làm tròn `round(p, 2)` (`1 cm`) làm suy biến mất `6,200–11,200` tam giác nhỏ trên mắt/mặt/ngón tay (`< 1 cm`). Nâng lên `round(p, 4)` (`0.1 mm`) + `round(uv, 4)` và bỏ `face_normal` khỏi khóa hàn đỉnh `v_map` giúp giữ 100% tam giác mà tổng số đỉnh của mọi `.DFF` (kể cả Dvalin `76,525F -> 51,253V` và 6 phòng nội thất `39k–79kF -> 29k–53kV`) vẫn nằm gọn dưới trần `65,535` (`uint16`) của RenderWare.
4. **Loại bỏ lưới trùng lặp `UV1 / UV2 / UV3` (Lightmap UV Channel), Morph Targets mặt & thư mục phụ `Objects/`**:
   - Cắt bỏ 100% các node `_UV1.._UV4`, `_LOD1.._LOD3`, các `<geometry>` biểu cảm khuôn mặt không gắn vào `<visual_scene>`, và đẩy các file vũ khí rời trong thư mục con `Objects/` (`Torch.dae`, `Axe.dae`, `Wand.dae`) xuống cuối ưu tiên để luôn lấy đúng mesh quái chính (`Hilichurl.dae`, `Mitachurl.dae`, `AnemoSamachurl.dae`).
5. **Loại bỏ lớp mặt nạ mắt `EyeStar`, vũ khí rời `MonEquip_*` / `EffectWater` tại `(0,0,0)`, hộp chắn sáng `*_Ocl`, vỏ rương `CreateTreasureBox*` và vỏ VFX `Purified_Eff_Mat` / `Evil_Eff_Mat` / `EffectMesh01`**:
   - Khắc phục triệt để lỗi đen mắt nhân vật, lỗi đống kiếm/khiên nằm dưới chân tượng `#604549`, lỗi vỏ hiệu ứng đen/tím trên `#328740 Dvalin` & `#540934 Andrius`, đồng thời uốn mượt dải bờm lưng ở tư thế bind-pose (`z > 4.2m`) của `#540934 Andrius` xuôi về phía đuôi.
6. **Lọc nghiêm ngặt kênh ảnh `_Diffuse` / `_Colored` & Nâng giới hạn lên `14–16` Texture/POI (`234` Texture `DXT1 Mipmapped` trong `m1_lmk.txd`)**:
   - Cấm tuyệt đối việc fallback nhầm vào ảnh `normal`, `smbe`, `lightmap`, `metal`, `mask`, `noise`, `ramp`, `matcap`, `fluid`, `icetilling`. Toàn bộ **97/97 model & phòng nội thất** đã được kiểm định trực quan 3D WebGL tại [`mondstadt-models-resource-conversion-audit-2026-10-24.html`](mondstadt-models-resource-conversion-audit-2026-10-24.html).

---

## 6. Bổ Sung Nguồn Tài Nguyên 3D Genshin Mới (`25/10/2026`): Kho `Aplaybox` (`aplaybox.com` — 模之屋) & Danh Mục 17 Bộ Model Mondstadt Đã Khảo Sát

Bên cạnh `HoyoMap 3D CDN` và `The Models Resource / Spriters Resource` (`models.spriters-resource.com`), người dùng đã phát hiện và bổ sung vào Knowledge Base nguồn kho model 3D Genshin cực kỳ phong phú thứ 3:
- **Trang chủ**: **`Aplaybox / 模之屋`** (`https://www.aplaybox.com`)
- **API Tìm kiếm trực tiếp đã giải mã**: `POST https://api.aplaybox.com/api/web/v1/work/search` (lưu ý bắt buộc truyền `"work_format_id": -1` để lấy mọi định dạng `.pmx`, `.blend`, `.fbx`; `"work_category_id": 2` là Cảnh quan `场景`, `3` là Đạo cụ `物件`, `-1` là Tất cả).
- **Danh mục JSON đã xuất**: [`D:\GTA Archive\Mod Donor Library\ky6-world-filling-assets\aplaybox-packs\aplaybox-mondstadt-catalog-2026-10-25.json`](file:///D:/GTA%20Archive/Mod%20Donor%20Library/ky6-world-filling-assets/aplaybox-packs/aplaybox-mondstadt-catalog-2026-10-25.json) (quét `465` tác phẩm Genshin, lọc ra `148` tác phẩm liên quan Mondstadt và tuyển chọn **17 bộ model đắt giá nhất mà `models.spriters-resource.com` chưa có**):

| Nhóm Tài Nguyên | Mã `work_uuid` Trên `Aplaybox` | Tên Tác Phẩm & Định Dạng | Giá Trị Bổ Sung Cho Map Mondstadt (`Sector M0 / M1`) |
| :--- | :---: | :--- | :--- |
| **1. Tượng Thần & Cổng Bí Cảnh (Chưa có trên Models Resource!)** | `4TpVcvWV0gjp`<br>`3dusvcTtd86u`<br>`W6XlBGcncAi6` | • **`原神风神像七天神像`** (`.fbx`, pass `0616`)<br>• **`【原神/风神像】`** (`.pmx`, `1.458 DLs`)<br>• **`温迪风神雕像`** (`.fbx`) | Cung cấp **Thất Thiên Thần Tượng Phong (`Statue of the Seven - Anemo`)** chuẩn 100% để đặt tại **Phong Khởi Địa (`POI-13`)**, **Đảo Hồ Sao Rơi (`POI-14`)**, **Đồi Tửu Trang Dawn Winery (`POI-15`)** và **Đại Tượng Phong Thần Barbatos** ở Quảng trường Đại Giáo Đường (`M0`). |
| **2. Cổng La Hoàn Thâm Uyên & Cổ Thụ Bí Cảnh** | `kuyKJEK6eGLp`<br>`6ujkqcr38uYz` | • **`原神深渊门`** (`.pmx`, Cổng Thâm Uyên)<br>• **`【原神场景】祝圣秘境`** (`.pmx`, `1.372 DLs`) | Đặt **Cổng Xoắn Ốc Thâm Uyên (`Spiral Abyss Portal`)** tại bờ Đông Đền Ngàn Gió (`POI-12`) và **Cổ Thụ Bí Cảnh** tại Đỉnh Nam (`POI-09`) / Hẻm Núi Minh Quán (`POI-17`). |
| **3. Tiểu Cảnh Sinh Thái: Phong Thần Đồng & Tinh Điệp Phong** | `QNGM69SsKvfk`<br>`D4q9HSLOEm91` | • **`【原神】小物1`** (`.pmx`, gồm `风神瞳` Anemoculus, `晶蝶` Tinh Điệp, `风神之心`...)<br>• **`【原神】四风原典`** (`.pmx`, `859 DLs`) | Treo **Phong Thần Đồng (`Anemoculus`)** lơ lửng trên các di tích `POI-12..18` và thả **Tinh Điệp Phong (`Anemo Crystalfly`)** bay quanh gốc Đại Thụ Phong Khởi Địa (`POI-13`) & Vườn nho Dawn Winery (`POI-15`). |
| **4. Toàn Cảnh Thành Mondstadt Chi Tiết Cao (`.FBX` / `.BLEND`)** | `HsIbExgYEgQb`<br>`fxp98JFWWMhJ` | • **`【原神场景/Blender版】蒙德城Ver1.2`** (`7.720 DLs`)<br>• **`【原神】蒙德城`** (`.fbx + .blend`, `1.616 DLs`) | Bản rip chi tiết cao (đầy đủ đèn đường, biển hiệu, bồn hoa, cổng vòm, bậc thang) giúp trích xuất các prop trang trí đường phố Mondstadt mà bản `City_HLOD` gộp thô chưa có. |
| **5. Trọn Bộ 6 Nội Thất (`Interiors`) Biểu Tượng Của Mondstadt** | `r7M5ahDhxVGu`<br>`SnwyfGBqUPZo`<br>`gDlBWQ2h2lHm`<br>`Mt6M3WvADvDy`<br>`6SEweR5GZMEy`<br>`cHHeC4QHKXV9`<br>`XpvQOQLwskzR` | • **Nội thất Tửu Trang Dawn Winery** (`4.857 DLs`)<br>• **Quán rượu Angel's Share** (`2.548 DLs`)<br>• **Quán rượu Đuôi Mèo (`Cat's Tail`)** (`3.304 DLs`)<br>• **Đại sảnh Đội Kỵ Sĩ Tây Phong** (`6.382 DLs`)<br>• **Văn phòng Đội trưởng Jean** (`3.723 DLs`)<br>• **Thư viện Mondstadt** (`1.917 DLs`)<br>• **Đại Giáo Đường Tây Phong** (`6.407 DLs`) | Cho phép mở rộng tính năng **Đi vào trong nhà (`Enterable Interiors` / `enex` markers)** cho cả Dinh thự Dawn Winery (`POI-15` ở `M1`) lẫn 5 tòa nhà quan trọng nhất trong Thành Mondstadt (`M0`). |

- **Quy chuẩn chuyển đổi khi lấy từ `Aplaybox`**:
  - Lưu trữ các gói tải về vào `D:\GTA Archive\Mod Donor Library\ky6-world-filling-assets\aplaybox-packs\`.
  - Chuyển đổi `.pmx` / `.fbx` / `.blend` / `.obj` sang `.DFF + .TXD` (`DXT1 Mipmapped`) + `.COL3` (`body_sz >= 0x58`, `offsetVertices == 0x74`, không ghi `.COL` rỗng cho LOD) theo đúng chuẩn nén 4 tầng ở Mục 4 & Mục 5.

---

## 7. 6 Nội Thất Tòa Nhà Mondstadt Có Thể Bước Vào (`INT-01 .. INT-06`, `IDs 6696..6701`, `Area Code = 1` @ `Z = +1500.0m`)

- **Kiến trúc chuẩn GTA San Andreas (`Interior Heaven` + `Area Code` + `enex`)**:
  - Toàn bộ 6 nội thất được gộp sẵn (pre-merged) thành **1 Model `.DFF` + 1 `.COL3` duy nhất cho mỗi phòng (`0` LOD)**, đặt tại cao độ **`Z = +1500.0m`** với **`Interior ID = 1`** (`mondstadt_m1_interiors.ide` & `mondstadt_m1_interiors_enex.ipl`).
  - **Ảnh hưởng lên giới hạn Render Open World (`Area 0`) = `0%`**: Khi ở ngoài trời (`Area 0`), engine GTA SA tự động loại bỏ toàn bộ thực thể có `Interior ID != 0` trước bước tính khoảng cách, không tốn bất kỳ slot `Visible Entity Pointers`, draw call hay VRAM nào. Khi bước vào nội thất (`Area 1`), toàn bộ thế giới bên ngoài (`Area 0`) được ẩn hoàn toàn.
- **Danh sách 6 Nội Thất & Cổng Dịch Chuyển (`enex`)**:

| Mã Nội Thất | Model ID | Tên Model (`.dff`/`.col`) | Tòa Nhà Ngoài Trời (`Area 0`) & Cửa `enex` | Tọa Độ Phòng (`Area 1` @ `Z=+1500m`) | Đồ Đạc Nội Thất & Nhân Vật Genshin Chính Chủ Bên Trong |
| :--- | :---: | :--- | :--- | :--- | :--- |
| **`INT-01`** | `6696` | `int_dawn_winery` | **POI-15 Dinh Thự Tửu Trang Dawn Winery** `(-470.0, -567.0, -35.17)` | `(-500.0, -500.0, 1500.0)` | Thảm đỏ Mondstadt (`#607246`), Lò sưởi đá (`#607992`), Quầy rượu (`#613118`), Thùng gỗ thông (`#611751`), Bàn tiệc (`#608648`), Sofa (`#607001`), Chân nến vàng (`#610989`) & **Lão gia Diluc (`#328746`)** |
| **`INT-02`** | `6697` | `int_angels_share` | **M0 Quán Rượu Angel's Share** `(172.0, -48.0, -52.89)` | `(-200.0, -500.0, 1500.0)` | Quầy bar (`#613118`), 4 Ghế đẩu gỗ thông (`#607248`), Thùng rượu (`#611751`), Thảm quán rượu (`#607659`), Bàn dài (`#612500`), Đàn Phong Cầm (`#551363`), **Venti (`#328741`)** & **Kaeya (`#328743`)** |
| **`INT-03`** | `6698` | `int_fav_cathedral` | **M0 Đại Giáo Đường Tây Phong** `(-46.0, 16.0, -11.47)` | `(100.0, -500.0, 1500.0)` | Thảm hành lang đỏ (`#607246`), 6 hàng ghế gỗ giáo đường (`#608003`), Tượng Đá Cẩm Thạch & Đồng (`#604549`), Đàn Phong Cầm (`#551363`), Chân nến vàng (`#610989`), **Barbara (`#328747`)** & **Rosaria (`#514444`)** |
| **`INT-04`** | `6699` | `int_knights_hq` | **M0 Trụ Sở Đội Kỵ Sĩ Tây Phong** `(-25.0, -18.0, 0.43)` | `(400.0, -500.0, 1500.0)` | Bàn Đội Trưởng (`#612331`), Bàn hội nghị (`#608647`), Tủ sách lớn (`#611117`), Kệ sách Cuihua (`#612330`), Bàn thư viện (`#610642`), Lò sưởi (`#607992`), **Jean (`#328744`)** & **Lisa (`#328745`)** |
| **`INT-05`** | `6700` | `int_cats_tail` | **M0 Quán Rượu Đuôi Mèo (Cat's Tail)** `(198.0, -64.0, -52.75)` | `(-500.0, -200.0, 1500.0)` | Quầy pha chế (`#613118`), Thảm quán rượu (`#607659`), Sofa (`#607001`), Bàn gỗ (`#612500`), Chậu cây (`#607247`), **Diona (`#539022`)** & **6 Chú Mèo Mondstadt (`#606769`)** |
| **`INT-06`** | `6701` | `int_alchemy_lab` | **POI-09 Thành Cổ Đỉnh Nam & Bí Cảnh Cecilia** `(160.0, -652.0, 28.25)` | `(-200.0, -200.0, 1500.0)` | Bàn Giả Kim (`#532651`), 2 Thiết bị Giả Kim (`#612465`), Tủ sách nghiên cứu (`#611117`, `#612330`), Phong Thần Đinh (`#606515`), **Albedo (`#525577`)**, **Sucrose (`#538867`)** & **Klee (`#536287`)** |

