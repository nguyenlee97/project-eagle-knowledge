# Bản sửa nền/portrait và nhạc main menu — 22/10/2026

**Trạng thái: đã cài sau khi người dùng xác nhận thoát game, ngày 22/10/2026.** Đúng thư mục Project Eagle chính. Chưa thử lại trong GTA; người dùng tự kiểm tra. Không mở/điều khiển game tự động.

## Lỗi đã được người dùng thấy

Người dùng gửi screenshot main menu với nền và logo bị kéo chéo, trang Start Game/New/Load/Delete vẫn dùng nền cũ, và portrait pause bị biến dạng tương tự. Nhạc nghe được trong pause nhưng không phát lúc mở main menu lần đầu.

## Thay đổi trong bản sửa

- Gom vẽ nền, logo, portrait qua `DrawSpriteRegion`. Hàm GTA nhận UV theo **TL, TR, BL, BR**, trong khi bản cũ truyền **TL, TR, BR, BL**. Hai góc dưới bị đổi chỗ, làm ảnh bị gập chéo. Không đổi artwork hay nén lại TXD.
- Nền pregame phủ thêm trang Start Game, New/Load/Delete/save, options/audio/display/controls thông thường và quit confirmation. Dùng danh sách page cụ thể; giữ đường map và special control binding riêng. Pause vẫn có portrait và điều hướng native.
- Dời logo xuống góc trái dưới ở menu chính để tránh tiêu đề native. Ẩn logo khi bảng F6 mở. Giữ đúng tỷ lệ 4:3.
- Nhạc theo toàn bộ phiên menu, gồm main menu và các trang con; dừng khi menu đóng để vào gameplay. Có thử lại mỗi ba giây nếu khởi tạo/phát thất bại.
- Menu dùng bản sao byte-identical của BASS đang có tại `plugins\wibu-menu\audio-runtime\wibu-bass.dll`, nạp bằng đường dẫn đầy đủ, xác nhận module khác thư viện gốc, rồi tự khởi tạo output trước khi mở MP3. Không gọi Init/Free hoặc chỉnh volume chung qua BASS của Eagle. Module/output riêng được giữ đến lúc tiến trình kết thúc; chỉ stream của menu bị dừng/giải phóng khi rời menu.
- Có log chẩn đoán tại `plugins\wibu-menu\wibu-menu.log`, gồm kết quả khởi tạo, phát nhạc và mã lỗi BASS khi cần. Log được tạo trong lần chạy bản sửa, không phải lúc chuẩn bị.
- Updater nhận diện được install-state bản đầu 31 file, thêm runtime thành 32 file; giữ favorite/mode/volume INI đang dùng khi update. Backup các file đang có trước khi thay.

## Kiểm tra

Build x86 và static verifier đều đạt với hai executable Eagle. Gói staging đủ **32/32 file** và manifest hash hoàn chỉnh.

Probe `qa/uv-native-probe.py` phân tích trực tiếp hàm `0x727A00` trong executable có hash đã xác minh. Nó trích mapping UV thực tế của bốn vertex, rồi dùng bốn tọa độ phân biệt để chứng minh thứ tự mới đúng, còn thứ tự cũ đổi chỗ hai góc dưới. Đây là kiểm tra offline trên mã máy, chưa phải render trong game. Bằng chứng chi tiết tại `uv-page-fix-audit.md`.

Helper x86 trong `qa/audio-isolation/` nạp DLL gốc và bản sao với handle/đường dẫn khác nhau; Init và Free của bản riêng thành công, trạng thái thiết bị của module gốc không đổi. Helper không tạo/phát stream, không tương tác với game. Kết quả tại `qa/audio-isolation/result.json` và `audio-start-fix-audit.md`.

ASI bản sửa: `e88457bba9fe2e71ae361bc99903c9225e2524759f0c6da49457427ef17fb0d6`.
Source: `d3fd80da4c0050acb407de41ed9b17c861534a4963117b55d0867c06ada8d2e3`.
ASI live hiện khớp bản sửa `e88457bba9fe2e71ae361bc99903c9225e2524759f0c6da49457427ef17fb0d6`; runtime riêng đã được cài.

Preflight và cài đặt đã thành công: **32/32 file live khớp SHA-256**, config favorite/mode/volume giữ nguyên byte so với trước update, **74 file được bảo vệ không đổi**. Lịch sử và backup bản trước: `backups\project-eagle\wibu-menu-installs\install-20261022-051017-453`. Báo cáo hậu kiểm: `staging\project-eagle\wibu-menu\qa\live-files-verification.json`.

Vẫn cần người dùng kiểm tra lại hình ảnh, nhạc phát từ main menu, chuyển qua trang con, vào gameplay và pause, cùng radio sau khi cài; chưa có xác nhận runtime cho bản sửa. Nếu còn lỗi nhạc, lần chạy này sẽ ghi kết quả khởi tạo và mã lỗi tại `plugins\wibu-menu\wibu-menu.log`.

Baseline source/ASI/scripts trước sửa nằm tại `staging\project-eagle\wibu-menu\revisions\20261022-before-render-audio-fix`. Lịch sử cài bản đầu và backup live không bị thay.
