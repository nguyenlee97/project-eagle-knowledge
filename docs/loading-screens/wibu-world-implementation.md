# Wibu World / Project Wibu — bản đã cài

Ngày 14/10/2026, bản đầy đủ đã được cài vào `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`. Người dùng đã duyệt pilot anime 2D và yêu cầu áp dụng cho cả bộ; người dùng đã tự test và xác nhận “oke nó work tốt rồi”.

## Kết quả

- 14 poster mới, 9 khung đôi và 5 khung đơn, bao phủ đủ 23 nhân vật nữ trong [mapping](wibu-world-screen-map.json).
- Anime 2D với lineart và cel shadow phẳng; outfit đô thị giữ nhận diện nhân vật; bố cục GTA. Chữ Grand Theft Auto Wibu World trắng/đen, lettering gợi Genshin.
- Title và PNG khởi động Project Wibu dùng silhouette Hu Tao trắng/đen. Caption đổi thành `Project Wibu is loading`.
- [Gallery đầy đủ: 14 poster, title và startup splash](../../../staging/project-eagle/loading-screens/implementation/qa/LOADSCS-wibu-world/gallery.html), [contact sheet](../../../staging/project-eagle/loading-screens/implementation/qa/LOADSCS-wibu-world/LOADSCS-wibu-world-decoded-contact-sheet.jpg), [title decode](../../../staging/project-eagle/loading-screens/implementation/qa/LOADSCS-wibu-world/title_pc_US-roundtrip.png).

## File thực tế

| Thành phần | Đường cài / bản phục hồi |
| --- | --- |
| TXD đầy đủ | `modloader\WibuWorldLoading\txd\loadscs.txd` |
| Core chứa startup PNG/caption | `PECore.asi` |
| Core gốc | `staging\project-eagle\loading-screens\implementation\pecore\backup\PECore-source.asi` |
| TXD gốc để đối chiếu | `staging\project-eagle\loading-screens\implementation\backup\LOADSCS.original.txd` |
| Biên bản cài | [install-state.json](../../../staging/project-eagle/loading-screens/implementation/install-state.json), [install-history.jsonl](../../../staging/project-eagle/loading-screens/implementation/install-history.jsonl) |

SHA-256 TXD cuối: `7A3E0899F94908EF89596B4939A59BA3C082193BBCED44CC5FB4F2CAAC96E80D`.
SHA-256 PECore đã cài: `4C3B891061D773B095C52B4CD87A1C1FC1A5FBFD40533AF707046D929B861560`.

Pilot và bản đầy đủ dùng cùng một folder WibuWorldLoading; bản đầy đủ đã thay pilot. Không có hai overlay cạnh tranh. TXD nền `models\txd\LOADSCS.txd` giữ nguyên hash gốc. Loader config, PECore.ini và hai executable giữ nguyên hash qua kiểm tra trước/sau. Phạm vi cài chỉ gồm overlay TXD và PECore PNG/caption; không sửa gameplay skin, NPC, radio, trainer, save hoặc Underground.

## Kiểm tra đã hoàn thành

[QA TXD đầy đủ](../../../staging/project-eagle/loading-screens/implementation/qa/LOADSCS-wibu-world/LOADSCS-wibu-world-qa.json) và [verification độc lập](../../../staging/project-eagle/loading-screens/implementation/qa/LOADSCS-wibu-world/LOADSCS-wibu-world-verification.json) xác nhận:
- Dictionary vẫn có 17 texture; thay 14 poster và title, giữ nguyên byte hai vendor texture và trailer.
- Giữ codec, kích thước native và một mip. LOADSC6 vẫn X8R8G8B8 và decode RGB khớp tuyệt đối; các poster khác và title dùng DXT1.
- Dải legal/credit title từ hàng 1456 giữ nguyên các block DXT1 gốc.
- Export không crop; nguồn sinh ảnh được giữ nguyên và resample tới kích thước native. Aspect delta lớn nhất 0,142%; PSNR DXT1 32,683–43,749 dB.
- Root đã xem từng artwork được sinh và contact sheet decode cuối, kiểm spelling và coverage.

[QA live install](../../../staging/project-eagle/loading-screens/implementation/qa/live-install-validation.json) xác nhận hash của file đã cài khớp staged candidate và protected files giữ nguyên. PECore resource 10/200/1033 decode đúng PNG 640×640 RGBA; 12 resource khác, code .text, imports/exports/entry point giữ nguyên; .rdata chỉ đổi caption đã xác định.

## Trạng thái thử trong game

Đã có một lần mở thử bản pilot trước khi người dùng yêu cầu tự test. Log ghi PECore splash Starting/Done; ModLoader phát hiện và cài file `wibuworldloading\txd\loadscs.txd` qua handler `gta3.std.fx` thực tế. Tài liệu std.sprites là cơ sở chọn layout thư mục; không đồng nhất handler được log với plugin đó.

Computer Use đọc được hộp Device Selection; chưa có capture xác nhận poster, title, alpha, crop/fade hoặc loading bar. Lần thử đã dừng, game không chạy tại thời điểm cài bản đầy đủ. Hai log pilot được lưu trong `implementation/qa/runtime-attempt/`. **Sau đó người dùng tự mở game và xác nhận ngày 14/10/2026: “oke nó work tốt rồi”. Task 3 đã hoàn tất trong phạm vi artwork/branding.** [Xác nhận runtime từ người dùng](../../../staging/project-eagle/loading-screens/implementation/qa/user-runtime-confirmation.json) ghi riêng nguồn bằng chứng này; không coi đó là phép đo performance hay capture kiểm từng poster của agent.

Một lần loading cơ sở chọn sáu poster ngẫu nhiên trong 14; có đủ nhân vật trong cả bộ, không đảm bảo thấy cả 23 trong một lần mở.

## Phục hồi

Đóng game, rồi chạy từ PowerShell:

```powershell
& 'C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\loading-screens\implementation\scripts\rollback_wibu.ps1'
```

Script kiểm hash và từ chối ghi đè nếu core hoặc overlay đã được thay bởi việc khác. Nó khôi phục PECore gốc, xóa đúng file overlay đã ghi nhận và chỉ xóa folder riêng khi rỗng; không recursive-delete. Base TXD giữ nguyên từ đầu.

## Artwork và prompt có thể sửa tiếp

Ảnh được tạo bằng **ImageGen built-in**. [Bộ prompt đã dùng](../../../staging/project-eagle/loading-screens/implementation/prompts/README.md) có link đến từng prompt. [Generation provenance](../../../staging/project-eagle/loading-screens/implementation/generation-provenance.json) lưu nguồn sinh của 14 poster. [Live QA manifest](../../../staging/project-eagle/loading-screens/implementation/qa/live-install-validation.json) lưu đường master, prompt riêng từng ảnh, hash và export. Master nằm trong `implementation/art-source/`; export native trong `implementation/final/`.

Các bản logo vàng và pilot 2.5D bị từ chối vẫn được giữ làm lịch sử, không nằm trong bản đã cài. Nguồn portrait official đã được đối chiếu; metadata Vesna được sửa theo trang nhân vật char=14, Shenhe đã được sửa trước khi tạo ảnh, và Lumine dùng nữ Traveler trong ảnh official có cả Aether.

