# Ghép TXD từ Downloads/fix và chọn phiên bản để gán NPC

## Kết quả

- 52 skin đang sử dụng được ghép TXD; 11 biến thể texture mới có key và ID riêng. Tổng catalog 3.131 record.
- Không còn bản DFF đang dùng nào thiếu TXD. 9 bản còn thiếu đều có review Không sử dụng, được giữ nguyên quyết định.
- 31 cặp có sẵn được nhận diện để tránh thêm lại. Các lựa chọn khác như Chasca không mũ, Mavuika đeo kính, Varesa eye mask, Daiwa Scarlet shading fix và Nemona Violet được thêm riêng.
- Hai bản Luffy được tạo TXD lossless từ 4 PNG trong gói nguồn, giữ kích thước/màu/alpha. Tatsumaki được tạo bản TXD đổi đúng tên `T_Body.png` và `T_Head.png` theo DFF, không đổi pixel hoặc file TXD gốc.
- 18 lượt ghép còn thiếu texture tham chiếu trong gói nguồn, phần lớn là texture phụ như `HM_B_Oral`, texture vũ khí hoặc phụ kiện. Có TXD không có nghĩa tất cả vật liệu đều đầy đủ; giữ cờ Thiếu texture trong TXD. Chi tiết tên thiếu nằm trong JSON kết quả.

## Chọn và gán phiên bản

Thanh Phiên bản trên khung model luôn hiện; chọn dropdown hoặc Trước/Sau để xem từng bản. Nút xanh Gán ghi rõ ID phiên bản đang xem và NPC đích. Trạng thái bản nháp cũng hiện ngay dưới nút; thay bản đang xem không tự sửa mapping.

Đại diện chỉ là lựa chọn mặc định của item. Có thể gán bất kỳ phiên bản hợp lệ đang xem, kể cả bản khác đại diện. Phiên bản có TXD khác nội dung được giữ dù dung lượng giống nhau. Rất thích tiếp tục đứng riêng, đồng thời vẫn có thể xem các phiên bản liên quan.

Hộp Bổ sung TXD có lựa chọn thêm một phiên bản mới thay vì ghi đè phiên bản hiện tại. File và đánh giá nguồn được giữ; bản mới có thể được chấm riêng.

## Xác minh

- Đã kiểm SHA-256 TXD và DFF của đủ 63 lượt ghép/thêm so với kết quả inspector. Giữ tất cả rating, note, manualFlags, sourceUrl và mappings của các record cũ so với snapshot trước thao tác.
- 17 Node tests trước bulk import pass; sau bổ sung bảo vệ cleanup đã chạy lại 8 tests liên quan, tất cả pass. Kiểm thử tạo phiên bản, chống nhập trùng hash, mapping theo key phiên bản và snapshot/journal được bao phủ.
- UI QA cổng riêng 18948: gán variant 2, chuyển sang variant 1 không đổi mapping; bấm Gán mới đổi mapping; reload giữ đúng key. Nút gán nhanh cạnh selector cũng lưu đúng variant 2.
- UI thật: Chasca có 8 phiên bản; mở bản không mũ #3237, nút gán ghi đúng #3237. Không gán NPC hoặc build/apply vào game trên dữ liệu thật.

## Bằng chứng và phục hồi

- `fix-txd-final-2026-10-18.json`: tổng kết và danh sách còn thiếu texture phụ / bản Không sử dụng.
- `fix-txd-import-2026-10-18.json`: các lượt ghép và 11 phiên bản; `fix-txd-supplement-import-2026-10-18.json`: hai bản Luffy và Tatsumaki.
- Hai JSON trên lưu đường dẫn snapshot catalog/reviews trước mỗi giai đoạn. Các transaction dưới `numbered-skins/imports` có inspector và journal.
- `fix-txd-candidates-2026-10-18.json`: đối chiếu DFF và ứng viên từ thư mục fix, snapshot trước nhập.
- Ảnh `evidence/fix-txd-variant-picker-2026-10-18.jpg` và `evidence/version-mapping-qa-2026-10-18.jpg`.
