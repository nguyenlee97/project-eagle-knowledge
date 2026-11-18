# Dọn thư viện, bổ sung TXD và cờ dung lượng — 18/10/2026

Viewer: http://127.0.0.1:8943/

Danh sách từ **3.236 còn 3.120 mục**. Loại 116 mục, đếm không chồng nhau: 3 lỗi preview đã ghi nhận, 66 không có Skin plugin, 6 vũ khí/phụ kiện còn lại và 41 bản trùng theo tên + đúng số byte DFF/TXD. Nhóm không Skin plugin ban đầu có 67 mục; một mục được tính trong lỗi preview. Bản trùng giữ record có mức đánh giá hiệu lực cao nhất (Rất thích > Thích > Hơi thích > Bình thường), gộp nguồn/ghi chú và chuyển mapping nháp. Tên/size giống nhau không bảo đảm nội dung byte giống nhau; tiêu chí này được dùng theo yêu cầu người dùng.

Đã sửa nhãn vũ khí sai cho 8 mẫu người được nêu, cùng `sasuke1`, `sakura1`, `kakash1` (tên file thực tế của mẫu Kakashi). Các skin thiếu texture bên trong TXD vẫn giữ; không loại chỉ vì cờ đó. 84 DFF thiếu TXD vẫn giữ để bổ sung.

Snapshot và file bị gỡ khỏi raw:

`C:\Users\LENOVO\Desktop\GTA\Skin Library\Project Eagle\numbered-skins\maintenance\2026-10-18T10-07-08.839Z-cleanup`

Có `catalog-before.json`, `reviews-before.json`, `removed-records.json`, `moved-assets.json`, `report.json`, `transaction.json` và `removed-assets`. Đã chuyển 232 raw link sang snapshot; không xóa kho nguồn/archive và không khẳng định giải phóng tương ứng dung lượng vật lý do dùng hardlink. `catalog-dispositions.json` giữ tombstone để importer cũ không phục hồi mục đã loại. Importer/enrichment giữ phân loại ped sửa tay và TXD được bổ sung.

## Cờ dung lượng

Tổng DFF + TXD **trên 10 MiB** (10.485.760 byte), theo mức chấm riêng hoặc kế thừa: 107 Bình thường được bật Không sử dụng vì policy dung lượng, 378 Thích/Hơi thích được bật Cần tối ưu. Rất thích không nhận thêm cờ tự động; cờ đã đánh tay vẫn giữ riêng. Mức chưa rõ/không chọn trước đây chưa bị suy thành Bình thường.

Quy tắc chạy mỗi lần đổi mức, trở về mức cũ, nhập đánh giá, import skin hoặc ghép TXD. Khi ranking đổi, chỉ cờ tự động do quy tắc tạo được gỡ; không xóa quyết định loại/tối ưu thủ công. Skin bị Không sử dụng không được gán NPC; nếu nháp đang gán sẽ bỏ gán. Chưa tối ưu texture/model trong lượt này và chưa thay game.

## Bổ sung TXD

Nút **Bổ sung / thay TXD** trong khung skin: chọn file → Kiểm tra TXD → xem tên texture, số vật liệu khớp/còn thiếu → Ghép TXD đã kiểm tra. Chặn sai định dạng/header, file vượt 128 MiB, giải mã lỗi, không có texture khớp, DFF/skin thay đổi giữa kiểm tra và commit. Khớp một phần có cảnh báo rõ. Giữ ID, ranking, ghi chú, mapping và phiên bản TXD cũ; cập nhật bytes, bộ lọc và cờ tự động. Không tự cài vào game.

## Ba mẫu Naruto

Mỗi TXD giải mã được 3 texture có màu; không thiếu tên texture và không có vertex prelight. Chế độ texture không ánh sáng/tắt tint không khôi phục được ngoại hình mong đợi của Sasuke trong lần thử; lật V làm đổi màu mẫu nhưng không chứng minh mapping đúng. UV có nhiều đỉnh trùng tọa độ, có vùng lấy mẫu tối; hiện chưa xác quyết nguyên nhân cuối cùng giữa dữ liệu UV/vật liệu và cách dựng của viewer. Không sửa DFF/TXD hoặc tự kết luận hỏng. Giữ ba mẫu với bộ lọc **Cần kiểm tra UV / vật liệu**. Chi tiết đo: `evidence/naruto-three-preview-inspection-2026-10-18.json`.

## Kiểm tra

12 kiểm tra Node và 5 kiểm tra Python qua, gồm chuyển ranking/cờ tự động, giữ cờ tay, gộp bản trùng và remap, TXD hỏng/không khớp/đúng cặp, giữ ID/ranking/ghi chú/mapping, import journal và build/apply/restore. Browser QA riêng xác nhận Bình thường → loại, Thích → tối ưu, Rất thích → gỡ cờ tự động; kiểm tra và ghép TXD đúng tên nội bộ, dung lượng và ghi chú được cập nhật/giữ lại.
