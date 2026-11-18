# Radio Studio — đã chuyển backup/cache sang D

Hoàn tất ngày 22/10/2026. Chuyển đúng hai thư mục đã được người dùng duyệt, không sửa game, skin, mapping hoặc candidate IMG.

| Thư mục | File | Đích thật |
|---|---:|---|
| `tools/eagle-radio-studio/data/backups` | 179 | `D:/GTA Archive/Eagle Radio Studio/backups` |
| `tools/eagle-radio-studio/data/cache` | 707 | `D:/GTA Archive/Eagle Radio Studio/cache` |

Tổng 886 file, **14,38695 GiB**. Hai đường dẫn C hiện là NTFS junction tới D; không còn thư mục nguồn tạm sau khi chuyển. Radio Studio không chạy trong lúc thao tác.

## Xác minh

- Chép từng file sang tên tạm, flush/fsync, tính SHA-256 dữ liệu nguồn trong khi chép; đọc lại toàn bộ file trên D để đối chiếu trước khi nhận file đích.
- Sau khi tất cả file đã đạt, đọc hash toàn bộ D thêm một lượt trước khi đổi đường dẫn hoặc dọn C.
- Kiểm tra danh sách nguồn không đổi, số lượng/kích thước đích, đường dẫn nằm đúng phạm vi. Giữ bản C cho tới khi D hoàn toàn được xác minh.
- Tạo junction, kiểm tra toàn bộ file truy cập qua đường dẫn C cũ và đọc hash mẫu qua junction; chỉ sau đó bỏ từng file nguồn đã kiểm kê. Không xóa đệ quy hoặc theo junction vào D.
- Thử riêng cơ chế lỗi bằng dữ liệu mẫu: hash D sai làm dừng và giữ nguồn; chuyển hợp lệ giữ byte và đọc qua junction được.
- Kiểm tra bằng `DeploymentManager.list_backups`: 7 snapshot lab và 6 snapshot main truy cập được qua đường dẫn cũ; mọi backup manifest đọc JSON được.
- 20/20 tham chiếu cache trong project/build_state vẫn trỏ tới file tồn tại. Không sửa các đường dẫn dự án.
- Manifest C/D cùng SHA-256: `D3D84624F0EFE68BF54E0216E007AF21B8814345E295E0C6561119CC17327EAF`.
- Không phát hiện sự kiện disk/NTFS ID 7/51/55/98/140/153 mới trong khoảng thao tác. Đây là kết quả kiểm tra lần chuyển này, không phải bảo đảm phần cứng lâu dài.

C còn **26,74 GiB** sau chuyển (trước lượt chép 11,83 GiB; số trống còn chịu ảnh hưởng cleanup bản build cũ chạy song song). D còn khoảng 1.076,66 GiB. Lượt build IMG đã hoàn tất trong khi chép; không áp dụng IMG trong tác vụ chuyển dữ liệu này.

Nhật ký từng file và hash: [radio-storage-migration-2026-10-22.json](evidence/radio-storage-migration-2026-10-22.json). Bản sao manifest: `D:/GTA Archive/Eagle Radio Studio/migration-manifest.json`. Helper chuyển: `tools/archive-radio-storage.py`; không chạy lại `stage` trên migration đã hoàn tất.

Giữ ổ D kết nối khi dùng Radio Studio hoặc phục hồi backup. Không xóa thư mục đích trên D khi dọn cache C; hai đường dẫn C đang dùng chính dữ liệu đó.
