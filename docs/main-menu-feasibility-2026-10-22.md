# Khả năng mod main menu Eagle

Kiểm tra nhanh ngày 22/10/2026. Chỉ đọc game; chưa cài hay sửa tài nguyên.

## Bằng chứng hiện tại

- Game có `models/fronten1.txd`, `fronten2.txd`, `fronten3.txd`, `fronten_pc.txd`.
- `PECore.ini` bật `TransparentMenu = true`; chú thích mô tả main menu trong suốt và cập nhật map. Log hiện tại có mục `TransparentMenu`.
- `plugins/CustomStartScreenByDarkP1xel.asi` có mặt; INI gốc chứa vị trí camera và điểm nhìn XYZ. Có mặt không chứng minh cảnh đang hiển thị.
- `plugins/menupatch.asi` có mặt; chưa xác định chức năng trong kiểm tra nhanh này.
- Khảo sát `loading-screens/README.md` trước đây tách 25 texture frontend khỏi bộ loading; tài nguyên loading đã được thay theo bộ Wibu World. Không dùng việc loading đã thay thành công làm bằng chứng menu cũng hoạt động tương tự.

## Kết luận và cách làm

Main menu SA có thể sửa. Đổi artwork/logo/cursor dùng đường texture TXD tương ứng sau khi xác định asset thật sự được renderer hiện tại sử dụng. Đổi vị trí nút, logic điều hướng, hiệu ứng và hình nền động có thể cần code/plugin frontend; không chỉ thay PNG vào TXD.

Eagle đã có thành phần sửa frontend. Cần quan sát cold start và pause menu, xác định nền đang do PECore/cảnh 3D hay TXD vẽ, rồi chọn một thay đổi pilot trong staging và backup trước khi cài. Chưa khẳng định thay riêng `fronten2.txd` sẽ thay toàn bộ nền menu Eagle; chưa thử tương thích plugin frontend khác.

Nguồn tác giả minh họa đường thay nền SA qua `fronten2.txd`: https://www.gtagarage.com/mods/show.php?id=21763 . Đây là bằng chứng cho SA nói chung, không phải thử nghiệm Eagle.
