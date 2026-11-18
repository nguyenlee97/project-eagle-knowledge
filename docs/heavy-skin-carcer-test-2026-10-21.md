# Thử 10 skin tối ưu tại Carcer City — 21/10/2026

Đã áp dụng 10 skin tối ưu vào game. Tổng DFF+TXD: 488.45 → 103.50 MiB; giảm 78.81%. Giữ nguyên độ phân giải, geometry/rig và file gốc.

| Skin / bản tối ưu | Trước → sau (MiB) | NPC ID / model | Nhóm thử |
|---|---:|---|---|
| Ikuyo Kita / #3248 | 90.45 → 17.80 | 48523 `CC_CCPD1` | CC cảnh sát / SWAT (dispatch cần thử) |
| Ororon / #3249 | 50.29 → 8.29 | 48524 `CC_CCPD2` | CC cảnh sát / SWAT (dispatch cần thử) |
| Kinich / #3250 | 50.21 → 8.21 | 48578 `CC_SWAT` | CC cảnh sát / SWAT (dispatch cần thử) |
| ellen / #3251 | 50.03 → 10.03 | 40 `HFYRI` | Ngoài đường, có trong pedgrp_cc.dat |
| Koleda / #3252 | 49.78 → 7.78 | 46 `HMYRI` | Ngoài đường, có trong pedgrp_cc.dat |
| Noa / #3253 | 49.54 → 7.54 | 12 `BFYRI` | Ngoài đường, có trong pedgrp_cc.dat |
| Narita Brian / #3254 | 45.37 → 12.12 | 93 `WFYST` | Ngoài đường, có trong pedgrp_cc.dat |
| Castorice / #3255 | 35.42 → 9.58 | 60 `OMYST` | Ngoài đường, có trong pedgrp_cc.dat |
| Fuuka Yamagishi / #3256 | 33.97 → 5.08 | 147 `WMYBU` | Ngoài đường, có trong pedgrp_cc.dat |
| Cyrene / #3257 | 33.40 → 17.06 | 91 `WFYRI` | Ngoài đường, có trong pedgrp_cc.dat |

Cách thử: khởi động lại game, vào Carcer City, đi/lái xe qua vài khu rồi thử tăng truy nã. Quan sát mặt/tóc/viền alpha từ gần và xa, animation đi/chạy/cầm súng, giật khi model xuất hiện, texture biến mất hoặc crash. Ba service slots có tên CC và COP/EMG trong IDE; chưa xác nhận bộ dispatch gọi đúng các ID này khi tăng truy nã. Bảy slot thường có cấu hình population Carcer City; vì dùng chung model nên các vùng khác cũng có thể đổi.

Đây là thử nghiệm các bản đã tối ưu, chưa có phép đo FPS/RAM trong game hoặc benchmark A/B với bản gốc. Không tự kết luận mức giảm file là mức giảm RAM/FPS tương ứng. Các cảnh báo thiếu texture sẵn có của nguồn được giữ nguyên, không phát sinh cảnh báo mới qua parser.

Cách so trong viewer: bỏ bộ lọc cũ, chọn Mapping phiên bản → Đã gán. Mỗi skin có dropdown bản gốc và bản “Tối ưu DXT • giữ độ phân giải • thử Carcer 21/10”. NPC: bỏ lọc khu vực, chọn Mapping NPC → Đã gán để thấy đủ 10 slot (3 service slots chưa có liên kết vùng trong metadata).

## Phục hồi

Tắt game, trong viewer mở Build & áp dụng vào game → Phục hồi trước viewer. Bản nháp được giữ; file thư viện gốc và bản tối ưu đều được giữ. Thao tác này trả IMG về snapshot ngay trước bài thử này, bao gồm các thay đổi cũ đã tồn tại lúc snapshot.

Backup: `C:\Users\LENOVO\Desktop\GTA\Skin Library\Project Eagle\numbered-skins\deployment\baseline`. Snapshot mapping trước thử: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\heavy-skin-test-2026-10-21\mappings-before.json`. Chỉ archive `S&S/Cdimages/default/COMPONENTPEDS.img` được thay đổi.

## Kiểm tra đã làm

- Hash IMG sau áp dụng trùng candidate; 20 payload DFF/TXD trong IMG trùng hash nguồn mới.
- Baseline immutable trùng hash ban đầu; toàn bộ 10 DFF và 10 TXD gốc giữ nguyên hash.
- DFF không chỉnh sửa. Số đỉnh/tam giác/texture và danh sách cảnh báo của 10 model giữ nguyên khi dựng bằng parser với TXD mới.
- Kiểm thử roundtrip nén alpha qua texconv đạt; 5 kiểm thử deployment/rollback đạt.
- Mức PSNR tối thiểu theo từng texture trong nhóm: 37.04 dB; đây chỉ là chỉ số sai khác ảnh, không thay cho đánh giá ngoại hình/alpha trong game.

## Phương pháp và nguồn

Microsoft DirectXTex texconv may2026, binary SHA256 `dcfdec10244e02cf5037fba089c55fb7e1326b1c8181742d77d15fa5cb5eef06`, chữ ký Microsoft hợp lệ. DXT1 cho texture hoàn toàn opaque; DXT5 khi có alpha; giữ texture đã nén. Không đổi độ phân giải hoặc số mip level; raster nén mới có mức mip phụ được texconv tạo lại khi nguồn có nhiều mip. Không tối ưu skin Rất thích; không đưa skin bị loại vào thử.

[Tài liệu texconv của Microsoft](https://github.com/microsoft/DirectXTex/wiki/texconv). Tệp đầy đủ: `registered.json`, `deployment-plan.json`, `deployment-build.json`, `deployment-apply.json`, `post-install-verification.json` trong staging bài thử.
