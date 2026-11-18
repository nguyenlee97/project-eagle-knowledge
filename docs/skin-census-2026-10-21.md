# Tổng kiểm kê skin — 2026-10-21 21:51:00 (Việt Nam)

Nguồn: catalog/reviews/npcs/deployment API của viewer. Reviews cập nhật 2026-10-21T14:44:14.480Z. Báo cáo chỉ đọc; không sửa đánh giá, cờ, mapping hoặc game.

## Kết luận về số lượng

Eagle hiện có **1.638 slot NPC** thuộc phạm vi thay skin của viewer. Đối chiếu lại data/peds.ide thực tế: 1.687 định nghĩa, loại 1 placeholder người chơi + 38 model mã người chơi + 10 slot nhiệm vụ, còn đúng 1.638 ID như catalog.

Kho có **3.131 bản skin/record**, tương ứng **2.753 item sau gom phiên bản**. Trong đó 3.113 cặp DFF+TXD, 9 DFF còn thiếu TXD (đều bị loại), 9 mục chỉ giữ metadata.

| Tập lựa chọn | Bản/phiên bản | Item chọn tối đa một bản | Item / 1.638 slot | Chênh lệch item |
|---|---:|---:|---:|---:|
| Còn giữ, đủ file/header, bỏ qua yêu cầu tối ưu | 3.052 | 2.691 | 164,29% | +1.053 |
| Đủ file/header và không có cờ tối ưu | 2.459 | 2.347 | 143,28% | +709 |

Đây là tỷ lệ nguồn cung so với số slot, không phải tỷ lệ đã cài và cũng không khẳng định mỗi item là một nhân vật khác nhau. Item vẫn được gom theo quy tắc tên/size/family hiện hành; Rất thích đứng riêng. Đếm một item một lần tránh dùng các phiên bản thay TXD để thổi phồng nguồn cung. Chưa kiểm thử rig/animation/performance toàn bộ pool trong game.

Bản nháp mapping qua viewer: **0/1638**; đã áp dụng qua viewer: **0/1638**. Không bao gồm các thay thế thử nghiệm cũ thực hiện ngoài viewer.

## Trạng thái theo bản skin (các hàng không trùng nhau)

| Trạng thái | Bản | % toàn kho |
|---|---:|---:|
| Giữ, đủ file/header, không cờ tối ưu | 2.459 | 78,54% |
| Giữ, cần tối ưu | 593 | 18,94% |
| Giữ, cần xem lại header | 1 | 0,03% |
| Không sử dụng / chỉ metadata | 78 | 2,49% |
| Tổng | 3.131 | 100% |

Tổng còn giữ: **3.053 bản** / **2.692 item**. Bỏ toàn bộ: 61 item. Có cờ tối ưu trên 598 bản, nhưng 5 bản đã bị bỏ; danh sách thực sự cần xử lý là **593 bản**, bằng 19,42% pool còn giữ.

Ở cấp item: 345 item có ít nhất một phiên bản cần tối ưu; 344 item chỉ có bản còn giữ đang cần tối ưu. Một item còn lại có cả bản tối ưu và bản không cần tối ưu, nên không cộng chồng các nhóm này.

Lý do bỏ: 49 bản vượt policy 10 MiB; 20 bản không ghi lý do; 9 bản chỉ metadata/giữ ngoài pool. Không có sai khác giữa cờ hiện lưu và cách áp dụng quy tắc dung lượng hiện hành.

## Mức đánh giá hiệu lực của các bản còn giữ

| Mức | Bản | % pool giữ |
|---|---:|---:|
| Rất thích | 27 | 0,88% |
| Thích | 584 | 19,13% |
| Hơi thích | 950 | 31,12% |
| Bình thường | 1.492 | 48,87% |
| Chưa có điểm | 0 | 0,00% |

Trong pool giữ: 605 bản có điểm chấm mới, 2448 bản kế thừa mức cũ; không còn bản thiếu cả hai. Toàn catalog có 650 bản có điểm mới, 2472 bản kế thừa, 9 metadata không có mức sử dụng.

## Dung lượng và kiểm tra file

| Tổng DFF+TXD mỗi bản còn giữ | Bản |
|---|---:|
| ≤2 MiB | 709 |
| >2–5 MiB | 1.240 |
| >5–10 MiB | 504 |
| >10 MiB | 600 |

Quét 6.198 đường dẫn tài nguyên; khử hardlink theo file ID có **5.766 file vật lý**: 3.092 DFF + 2.674 TXD, **14.99 GiB**. Chỉ tính tài nguyên được catalog tham chiếu, không cộng archive, extraction cũ, NPC assets và các backup.

735 bản còn giữ có cờ thiếu texture trong TXD. Theo quyết định trước đó, không loại các bản này khỏi pool chỉ vì cờ đó. Đây là cảnh báo tài nguyên, không phải kết luận tất cả chúng hiển thị sai.

Một trường hợp cần xem lại: **#2866 MW SOMYRG**, TXD khai báo chiều dài lớn hơn file thật 12 byte. Decoder viewer vẫn đọc được 7 tên texture không cảnh báo; chưa kết luận model hỏng. Tạm tách khỏi con số đủ file/header thận trọng, không tự đổi đánh giá hoặc cờ của người dùng.

Kiểm tra lần này gồm tồn tại file, kích thước và header/chunk boundary. Không giải mã lại toàn bộ texture, không quét lại từng rig hoặc chạy thử từng skin trong game.

Dữ liệu từng bản, item và số liệu máy đọc được: [skin-census-2026-10-21.json](skin-census-2026-10-21.json).
