# Mục mở đầu: hai clip gốc → Project Wibu

**Cập nhật03/11:** Hai clip0.2s bên dưới hiện được giữ trên đĩa nhưng đã có runtime startup-state bypass03/11; không dùng lại transaction cũ để chữa flash. [Bàn giao mới](menu-autonext-no-intros-2026-11-03.md).

**Đã cài vào gameplay-lab ngày 01/11/2026, chờ người dùng thử và báo pass.** Theo yêu cầu xử lý từng hạng mục, chưa sửa ảnh Barbara hoặc generate các artwork/batch tiếp theo. Toàn bộ hàng đợi và yêu cầu reference được giữ trong [phiếu công việc](../work-items/2026-11-01-codex-wibu-startup-intros.md).

## Thay đổi

Hai video mở đầu ở `movies/Logo.mpg` và `movies/GTAtitles.mpg` được thay bằng hai đoạn khoảng **0,2 giây**, chỉ hiện logo Hu Tao **Project Wibu trắng/đen** đã duyệt, không nhạc. Mỗi clip có 5 frame, MPEG-1 video + MP2 audio im lặng, 1920×1080. Nội dung hiển thị được lấy từ `project-wibu-startup-640.png` đã dùng trước đây; không generate artwork mới.

Đây là phương án thay clip cực ngắn để giữ đường kết thúc video tự nhiên, **không phải vá engine để loại bỏ hoàn toàn bước video**. Thời lượng đọc từ file là 0,190911 giây mỗi clip, tổng khoảng 0,38 giây; chưa đo thời gian mở thực tế/khởi tạo DirectShow.

Không chỉ xóa/đổi tên hai file: kiểm mã máy xác nhận lỗi mở video vẫn đưa game vào trạng thái đang phát và không có completion event để tự chuyển tiếp. Tùy chọn SilentPatch hiện bật chỉ bỏ EAX/NVIDIA. Bằng chứng callsite/state trong [audit riêng](intro-skip-audit-2026-11-01.md), đối chiếu [startup state machine](https://github.com/gta-reversed/gta-reversed/blob/master/source/app/platform/win/WinMain.cpp). Clip hợp lệ là phương án được chọn trong phạm vi người dùng cho phép thay clip hoặc bỏ intro; không sửa executable/core hoặc thêm ASI.

## Kiểm tra và giới hạn

- Đủ 2 file live khớp SHA-256 candidate; đủ 2 backup gốc khớp SHA-256 trước sửa.
- ffprobe xác nhận format, codec, kích thước, thời lượng và 5 frame; FFmpeg giải mã clip đầy đủ không lỗi. Frame đã được xem lại.
- **7 kiểm thử transaction trên thư mục giả đạt**: prepare không ghi game, apply/restore, backup hash, game đang chạy, lock đang giữ, stale movie/protected hash và rollback khi lỗi giữa chừng.
- **8 file được bảo vệ giữ nguyên hash**, gồm hai exe, PECore, SilentPatch config, launcher, WibuMenu, INI menu music và loading TXD đang cài.
- Có khóa ghi chung lúc apply, đã trả khóa. Không mở GTA/Sidecar, chưa xác nhận DirectShow thực tế hoặc chuỗi khởi động bằng runtime; người dùng tự thử.

Target: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
Staging/transaction: `staging/project-eagle/startup-intros-20261101/transaction.json` (`installed`).
Backup hai file gốc: `staging/project-eagle/startup-intros-20261101/backup/`.
Hậu kiểm: `staging/project-eagle/startup-intros-20261101/qa/verification.json`.
Frame xem trước: `staging/project-eagle/startup-intros-20261101/qa/intro-frame.png`.

## Phục hồi riêng hai clip

Thoát GTA rồi chạy từ workspace GTA:

```powershell
C:\Python310\python.exe staging\project-eagle\startup-intros-20261101\manage_intro.py restore
```

Lệnh nhận khóa ghi chung, kiểm đúng target, hash clip hiện tại và backup; chỉ phục hồi hai đường dẫn đã ghi. Nếu clip bị thay ngoài transaction thì từ chối ghi đè. Không dùng rollback clean/merge/loading cho thay đổi này.

## Bước tiếp theo

Người dùng mở launcher lab thông thường, kiểm rằng không còn nội dung hai clip gốc và game đi tiếp qua Project Wibu/loading/menu mà không phải bấm phím bỏ video. Dừng ở đây đợi **pass**; sau đó mới sửa loading Barbara ba tay. Chưa bắt đầu roster/reference/batch generation.
