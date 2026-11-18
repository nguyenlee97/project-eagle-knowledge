> Mô phỏng phân bố trong tài liệu này đã được thay thế bởi yêu cầu mới ngày 15/10: Hơi thích còn dư → Thích có DFF+TXD dưới 2 MB → cụm yêu thích nhất + Bình thường. Chỉ giữ các số inventory trước tải làm tham khảo; chưa có kết quả phân bố theo quy tắc mới. Xem skin-fill-rule-2026-10-15.md.

# Dự tính phủ ped theo quy tắc quay vòng — 15/10/2026

**Quy tắc hiện tại cho phép dùng lại skin giữa nhiều ped ID. Vì vậy số skin riêng biệt ít hơn số ID không còn là thiếu hụt bắt buộc phải tìm thêm.** Đây là kiểm tra số lượng trước download; chưa mapping hoặc cài game.

Phạm vi: **403 ID** Vice City/Carcer City/Los Santos và **1,235 ID** còn lại; tổng **1,638 NPC**. Các tập không trùng nhau trong phép tính. Manifest Eagle không đổi so với roster.

## Pool đã chọn trước khi mở archive

| Nguồn | Thích | Hơi thích | Bình thường | Model ứng viên |
| --- | ---: | ---: | ---: | ---: |
| Skin cũ có file | 25 | 44 | 167 | 236 |
| Gallery anime/game yêu thích đã chọn, gộp trùng nguồn | 211 | 386 | 34 | 631 |
| Skin đơn duyệt trong gallery nhẹ, chưa có ở nguồn yêu thích | 0 | 0 | 313 | 313 |
| **Tổng** | **236** | **430** | **514** | **1180** |

Gallery nhẹ/pack: giữ **457 nguồn** (372 skin đơn và 85 pack), bỏ **0 nguồn**. 59 nguồn đơn trùng chính source đã chọn ở gallery yêu thích được đếm một lần, giữ tier cao hơn; vẫn được dùng ở vùng còn lại. Các nguồn khác site có thể trùng byte, chưa khẳng định khác DFF/TXD.

Có **85 pack/biến thể** chưa cộng member vào số model. 21 skin đơn mới còn cần kiểm tra size. Skin cũ bỏ tám trường hợp theo policy được giữ nguyên; các thẻ favorite chưa chọn/Không sử dụng vẫn ngoài pool.

## Mô phỏng theo thứ tự đã chốt

| Phạm vi | ID cần phủ | Bình thường | Thích | Hơi thích | Chưa phủ |
| --- | ---: | ---: | ---: | ---: | ---: |
| Ba vùng ưu tiên | 403 | 0 | 236 | 167 | 0 |
| Các vùng còn lại | 1235 | 573 | 270 | 392 | 0 |
| **Tổng** | **1638** | **573** | **506** | **559** | **0** |

Có 59 nguồn vừa được duyệt trong gallery nhẹ vừa có ở nguồn yêu thích. Khi đếm số model riêng thì giữ một nguồn tại tier cao hơn; khi cấp vùng còn lại thì các nguồn này vẫn được dùng trong lượt Bình thường đầu theo yêu cầu. Vì vậy lượt đầu ngoài ưu tiên có 573 nguồn Bình thường, 215 Thích chưa dùng trong lượt đó và 392 Hơi thích chưa dùng. Tổng vẫn là 1180, không cộng trùng.

**Vùng ưu tiên:** Thích 236 → Hơi thích 167.

**Vùng còn lại:** Bình thường 573 → Thích 215 → Hơi thích 392 → Thích 55 (lặp).

Lượt đầu của từng phạm vi không có nghĩa là skin chưa dùng ở phạm vi khác. Một skin có thể được dùng ở nhiều ID, và một ID có thể spawn nhiều NPC instance. Số lần dùng theo ID trong bảng không phải tỉ lệ gặp NPC hoặc mật độ spawn. Đây chưa là mapping cụ thể từng char/ID.

## Kiểm tra trước khi chốt sau download

- Đếm DFF/TXD thật trong từng pack, tách skin khỏi vũ khí/phụ kiện và xác nhận các member được duyệt.
- Gộp trùng hash giữa nguồn mới, nguồn cũ và các bản tải từ nhiều site; không suy ra khác skin chỉ từ URL khác.
- Bỏ nguồn tải lỗi hoặc model không dùng được, kiểm tra size thực tế và tương thích NPC/Eagle.
- Chạy lại phép cấp theo tier. Khi cho phép lặp, việc giảm số nguồn thường làm tăng độ lặp; vẫn cần ít nhất một nguồn dùng được trong tier được phép cho từng phạm vi.

[JSON mô phỏng và các lượt cấp](evidence/skin-fill-plan-2026-10-15.json). [Policy hiện tại](evidence/skin-placement-policy.json). Không sửa các bản đánh giá gốc hoặc cài/thay đổi game.

