# Quy Hoạch Lấp Đầy Mặt Tiền Đường & Mật Độ Đô Thị (`Perimeter Streetwall Infill Plan`) Cho `INLAND-03A` (Bắc Chicago)

- **Ngày lập**: `01/11/2026`
- **Tác giả**: `Antigravity` (`183449f8-aedb-4f83-95af-85c72771adcd`)
- **Đích áp dụng**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\CUSTOM\inland03a_sakura_chicago.ipl`
- **Bản vẽ so sánh Trước & Sau 3D Low-Detail**: [`evidence/inland03a_perimeter_infill_3d_blueprint.png`](evidence/inland03a_perimeter_infill_3d_blueprint.png)
- **Dữ liệu tọa độ 1,015 instances**: [`D:\GTA Archive\Staging\inland03a-sakura-chicago-2026-11-01\inland03a_perimeter_infill_instances.json`](file:///d:/GTA%20Archive/Staging/inland03a-sakura-chicago-2026-11-01/inland03a_perimeter_infill_instances.json)

---

## 1. Nguyên Tắc Thiết Kế Đô Thị Theo Chỉ Đạo Của Người Dùng

1. **Đưa cổng và mặt tiền công trình ra sát mép vỉa hè (`Perimeter Block / Streetwall`)**:
   - Thay vì đặt 1–2 công trình nằm lọt thỏm ở tâm ô đất rộng `220m × 270m` để lộ nền đất trống, toàn bộ các tòa nhà được dịch chuyển ra bám sát mép vỉa hè của **4 trục đường bao quanh ô phố (`Bắc - Nam - Đông - Tây`)**, xoay mặt tiền/cổng quay thẳng ra lòng đường.
   - Tạo thành "bức tường phố" (`continuous streetwall`) liên tục dọc theo cả 5 đại lộ dọc (`Ave 1..5`) và 5 đại lộ ngang (`South Border, Cross 1..4`).
2. **Xóa bỏ triệt để "Nhà mỏng như tờ giấy" tại Quảng trường `C3` (`PDFT Puzzle Stage #193789`)**:
   - Đã loại bỏ hoàn toàn **7 model tấm phông nền 2D mỏng / khung lưới rỗng** (`12254..12258, 12260, 12261`: `in03_puz_1`, `in03_puz_2`, `in03_puz_p1..p3`, `in03_puz_p5`, `in03_puz_w1`).
   - Chỉ giữ lại **sàn quảng trường & bục biểu diễn trung tâm khối đặc** (`12253 in03_puz_main` và `12259 in03_puz_p4`), đồng thời **dựng 10 tòa cao ốc/cửa hiệu 3D khối đặc 4 mặt (`in03_akiba_twr1`, `in03_otaku_shop`, `in03_kawaii_v1`) bao kín 4 cạnh mặt tiền đại lộ quanh quảng trường**, biến `C3` thành một quảng trường sự kiện thực thụ giữa lòng khu phố Akihabara.
3. **Tăng mật độ công trình 3D từ `117` lên `327` tòa nhà (`+210` tòa nhà 3D khối đặc, tổng `1,015` IPL instances)**:
   - Lấp kín hoàn toàn **Dải Cửa Ngõ Phía Nam (`Row 0: Y = 10042..10185`)** ngay sau 5 mối hàn `WELD-1..5` (trước đây trống 100%).
   - Lấp kín mặt tiền 4 cạnh của toàn bộ các ô quy hoạch thuộc **Phân khu A (Học viện)**, **Phân khu B (Phố Nhật Nobita & Phố Ramen)**, **Phân khu C (Akihabara & Quảng trường Miku)** và **Phân khu D (Thương mại, Cao ốc, Showroom, Biệt thự ven vịnh & Rừng thông Bắc)**.

---

## 2. Bảng Phân Bổ Chi Tiết Theo Từng Ô Quy Hoạch (`Row 0 .. Row 4`)

| Dải Ô Phố | Tọa Độ `(X, Y)` | Trước Khi Fill | Sau Khi Fill (`Perimeter Streetwall`) | Giải Pháp Bố Cục Mặt Tiền Đường |
| :--- | :--- | :---: | :---: | :--- |
| **Row 0 (`S0..S4`)**<br>*Cửa Ngõ Nam Bắc Chicago* | `X = [5650..6710]`<br>`Y = [10042..10185]` | `0` tòa nhà<br>*(Trống 100%)* | **`31` tòa nhà 3D** | Xếp kín hai bên `Ave 1 (WELD-1)`, `Ave 2 (WELD-2)`, `Sakura Blvd (WELD-3)` và `South Border Blvd` bằng các khối cao ốc `Akiba Tower (12244)`, `OtakuShoppu (12249)`, `Kawaii (12250..12252)`, `Nagato Hall (12226)` và biệt thự `Villa F (12278)`. |
| **Row 1 — Khu A (`A0, A1/A2`)**<br>*Quần Thể Học Viện Escuela* | `X = [5650..6090]`<br>`Y = [10214..10465]` | `4` tòa nhà | **`29` tòa nhà 3D** | Đưa cổng chính `Escuela High School (12220)` + hai cánh `Nagato Hall (12226)` ra sát mặt đường `Cross-1W` & `Cross-2`; viền 2 cạnh `Ave 1` & `Ave 2` bằng `Anime Club (12225)` và `CasaCampo (12224)`; bố trí `8` dãy lớp học `Classroom (12221)` quanh sân trường trung tâm. |
| **Row 1 — Khu B (`B1/B2`)**<br>*Phố Nobita & Bãi Ống Cống* | `X = [6121..6303]`<br>`Y = [10214..10465]` | `4` tòa nhà | **`16` tòa nhà 3D** | Giữ `Bãi Ống Cống (12237)` bám sát góc Tây-Nam; xếp chuỗi **`14` căn nhà dân Nhật Bản 2 tầng (`in03_nobita_h1`, `32m × 41m`)** nối tiếp nhau kín suốt mặt tiền `Sakura Central Blvd`, `Cross-2` và `Ave 2`. |
| **Row 1 — Khu C (`C1, C2`) & Đông**<br>*Little Akihabara & OtakuShoppu* | `X = [6335..6945]`<br>`Y = [10214..10465]` | `12` tòa nhà | **`28` tòa nhà 3D** | Khép kín 4 mặt tiền `Block C1` và `Block C2` bằng `Akiba Tower (12244)`, `OtakuShoppu (12249)`, `Kawaii (12250..12252)`; bổ sung dãy biệt thự ven vịnh `Villa F` & `New Mansion` ở rìa Đông (`X = 6780..6900`). |
| **Row 2 — Khu A (`A4, A3`)**<br>*Sân Trượt Băng & Sân Bóng Đá* | `X = [5650..6090]`<br>`Y = [10494..10735]` | `9` tòa nhà | **`23` tòa nhà 3D** | Giữ `Sân Trượt Băng (12230..12231)` làm tâm `A4` và lấp cạnh Bắc bằng `Nagato Hall + Anime Club`; bao quanh `Sân Bóng Đá (12223)` ở `A3` bằng **12 tòa nhà học viện** bám kín 4 mặt đường `Ave 1`, `Ave 2`, `Cross-2`, `Cross-3`. |
| **Row 2 — Khu B (`B3/B4`)**<br>*Phố Mì Ichiraku & Chợ Đêm* | `X = [6121..6303]`<br>`Y = [10494..10735]` | `4` tòa nhà + xe mì | **`21` tòa nhà 3D** + xe mì | Xếp **14 quán mì `Ichiraku Ramen (12240)`** dọc kín hai mặt tiền `Ave 2` & `Sakura Central Blvd`, kết hợp `4` quán `Starbucks (12267)` ở mặt tiền Bắc/Nam và khu chợ đêm ở lõi giữa. |
| **Row 2 — Khu C (`C3, C4`)**<br>*Quảng Trường 3 Sân Khấu Miku* | `X = [6335..6712]`<br>`Y = [10494..10735]` | `3` sân khấu + `7` tấm phông giấy 2D | **`23` tòa nhà 3D đặc** + `3` sân khấu | **Xóa sạch 7 tấm phông giấy 2D ở `C3`**. Bao quanh cả `C3 (Puzzle Stage)` và `C4 (Romeo & World Is Mine)` bằng **20 tòa cao ốc/shophouse 3D khối đặc** (`Akiba Tower`, `OtakuShoppu`, `Kawaii`) bám sát 4 mặt tiền đại lộ. |
| **Row 2 & 3 — Khu D (`D0..D6`)**<br>*Cao Ốc, Siêu Thị, Showroom, Biệt Thự* | `X = [5650..6950]`<br>`Y = [10494..11065]` | `18` tòa nhà | **`98` tòa nhà 3D** | Viền kín 4 mặt tiền quanh `Avengers HQ (D1)`, `Tallest Tower & Starbucks (D2/D6)`, `Walmart & IKEA (D3)`, `Car Showroom & Modern Mansion (D4)` và đồi biệt thự `Villa F / New Mansion (D5)`. |
| **Row 4 (`D7, D8`)**<br>*Vành Đai Bắc, Trạm Nghỉ & Rừng Thông* | `X = [5650..6950]`<br>`Y = [11094..11220]` | `8` tòa nhà + `48` cây thông | **`13` tòa nhà** + **`124` cây thông** | Bổ sung dãy trung tâm thương mại dọc Vành đai Bắc (`X = 5720..6080`) và mở rộng rừng thông/redwood (`sm_redwood_`, `vbg_fir_copse`) phủ kín toàn bộ dải công viên phía Bắc (`X = 6400..6920`). |

---

## 3. Kiểm Định Dẫn Đường GPS (`pecore_gps_graph.pegg`) & `EagleRide` (`PeggGraphRouter`) Từ 4 Hướng Ngoài Thành Phố & Nội Thành

- **Đồ thị `data/pecore_gps_graph.pegg`**:
  - Tổng cộng **`148,637` nodes / `253,196` edges** (`+202` road-centerline nodes rải đều mỗi `~60m` dọc theo toàn bộ 5 đại lộ dọc `Ave 1..5`, 4 đại lộ ngang `Cross 1..4`, `South Border Blvd`, nhánh Tây `A2/A4`, đồi biệt thự Đông `D5/D8` và trạm dừng Vành đai Bắc `D7`).
  - **`202 / 202` (`100%`)** node mới nằm trong thành phần liên thông chính của toàn thế giới (`main_comp`), kết nối trực tiếp vào mạng lưới Bắc Chicago tại các mối hàn thực tế (`137911`, `137903`, `137832`, `137946`, `137938`, `137937`, `137929`, `137685`).
  - Đã kiểm tra va chạm biên hình học (`3D World Bounding Box`) của toàn bộ **`324` công trình 3D** với tất cả các làn đường dọc/ngang: **`0` công trình lấn làn đường (`Total road encroachments found: 0`)**.
- **Bản đồ & Bảng ảnh Nghiệm thu In-Game**:
  - Sơ đồ 9 tuyến dẫn đường (`4 hướng ngoài thành phố + 5 tuyến nội thành & 17 POIs`): [`evidence/inland03a_gps_4dirs_route_diagram.png`](evidence/inland03a_gps_4dirs_route_diagram.png)
  - Bảng ảnh nghiệm thu 12 góc nhìn In-Game (`01..05` cửa ngõ 4 hướng Đông/Tây/Nam/Bắc + `06..12` di chuyển nội thành & trạm `EagleRide`): [`evidence/inland03a_gps_eagleride_4dirs_verification.png`](evidence/inland03a_gps_eagleride_4dirs_verification.png)

| Mã Tuyến | Lộ Trình Kiểm Thử (`Start -> Destination`) | Khoảng Cách Đường Bộ (`road_dist_m`) | Số Node / Waypoint `EagleRide` | Điểm Đón `pickup_xyz` $\rightarrow$ Điểm Trả `dropoff_xyz` | Kết Quả Crawler In-Game |
| :--- | :--- | :---: | :---: | :--- | :---: |
| **`EXT-SOUTH`** | **Hướng Nam**: Downtown Chicago `(6200, 9200)` $\rightarrow$ Quảng Trường Miku `C3 (6335, 10605)` | `1,561.1 m` | `76` nodes / `319` wps | `(6235.6, 9202.8, 8.3)` $\rightarrow$ `(6319.9, 10588.0, 14.9)` | **PASS (`2/2 segs`)** |
| **`EXT-WEST`** | **Hướng Tây**: West Chicago Hwy `(5520, 9265)` $\rightarrow$ `WELD-2` $\rightarrow$ Trường Escuela `A1 (5965, 10215)` | `1,878.1 m` | `93` nodes / `384` wps | `(5525.0, 9248.8, 22.6)` $\rightarrow$ `(5992.6, 10200.7, 14.9)` | **PASS (`2/2 segs`)** |
| **`EXT-EAST`** | **Hướng Đông**: East Chicago Coast / Island `(7074.8, 10302.8)` $\rightarrow$ `WELD-5` $\rightarrow$ Kawaiiboutique `C2 (6525, 10350)` | `1,553.2 m` | `71` nodes / `323` wps | `(7073.2, 10302.8, 20.0)` $\rightarrow$ `(6510.7, 10368.0, 14.9)` | **PASS (`2/2 segs`)** |
| **`EXT-NORTH`** | **Hướng Bắc**: Vành Đai Bắc `(6105.8, 11180)` $\rightarrow$ Đại Lộ Sakura $\rightarrow$ Nam Chicago `(6200, 9500)` | `1,838.6 m` | `63` nodes / `371` wps | `(6105.1, 11180.0, 14.9)` $\rightarrow$ `(6229.1, 9502.4, 8.3)` | **PASS (`2/2 segs`)** |
| **`INTRA-1`** | **Nội Thành 1 (Tây $\rightarrow$ Trung Tâm)**: Sân Trượt Băng `A4` $\rightarrow$ Quán Mì Ichiraku Ramen `B3` | `712.5 m` | `14` nodes / `145` wps | `(5822.0, 10588.0, 14.9)` $\rightarrow$ `(6319.9, 10588.0, 14.9)` | **PASS (`2/2 segs`)** |
| **`INTRA-2`** | **Nội Thành 2 (Tây Nam $\rightarrow$ Đông Trung Tâm)**: Trường Escuela `A1` $\rightarrow$ Sân Khấu Miku `C3` | `714.6 m` | `14` nodes / `147` wps | `(5992.6, 10199.3, 14.9)` $\rightarrow$ `(6319.9, 10588.0, 14.9)` | **PASS (`2/2 segs`)** |
| **`INTRA-3`** | **Nội Thành 3 (Nam $\rightarrow$ Bắc)**: Sân Ống Cống Doraemon `B2` $\rightarrow$ Đại Siêu Thị Walmart & IKEA `D3` | `821.7 m` | `16` nodes / `167` wps | `(6212.5, 10199.3, 14.9)` $\rightarrow$ `(6319.9, 10915.0, 14.9)` | **PASS (`2/2 segs`)** |
| **`INTRA-4`** | **Nội Thành 4 (Tây Bắc $\rightarrow$ Đồi Biệt Thự Đông)**: Avengers HQ `D1` $\rightarrow$ Bayfront Villa `D5` | `826.9 m` | `16` nodes / `168` wps | `(5992.6, 10749.3, 14.9)` $\rightarrow$ `(6819.5, 10749.3, 14.9)` | **PASS** |
| **`INTRA-5`** | **Nội Thành 5 (Vành Đai Bắc $\rightarrow$ Đông Bắc)**: Trạm Xe Tải `D7` $\rightarrow$ Hải Đăng & Rừng Thông `D8` | `629.1 m` | `12` nodes / `128` wps | `(6265.9, 11079.3, 14.9)` $\rightarrow$ `(6895.0, 11079.3, 14.9)` | **PASS** |

---

## 4. Khả Năng Mở Rộng Tiếp Theo Với Danh Mục Tòa Nhà Mới (`urban-infill-building-catalog-2026-11-01.md`)

Thiết kế `Perimeter Streetwall` trong [`generate_perimeter_infill_plan.py`](file:///d:/GTA%20Archive/Staging/inland03a-sakura-chicago-2026-11-01/generate_perimeter_infill_plan.py) được tổ chức theo cấu trúc mô-đun từng cạnh đường (`West/East/South/North Streetwall`). Với bộ danh mục [`docs/project-eagle/urban-infill-building-catalog-2026-11-01.md`](urban-infill-building-catalog-2026-11-01.md) (`82` mẫu 3D đặc trong `Mod Donor Library` + `75` mẫu 3D đế phẳng từ `8` kho `.IMG` + `26` gói mod trên mạng), ta có thể tiếp tục đa dạng hóa từng mặt phố bất kỳ lúc nào.
