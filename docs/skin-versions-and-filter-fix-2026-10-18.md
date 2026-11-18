# Gom phiên bản skin và giữ filter sau ghép TXD

Viewer: http://127.0.0.1:8943/

## Hành vi

- Cùng tên và chênh tổng DFF+TXD tối đa 5%, so với bản nhỏ nhất trong cụm. Không gom nối dây chuyền vượt ngưỡng.
- Rất thích: giữ riêng; đổi mức có hiệu lực ngay. Chỉ metadata: giữ riêng.
- Đúng cả dung lượng DFF và TXD: một phiên bản, chọn bản có mức cao nhất. Không suy ra bằng chứng byte/hash giống nhau.
- Đại diện mặc định là phiên bản có mức hiệu lực cao nhất; người dùng đổi trong dropdown rồi bấm nút đặt đại diện. Lựa chọn lưu trên đĩa, không phụ thuộc localStorage.
- Bộ lọc khớp từng phiên bản; một cụm xuất hiện nếu có bản khớp. Đại diện nằm ngoài filter thì dùng bản khớp điểm cao nhất để hiển thị.
- Đánh giá/cờ/nguồn và mapping NPC vẫn là của từng key. Không đổi file, xóa archive hay áp dụng mod vào game.
- Tất cả filter, trang và vị trí cuộn được giữ sau ghép TXD; filter hết kết quả được giữ với số 0. Model vừa sửa tiếp tục ở khung xem.

## Kiểm tra

- 15 Node tests pass: grouping 5%, chống nối dây chuyền, trùng kích thước, giữ Rất thích riêng, chọn đại diện và lưu qua restart, reviews/import/repair/preview/texture decoder.
- QA browser trên thư viện riêng cổng 18948: chọn bản đại diện rồi reload giữ lựa chọn; chấm Rất thích chuyển từ 2 item thành 3, hạ về Thích gom lại.
- QA ghép TXD hợp lệ vào bản thiếu: giữ `term=Repair target`, `series=QA`, `issue=missing_txd`, `exclude=hide`, `sort=size-desc`; kết quả 0 item, option `Thiếu TXD (0)` vẫn được chọn và Repair target vẫn trong khung xem.
- Ảnh bằng chứng: `evidence/txd-filter-preserved-2026-10-18.jpg`.
- Thư viện thật trước phục hồi metadata: 3.120 bản, 2.808 item, 206 cụm nhiều bản. Các con số sẽ thay đổi khi người dùng tiếp tục chấm.

Nguồn thiếu metadata được điều tra riêng trong `missing-metadata-investigation-2026-10-18.md` và JSON cùng tên.

## Phục hồi metadata đã áp dụng

`recover_metadata.py --write` thêm nguồn cho 20 bản, series cho 19 bản và mức cũ có bằng chứng cho 7 bản. Ghi archive name cho Promeia nhưng để URL/series/mức cũ chưa xác nhận. Burnice chỉ có nguồn archive, không đổi nhãn A74 Charlotte. Thêm nhóm lọc Fadxploit cho 20 bản có nguồn xác nhận.

Giữ nguyên cả 21 key/ID, review, mapping, DFF/TXD và cờ thiếu TXD. Trong 20 bản có nguồn, inspection có tổng 43 đường dẫn TXD ứng viên; chưa tự chọn cặp khi còn mơ hồ. Bản snapshot trước phục hồi: `Skin Library/Project Eagle/numbered-skins/metadata-migrations/catalog-before-source-recovery-20261018T133700Z.json`.

Kiểm tra sau áp dụng: lần chạy dry-run kế tiếp đổi 0 mục; dry-run toàn bộ `build_enrichment` giữ lại nguồn, series và 7 mức cũ được phục hồi. Agent chính đối chiếu lại hash archive Nefer, Yuzuha và Zani với inspection/source manifest; khớp. Không truy cập nguồn ngoài hoặc tải thêm.
