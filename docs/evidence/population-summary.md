# Project Eagle population evidence

Khảo sát chỉ đọc ngày 13/10/2026 trong thư mục Eagle đã chọn. Không launch game, sửa file game, mở archive hay thử spawn. [population-catalog.json](population-catalog.json) là bản kiểm kê đầy đủ; [population_inventory.py](population_inventory.py) tái tạo JSON từ các tệp text.

## Pedestrian groups

Parser ghi mọi dòng dữ liệu, kể cả dòng chỉ có một model token; mỗi record giữ `row_index`, `row_index_within_group_label`, source line, raw comment, danh sách member có lặp và group label. Các hậu tố `(SF)`/`(VEGAS)` trong inline label được giữ nguyên. Những file dùng heading riêng giữ qualifier đúng như source nếu có; vị trí dòng trong group giúp phân biệt các row song song mà source không gắn hậu tố.

| Tệp | Data rows | Members có lặp | Unique model names | Unlabelled rows |
|---|---:|---:|---:|---:|
| `pedgrp.dat` | 57 | 470 | 218 | 0 |
| `pedgrp_at.dat` | 57 | 396 | 198 | 0 |
| `pedgrp_bw.dat` | 57 | 308 | 188 | 0 |
| `pedgrp_cc.dat` | 57 | 477 | 226 | 0 |
| `pedgrp_cm.dat` | 57 | 396 | 198 | 0 |
| `pedgrp_lc.dat` | 57 | 465 | 195 | 0 |
| `pedgrp_mll.dat` | 57 | 358 | 181 | 0 |
| `pedgrp_vc.dat` | 57 | 687 | 206 | 0 |

Các số được tính trực tiếp từ dòng dữ liệu, giữ các model trùng lặp; unique count là trong phạm vi từng file. JSON có tổng và breakdown theo group cho mỗi file. Tên hậu tố vẫn là key cấu hình, không tự gán thành khu vực runtime. Một số group có model names chỉ một lần hoặc các dòng không có dấu phẩy; parser giữ nguyên và tính vào số liệu.

Trong file cơ sở `data/pedgrp.dat`, civilian examples và source lines là: Workers `:8`; Business `:12`; Clubbers `:16`; Casual Rich `:28`; Casual Average `:32`; Casual Poor `:36`; Criminals `:45`; gangs `:69-87`; Dealers `:89`; Wives `:97`. Các nhóm và member đầy đủ nằm trong JSON theo từng tệp, không chỉ ở file cơ sở.

## Candidate pilot BFYST và WFYST

`BFYST` và `WFYST` đều xuất hiện ở `POPCYCLE_GROUP_CASUAL_AVERAGE` của file cơ sở, dòng 32. `data/peds.ide:51` mô tả BFYST là `CIVFEMALE`, `STAT_STREET_GIRL`, voice `VOICE_GEN_BFYST`; `:131` mô tả WFYST cũng là `CIVFEMALE`/`STAT_STREET_GIRL`, voice `VOICE_GEN_WFYST`. Đây là config/metadata, không phải thử nghiệm giọng runtime.

Blast radius theo các `pedgrp` đang có:

- BFYST có 16 occurrences: tại `pedgrp.dat`, `pedgrp_at.dat`, `pedgrp_cc.dat`, `pedgrp_cm.dat`, dòng 32 (Casual Average), 34 (Casual Average (VEGAS)), 36 (Casual Poor), 38 (Casual Poor (VEGAS)) trong từng file. Không tìm thấy token BFYST chính xác trong `_bw`, `_lc`, `_mll`, `_vc`.
- WFYST có 40 occurrences. Nó xuất hiện ở Clubs dòng 16 và 18 (VEGAS); Casual Average dòng 32 và 34 (VEGAS); Casual Poor dòng 36 và 38 (VEGAS), mỗi dòng hai lần; và Wives dòng 97 trong `pedgrp.dat`, `_at`, `_cc`, `_cm`. Ngoài ra nó nằm ở Clubbers rows 22 và 24 trong `_bw`, Wives dòng 97 trong `_lc`, và Wives dòng 93 trong `_vc`. Tất cả source line, row index và vị trí member đều có trong `candidate_memberships` của JSON.
- Cả hai cũng có mặt trong một số group `Casual Poor`, không chỉ Casual Average. WFYST có thêm Clubbers và Wives roles. Không thấy hai token chính xác trong group Gang hay Dealers trong các danh sách đã parse. Các model variants như `SBFYST`, `SWFYST`, `VCS_BFYST`, `VC_WFYST` là model names khác và được giữ riêng.

Trong `peds.ide`, các biến thể có tên chứa BFYST/WFYST khác còn có ID và role riêng (ví dụ SBFYST ID 69 ở dòng 107; SWFYST ID 233 ở dòng 271; VCS_BFYST ID 48023 ở dòng 366; VCS_WFYST ID 48136 ở dòng 479; VC_BFYST ID 48268 ở dòng 611; VC_WFYST ID 48387 ở dòng 730). `pedcols.dat:265,283` có color rows cho VCS_BFYST/VCS_WFYST; không có row tên chính xác BFYST/WFYST. Những entry này có thể ảnh hưởng appearance của model variants tương ứng, không chứng minh chúng được chọn bởi population file nào.

Đã tìm tên BFYST/WFYST trong `pedstats.dat`, `pedtype.dat`, `variation.dat` và `model_special_features.dat`; không thấy dòng match trực tiếp. `pedstats`/`pedtype` có schema dùng chung nhưng không liên kết hai model bằng tên trong nội dung hiện tại. Tài liệu JSON lưu tất cả dòng match từ `peds.ide` và `pedcols.dat`.

## Popcycle

`data/popcycle.dat:1-13` mô tả zone population type, 12 khung giờ cách nhau 2 giờ cho weekday và weekend, các cột Peds/Cars, hệ số Dealers/Gang/Cops/Other, rồi các phần trăm thành phần `Other` (comment nói các phần này cần tổng 100%). Header tại dòng 20 nêu 24 trường; header spellings được giữ trong JSON, gồm typo nguồn `Crimimals`. Parser giữ đúng thứ tự header và số nguyên thực tế trong từng record, không tự tính xác suất spawn.

Catalog parse đủ **20 type blocks**, **480 numeric rows**, mỗi block có 12 weekday + 12 weekend rows, mỗi row 24 trường. Không có schema anomalies. Mỗi record có block ordinal, type label, schedule, index 0–11, nhãn giờ từ comment, source line, numeric values theo tên cột và raw line. Header labels gồm Business, Desert, Entertainment, Countryside, Residential Rich/Average/Poor, Gangland, Beach, Shopping, Park, Industry, Entertainment Busy, Shopping Busy, Shopping Posh, Residential Rich Secluded, Airport, Golf Club, Out-of-Town Factory và Airport Runway. Header/bảng đầy đủ theo line được giữ trong JSON. Các giá trị cấu hình không phải tần suất model đã quan sát trong game.

## Zone files và manifest

Manifest được chọn là `data/gta.dat`. Ba tệp `S&S/ZON/map.zon`, `info.zon`, `weather.zon` được khai báo lần lượt tại `data/gta.dat:295-297`, và saved `modloader/modloader.log:309-311` ghi chúng được nạp như default scene. Chúng có `active_manifest: true` trong JSON. `S&S/ZON/map.zon:14-15` ghi LA01/LA02 và region field `1`; các region tiếp theo cũng được lưu từng dòng raw.

`data/map.zon` và `data/info.zon` không được khai báo trong `data/gta.dat`; chúng chỉ được tham chiếu bởi alternate manifests `data/gta4.dat:162,164` và `data/gta_quick.dat:31,33`, nên được đánh dấu inactive đối với manifest đã chọn. `data/weather.zon` cũng không được khai báo trong selected manifest; không tìm thấy mount reference trong hai alternate manifests vừa nêu. JSON phân biệt presence, active manifest state và mount source refs cho cả sáu file. `data/gta.dat` không có mount record cho các tệp `pedgrp*.dat`; do vậy runtime group file selection vẫn chưa xác minh.

`PECore.ini:21` bật `ZoneEx`, `:119` đặt `PedPopulationMult=1.5`, và `PECore.log:29` ghi ZoneEx initialized. `PECore.log:107-123` mô tả index của GangWars (navzones/info slots/city counts), không phải số hoặc phân bố pedestrian. Local changelog `data/Changelog.txt:108` tuyên bố mỗi area có pedestrian group phù hợp, `:188` ghi popcycle density được tăng; changelog PE 1.3 công khai cũng nêu zone fix, density settings và `popcycle.dat` update: [Project Eagle PE 1.3 changelog](https://www.projecteaglemod.games/changelog/pe-1.3.0). Đây là mô tả sản phẩm, không thay cho bằng chứng về từng mapping trong runtime.

## Ranh giới của kết luận

Đã xác nhận riêng ba lớp cấu hình: zone/region descriptors; popcycle type/time rows; và các danh sách model theo group. Text files hiện có không cung cấp một bảng nối tường minh `zone/coordinates -> popcycle type -> pedgrp filename/group row`. Do đó không gán chắc BFYST/WFYST hoặc một file hậu tố nào vào một khu phố Los Santos. Catalog cũng không suy ra xác suất từ vị trí model trong list, không coi tên model có trong group là bằng chứng chắc chắn nó spawn, và không xác nhận appearance/voice thực tế.

