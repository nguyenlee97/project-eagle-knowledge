# Bàn giao: Cập nhật GG Map (`715` POIs) & Ứng dụng Đặt Xe Công Nghệ EagleRide (Uber / Xanh SM / Grab / Be)

- **Ngày**: 2026-10-31
- **Agent thực hiện**: Antigravity (`ac8ced36-7cb3-4d1a-8a29-ea37793adcec`)
- **Đích tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Trạng thái `game-write.lock`**: Đã giải phóng (`Unlocked (Clean)`)
- **Trạng thái `eagle_doctor.py --doctor`**: `11/11 PASS, 0 WARN, 0 FAIL`

---

## 1. Tổng hợp Cập nhật GG Map (`715` POIs trong `eagle_gg_map_pois.py`)

- **Quần đảo Nhật Bản `WIBU-01` (Mokuloa Island)**:
  - Đồng bộ lại tọa độ sau quy hoạch đô thị 25/10 cho `wb_wibu01_tokyo_tower`, `wb_wibu01_castle_kawaii`, `wb_wibu01_kerorin_capital`.
  - Bổ sung 8 địa điểm mới: Trạm Thu Phí Nam (`wb_wibu01_toll_south`), Nhà Ga Ishimaru (`wb_wibu01_ishimaru_station`), Kawaii Boutique (`wb_wibu01_kawaiiboutique`), Đại Lộ Hoa Anh Đào (`wb_wibu01_sakura_blvd`), Khu Phố Nam Kerorin (`wb_wibu01_kerorin_south`), Cổng Đông Khu Zero (`wb_wibu01_zero_east_gate`), Quảng Trường Trung Tâm Zero (`wb_wibu01_zero_plaza`), Cảng Tây Zero (`wb_wibu01_zero_west_harbor`).
- **Lục địa Mondstadt `M0 + M1 + M2` (`64` POIs)**:
  - Chuẩn hóa tên hiển thị không dấu ASCII + tên tiếng Anh (`_POI_EN_BY_ID`) và phân loại đúng vào các Tab chức năng (`FOOD_CLUB`, `SHOPS_STYLE`, `GUN_GARAGE`, `ACTIVITIES`, `SAFEHOUSE_INT`, `LANDMARKS`, `WIBU_WORLD`) cho toàn bộ `64` địa điểm (`wb_mondstadt_cathedral` + `mondstadt_poi_01..63`).
- **Hệ thống Cầu Cao Tốc Liên Đảo & Quần đảo Dublin (`WIBU-04`)**:
  - Đầy đủ 6 cây cầu vượt biển (`wb_wibu01_seto_bridge`, `lm_bridge_br1_carcer_windy`, `lm_bridge_br2_carcer_bullworth`, `lm_bridge_br3a_bullworth_dublin`, `lm_bridge_br3b_liberty_dublin`, `lm_bridge_br4_ls_peraloca`) và Quần đảo Dublin (`lm_dublin_island`).

---

## 2. Ứng dụng #12 trên EaglePhone — `EagleRide (Uber / Xanh SM / Grab / Be)`

### 2.1. 5 Dịch vụ Đặt Xe Thương Hiệu & Tài Xế Aether Mặc Đồng Phục
Tích hợp trực tiếp với bộ 5 phương tiện custom (`30669..30673`) và 5 skin tài xế Aether (`49423..49427`) từ bàn giao [handover-eagle-ride-driver-skins-and-vehicles-2026-10-31.md](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/handover-eagle-ride-driver-skins-and-vehicles-2026-10-31.md):

| Phím | Dịch vụ | Model Xe (`veh_model`) | Tài xế Aether (`ped_model`) | Ghế ngồi (`seat_id`) | Giá cước |
| :---: | :--- | :--- | :--- | :---: | :--- |
| `1` | **Uber Car** | `#30669` (`uber_car` — Mercedes E-Class Sedan Đen Bóng) | `#49423` (`aether_uber` — Vest Đen + Sơ Mi Trắng) | `2` (Ghế sau phải) | `$25 + $35/km` |
| `2` | **Xanh SM Car** | `#30670` (`xanh_car` — VinFast VF e34 Crossover SUV Cyan) | `#49424` (`aether_xanhcar` — Áo Polo Cyan Ngắn Tay) | `2` (Ghế sau phải) | `$18 + $28/km` |
| `3` | **GrabBike** | `#30671` (`grab_bike` — Xe Tay Ga Xanh Lá Grab) | `#49425` (`aether_grab` — Áo Khoác + Mũ 3/4 Grab) | `0` (Yên sau xe máy) | `$10 + $14/km` |
| `4` | **Xanh SM Bike** | `#30672` (`xanh_bike` — VinFast Feliz S Cyan) | `#49426` (`aether_xanhbike` — Áo Khoác + Mũ 3/4 Xanh SM) | `0` (Yên sau xe máy) | `$12 + $16/km` |
| `5` | **BeBike** | `#30673` (`be_bike` — Xe Tay Ga Vàng Nghệ Be) | `#49427` (`aether_be` — Áo Khoác + Mũ 3/4 Be) | `0` (Yên sau xe máy) | `$8 + $12/km` |

### 2.2. Cơ chế Khám phá Địa điểm (`Fog-of-War` `85m`)
- Khởi đầu mở sẵn `10` điểm cơ bản (`DEFAULT_UNLOCKED_POIS`).
- Khi người chơi tự di chuyển trong bán kính `<= 85m` quanh bất kỳ POI nào trong `715` POIs, hệ thống tự động mở khóa địa điểm đó và lưu vào `data/eagleride_visited_pois.json`.
- Khi chọn một địa điểm chưa mở khóa (`[LOCKED]`) và nhấn `F9`, EagleRide chặn đặt xe và tự động ghim mốc đỏ chỉ đường GPS (`T`) để người chơi tự lái tới khám phá lần đầu.

### 2.3. Điều khiển Trong Chuyến Đi
- **Đổi đài Radio**: Nhấn phím `O` (hoặc `U`) ngay khi đang ngồi trên xe để chuyển qua 13 đài Radio (bao gồm các đài Genshin Custom Radio).
- **Tua Nhanh Tới Nơi (`Fast-Forward`)**: Nhấn `F9` hoặc `F10` để bỏ qua quãng đường còn lại và tới ngay điểm đích.

---

## 3. Kết quả Kiểm thử Thực tế Trong Game (`8/8 Steps PASS`)

- Báo cáo JSON: [eagleride-live-ingame-latest.json](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/eagleride-live-ingame-latest.json)
- Bộ ảnh chụp trực tiếp trong `gta_pe.exe` (`1920x1080`):
  - **Uber Car (`#30669` + `#49423`)**: [uber_live_04b_uber_car_3rdperson.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_04b_uber_car_3rdperson.png) | [uber_live_04c_uber_car_driver_and_passenger.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_04c_uber_car_driver_and_passenger.png)
  - **Xanh SM Car (`#30670` + `#49424`)**: [uber_live_05a_xanh_car_hud.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_05a_xanh_car_hud.png) | [uber_live_05b_xanh_car_3rdperson.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_05b_xanh_car_3rdperson.png) | [uber_live_05c_xanh_car_driver_and_passenger.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_05c_xanh_car_driver_and_passenger.png)
  - **GrabBike (`#30671` + `#49425`)**: [uber_live_06b_grab_bike_3rdperson.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_06b_grab_bike_3rdperson.png) | [uber_live_06c_grab_bike_driver_and_passenger.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_06c_grab_bike_driver_and_passenger.png)
  - **Xanh SM Bike (`#30672` + `#49426`)**: [uber_live_07c_xanh_bike_driver_and_passenger.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_07c_xanh_bike_driver_and_passenger.png)
  - **BeBike (`#30673` + `#49427`)**: [uber_live_08c_be_bike_driver_and_passenger.png](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/uber_live_08c_be_bike_driver_and_passenger.png)
