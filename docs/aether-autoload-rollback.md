# Gỡ thử nghiệm tự nạp Aether

Ngày: **13/10/2026**. Người dùng báo tự nạp có vẻ không hoạt động, chọn tiếp tục cách F2 và yêu cầu gỡ các thay đổi, kết thúc tác vụ. Không tiếp tục chẩn đoán hoặc triển khai tự nạp.

Đã thực hiện khi Eagle không chạy:

- Gỡ `modloader\Aether-Autoload\cleo\AetherAuto.cs`, `Aether.img`, `enabled.flag` và các thư mục trống của gói.
- Gỡ dòng `IMG modloader\Aether-Autoload\Aether.img`; khôi phục `data\default.dat` byte-for-byte từ backup trước thử nghiệm.
- Giữ nguyên `modloader\RZL-Skin\AETHER.dff` và `AETHER.txd` cho cách chọn **F2 → Player Options → Change Player → ModLoader Actors → AETHER** đã được người dùng thử.

Xác minh: thư mục tự nạp không còn, dòng mount không còn, **12/12 file khớp SHA-256 với baseline trước thử nghiệm tự nạp**: hai executable, player.img, COMPONENTPEDS.img, gta.dat, default.dat, peds.ide, RZL-Trainer.cs/ini, modloader.ini và cặp AETHER của RZL-Skin. Hash của default.dat sau phục hồi là `46893011F9BE62CFB8F75AE5BA677884449D41F69DF501503357C93F4D14852C`.

Chứng cứ máy đọc được: `C:\Users\LENOVO\Desktop\GTA\backups\project-eagle\aether-autoload-20261013\rollback-verification.json`. Backup, staging và ghi chú nghiên cứu được giữ ngoài phần game đang nạp để lưu lịch sử; gói tự nạp không còn hoạt động trong game.

**Tác vụ đã kết thúc.**
