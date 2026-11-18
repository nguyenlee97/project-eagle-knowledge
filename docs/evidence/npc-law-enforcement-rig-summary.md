# Kiểm tra rig NPC law-enforcement cho Eagle

Ngày kiểm tra: 13/10/2026. Đã đối chiếu ba cặp model lịch sử đang có trong staging với đúng model đích của Eagle `COMPONENTPEDS.img`, rồi chuẩn bị bản sao mang basename đích trong staging riêng. Game, IMG và nguồn RAR giữ nguyên; không mở game.

## Basename đích

Catalog Eagle xác nhận `lapd1` (ID 280, dòng 321 `peds.ide`) là COP của Los Santos; `swat` (ID 285, dòng 330) và `army` (ID 287, dòng 332) đều là COP với animation group `swat`. `lapd1` là selector của Los Santos; `swat` và `army` dùng chung cho mainland CS/LS/SF/LV. Danh sách này được giữ làm bộ LS/mainland staging tham khảo. Tình trạng mới nhất chỉ ra người dùng đang ở Carcer City; catalog chưa tìm thấy wanted selector Carcer, nên không dùng các basename LS này như target Carcer. Xem [npc-carcer-target-rig-summary.md](npc-carcer-target-rig-summary.md).

| Basename Eagle | Ped ID / dòng | DFF Eagle | TXD Eagle | Vertices / triangles |
|---|---:|---:|---:|---:|
| `lapd1` | 280 / 321 | 73,477 B | 16,552 B | 888 / 1,034 |
| `swat` | 285 / 330 | 80,606 B | 131,240 B | 1,019 / 1,050 |
| `army` | 287 / 332 | 73,925 B | 131,240 B | 919 / 976 |

## Các cặp tạm đã chuẩn bị

| Tên mapping lịch sử | Basename Eagle đề xuất | Pair DFF+TXD | Vertices / triangles | Kiểm tra tĩnh |
|---|---|---:|---:|---|
| ReiAyanami2 | `lapd1` | 136,298 B | 1,553 / 1,601 | 32-bone skin hợp lệ, texture đủ, không trailing data |
| hanekawa | `swat` | 372,770 B | 3,113 / 3,622 | 32-bone skin hợp lệ, texture đủ, không trailing data |
| senjo | `army` | 377,322 B | 3,154 / 3,696 | 32-bone skin hợp lệ, texture đủ, không trailing data |

Các tên nguồn lấy từ các mapping cũ trong audit NPC; không có URL nguồn trong các bản ghi đã audit và chưa kiểm tra hình ảnh. Chúng là nhãn lịch sử, không phải xác nhận visual. Cả ba cặp đều đã được so byte/hash với IMG payload Underground theo chiều dài source chính xác, bỏ sector padding; CRC32 khớp metadata RAR ở audit trước.

Ba DFF có cùng 33 frame, cùng 32 bone IDs, cùng hierarchy số và cùng quan hệ bone cha gần nhất với model Eagle tương ứng. Tên frame UpperArm, ForeArm, Hand, Finger và Finger01 cùng bone ID/parent cũng khớp target. Ba skin có influence hợp lệ, tổng weight đạt tolerance, không invalid index, zero weight, non-finite hoặc negative weight; các material texture names đều có trong TXD. Đây là bằng chứng phù hợp cho rig cơ bản, gồm cấu trúc tay/bàn tay cần khi cầm vũ khí. Không thử pose cầm súng, reload, đánh nhau hoặc bất kỳ animation nào trong game.

Bản sao để review trước khi parent xử lý backup/install nằm tại `staging\project-eagle\law-enforcement\ready`. JSON có manifest riêng cho mỗi file: đường dẫn/member RAR nguồn, SHA-256 và size nguồn, member gốc chính xác trong Eagle `COMPONENTPEDS.img`, hash/size của DFF/TXD gốc Eagle, hash/size của bản staging, cùng SHA-256 của hợp đồng rig so sánh:

- `lapd1.dff` / `lapd1.txd` ← ReiAyanami2
- `swat.dff` / `swat.txd` ← hanekawa
- `army.dff` / `army.txd` ← senjo

Chọn vùng muốn thử vẫn cần căn theo selector wanted của thành phố; báo cáo này chưa khẳng định tần suất spawn, hành vi wanted thực tế, hay ngoại hình của các tên lịch sử.

Evidence chi tiết: [npc-law-enforcement-rig-audit.json](npc-law-enforcement-rig-audit.json). Script kiểm tra/staging: [inspect_targets.py](../../../staging/project-eagle/law-enforcement/inspect_targets.py).
