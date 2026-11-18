# Skin nhỏ / pack: cách tìm và phạm vi đã rà

## Vì sao vòng trước ít

Vòng trước có 136 thẻ nguồn: 97 skin đơn và 39 pack. Phần chính bắt đầu từ 85 link LibertyCity người dùng gửi; lượt skin đơn bên ngoài mới đọc 37 trang GTAinside và giữ 36 record nguồn trước khi ghép/khử trùng/phân loại pack. Pack bổ sung được tìm theo một số truy vấn series và skin pack, cùng một blog tác giả. Chưa rà rộng các danh mục, phân trang và portfolio tác giả. Danh sách khi đó phản ánh lượt tìm hẹp, không phải toàn bộ skin đang có.

Ngưỡng skin đơn là archive nguồn công bố dưới 2.500.000 byte. Trang không công bố size chưa thể xác nhận vào nhóm này. GTAall thường không công bố size ở các bài đã đọc; pack được phép thiếu size vì không áp dụng giới hạn cho toàn gói. Mỗi pack là một thẻ để chọn, có thể chứa nhiều model/variant. Chưa cộng các thành viên thành số skin độc nhất vì chưa tải và kiểm tra archive.

## Lượt mở rộng này

Gallery từ 136 lên 400 thẻ; thêm ròng 240 skin đơn và 24 pack. Hiện có 337 skin đơn và 63 pack. Giữ đủ 136 ID, URL, ảnh và khóa/schema quyết định trước lượt này.

| Phạm vi | Cách rà thực tế |
| --- | --- |
| LibertyCity | 540 request trang index: 20 từ khóa anime/game ở New characters và 16 ở Skin packs, mỗi từ khóa trang 1–10; danh mục trực tiếp trang 1–10; 8 tác giả, cả hai nhóm, trang 1–10. Đọc 284 trang chi tiết, đều có JSON-LD bytes và gallery riêng. |
| GTAinside | 20 request: New look/model và Other skins & packs, trang 1–10. Đọc 18 chi tiết; 16 có gallery xác minh được, 8 skin mới qua size/ảnh. Bộ phân tích chưa lấy được card của 10 trang Other, nên đây là khoảng trống còn lại. |
| GTAall | Rà truy vấn pack theo series, danh mục và bài chi tiết; thêm hai pack Anime Characters và Naruto. Các skin đơn đọc được thiếu size nên nằm ngoài mục nhỏ. |
| GameModding | Đọc đủ 29 trang index pack, 291 link chi tiết, chọn đọc 11 bài có khả năng phù hợp; không thêm được anime pack mới. |
| FadXploit / blog tác giả / MixMods | Rà tìm theo series và tác giả; thiếu size ở các skin đơn, blog có trang giới hạn lượt truy cập, một số kết quả sai phong cách hoặc chỉ cho mobile. Kết quả và URL lưu trong input metadata. |

560 request index ở lượt LibertyCity/GTAinside gồm cả 160 request portfolio tác giả; không cộng lại hai lần mục portfolio. Đọc 302 trang chi tiết trong log hợp nhất. Có trang không có kết quả hoặc không được parser lấy ra; HTTP 200 không đồng nghĩa đã lấy đủ card. Các khoảng trống được ghi trong pageAudit. Đây là lượt rà theo từ khóa/trang/tác giả đã chọn.

14 record LibertyCity trong input trùng publication ID đã có; builder giữ thẻ cũ và gộp metadata hợp lệ, không tăng số thẻ. Số 264 bổ sung là sau khử trùng theo source publication ID. Asset đăng lại ở trang khác chưa xác minh trùng byte.

## Cách kiểm tra một lựa chọn

- Tên/series dựa trên tiêu đề và mô tả bài mod, không dùng tên/ảnh ở phần gợi ý để gán danh tính. Tên outfit/edition ở variant, giữ sourceTitle gốc.
- LibertyCity lấy byte chính xác từ SoftwareApplication.fileSize; ảnh từ #file_gallery li[data-src] của chính bài. GTAinside lấy gallery /img/YYYYMM/b/ từ HTML và size KB/MB quy đổi thận trọng, đánh dấu ước lượng.
- Skin đơn thiếu size, vượt ngưỡng, thiếu preview hoặc sai loại được để ngoài lựa chọn chính. Pack phải có bằng chứng nhiều model/variant; không suy ra số model từ số ảnh hay số slot thay thế.
- Anime/nhân vật game theo aesthetic là phạm vi thêm mới; các skin hoạt hình phương Tây trong list người dùng cũ vẫn giữ để người dùng tự loại. Pokémon/Yu-Gi-Oh giữ yêu cầu nhân vật người.
- Pack được giữ để xét/tải/tách sau, chưa được đánh dấu là một skin có thể gán cho một ped ID. Chưa đo DFF+TXD/VRAM hoặc kiểm thử trong Eagle.

[Mở gallery và chọn “Mới bổ sung lượt này”](/C:/Users/LENOVO/Desktop/GTA/staging/project-eagle/skin-light-gallery-2026-10-14/gallery.html). [Danh sách nguồn/size đầy đủ](light-skin-search.md). [Log LibertyCity/GTAinside](evidence/light-skin-sources-more-catalogs.json). [Log nguồn ngoài](evidence/light-skin-sources-more-external.json).

Nguồn đã mở và metadata có hash; ảnh đầu của đủ 400 thẻ đã tải được trong kiểm tra, 136 ảnh cũ giữ bằng chứng trước đó vì URL không đổi. Ảnh phụ chưa kiểm tra toàn bộ. Bộ lọc, giữ quyết định cũ, xuất/nạp JSON và layout desktop/mobile đã kiểm tra. Chưa tải ZIP/RAR/DFF/TXD hoặc cài mod.
