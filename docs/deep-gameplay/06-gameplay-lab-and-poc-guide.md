# 06 — Hướng Dẫn Gameplay Lab & EaglePhone OS v2.0 (Project Eagle v1.3)

Tài liệu này ghi nhận bản nâng cấp **EaglePhone OS v2.0** trong môi trường thử nghiệm độc lập (`gta sa gameplay-lab`) cùng phân tích tương thích chi tiết cho 2 video mod Realistic Life / Jobs trên YouTube.

---

## 1. Những Nâng Cấp Lớn Trong EaglePhone OS v2.0

1. **Đồng Bộ 100% Thời Gian Thực Tiền Mặt (`Cash`) & Máu (`Health`) Với GTA SA (Bỏ Theo Dõi Xăng)**:
   - **Cầu nối Bộ Nhớ Win32 Trực Tiếp (`GTAProcessBridge` trong [`EagleCompanion.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/EagleCompanion.py))**:
     - Đọc/ghi trực tiếp vào RAM của `gta_pe.exe` / `gta_sa.exe` mỗi `100ms`:
       - `0x00B7CE50` (`CWorld::Players[0].m_nMoney` — Tiền mặt thực tế) & `0x00B7CE54` (`m_nDisplayMoney` — Bộ đếm tiền trên HUD).
       - `*(0x00B7CD98) + 0x540` (`CPed::m_fHealth` — Máu thực của Aether), `+ 0x544` (`m_fMaxHealth`), `+ 0x548` (`m_fArmour`).
       - `0x00B70153` / `0x00B70152` / `0x00B70154` (Giờ, Phút, Ngày thực trong game).
   - **Cầu nối CLEO 5 Song Hành ([`EagleLifePoC.cs`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/cleo/EagleLifePoC.cs))**:
     - Mỗi `200ms`, script CLEO 5 đọc `010B` (`store_score`) và `0226` (`get_actor_health`), đồng thời thực thi `0109` (`add_score`) và `0223` (`set_actor_health`) nếu có bất kỳ thay đổi nào từ Sidecar.
   - **Loại bỏ hoàn toàn thanh Xăng (`Fuel`)**: Giữ trải nghiệm lái xe dạo phố mượt mà.

2. **Giao Diện Màn Hình Điện Thoại Thông Minh Kép (`Dual Smartphone Screen UI`)**:
   - **Màn hình Điện Thoại DirectX 9 ngay trong Game ([`hud.lua`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/hud.lua))**:
     - Loại bỏ hoàn toàn bảng `08D4` thô kệch của GTA SA gốc.
     - Vẽ khung điện thoại bo góc Titanium, màn hình OLED tối, tai thỏ Dynamic Island, thanh trạng thái `5G` + Giờ game + Máu & Tiền thật, cùng **biểu đồ nến/đường (`Sprite2d.DrawLine` & `Sprite2d.DrawRect`)** ngay góc dưới bên phải màn hình GTA SA!
   - **Ứng dụng Điện Thoại Tương Tác Chuột ([`eagle_phone_ui.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_phone_ui.py) tại `http://127.0.0.1:8765`)**:
     - Tự động mở ở chế độ cửa sổ Smartphone (`450x890`) hoặc chuyển sang chế độ Máy Tính Bảng (`Tablet Mode`) với 1 cú click.

3. **Chứng Khoán (2010–2020) & Crypto (2017–2021) — Biểu Đồ OHLC, Delta %, Spot & Futures Long/Short**:
   - 9 mã tài sản lịch sử ([`eagle_historical_data.py`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab/eagle_historical_data.py)): `BTC`, `ETH`, `BNB`, `DOGE` (giai đoạn hậu bùng nổ 2017–2021) và `NVDA`, `TSLA`, `AAPL`, `AMZN`, `NFLX` (giai đoạn 2010–2020).
   - Biểu đồ 60 cây nến **OHLC Candlestick** + **Line Chart** + đường trung bình động **MA7**, hiển thị `% Delta 24h`, đỉnh/đáy 24h.
   - Hỗ trợ **Mua/Bán Spot** và **Giao dịch Futures Vĩnh Cửu (`Mở LONG` / `Mở SHORT`)** với đòn bẩy `2x`, `5x`, `10x`, `20x`, `50x`, tự động tính **Giá Thanh Lý (`Liquidation Price`)**, **PnL ($)** và **ROE (%)**.

4. **Cá Cược Thể Thao Đa Giải Đấu (`EagleBet` — Dữ Liệu Lịch Sử 2010–2020)**:
   - 5 giải đấu kinh điển: **Premier League (2011–2019)**, **UEFA Champions League (2011–2019)**, **La Liga (2011–2018)**, **FIFA World Cup (2010/2014/2018)**, và **NBA Playoffs (2011–2019)**.
   - Đầy đủ khung giờ thi đấu, tỉ lệ kèo **`1X2` (Chủ – Hòa – Khách)**, **Kèo Chấp (`Handicap`)**, **Tài Xỉu (`Over/Under`)**, **Bảng Xếp Hạng Giải Đấu**, và **Trang Lịch Sử Kết Quả & Bản Tin Thể Thao 2010–2020**.

5. **Trung Tâm Vé Số 4-Trong-1 (`EagleLotto`)**:
   - **Vé Số Cào Nhận Thưởng Ngay (`Scratch Card` \$20 Bạc / \$100 Hoàng Kim)**: Lưới cào 3x3 ô với xác suất kiểm soát thực tế, trúng từ \$20 đến \$50,000.
   - **Vé Số Kiến Thiết 6 Chữ Số (\$10/vé)**: Cơ cấu giải thưởng từ trúng 2 số cuối (\$50), 3 số cuối (\$150), 4 số (\$2,500), 5 số (\$15,000) đến **Giải Đặc Biệt 6 số (\$200,000)**.
   - **Vietlott `Mega 6/45` & `Power 6/55` (\$10/vé)**: Tự chọn 6 cặp số hoặc máy chọn (`Quick Pick`), giải Jackpot tích lũy từ **\$1,250,000+**.

---

## 2. Đánh Giá Kỹ Thuật 2 Video Mod Realistic Life / Nghề Nghiệp Trên YouTube

### Video 1: `https://www.youtube.com/shorts/z837CaX2mDc` (*TheJizzy — "These Realistic Mods Bring GTA San Andreas to LIFE"*)
- **Nội dung**: Giới thiệu các CLEO script tạo hoạt cảnh NPC dọn vệ sinh đường phố (công nhân quét rác), xe chở rác hoạt động, nghệ sĩ đường phố và hành vi NPC tự nhiên.
- **Đánh giá tương thích với Project Eagle v1.3**:
  - **Không xung đột với EaglePhone OS**: Các mod hành vi NPC ngoại cảnh chỉ spawn task (`CTaskComplex`) trên ped thường.
  - **Lưu ý quan trọng**: Project Eagle v1.3 đã tích hợp sẵn nhiệm vụ xe rác (`TRASHMASTER` — Trash Dash trong `main.scm`) và hệ thống `PedFuncs.asi`. Nếu cài thêm script CLEO spawn xe rác tự động, chỉ nên dùng bản `.cs` thuần (không thay `main.scm` hay `ped.ifp`).

### Video 2: `https://www.youtube.com/watch?v=pH0zMQlAifI` (*ZeeMods — "Convertí GTA San Andreas en un Simulador de la Vida Real..."*)
Video tổng hợp 20 mod đời sống thực tế. Khi đối chiếu trực tiếp với cấu trúc file của **Project Eagle v1.3**, kết quả phân loại như sau:

| Nhóm | Các Mod trong Video | Trạng thái trên Project Eagle v1.3 & Khuyến nghị |
| :--- | :--- | :--- |
| **1. Đã có sẵn trong Project Eagle v1.3 (TUYỆT ĐỐI KHÔNG CÀI ĐÈ)** | • `1:21` Car Wash (Rửa xe)<br>• `5:23` Peds Vary (Đa dạng trang phục NPC)<br>• `13:18` Climbmod (Leo thang)<br>• `16:56` Loader Work (Lái xe nâng hàng Forklift)<br>• `19:51` Motel Mod (Thuê phòng khách sạn)<br>• Garbage Collector (Lái xe rác) | **Đã tích hợp sẵn trong Eagle v1.3**:<br>- Rửa xe (`CARWSHA`), Xe nâng (`Side_Games_Mission`), Khách sạn (`X_HOTEL`), Xe rác (`TRASHMASTER`) đã nằm trong `main.scm` của Eagle.<br>- Leo thang đã có trong `PECore.asi` (`ClimbingLadders`).<br>- Đa dạng NPC đã có `scripts\PedFuncs.asi`.<br>👉 **Cài đè các bản rời trên mạng sẽ gây trùng marker hoặc crash `main.scm`.** |
| **2. Tương thích tốt & Rất hợp để tích hợp tiếp** | • `14:21` Talk with people like RDR2 (Chào hỏi / Trêu chọc NPC)<br>• `15:28` CJ Street Guitar (Đánh đàn kiếm tiền trên phố)<br>• `17:38` Gasoline Job (Làm nhân viên trạm xăng)<br>• `3:53` Vending Machines / `2:15` Peds Umbrella | **Tương thích cao**:<br>- Cơ chế chào hỏi/nói chuyện với NPC kiểu RDR2 khớp hoàn hảo với định hướng AI NPC (Trụ cột 4) của chúng ta.<br>- Các nghề phụ (đánh đàn đường phố, làm việc tại trạm xăng/cửa hàng) có thể tích hợp trực tiếp vào **App 1 (`Life & Jobs`)** trên `EaglePhone` để trả lương thẳng vào tài khoản GTA SA mà không sợ xung đột biến toàn cục `$var`. |
| **3. Cần thận trọng với Animation Aether** | • `10:15` Diving (Nhảy chúi đầu xuống nước)<br>• Các mod thay `ped.ifp` gốc | Cần kiểm tra kỹ với rig xương của skin `AETHER.dff` trước khi cài các mod sửa file animation gốc `anim\ped.ifp`. |
