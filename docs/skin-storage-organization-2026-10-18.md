# Tổ chức kho skin và backup Project Eagle — 18/10/2026

Hoàn tất lúc 2026-10-18T03:09:44.923133+07:00. Bản chính và bản backup đã được đối chiếu SHA-256. Không cài skin hay sửa thư mục game.

## Vị trí và tính toàn vẹn

- Kho chính: `C:\Users\LENOVO\Desktop\GTA\Skin Library\Project Eagle`.
- Backup chính: `D:\Skin Backup\Project Eagle-2026-10-18\Project Eagle`.
- Số file đã xác minh, kể cả manifest: **9,177**.
- Dung lượng logic kho chính: **20.17 GB (18.79 GiB)**.
- Tất cả 9,167 file trong manifest cũ đã được đọc và so hash C/D sau khi Windows sửa ổ. Metadata thêm/sửa sau đó được hash và đối chiếu riêng; manifest được xác minh riêng để tránh tự tham chiếu.
- Lượt kiểm tra đã giữ 9,010 bản D đúng hash và chép bù/thay 157 file (0.51 GB (0.48 GiB)). Các bản D cũ bị thay được giữ ở `D:\Skin Backup\Project Eagle-2026-10-18\replaced-after-repair-2026-10-18`, ngoài backup chính.
- HealthStatus sau kiểm tra: `Healthy`; OperationalStatus: `OK`; số lỗi NTFS/I/O mới liên quan D trong lượt này: **0**.
- File bổ sung ngoài manifest trong backup chính: 0. Những file ngoài manifest không được tự xóa.

SHA-256 manifest hiện tại: `4f5f737edd287d71df24b99757df1a6b6621ee96ad79d98adef1c4c3851ae2ff`.

## Giải thích chênh lệch khoảng 4,9 GB và hơn 20 GB

Con số report cũ là tổng archive trong sổ nguồn, không phải dung lượng toàn bộ workspace. Kiểm kê trực tiếp staging trước khi gom:

| Thành phần | Dung lượng logic |
|---|---:|
| Toàn bộ ZIP/RAR/7z có trên đĩa, gồm bản phụ/nested archive | 5.14 GB (4.79 GiB) |
| DFF/TXD đã giải nén để kiểm tra | 14.80 GB (13.78 GiB) |
| Metadata, report và phần khác | 0.05 GB (0.04 GiB) |
| **Tổng staging trước khi gom** | **19.99 GB (18.61 GiB)** |

Kho chính hiện còn có 18 archive từ thư mục người dùng chọn, ba archive chưa phân loại và các bản metadata/manifest phục hồi. Archive gốc và DFF/TXD giải nén có mục đích khác nhau, nên giữ cả hai không đồng nghĩa hai bản byte-identical. Dung lượng pair DFF+TXD trong report cũng có thể tính TXD dùng chung cho từng biến thể; không cộng nó lần nữa vào dung lượng folder.

## File đã gom và bản trùng đã bỏ

- Đã bỏ **753 bản sao trong Downloads**, tương ứng **3.51 GB (3.27 GiB)** dung lượng logic. Mỗi file chỉ được bỏ sau khi bản chính C và backup D đều khớp cùng SHA-256.
- Phân loại thao tác: {"downloads-exact-hash-duplicate": 442, "supplemental-exact-known-skin-duplicate": 297, "renamed-exact-known-skin-duplicate": 14}.
- Ba archive chưa phân loại đã được chuyển vào `user-downloaded-unreviewed` ở lượt trước; chúng được giữ nguyên và không tự đưa vào pool/đổi rating.
- 72 archive còn lại trong Downloads không khớp hash kho skin và metadata không xác định chúng là archive DFF/TXD thuần; giữ nguyên. Không xóa partial `.crdownload`, cache hệ thống hoặc file ngoài danh sách.
- Thư mục role-pool cũ trong Downloads được thay bằng junction tới kho chính; nội dung, nguồn gốc, rating và các mục giữ lại vẫn được bảo quản.

Dung lượng trống C ngay trước/sau bước gom bản trùng: **12.79 GB (11.91 GiB) → 16.24 GB (15.13 GiB)**. Thay đổi quan sát được là 3.45 GB (3.21 GiB); đây là số đo volume, có thể chịu ảnh hưởng tác vụ nền Windows. Tổng byte các bản sao đã bỏ ở trên là số đo theo nhật ký file.

## Các phần dung lượng khác đã đo, không tự dọn

| Thư mục | Dung lượng logic |
|---|---:|
| `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean` | 12.83 GB (11.94 GiB) |
| `C:\Users\LENOVO\AppData\Local\Temp` | 1.25 GB (1.16 GiB) |
| `C:\Users\LENOVO\AppData\Roaming\Codex\web` | 1.03 GB (0.96 GiB) |
| `C:\Users\LENOVO\.codex\cache` | 0.06 GB (0.06 GiB) |
| `C:\Users\LENOVO\AppData\Local\Codex` | 0.11 GB (0.10 GiB) |

Đây là tổng độ dài file, bỏ qua reparse point; không phải đo từng cluster vật lý. Có một mục Temp không đọc được, nên tổng Temp có thể thấp hơn thực tế một chút. Game đã cài được đo riêng và không được gom vào backup skin.

## Đường dẫn tương thích và chứng cứ

- `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\skin-downloads-2026-10-15` là junction tới `download-run-2026-10-15` trong kho chính, không chứa thêm một bản 20 GB.
- `C:\Users\LENOVO\Downloads\prosititute skin` là junction tới `user-selected\prosititute skin` trong kho chính.
- [Report skin cũ vẫn hoạt động](http://127.0.0.1:8942/skin-downloads-2026-10-15/download-report.html).
- [Xác minh backup cuối](evidence/skin-storage-final-verification-2026-10-18.json).
- [Xác minh đầy đủ sau sửa ổ](evidence/skin-storage-backup-verification-after-repair-2026-10-18.json).
- [Nhật ký gom bản trùng](evidence/skin-storage-duplicate-consolidation-journal-2026-10-18.jsonl).

Các lỗi Ntfs 55 và disk 153 trước đó thuộc giai đoạn trước khi người dùng sửa ổ. Trong lượt hiện tại, file nguồn C được kiểm tra với manifest gốc trước khi chép; các bản D cũ không khớp đã được thay bằng temp-file, flush, kiểm tra hash rồi đọc lại. Không suy diễn rằng một skin ZIP lỗi có thể giải thích toàn bộ lỗi filesystem/I/O cũ, cũng không kết luận ổ bị hỏng vật lý chỉ từ nhật ký đó.
