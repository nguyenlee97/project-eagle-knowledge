# Báo Cáo Triển Khai & Nghiệm Thu In-Game: Khu Đô Thị Học Viện, Đời Thường Nhật Bản & Đại Lộ Hoa Anh Đào (`INLAND-03A` Bắc Chicago)

- **Ngày thực hiện**: `01/11/2026`
- **Agent thực hiện**: `Antigravity` (`183449f8-aedb-4f83-95af-85c72771adcd`)
- **Đích tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & Backup**: `D:\GTA Archive\Staging\inland03a-sakura-chicago-2026-11-01\`
- **Bản thiết kế gốc**: [`docs/project-eagle/inland03a-north-chicago-sakura-district-blueprint-2026-11-01.md`](inland03a-north-chicago-sakura-district-blueprint-2026-11-01.md)
- **Phiếu công việc (`work-item`)**: [`docs/project-eagle/work-items/2026-11-01-antigravity-inland03a-sakura-chicago-district.md`](work-items/2026-11-01-antigravity-inland03a-sakura-chicago-district.md) (`status: done`)

---

## 1. Tổng Quan Kiến Trúc & Phạm Vi Đã Triển Khai

Khu đô thị mới **`INLAND-03A` (North Chicago Sakura & Academy District)** được xây dựng trên vùng đất trống nội địa rộng **`1.28 km × 1.23 km = 1.57 km²`** (`X = [5630 .. 6980], Y = [10028 .. 11260]`) ngay phía Bắc rìa đường 3D của Bắc Chicago (`nmile.ipl`), không cần cầu vượt biển.

### 1.1. Tọa độ, Cao độ & 5 Mối Hàn Nội Địa (`WELD-1..5`)
- **Tấm nền đô thị (`9` mảng `in03_pad_r0_c0 .. in03_pad_r2_c2`, ID `12200..12208`)**: Đặt tại cao độ mặt trên **`Z = 14.40m`** (độ dày `2.40m`, kéo xuống `Z = 12.00m`), mỗi tấm nền có kích thước cục bộ `< ±225m` tâm khối để tuân thủ giới hạn nén đỉnh `int16 / 128.0` (`±255.0m`) của `COL3`.
- **Lưới đại lộ bàn cờ `5×4` (`9` mảng `in03_rd_r0_c0 .. in03_rd_r2_c2`, ID `12209..12217`) + Đệm chuyển tiếp (`12288`, `in03_weld_ramp`)**: Mặt đường nhựa đặt tại **`Z = 14.50m`**, vỉa hè lát đá tại **`Z = 14.65m`**, dải phân cách trồng hoa anh đào giữa đại lộ chính `Sakura Central Blvd` (`X = 6319.2`) tại **`Z = 14.68m`**.
- **Khớp phẳng tuyệt đối (`ΔZ = 0.00m`) tại 5 đầu đại lộ Bắc Chicago (`nmile.ipl`)**:
  1. **`WELD-1` (`Academy West Ave`)**: `X = 5822.70, Y = 10027.94, Z = 14.50m` (`nj05_349` — đại lộ đôi 4 làn).
  2. **`WELD-2` (`Nobita & Ramen Ave`)**: `X = 6105.78, Y = 10027.94, Z = 14.50m` (`nj05_389` — đại lộ đôi 4 làn).
  3. **`WELD-3` (`Sakura Central Blvd`)**: `X = 6319.20, Y = 10027.94, Z = 14.50m` (`nj05_60` — đại lộ trung tâm 6 làn có dải phân cách cây hoa anh đào `12218` & đèn đường đôi `12219`).
  4. **`WELD-4` (`Otaku & Showroom Ave`)**: `X = 6542.49 -> 6510.00, Y = 10199.78, Z = 14.50m` (`nj05_69`).
  5. **`WELD-5` (`Lakeside Villa Dr`)**: `X = 6728.35, Y = 10479.88, Z = 14.50m` (`nj05_245`).

### 1.2. Bộ File Runtime Độc Lập & Dải Model ID (`12200 .. 12388`)
Toàn bộ tài nguyên được đóng gói vào bộ file độc lập, không chạm vào bất kỳ file nào của `WIBU-01` hay `Mondstadt`:
- `CUSTOM\inland03a_sakura_chicago.ide`: **`147` model definitions** trong dải ID độc lập **`12200 .. 12388`** (`71` Near models `12200..12288` + `76` LOD models `12300..12388`). Tất cả mặt đường, tấm nền và công trình đặc đều đặt **`IDE Flag = 0`** (không bật `DRAW_LAST (4)`).
- `CUSTOM\inland03a_sakura_chicago.ipl`: **`512` instances** (`436` Near instances có `lod_index` trỏ trực tiếp tới `76` LOD instances trong cùng file `.ipl`).
- `CUSTOM\inland03a_sakura_chicago.col` (và bản nhúng `inland03a_sakura.col` `<= 23` ký tự trong `.img`): **`89` `COL3` entries** (`1,799.7 KB`), đầy đủ va chạm vật lý cho toàn bộ mặt đường, tấm nền và công trình.
- `CUSTOM\inland03a_sakura_chicago.img`: Archive `VER2` gồm **`190` entries** (`114` `.dff` + `75` `.txd` + `1` `.col`, tổng dung lượng **`222.08 MB`**).

---

## 2. Danh Mục 20 Tổ Hợp Công Trình Mới (4 Phân Khu `A1 .. D8`)

Toàn bộ `20` tổ hợp công trình/map dưới đây được trích xuất từ `D:\GTA Archive\Mod Donor Library` (100% chưa từng sử dụng trên Đảo Wibu hay Mondstadt):

| Phân khu | Mã | Tên tổ hợp công trình | Model ID (Near / LOD) | Mesh `.dff` & Texture `.txd` chính | Tọa độ tâm `(X, Y, Z)` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Phân khu A**<br>*(Học Viện & Thể Thao Anime)* | **A1** | Trường Cấp 3 `Escuela High School` | `12221` / `12321` | `in03_school_main.dff` + `in03_school_main.txd` | `(5920.0, 10310.0, 14.50)` |
| | **A2** | Khu Lớp Học & Phòng Hiệu Trưởng | `12222..12223` / `12322..12323` | `in03_classroom.dff`, `in03_director_of.dff` | `(5860.0, 10250.0, 14.50)` |
| | **A3** | Sân Bóng Đá Học Đường & Nhà CLB Anime (`#165621`) | `12224..12229` / `12324..12329` | `in03_soccer_fld.dff`, `in03_club_house.dff`, `in03_anime_room.dff`, `in03_nagato_1..3.dff` | `(5750.0, 10540.0, 14.50)` |
| | **A4** | Sân Trượt Băng Nghệ Thuật (`Figure Skating Rink #193661`) | `12230..12234` / `12330..12334` | `in03_skate_rink.dff`, `in03_skate_park.dff`, `in03_skate_l1.dff`, `in03_skate_snow.dff`, `in03_skate_kon.dff` | `(5930.0, 10600.0, 14.50)` |
| **Phân khu B**<br>*(Phố Đời Thường Nhật Bản & Ramen)* | **B1** | Khu Phố Nhà Nobita & Doraemon (`Doraemon Town`) | `12235..12236` / `12335..12336` | `in03_nobita_ie1.dff`, `in03_nobita_ie2.dff` (`12` căn nhà dọc phố) | `(6175.0, 10280.0, 14.50)` |
| | **B2** | Sân Bãi Đất Trống Ống Cống & Đồi Sau Trường (`Kino's Journey`) | `12237..12239` / `12337..12339` | `in03_nobita_lot.dff`, `in03_kino_fuj.dff`, `in03_kino_set.dff` | `(6045.0, 10330.0, 14.50)` |
| | **B3** | Quán Mì `Ichiraku Ramen` (`Naruto #86716`) | `12240` / `12340` | `in03_ichiraku.dff` + `in03_ichiraku.txd` (`2` cơ sở) | `(6155.0, 10560.0, 14.50)` |
| | **B4** | Phố Xe Đẩy Mì Đêm & Kiosk Ven Đường | `12241..12243` / `12341..12343` | `in03_noodle_crt.dff`, `in03_chilli_crt.dff`, `in03_ramen_hut.dff` | `(6148.0, 10540.0, 14.50)` |
| **Phân khu C**<br>*(Phố Otaku & Quảng Trường 3 Sân Khấu Miku)* | **C1** | Tổ Hợp `Little Akihabara V1 & V2` | `12244..12245` / `12344..12345` | `in03_akiba_v1.dff`, `in03_akiba_v2.dff` | `(6385.0, 10310.0, 14.50)` |
| | **C2** | Phố Cửa Hiệu `OtakuShoppu & Kawaiiboutique` (`V1 & V2`) | `12246..12247` / `12346..12347` | `in03_otaku_v1.dff`, `in03_otaku_v2.dff` | `(6465.0, 10310.0, 14.50)` |
| | **C3** | Quảng Trường Sân Khấu `Hatsune Miku PDFT Puzzle Stage (#193789)` | `12220`, `12248..12257` / `12320`, `12348..12357` | `in03_miku_plaza.dff` + `10` bộ phận `in03_puz_stage .. in03_puz_strs.dff` | `(6420.0, 10580.0, 14.50)` |
| | **C4** | Sân Khấu `Romeo & Cinderella (#195825)` + `World Is Mine (#186849)` + `Miku Neon Signs (#180718)` | `12258..12264` / `12358..12364` | `in03_miku_rc.dff`, `in03_miku_wim.dff`, `in03_miku_sgn1..5.dff` | `(6590.0, 10560.0, 14.50)` |
| **Phân khu D**<br>*(Thương Mại, Showroom & Biệt Thự Ven Vịnh)* | **D1** | Trụ Sở Công Nghệ `Avengers Facility HQ (#137628)` | `12265` / `12365` | `in03_avengers_hq.dff` + `in03_avengers_hq.txd` | `(5850.0, 10880.0, 14.50)` |
| | **D2** | Quán Cà Phê `Starbucks (#159350)` (`2` cơ sở) | `12266` / `12366` | `in03_starbucks.dff` + `in03_starbucks.txd` | `(6160.0, 10810.0, 14.50)` |
| | **D3** | Đại Siêu Thị `Walmart (#48878)` & `IKEA Megastore (#8759)` | `12267..12270` / `12367..12370` | `in03_walmart.dff`, `in03_ikea_main.dff`, `in03_ikea_sign.dff`, `in03_ikea_pipe.dff` | `(6430.0, 10880.0, 14.50)` |
| | **D4** | `Car Showroom (#150767)` & `Modern Mansion (#127449)` | `12271..12272` / `12371..12372` | `in03_car_showrm.dff`, `in03_mod_mansion.dff` | `(6580.0, 10820.0, 14.50)` |
| | **D5** | Đồi Biệt Thự `Villa F 1.1 (#167239)` & `New Mansion (#193945)` | `12273..12277` / `12373..12377` | `in03_villa_f1..3.dff`, `in03_new_mansion.dff`, `in03_new_man_int.dff` | `(6820.0, 10620.0, 14.50)` |
| | **D6** | Tháp Chọc Trời `Tallest Tower (#129128)` | `12278` / `12378` | `in03_tall_tower.dff` + `in03_tall_tower.txd` | `(6240.0, 10920.0, 14.50)` |
| | **D7** | Trạm Dừng Nghỉ Cao Tốc `Truck & Bus Rest Park (#133149)` | `12279..12281` / `12379..12381` | `in03_rest_hut.dff`, `in03_rest_shed.dff`, `in03_rest_tank.dff` | `(6210.0, 11140.0, 14.50)` |
| | **D8** | Công Viên Rừng Thông (`#27339`), Khu Cắm Trại (`#52962`) & Hải Đăng Ven Vịnh (`#212020`) | `12282..12287` / `12382..12387` | `in03_pine_tree1..2.dff`, `in03_camp_tent.dff`, `in03_camp_fire1..2.dff`, `in03_lighthouse.dff` | `(6850.0, 11120.0, 14.50)` |

---

## 3. Các Phát Hiện Kỹ Thuật Quan Trọng & Xử Lý Triệt Để Crash Streaming

Trong quá trình kiểm thử in-game, chúng tôi đã phát hiện và xử lý triệt để **4 nguyên nhân gốc rễ** gây lỗi streaming/render đối với các mesh donor từ cộng đồng:

1. **Giới hạn độ dài tên file `.col` nhúng trong `VER2` `.img` (`<= 23` ký tự)**:
   - Cấu trúc thư mục `VER2` `.img` chỉ dành `24` byte (`23` ký tự ASCII + `NUL`) cho tên file. Tên `"inland03a_sakura_chicago.col"` (`28` ký tự) bị cắt thành `"inland03a_sakura_chicag"`, khiến engine không nạp được `.col` khi liên kết LOD (`_LinkLods`), dẫn tới `CEntity::GetBoundRect` (`0x00534134`) đọc `m_pColModel == NULL`.
   - **Giải pháp**: Đặt tên entry `.col` bên trong `.img` là **`"inland03a_sakura.col"`** (`20` ký tự `<= 23`).
2. **Loại bỏ `RpSkin` / `RpHAnim` (33 bones) và `2dfx` (`0x0253F2F8`) khỏi mesh công trình tĩnh**:
   - Hai mesh đồi cây `fujyou_kino.dff` (`12238`) và `setti_Kino.dff` (`12239`) thực chất được tác giả xuất dưới dạng skinned mesh 33 xương (`RpSkinPLG 0x0116` + `RpHAnimPLG 0x011E`), còn `PD_Puzzle_W1.dff` (`12253`) có chunk `0x002B` ở đầu file và `car_showroom.dff` (`12271`) thiếu chunk kết thúc `0x0003`.
   - **Giải pháp**: Viết bộ đóng gói lại `_repack_clean_static_dff()` trong [`build_inland03a_sakura_district.py`](file:///d:/GTA%20Archive/Staging/inland03a-sakura-chicago-2026-11-01/build_inland03a_sakura_district.py), tái cấu trúc toàn bộ `114` DFF thành `RpClump` tĩnh thuần khiết (`1 Frame`, `1 Geometry`, `1 Atomic`, `0 Lights`, giữ nguyên `BinMeshPLG 0x050E`, và kết thúc bằng `Extension 0x0003`).
3. **Tràn bộ đệm ngăn xếp (Stack Buffer Overflow `EIP = 0xFFFFFFFF`) trong `CVisibilityPlugins::RenderFadingAtomic` (`0x00732480`) khi `numMaterials > 136`**:
   - Phân tích mã máy tại `0x00732480` trong `gta_pe.exe` cho thấy hàm cấp phát `sub esp, 0x98` (mảng cục bộ `char savedAlphas[136]` tại `[esp+0x10 .. esp+0x98]`) nhưng chạy vòng lặp không kiểm tra cận trên: `for (esi = 0; esi < geometry->matList.numMaterials; esi++) mov [esp + esi + 0x10], cl`.
   - Khi `in03_classroom.dff` (`158` materials) và `in03_school_main.dff` (`270` materials) đi vào vùng fade-in khoảng cách, vòng lặp ghi đè `0xFF` (`alpha = 255`) lên địa chỉ trả về trên stack (`[esp+0x98]`), làm `ret` nhảy tới `EIP = 0xFFFFFFFF`.
   - **Giải pháp**: Bổ sung thuật toán gộp vật liệu trùng lặp (`MaterialList 0x08` deduplication) và ánh xạ lại chỉ số vật liệu trong `RpGeometry` + `BinMeshPLG (0x050E)` ngay trong `_repack_clean_static_dff()`. Kết quả giảm số vật liệu của `in03_classroom.dff` từ `158 -> 14` và `in03_school_main.dff` từ `270 -> 9` (số vật liệu lớn nhất toàn khu chỉ còn **`62 << 136`**).
4. **Chuẩn hóa kích thước lũy thừa của 2 (`POT`) cho `5` file `.txd` donor**:
   - Thay thế các texture có kích thước không phải lũy thừa của 2 (`500×362`, `640×429`, `300×300`, `474×355`) trong `in03_anime_room.txd`, `in03_skate_rink.txd`, `in03_otaku_v1.txd`, `in03_otaku_v2.txd`, `in03_tall_tower.txd` bằng chunk `128×128 DXT1` hợp lệ đúng chuẩn `RwTexNative` (`offset + 104`).

---

## 4. Hệ Thống GPS (`pecore_gps_graph.pegg`), Radar 2D (`radar.img`) & `EagleRide`

1. **Đấu nối đồ thị GPS (`data\pecore_gps_graph.pegg`)**:
   - Bổ sung **`53` nút giao thông mới** (`IDs 148414 .. 148466`) và **`132` cạnh hai chiều** (`252,842` edges tổng cộng), hàn trực tiếp vào `5` nút biên Bắc Chicago (`Node 56117, 56108, 56119, 55884, 56137`).
   - Toàn bộ **`17/17` POI của `INLAND-03A`** thuộc cùng thành phần liên thông chính **`Comp #0` (`142,743` nodes)** và định tuyến Dijkstra/A* liền mạch từ nhà CJ (`Grove Street`, `Node 87358`) tới từng công trình.
2. **Cập nhật Minimap 2D (`S&S\Cdimages\default\radar.img`)**:
   - Cập nhật **`9` radar tiles** (`rows 25..27, cols 59..61`, tức `radar2559.png .. radar2761.png`) thể hiện rõ lưới đại lộ `5×4`, dải hoa anh đào hồng dọc `Sakura Central Blvd`, và mặt bằng các phân khu `A, B, C, D`.
3. **Tích hợp `17` điểm đón/trả `EagleRide` & Bản đồ lớn**:
   - Cập nhật `eagle_gg_map_pois.py`, `eagle_ride_engine.py`, và `world_pois.json` với `17` địa danh mới tại `INLAND-03A`.

---

## 5. Kết Quả Nghiệm Thu Thực Tế In-Game (`gta_pe.exe`)

| Hạng mục kiểm thử | Công cụ / Phương pháp | Kết quả | Chi tiết bằng chứng |
| :--- | :--- | :--- | :--- |
| **1. Kiểm tra sức khỏe hệ thống (`Doctor`)** | `python eagle_doctor.py` | **11/11 PASS**<br>*(0 WARN, 0 FAIL)* | `529` map mounts (`0` missing), `FLA Memory = 2800 MiB`, `PEGG = 148,467 nodes / 252,842 edges`, `Write Lock = Unlocked (Clean)`. |
| **2. Kiểm tra `Route Crawler` qua 5 mối hàn Bắc Chicago (`WELD-1..5`)** | `tester.run_route_crawler()` | **5/5 PASS**<br>*(11/11 segments PASS)* | - `WELD1_ACADEMY_WEST_AVE`: **2/2 PASS** (`3113ms`)<br>- `WELD2_NOBITA_RAMEN_AVE`: **2/2 PASS** (`3010ms`)<br>- `WELD3_SAKURA_CENTRAL_BLVD`: **2/2 PASS** (`3130ms`)<br>- `WELD4_OTAKU_SHOWROOM_AVE`: **3/3 PASS** (`4635ms`)<br>- `WELD5_LAKESIDE_VILLA_DR`: **2/2 PASS** (`3196ms`)<br>Không có khe hở `.COL`, không sụt gầm, không vướng tường vô hình (`ΔZ = 0.00m` tại `Z = 14.50m`). |
| **3. Kiểm tra 6 bước nhân vật chính Aether (`Aether Rig & Action Test`)** | `tester.run_aether_action_test()` tại `(6325.2, 10350.0, 14.50)` | **6/6 PASS**<br>*(3723ms)* | `01_CLUMP_AND_MODEL_RAM` (`PASS`), `02_WALK_IMPULSE` (`PASS`), `03_SPRINT_IMPULSE` (`PASS`), `04_JUMP_AND_LAND_COL` (`PASS`), `05_WEAPON_GRANT_AND_AIM` (`PASS`), `06_VEHICLE_SPAWN_PROXIMITY` (`PASS`). |
| **4. Kiểm toán RAM trực tiếp (`Live Scene RAM Audit`) & Chụp ảnh 12 góc nhìn ngang tầm mắt** | `tester.audit_live_scene_ram()` + `capture_game_window_png()` | **12/12 PASS**<br>*(0 Anomalies)* | Kiểm tra trực tiếp `CModelInfo` + `RpClump` + `CColModel` trong RAM tại `12` tọa độ trải khắp Phân khu `A, B, C, D`: **`0` lỗi model/texture/collision**, hiển thị rõ Minimap 2D và vạch dẫn đường GPS PECore. |
| **5. Quy tắc đóng game bắt buộc** | `Get-Process gta_pe` | **PASS** | `gta_pe.exe running = False` ngay sau khi hoàn tất chụp hình nghiệm thu. |

### Bộ Ảnh Nghiệm Thu In-Game (`Contact Sheet 12 Góc Nhìn`)
- File ảnh chất lượng cao tại kho tài liệu dự án: [`docs/project-eagle/evidence/inland03a_ingame_verification_contact_sheet.png`](evidence/inland03a_ingame_verification_contact_sheet.png)
- Báo cáo JSON chi tiết từng bước: [`D:\GTA Archive\Staging\inland03a-sakura-chicago-2026-11-01\inland03a_ingame_verification_report.json`](file:///d:/GTA%20Archive/Staging/inland03a-sakura-chicago-2026-11-01/inland03a_ingame_verification_report.json)

---

## 6. Hướng Dẫn Phục Hồi (Rollback) Khi Cần

Toàn bộ bản sao lưu nguyên trạng trước khi tích hợp được lưu tại `D:\GTA Archive\Staging\inland03a-sakura-chicago-2026-11-01\backups\`:
- `gta.dat.bak`
- `pecore_gps_graph.pegg.bak`
- `radar.img.bak`
- `eagle_gg_map_pois.py.bak`, `eagle_ride_engine.py.bak`, `world_pois.json.bak`
Để hoàn tác, chỉ cần chép đè các file `.bak` về vị trí tương ứng trong `gta sa gameplay-lab` và xóa `CUSTOM\inland03a_sakura_chicago.{ide,ipl,col,img}`.

---

## 7. Tài Liệu Bổ Sung: Danh Mục Tòa Nhà 3D Chuẩn Infill Mặt Tiền Đường (`Urban Building Infill Catalog`)

Để lấp kín toàn bộ mặt tiền vỉa hè (`streetwall infill`) cho các ô phố `220m × 270m` của `INLAND-03A` (cao độ `Z = 14.50m`) bằng các tòa nhà 3D đặc 4 mặt (thay thế hoàn toàn các tấm backdrop 2D rỗng như `PD_PuzzleP1..P5.dff`), sử dụng bộ tài liệu và dataset đã kiểm định hình học nhị phân:
- **Báo cáo Catalog đầy đủ (3 Phần A, B, C + Công thức `Z_IPL = 14.50 - min_z` + 4 Phương án ghép kín ô phố `220m × 270m`)**: [`docs/project-eagle/urban-infill-building-catalog-2026-11-01.md`](urban-infill-building-catalog-2026-11-01.md)
- **Dataset JSON cấu trúc cho script sinh `.ipl` (`82` mẫu Donor 3D + `16` mẫu cảnh báo 2D bị loại + `75` mẫu `.IMG` đế phẳng)**: [`docs/project-eagle/evidence/urban-infill-building-catalog-2026-11-01.json`](evidence/urban-infill-building-catalog-2026-11-01.json)
- **Bảng ảnh 3D Isometric Phần A (`Mod Donor Library`)**: [`docs/project-eagle/evidence/urban_infill_building_catalog_part_a.png`](evidence/urban_infill_building_catalog_part_a.png)
- **Bảng ảnh 3D Isometric Phần B (`8` kho `.IMG` của `gameplay-lab`)**: [`docs/project-eagle/evidence/urban_infill_building_catalog_part_b.png`](evidence/urban_infill_building_catalog_part_b.png)
