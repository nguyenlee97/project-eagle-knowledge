# Wibu World menu — kết quả cài đặt 22/10/2026

**23/10: Random nhạc mỗi lần khởi động đã cài và bật.** Playlist 7 bài giữ nguyên; checkbox ở Radio Studio > Menu Music. [Trạng thái và bằng chứng mới nhất](random-music-2026-10-23.md).

**23/10: Menu Music Studio đã cài vào gameplay-lab và lưu 7 bài người dùng chọn.** Tab Radio Studio sửa playlist/bài mở đầu, tự chuyển M4A/FLAC sang MP3 và plugin lưu F3/F4 qua lần mở sau. Xem [hướng dẫn/bàn giao hiện tại](menu-music-studio-2026-10-23.md). Không áp lại các đường clean lịch sử bên dưới.

**Bàn giao sau merge:** bộ 32 file menu hiện tại đã được đưa vào gameplay-lab cùng loading/NPC và có state riêng trỏ đúng lab. Xem [báo cáo tích hợp và rollback lab](../merge-clean-to-gameplay-lab-2026-10-22.md). Các script cài/rollback menu riêng bên dưới vẫn nhắm bản clean; lịch sử kiểm thử dưới đây mô tả từng lần cài nguồn.

**Cập nhật sau khi người dùng thử:** bản sửa UV cho nền/logo/portrait, thêm nền trang con và âm thanh riêng cho main menu đã được cài ngày 22/10/2026. Đã đối chiếu 32/32 file, giữ nguyên config người dùng và 74 file được bảo vệ. Chờ người dùng thử lại trong GTA. Xem [render-audio-fix.md](render-audio-fix.md) để biết trạng thái hiện tại. Phần bên dưới ghi lại lần cài đầu.

Đã cài vào **Project Eagle chính**:
`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`.
Không cài vào gameplay-lab. Người dùng tự thử trong game; chưa có xác nhận runtime.

## Tính năng trong bản này

- 23 background riêng cho toàn bộ danh sách nhân vật nữ đã chọn, phong cách anime 2D và trang phục đô thị. Dừng tạo thêm artwork sau đợt này.
- Logo Wibu World trắng đen, giữ đúng tỷ lệ. Background ở menu chính; portrait nhân vật đang chọn ở menu pause.
- Chọn nhân vật, lưu yêu thích, hoặc ngẫu nhiên mỗi lần khởi động. Mặc định ngẫu nhiên; Hu Tao là favorite ban đầu.
- Lời chào dạng chữ khi vào menu chính.
- Năm MP3 Genshin có sẵn từ ổ D, âm lượng riêng mặc định 25%. Bản đầu là A Day in Mondstadt. Nhạc riêng dừng khi rời màn menu được hỗ trợ.
- Giữ các thao tác Play/Load/Options của menu game. Bảng chọn riêng chỉ mở ở menu chính; pause hiển thị portrait. Map và trang settings dùng giao diện hiện có.

## Phím sử dụng

Ở menu chính, nhấn **F6** mở bảng chọn. Các phím sau dùng khi bảng đang mở:

| Phím | Thao tác |
| --- | --- |
| F7 / F8 | Nhân vật trước / sau |
| F9 | Lưu nhân vật hiện tại làm yêu thích |
| F10 | Đổi chế độ random / favorite; trạng thái hiển thị trên bảng |
| F3 / F4 | Bản nhạc trước / sau |
| F11 | Tắt / bật tiếng |
| + / - | Tăng / giảm âm lượng |
| F6 | Đóng bảng để tiếp tục dùng Play/Load/Options |

Muốn lần sau luôn hiện một waifu: chọn bằng F7/F8, F9 lưu, rồi dùng F10 để chuyển về **Mode: favorite**.
Favorite, mode, mute và volume lưu tại `plugins\wibu-menu\wibu-menu.ini`.
Track được đổi trong phiên chơi; lần khởi động sau bắt đầu lại từ track0.

## Kiểm tra đã hoàn tất

Plugin x86 biên dịch thành công; kiểm tra tĩnh với cả hai executable và dependency của bản Eagle hiện tại đều đạt. TXD đã được parse/giải mã độc lập; đủ 23 cover, logo alpha chính xác, UV portrait được xem lại, không có lỗi đóng gói. Gallery tại `staging\project-eagle\wibu-menu\qa\gallery.html` là ảnh giải mã tài nguyên, không phải screenshot trong GTA.

Cài đặt đủ **31 file**, kiểm tra lại **31/31 SHA-256 khớp**. Snapshot của **74 file được bảo vệ** không đổi, gồm core/ASI/config hiện có, loading và radio trong phạm vi ghi nhận. Không thay executable, loader config, skin hay radio. ASI được cài thêm: `WibuMenu.asi`; dữ liệu riêng: `plugins\wibu-menu`.

ASI SHA-256: `7fa4b33ddd6204df35c576ef43521b627c231cadaa1eb61a66087a196256f834`.

Lịch sử/manifest phục hồi:
`backups\project-eagle\wibu-menu-installs\install-20261022-045110-497`.
Đây là lần cài đầu, các đường dẫn mới trước đó chưa có; không có file menu cũ bị ghi đè.
Chứng cứ: `install-report.json` trong thư mục lịch sử và
`staging\project-eagle\wibu-menu\qa\live-files-verification.json`.

## Phần người dùng tự thử

Chưa mở game tự động. Cần quan sát nền/logo, F6 và chọn favorite, việc giữ lựa chọn sau mở lại, portrait khi pause, nhạc và chuyển từ menu vào gameplay, cùng menu map/options hiện có. Độ ổn định và phối hợp thực tế với các plugin Eagle chưa được xác nhận bằng runtime; kiểm tra tĩnh không thay thế bước này.

Khi cần gỡ, thoát game rồi chạy từ workspace GTA:

```powershell
& .\staging\project-eagle\wibu-menu\scripts\rollback_menu.ps1
```

Rollback preflight đã đạt. Lệnh gỡ chỉ xử lý file có ownership; giữ file ngoài gói hoặc file tài nguyên đã bị thay đổi, sao lưu config mới nhất trước khi gỡ. Chi tiết tại `installation.md`.
