# Dữ liệu có thể cất sang D — 22/10/2026

Khảo sát chỉ đọc trong lúc viewer đang build IMG trên D. Không di chuyển/xóa file, không thay mapping hoặc game. C còn khoảng 11,83 GiB tại lúc đo; D khoảng 1.091 GiB. Số đo bên dưới là GiB (1.073.741.824 byte).

## Đề xuất ưu tiên

| Thư mục trên C | Dung lượng logic | Đề xuất |
|---|---:|---|
| `tools/eagle-radio-studio/data/backups` | 11,02 GiB | Ưu tiên cất sang D: snapshot radio ngày 14–16/10, không phải tài nguyên skin/build. Giữ đủ manifest và file để phục hồi. |
| `tools/eagle-radio-studio/data/cache` | 3,37 GiB | Có thể chuyển nguyên thư mục sang D và giữ junction ở đường dẫn cũ, khi Radio Studio không đang compile/apply. Cache gồm tracks 1,58 và stations 1,78 GiB; project/build_state đang tham chiếu đường dẫn station cache, nên không xóa hoặc di chuyển trần. |
| `staging/project-eagle/skin-gallery-2026-10-14/source/gtaug` | 7,25 GiB | Đợi test skin/IMG theo yêu cầu. Là nguồn gallery cũ; catalog viewer hiện đọc raw ở kho cá thể, nhưng còn dùng cho truy vết/phục hồi. |
| `ProjectEagleModPack` | 10,29 GiB | Chưa xác nhận không dùng. Giữ để đối chiếu khi merge các thay đổi game; không đưa vào số dung lượng có thể giải phóng ngay. |

Hai mục radio đầu có tổng khoảng 14,39 GiB. Ưu tiên chỉ chuyển backup radio trước cũng giải phóng khoảng 11 GiB mà không cần chờ xử lý skin hoặc merge game. Đích gợi ý: `D:/GTA Archive/Eagle Radio Studio/{backups,cache}`. Junction giữ nguyên đường dẫn C cho công cụ phục hồi và các đường dẫn cache đang lưu.

Quy trình cho lượt di chuyển được yêu cầu sau: dừng riêng tác vụ radio liên quan, sao chép sang thư mục đích riêng, đối chiếu số lượng/kích thước/SHA-256, chỉ sau khi đạt mới bỏ nguồn C và tạo junction, kiểm tra đọc/list backup/cache qua đường dẫn cũ. Không áp dụng quy trình này vào skin, game hay IMG đang build trong lượt khảo sát này.

## Giữ nguyên lúc này

- Hai game: `Project Eagle/gta sa gameplay-lab` 12,98 GiB và `Project Eagle/gta sa clean/gta sa clean` 11,95 GiB. Radio Studio đang chọn gameplay-lab, viewer/build skin đang chọn clean. Không loại bản nào trước khi merge.
- `Skin Library`, `Downloads/fix` (0,839 GiB), các staging tối ưu gần đây: đợi kiểm thử IMG/game. Mọi đường dẫn DFF/TXD hoạt động của catalog viewer đều nằm trong `numbered-skins/raw`; NPC preview nằm trong `numbered-skins/npc-assets`.
- `numbered-skins/deployment/baseline`: bản phục hồi hiện hành, cần giữ.
- `[SA-MP.VN] GTA Online` 7,05 GiB: game cũ; chưa được giao thay đổi hoặc loại bỏ.
- Các project và nhạc riêng trong Downloads: chưa có bằng chứng không còn dùng.

## Cách đọc số dung lượng

Workspace GTA có 43.236 file thường, tổng theo đường dẫn 109,316 GiB; tính mỗi NTFS file ID một lần còn 88,083 GiB. Khoảng 21,232 GiB chênh lệch chủ yếu là hardlink của skin, không phải bấy nhiêu byte có thể thu hồi bằng việc xóa một đường dẫn. Đây chưa phải phép đo cluster được cấp phát.

Top-level theo đường dẫn: Skin Library 42,41 GiB; Project Eagle 25,05; tools 14,45; ProjectEagleModPack 10,29; staging 9,48; GTA Online 7,05; backups 0,44; docs 0,14. Không cộng thêm junction `staging/project-eagle/skin-downloads-2026-10-15` vì trỏ về kho skin. Downloads quét riêng 17,117 GiB; không cộng nó vào tổng C một cách máy móc vì có đường dẫn nối và phạm vi project khác.

Builder đang tạo IMG trên D, nhưng Apply vẫn chuẩn bị file cạnh archive game trên C. Mã `deploy_skins.py` yêu cầu chỗ trống C ít nhất bằng kích thước candidate cộng 1 GiB dự phòng; với candidate dự kiến khoảng 11,7 GiB, C 11,83 GiB hiện tại sẽ thiếu. Chuyển backup radio là đủ tạo khoảng trống cho bước này. Chưa xác nhận build hoàn tất hay thử game trong báo cáo dung lượng.
