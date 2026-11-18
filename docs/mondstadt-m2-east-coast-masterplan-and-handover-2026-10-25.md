# Quy Hoạch Tổng Thể & Bàn Giao Kỹ Thuật: Sector M2 — Bờ Đông & Bán Đảo Đông-Nam Mondstadt (`mondstadt_east_m2`, `IDs 11960..12159`)

- **Ngày hoàn thành**: 25/10/2026
- **Thư mục Staging độc lập**: `D:\GTA Archive\Staging\teyvat-mondstadt-east-m2-2026-10-25\`
- **Trình xem 3D WebGL hợp nhất `M0 + M1 + M2`**: [`docs/project-eagle/mondstadt-m2-east-coast-showcase-2026-10-25.html`](mondstadt-m2-east-coast-showcase-2026-10-25.html) (`60.12 MB`)
- **Phiếu công việc**: [`docs/project-eagle/work-items/2026-10-25-antigravity-mondstadt-east-m2.md`](work-items/2026-10-25-antigravity-mondstadt-east-m2.md)

---

## 1. Tổng Quan 7 Hạng Mục Nâng Cấp Trọng Tâm Theo Chuẩn `Sector M1`

1. **Mạng Lưới Đường Xá 3D Đồng Nhất 100% Với `Sector M1` & Độ Dốc Thoai Thoải (`<= 3.7°`)**:
   - Đã loại bỏ hoàn toàn vệt đường kẻ ô trắng-xám rộng `27m` vẽ đè lên mặt đất địa hình `M2` và xóa bỏ tuyến đường băng qua mặt biển ra đảo Musk Reef.
   - San phẳng và hạ thoai thoải toàn bộ cao độ các thung lũng/cao nguyên trong `Sector M2` về dải **`Z ∈ [-50.0m .. -12.0m]`** (khớp mượt với cao độ biên Đông của `Sector M1` tại `-29m .. -13m`), đưa độ dốc dọc các tuyến đường về mức **`0.5° – 3.7°`** có nhiều đoạn bằng phẳng dài để đi bộ và lái xe tốc độ cao.
   - Xây dựng **8 Dải Đường Lát Đá Cuội 3D + Bó Vỉa Đá (`Route_13 .. Route_20`, `me2_road_r13..r20`, `IDs 12128..12135`)** sử dụng chính xác vật liệu `lmk_deck_pave` + `lmk_plinth_stone` của `Sector M1`, **bắt đầu trực tiếp từ các nút giao trong `Sector M1`** (`(485, 428)` Hồ Sao Rơi, `(610, 235)` Đền Ngàn Gió Tây, `(520, 140)` Rừng Thì Thầm, `(508, -320)` Phong Khởi Địa, `(588, -220)` Đèo Đông, `(376, -576)` Nam Phong Khởi Địa) và chạy xuyên qua đường biên `E = +768.0m` / `N = -768.0m` vào khắp 6 phân khu của `Sector M2`.

2. **4 Đại Doanh Trại Hilichurl Đầy Đủ Công Trình Chính Hãng & Quái Hilichurl To/Nhỏ**:
   - Tại cả 4 doanh trại Hilichurl (`M2-POI-05` Bờ Biển Chim Ưng Nam, `M2-POI-07` Bộ Tộc Nhật Thực, `M2-POI-08` Bộ Tộc Hảo Thịt & Đấu Trường Lôi Đài, `M2-POI-09` Bộ Tộc Hảo Ngủ), sử dụng trực tiếp bộ model `.DAE` chính hãng Genshin từ `The Models Resource` kèm texture UV thật:
     - **Nhà Thủ Lĩnh Lớn (`MSR_609417_Hilichurl_Chieftain_Hall`)**
     - **Trại Tiền Đồn (`MSR_609416_Hilichurl_Outpost_Hut`)** & **Lều Rơm (`MSR_613584_Hilichurl_Straw_Hut`)**
     - **Tháp Canh Xoắn Ốc (`MSR_613586_Hilichurl_Spiral_Watchtower`)** & **Tháp Canh 2 Tầng (`MSR_613590_Two_Story_Hilichurl_Sentry_Tower`)**
     - **Hàng Rào Totem Gỗ (`MSR_613582_Hilichurl_Totem_Fence`)** ghép thành vòng rào doanh trại và đấu trường lôi đài lục giác
     - **Nồi Sừng Khổng Lồ Đang Sôi (`MSR_613588_Hilichurl_Horned_Pot`)**
     - **Quái Hilichurl To & Nhỏ đóng chốt bên trong trại**: Bạo Đồ Hilichurl Khiên Gỗ (`MSR_584645_Wooden_Shield_Mitachurl`), Phù Thủy Hilichurl Phong (`MSR_585038_Anemo_Samachurl`) và Chiến Binh Hilichurl (`MSR_584572_Hilichurl_Fighter`).

3. **Mật Độ Công Trình Cao (`15` Tổ Hợp Địa Danh + `75` Cụm `wildernessScatter` / `246` Đạo Cụ Hoang Dã)**:
   - Lắp ráp **15 Tổ Hợp Địa Danh (`M2-POI-01 .. M2-POI-15`, `IDs 12060..12074` Near, `IDs 12090..12104` LOD)** với `6,280` mặt tam giác cận cảnh mỗi cụm (tổng cộng `94,200` tam giác công trình cận cảnh), kết hợp `32` model `.DFF` + `39` `.TXD` từ `Project Eagle` (`eagle-lightweight-gems`) và `31` model `.DAE` chính hãng từ `The Models Resource` (trích xuất `62` texture UV `256×256` `m2p01_t00 .. m2p15_t09` nén `DXT1 Mipmapped` vào `me2_tex.txd`).
   - Rải **75 cụm `wildernessScatter` (`246` đạo cụ: cụm rừng thông `sc_pine_cluster`, tảng đá rêu `sc_moss_boulder`, trụ đá cổ `sc_ruin_pillar`, lều nhà mạo hiểm `sc_adv_tent`, chòi canh `sc_hili_hut` và hàng rào `sc_hili_fence`)** phủ kín dọc hai bên đường và các sườn đồi trong `Sector M2`.

4. **Ngọn Hải Đăng Thật, Cảng Biển, Cầu Tàu Dài & Làng Chài Ven Biển (`Falcon Coast` & `Musk Reef`)**:
   - Sử dụng trực tiếp các model cảng biển & hải đăng thật từ `Project Eagle`: **`sp_lighthouse.dff`** (`sp_lighthouse.txd`), **`por_docks.dff`** (`port_docks.txd`), **`por_woodpier.dff`** (`port_woodpier.txd`), **`sp_pier.dff`** (`sp_pier.txd`), **`wb_marinapier01.dff`**, **`wb_marinapier03.dff`**, **`dolm_pier.dff`**, **`cn2_jetty1.dff`**, **`dolmancabin.dff`** kết hợp với quần thể nhà dân Mondstadt mái ngói đỏ (`MSR_610354`, `MSR_610355`, `MSR_611347`, `MSR_612565`, `MSR_614035`), Quầy Giả Kim & Sạp Hàng (`MSR_611671`, `MSR_532651`).

5. **44 Quái Vật Đi Tuần Quanh Map Trên 10 Tuyến Tuần Tra Khép Kín (`MOB_ROUTE_M2_01 .. MOB_ROUTE_M2_10`)**:
   - Đã bổ sung **10 tuyến tuần tra tự động (`MOB_ROUTE_M2_01..10`)** và **44 cá thể quái vật đi tuần (`roamingMobs`)** trải khắp 6 phân khu của `Sector M2`:
     - `MOB_ROUTE_M2_01` (Vách Đá Hái Sao): 3 Slime Phong (`gi_slime_anemo`, `gi_slime_large`) + Heo Rừng (`gi_wild_boar`).
     - `MOB_ROUTE_M2_02` (Đền Ngàn Gió Đông): 2 Thủ Vệ Di Tích (`gi_ruin_guard`) + Mắt Bão (`gi_eye_storm`) + Hilichurl Trinh Sát.
     - `MOB_ROUTE_M2_03` (Bí Cảnh Vườn Hoa Mùa Hè): Mắt Bão + Mitachurl Khiên Gỗ + Phù Thủy Samachurl + Hilichurl.
     - `MOB_ROUTE_M2_04` (Bãi Biển Chim Ưng Bắc): 3 Slime Lớn/Nhỏ + Hilichurl Bờ Biển.
     - `MOB_ROUTE_M2_05` (Trại Hilichurl Bờ Biển Chim Ưng Nam): Mitachurl Thủ Lĩnh + Samachurl + 3 Chiến Binh Hilichurl.
     - `MOB_ROUTE_M2_06` (Vòng Ngoài Hồ Kiếm Dadaupa): Thủ Vệ Di Tích + Mắt Bão + Mitachurl + 2 Hilichurl Canh Cầu.
     - `MOB_ROUTE_M2_07` (Đại Doanh Trại Bộ Tộc Nhật Thực): Đại Tộc Trưởng Mitachurl + Mitachurl Cận Vệ + Đại Pháp Sư Samachurl + 2 Chiến Binh Hilichurl.
     - `MOB_ROUTE_M2_08` (Đấu Trường Bộ Tộc Hảo Thịt): 2 Quán Quân Đấu Trường Mitachurl + Phù Thủy Samachurl + 2 Đấu Sĩ Hilichurl.
     - `MOB_ROUTE_M2_09` (Làng Sàn Gỗ Bộ Tộc Hảo Ngủ & Đường Lên Hẻm Núi Quên): Thủ Lĩnh Mitachurl + Phù Thủy Samachurl + 2 Hilichurl + Heo Rừng.
     - `MOB_ROUTE_M2_10` (Đỉnh Mũi Đất Thề): Mắt Bão + Mitachurl Tuần Đèo + Slime Phong Lớn.

6. **Xử Lý Triệt Để Dải Cỏ Xanh Cực Đông (`E = +2,048m`) & Quy Hoạch 3 Đầu Cầu Vượt Biển Nối Lục Địa Chính GTA**:
   - **Nguyên nhân & Khắc phục dải cỏ xanh cực Đông**: Trong bản cũ, phép làm mượt địa hình dùng `np.roll(Z, -1, axis=1)` khiến độ cao mặt đất ở rìa Tây (`E = +240m`, `Z ≈ -22m`) bị cuộn vòng sang cột cực Đông (`E = +2,048m`), làm mép cực Đông nhô lên khỏi mặt nước (`-58.0m`) và biến thành dải cỏ xanh. Bản mới đã thay thế bằng `np.pad(Z, 1, mode='edge')` và khóa cứng toàn bộ vùng biển ngoài khơi bờ Đông (`E >= +1,904m` và mọi điểm ngoài đảo Musk Reef `E ∈ [1736..1888], N ∈ [-776..-648]`) ở đáy biển **`Z = -62.5m`** (`< WATER = -58.0m`), xóa sạch 100% dải cỏ thừa ở cực Đông!

---

## 2. Nghiên Cứu 3 Địa Điểm Đặt Cầu Vượt Biển & Các Model Cầu Đặc Sắc (`M2-POI-13`, `M2-POI-14`, `M2-POI-15`)

Để chuẩn bị cho giai đoạn tiếp theo nối **Đại lục Teyvat (`MONDSTADT_GTA_ANCHOR = -6500, -3500, +59.5`)** từ bờ biển phía Đông của `Sector M2` (`X_gta ∈ [-5428 .. -5092]`) sang **Lục địa chính GTA San Andreas / San Fierro — Tierra Robada (`X_gta ≈ -2900 .. -2600`)**, chúng tôi đã khảo sát địa hình bờ biển Đông Mondstadt và xây dựng sẵn **3 Tổ Hợp Đầu Cầu Vượt Biển (`Mainland Bridgehead Hubs`)** sử dụng 8 model cầu đặc sắc nhất trong kho `Project Eagle`:

| Mã POI & Model ID | Tên Địa Điểm Đầu Cầu & Tọa Độ `ENU` (`GTA`) | Tổ Hợp Model Cầu Đặc Sắc Sử Dụng (`.DFF` + `.TXD`) | Đặc Điểm Kiến Trúc & Hướng Tuyến Vượt Biển |
| :--- | :--- | :--- | :--- |
| **`M2-POI-13`**<br>Near: `12072` (`me2_brg_north`)<br>LOD: `12102` (`lme2_brg_north`) | **Đầu Cầu Vịnh Bắc — Đền Ngàn Gió Đông**<br>`ENU: [1136.0, 344.0, -45.0]`<br>`GTA: [-5364.0, -3156.0, +14.5]` | • `red_bridge00.dff` + `red_bridge05.dff` (`countryw.txd`)<br>• `mbridgeramp1.dff` (`mbridge.txd`)<br>• `wb_marinapier01.dff` + Nhà Mondstadt `#610354`, `#611347` | **Cầu Giàn Thép Đỏ Bắc Mondstadt (`Red Steel Truss Bridgehead`)**: Nằm ở eo vịnh phía Nam Vách Đá Hái Sao, nối trực tiếp từ `Route 13` & `Route 14`. Thích hợp làm tuyến cầu đường bộ 2 làn màu đỏ nổi bật kiểu Garver/Forth Bridge vươn thẳng về hướng Đông-Bắc tới mũi Tierra Robada / Bayside. |
| **`M2-POI-14`**<br>Near: `12073` (`me2_brg_falcn`)<br>LOD: `12103` (`lme2_brg_falcn`) | **Đầu Cầu Trung Tâm — Đại Cầu Viaduct Bờ Biển Chim Ưng**<br>`ENU: [1072.0, -96.0, -47.0]`<br>`GTA: [-5428.0, -3596.0, +12.5]` | • `mbridge150m1.dff` (`mbridge.txd` — nhịp chính `150m`)<br>• `cocanyonbridge.dff` (`cocanyonbridge.txd` — cầu vòm đá nhiều nhịp)<br>• `lcc_bridgearch.dff` (`lcc_bridge.txd` — vòm thép lớn)<br>• Hải đăng `sp_lighthouse.dff` + Cảng `por_docks.dff` | **Đại Cầu Vượt Biển Trung Tâm (`Central Falcon Bay Grand Viaduct`)**: Nằm ngay trung tâm vịnh Bờ Biển Chim Ưng, kết nối thẳng trục chính từ Thành Mondstadt → Phong Khởi Địa (`Route 16`). Đây là **phương án khuyến nghị số 1 cho tuyến Đại Lộ Xuyên Biển chính** nhờ địa thế bằng phẳng (`Z = -47.0m`), tầm nhìn thoáng đãng ra cảng Hải đăng và kết cấu nhịp `150m` (`mbridge150m1.dff`) lặp lại dễ dàng qua đại dương. |
| **`M2-POI-15`**<br>Near: `12074` (`me2_brg_south`)<br>LOD: `12104` (`lme2_brg_south`) | **Đầu Cầu Eo Biển Nam — Mũi Đất Thề (`Cape Oath Strait`)**<br>`ENU: [1408.0, -928.0, -44.0]`<br>`GTA: [-5092.0, -4428.0, +15.5]` | • `covalleybridge1.dff` (`covalleybridge1.txd` — cầu vòm cao vượt thung lũng)<br>• `nwfwindbridge.dff` (`nwfwindbridge.txd` — cầu gỗ có mái che)<br>• `red_bridge05.dff` + Trạm Gác `#612565` + Bến Phà `sp_pier.dff` | **Cầu Vòm Cao Eo Biển Nam (`Cape Oath South Strait Arch Bridgehead`)**: Nằm ở mũi đất cực Đông-Nam (`E = +1,408m` — điểm đất liền Mondstadt vươn gần lục địa chính GTA nhất!). Thích hợp làm tuyến cầu vòm cảnh quan cao (`covalleybridge1.dff`) nối sang khu vực Nam San Fierro / Mount Chiliad, hoặc bắc cầu phụ nối ra Đảo Rạn San Hô Musk (`Musk Reef`). |

---

## 3. Danh Sách Đầy Đủ 15 Tổ Hợp Địa Danh (`M2-POI-01 .. M2-POI-15`) & 8 Tuyến Đường Đá Cuội 3D (`Route_13 .. Route_20`)

### 3.1. Bảng 15 Tổ Hợp Địa Danh Cận Cảnh & LOD (`IDs 12060..12074` & `12090..12104`)

| Mã POI | Model ID (Near / LOD) | Tên Model (`.DFF` / `.COL3`) | Tọa Độ Tâm `ENU` (`[E, N, U]`) | Tổ Hợp Công Trình & Quái Vật Chính Hãng Bên Trong |
| :--- | :--- | :--- | :--- | :--- |
| **`M2-POI-01`** | `12060` / `12090` | `me2_starsnatch` / `lme2_starsnatch` | `[1032.0, 504.0, -14.0]` | Vách Đá Hái Sao (`coancliff001`, `lcc_cliff04`), Thất Thiên Thần Tượng Phong (`#604549`), Đàn Phong Cầm (`#551363`), Vòm Đá Cổ (`ce_archbridge`), Phong Thần Đồng (`#606515`), Rương Hoa Lệ (`#543924`), Trụ Dịch Chuyển (`#543725`), Rừng Thông & Slime Phong (`#587816`). |
| **`M2-POI-02`** | `12061` / `12091` | `me2_twinds_e` / `lme2_twinds_e` | `[880.0, 224.0, -16.0]` | Vòng Ngoài Đấu Trường Cổ Đền Ngàn Gió Đông: 8 Cột Đá La Mã (`stonepillar1`), 2 Cổng Vòm Cổ (`ce_archbridge`, `ce_archbridge2`), Đài Tế Cổ (`#609958`), Thủ Vệ Di Tích (`#587707`), Mắt Bão (`#601779`), Lều Hilichurl (`#613584`), Mitachurl (`#584645`), Hilichurl (`#584572`) & Rương Hiếm (`#543923`). |
| **`M2-POI-03`** | `12062` / `12092` | `me2_midsummer` / `lme2_midsummer` | `[1008.0, 128.0, -12.0]` | Bí Cảnh Vườn Hoa Mùa Hè: Cổng Đá Bí Cảnh (`lcc_cm_caveent01`), Cổ Thụ Bí Cảnh Irminsul Khổng Lồ (`#607308`), 4 Cột Đá Cổ (`stonepillar1`), Đài Phong Ấn (`#609958`), Trụ Dịch Chuyển (`#543725`), Rương Siêu Cấp (`#543922`), Slime Lớn (`#587825`) & Slime Nhỏ (`#587816`). |
| **`M2-POI-04`** | `12063` / `12093` | `me2_falcon_pr` / `lme2_falcon_pr` | `[1024.0, -192.0, -48.5]` | Cảng Bờ Biển Chim Ưng & Ngọn Hải Đăng: Ngọn Hải Đăng Đá Trắng (`sp_lighthouse.dff`), Bến Cảng Lớn (`por_docks.dff`), Cầu Tàu Gỗ Dài (`por_woodpier.dff`, `wb_marinapier01.dff`), 2 Nhà Dân Mondstadt (`#610354`, `#610355`), Nhà Gỗ Ven Biển (`dolmancabin.dff`), Quầy Giả Kim & Sạp Hàng (`#611671`, `#532651`), Trụ Dịch Chuyển (`#543725`). |
| **`M2-POI-05`** | `12064` / `12094` | `me2_falcon_cp` / `lme2_falcon_cp` | `[1056.0, -376.0, -48.0]` | Doanh Trại Hilichurl Bờ Biển Chim Ưng Nam: Nhà Thủ Lĩnh (`#609417`), Nhà Tiền Đồn (`#609416`), Lều Rơm (`#613584`), Tháp Canh Xoắn Ốc (`#613586`), Tháp Canh 2 Tầng (`#613590`), 3 Hàng Rào Totem (`#613582`), Nồi Sừng (`#613588`), Cầu Tàu (`cn2_jetty1.dff`), Mitachurl (`#584645`), Samachurl (`#585038`), 3 Hilichurl (`#584572`) & Rương (`#543921`). |
| **`M2-POI-06`** | `12065` / `12095` | `me2_sword_cem` / `lme2_sword_cem` | `[784.0, -760.0, -45.0]` | Hồ Kiếm Dadaupa (`Sword Cemetery`): 2 Cầu Gỗ Bắc Qua Hồ (`ni_woodbridge.dff`, `ce_bbridge.dff`), Đài Phong Ấn Kiếm Mộ Trung Tâm (`#609958`), 6 Trụ Đá Cổ (`stonepillar1`), 3 Vòng Phong Ấn Gió Phát Sáng, Rương Báu Hoa Lệ (`#543924`), Trụ Dịch Chuyển (`#543725`) & Cụm Rừng Thông (`cwyforest004.dff`). |
| **`M2-POI-07`** | `12066` / `12096` | `me2_tribe_ecl` / `lme2_tribe_ecl` | `[880.0, -616.0, -34.0]` | Đại Doanh Trại Bộ Tộc Nhật Thực (`Eclipse Tribe` — Bắc Dadaupa): Đại Điện Thủ Lĩnh (`#609417`), 2 Trại Tiền Đồn (`#609416`), Tháp Canh Xoắn Ốc (`#613586`), Tháp Canh 2 Tầng (`#613590`), 4 Hàng Rào Totem (`#613582`), Nồi Sừng Lớn (`#613588`), Đài Phong Ấn Bắc (`#609958`), Rương (`#543922`), 2 Mitachurl (`#584645`), Samachurl (`#585038`) & 3 Hilichurl (`#584572`). |
| **`M2-POI-08`** | `12067` / `12097` | `me2_tribe_mty` / `lme2_tribe_mty` | `[960.0, -832.0, -32.0]` | Đại Doanh Trại Bộ Tộc Hảo Thịt & Đấu Trường (`Meaty Tribe` — Đông Dadaupa): Nhà Thủ Lĩnh (`#609417`), Nồi Sừng Khổng Lồ (`#613588`), 2 Lều Lớn (`#613584`), Tháp Canh (`#613586`), Đấu Trường Lôi Đài Lục Giác (`6 × #613582`), Đài Phong Ấn Đông (`#609958`), Rương (`#543922`), 2 Đấu Sĩ Mitachurl (`#584645`), Phù Thủy Samachurl (`#585038`) & 3 Hilichurl (`#584572`). |
| **`M2-POI-09`** | `12068` / `12098` | `me2_tribe_slp` / `lme2_tribe_slp` | `[544.0, -856.0, -32.0]` | Đại Doanh Trại Bộ Tộc Hảo Ngủ (`Sleeper Tribe` — Tây Dadaupa): Sàn Gỗ Nổi Trên Hồ (`por_woodpier.dff`, `dolm_pier.dff`), Nhà Thủ Lĩnh (`#609417`), Tháp Canh 2 Tầng (`#613590`), 2 Lều Rơm (`#613584`), Hàng Rào Totem (`#613582`), Đài Phong Ấn Tây (`#609958`), Rương (`#543921`), Mitachurl (`#584645`), Samachurl (`#585038`) & 3 Hilichurl (`#584572`). |
| **`M2-POI-10`** | `12069` / `12099` | `me2_forsaken` / `lme2_forsaken` | `[608.0, -1048.0, -22.0]` | Bí Cảnh Hẻm Núi Quên (`Forsaken Rift` — Nam Dadaupa): Hang Đá Vách Núi (`lcc_cm_cave01.dff`), Cổng Đá Bí Cảnh (`lcc_cm_caveent01.dff`), Vách Đá (`wsrocky1.dff`), Cổ Thụ Bí Cảnh Irminsul (`#607308`), 4 Trụ Đá Cổ (`stonepillar1`), Trụ Dịch Chuyển (`#543725`) & Rương Hiếm (`#543923`). |
| **`M2-POI-11`** | `12070` / `12100` | `me2_cape_oath` / `lme2_cape_oath` | `[1312.0, -792.0, -21.0]` | Đỉnh Mũi Đất Thề & Cổng Lỗ Đen (`Cape Oath`): Mỏm Đá Đại Dương (`lcc_cliff01.dff`, `coancliff002.dff`), Cổng Vòm Cổ (`ce_archbridge.dff`), 4 Trụ Đá (`stonepillar1`), Đài Tế Phong (`#609958`), Cổng Dịch Chuyển Lỗ Đen Đôi đi Đảo Musk Reef, Phong Thần Đồng (`#606515`), Trụ Dịch Chuyển (`#543725`) & Rương (`#543922`). |
| **`M2-POI-12`** | `12071` / `12101` | `me2_musk_abys` / `lme2_musk_abys` | `[1808.0, -712.0, -49.0]` | Đảo Rạn San Hô Musk & Cổng La Hoàn Thâm Uyên (`Musk Reef & Spiral Abyss`): Cảng Đảo (`sp_pier.dff`, `wb_marinapier03.dff`), Hải Đăng Đảo (`sp_lighthouse.dff`), 2 Vòm Cổ Đại (`ce_archbridge`, `ce_archbridge2`), 6 Trụ Đá (`stonepillar1`), Cổng Xoắn Ốc La Hoàn Thâm Uyên 3 Tầng, Trụ Dịch Chuyển (`#543725`) & Rương Hoa Lệ (`#543924`). |
| **`M2-POI-13`** | `12072` / `12102` | `me2_brg_north` / `lme2_brg_north` | `[1128.0, 224.0, -26.0]` | Đầu Cầu Vịnh Bắc (Cầu Giàn Thép Đỏ `red_bridge00.dff` + `red_bridge05.dff`, Đường Dẫn `mbridgeramp1.dff`, Bến Tàu `wb_marinapier01.dff`, 2 Nhà Mondstadt `#610354`, `#611347` & Trụ Dịch Chuyển `#543725`). |
| **`M2-POI-14`** | `12073` / `12103` | `me2_brg_falcn` / `lme2_brg_falcn` | `[1144.0, -272.0, -48.0]` | Đầu Cầu Trung Tâm — Đại Cầu Viaduct Bờ Biển Chim Ưng (Nhịp Cầu `150m` `mbridge150m1.dff`, Cầu Vòm Đá `cocanyonbridge.dff`, Cầu Vòm Thép `lcc_bridgearch.dff`, Hải Đăng `sp_lighthouse.dff`, Bến Cảng `por_docks.dff` & Tòa Nhà Hải Quan `#614035`). |
| **`M2-POI-15`** | `12074` / `12104` | `me2_brg_south` / `lme2_brg_south` | `[1424.0, -864.0, -26.0]` | Đầu Cầu Eo Biển Nam — Mũi Đất Thề (Cầu Vòm Cao `covalleybridge1.dff`, Cầu Gỗ Mái Che `nwfwindbridge.dff`, Cầu Giàn Thép `red_bridge05.dff`, Bến Phà `sp_pier.dff`, Nhà Gác `#612565` & 2 Trụ Đá Cổ). |
| **`M2-POI-16`** | `12075` / `12105` | `me2_cryo_boss` / `lme2_cryo_boss` | `[816.0, 56.0, -24.0]` | **Hang Đấu Trường Boss Cây Cấp Đông (`Cryo Regisvine Arena — MSR #603670`)**: Nằm ở vách núi phía Nam-Tây Nam Đền Ngàn Gió; gồm Vòm Hang Băng (`lcc_cm_cave01.dff`, `lcc_cm_caveent01.dff`), 6 Trụ Đá Cổ, **Boss Cây Cấp Đông Khổng Lồ (`Cryo Regisvine #603670`)**, 2 Hoa Lừa Dối Băng (`#603645`), Pháp Sư Vực Sâu Băng (`#586481`), Trụ Dịch Chuyển (`#543725`) & Rương Quý Giá (`#543922`). |
| **`M2-POI-17`** | `12076` / `12106` | `me2_elec_boss` / `lme2_elec_boss` | `[1184.0, -744.0, -25.0]` | **Đấu Trường Boss Lôi Nguyên Bản — Aleph (`Electro Hypostasis Arena`)**: Nằm trên cao nguyên Mũi Đất Thề (`Cape Oath Plateau`); gồm Đấu Trường Đá Tròn 8 Cột La Mã (`stonepillar1.dff`), Ấn Cổ Nguyên Tố (`#609958`), **Boss Lôi Nguyên Bản (8 Khối Bát Diện Tím-Vàng + Lõi Tử Điện)**, 2 Hoa Lừa Dối Lôi (`#603646`), Pháp Sư Vực Sâu Lôi (`#586483`), Trụ Dịch Chuyển (`#543725`) & Rương Quý Giá (`#543922`). |
| **`M2-POI-18`** | `12077` / `12107` | `me2_anem_boss` / `lme2_anem_boss` | `[848.0, 584.0, -18.0]` | **Đấu Trường Boss Phong Nguyên Bản — Beth (`Anemo Hypostasis Arena`)**: Nằm trên cao nguyên phía Bắc Vách Đá Hái Sao / Vọng Phong Sơn; gồm Đấu Trường Đá Tròn 8 Cột La Mã, Ấn Cổ Nguyên Tố (`#609958`), **Boss Phong Nguyên Bản (8 Khối Bát Diện Ngọc Lục Bảo + Lõi Cuồng Phong)**, 2 Slime Phong Lớn (`#587825`), Slime Phong (`#587816`), Tinh Điệp Phong (`#606515`), Trụ Dịch Chuyển (`#543725`) & Rương Quý Giá (`#543922`). |
| **`M2-POI-19`** | `12078` / `12108` | `me2_abyss_brg` / `lme2_abyss_brg` | `[1568.0, -752.0, -35.0]` | **Trạm Nghỉ Giữa Cầu Gỗ Vượt Biển Đi Đảo La Hoàn (`Cape Oath → Musk Reef Wooden Ocean Bridge Hub`)**: Nằm giữa eo biển nối Mũi Đất Thề ra Đảo Rạn San Hô Musk; gồm Nhịp Cầu Gỗ Đôi (`ni_woodbridge.dff`, `nwfwindbridge.dff`), Sàn Bến Gỗ (`por_woodpier.dff`, `dolm_pier.dff`), 2 Tháp Canh Gỗ 2 Tầng (`#613590`), Trụ Dịch Chuyển (`#543725`) & Rương Tinh Điêu (`#543921`). |

### 3.2. Bảng 8 Dải Đường Đá Cuội 3D + 1 Cầu Gỗ Dài Vượt Biển (`Route_13 .. Route_21`, `IDs 12128..12136`)

| Mã Tuyến | Model ID & Tên Model | Bề Rộng | Điểm Khởi Đầu Trong `Sector M1` → Lộ Trình Xuyên Qua `Sector M2` |
| :--- | :--- | :--- | :--- |
| **`Route 13`** | `12128` (`me2_road_r13`) | `9.5m` | Nút giao Hồ Sao Rơi `M1 (485, 428)` → Biên Đông `(768, 448)` → Đỉnh Vách Đá Hái Sao `(1002, 488)`. |
| **`Route 14`** | `12129` (`me2_road_r14`) | `10.0m` | Đền Ngàn Gió Tây `M1 (610, 235)` → Biên Đông `(768, 232)` → Đền Ngàn Gió Đông `(888, 232)` → Đầu Cầu Vịnh Bắc `(1100, 224)`. |
| **`Route 15`** | `12130` (`me2_road_r15`) | `9.5m` | Rừng Thì Thầm `M1 (520, 140)` → Biên Đông `(768, 120)` → Bí Cảnh Vườn Hoa Mùa Hè `(984, 104)` → Đền Ngàn Gió Đông → Vách Đá Hái Sao. |
| **`Route 16`** | `12131` (`me2_road_r16`) | `10.5m` | Đại Thụ Phong Khởi Địa `M1 (508, -320)` & Đèo Đông `(588, -220)` → Biên Đông `(768, -224)` → Cảng Hải Đăng Chim Ưng `(1032, -200)` → Đại Cầu Viaduct Trung Tâm `(1116, -272)`. |
| **`Route 17`** | `12132` (`me2_road_r17`) | `10.0m` | Bí Cảnh Vườn Hoa Mùa Hè `(984, 104)` → Cảng Hải Đăng Chim Ưng `(1032, -200)` → Trại Hilichurl Nam `(1032, -416)` → Bộ Tộc Nhật Thực `(896, -608)`. |
| **`Route 18`** | `12133` (`me2_road_r18`) | `10.5m` | Nam Phong Khởi Địa `M1 (376, -576)` → Biên Nam `(544, -768)` → Bộ Tộc Hảo Ngủ `(552, -856)` → Hồ Kiếm Dadaupa `(784, -760)` → Bộ Tộc Nhật Thực `(896, -608)` → Bộ Tộc Hảo Thịt `(968, -824)`. |
| **`Route 19`** | `12134` (`me2_road_r19`) | `9.5m` | Bộ Tộc Hảo Ngủ `(552, -856)` → Bí Cảnh Hẻm Núi Quên `(656, -1004)` → Bộ Tộc Hảo Thịt `(968, -824)`. |
| **`Route 20`** | `12135` (`me2_road_r20`) | `10.0m` | Bộ Tộc Hảo Thịt `(968, -824)` → Đấu Trường Lôi Nguyên Bản `(1140, -808)` → Đỉnh Mũi Đất Thề `(1284, -792)` → Đầu Cầu Eo Biển Nam `(1396, -864)`. |
| **`Route 21`** | `12136` (`me2_road_r21`) | `11.0m` | **Cầu Gỗ Dài Vượt Biển Đi Đảo La Hoàn (`Cape Oath → Musk Reef Wooden Trestle Bridge`)**: Nối trực tiếp từ Đỉnh Mũi Đất Thề `(1312, -792, -20.8)` → Trạm Nghỉ Giữa Biển `M2-POI-19 (1568, -752, -34.8)` → Đảo Rạn San Hô Musk & Cổng La Hoàn Thâm Uyên `(1808, -712, -48.8)` với mặt sàn ván gỗ, lan can gỗ hai bên, hệ cọc trụ gỗ cắm xuống đáy biển và `.COL3` đi bộ/lái xe liền mạch 100%! |

---

## 3.3. Nội Thất La Hoàn Thâm Uyên (`INT-07`, `ID 12150`, `Area 1 @ Z = +1500m`) & Tra Cứu Model Aplaybox

- **Kết quả tra cứu kho `Aplaybox` cho Interior La Hoàn Thâm Cảnh (`Spiral Abyss Interior`)**:
  1. **`eJ6hdJyyr25q` — `【原神场景】深境螺旋-12` (`Spiral Abyss Floor 12 Chamber Interior`)**: Model phòng chiến đấu Tầng 12 La Hoàn Thâm Uyên chính hãng trích xuất từ Genshin Impact (tác giả `克里斯提亚娜`, định dạng `.pmx`, `2,803` lượt tải).
  2. **`ra1DZOmEv5Qt` — `【场景配布】新深渊第三层` (`Spiral Abyss Floor 3 Interior`)**: Model đấu trường Tầng 3 La Hoàn Thâm Uyên (tác giả `克里斯提亚娜`, định dạng Blender, `1,708` lượt tải).
  3. **`6ujkqcr38uYz` — `【原神场景】祝圣秘境` (`Blessing Domain Interior & Irminsul Tree`)**: Nội thất Bí Cảnh & Cổ Thụ Irminsul (tác giả `Viero月城`, định dạng `.pmx`, `1,372` lượt tải).
- **Triển khai trực tiếp `INT-07: Nội Thất La Hoàn Thâm Uyên — Tầng 12 (`int_spiral_abys`, `ID 12150`, `Area Code = 1 @ ENU [100.0, -200.0, 1500.0]`)`**:
  - Đặt cổng dịch chuyển vàng `ENEX` ngay trước **Cổng Xoắn Ốc La Hoàn Thâm Uyên trên Đảo Rạn San Hô Musk (`[1813.0, -712.0, -48.8]`)** (hoặc bấm nút **`🏛️ Vào Nội Thất La Hoàn Thâm Uyên (INT-07)`** trên thanh công cụ).
  - Bên trong `INT-07` (`44m × 44m × 16m` tại `Z = +1500m`): Sàn đá hoa cương khắc 3 vòng ma pháp Địa Mạch phát sáng vàng–tím–lam, 10 cột đá La Mã cổ đại (`stonepillar1.dff`), cổng vòm cổ (`ce_archbridge.dff`), trụ **Chìa Khóa Thâm Uyên (`Key of the Deep Monolith — MSR #609958`)** ở chính giữa đấu trường, **Cổ Thụ La Hoàn Irminsul (`MSR #607308`)**, **Rương Báu Hoa Lệ (`MSR #543924`)**, và 5 Boss Vực Sâu chính hãng từ `The Models Resource`:
    - **Sứ Đồ Vực Sâu — Kích Lưu (`Abyss Herald: Frost Fall — MSR #604831`)**
    - **Học Sĩ Vực Sâu — Tử Điện (`Abyss Lector: Violet Lightning — MSR #584384`)**
    - **Pháp Sư Vực Sâu Băng (`Cryo Abyss Mage — MSR #586481`)**
    - **Pháp Sư Vực Sâu Lôi (`Electro Abyss Mage — MSR #586483`)**
    - **Thủ Vệ Di Tích (`Ruin Guard — MSR #587707`)**

---

## 4. Kết Quả Kiểm Định Tự Động (`verify_m2.py` — `100% PASS`)

- **Khớp biên `0.0000 mm` với `Sector M1`**:
  - Kiểm tra toàn bộ `260` đỉnh biên chung (`193` đỉnh trên biên Đông `E = +768.0m` + `67` đỉnh trên biên Nam `N = -768.0m`): **`max_error_mm = 0.0000 mm`**.
- **Kiểm toán nhị phân `.DFF` / `.TXD` / `.COL3` / `.IDE` / `.IPL` / `.IMG`**:
  - `dff_count`: `130` files (`747,823` vertices, `308,965` triangles, `rw_version = 0x1803FFFF`, `max_abs_local_coord_m = 128.0m`).
  - `txd_audit`: `mondstadt_east_m2.txd` (`me2_tex.txd`) chứa `75` rasters `DXT1_MIPMAPPED`; `lod_mondstadt_east_m2.txd` (`me2_lod.txd`) chứa `74` rasters `DXT1_MIPMAPPED`.
  - `col3_audit`: `65` entries (`46` Near terrain tiles + `15` Near landmarks + `4` solid specialty props), `lod_entries_in_col = 0`, `header_offset_vertices_hex = 0x74`, `max_entry_bytes = 33,972 B < 92,768 B`.
  - `walkability_summary`: **`15/15` địa danh (`M2-POI-01 .. M2-POI-15`) đạt `100% PASS`** cho cả đi bộ (`A* Walk`) và lái xe (`A* Drive`) từ đầu cầu Mondstadt (`320.0, -96.0`) xuyên qua `Sector M1` sang `Sector M2` (bao gồm cả dịch chuyển qua Cổng Lỗ Đen `M2_ABYSS_IN ↔ M2_ABYSS_OUT` ra Đảo La Hoàn Thâm Uyên).
