# Crash animation sau lần sửa định dạng RenderWare

Log gốc mới `2026-10-22_04-59-01.log` và attachment d83fc40c: EIP `0x004D0752`, `CAnimBlendNode::Update`, đọc `[ebx+4]` với EBX `0x36`. Đọc tĩnh executable thực tế xác nhận EBX được lấy từ trường con trỏ sequence của animation node (`[edi+0x10]`), không phải chỉ số bone 54. `discord-ipc-9` chỉ là file/pipe mở sau cùng, không xác định nguyên nhân crash. Log thứ hai khi shutdown được tách khỏi lỗi này.

## Sai khác xác định được

Bản sửa trước đã xử lý wire format RW/D3D nhưng chưa chuyển rig VC sang rig SA. Evelyn đang gán NPC 7 `male01` cùng ba model cũ khác vẫn dùng HAnim/Skin **24 khớp**, còn toàn bộ baseline NPC dùng **32 khớp**. Khảo sát toàn bộ nguồn build: 1.201 đường dẫn DFF có 32/32; chỉ bốn đường dẫn cũ có 24/24. Không tìm thấy HAnim/Skin lệch số khớp hoặc vượt giới hạn mảng 64 trong khảo sát này.

`male01` còn được dùng làm mẫu animation chung. Trong executable, `ReadAnimAssociationDefinitions` tại `0x5BC990` thực sự `push 7` trước khi gọi `AddAnimAssocDefinition` tại `0x5BC99C`. Mã animation tạo association theo skeleton mẫu rồi sao chép association vào clump đích, trong khi vòng cập nhật chạy theo số khớp của clump đích. Mẫu 24 và đích 32 tạo đường đọc vượt mảng; đây là cơ chế phù hợp với con trỏ sequence rác trong crash. Chưa có memory dump đủ để xác định chính xác instance NPC đang cập nhật, nên không gán tên thủ phạm từ dòng streaming cuối.

Tham chiếu mã cộng đồng: [AnimManager](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Animation/AnimManager.cpp), [AnimBlendAssociation](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Animation/AnimBlendAssociation.cpp), [RpAnimBlend](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Plugins/RpAnimBlendPlugin/RpAnimBlend.cpp). Snapshot byte/lệnh của executable đang cài nằm trong `evidence/crash-animation-rig-2026-10-22/static-exe.json`; không vá executable hay ASI.

## Chuyển rig trong bản build

`tools/skin-viewer/sa_ped_rig.py` chỉ nhận layout VC 24 khớp có danh sách ID chính xác đã nhận diện; không đoán cách chuyển skeleton bất kỳ:

- Chuyển HAnim sang thứ tự/flags 32 khớp của `male01` baseline. Hai toe tag 2000/2001 đổi sang 44/54.
- Thêm tám khớp thiếu không có đỉnh được gắn trọng số: jaw/brow, đầu ngón tay và các khớp phụ. Inverse bind của khớp thêm lấy theo parent; frame local là identity.
- Chuyển hai thigh từ parent Spine sang Pelvis như SA, nhân bù local matrix để giữ nguyên world matrix ở bind pose.
- Remap chỉ mục đỉnh, used-bones và vị trí inverse-bind theo thứ tự mới. Không đổi tọa độ, UV, triangles, material, texture hay giá trị trọng số; 24 ma trận inverse-bind gốc được giữ nguyên theo bone tương ứng.
- Chỉ tạo tài nguyên dẫn xuất trong `sa-compatible` ở thư mục build ổ D. Không thay file thư viện, đánh giá hay mapping.

Bốn nguồn tương ứng bảy NPC: Evelyn (7, 48897), player4 (165, 48574), Yanagi (48105, 48570), Grace Howard (49165). Các model 32 khớp khác không bị sửa bởi bộ chuyển này.

## Kiểm tra

18 lượt unittest của bộ chuyển rig/định dạng và build/ghép TXD/apply/restore đã qua. Kiểm tra độc lập bằng DFFReader JavaScript trên bốn nguồn thật xác nhận geometry/material/UV/morph bằng nhau, weights bằng nhau, toàn bộ chỉ mục đã remap đúng, 24 inverse-bind gốc bằng nhau theo tag, preview parse được. Sai khác world matrix tối đa dưới `3e-8` sau bù parent. Script và kết quả: `tools/skin-viewer/qa-data/crash-animation/verify-rig.mjs` và `rig-verification.json`.

Metadata trước sửa và crash được giữ tại `evidence/crash-animation-rig-2026-10-22/`. Baseline IMG nguyên gốc vẫn là bản phục hồi của viewer. Các kiểm tra trên không thay cho nghiệm thu animation trong game.

## Triển khai

Đã build thành công lúc **05:20:05 ngày 22/10/2026** và áp dụng lúc **05:29:52** (giờ Việt Nam), đủ 1.638 mapping. SHA-256 IMG đã cài được transaction kiểm tra: `9bf8f76c59167c3664f187083d2b951213bf69ce7dc6f242c7706dbdefbf37e2`.

Sau cài đã đọc trực tiếp bảy DFF trong IMG: hash khớp build, HAnim/Skin đều 32/32. Baseline đúng hash; không còn transaction, operation lock hoặc file `.viewer-new`/`.viewer-rollback`. Toàn bộ `reviews.json` khớp snapshot trước sửa. Mã kiểm rig cũng đã chạy lại trên cả 1.205 DFF của build và không tìm thấy chuyển đổi còn thiếu; trường hợp VC rig có version tag hiện đại được xử lý ở các build sau, không bị bỏ qua chỉ vì header mới.

Bằng chứng: `evidence/crash-animation-rig-2026-10-22/applied-verification.json`, `candidate-members.json`, `built-rig-idempotence.json`, và [khảo sát rig trước sửa](evidence/crash-animation-rig-audit-2026-10-22.md).

**Chưa nghiệm thu trong game:** người dùng cần load save/New Game để xác nhận đã qua crash và kiểm tra chuyển động. Không khẳng định toàn bộ crash đã hết chỉ từ kiểm tra binary.
