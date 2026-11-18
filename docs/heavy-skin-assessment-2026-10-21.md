# Đánh giá skin giữ lại nặng nhất – 2026-10-21

## Kết luận

Skin lớn nhất đang **không bị loại** trong catalog là **Ikuyo Kita** (ID 2050, model `hfypro`): **94,844,002 byte = 90.45 MiB**, gồm DFF **1.85 MiB** và TXD **88.60 MiB**. Đánh giá hiện tại là `excluded=false`, `optimize=true`; điểm đánh giá riêng để trống, còn điểm kế thừa từ catalog là `like`.

Các file được catalog trỏ tới nằm trong thư viện `Skin Library\Project Eagle\numbered-skins\raw`, ngoài thư mục cài game. Không tìm thấy file cùng tên Ikuyo/Kita/hfypro bên trong thư mục Eagle. Do đó skin này **chưa gây ảnh hưởng tới game ở trạng thái hiện tại**; giữ nguyên file thư viện là hợp lý.

Nếu sau này dùng nó làm NPC trong Eagle, nên tối ưu riêng skin này trước khi triển khai. TXD có 20 texture D3D không nén 32-bit; tổng 23,225,437 pixel tương ứng khoảng 88.60 MiB dữ liệu màu nền. Có bốn texture 2048×2048, mỗi texture chiếm 16 MiB ở dạng 32-bit. Eagle có giới hạn streaming được cấu hình là 2,048 MiB; skin này chiếm xấp xỉ **4.4%** giới hạn đó nếu toàn bộ cặp model/texture được nạp. Đây là nguy cơ tạo áp lực streaming hoặc tăng thời gian nạp khi kết hợp với nhiều model nặng, nhưng dữ liệu tĩnh không chứng minh skin chắc chắn crash hay gây tụt khung hình.

Không có cơ sở để loại mọi skin trên 10 MiB: census hiện ghi nhận 600 bản ghi giữ lại vượt ngưỡng này. Dùng cờ `optimize` để ưu tiên xem xét từng skin; với Ikuyo Kita, cân nhắc giảm độ phân giải ở các texture ít quan trọng và dùng định dạng nén phù hợp alpha nếu triển khai. Không thay đổi file trong lần khảo sát này.

Hướng tối ưu cụ thể: giữ DFF trước vì chỉ chiếm 1,85 MiB, tạo **phiên bản TXD mới** để so sánh. Nén các texture có alpha bằng DXT5 (khối 4×4 chiếm 16 byte) cho dữ liệu mức nền khoảng 22,15 MiB thay vì 88,60 MiB; texture không cần alpha có thể dùng DXT1 (8 byte/khối, khoảng 11,08 MiB nếu áp dụng toàn bộ). Đây là ước tính dữ liệu texture, chưa cộng header/mipmap và chưa khẳng định mọi texture dùng được cùng một định dạng. Giảm cạnh texture 2048 xuống 1024 sẽ còn 1/4 số pixel ở texture đó; cần nhìn đối chiếu để quyết định mức mất chi tiết. Viewer giải mã texture ra RGBA để xem nên file TXD nhỏ hơn không đồng nghĩa bộ nhớ preview giảm tương ứng. Chưa tạo hay ghi đè TXD trong lần này.

## Bằng chứng đã kiểm tra

- Đọc trực tiếp API `/api/catalog` và `/api/reviews` của viewer. Catalog được cập nhật ngày 18/10; reviews cập nhật `2026-10-21T14:44:14.480Z`. Sau khi lọc các review `excluded=true`, Ikuyo Kita là bản ghi lớn nhất; bản đứng tiếp theo là Citlali ở khoảng 50.53 MiB.
- Review hiện tại của key `bf055a34adfa90d13e91b3bc8dca45bd8e8e292f596e0f06706f12b5a553d7c2`: `excluded=false`, `optimize=true`, `autoSizePolicy.thresholdBytes=10485760`, `action=optimize`. Nguồn catalog ghi tên archive `archive.rar` và nguồn GTAInside “Ikuyo Kita from Bocchi the Rock”.
- Đọc hai file gốc tại `Skin Library\Project Eagle\numbered-skins\raw\Ikuyo Kita__868d8c4f4927.dff` và `.txd`; dùng bộ đọc DFF/TXD có sẵn trong viewer để dựng mesh tĩnh. TXD đọc đủ 20 texture, không báo lỗi cấu trúc; tất cả chỉ có một mip level. DFF dựng được một skinned mesh với 83,286 đỉnh, 27,762 tam giác, 32 xương và 27 material slots.
- Catalog gắn cờ `missing_material_textures`; lần đọc DFF ghi nhận ba tên texture material chưa khớp: `body00_MikuAp_b`, `base_color_texture`, `TexÃ¢JÃ¶`. Vì vậy trạng thái texture chưa hoàn toàn sạch dù TXD tự đọc thành công.
- `fastman92limitAdjuster_GTASA.ini` đặt `Memory available = 2048` (dòng 460). `fastman92limitAdjuster.log` ghi streaming memory đã được đặt thành `2,147,483,648 bytes (2048 MB)` (dòng 248). Log được ghi lần cuối ngày 14/10/2026; đây là bằng chứng cấu hình/log đã áp dụng khi đó, không phải phép đo phiên chạy hiện tại. `stream.ini` vẫn có `memory=13500` và `devkit_memory=13500`.

## Giới hạn đánh giá

Đây là kiểm tra catalog, cấu hình, kích thước file và khả năng dựng dữ liệu tĩnh. Không cài skin, không chạy cảnh thử trong game, và chưa đo thời gian nạp, FPS, bộ nhớ tiến trình hoặc tương thích animation. Bởi vậy kết luận về hiệu năng khi sử dụng trong game vẫn cần một lần thử runtime sau khi có bản staging.
