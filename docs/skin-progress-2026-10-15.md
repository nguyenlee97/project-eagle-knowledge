# Tiến độ pool skin ped — 15/10/2026

> Sau bản thống kê này, người dùng đã chốt quy tắc cho phép lặp nguồn để phủ ID. Các số thiếu ở đây chỉ có nghĩa trong giả định mỗi ID một skin khác nhau. [Kế hoạch quay vòng hiện tại](skin-fill-plan-2026-10-15.md) dùng Bình thường trước ở vùng còn lại, rồi Thích → Hơi thích và lặp.

Dùng bản đánh giá người dùng vừa xuất lúc **00:15 15/10/2026 (giờ Việt Nam)**: `new-skin-ratings (1).json`. Đã đối chiếu đủ ID/URL core gallery, các thẻ tự thêm và counts JSON. Ba manifest roster của bản Eagle chính không đổi so với census. Không sửa game, gallery hoặc rating gốc.

**Cần 1,638 ped NPC. Pool đã xác nhận lựa chọn hiện có 587 ứng viên model, tương đương 35.8% về số lượng; còn 1,051 trước khi tính thêm thành viên pack.** Đây là giả định mỗi ID một skin riêng, trước kiểm tra trùng byte/rig ở nguồn mới. Chỉ 236 ứng viên có DFF/TXD đang nằm trong staging (14.4%). Không hiểu phần trăm này là đã cài/phủ xong ped ID.

| Nguồn | Thích | Hơi thích | Bình thường | Tổng model ứng viên |
| --- | ---: | ---: | ---: | ---: |
| Skin cũ có file, sau bỏ 8 trường hợp | 25 | 44 | 167 | 236 |
| Gallery mới đã chọn, gộp thẻ trùng nguồn | 231 | 58 | 27 | 316 |
| Skin đơn bạn chỉ định Bình thường | 0 | 0 | 35 | 35 |
| **Tổng trước xác minh archive mới** | **256** | **102** | **229** | **587** |

## Ba vùng ưu tiên

Vice City, Carcer City và Los Santos có **403 ID ứng viên sau khử trùng**. Chỉ Thích/Hơi thích được dùng ở vùng ưu tiên: **358/403 = 88.8%**, còn **45** theo giả định mỗi ID một skin riêng. Không đưa Bình thường vào phép tính này. Đây chưa phải đo tần suất spawn hoặc phân bổ hoàn tất.

## Pack và nguồn chờ

Có **22 nguồn pack/biến thể** được bạn chỉ định vào pool thường, chưa cộng chúng như 22 skin. Trong đó metadata có **15 nguồn mô tả ít nhất 128 mục model/nhân vật/variant**; chưa tải để kiểm tra file, sự trùng lặp hoặc chọn từng member. Pack có thêm biến thể trong gallery yêu thích cũng chưa được tự nhân số lượng từ các thẻ tên nhóm.

Gallery yêu thích mới có 693 thẻ: Thích 231, Hơi thích 58, Bình thường 28, Không sử dụng 42, chưa chọn 334. Tổng chọn gốc 317, gộp 1 nhóm thẻ trùng còn 316. Thẻ chưa chọn/loại không được cộng vào pool; 10 thẻ bạn tự thêm còn chưa đánh giá.

Không có `light-skin-decisions.json` mới trong Downloads ở lượt này: chỉ tính 57 nguồn bạn chỉ định trực tiếp (35 đơn + 22 mục pack), chưa coi 400 thẻ mặc định còn lại là quyết định đã xác nhận. Nếu có bản xuất pool thường, cập nhật báo cáo bằng `evidence/build_skin_progress.py` để xét thêm Giữ/Không sử dụng và tránh cộng nguồn trùng.

Về thu thập nguồn, có 693 thẻ ở gallery yêu thích và 457 nguồn ở gallery nhẹ/pack. Sau chuẩn hóa URL nguồn/tải, có 1,034 trang/landing nguồn khác nhau trên hai gallery. Đây là số nguồn, không phải số model hoặc số archive đã tải.

## Khử trùng và kiểm tra

Hai thẻ Annie Leonhart / Female Titan form và Female Titan / Annie Leonhart cùng trỏ [một skin Female Titan](https://www.gtainside.com/sanandreas/skins/146197-female-titan-from-attack-on-titan/), cùng preview/title/size và đều được ghi là single. Giữ mức cao hơn Hơi thích trong thống kê; không đổi rating gốc. Do đó Bình thường của gallery mới giảm từ 28 dòng chọn xuống 27 ứng viên nguồn. Các pack cùng trang nhưng có nhân vật khác nhau vẫn đếm riêng các member đã chọn.

236 cặp cũ có hash DFF/TXD khác nhau theo census trước; đã kiểm tra lại tất cả đường dẫn còn tồn tại và đúng size. Ba pilot 280/285/287 đã nằm trong số này, không cộng thêm lần nữa. Các nguồn mới khác URL vẫn có thể chứa asset giống nhau; phải kiểm tra hash khi tải mới biết số skin riêng biệt cuối cùng.

Nếu tính cả 38 model có pedtype PLAYER1/2 chưa chốt vai trò, phạm vi tăng lên 1,676, tỉ lệ ứng viên là 35.0% và còn 1,089. Nhân vật chính/placeholder và 10 slot mission động giữ ngoài phạm vi NPC đang tính.

[JSON thống kê và provenance](evidence/skin-progress-2026-10-15.json). Bản rating được chụp nguyên vẹn thành `evidence/new-skin-ratings-20261015-24e8907239f8.json`; không chỉnh file Downloads. Các thay đổi trong trình duyệt chưa xuất sau thời điểm trên không nằm trong báo cáo.
