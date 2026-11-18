> Quy tắc phân bổ đã được người dùng cập nhật: Thích/Hơi thích dùng ở mọi vùng; Thích lặp nhiều hơn một chút; Bình thường chỉ dùng ở vùng không ưu tiên. Phân bổ và tỉ lệ sẽ xử lý sau. Các phép tính phủ slot trước đó là lịch sử theo giả định cũ, chưa phải kế hoạch phân bổ mới. [Policy hiện tại](evidence/skin-placement-policy.json).

> Cập nhật 15/10/2026: người dùng đã cho phép lặp nguồn để phủ ID, dùng Bình thường trước ở vùng còn lại, rồi Thích → Hơi thích → quay vòng hai mức này. Các số thiếu dưới đây là phép tính lịch sử khi không lặp nguồn. Xem [dự tính cấp theo tier hiện tại](skin-fill-plan-2026-10-15.md).

# Pool skin hiện tại và logic phủ ped ID

Cập nhật 14/10/2026: **mỗi ped ID dùng một skin riêng biệt**. Theo yêu cầu mới, tạm bỏ qua tám skin trước đó có ghi chú cần kiểm tra tài nguyên. File đánh giá gốc, gallery, source và game được giữ nguyên.

## 25 skin Thích phủ được bao nhiêu?

**25 skin Thích chỉ cấp được tối đa 25 ped ID khác nhau.** Không có phép tính nào làm 25 skin phủ hết 403 slot nếu không lặp nguồn giữa các ID. Một ID có thể sinh nhiều NPC instance cùng ngoại hình trong gameplay; đó vẫn là một ID đã được gán skin, không làm tăng số ID được phủ.

Phép tính trước sử dụng tổng ba nhóm được chọn: 25 Thích + 50 Hơi thích + 169 Bình thường = 244 skin. Vì vậy trước khi bỏ tám mẫu cần kiểm tra, 403 slot vẫn thiếu 159; chưa có mapping hoặc cài đặt phủ đủ 403 ID.

403 là tổng ứng viên của ba vùng, gồm dân sự, gang và các vai trò có điều kiện xuất hiện. Trong đó 64 slot P1 là nhóm nên thử trước cho favorite dựa vào độ phủ cấu hình, chưa phải 403 ID đều phổ biến hoặc tần suất spawn đã đo. Skin Thích ưu tiên gán vào các slot thường gặp; Hơi thích/Bình thường dành cho lựa chọn ưu tiên thấp hơn khi usage đã xác minh.

## Pool sau khi bỏ qua mẫu cần kiểm tra

| Mức | Dòng người dùng đã chọn | Tạm bỏ qua tài nguyên | Skin còn trong pool |
| --- | ---: | ---: | ---: |
| Thích | 25 | 0 | 25 |
| Hơi thích | 50 | 6 | 44 |
| Bình thường | 169 | 2 | 167 |

**Pool hiện tại: 236 skin khác nhau**. Bỏ khỏi kế hoạch 1,485 dòng: 16 Không muốn sử dụng + 1.461 chưa chọn + 8 mẫu tài nguyên được bỏ qua theo yêu cầu mới. Bỏ là trạng thái kế hoạch, không xóa file hoặc sửa rating.

| Phạm vi | Slot mục tiêu | Pool có thể cấp tối đa | Còn thiếu skin riêng biệt |
| --- | ---: | ---: | ---: |
| Ba vùng ưu tiên | 403 | 236 | **167** |
| NPC theo role trong IDE | 1,638 | 236 | **1,402** |
| Mọi actor cố định, thêm 38 model PLAYER1/2 | 1,676 | 236 | **1,440** |

Ba pilot 280/285/287 khớp ba skin Thích trong pool và đã được tính trong 236. Hiện còn **233 skin chưa gán**. Với 403 slot, còn 400 slot chưa phủ: 400 − 233 = **167**. Nguồn trong pool mới là nguồn ứng viên; chưa có mapping cho các skin còn lại và chưa nghiệm thu animation trong game.

25 Thích gồm ba pilot đã dùng ở cảnh sát/SWAT/army. Nếu giữ ba vị trí hiện tại thì còn 22 Thích cho 64 slot P1, thiếu 42 nếu yêu cầu mọi P1 chỉ dùng Thích. Nếu chuyển cả ba sang P1 thì có thể cấp 25 và thiếu 39. Chưa chốt chuyển char hoặc bắt buộc mọi P1 dùng Thích.

Phạm vi NPC 1.638 gồm 1.105 dân thường, 324 gang, 136 cảnh sát/quân đội/cứu hộ, 31 criminal và 42 prostitute. Phạm vi 1.676 thêm 38 model có pedtype PLAYER1/2; chưa xác nhận chúng đang là nhân vật người chơi. ID 0, special01–10 và Aether nằm ngoài các mẫu số NPC tĩnh. 434 cặp component ngoài ModelName IDE chưa có binding/usage đầy đủ nên không cộng vào đây. Không cộng các phạm vi với nhau.

## Tám mẫu tạm bỏ qua

Đây là các trường hợp đã gắn cờ cần kiểm tra tài nguyên; thiếu normals có thể là shading có chủ đích. Theo yêu cầu hiện tại, chúng bị loại khỏi pool để khỏi mất thời gian kiểm tra, không kết luận toàn bộ đều hỏng.

| Index gallery | Tên cũ / workbook | Model nguồn | Mức đánh giá gốc | Ghi chú |
| ---: | --- | --- | --- | --- |
| 430 | Ren_chon.dff | `DNMYLC.dff` | Hơi thích | Một phần geometry thiếu normals |
| 1109 | skin (14).dff | `SOMYST.dff` | Hơi thích | TXD chưa parse được trong census cũ |
| 1334 | skintrash2 (104).dff | `VC_HMOTR.dff` | Hơi thích | Một phần geometry thiếu normals |
| 1521 | skin (217).dff | `VCS_GANG7B.dff` | Bình thường | Một phần geometry thiếu normals |
| 1655 | skin (58).dff | `VWFYWAI.dff` | Hơi thích | Một phần geometry thiếu normals |
| 1675 | skin (95).dff | `WFYLG.dff` | Bình thường | Một phần geometry thiếu normals |
| 1700 | skin (61).dff | `WMYCLOT.dff` | Hơi thích | Một phần geometry thiếu normals |
| 1702 | Yoshino.dff | `WMYCONB.dff` | Hơi thích | Một phần geometry thiếu normals |

## Các quy tắc nguồn được giữ

Gallery có 1.721 dòng nhưng chỉ **725 cặp DFF/TXD khác byte**. Các bản chưa chọn vẫn nằm ngoài pool. Trần số lượng toàn nguồn cũ cũng thấp hơn 1.638 slot nếu không lặp; không tự đưa model chưa chọn trở lại kế hoạch.

Tên model trong gallery/workbook là basename nguồn cũ, không phải Eagle ID đã được gán char. Hai file cùng char nhưng khác byte có thể là variant khác; khác byte chưa bảo đảm khác nhân vật/ngoại hình rõ rệt.

Cặp được chọn ở dòng 1347 `VC_KENTPAUL` (Bình thường) có bản trùng dòng 937 `MW_WFOYA` bị đánh dấu Không muốn sử dụng. Giữ đúng nguồn đã chọn ở dòng 1347; dòng 937 vẫn bỏ và không tính thêm vào pool. Chưa coi mâu thuẫn rating của bản trùng là lỗi tài nguyên.

Tổng source file pool hiện tại: **432.75 MiB**; đây không phải tổng VRAM hoặc kích thước IMG sau cài.

## Danh sách và bằng chứng

- [Danh sách 236 skin giữ](skin-pool-keep-list.md).
- [Danh sách 1,485 dòng bỏ](skin-pool-drop-list.md).
- [Pool JSON và rating gốc theo dòng](evidence/skin-selected-pool.json).
- [Chính sách bỏ qua tài nguyên](evidence/skin-pool-exclusions.json).
- [Coverage JSON](evidence/skin-pool-coverage.json).
- [Bản chụp đánh giá đã nhập](evidence/skin-ratings-20261014-00af1091ca72.json).
- [Roster Eagle hiện tại](eagle-current-ped-resources.md).

Làm lại theo thứ tự: `evidence/build_selected_skin_pool.py`, `evidence/build_skin_pool_coverage.py`, `evidence/refresh_skin_pool_reports.py`. Bản đánh giá raw không bị sửa bởi policy.
