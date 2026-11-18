# Danh sách ped ID cần xem xét thay skin — Project Eagle

Cập nhật: **2026-10-14**. Phạm vi: lập danh sách; không cài thêm, không tìm/check thêm skin cũ, không sửa game.

**Đã rà đủ 1.687 ID trong IDE được manifest Eagle khai báo. Có 403 ID ứng viên cho ba vùng ưu tiên và 64 slot dân sự nên xem trước để dành cho nhân vật yêu thích.** Danh sách không bắt buộc thay toàn bộ 403 ID trong một lượt.

Bổ sung 14/10: [phân tích dung lượng/mesh/texture và ngân sách skin](skin-resource-budget.md), cùng [125 mẫu nguồn ít tài nguyên nên review trước](skin-review-shortlist.md). Bảng ID và cột char chưa bị thay đổi; basename cũ chỉ là đầu mối tìm skin.

Đã bổ sung [thống kê tài nguyên Eagle hiện tại](eagle-current-skins.md) và [bảng theo đủ 1.687 ID](eagle-current-ped-resources.md) để xem asset đang có trước khi chọn bản thay thế.

Đã nhập đánh giá gallery vào [pool hiện tại và số thiếu](skin-pool-plan.md): còn 236 skin sau khi bỏ qua 8 mẫu cần kiểm tra; chưa chọn = bỏ trong kế hoạch; hiện một skin riêng biệt cho mỗi ped ID. Các bảng đích và cột char vẫn chưa được gán tự động từ tên source cũ.

Vai trò prostitute cho skin collection do người dùng chọn được ghi riêng trong [pool skin vai trò prostitute](prostitute-npc-skin-pool-2026-10-17.md). Nhãn này là ý định dùng về sau, tách khỏi rating, nguồn và ID ped; chưa gán skin vào NPC hoặc cài trong game.

Ba vùng theo yêu cầu: **Vice City → Carcer City → Los Santos**. Carcer City là tên vùng khởi đầu được Changelog.txt:84 nêu; việc ưu tiên vùng đó dựa cả vào mong muốn road trip của bạn. ID trùng giữa các bảng chỉ là một model cần thay một lần.

| Vùng ứng viên | Nhóm dân cư dùng trong bảng chính | ID theo selector | Tổng ứng viên riêng vùng | Slot P1 cho favorite | Danh sách đầy đủ |
| --- | ---: | ---: | ---: | ---: | --- |
| Vice City | 206 | 23 | 225 | 29 | [Vice City](npc-rosters/vice-city.md) |
| Carcer City | 226 | 0 | 226 | 35 | [Carcer City](npc-rosters/carcer-city.md) |
| Los Santos | 167 | 14 | 180 | 21 | [Los Santos](npc-rosters/los-santos.md) |

**Khử trùng:** 403 ID ứng viên và 64 slot P1 trên toàn bộ ba bảng, không cộng số vùng thành số skin. Carcer/LS chia sẻ **164 ID** trong các tập ứng viên; thay model chung có thể phục vụ cả hai vùng, đồng thời ảnh hưởng những vùng khác dùng cùng ID.

## Cách hiểu 'phổ biến' để gán char

P1 dùng độ phủ cấu hình: dân sự thuộc ít nhất 2 trong 5 nhóm Average/Poor/Rich/Business/Clubbers. Nên kiểm tra Average/Poor và các model có nhiều nhóm trước, rồi Business/Rich. Clubbers có điều kiện giờ thiên về tối/đêm trong bảng popcycle. Cột độ phủ 0–5 đếm nhóm khác nhau; dòng SF/VEGAS hay token lặp không làm tăng số nhóm.

**Chưa có tần suất/mật độ model đo trong game hoặc liên kết zone → popcycle type → pedgrp được xác minh.** P1 là danh sách nên thử để dành cho favorite, không phải bảo đảm spawn nhiều nhất. Một model chỉ thuộc 1 nhóm vẫn có thể thường gặp; NPC gang/cảnh sát cũng có thể xuất hiện nhiều khi điều kiện gameplay phù hợp. 910 ID chưa biết usage không được gọi là NPC hiếm.

| Nhóm cấu hình | Type blocks có trọng số >0 | Dòng thời gian >0 / 480 | Dùng để lập kế hoạch |
| --- | ---: | ---: | --- |
| Business | 11 / 20 | 115 | Nhóm rộng; cần xác minh vùng/model runtime |
| Clubbers | 8 / 20 | 65 | Nhóm rộng; cần xác minh vùng/model runtime |
| Casual_Rich | 9 / 20 | 173 | Nhóm rộng; cần xác minh vùng/model runtime |
| Casual_Average | 12 / 20 | 220 | Nhóm rộng; cần xác minh vùng/model runtime |
| Casual_Poor | 11 / 20 | 136 | Nhóm rộng; cần xác minh vùng/model runtime |

Các số trên là cấu hình nhóm theo type/giờ, không phải phần trăm gặp NPC. [Bằng chứng popcycle](evidence/npc-group-opportunity.md).

## Các slot favorite nên xem trước

Đây là ví dụ đầu danh sách, chưa gán nhân vật. Các bảng vùng có đủ 64 slot P1, gồm model nam/nữ và animation gốc để chọn phù hợp.

### Vice City

| ID | Model | Pedtype / animation | Nhóm cấu hình | Độ phủ 5 nhóm | Trạng thái | Char dự kiến |
| ---: | --- | --- | --- | ---: | --- | --- |
| 48033 | `VCS_BMYRI` | CIVMALE / man | Business, Average, Poor, Rich, Clubbers | 5 | Chưa thay | — |
| 48282 | `VC_BMYRI` | CIVMALE / man | Business, Average, Poor, Rich | 4 | Chưa thay | — |
| 48087 | `VCS_HFYBU` | CIVFEMALE / busywoman | Business, Average, Rich, Clubbers | 4 | Chưa thay | — |
| 48103 | `VCS_HMYRI` | CIVMALE / man | Business, Poor, Rich, Clubbers | 4 | Chưa thay | — |
| 48310 | `VC_HFYBU` | CIVFEMALE / busywoman | Business, Average, Rich, Clubbers | 4 | Chưa thay | — |
| 48034 | `VCS_BMYST` | CIVMALE / gang2 | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 48323 | `VC_HMYRI` | CIVMALE / man | Business, Poor, Rich | 3 | Chưa thay | — |
| 48377 | `VC_WFYBU` | CIVFEMALE / busywoman | Business, Average, Rich | 3 | Chưa thay | — |

### Carcer City

| ID | Model | Pedtype / animation | Nhóm cấu hình | Độ phủ 5 nhóm | Trạng thái | Char dự kiến |
| ---: | --- | --- | --- | ---: | --- | --- |
| 22 | `BMYST` | CIVMALE / gang2 | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 56 | `OFYST` | CIVFEMALE / woman | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 58 | `OMOST` | CIVMALE / man | Average, Poor, Clubbers, Husbands | 3 | Chưa thay | — |
| 60 | `OMYST` | CIVMALE / man | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 93 | `WFYST` | CIVFEMALE / sexywoman | Average, Poor, Clubbers, Wives | 3 | Chưa thay | — |
| 101 | `WMYST` | CIVMALE / man | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 142 | `SBMYST` | CIVMALE / man | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 226 | `SOFYST` | CIVFEMALE / woman | Average, Poor, Clubbers | 3 | Chưa thay | — |

### Los Santos

| ID | Model | Pedtype / animation | Nhóm cấu hình | Độ phủ 5 nhóm | Trạng thái | Char dự kiến |
| ---: | --- | --- | --- | ---: | --- | --- |
| 22 | `BMYST` | CIVMALE / gang2 | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 56 | `OFYST` | CIVFEMALE / woman | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 58 | `OMOST` | CIVMALE / man | Average, Poor, Clubbers, Husbands | 3 | Chưa thay | — |
| 60 | `OMYST` | CIVMALE / man | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 93 | `WFYST` | CIVFEMALE / sexywoman | Average, Poor, Clubbers, Wives | 3 | Chưa thay | — |
| 101 | `WMYST` | CIVMALE / man | Average, Poor, Clubbers | 3 | Chưa thay | — |
| 12 | `BFYRI` | CIVFEMALE / sexywoman | Business, Rich, Clubbers, Wives | 3 | Chưa thay | — |
| 20 | `BMYRI` | CIVMALE / man | Business, Rich, Clubbers | 3 | Chưa thay | — |

## Những phần còn lại của toàn bộ catalog

| Quyết định | Số ID | Cách xử lý |
| --- | ---: | --- |
| Ứng viên của ba vùng ưu tiên | 403 | Chọn skin và kiểm chứng theo batch nhỏ |
| Đã có trong các bộ nhóm khác | 325 | Để sau, khi mở rộng tuyến road trip |
| Chưa xác minh cách sử dụng | 910 | Có IDE/asset nhưng không đủ link; kiểm tra script/runtime trước khi gán 'hiếm' |
| Player/protagonist | 39 | Giữ ngoài đợt NPC, bảo toàn phạm vi Aether |
| Special/mission slots | 10 | Giữ ngoài đợt NPC; slot runtime chưa truy script |

[Chỉ mục có đủ 1.687 ID và quyết định từng ID](npc-rosters/all-1687-ids.md). [Master JSON đầy đủ để dùng cho mapping](evidence/npc-replacement-master.json). Các definition theo prefix/section nhưng chưa có population/selector được để riêng cuối từng bảng vùng.

## Bước bạn check skin cũ

1. Xem các slot P1 và chọn danh sách char yêu thích. Chưa cần ghép theo ID cũ của Underground.
2. Với từng skin cũ, bạn đánh dấu tên/ngoại hình muốn dùng; bước kiểm tra tài nguyên tiếp theo sẽ giữ riêng hình ảnh đúng, rig/TXD cơ bản và trọng lượng asset. Lượt này chưa tự kết luận toàn bộ 1.721 cặp skin cũ dùng được.
3. Ghép favorite vào các slot P1 đã xác minh xuất hiện tại tuyến bạn đi; char khác vào nhóm nghề, địa điểm, gang hoặc sự kiện theo ý muốn. Có thể gán cùng một char vào nhiều ID riêng, như bản VC và VCS, nếu muốn gặp xuyên khu; vẫn phải map DFF/TXD riêng và chọn asset nhẹ cho model được dùng nhiều.
4. Giữ voice/AI/population hiện tại khi đổi appearance. Thay theo từng batch có backup; chỉ chỉnh mật độ/spawn khi có yêu cầu riêng.

Các bảng Markdown có cột Char dự kiến; master JSON có review.character_name, is_favorite, legacy_skin_label, skin_review_state và notes để cập nhật ở bước chọn skin. Các lựa chọn này hiện để trống. Builder giữ lại review fields của master JSON nếu dựng lại; chỉnh Markdown riêng không tự đồng bộ vào JSON.

## Trạng thái bộ thử hiện tại

Bạn đã báo cảnh sát LS **280/lapd1** và **285/swat** trigger được và skin hoạt động ổn. Ghi nhận này không được mở rộng thành nghiệm thu đầy đủ mọi animation. **287/army** vẫn là đã cài thử, chưa có kết quả gameplay được báo. Aether tiếp tục giữ cách chọn F2.

Bằng chứng: [ghi nhận runtime của người dùng](evidence/user-runtime-observations.json), [biên bản cài và phục hồi](npc-law-enforcement-installed.md). Lượt lập danh sách này chỉ ghi docs/evidence, không sửa archive, loader, trainer, audio, save hoặc population.

## Nguồn và giới hạn

Catalog IDE/archive trước pilot có 1.687 record, 1.676 cặp basename DFF/TXD khớp. ID 0/null và 10 special slots là 11 trường hợp không có cặp basename đầy đủ. Current peds.ide và 456 dòng group đã được đối chiếu với snapshot. Offset của sáu asset pilot đã đổi: dùng installed manifest thay vì offset cũ khi triển khai tiếp.

pedgrp_vc/cc là liên kết ứng viên từ tên file và member; các dòng SF/VEGAS vẫn còn trong file hậu tố nên không tự suy ra địa bàn. LS view lọc những nhãn đó để dễ xem, giữ toàn bộ file ở phần bổ sung. ModelVariation/variation.dat cung cấp selector riêng; CC chưa có selector trong file hiện tại. Catalog không bao phủ toàn bộ actor tạo bởi script hoặc chỉ dùng trong cutscene.

Chi tiết: [regional crosswalk](evidence/npc-priority-regions.md), [global disposition](evidence/npc-replacement-disposition.md), [group opportunity](evidence/npc-group-opportunity.md). Script dựng lại: evidence/build_npc_replacement_list.py. Không suy ra xác suất từ số lần lặp tên hoặc số file chứa tên.
