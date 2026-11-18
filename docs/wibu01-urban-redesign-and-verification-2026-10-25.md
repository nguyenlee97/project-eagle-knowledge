# Quy Hoạch Đô Thị Tổng Thể, Kỹ Thuật Hạ Tầng & Nghiệm Thu In-Game Lục Địa WIBU-01 (Mokuloa / Đảo Nhật Bản)

- **Ngày thực hiện**: `2026-10-25`
- **Agent thực hiện**: Antigravity (`7251e9e7-9b8c-48c0-8cee-c5d25efec8dc`)
- **Đích tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Trạng thái**: `DONE — 100% PASS (Pre-Flight Doctor 11/11 PASS, Route Crawlers 3/3 PASS [9/9 chặng], Contact Sheet 6/6 PASS [0 anomalies], Aether Rig 6/6 PASS)`

---

## 1. Tóm tắt kiến trúc & quy hoạch đô thị WIBU-01 (`X=[-1850..-1000], Y=[-5500..-2950]`)

1. **Trục giao thông Bắc -> Nam xuyên suốt**:
   - **Cầu vượt biển Seto Ohashi (`wb_gg_*`, `wb_toll`)**: Từ Whetstone (`Y = -2965.0, Z = 47.56m`) qua Đảo Trung Tâm Ocean Citadel (`Y = -3745.6, Z = 35.95m`) xuống Quảng trường Đón tiếp phía Nam (`Y = -4525.0, Z = 24.37m`).
   - **Phố Điện Tử Akihabara Chuo-dori (`dodai01`, `dodai02`, `11850..11924`)**: Đại lộ chính chạy từ `Y = -4548.0` tới `Y = -4740.0` (`Z = 24.34m`), hai bên là hệ thống cửa hàng điện tử, biển hiệu neon hoạt động từ `18:00–05:00`, cầu vượt đường sắt JR Soubusen và hàng cây hoa anh đào.
   - **Đại lộ Kết nối Trung tâm & Hai Quảng trường Biểu tượng Đông/Tây (`kentry01`, `dodai03`)**:
     - Trục đại lộ trung tâm `kentry01` (`X = -1390.38, Y = -4740.0..-4900.7, Z = 23.33m`).
     - **Quảng trường Đông (`X = -1291.0, Y = -4745.0, Z = 23.33m`)**: Đặt **Tháp Tokyo (`Abase1..3` + `lodabase1`)** trên nền móng `dodai03` (`-1310.0, -4680.0 / -4810.0, Z = 22.25m`), tách hoàn toàn khỏi lòng đường cao tốc.
     - **Đồi Lâu đài Tây (`X = -1465.0, Y = -4745.0, Z = 25.33m`)**: Hạ **Lâu đài Nhật Bản (`jp_castle_wibu`)** từ cao độ lơ lửng `Z = 45.0m` xuống đúng mặt đất `Z = 25.33m` trên nền `dodai03` (`-1470.0, -4680.0 / -4810.0, Z = 22.25m`).
   - **Thủ phủ Kerorin (`kero01..15`, `IDs 11800..11815`)**:
     - Tịnh tiến đồng bộ toàn khu theo vector `dX = +6.581m, dY = -20.083m, dZ = +1.6167m` trong `CUSTOM\wibu01_japan_island.ipl` để cổng chào phía Bắc của `kero12` (cổng `ケロリン町` tại `Y = -4900.70, Z = 23.34m`) khớp liền mạch với mép Nam của `kentry01` (`Y = -4900.70, Z = 23.33m`, chênh cao `< 0.01m`).
     - Cắt bỏ `57` mặt tường vô hình (`mat=50`) chắn ngang điểm nối `kentry01 <-> kero12` trong `CUSTOM\wibu01_japan_island.col`.
   - **Đặc khu ZERO (`zero01..26`, `IDs 11817..11842`)**:
     - Quy hoạch lại về phía Tây của Thủ phủ Kerorin (`dX = -219.7374m, dY = -362.5875m, dZ = +5.2071m`, giữ nguyên góc xoay `90° CCW`), khớp đường nối phía Đông (`X = -1536.74, Y = -5120.73, Z = 23.34m`) với biên Tây của Kerorin (`0.00m` khe hở, `0.00m` lệch cao độ), chấm dứt hoàn toàn tình trạng chồng lấn lên `kentry01` và Kerorin.

2. **Xử lý Cờ Render (`IDE Flags`) & Va chạm (`.COL3`)**:
   - Gỡ bỏ cờ `4` (`DRAW_LAST` alpha-sort) khỏi toàn bộ các khối mặt đường và địa hình đặc (`dodai01..02`, `kentry01`, `kero01..15`, `zero01..26`) trong `CUSTOM\wibu01_japan_island.ide`, khắc phục triệt để lỗi mặt đất vẽ đè lên cây cối/hàng rào.
   - Bổ sung `.COL3` (`5,500` faces) cho `kero11` (`11810`) trong `CUSTOM\wibu01_japan_island.col` và đóng gói lại `MODELS\MODS\eagle_merged_mods.img`.

3. **Bản đồ 2D Minimap (`radar1300..1535.txd`) & AI Giao thông (`Wibu01HighwayNodes`)**:
   - Kết xuất mới **51 tile radar `128×128 DXT1`** (`radar1300.txd`..`radar1535.txd`) phủ kín `X=[-1850..-1000], Y=[-5500..-3000]` trong `S&S\Cdimages\default\radar.img` với shader tương phản cao (lòng đường nhựa tối `#23262E`, vỉa hè sáng `#C8CDD6`, công trình và cây anh đào phân tách rõ).
   - Biên soạn mới **6 file node AI** (`nodes1502.dat`, `nodes1566.dat`, `nodes1629.dat`, `nodes1630.dat`, `nodes1693.dat`, `nodes1694.dat`) trong `modloader\Wibu01HighwayNodes\data\Paths\` (`65` node phương tiện + `92` node người đi bộ), đưa xe cộ và NPC hoạt động thực tế trên khắp Cầu Seto Ohashi, Akihabara, Đại lộ Sakura, Thủ phủ Kerorin và Đặc khu ZERO.

---

## 2. Kết quả Nghiệm thu In-Game (`task-1346`)

| Hạng mục kiểm thử | Kết quả | Chi tiết kỹ thuật |
| :--- | :---: | :--- |
| **1. Pre-Flight Doctor** | **`11/11 PASS`** | `0 WARN, 0 FAIL` (`59 ms`) — toàn bộ bảng `FLA 7.7`, `.COL`, `.IDE`, `.IPL`, `radar.img` hợp lệ. |
| **2A. Route Crawler `WIBU01_BUG011_SPAN`** | **`3/3 PASS`** | Đi bộ thực tế qua nhịp Bắc cầu Seto Ohashi (`wb_gg_n03`, `Y = -3398.5 -> -3415.0, Z = 56.25 -> 55.78m`). |
| **2B. Route Crawler `WIBU01_BRIDGE_SEAM`** | **`3/3 PASS`** | Đi bộ qua mối nối chân cầu Nam Seto Ohashi vào đại lộ Akihabara Chuo-dori (`Y = -4538.0 -> -4564.7, Z = 24.37 -> 24.52m`). |
| **2C. Route Crawler `WIBU01_SAKURA_TO_KERORIN`** | **`3/3 PASS`** | Đi bộ từ đại lộ Sakura (`kentry01`) qua cổng chào `ケロリン町` vào vòng xuyến và trục chính Thủ phủ Kerorin (`Y = -4890.0 -> -4931.7, Z = 24.15 -> 24.32m`). |
| **3. Contact Sheet 6 Điểm Dừng (`WIBU01_TOUR`)** | **`6/6 PASS`** | `0 anomalies` trên cả 6 điểm dừng; ghi nhận đầy đủ mô hình tĩnh, xe cộ và NPC trong RAM. |
| **4. Aether 6-Step Rig & Action Test** | **`6/6 PASS`** | `Clump/RAM PASS`, `Walk 0.45m PASS`, `Sprint 1.55m PASS`, `Jump +0.87m & Land Z=24.34m PASS`, `Weapon/PedState PASS`, `Camera & Screenshot PASS`. |
| **5. Kiểm tra Thị giác Ban ngày (`12:00`) & Ban đêm (`22:00`)** | **`12/12 PASS`** | Chụp và xác nhận thực tế 6 ảnh Contact Sheet ban ngày, 4 ảnh ban đêm (`22:00`) và 2 ảnh đại cảnh Đặc khu ZERO & Tháp Tokyo. |

---

## 3. Danh sách File đã cập nhật & Trạng thái Khóa

- `CUSTOM\wibu01_japan_island.ide`
- `CUSTOM\wibu01_japan_island.ipl`
- `CUSTOM\wibu01_japan_island.col`
- `CUSTOM\wibu01_japan_island.img`
- `MODELS\MODS\eagle_merged_mods.img`
- `S&S\Cdimages\default\radar.img` (`radar1300..1535.txd`)
- `modloader\Wibu01HighwayNodes\data\Paths\nodes1502.dat`, `nodes1566.dat`, `nodes1629.dat`, `nodes1630.dat`, `nodes1693.dat`, `nodes1694.dat`
- `eagle_ingame_tester.py` (hỗ trợ con trỏ RAM LAA `< 0xFFFF0000`, sửa nút chạy nước rút `ButtonCross` `+0x20`, tránh xe NPC cản đường khi chạy crawler, gỡ kẹt `CTimer::m_CodePause` khi chạy nền)
- **Trạng thái khóa**: Đã giải phóng (`docs/project-eagle/locks/active-locks.json` trống, không giữ `game-write.lock`).
