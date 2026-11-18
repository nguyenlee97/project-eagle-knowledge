# Skin viewer cá thể — 18/10/2026

Viewer: http://127.0.0.1:8943/

Kho có **3.236 mục**: 3.143 cặp DFF/TXD, 84 DFF chưa ghép được TXD, 9 mục chỉ giữ metadata. Mỗi mục được bổ sung thông tin từ dữ liệu nguồn và đánh giá cũ; đánh giá riêng được ưu tiên khi có.

6.370 file nằm tại `Skin Library/Project Eagle/numbered-skins/raw`, đã đổi sang tên gợi nhớ kèm hậu tố hash chống trùng, dùng hardlink cùng ổ C. Tên thư mục `numbered-skins` được giữ để tương thích; số thứ tự không còn là nhãn chính. Mọi file tham chiếu đều tồn tại, có tối thiểu hai liên kết; không có file model được liên kết cho các mục chỉ giữ metadata. Không sửa trực tiếp các hardlink. Khóa nhận dạng, đánh giá và mapping cũ được giữ nguyên; nội dung file gốc không thay đổi.

## Cập nhật bộ lọc và dữ liệu cá thể

- Lọc kết hợp theo game/anime, nhóm nguồn (skin cũ, yêu thích, skin nhỏ, skin pack…), mức đánh giá và tình trạng thiếu dữ liệu/lỗi kỹ thuật. Có thể chọn lọc theo mức hiệu lực, chỉ mức cũ hoặc chỉ đánh giá riêng.
- Khi chưa chấm riêng, skin kế thừa Thích / Hơi thích / Bình thường. Rất thích chỉ có khi người dùng chấm riêng. Nút “Dùng mức cũ” xóa mức riêng và khôi phục kế thừa; ghi chú/cờ riêng không làm mất kế thừa.
- Skin nhỏ/pack dùng quyết định cũ thực tế, bao gồm các ngoại lệ đã duyệt trước đó. Các mục trước đây không chọn được ghi riêng, không tự biến thành cờ vi phạm policy.
- Link nguồn có sẵn được hiển thị trong viewer; cho phép bổ sung link thủ công theo từng skin. Đường dẫn file gốc và tên archive vẫn được giữ để truy vết. Các mục chỉ giữ metadata không cung cấp model hay link nội dung.
- 2.619 mục có series; 2.612 mục có link HTTP(S) hiển thị. Còn 615 mục thường chưa tìm được link nguồn và 9 mục giữ metadata không hiển thị link. Bộ lọc cho phép tìm phần thiếu này; không bịa link từ tên nhân vật.
- Mức cũ gồm 483 Thích, 685 Hơi thích, 1.503 Bình thường, 392 không chọn trước đây và 173 chưa xác định. Các số này bao gồm mục giữ metadata; giao diện loại chúng khỏi kế thừa hiệu lực.
- Chẩn đoán gồm 84 mục thiếu TXD, 726 mục thiếu texture được vật liệu tham chiếu, 97 trường hợp ghép cặp chưa rõ và 3 lỗi dựng preview. Đây là cờ kỹ thuật để xem xét, không tự kết luận skin phải bỏ.

Ảnh giao diện sau cập nhật: `docs/project-eagle/evidence/skin-viewer-enriched-2026-10-18.jpg`. Báo cáo enrichment và lịch sử đổi tên nằm trong `numbered-skins/enrichment-report.json` và `numbered-skins/metadata-migrations/`.

## Chức năng

- Hai khung 3D độc lập: skin mod và NPC hiện tại của Eagle; kéo xoay, zoom, tự xoay, khung lưới và ảnh chụp.
- Rất thích / Thích / Hơi thích / Bình thường; hai cờ riêng cần phân tích tối ưu dung lượng và Không sử dụng; ghi chú và lý do.
- Tự lưu vào `numbered-skins/reviews.json`, lịch sử JSONL, xuất/nhập JSON. Gán NPC là bản nháp, không sửa game.
- Hiển thị dung lượng DFF+TXD đã giải nén. 1 MiB = 1.048.576 byte.
- 1.638 slot NPC với tài nguyên được xuất từ IMG được khai báo trong Eagle. Khu vực/nhóm và tỉ trọng phần tử lấy từ cấu hình; không coi đó là xác suất spawn. Chưa có tọa độ/đường xuất hiện cụ thể.

## Kiểm tra thực hiện

- Dựng mesh CPU: 3.224 mục mod thành công, 9 mục metadata được bỏ qua; toàn bộ 1.638 NPC thành công. Đây không phải kiểm thử texture/rig trong game trên toàn bộ mẫu.
- Browser: đã xem mẫu nhẹ, mẫu 31,92 MiB, NPC gốc và cảnh sát thay thế; thử xoay, lưu đánh giá, tải lại giữ mức đã chọn và chọn mức không giật cuộn khi bố cục ổn định. Đánh giá thử dùng thư viện riêng, không ghi vào kho thật.
- Năm kiểm tra tự động qua: kế thừa/ghi đè mức riêng; bộ lọc kết hợp; lưu/nhập/khởi động lại, bảo vệ asset và xác thực link nguồn; giải mã D3D9 DXT1; giải mã D3D9 DXT5. Thử đánh giá dùng thư viện riêng, không ghi vào kho thật.
- Đã kiểm tra trên dữ liệu thật: 3.236 khóa nhận dạng không đổi, 6.370 đường dẫn duy nhất không phân biệt hoa/thường và tồn tại; không có mức Rất thích kế thừa. Browser lọc Genshin/Thích, mở link nguồn, dựng và xoay Keqing Maid từ tên file mới thành công.
- Dựng model trong Web Worker, giới hạn 15 giây/mẫu để giữ giao diện phản hồi. Có kiểm tra biên và giới hạn bộ nhớ.

Các mục chưa dựng được vẫn còn trong kho:

- #1210 — bat: `DFFLoader: Offset is outside the bounds of chunk CHUNK_CLUMP`.
- #2912 — LC CAS WOM: `DFF chunk out of bounds`.
- #3029 — SA MAFGOON1: `DFFLoader: Offset is outside the bounds of chunk CHUNK_CLUMP`.

## Tình trạng giải nén

- Đối chiếu manifest: 1.159 đường dẫn archive, 1.120 hash archive riêng biệt. 1.118 hash đã có kiểm tra trực tiếp/đệ quy; hai archive nội dung đã giữ theo policy không mở.
- Bổ sung 13 archive thường trước đây chưa có inspection, đưa thêm 14 cặp vào kho. 48 archive lồng nhau có kiểm tra integrity đệ quy thành công.
- Len/KAITO: archive gốc lỗi descriptor nhưng đã có các cặp từ bản phục hồi. Không cần người dùng xử lý lại.
- Naruto: archive gốc lỗi header; 14 file DFF/TXD đọc qua kiểm tra CRC và cho 7 cặp đã có trong kho, không tăng ID.
- Rosaria: archive vẫn không mở được qua kiểm tra integrity/mật khẩu; đã bỏ theo quyết định trước đó. Không khẳng định mọi archive đều giải nén thành công.

Chi tiết: `numbered-skins/extraction-coverage.json`, `viewer-mesh-validation.json`, `catalog.json`, `npcs.json`. Mẫu thiếu TXD hoặc cảnh báo kỹ thuật vẫn được giữ; các mẫu nội dung không đủ điều kiện dựng hình chỉ có metadata.

## Vận hành

Chạy `tools/skin-viewer/Start-Viewer.ps1` khi server chưa chạy; sau đó mở URL trên. Hướng dẫn trong `tools/skin-viewer/README.md`. Bản snapshot backup ổ D trước đó không tự cập nhật các file viewer/đánh giá mới. Tài nguyên game không bị thay đổi.
