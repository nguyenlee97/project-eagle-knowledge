# Eagle Radio Studio — Tài Liệu Bàn Giao Toàn Diện

- **Ngày bàn giao:** 14/10/2026
- **Mã nguồn & Ứng dụng:** [`C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio`](file:///C:/Users/LENOVO/Desktop/GTA/tools/eagle-radio-studio)
- **Launcher khởi động nhanh (Nhấp đúp chuột):** [`C:\Users\LENOVO\Desktop\GTA\Start_Eagle_Radio_Studio.bat`](file:///C:/Users/LENOVO/Desktop/GTA/Start_Eagle_Radio_Studio.bat)
- **Giao diện Web cục bộ:** `http://127.0.0.1:8790`

---

## Mục Lục Bộ Tài Liệu (`docs\project-eagle\radio-studio\`)

1. **[`01-radioex-discovery-and-regions.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/radio-studio/01-radioex-discovery-and-regions.md)**
   - Báo cáo giải phẫu nhị phân `PECore.asi` (`RadioEx` & `ZoneEx`), `bass.dll` v2.4.17 và `models\txd\radio.txd` với địa chỉ VA/RVA cụ thể cho cả 8 câu hỏi Discovery.
   - Chứng minh cơ chế ưu tiên `ZoneEx::GetRadioRegion` (`0x1012F1C0`) trước kiểm tra `inSA` (`0x100F77A2..0x100F7826`), mở khóa khả năng phát Radio custom ngay tại **San Andreas (`Region=2`)** bên cạnh 7 bang mới của Project Eagle.
2. **[`02-architecture-and-schema.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/radio-studio/02-architecture-and-schema.md)**
   - Kiến trúc hệ thống 2 lớp (Project Multi-Track Playlist $\rightarrow$ Compiled OGG Stream + Track Offset Manifest).
   - Sơ đồ thư mục, dependencies (`Python 3.10`, `FFmpeg`, `Win32 ctypes`), và JSON Schema cho `project.json`, `build_state.json`, `installed_<target>.json`, `backup_manifest.json`.
3. **[`03-user-guide.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/radio-studio/03-user-guide.md)**
   - Hướng dẫn sử dụng hằng ngày bằng Tiếng Việt: Chọn Target (`Lab` vs `Main`) $\rightarrow$ Tạo Kênh & Chọn Logo HUD $\rightarrow$ Thêm nhạc (`MP3/WAV/OGG/FLAC`) & Sắp xếp $\rightarrow$ Gán vùng chung/riêng $\rightarrow$ Build & Apply $\rightarrow$ Khôi phục (Restore/Rollback).
4. **[`04-verification-and-recovery-report.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/radio-studio/04-verification-and-recovery-report.md)**
   - Kết quả kiểm thử tự động End-to-End, kiểm thử các kịch bản lỗi (Failure Modes), danh sách file thay đổi, mã băm SHA-256 đối chiếu trước/sau khi Restore trên `gta sa gameplay-lab`, và hướng dẫn nghiệm thu trực tiếp trong game.
