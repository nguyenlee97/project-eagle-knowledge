# 03. Hướng Dẫn Sử Dụng Eagle Radio Studio (Từ Tạo Kênh Đến Cài Đặt & Phục Hồi)

## 1. Cách Mở Công Cụ

Nhấp đúp chuột vào file:
- [`C:\Users\LENOVO\Desktop\GTA\Start_Eagle_Radio_Studio.bat`](file:///C:/Users/LENOVO/Desktop/GTA/Start_Eagle_Radio_Studio.bat)

Trình duyệt sẽ tự động mở giao diện **Eagle Radio Studio** tại địa chỉ `http://127.0.0.1:8790`.

---

## 2. Chọn Đúng Mục Tiêu (Gameplay-Lab vs. Game Chính)

Ở thanh trên cùng của ứng dụng:
- **🧪 Bản Thử Nghiệm (`gta sa gameplay-lab`) [Khuyến nghị]:** Dùng để thử nghiệm kênh mới, logo mới và phân bổ vùng mà không chạm vào bản game chính.
- **🎮 Bản Game Chính (`gta sa clean`):** Dùng khi bạn đã hài lòng với danh sách nhạc và muốn đưa vào bản game chính.
- Thanh trạng thái phía dưới luôn hiển thị rõ:
  - Tình trạng game đang chạy hay đang đóng (`🟢 Game đang đóng` / `🔴 Game đang mở`).
  - Tình trạng bảo toàn các mod hiện có (`🛡️ Aether F2: Nguyên vẹn`, `🛡️ NPC COMPONENTPEDS.img: Nguyên vẹn`, `🛡️ EagleCompanion Lab: Nguyên vẹn`).

---

## 3. Tạo Kênh, Thêm Nhạc & Sắp Xếp Playlist (Tab 1)

1. **Tạo kênh mới:**
   - Bấm **`➕ Tạo Kênh Mới`** ở cột bên trái (hoặc bấm **`✨ Tạo Nhanh 3 Kênh Mẫu`** để nạp thử bộ 3 kênh mẫu kèm 4 định dạng nhạc test).
   - Đặt **Tên Kênh Hiển Thị**: Tool tự động hiển thị bản xem trước tên ASCII/GXT sẽ xuất vào `data\radio.dat` (tự động chuyển tiếng Việt có dấu sang không dấu và thay dấu phẩy `,` bằng `-` để không làm gãy bộ đọc CSV của `PECore.asi`).
2. **Chọn Logo hiển thị trên HUD:**
   - **Chế độ 1 (Mặc định):** `✨ Tự tạo Logo 256×256 theo Tên Kênh (Auto-Badge)` — chọn 1 trong 6 tông màu (`Neon Anime`, `City Pop 80s`, `Lo-Fi Chill`, `Cyber Gold`, `Crimson Rock`, `Emerald OST`) và nhãn phụ. Tool sẽ tự vẽ đĩa logo tròn 256×256 sắc nét và đóng gói vào `models\txd\radio.txd`.
   - **Chế độ 2:** `🎨 Dùng 1 trong 75 Logo có sẵn của Eagle` — bấm nút chọn để xem toàn bộ 75 biểu tượng có sẵn trong `radio.txd` mà không cần sửa file TXD.
   - **Chế độ 3:** `🖼️ Tải ảnh PNG/JPG riêng` — chọn bất kỳ file ảnh nào trên máy, tool tự động chuẩn hóa về `256×256` 32-bit BGRA cho game.
3. **Thêm bài hát vào Playlist:**
   - **Cách 1 (Khuyến nghị):** Bấm **`📂 Chọn File Nhạc Từ Máy (Windows Explorer)`** để chọn nhiều file `MP3, WAV, OGG, FLAC, M4A, AAC, OPUS` trực tiếp tại vị trí gốc trên ổ đĩa (không sao chép trùng lặp).
   - **Cách 2:** Kéo và thả các file nhạc từ Windows Explorer thẳng vào khung nét đứt trong giao diện.
4. **Chỉnh sửa, sắp xếp & nghe thử:**
   - Kéo-thả các dòng trong bảng (hoặc bấm nút `↑` / `↓`) để đổi thứ tự phát.
   - Sửa trực tiếp **Tên Bài Hiển Thị** và **Nghệ Sĩ** ngay trên bảng.
   - Bấm **`▶️`** ở từng bài để nghe thử bài gốc, hoặc bấm **`▶️ Nghe Thử Luồng Đã Build`** để nghe toàn bộ chương trình phát sóng của kênh và nhấp vào từng mốc bài (Chapter Pills) ở thanh dưới cùng để tua nhanh.
   - Nếu một file nhạc nguồn bị di chuyển hoặc đổi tên trên ổ đĩa, dòng đó sẽ báo `❌ Mất file nguồn` kèm nút **`🔗 Chọn lại file (Relink)`** để bạn trỏ lại đường dẫn mới.

---

## 4. Chọn Vùng Phát Sóng: Kênh Chung & Kênh Đặc Thù Vùng (Tab 2)

Chuyển sang **Tab 2 (`🗺️ Phân Bổ Vùng & Lineup`)**:
1. **Tùy chọn vùng San Andreas (`Region 2`):**
   - Bật công tắc **`Bật RadioEx Custom tại San Andreas (Region 2)`** nếu bạn muốn nghe các kênh custom ngay khi lái xe tại **Los Santos, San Fierro, Las Venturas**.
   - Nếu tắt công tắc này, vùng San Andreas sẽ giữ nguyên 11 đài gốc của GTA San Andreas, còn 7 bang mới của Project Eagle (`Liberty City`, `Vice City / Leonida`, `Praire / Carcer & Windy Bay`, `Cheyenne`, `Cordillera`, `Anneland`, `Neijas`) vẫn phát các kênh custom bình thường.
2. **Góc nhìn 1 (Ma trận Kênh ↔ Vùng):**
   - Tích chọn các ô vuông để gán một kênh vào **nhiều vùng dùng chung** (ví dụ kênh Anime/J-Pop phát ở mọi vùng) hoặc **chỉ một vài vùng đặc thù** (ví dụ kênh City Pop chỉ phát ở Vice City/Leonida, kênh OST chỉ phát ở Liberty City).
3. **Góc nhìn 2 (Thứ tự kênh trong từng vùng & Sơ đồ tọa độ):**
   - Nhấp vào một vùng trên sơ đồ bản đồ (hoặc thẻ vùng) để xem danh sách kênh của vùng đó.
   - Dùng nút `⬆️ Lên` / `⬇️ Xuống` để chỉnh thứ tự xuất hiện của các kênh custom trong vùng đó, và chọn đặt các kênh custom ở **Đầu danh sách** hay **Cuối danh sách** (sau các kênh baseline của Eagle).

---

## 5. Build, Xem Trước Thay Đổi (Diff) & Cài Vào Game (Tab 3)

1. **Bước 1 — Build Radio (`⚡ Build Tất Cả Kênh Đang Bật`):**
   - Tool kiểm tra toàn bộ file nhạc nguồn, chuẩn hóa âm lượng và đóng gói từng kênh thành 1 file `.OGG` trong bộ nhớ đệm.
   - **Cơ chế Cache thông minh:** Những kênh không thay đổi playlist sẽ báo `Cache Hit` tức thì (< 0.05 giây), không phải chờ biên dịch lại.
2. **Bước 2 — Kiểm tra Staging & Cài đặt (`🚀 Cài Đặt Vào Target Đang Chọn (Apply)`):**
   - Xem bảng so sánh **Diff trực tiếp** của `data\radio.dat` và `S&S\ZON\radio.zon` trước khi cài.
   - Đảm bảo game đang đóng (`🟢 Game đang đóng`).
   - Bấm **`🚀 Cài Đặt Vào Target Đang Chọn (Apply)`**. Tool sẽ tự động tạo một bản sao lưu (Backup) ngay trước khi ghi file, sau đó cập nhật `AUDIO\PE\RADIO\CUSTOM\*.OGG`, `models\txd\radio.txd`, `S&S\ZON\radio.zon`, `audio\pe\radio\static.mp3` và `data\radio.dat`.
   - Mở game, lên xe ô tô/xe máy và lăn chuột chuyển đài để thưởng thức!

---

## 6. Khôi Phục Nguyên Trạng (Restore / Rollback)

Ở cuối **Tab 3 (`🛡️ Trung Tâm Sao Lưu & Phục Hồi`)**:
- **Cách 1 — Khôi phục theo bản sao lưu (`⏪ Khôi Phục Bản Sao Lưu Gần Nhất`):** Đưa toàn bộ `data\radio.dat`, `S&S\ZON\radio.zon`, `PECore.ini`, `models\txd\radio.txd` về đúng 100% mã băm SHA-256 trước khi cài và dọn sạch các file âm thanh custom.
- **Cách 2 — Gỡ riêng các kênh của Tool (`🧹 Gỡ Riêng Kênh Của Tool`):** Chỉ xóa các dòng kênh do Eagle Radio Studio thêm vào và file `.OGG` trong `AUDIO\PE\RADIO\CUSTOM\`, giữ nguyên mọi chỉnh sửa thủ công khác trong `data\radio.dat`.
