# Skin Viewer: ghép TXD chung có MatFX

## Lỗi và bản sửa

Build trên gameplay-lab bị chặn ở NPC 49229 (`LCS_CHAUFF`, Shinji Ikari) và NPC 49236 (`LCS_JDMADE`, Yukino Shichido), cùng dùng `lcs_chauff.txd`. `rewrite_dff` trước đây chủ động từ chối mọi material MatFX đang bật vì chưa đổi tên texture nằm bên trong hiệu ứng.

Đã sửa `tools/skin-viewer/shared_txd.py`: đọc có kiểm biên header và hai slot MatFX theo [librw readMaterialMatFX](https://github.com/aap/librw/blob/master/src/matfx.cpp), đối chiếu [DragonFF](https://github.com/Parik27/DragonFF/blob/master/gtaLib/dff.py). Hỗ trợ bump, env, dual, UV transform và hai kiểu kết hợp chuẩn; texture/mask bên trong được đổi tên theo cùng namespace như texture chính. Giữ nguyên coefficient, framebuffer-alpha, blend mode và plugin khác; cập nhật kích thước chunk cha. Loại lạ, layout không khớp, dữ liệu thiếu/vượt biên hoặc dư chưa hiểu vẫn bị từ chối. Atomic MatFX flags không bị coi nhầm là material effect.

Shinji thực tế có năm material MatFX env-map với tên `nah`/`hh`. Hai tên này không nằm trong TXD nguồn của Shinji, nên được giữ nguyên theo nguồn, không tự tạo texture hoặc nhận nhầm texture từ skin còn lại. Cả năm payload MatFX giữ byte nguyên vẹn trong trường hợp này. Texture có trong TXD nguồn vẫn được đổi namespace bình thường. Tên chưa tìm thấy trong nguồn không phải do lượt ghép tạo ra; chưa đánh giá lại hiệu ứng phản chiếu trong game.

## Kiểm tra và phạm vi

- 22 lượt unittest qua, bao gồm MatFX modes 0–6, đổi texture/mask lồng trong hiệu ứng, giữ byte thông số, kiểm độ dài chunk và từ chối input lỗi. Test build/apply/restore trên game giả có MatFX đồng thời kiểm mirror sang GROUP_A.
- Chạy đúng `assemble_shared` rồi `assemble_compatible` trên hai skin đang gán, dùng TXD baseline thật, chỉ xuất staging riêng. Kết quả: giữ 5 texture baseline, thêm 54 texture, tổng 59; đổi tên 59 tham chiếu ở hai DFF.
- Reader JavaScript độc lập đọc lại hai DFF sau ghép: geometry/UV/triangles/morph/Skin/HAnim/frame giữ nguyên so với nguồn. Hash bốn DFF/TXD nguồn không đổi.
- Bằng chứng và bản sao code trước sửa: `tools/skin-viewer/qa-data/shared-matfx-20261022/`, gồm `pipeline-verification.json` và `independent-reader.json`.

Không thay archive game, metadata deployment, mapping hoặc đánh giá. Không tự chạy full IMG build/apply trong lượt sửa này. Viewer gọi Python mới cho từng job nên không cần khởi động lại server: người dùng bấm **Build** lại với nháp hiện tại, sau đó **Áp dụng** khi build thành công. Target tiếp tục là gameplay-lab. Tương thích MatFX trong chuyển wire format legacy RW 3.3 vẫn theo guard riêng, không được mở rộng bằng thay đổi này.

## Bàn giao

Không nhận khóa ghi chung vì chỉ sửa source và tạo staging độc lập; không ghi runtime/deployment. Backup source nằm trong staging (`*.before`); phục hồi source chỉ khi hash bản hiện tại vẫn khớp lượt sửa này để không ghi đè người chỉnh sau. Phiếu: `work-items/2026-10-22-codex-shared-txd-matfx.md`.
