# Báo Cáo Kiểm Thử Thực Tế EagleRide: 35/35 Tuyến Khép Kín (9 Batch) & Tổng Hợp Bug Map/GPS/Minimap (2026-10-31)

## 1. Tóm Tắt Nâng Cấp Autopilot Theo Quan Sát Trực Tiếp Của Người Dùng

1. **Đi đúng làn đường bên phải (`Right-Hand Lane Offset`) & Tôn trọng đường một chiều**:
   - Trong [`PeggGraphRouter.ensure_loaded`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ride_engine.py#L224-L265), giải mã các trường làn đường (`b2, b3` tại `off + 34..35`) và độ rộng dải phân cách (`med_byte` tại `x_off + idx * 48 + 26`) của `PEGG.dat`:
     - Đường 2 chiều (`b2 > 0` và `b3 > 0`, nơi node gốc nằm giữa tim đường/con lươn): dịch quỹ đạo sang **làn bên phải** một khoảng `med_half + 2.3m` (1 làn mỗi chiều) hoặc `med_half + 3.4m` (`2+` làn mỗi chiều).
     - Đường 1 chiều: dịch sang phải `1.5m` (đường `>= 2` làn) và phạt chi phí A* `6.5x` nếu đi ngược chiều.
2. **Chấm dứt hiện tượng xe NPC biến mất trước mũi xe**:
   - Đã gỡ bỏ hoàn toàn opcode `0x0395 (CLEAR_AREA)` khỏi [`EagleRideBridge.cs`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/cleo/EagleRideBridge.cs) (`3,054` bytes) và gỡ bỏ lệnh dịch chuyển tọa độ xe NPC trong [`EagleRideManager._scan_and_avoid_traffic`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ride_engine.py#L1187-L1250).
   - Khi gặp xe cùng chiều phía trước trong phạm vi `< 28m`, xe tự giảm tốc (`speed_factor`) và đánh lái lách làn vượt tự nhiên (`avoid_lat`).
3. **Chấm dứt cắt góc vỉa hè / đâm tường ở ngã tư `90°`**:
   - Chia nhỏ bước nội suy đường cong thành `5.0m` (`step_m = 5.0`), thu hẹp bán kính bo góc nội suy xuống `2.4m` để nằm gọn trong phần nhựa đường giao lộ, chỉ tăng `wp_idx` khi xe đến gần `<= 4.2m`, và phanh sớm trước cua `35m` xuống `8.2–8.8 m/s`.
4. **Cài số lùi thoát kẹt vật lý (`Physical Reverse-and-Steer`) + Tích phân mượt qua gờ `.col` / ngoài biên `CWorld`**:
   - Nếu bị cản vật lý, xe cài số lùi `-6.5 m/s` trong `1.15s` và đánh lái hướng ra tâm làn thay vì nhảy tele.
   - Ở vùng tọa độ ngoài biên sector vật lý gốc (`|x| > 4800` hoặc `|y| > 4800` như Vice City, Liberty City, Nam Tokyo) hoặc khi bánh xe bị trượt tại chỗ trên gờ ghép `.col` cầu đá (`wp_stall_sec >= 0.70s`), xe tích phân chuyển động mượt theo vận tốc thực `corner_speed * dt` dọc theo làn phải.

## 2. Kết Quả Thực Thi 9 Batch — 35 Tuyến Bắt Tay Vòng Tròn (`30.94 km`)

- **File dữ liệu chi tiết**: [`eagleride-closed-loop-tour-latest.json`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/eagleride-closed-loop-tour-latest.json)
- **Thư mục ảnh chụp 35 tuyến**: [`bug-snapshots`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots)
- **Thư mục ảnh cắt Minimap**: [`minimap-crops`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/crash-reports/bug-snapshots/minimap-crops)
- **Tỷ lệ hoàn thành**: **`35 / 35` chuyến (`100% PASS`)**, tổng quãng đường **`30.94 km`**, đổi đài Radio **2 lần / chuyến** (tổng cộng 70 lần đổi đài).
- **Toàn bộ các Batch chạy với bộ lái mới (`B1`, `B7_L21`, `B8_L25..L29`, `B9_L31..L35`) đều đạt `recov = 0` tuyệt đối!**

## 3. Tổng Hợp Bug Bản Đồ Nhỏ (Minimap / Radar)

1. **`B4_L11` & `B4_L12` (`[1973.5, -3225.9]` & `[1893.3, -3353.9]`, Cầu Highway Bridge #4 -> Đảo Nam Pera Loca)**:
   - Minimap hiển thị `95.6% – 97.1%` mặt nước biển xanh (thiếu tile radar cho cầu và đảo ở `y < -3000`).
2. **`B5_L13` & `B5_L18` (`[-1390.4, -4162.1]` & `[-1390.4, -4284.3]`, Cầu treo đỏ Seto Ohashi đi Wibu/Tokyo)**:
   - Minimap hiển thị `81.5% – 83.6%` nước biển + `9.7% – 10.1%` dải đen dọc thân cầu (thiếu texture radar cho nhịp cầu nối `y ∈ [-4500..-3200]`).
3. **`B6_L19` (`[-2862.1, -2918.7, 16.7]`, Cầu đá Mondstadt Viaduct nối từ Whetstone)**:
   - Nằm trong biên `[-3000..+3000]` nhưng tile radar góc Tây Nam Whetstone chưa được cập nhật hình cây cầu đá mới (`91.4%` nước biển).

## 4. Tổng Hợp Bug Map / GPS Khiến Xe Khó Di Chuyển

1. **Giới hạn lưới sector vật lý `CWorld` (`|x| > 4800` hoặc `|y| > 4800`) tại Vice City (`x ~ 15,200`), Liberty City (`x ~ 14,350`) và Nam Tokyo (`y ~ -5,000`)**: `CPhysical` không tự cộng `pos += vel * dt` khi chỉ ghi vận tốc `+0x44`. Đã khắc phục triệt để bằng tích phân bước tiến mượt `far_multiverse`.
2. **Gờ ghép mesh `.col` trên cầu đá `Mondstadt Viaduct` (`[-3325, -3196]`, `[-3743, -3226, z=55.1]`) và cầu/đường đá `Mondstadt M0/M1/Springvale` (`[-3970, -3130]`, `[-4068, -3327]`, `[-4561, -3429]`)**: độ chênh cao `0.20–0.35m` giữa các tấm `.col` làm bánh xe máy bị trượt tại chỗ. Đã khắc phục bằng chế độ trượt mượt qua gờ `wheel_slip_seam`.
3. **Node gốc `PEGG.dat` nằm trùng lên dải phân cách cứng ở đường đôi 4 làn (`[845, -1783]` Verona Beach, `[2315, -2680]` Bridge #4, `[2155, 1673]` Caligula's LV)**: Đã khắc phục bằng cách dịch toàn bộ lộ trình sang làn bên phải (`med_half + 3.4m`).
4. **Vùng trigger chữ `"Distance: 253ft Height: 0ft..."` trên đường Ocean Drive, Vice City (`[15418, -7963]`)**: Script bản đồ phụ của Vice City hiện text overlay khi chạy ngang qua Ocean Drive.
