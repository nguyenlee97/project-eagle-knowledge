# Dịch chuyển giữa các thành phố trong Eagle

Kiểm tra cấu hình/script cục bộ ngày 13/10/2026; không sửa game và chưa thử thao tác trực tiếp trong game.

## Đi tới Los Santos để thử NPC

1. Đứng ngoài trời và xuống xe.
2. Nhấn **Ctrl trái + K** để mở **Teleporter**. `MapTeleporter.ini` hiện đặt Type=1, Keybind1=162, Keybind2=75.
3. Chọn **Custom Teleport Locations → Custom Teleport Location #4 → Load Location in this Slot**.
4. Dùng phím mũi tên để chọn dòng; xác nhận bằng **phím Sprint (chạy nhanh)** của game. **Backspace** để quay lại.

Slot #4 hiện lưu `(1795.89, -2140.71, 13.5469)`. Điểm này nằm trong hộp vùng Los Santos LA01 của `S&S/ZON/map.zon:14`; không phải điểm được thêm bởi lượt cài NPC. Script đọc tọa độ từ slot và chuyển actor tới đó. Vị trí mặt đất/hiệu quả trong game chưa được thử trực tiếp.

Đường **Load Location** dùng điểm đã lưu. Mục **Save Location in this Slot** sẽ ghi vị trí hiện tại vào slot, nên đó là thao tác khác với đi tới điểm có sẵn.

Script xác nhận menu bằng `is_button_pressed ... 16`, tương ứng hành động Sprint trong SA, không phải keybind Enter của RZL. [Tài liệu Button IDs của Sanny Builder](https://docs.sannybuilder.com/scm-documentation/sa/buttons).

## Đi tới thành phố khác

Ở menu Teleporter chính, chọn **Main World**, sau đó chọn tên nơi đến. FXT cục bộ có các mục Rose City, các phần Liberty City, Vice City, Bullworth, Carcer City và các điểm khác; có các dòng chuyển trang. Los Santos không có mục mang tên riêng trong danh sách Main World hiện tại, nên dùng slot #4 ở trên cho lượt thử.

## Nguồn cục bộ

- `cleo/MapTeleporter.ini:7,13-14,42-47`: chế độ/phím mở và điểm slot #4.
- `cleo/MapTeleporter.txt`: script dạng text đi kèm; menu slot #4 tại label Noname_1851, đọc/load tại Noname_3603.
- `cleo/cleo_text/MapTeleporter.fxt:31-32,66-74`: nhãn Main World, Custom Teleport Locations và Load.
- `cleo.log`: phiên log lưu sẵn có bản ghi nạp MapTeleporter.cs và FXT; không phải kiểm chứng thao tác teleport trong lượt này.

Nếu Ctrl trái + K không mở menu, cần đối chiếu script được nạp trong phiên game hiện tại; không dùng lệnh cheat TELEPORTER như một fallback được bảo đảm vì config đang chọn chế độ phím custom.
