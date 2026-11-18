# Sector M1 Enhanced — Driveable Terrain, Scenic Highway, 10 Development Pads & GPS Network (`M0 + M1`)

Cập nhật **2026-10-24 03:15 (Asia/Saigon)**.
- **Trình xem WebGL 3D hợp nhất (Drive Mode + GPS + Minimap Radar)**: [mondstadt-m0-m1-3d-inspection-report-2026-10-23.html](mondstadt-m0-m1-3d-inspection-report-2026-10-23.html)
- **Phiếu công việc nâng cấp Sector M1 Enhanced**: [2026-10-24-antigravity-mondstadt-wilds-m1-enhanced.md](work-items/2026-10-24-antigravity-mondstadt-wilds-m1-enhanced.md)
- **Phiếu baseline trước nâng cấp**: [2026-10-23-codex-mondstadt-wilds-m1.md](work-items/2026-10-23-codex-mondstadt-wilds-m1.md)

---

## 1. Tổng quan Kết quả Nâng cấp (`Sector M1 Enhanced`)

Gói `Sector M1` trong `D:\GTA Archive\Staging\teyvat-mondstadt-wilds-m1-2026-10-23\` (`IDs 6730..6801`, khung ENU `[-768m .. +768m]`) đã được nâng cấp toàn diện thành bản **Sector M1 Enhanced (Driveable Terrain + Scenic Highway + 10 Development Pads + GPS Network)** và đạt **100% PASS** trên toàn bộ các phép kiểm định nhị phân, đi bộ `A*`, lái xe `A*` và trình duyệt WebGL:

| Hạng mục / Kiểm định | Kết quả Đo lường Thực tế |
| --- | --- |
| **Lưới địa hình & Pivot** | `6×6` (`36` tile `256m × 256m`, ENU `[-768m .. +768m]`); toàn bộ Pivot `Z` căn chỉnh chính xác trên lattice `1/128m` (`0.0078125m`) |
| **Khóa biên M0–M1** | Bảo toàn nguyên vẹn **231 đỉnh chung (`shared_boundary_vertices`)** và **34 đỉnh biến dạng (`modified_vertices`)** từ `mondstadt_m0_m1_ownership.json`; sai số analytic `0.000 m`, sai số DFF `0.005 mm`, sai số COL3 `6.117 mm` |
| **Near Models (`6730..6765`)** | `36` model (`mw1_t00..35`), `109,928` triangles (gồm mặt đất, đường bộ, 10 bãi đất nền, đáy hồ `-61.5m`, cây thông/bụi cỏ và `171` cột đèn đường `2dfx` ban đêm); draw distance `295.0 m` |
| **LOD Models (`6766..6801`)** | `36` model (`lmw1_t00..35`), `73,961` triangles; draw distance `1500.0 m` |
| **Collision (`mondstadt_wilds_m1.col`)** | `36` `.COL3` entries; dung lượng tối đa **26,804 B < 92,768 B** (`28.9%` hạn mức); mọi tọa độ local thuộc `±128m` |
| **Mạng lưới Đường Ô tô 2 Làn** | `6` tuyến chính (`Route M1-Ring 360°`, `Route Whispering Woods`, `Route Springvale Highway`, `Route East Touge`, `Route South Touge`, `Route West Peak Overlook`), rộng `11m–12m`, vật liệu `SURF_PAVEMENT = 4`, độ dốc dọc tối đa `10.4° <= 15°` (`nz >= 0.983`), có lề đường đá và `171` bóng đèn `2dfx` (`0x0253F2F8`) |
| **10 Khu Đất Nền Phẳng (`PAD-01..10`)** | `10` bãi đất nền phẳng (`36m×36m` đến `60m×60m`, độ dốc `0.0°`, `nz = 1.000`, sai số lượng tử hóa `.COL3` `0.000 mm`), xuất tại `m1_development_pads.json` |
| **Đồ thị Định tuyến GPS & Lua** | `mondstadt_m1_gps_graph.json` (**446 nodes**, **452 bidirectional edges**, **38 POIs** gồm 20 POI trong `M0`, 10 `PAD-01..10`, 4 mốc `M1` và 4 đỉnh núi) + `lua/mondstadt_gps_navigator.lua` |
| **Foliage Raycast** | **4,112** cụm (`789` pine + `3,323` grass), chỉ mọc trên `SURF_GRASS_LUSH = 9` (`nz >= 0.80`), loại trừ 100% mặt đường ô tô và 10 Development Pads |
| **Kiểm toán Nhị phân (`verify_m1.py`)** | **83/83 PASS** (`status: "pass"`, `errors: []`, `7/7` geometry fixtures PASS) |
| **Kiểm định `A* Walkability`** | **17/17 PASS (100%)** từ đầu Cầu Đá Mondstadt `(321.0, -93.1)` tới cả 3 mốc gốc (`Rừng Thì Thầm`, `Thanh Tuyền`, `Bờ Nam Hồ Cider`) + `4` đỉnh núi + `10` Development Pads (`251,291` walkable support samples) |
| **Kiểm định `A* Vehicle Driveability`** | **38/38 POI PASS (100%)**, bề rộng thông thủy `>= 11.0m >= 8.0m`, độ dốc dọc đường tối đa `<= 10.4° <= 15.0°` |
| **Kiểm định Độc lập `Glitch Lab` (`Retest Vòng 1`)** | **`0` lỗi hình học trong `M1` (`M1 glitches = []`)**, **`0 / 100` Swarm Bots gặp lỗi thật** (`75/100 PASS` + `25/100 INTENDED_TERRAIN` dừng tại bờ hồ `-61.5m` / vách núi cao tự nhiên), độ phủ đi bộ **`98.23%`** (`348,525 / 354,816` ô), bảo toàn nguyên vẹn 4 đỉnh núi (`+12m..+36m`) và lòng hồ `-61.5m` (Anti-Pancake) |
| **Kiểm định Trình duyệt (`browser_qa.py`)** | **11/11 PASS** trên Headless Chromium (`file://` offline, `16,420,292 bytes`, SHA-256 `a18ea637c44be5844c798a2547a9b241354dc5c7be9a01cfdefff91bcd47328b`, 0 CDN requests, 0 JS errors) |

---

## 2. Chi tiết 17/17 Tuyến `A* Walkability` & `Vehicle Driveability` (`walkability.json`)

Xuất phát từ **Đầu Cầu Đá Chính Mondstadt `M0` `(E = +321.0, N = -93.1, U = -55.38)`** trên lưới va chạm hợp nhất `M0 + M1` (`80,052` tam giác `.COL3`, `247,861` mẫu mặt đứng hợp lệ):

| # | Mốc kiểm định / Development Pad | Tọa độ ENU `(E, N, U)` | Kết quả `A*` | Chiều dài tuyến (m) | Số nút duyệt | Thời gian (s) |
| :-: | --- | --- | :-: | ---: | ---: | ---: |
| 1 | **Rừng Thì Thầm (mốc gốc #1)** | `(+520.0, +140.0, -46.0)` | **PASS** | `376.801` | `1,285` | `2.34` |
| 2 | **Thị trấn Thanh Tuyền (mốc gốc #2)** | `(-364.0, -420.0, -36.0)` | **PASS** | `966.200` | `15,918` | `28.06` |
| 3 | **Bờ nam Hồ Cider (mốc gốc #3)** | `(-250.0, -280.0, -52.0)` | **PASS** | `793.787` | `7,556` | `1.05` |
| 4 | **Đỉnh núi phía Đông (East Peak Touge)** | `(+660.0, -40.0, +12.0)` | **PASS** | `403.558` | `3,021` | `2.17` |
| 5 | **Đỉnh núi phía Nam (South Peak Touge)** | `(+160.0, -640.0, +28.0)` | **PASS** | `683.772` | `6,957` | `6.58` |
| 6 | **Đỉnh đồi phía Tây (West Peak Overlook)** | `(-560.0, +180.0, +24.0)` | **PASS** | `1,274.929` | `17,745` | `15.08` |
| 7 | **Đỉnh núi phía Bắc (Stormbearer North Peak)** | `(+260.0, +620.0, +36.0)` | **PASS** | `850.282` | `7,356` | `7.22` |
| 8 | **PAD-01: Quảng Trường Đầu Cầu Mondstadt** | `(+372.0, -96.0, -55.0)` | **PASS** | `78.468` | `264` | `0.31` |
| 9 | **PAD-02: Quảng Trường Rừng Thì Thầm** | `(+520.0, +140.0, -46.0)` | **PASS** | `376.801` | `1,285` | `0.36` |
| 10 | **PAD-03: Bến Hồ Đông & Phố Ẩm Thực** | `(+376.0, -210.0, -53.0)` | **PASS** | `153.573` | `272` | `0.34` |
| 11 | **PAD-04: Trung Tâm Thị Trấn Thanh Tuyền** | `(+180.0, -450.0, -42.0)` | **PASS** | `470.112` | `2,234` | `0.38` |
| 12 | **PAD-05: Bờ Nam Hồ Cider & Bến Du Thuyền** | `(-250.0, -280.0, -52.0)` | **PASS** | `793.787` | `7,556` | `0.44` |
| 13 | **PAD-06: Đồi Tây Thanh Tuyền & Trang Viên** | `(-364.0, -420.0, -36.0)` | **PASS** | `966.200` | `15,918` | `0.66` |
| 14 | **PAD-07: Trạm Dừng Chân Lưng Đèo Đông** | `(+610.0, -220.0, -8.0)` | **PASS** | `348.993` | `2,061` | `1.38` |
| 15 | **PAD-08: Đỉnh Núi Đông — Đài Quan Sát** | `(+660.0, -40.0, +12.0)` | **PASS** | `403.558` | `3,021` | `0.44` |
| 16 | **PAD-09: Đỉnh Núi Nam — Đấu Trường Thượng Đỉnh** | `(+160.0, -640.0, +28.0)` | **PASS** | `683.772` | `6,957` | `0.64` |
| 17 | **PAD-10: Đỉnh Đồi Tây — Lâu Đài Hoàng Hôn** | `(-560.0, +180.0, +24.0)` | **PASS** | `1,274.929` | `17,745` | `0.98` |

---

## 3. Danh sách 10 Bãi Đất Nền Phẳng (`m1_development_pads.json`) Cho Hội Thoại #2

Toàn bộ 10 bãi đất nền đều được đặt tại cao độ `U` nguyên (`integer meters`) nên có **sai số lượng tử hóa `.COL3` (`1/128m`) bằng đúng `0.000 mm`**, mặt phẳng ngang tuyệt đối (`nz = 1.000`, `slope = 0.0°`), nối trực tiếp với mạng lưới đường ô tô `SURF_PAVEMENT = 4`:

| Mã Pad | Tên Khu Đất | Tâm ENU `(E, N, U)` | Kích thước `(W × D)` | Hướng mặt tiền (`heading_deg`) | Tuyến đường kết nối |
| :---: | --- | --- | :---: | :---: | --- |
| `PAD-01` | Quảng Trường Đầu Cầu & Trạm Dừng Konbini | `(372.0, -96.0, -55.0)` | `40m × 40m` | `270.0°` | `Route M1-Ring` & Cầu Đá `M0` |
| `PAD-02` | Quảng Trường Rừng Thì Thầm | `(520.0, 140.0, -46.0)` | `48m × 48m` | `225.0°` | `Route Whispering Woods` |
| `PAD-03` | Bến Hồ Đông & Phố Ẩm Thực Ven Hồ | `(376.0, -210.0, -53.0)` | `44m × 44m` | `280.0°` | `Route M1-Ring` & `East Touge` |
| `PAD-04` | Trung Tâm Thị Trấn Thanh Tuyền | `(180.0, -450.0, -42.0)` | `60m × 60m` | `0.0°` | `Route Springvale Highway` & `South Touge` |
| `PAD-05` | Bờ Nam Hồ Cider & Bến Du Thuyền | `(-250.0, -280.0, -52.0)` | `56m × 48m` | `15.0°` | `Route M1-Ring` & `Springvale Highway` |
| `PAD-06` | Đồi Tây Thanh Tuyền & Trang Viên | `(-364.0, -420.0, -36.0)` | `52m × 52m` | `45.0°` | `Route Springvale Highway` |
| `PAD-07` | Trạm Dừng Chân Lưng Đèo Đông | `(610.0, -220.0, -8.0)` | `36m × 36m` | `210.0°` | `Route East Touge` |
| `PAD-08` | Đỉnh Núi Đông — Đài Quan Sát Toàn Cảnh | `(660.0, -40.0, +12.0)` | `40m × 40m` | `265.0°` | `Route East Touge` |
| `PAD-09` | Đỉnh Núi Nam — Đấu Trường Thượng Đỉnh | `(160.0, -640.0, +28.0)` | `44m × 44m` | `350.0°` | `Route South Touge` |
| `PAD-10` | Đỉnh Đồi Tây — Lâu Đài Hoàng Hôn | `(-560.0, 180.0, +24.0)` | `44m × 44m` | `100.0°` | `Route West Peak Overlook` |

---

## 4. Bằng chứng Tệp trên Đĩa (`D:\GTA Archive\Staging\teyvat-mondstadt-wilds-m1-2026-10-23\`)

- **Binary & Placement**:
  - `mondstadt_wilds_m1.img` (`VER2`, `75` members: `36` Near `.DFF`, `36` LOD `.DFF`, `mondstadt_wilds_m1.txd`, `mw1_lod.txd`, `mw1.col`)
  - `mondstadt_wilds_m1.ide`, `mondstadt_wilds_m1_west_continent.ipl`, `mondstadt_wilds_m1_sandar_bay.ipl`
  - `models/col/mondstadt_wilds_m1.col` (`mw1.col`), `models/txd/mondstadt_wilds_m1.txd`, `models/txd/lod_mondstadt_wilds_m1.txd` (`mw1_lod.txd`)
- **Development Pads & GPS System**:
  - `m1_development_pads.json` (`10` flat development pads `PAD-01..10`)
  - `mondstadt_m1_gps_graph.json` (`445` nodes, `451` edges, `38` POIs)
  - `lua/mondstadt_gps_navigator.lua` (Lua module tương thích `EaglePhone GG Map` & `SanViveLuaHudSA`)
- **Audit & QA Evidence**:
  - `audit.json` (`83/83 PASS`), `walkability.json` (`17/17 PASS`), `evidence/seam.json`, `evidence/protected-inputs.json`, `evidence/browser-qa.json` (`11/11 PASS`)
  - `evidence/viewer-overview.png`, `evidence/viewer-drive-gps.png`, `evidence/viewer-collision-grid.png`, `evidence/viewer-walk-bridge.png`, `evidence/viewer-night.png`, `evidence/viewer-audit-panel.png`
