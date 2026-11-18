# Merge Project Wibu vào gameplay-lab — 22/10/2026

> **Cập nhật sau merge:** clean và Library đã chuyển vật lý sang D, giữ junction tại các đường C cũ. Công cụ/metadata build đã chuyển sang lab; các đoạn nói công cụ còn nhắm clean bên dưới mô tả thời điểm merge. Xem [bàn giao chuyển ổ và đổi đích build](storage-migration-and-lab-handover-2026-10-22.md) để biết trạng thái hiện tại.

**Đã merge và kiểm tra file thành công lúc 05:59:14 22/10/2026 (Asia/Saigon).** Bản chơi hợp nhất ở `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`. Khởi động bằng [Start_Eagle_Lab_With_Sidecar.bat](../../Project%20Eagle/gta%20sa%20gameplay-lab/Start_Eagle_Lab_With_Sidecar.bat).

Nguồn là `Project Eagle\gta sa clean\gta sa clean`. Người dùng xác nhận loading screen, main menu, Aether và NPC đã hoàn tất khi yêu cầu merge. Agent kiểm tra file/binary sau tích hợp; **chưa mở hoặc kiểm thử bản hợp nhất trong game**.

## Nội dung đã đưa vào lab

| Thành phần | Thay đổi |
| --- | --- |
| Startup/loading Wibu World | Thay `PECore.asi`; thêm `modloader/WibuWorldLoading/txd/loadscs.txd`; thay `modloader/modloader.img` có Aether và loading TXD |
| Main menu | Đủ 32 file từ bản đang cài: `WibuMenu.asi`, INI hiện tại, 23 cover, logo, 5 MP3 và DLL audio riêng |
| State menu | Tạo lại `.wibu-menu-install-state.json` với `game_root` trỏ lab và hash thực tế; không mang đường dẫn ownership clean sang lab |
| NPC | Thay `S&S/Cdimages/default/COMPONENTPEDS.img`: 444.977.152 → 12.782.344.192 byte; giữ nguyên 1.638 mapping của build đã áp dụng |
| Aether/radio | Cặp Aether ngoài archive và toàn bộ radio hiện có đã khớp nguồn; giữ file lab. Aether trong `modloader.img` được đối chiếu payload trực tiếp |

Tổng cộng **37 file**: 36 file nội dung và 1 state được tạo cho lab; thay 3 file hiện có, thêm 34 file. NPC là bản sao độc lập, mỗi archive có link count 1. Bản nguồn giữ nguyên. Không chép secrets hoặc log runtime từ nguồn.

## Kiểm chứng

- SHA-256 của đủ 37 file đã cài khớp transaction. Archive NPC khớp build sửa rig mới nhất: `9bf8f76c59167c3664f187083d2b951213bf69ce7dc6f242c7706dbdefbf37e2`.
- Đọc trực tiếp 7 DFF đã sửa trong IMG: hash payload khớp candidate; HAnim/Skin 32/32, phiên bản RW 3.6.0.3. Kiểm bảng IMG 4.224 member và đủ 3 member `aether.dff`, `aether.txd`, `loadscs.txd` của ModLoader.
- Kiểm toàn bộ điều kiện nhận diện executable/hook/helper/menu table mà WibuMenu dùng với **cả hai executable của lab**. Không dùng hash exe clean để đánh giá exe lab đã có patch.
- `.text` và `.data` của PECore mới bằng bản lab cũ; RVA `0xD0743` vẫn có chữ ký `8B 81 8C 05 00 00` cho patch RAM GPS của Sidecar.
- **2.789 file lab ngoài phạm vi merge giữ nguyên SHA-256**, gồm executable/pathfinding, CLEO+, Sidecar/EaglePhone/state, HUD, loader, mod Nhóm A/B1/B3, map fixes và radio. Đủ **10 junction** giữ nguyên đích.
- Metadata nguồn và hash toàn bộ nội dung được chép giữ nguyên. **5 file save/settings dùng chung** giữ nguyên hash; có snapshot riêng trên D.
- Rollback preflight đạt: đủ backup cũ và hash tương ứng. Chưa chạy rollback sau lần merge thành công.

File nguồn không bật thuộc tính chỉ đọc. Lỗi `WinError 5` lúc commit đầu tiên được tái hiện trên file thử: parser PE giữ file-backed mmap nên Windows chặn rename. Công cụ đã chuyển sang parse PECore từ bytes trong RAM, dọn đúng restore temp đã kiểm hash và tiếp tục transaction. Lần hoàn tất qua toàn bộ kiểm tra nêu trên.

## Bảo toàn và phục hồi

Backup: `D:\GTA Archive\Project Eagle Merges\clean-to-lab-2026-10-22`.

- `files/`: PECore, modloader IMG và COMPONENTPEDS trước merge, đủ hash trong transaction.
- `shared-save-snapshot/`: save/settings chụp trước merge. Rollback nội dung không tự khôi phục snapshot save.
- `transaction.json` và `preparation.json`: đường dẫn, allowlist, hash trước/sau và trạng thái.

Thoát game và Sidecar trước khi phục hồi. Tại staging có [Check_Rollback.bat](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/Check_Rollback.bat) để kiểm tra, [Rollback_Merge.bat](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/Rollback_Merge.bat) để thực hiện. Rollback chỉ xử lý 37 đường dẫn đã ghi; giữ file ngoài gói, chặn tài nguyên đã bị sửa khác hash và lưu INI menu mới nhất trước khi gỡ. Có thể gọi trực tiếp:

```powershell
C:\Python310\python.exe -X utf8 .\staging\project-eagle\merge-clean-to-lab-2026-10-22\merge_game.py rollback-preflight
C:\Python310\python.exe -X utf8 .\staging\project-eagle\merge-clean-to-lab-2026-10-22\merge_game.py rollback
```

C sau merge còn khoảng 2.93 GiB trống tại thời điểm kiểm tra; backup cũ đặt ở D. Không đổi tên hoặc di chuyển thư mục lab.

## Trạng thái bàn giao

Báo cáo [gameplay-lab-current-status-2026-10-22.md](gameplay-lab-current-status-2026-10-22.md) là snapshot trước merge lúc 04:20. Điều kiện chờ sửa RW/rig ở đó đã được xử lý trong bản nguồn hiện tại. Main menu là thành phần bổ sung mới ngoài danh sách copy của snapshot đó. Số file cũ đếm theo junction không dùng để xác định phạm vi merge này.

Các installer/rollback riêng của main menu/loading và deployment của Skin Viewer trước đây vẫn nhắm bản clean. **Chưa đổi đích các công cụ đó sang lab**; dùng transaction merge này để phục hồi lần tích hợp lab. Radio Studio đã có các target riêng; không đổi cấu hình công cụ trong lượt này.

Bản hợp nhất cần một lượt thử thực tế: mở launcher, xem splash/loading/menu và nhạc, load save hoặc New Game, chọn Aether bằng F2, quan sát NPC, thử phone/GG Map và radio. Việc Waypoint/ENEX và stress-test B3 còn chờ nghiệm thu trong snapshot lab không được coi là đã nghiệm thu chỉ vì đã merge.

## Bằng chứng

- [Transaction](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/transaction.json)
- [Kết quả kiểm sau merge](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/verification.json)
- [Save, tính độc lập archive và disk](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/supplemental-verification.json)
- [Preflight binary/assets](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/preflight.json)
- [Audit trước merge](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/audit/merge-audit.md)
- [Script merge/rollback](../../staging/project-eagle/merge-clean-to-lab-2026-10-22/merge_game.py)
