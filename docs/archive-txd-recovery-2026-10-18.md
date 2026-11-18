# Ghép TXD từ archive và tạo TXD cho Promeia

Đã ghép cả 21 DFF trong nhóm điều tra trước bằng transaction API của viewer. Không áp dụng vào game. Giữ ID/key, DFF, mức chấm riêng, ghi chú, cờ người dùng và mapping NPC. Các cờ dung lượng tự động được tính lại theo tổng DFF+TXD mới.

## Promeia / Promelija

- Archive gốc: `Skin Library/Project Eagle/user-downloaded-unreviewed/FadXploit Promelija.7z`.
- Ba PNG trong `Without alpha`: `Image_1.png`, `Image_3.png`, `Image_4.png`; mỗi ảnh RGB 1024×1024.
- DFF yêu cầu đúng ba tên trên. Tạo TXD RenderWare PC D3D9, BGRA32 opaque, một mip level, không resize hoặc nén mất dữ liệu. Không tự tạo alpha khi nguồn không có.
- TXD mới: `Skin Library/Project Eagle/numbered-skins/generated/Promeia-2026-10-18/Promeia.txd` cùng manifest SHA-256 và ảnh nguồn.
- TXD 12.00 MiB; tổng DFF+TXD **14.40 MiB**. Bản raw được transaction API thêm vào catalog ID 2770.
- Inspector xác nhận 3/3 vật liệu có texture, không thiếu tên. Pixel RGBA sau giải mã TXD khớp SHA-256 của từng PNG gốc. Viewer mở được mô hình có màu/texture.

## Các archive còn lại

Ghép 20 bản từ TXD có sẵn trong đúng archive. Ưu tiên cùng basename DFF rồi vị trí gốc trong gói; các bản TXD cùng SHA-256 không được thử lặp. Các tùy chọn TXD phụ vẫn nằm nguyên trong archive/thư mục giải nén.

19 bản có đủ texture tham chiếu. A74 Charlotte khớp 3/4 vật liệu; TXD gốc thiếu `HM_B_Headset`. Vẫn ghép theo chỉ dẫn người dùng và giữ cờ Thiếu texture trong TXD, không tạo texture giả. Cộng Promeia: **21 bản đã có TXD, 20 bản đủ texture, 1 bản thiếu texture phụ**.

Đã bỏ cờ ghép mơ hồ và cảnh báo DFF lẻ cũ khỏi 21 bản sau khi ghép; không bỏ cảnh báo texture thực sự thiếu. Toàn thư viện còn 61 mục mang cờ Thiếu TXD tại thời điểm này.

## Bằng chứng

- `archive-txd-recovery-2026-10-18.json`: đủ 21 key/ID, TXD path, hash, kết quả inspector và session transaction; các đường dẫn snapshot trước thay đổi.
- `png_to_txd.py`: chuyển PNG sang TXD; `repair-archive-txds.mjs`: ghép qua API kiểm tra/transaction hiện có.
- Kiểm tra lại rating, note, sourceUrl, manualFlags và mappings so với snapshot trước ghép: giữ nguyên.
- Kiểm thử `txd-repair.test.mjs`: pass.
