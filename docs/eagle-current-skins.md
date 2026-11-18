# Project Eagle hiện tại đang dùng skin có tài nguyên thế nào?

Ngày: **14/10/2026**. Đây là đợt quét **bản Eagle hiện tại**, không phải bộ skin Underground cũ. Đọc lại manifest, IDE, chỉ mục IMG và payload đang có; bao gồm ba NPC pilot đã cài. Không cài thêm/sửa game, không mở game hoặc chạy benchmark.

**Nền ped của Eagle hiện tại khá nhẹ về mesh và dung lượng.** Trong 1.676 model có asset cố định, toàn bộ có tối đa 5.000 tam giác; 1.656 cặp (98,8%) có root payload DFF+TXD ≤0,5 MiB. Với các char muốn gặp thường xuyên, nên chọn bản có tài nguyên gần nền này hoặc thử tăng theo từng nhóm.

## Phạm vi đã quét

- **1.687/1.687 ped ID** trong các IDE được manifest hiện tại khai báo: 1.676 cặp cố định đọc thành công, không có cặp thiếu/parse lỗi ngoài các slot động dự kiến.
- ID 0 `null` và 290–299 `special01`–`special10` là 11 placeholder/slot động; chưa gán một DFF/TXD tĩnh từ các tên đó. Aether được ghi riêng.
- 1.676 model gồm **1.638 model thuộc các vai trò NPC** và **38 model có pedtype PLAYER1/2**; pedtype này không xác nhận đang là nhân vật người chơi.
- Đọc đủ **2.110 cặp cùng basename** trong `COMPONENTPEDS.img`, gồm **434 cặp ngoài ModelName của IDE**, cùng 4 TXD chỉ có dictionary. Nhóm ngoài IDE có thể được script/mission/trainer yêu cầu; chưa xác nhận usage và không gọi là hiếm/không dùng.
- 61 IMG duy nhất từ 62 dòng IMG, 186 file IDE duy nhất. `CUSTOM_MODS` được khai báo lặp nên khử trùng đường archive; không tạo model trùng giả.
- Không quét riêng toàn bộ nhân vật trong `cutscene.img` (634 entries), toàn bộ các mảnh quần áo/CJ trong `player.img`, hoặc truy vết script chọn model. Thống kê này bao phủ roster ped khai báo và archive component-ped; chưa phải mọi tài nguyên nhân vật của mọi cơ chế game.

## Số liệu của 1.676 model cố định

| Chỉ số | Trung vị | P90 | Lớn nhất |
| --- | ---: | ---: | ---: |
| DFF+TXD root RW · MiB | 0,147 | 0,401 | 5,107 |
| DFF+TXD cấp phát IMG · MiB | 0,148 | 0,403 | 5,109 |
| Tam giác/model | 1.168 | 2.018 | 4.680 |
| Vertex/model | 1.154,5 | 2.038,0 | 8.202,0 |
| Texture mip/model · MiB | 0,031 | 0,251 | 4,906 |
| Material slots/model | 1 | 7 | 16 |
| Texture/model | 1 | 7 | 10 |

Tính theo member thực sự, khử trùng TXD dùng chung: **1676 DFF + 1675 TXD = 3351 member**, khoảng **332,88 MiB root payload / 336,23 MiB cấp phát IMG**. Nếu cộng cặp theo mỗi ID, TXD `lcs_chauff` dùng bởi 49229/49236 được tính hai lần; đó là tổng theo slot, không phải tổng member duy nhất.

Mọi DFF của 1.676 model có một geometry, một atomic, một skinned geometry, normals và skin header 32 bone. Đây là kiểm tra cấu trúc, chưa phải nghiệm thu bone hierarchy/weights hoặc mọi animation. Vertex lớn nhất là `MH2_SCARECROW` ID 49104: 8.202 vertex nhưng chỉ 3.408 tam giác; số tam giác thấp chưa mô tả hết công việc skinning.

## Theo vai trò và vùng bạn ưu tiên

| Vai trò | Model | Trung vị cặp RW MiB | Trung vị tam giác | Trung vị texture mip MiB |
| --- | ---: | ---: | ---: | ---: |
| Dân thường | 1105 | 0,136 | 1.113 | 0,031 |
| Gang | 324 | 0,175 | 1.334 | 0,062 |
| Cảnh sát / quân đội / cứu hộ | 136 | 0,113 | 1.096 | 0,021 |
| Criminal | 31 | 0,158 | 1.112 | 0,062 |
| Prostitute | 42 | 0,112 | 1.104 | 0,021 |
| Model có pedtype PLAYER1/2 | 38 | 0,202 | 2.109 | 0,031 |

| Tập ứng viên | Model | Tổng root cặp MiB theo slot | Trung vị cặp RW MiB | Trung vị tam giác |
| --- | ---: | ---: | ---: | ---: |
| Toàn bộ 403 slot ưu tiên | 403 | 61,42 | 0,176 | 1.024 |
| 64 slot P1/favorite | 64 | 10,00 | 0,187 | 1.042 |
| Vice City | 225 | 28,75 | 0,108 | 995 |
| Carcer City | 226 | 41,95 | 0,193 | 1.106 |
| Los Santos | 180 | 33,08 | 0,193 | 1.106 |

Các vùng dùng tập ứng viên từ báo cáo roster, **có overlap**, chưa phải danh sách model được quan sát nạp ở từng thành phố. Không cộng ba hàng vùng thành tổng skin hoặc coi số liệu này là mật độ/tần suất NPC.

## So với bộ skin cũ

Đối chiếu **1.676 basename nguồn cũ trùng các model Eagle có asset**, thay vì lấy cả 1.721 mẫu cũ có phạm vi khác. Tên trùng chỉ là counterpart filename; không xác nhận char hoặc quyết định dùng lại.

| Chỉ số trung vị | Eagle hiện tại | Nguồn skin cũ trùng basename |
| --- | ---: | ---: |
| DFF+TXD · MiB | 0,148 cấp phát IMG | 2,914 file nguồn |
| Tam giác/model | 1.168 | 19.899 |
| Texture mip/model · MiB | 0,031 | 1,502 |

Trung vị tam giác nguồn cũ khoảng **17,0 lần** Eagle; texture mip khoảng **48,1 lần**. Đây là tỷ số phân bố tài nguyên, **không phải tỷ số FPS/VRAM runtime**. MiB cấp phát Eagle có padding, byte nguồn cũ lấy metadata RAR; báo cáo không coi hai phép đo file là đồng nhất.

Bản nhẹ cho char phổ biến vẫn nên ưu tiên ≤5.000 tam giác, xem thêm vertex/material, và khoảng ≤1 MiB texture mip để review trước. Mức 5.000 vẫn cao hơn trung vị Eagle vài lần; cần đo khi nhân nhiều instance. Với skin đẹp nhưng mesh 15.000–25.000 tam giác, giảm TXD không giảm chi phí geometry; tìm version mesh nhẹ hoặc thử ít slot trước.

## Texture hiện tại

Có **4.019 texture entries** trong 1.675 TXD duy nhất: **3.718 (92,5%)** có cả hai chiều ≤256. Một số model dùng texture lớn hơn; đọc từng texture thay vì chỉ nhìn dung lượng cặp.

| Format | Texture entries | Tổng mip payload MiB |
| --- | ---: | ---: |
| DXT1 | 3.565 | 92,94 |
| uncompressed-32 | 407 | 74,53 |
| DXT3 | 30 | 0,81 |
| DXT5 | 15 | 0,03 |
| DXT4 | 2 | 0,0007 |

Tổng mip ở bảng trên khử trùng theo TXD archive member, chưa khử trùng các ảnh giống nhau nằm ở hai TXD khác ID. Không suy ra mức VRAM còn trống, residency hoặc FPS từ tổng byte. Mip count/dimensions/format của từng ảnh có trong JSON. Bảng dùng FOURCC DXT trước depth header; mask tên trong DFF được ghi riêng, không yêu cầu thành một native texture khác trong TXD.

## Ngoại lệ lớn và ba skin đã thay

| ID / model | Cặp RW MiB | Tam giác | Texture mip MiB |
| --- | ---: | ---: | ---: |
| 48048 / `VCS_CS_RENOP` | 5,107 | 2.038 | 4,906 |
| 48111 / `VCS_MENDEZ2` | 4,897 | 2.034 | 4,703 |
| 48110 / `VCS_MENDEZ1` | 4,887 | 1.936 | 4,703 |
| 48046 / `VCS_CS_PED1` | 4,825 | 1.926 | 4,641 |
| 48043 / `VCS_CS_LOUISE3` | 4,540 | 1.954 | 4,344 |
| 48041 / `VCS_CS_FORBES` | 4,404 | 2.004 | 4,203 |
| 48049 / `VCS_CS_TROY` | 3,879 | 1.970 | 3,688 |
| 48047 / `VCS_CS_PHCOLLINS2` | 3,449 | 2.020 | 3,250 |

Những cặp lớn nhất trong bảng này chủ yếu lớn ở TXD; không tự gọi là NPC hiếm theo tên `CS` hoặc kích thước file. Mesh nhiều tam giác nhất là `LC_MARIA` ID 49265 (4.680), rồi `LC_CURLY` ID 48439 (4.248) và `LC_TONY` ID 48518 (4.060).

| ID / slot hiện tại | Nhãn nguồn đã thay | Cặp RW MiB | Tam giác | Texture mip MiB |
| --- | --- | ---: | ---: | ---: |
| 280 / `lapd1` | ReiAyanami2 | 0,130 | 1.601 | 0,016 |
| 285 / `swat` | hanekawa | 0,356 | 3.622 | 0,125 |
| 287 / `army` | senjo | 0,360 | 3.696 | 0,125 |

Cảnh sát và SWAT LS đã được người dùng báo hoạt động ổn. Army đã cài nhưng chưa có báo cáo runtime. Số liệu census đọc đúng payload pilot trong chỉ mục hiện tại, không dùng offsets của backup trước cài.

Aether có **2,281 MiB cặp file, 17.706 tam giác, 15.487 vertex và 1,250 MiB texture mip**, ghi ngoài 1.676 cặp tĩnh. `default.dat` khai báo `modloader.img`; toàn bộ byte loose AETHER.dff/TXD khớp prefix của member trong IMG, phần dư chỉ là padding zero. DFF có đuôi 35.087 byte sau root RW. F2 đã được người dùng thử; ID 0 vẫn là placeholder, không phải khai báo `AETHER` trong IDE. Cờ `gta3.std.stream=0` đang tắt nên không quy mọi file loose thành override đã hoạt động.

## 434 cặp component ngoài ModelName của IDE

Đã đọc đủ 434 cặp này: trung vị **0,187 MiB/cặp**, **1.323 tam giác**, lớn nhất **4.054 tam giác**. Chúng có tài nguyên thật trong archive, nhưng cần truy vết script/trainer/mission để biết usage.

Toàn bộ **2.110 cặp cùng basename** có tổng khoảng **419,07 MiB root RW / 423,40 MiB cấp phát IMG**. Phần này chứa các actor đã thống kê ở trên, nên không cộng hai tổng. Kích thước file archive còn bao gồm directory, alignment và dữ liệu cũ không được index trỏ tới sau thao tác append pilot.

Không trộn 434 cặp đó với số slot cần thay. Tính toàn bộ 2.110 cặp cùng basename cũng khác việc ghép DFF với TXD theo IDE: có model khai báo TXD khác tên và dictionary được dùng chung. Bốn TXD-only stems là `bluebl`, `bluebr`, `vc_soonygoona`, `vc_soonygoonb`; chỉ thiếu DFF cùng tên chưa có nghĩa dictionary lỗi hoặc không dùng.

## Các giới hạn và dữ liệu để kiểm tra

Có 16 cặp actor có dữ liệu nonzero sau root chunk (15 DFF và 2 TXD theo member). Do không có độ dài file nguồn chuẩn cho các member gốc, root bytes là phần kê khai/lower bound, IMG bytes là cấp phát; không đặt tên mọi phần đuôi là padding. 8 actor còn thiếu tên texture trực tiếp sau khi tách mask; nếu có, cần kiểm tra resolver/parent/global trước khi coi là lỗi.

Các tên chưa thấy trực tiếp trong TXD khai báo, để kiểm tra khi review/gameplay:

| ID / model | Tên texture |
| --- | --- |
| 48094 / `VCS_HIGH_EMPB` | gang9b_trousers |
| 48120 / `VCS_VICE1` | vice2_shoe |
| 48227 / `LCS_NED_01` | ciggie |
| 48664 / `BW_N_BUCKY` | ndh3_bucky_glasses_d |
| 48760 / `MW_BIKER01` | wmycr |
| 48909 / `sfpdh1` | sfpd1 |
| 49137 / `UL_BMYMECH` | sweet |
| 49236 / `LCS_JDMADE` | ig_otoole_head, ig_otoole_suit |

Bảng này không kết luận skin bị lỗi; chưa truy vết TXD parent/global hoặc alias trong runtime.

Asset có file, khai báo được nạp và model thực sự đang cư trú/vẽ là các mức bằng chứng khác nhau. Để biết game đang tiêu tốn bao nhiêu khi road trip, cần đo GPU/working set/frametime và model usage trong cùng cảnh. Thống kê lần này chưa đo các yếu tố đó.

- [Tài nguyên theo đủ 1.687 ID](eagle-current-ped-resources.md).
- [JSON thống kê đã tổng hợp, cohort/vùng/vai trò](evidence/eagle-current-skin-summary.json).
- [Census đầy đủ: archive, offset, hash, geometry và texture từng ảnh](evidence/eagle-current-skin-census.json), [báo cáo census](evidence/eagle-current-skin-census.md).
- [Đường nạp hiện tại, Aether và phạm vi ngoài IDE](evidence/eagle-current-loading-context.md), [JSON bằng chứng](evidence/eagle-current-loading-context.json).
- [Báo cáo nguồn skin cũ và ngân sách mod](skin-resource-budget.md).
- Scripts: `staging/project-eagle/skin-budget/inspect_eagle_current.py`, `evidence/build_eagle_skin_summary.py`.

Kiểm tra bổ sung: geometry/vertex/material của ba pilot và ba mẫu cực trị khớp parser sâu độc lập. Bảng đủ 1.687 ID và tổng cohort 403/64 đã đối chiếu; SHA256 COMPONENTPEDS và cặp Aether khớp trạng thái cài trước khảo sát. [Bằng chứng kiểm tra](evidence/eagle-current-skin-verification.json).
