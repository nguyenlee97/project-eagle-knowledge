# Bàn giao Kỹ thuật: Bộ 5 Phương Tiện Đặt Xe Công Nghệ 3D (`30669..30673`) & 5 Tài Xế Aether Mặc Đồng Phục Hãng Xe (`49423..49427`) cho EagleRide (App #12)

- **Ngày thực hiện**: 31/10/2026
- **Agent thực hiện**: Antigravity (`f1234b7b-c8eb-4722-bc98-7c8e75d7686a`)
- **Đích tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Phiếu công việc**: [`work-items/2026-10-31-antigravity-eagleride-branded-models-and-aether-drivers.md`](work-items/2026-10-31-antigravity-eagleride-branded-models-and-aether-drivers.md)
- **Staging & Bộ công cụ Build**: `D:\GTA Archive\Staging\eagleride-branded-models-and-aether-drivers\`

---

## 1. Tổng quan Kiến trúc & Dải ID Cấp phát

Để đảm bảo không ghi đè lên các phương tiện giao thông mặc định của GTA SA (`420`, `438`, `522`...) hay các NPC hiện có trong thành phố và Mondstadt (`2900..2909`, `49412..49422`), toàn bộ 5 phương tiện và 5 tài xế của ứng dụng **EagleRide (App #12 trên EaglePhone)** được cấp phát dải ID mở rộng riêng biệt qua Fastman92 Limit Adjuster và đóng gói vào `CUSTOM\custom_mods.img`:

| Dịch vụ (`service_id`) | Tên hiển thị | Vehicle ID | Model Xe (`.dff`/`.txd` — Base) | Driver Ped ID | Model Tài xế (`.dff`/`.txd`) | Ghế Hành khách (`seat_id`) | Biển số & Nhận diện Chuẩn Hàng Thật (Ảnh 1–5) |
| :--- | :--- | :---: | :--- | :---: | :--- | :---: | :--- |
| `UBER_CAR` | **Uber Car (4-Cho)** | `30669` | `uber_car` (`schafterle.dff` — Mercedes Sedan) | `49423` | `aether_uber` | `2` (Ghế sau phải) | `30K - 888.88` • Sedan VIP Đen Obsidian, đèn nóc `Uber`, chữ `Uber` bạc trên cửa trước; Aether mặc Vest đen VIP, sơ mi trắng, cà vạt đen |
| `XANH_CAR` | **Xanh SM Car (4-Cho)** | `30670` | `xanh_car` (`rebla.dff` — Crossover SUV 5 cửa) | `49424` | `aether_xanhcar` | `2` (Ghế sau phải) | `29E - 042.44` (Biển vàng 2 dòng) • Chuẩn Ảnh 4: SUV Điện Xanh Cyan `#00C2D1`, dải đèn V-Wing trước, logo cánh chim + `XANH SM / TAXI` in trực tiếp trên cửa trước, ốp gầm đen viền bạc; Aether mặc Áo Polo Cyan ngắn tay nẹp cổ Cam + quần âu đen |
| `GRAB_BIKE` | **GrabBike (2-Banh)** | `30671` | `grab_bike` (`lcs_faggio2.dff` — Xe tay ga sàn phẳng) | `49425` | `aether_grab` | `0` (Yên sau xe ga, dáng ngồi thẳng `bikev`) | `29-G1 888.88` • Chuẩn Ảnh 2: Xe tay ga Xanh Grab `#00B14F` + sàn/yên đen; Aether mặc áo khoác Grab Xanh Lá có nẹp khóa & hông Xám Bạc phản quang, logo `Grab` trắng ngực trái & lưng + nón 1/2 đầu `Grab` |
| `XANH_BIKE` | **Xanh SM Bike (2-Banh)** | `30672` | `xanh_bike` (`lcs_faggio2.dff` — Xe máy điện VinFast Feliz S) | `49426` | `aether_xanhbike` | `0` (Yên sau xe ga, dáng ngồi thẳng `bikev`) | `29-MD1 686.88` • Chuẩn Ảnh 1 & 5: Xe máy điện Cyan `#00C2D1` + sàn/yên đen; Aether mặc áo khoác Cyan cổ Vàng cao viền đen, ống tay in dọc `XANH SM`, lưng sọc chữ V xám đen viền vàng + `XANH SM / xin chào!` + nón 1/2 đầu Cyan |
| `BE_BIKE` | **BeBike (2-Banh)** | `30673` | `be_bike` (`lcs_faggio2.dff` — Xe tay ga sàn phẳng) | `49427` | `aether_be` | `0` (Yên sau xe ga, dáng ngồi thẳng `bikev`) | `29-B1 999.99` • Chuẩn Ảnh 3: Xe tay ga Vàng Nghệ `#FFD000` phối Xanh Navy `#0F1D56`; Aether mặc áo khoác Vàng nghệ cổ Xanh Navy, các dải sọc ngang Xanh Navy/Vàng quanh thân, sọc Trắng/Navy dọc ống tay, lưng in biểu tượng `b` + `"be đến nơi, về đến chốn"` + nón 1/2 đầu `be` |

---

## 2. Chi tiết Kỹ thuật Xây dựng Model 3D & Texture (v2 — Chuẩn 5 Ảnh Thực Tế)

### 2.1. Tối ưu hóa `AETHER.dff` / `AETHER.txd` & Xây dựng 5 Tài xế Aether (`build_aether_drivers.py`)
- **Tối ưu hóa model gốc `AETHER.dff` & `AETHER.txd`**:
  - Giữ nguyên 100% khuôn mặt, mái tóc vàng, bím tóc dài sau lưng và toàn bộ trọng số xương (`PLG_SKIN` `0x0116` trên hệ xương chuẩn `Biped`).
  - Gộp từ 18 material xuống 3 material chuẩn (`910,679` B, `12,491` đỉnh, `17,706` tam giác) và nén chuẩn bộ `AETHER.txd` xuống **`786,856` B** (`DXT1`).
- **Tái cấu trúc hình thể & 5 bộ đồng phục tài xế Aether (`49423..49427`) theo 5 ảnh thực tế**:
  - Loại bỏ các phụ kiện giáp cổ trang tách rời trên bản đồng phục tài xế (túi da hông, giáp đầu gối vàng, cầu vai lớn, vây gai khuỷu tay/cổ tay), nắn phẳng vùng eo hở bụng thành phom áo khoác/áo Polo nam thẳng lịch sự, thu gọn quần phồng thành quần âu/quần dài ống đứng hiện đại và chuyển bàn tay về màu da tự nhiên.
  - Tham số hóa UV ống tay `(s_arm, t_arm)` dọc theo trục xương cánh tay thực tế (`slope = 0.970`) giúp dòng chữ `XANH SM` trên cẳng tay (`aether_xanhbike`), sọc Trắng/Navy dọc tay áo (`aether_be`) và mảng Xám Bạc dưới cánh tay (`aether_grab`) chạy thẳng tắp, không bị xoắn chéo; riêng `aether_xanhcar` mặc áo Polo ngắn tay lộ cẳng tay trần chuẩn Ảnh 4.
  - Đối với 3 tài xế xe máy (`49425` `aether_grab`, `49426` `aether_xanhbike`, `49427` `aether_be`), trang bị **nón bảo hiểm 1/2 đầu (`generate_half_helmet_mesh`)** gọn gàng ôm sát đầu (`bone_index = 5`), có lưỡi trai đen phía trước và quai đeo cằm màu đen chuẩn Ảnh 5.

### 2.2. Xây dựng 5 Phương tiện Đặt xe Công nghệ (`build_branded_vehicles.py`)
- **Đổi sang đúng dòng xe thực tế từ kho `vehicles.img` của Project Eagle**:
  - `uber_car` (`30669`): dùng base **`schafterle.dff`** (Sedan hạng sang Mercedes S/E-Class có cửa sổ trời) với handling `SCHALE`.
  - `xanh_car` (`30670`): dùng base **`rebla.dff`** (Crossover SUV 5 cửa hiện đại giống hệt phom VinFast VF e34 / VF 5 trong Ảnh 4) với handling `REBLA`.
  - `grab_bike` (`30671`), `xanh_bike` (`30672`), `be_bike` (`30673`): dùng base **`lcs_faggio2.dff`** (Xe máy điện / xe tay ga sàn phẳng có cụm đèn pha trên ghi-đông, yên đôi đen rộng rãi, mâm đúc đen phanh đĩa bạc giống hệt VinFast Feliz S trong Ảnh 5) với handling `MOPED` và nhóm animation **`bikev`** (giúp tài xế và hành khách ngồi thẳng lưng tự nhiên).
- **Ánh xạ Livery Trực tiếp lên Lưới Tam giác Cửa xe & Yếm xe (Zero Floating Box)**:
  - Thay vì gắn bảng hộp chữ nhật tối màu nổi bên ngoài, `build_branded_vehicles.py` ánh xạ trực tiếp các tam giác vỏ ngoài của `door_lf_ok` / `door_rf_ok` (trên `schafterle.dff` và `rebla.dff`) và mặt nạ trước / ốp hông sau của `chassis_hi` (trên `lcs_faggio2.dff`) vào `eagleride_livery` có nền trùng khớp 100% với màu sơn thân xe (`#00C2D1`, `#00B14F`, `#FFD000`, `#14171E`), đồng thời thay thế trực tiếp chất liệu `'carplate'` bằng `'eagleride_plate'` (biển vàng 2 dòng `29E / 042.44` cho `xanh_car`, `30K-888.88` cho `uber_car`, `29-G1 888.88`, `29-MD1 686.88`, `29-B1 999.99` cho 3 xe ga).
- **Ảnh Chụp Studio & So sánh Trực tiếp**:
  - Bảng 5 tài xế Aether (Mặt trước & Mặt sau): `D:\GTA Archive\Staging\eagleride-branded-models-and-aether-drivers\previews\aether_drivers_5x_front_back.png`
  - Bảng 5 phương tiện (Góc 3/4 Trước-Trái & Góc Ngang): `D:\GTA Archive\Staging\eagleride-branded-models-and-aether-drivers\previews\branded_vehicles_5x_preview.png`
  - Bảng đối chiếu trực tiếp 5 ảnh thật của User vs. 5 Skin & 5 Xe 3D: `D:\GTA Archive\Staging\eagleride-branded-models-and-aether-drivers\previews\real_vs_3d_comparison.png`

---

## 3. Kết quả Kiểm toán & Nghiệm thu Trực tiếp Trong Game (`8/8 PASS`)

1. **Kiểm toán Cấu trúc Nhị phân (`audit_models.py`)**:
   - Toàn bộ `22/22` file `.dff` và `.txd` đạt `100% PASS` (RenderWare `0x1803FFFF`, hợp lệ `Clump`, `FrameList`, `GeometryList`, `Atomic`, `MaterialList`, `PLG_SKIN`, `TextureNative`).
2. **Kiểm thử Mô phỏng 10,000 Chuyến đi (`--test-uber --trips 10000`)**:
   - Đạt **`10,000 / 10,000 PASS (100.0%)`**, `0` lỗi định tuyến hay trạng thái.
3. **Nghiệm thu Trực tiếp Trong Game (`python eagle_doctor.py --test-uber-live` trên `gta_pe.exe`)**:
   - Báo cáo JSON: [`crash-reports/eagleride-live-ingame-latest.json`](crash-reports/eagleride-live-ingame-latest.json)
   - Tổng kết: **`EagleRide Live In-Game Test: 8/8 Steps PASS (38008ms)`** (`0` crash):
     - `01_CLEO_BRIDGE_SHM`: Kết nối Shared Memory `0x433C4F20` với `cleo/EagleRideBridge.cs` (`PASS`).
     - `02_OPEN_APP12_HUD`: Mở App #12 `EagleRide` trên EaglePhone (`uber_live_01_app12_hud.png` — `PASS`).
     - `03_FOG_OF_WAR_LOCK_AND_GPS_PIN`: Chặn đặt xe tới POI chưa khám phá (`wb_wibu01_tokyo_tower`) và tự động ghim lộ trình GPS màu đỏ (`PASS`).
     - `04_UBER_CAR_LIVE_ACCEPTANCE`: Spawn `veh_model = 30669` (`veh_rw_obj = 0x5C7180D8`, `txd_slot = 1945`) + tài xế `ped_model = 49423` (`drv_rw_obj = 0x5C718118`, `txd_slot = 3625`), khách ngồi ghế sau (`seat_id = 2`), đổi đài `CSR 103.9`, xe tự lái `7.73m`, Tua nhanh (`Fast-Forward`) tới đích, trừ `$48` (`PASS`).
     - `05_XANH_CAR_LIVE_ACCEPTANCE`: Spawn `veh_model = 30670` (`veh_rw_obj = 0x659EE180`, `txd_slot = 1946`) + tài xế `ped_model = 49424` (`drv_rw_obj = 0x659EE1C0`, `txd_slot = 3626`), khách ngồi ghế sau (`seat_id = 2`), đổi đài `K-Jah West`, xe tự lái `32.50m`, Tua nhanh tới đích, trừ `$50` (`PASS`).
     - `06_GRAB_BIKE_LIVE_ACCEPTANCE`: Spawn `veh_model = 30671` (`veh_rw_obj = 0x659EE940`, `txd_slot = 1947`) + tài xế `ped_model = 49425` (`drv_rw_obj = 0x659EE980`, `txd_slot = 3627`), khách ngồi yên sau (`seat_id = 0`), đổi đài `Master Sounds 98.3`, xe tự lái `9.60m`, Tua nhanh tới đích, trừ `$102` (`PASS`).
     - `07_XANH_BIKE_LIVE_ACCEPTANCE`: Spawn `veh_model = 30672` (`veh_rw_obj = 0x659EE9C0`, `txd_slot = 1948`) + tài xế `ped_model = 49426` (`drv_rw_obj = 0x659EEA00`, `txd_slot = 3628`), khách ngồi yên sau (`seat_id = 0`), đổi đài `WCTR Talk Radio`, xe tự lái `9.92m`, Tua nhanh tới đích, trừ `$35` (`PASS`).
     - `08_BE_BIKE_LIVE_ACCEPTANCE`: Spawn `veh_model = 30673` (`veh_rw_obj = 0x659EEE40`, `txd_slot = 1949`) + tài xế `ped_model = 49427` (`drv_rw_obj = 0x659EEE80`, `txd_slot = 3629`), khách ngồi yên sau (`seat_id = 0`), đổi đài `User Track Player (Custom)`, xe tự lái `9.63m`, Tua nhanh tới đích, trừ `$30` (`PASS`).

### Bộ 16 Ảnh Nghiệm thu Thực tế Trong Game (`12:00` Trưa — Pershing Square)
- Giao diện App #12 EagleRide: [`uber_live_01_app12_hud.png`](crash-reports/bug-snapshots/uber_live_01_app12_hud.png)
- **Uber Car (`30669` + `49423`)**:
  - [`uber_live_04a_uber_car_hud.png`](crash-reports/bug-snapshots/uber_live_04a_uber_car_hud.png)
  - [`uber_live_04b_uber_car_3rdperson.png`](crash-reports/bug-snapshots/uber_live_04b_uber_car_3rdperson.png)
  - [`uber_live_04c_uber_car_driver_and_passenger.png`](crash-reports/bug-snapshots/uber_live_04c_uber_car_driver_and_passenger.png)
- **Xanh SM Car (`30670` + `49424`)**:
  - [`uber_live_05a_xanh_car_hud.png`](crash-reports/bug-snapshots/uber_live_05a_xanh_car_hud.png)
  - [`uber_live_05b_xanh_car_3rdperson.png`](crash-reports/bug-snapshots/uber_live_05b_xanh_car_3rdperson.png)
  - [`uber_live_05c_xanh_car_driver_and_passenger.png`](crash-reports/bug-snapshots/uber_live_05c_xanh_car_driver_and_passenger.png)
- **GrabBike (`30671` + `49425`)**:
  - [`uber_live_06a_grab_bike_hud.png`](crash-reports/bug-snapshots/uber_live_06a_grab_bike_hud.png)
  - [`uber_live_06b_grab_bike_3rdperson.png`](crash-reports/bug-snapshots/uber_live_06b_grab_bike_3rdperson.png)
  - [`uber_live_06c_grab_bike_driver_and_passenger.png`](crash-reports/bug-snapshots/uber_live_06c_grab_bike_driver_and_passenger.png)
- **Xanh SM Bike (`30672` + `49426`)**:
  - [`uber_live_07a_xanh_bike_hud.png`](crash-reports/bug-snapshots/uber_live_07a_xanh_bike_hud.png)
  - [`uber_live_07b_xanh_bike_3rdperson.png`](crash-reports/bug-snapshots/uber_live_07b_xanh_bike_3rdperson.png)
  - [`uber_live_07c_xanh_bike_driver_and_passenger.png`](crash-reports/bug-snapshots/uber_live_07c_xanh_bike_driver_and_passenger.png)
- **BeBike (`30673` + `49427`)**:
  - [`uber_live_08a_be_bike_hud.png`](crash-reports/bug-snapshots/uber_live_08a_be_bike_hud.png)
  - [`uber_live_08b_be_bike_3rdperson.png`](crash-reports/bug-snapshots/uber_live_08b_be_bike_3rdperson.png)
  - [`uber_live_08c_be_bike_driver_and_passenger.png`](crash-reports/bug-snapshots/uber_live_08c_be_bike_driver_and_passenger.png)

### 3.2. Nghiệm thu Lái Tự Động Thực Tế `15/15` Tuyến Đường (`5 Batches`) & Bộ 5 Lớp Chống Đâm Xe / Cân Bằng Xe Máy
- **Báo cáo JSON chi tiết**: [`eagleride-batch-driving-latest.json`](crash-reports/eagleride-batch-driving-latest.json) — **`15/15 ROUTES PASS`** (`BATCH_1_LOS_SANTOS: 3/3`, `BATCH_2_SF_LV_LSIA: 3/3`, `BATCH_3_WIBU01_ISLAND: 3/3`, `BATCH_4_MONDSTADT: 3/3`, `BATCH_5_MULTIVERSE_BRIDGES: 3/3`).
- **5 Lớp Chống Đâm Xe & Chống Ngã Xe Máy (`eagle_ride_engine.py`, `EagleCompanion.py`, `cleo/EagleRideBridge.cs`)**:
  1. **Chaikin Corner Beveling & Chia mịn Waypoint `8.0m`**: Bo tròn mọi góc cua `> 20°` và chia nhỏ waypoint mỗi `8.0m` kèm lực kéo tâm đường (`center_pull`), triệt tiêu hiện tượng cắt góc lên vỉa hè.
  2. **Adaptive Corner Speed Braking**: Quét trước `32m` đường phía trước, tự động hãm tốc xuống `10.5 m/s` (`~38 km/h`) ở cua gắt `>= 52°` và `13.5 m/s` (`~48 km/h`) ở cua vừa `30°–52°`.
  3. **Live `CPool<CVehicle>` Radar & Dual `0395: CLEAR_AREA` Bubbles**: Quét trực tiếp `CPools::ms_pVehiclePool` (`0x00B74494`) để lách làn (`±2.2m`), giảm tốc và dọn sạch xe NPC chắn ngang trước mũi xe (`8.5m` & `16.0m`).
  4. **Heavy Cruiser Armor (`8.500 kg`) & Bike Gyro Roll/Pitch Stabilizer**: Bật `01EC: SET_CAR_HEAVY`, khóa `m_fMass = 8500.0`, `m_fTurnMass = 12000.0`, `bCantBeKnockedOffBike = 1` (`0x08000000` tại `CPed + 0x474`) cho cả tài xế và khách; kẹp góc ngóc đầu xe máy `nfz` trong `[-0.12, +0.12]`, `nrz = 0.0` và triệt tiêu vận tốc góc (`avx = avy = avz = 0`).
  5. **Tần số điều khiển lái `30 Hz` (`32ms`)**: Rút ngắn chu kỳ `ride_mgr.tick` trong `EagleCompanion.py` xuống `32ms`.
- **Kết quả kiểm thử thực tế sau nâng cấp**:
  - `B1_R1_GROVE_TO_IDLEWOOD` (`Uber Car`, `559.5m`): `84/85` wps (`98.8%`), **`recov = 0`** ([`batch1_r1_ls_uber_car.png`](crash-reports/bug-snapshots/batch1_r1_ls_uber_car.png))
  - `B1_R2_IDLEWOOD_TO_UNITY` (`GrabBike`, `478.4m`): `60/61` wps (`98.4%`), **`recov = 0`** ([`batch1_r2_ls_grabbike.png`](crash-reports/bug-snapshots/batch1_r2_ls_grabbike.png))
  - `B1_R3_PERSHING_TO_VERONA` (`Xanh SM Car`, `936.8m`): `63/64` wps (`98.4%`) ([`batch1_r3_ls_xanh_car.png`](crash-reports/bug-snapshots/batch1_r3_ls_xanh_car.png))
  - `B2_R1_LSIA_TO_SANTA_MARIA` (`Xanh SM Bike`, `2070.8m`): `135/136` wps (`99.3%`) ([`batch2_r1_lsia_xanh_bike.png`](crash-reports/bug-snapshots/batch2_r1_lsia_xanh_bike.png))
  - `B2_R2_SF_DOHERTY_TO_CHINATOWN` (`Uber Car`, `517.8m`): `34/35` wps (`97.1%`) ([`batch2_r2_sf_uber_car.png`](crash-reports/bug-snapshots/batch2_r2_sf_uber_car.png))
  - `B2_R3_LV_STRIP_CASINOS` (`BeBike`, `794.7m`): `112/113` wps (`99.1%`), **`recov = 0`** ([`batch2_r3_lv_bebike.png`](crash-reports/bug-snapshots/batch2_r3_lv_bebike.png))
  - `B3_R1_SETO_BRIDGE_TO_AKIHABARA` (`Xanh SM Car`, `935.0m`): `39/40` wps (`97.5%`) ([`batch3_r1_wibu01_seto_xanh_car.png`](crash-reports/bug-snapshots/batch3_r1_wibu01_seto_xanh_car.png))
  - `B3_R2_AKIHABARA_TO_KERORIN` (`GrabBike`, `222.0m`): `11/12` wps (`91.7%`), **`recov = 0`** ([`batch3_r2_wibu01_akiba_grabbike.png`](crash-reports/bug-snapshots/batch3_r2_wibu01_akiba_grabbike.png))
  - `B3_R3_KERORIN_TO_ZERO_PLAZA` (`Xanh SM Bike`, `238.8m`): `29/30` wps (`96.7%`), **`recov = 0`** ([`batch3_r3_wibu01_zero_xanh_bike.png`](crash-reports/bug-snapshots/batch3_r3_wibu01_zero_xanh_bike.png))
  - `B4_R1_WHETSTONE_TO_FALCON_VIADUCT` (`Xanh SM Car`, `891.8m`): `48/49` wps (`98.0%`) ([`batch4_r1_mondstadt_viaduct_xanh_car.png`](crash-reports/bug-snapshots/batch4_r1_mondstadt_viaduct_xanh_car.png))
  - `B4_R2_M0_BRIDGE_TO_M1_SHOWROOM` (`BeBike`, `249.1m`): `18/19` wps (`94.7%`) ([`batch4_r2_mondstadt_m0_m1_bebike.png`](crash-reports/bug-snapshots/batch4_r2_mondstadt_m0_m1_bebike.png))
  - `B4_R3_SPRINGVALE_TO_DAWN_WINERY` (`Uber Car`, `1046.3m`): `72/73` wps (`98.6%`) ([`batch4_r3_mondstadt_winery_uber_car.png`](crash-reports/bug-snapshots/batch4_r3_mondstadt_winery_uber_car.png))
  - `B5_R1_VICE_CITY_MALIBU_TO_STARFISH` (`Xanh SM Car`, `1240.8m`): `83/84` wps (`98.8%`) ([`batch5_r1_vice_city_xanh_car.png`](crash-reports/bug-snapshots/batch5_r1_vice_city_xanh_car.png))
  - `B5_R2_LIBERTY_STAUNTON_TO_SAFEHOUSE` (`Uber Car`, `786.3m`): `57/59` wps (`96.6%`) ([`batch5_r2_liberty_city_uber_car.png`](crash-reports/bug-snapshots/batch5_r2_liberty_city_uber_car.png))
  - `B5_R3_BRIDGE_BR4_TO_PERA_LOCA` (`GrabBike`, `1421.9m`): `186/187` wps (`99.5%`), không còn bốc đầu/bay khỏi mặt cầu ([`batch5_r3_bridge4_peraloca_grabbike.png`](crash-reports/bug-snapshots/batch5_r3_bridge4_peraloca_grabbike.png))

---

## 4. Phục hồi (Rollback) & Khóa ghi

- Bản sao lưu nguyên trạng trước khi triển khai nằm tại: `D:\GTA Archive\Staging\eagleride-branded-models-and-aether-drivers\backup\`
- Để phục hồi riêng phạm vi EagleRide Models (khi game đã đóng):
  ```powershell
  python "D:\GTA Archive\Staging\eagleride-branded-models-and-aether-drivers\src\rollback_eagleride_models.py"
  ```
- Khóa ghi `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\coordination\game-write.lock` đã được nhả hoàn toàn.
