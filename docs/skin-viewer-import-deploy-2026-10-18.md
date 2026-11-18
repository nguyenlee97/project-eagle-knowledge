# Viewer — nhập skin và build mapping NPC

Viewer: http://127.0.0.1:8943/

Đã thêm **+ Nhập skin** và **Build & áp dụng vào game**. Bản game thật chưa được thay đổi bởi lượt triển khai tính năng này; chưa có mapping nào được tự động áp dụng.

## Cách dùng

- Nhập: chọn cặp DFF/TXD hoặc ZIP/RAR/7Z → chọn series có sẵn/tạo series mới → chọn mức đánh giá → phân tích → chọn các cặp để nhập. Link nguồn là tùy chọn. Cặp trùng byte được bỏ qua, đánh giá cũ được giữ nguyên. Mỗi thành viên pack vẫn là một cá thể.
- Thay NPC: chọn NPC + skin → Gán skin đang xem → mở Build & áp dụng vào game → Build IMG → tắt game → Áp dụng bản build. Lần sau đổi/bỏ gán rồi làm lại.
- Phục hồi trước viewer: trả archive về snapshot lần build đầu, bao gồm các mod đã tồn tại trước lần đó; không phải bản GTA SA vanilla. Bản nháp vẫn được giữ.

## Phạm vi kỹ thuật

Eagle tắt plugin stream loose DFF/TXD. Tool đọc manifest/IDE và thay đúng member trong IMG đang mount. Không bật plugin, mount thêm archive, thay Aether hay sửa tần suất/AI/population/save. Đối chiếu lại cấu hình, tên member, hash nguồn, hash archive; mỗi build dựa vào baseline bất biến để không tăng dung lượng dần. TXD dùng chung có kiểm tra xung đột, từ chối thay lén NPC chưa chọn.

Kho: `Skin Library/Project Eagle/numbered-skins`. Baseline/candidate/journal tại `deployment`; provenance import tại `imports`; cặp cuối nằm trong `raw`. Snapshot D cũ chưa tự cập nhật những dữ liệu này. Có rollback khi lỗi và nút phục hồi giao dịch bị ngắt; không ghi đè hash archive không nhận diện được.

## Kiểm tra

- 5 kiểm tra Python: build/apply/restore/bỏ gán, payload và baseline không đổi, build lặp không phình, từ chối mapping/config/hash ngoài dự kiến, skin bị loại/TXD dùng chung, lỗi copy dở dang, journal phục hồi tác vụ bị ngắt.
- 6 kiểm tra Node: ranking và bộ lọc cũ, lưu/nhập reviews, bảo vệ asset và source URL, import cặp/pack/series/ranking, duplicate và phục hồi journal, DXT1/DXT5.
- Browser QA dùng thư viện và IMG giả lập riêng dưới `staging/project-eagle/skin-viewer-qa-import-deploy-20261018`: nhập cặp thật với series mới và Rất thích; gán NPC 7, build, áp dụng, xem khung NPC cập nhật, phục hồi. Hash IMG giả lập sau phục hồi phải khớp hash ban đầu.
- Không mở game thật hoặc nghiệm thu animation/FPS của skin mới. Kiểm tra header/CRC/hash không chứng minh rig hoạt động trong game.

Hướng dẫn vận hành và giới hạn upload chi tiết: `tools/skin-viewer/README.md`.
