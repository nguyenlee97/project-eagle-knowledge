# Gom các biến thể trong nhóm thiếu TXD

Đã gắn family cho 85 record thuộc 29 cụm có ít nhất một bản thiếu TXD. Căn cứ: cùng hash archive giải nén trong originalDffPaths và cùng tên literal hoặc biến thể đuôi 2 có tên gốc tồn tại trong chính archive đó. Không đổi tên hoặc xóa tài nguyên, không sửa review hoặc mapping.

- Jingliu HSR / Jingliu HSR2: ID 310, 1005, 2764, 2775 → một item, bốn phiên bản; hai bản đã có TXD, hai bản còn thiếu.
- Sinon Bikini / Sinon Bikini2: ID 577, 1339, 2766, 2777 → một item, bốn phiên bản.
- Các cụm tương tự: Charolic, FuXuan, Lenna, Klukai, Shenhe, OguriSport, Kurumi, Chasca, Jinhsi và các cụm khác trong JSON cùng tên.

Family là ngoại lệ có căn cứ nguồn đối với ngưỡng 5%: tổng size thiếu TXD không thể so trực tiếp với tổng size của cặp đầy đủ. Liên kết family được giữ sau khi ghép TXD. Các phiên bản vẫn giữ rating/cờ/mapping và nguồn riêng. Rất thích tự đứng riêng. Đúng dung lượng DFF và cùng trạng thái/dung lượng TXD trong cụm thì chỉ hiện bản điểm cao nhất; các record còn lại được giữ để truy vết.

Kiểm tra snapshot hiện tại: thư viện vẫn 3.120 record, 2.753 item; filter thiếu TXD + ẩn bị loại giảm 47 → 30 item. Số liệu thay đổi theo đánh giá và ghép TXD sau này. Không tìm thấy nhãn literal Shion trong catalog; có Sinon Bikini và nhóm này đã được gom.

Kiểm thử: 3 tests grouping và 1 test server pass; UI thật xác nhận tìm Jingliu + thiếu TXD còn một item, dropdown đủ bốn phiên bản và cho mở bản có TXD trong cùng cụm. Ảnh: `evidence/unpaired-version-groups-2026-10-18.jpg`.

JSON cùng tên chứa snapshot catalog trước thay đổi và đủ ID/key của từng cụm. Công cụ tái lập: `tools/skin-viewer/group-unpaired-families.py` (mặc định dry-run, --write khi server tắt).
