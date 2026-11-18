# Chọn skin NPC theo dung lượng và độ nặng — Project Eagle

Ngày khảo sát: **14/10/2026**. Chỉ đọc asset, archive, cấu hình và phần cứng; không cài thêm hoặc sửa game. Dữ liệu phục vụ bước review skin cho [403 ID ứng viên / 64 slot P1](npc-replacement-list.md), chưa gán char vào slot.

**Phạm vi:** 1.721 cặp và shortlist 125 bên dưới là **nguồn skin Underground cũ**; phần Eagle trong báo cáo này chỉ là baseline 403 model. Đợt quét đầy đủ bản Eagle hiện tại được ghi riêng tại [tài nguyên skin Eagle hiện tại](eagle-current-skins.md), gồm 1.676 cặp actor cố định và toàn bộ 2.110 cặp COMPONENTPEDS.

## Đề xuất cho cách chơi của bạn

**Dành bản skin có mesh nhẹ cho char yêu thích xuất hiện thường xuyên ở Vice City, Carcer City và Los Santos.** Với nhân vật chính Aether, chấp nhận nhiều chi tiết hơn vì thường chỉ có một instance. Với skin nặng của NPC, thử ở một số slot và đo cảnh đông người trước khi nhân rộng.

Không cần hy sinh char yêu thích: nên chọn **phiên bản nhẹ của cùng char** trước. Nếu chỉ có bản nặng, tối ưu texture và mesh riêng, hoặc dành cho vai trò xuất hiện hạn chế đã được xác minh. Slot P1 hiện được chọn theo độ phủ nhóm cấu hình, chưa phải tần suất đo trong game; 910 ID chưa rõ usage không được xem là NPC hiếm.

Đề xuất sàng lọc ban đầu dưới đây là quy tắc biên tập để chọn thứ tự thử, **không phải giới hạn Eagle hoặc bảo đảm FPS**:

| Mục đích | Mesh nên ưu tiên | Texture nên ưu tiên | Dung lượng cặp dùng để sàng lọc |
| --- | --- | --- | --- |
| NPC nhiều instance / char yêu thích phổ biến | Khoảng 1.000–5.000 tam giác; xem thêm vertex, material và rig | Tổng mip khoảng ≤1 MiB; atlas 512 hoặc 1024 khi cần; format nén phù hợp alpha | Ưu tiên ≤1 MiB, linh hoạt đến 2 MiB nếu mesh/texture tốt |
| NPC dùng có chọn lọc | 5.000–12.000 tam giác, hoặc nhiều vertex/material dù ít tam giác | Khoảng 1–4 MiB tổng mip: so với mức chi tiết thật sự nhìn thấy | 1–4 MiB là điểm cần kiểm tra, không tự động loại |
| Skin cần cân nhắc / tối ưu | >12.000–20.000 tam giác; >20.000 nên tránh nhân rộng trước khi đo | >4 MiB mip, nhiều texture lớn hoặc alpha/material phức tạp | >4–8 MiB cần tìm nguyên nhân; >8 MiB nên tìm bản nhẹ hơn |

Hai trục phải đọc riêng: skin 2 MiB vẫn có thể có 20.000 tam giác; skin 8 MiB có thể chủ yếu do texture chưa nén. Số material slot chỉ là chỉ báo cấu trúc, không phải số draw call đo được. Nhiều slot cùng dùng một texture cũng không biến thành một draw call theo mặc định.

## Khảo sát toàn bộ nguồn cũ

Đã quét **1.721 cặp DFF/TXD** trong năm IMG của bộ Underground cũ; nguồn này dùng để tra cứu skin, không phải 1.721 skin đã cài vào Eagle. IMG directory hiện tại khớp audit tên/sector; dung lượng file gốc lấy từ metadata RAR. Đã đọc geometry và native texture headers từng member, không dựng hình hoặc test animation hàng loạt.

| Chỉ số | Bộ skin nguồn cũ | 403 model gốc Eagle trước cài thử |
| --- | ---: | ---: |
| DFF geometry đọc được | 1.719 / 1.721 | 403 / 403 |
| TXD đọc được | 1.715 / 1.721 | 403 / 403 |
| Trung vị tam giác/model | 19.847 | 1.024 |
| P90 tam giác/model | 52.108 | 1.270 |
| Tam giác lớn nhất/model | 103.862 | 1.996 |
| Trung vị vertex/model | 15.066 | 1.017 |
| Trung vị texture mip payload/model | 1,50 MiB | 0,063 MiB |

Trung vị tam giác nguồn cũ khoảng **19,4 lần** baseline Eagle; đây là so sánh các phân bố khác nhau, không phải dự đoán FPS giảm 19,4 lần. Chất lượng hình ảnh cũng chưa được chấm: chi tiết thêm có thể hữu ích khi nhìn gần, nhưng không đảm bảo nhìn đẹp hơn từ khoảng cách đi đường.

Tổng file gốc của 1.721 cặp là **7,25 GiB**; trung vị cặp **2,90 MiB**, P90 **10,11 MiB**, lớn nhất **26,58 MiB**. TXD chiếm **68,6%** số byte, DFF chiếm 31,4%. RAR nén nhỏ hơn không có nghĩa asset mà game nạp cũng nhỏ tương ứng.

| Khoảng | Số cặp theo tổng DFF+TXD | Khoảng tam giác | Số DFF |
| --- | ---: | --- | ---: |
| ≤0,5 MiB | 111 | ≤5.000 | 160 |
| 0,5–1 MiB | 104 | >5.000–12.000 | 323 |
| 1–2 MiB | 298 | >12.000–20.000 | 392 |
| 2–4 MiB | 591 | >20.000 | 844 |
| 4–8 MiB | 313 | Không đọc được | 2 |
| >8 MiB | 304 | — | — |

Các cột dung lượng và tam giác là **hai phân bố độc lập**, không phải cùng các skin theo từng hàng. Có **125 mẫu** đáp ứng đồng thời bộ lọc ≤5.000 tam giác, ≤6.000 vertex, ≤1 MiB texture mip, ≤2 MiB tổng cặp và có skin extension: [danh sách nên review trước](skin-review-shortlist.md). Chưa coi các mẫu đó là đẹp, hợp rig hoặc đã được duyệt.

Texture của nguồn cũ chủ yếu đã nén: 6.457 DXT1, 1.056 DXT3, 839 DXT5, 1.100 uncompressed 32-bit và 3 format chưa rõ trong 9.455 texture entries. Vì vậy **không thể chỉ nén TXD là giải quyết hết độ nặng**; nhiều mesh vẫn cần giảm polygon/vertex. Bộ quét đã đối chiếu 11 mẫu với audit sâu trước đó: tam giác, kích thước texture và byte mip đều khớp.

8 member chưa đọc an toàn được: `LC_CAS_WOM.dff`, `ulpdh1.dff`, `BMOSEC.txd`, `UL_WMYCV.txd`, `MH2_WATCHDOGS1.txd`, `SOMYST.txd`, `MW_SOMYRG.txd`, `VC_HMYST.txd`. Chúng giữ trạng thái unknown, không được tính là nhẹ. Có skin extension hoặc 32 bone header chưa chứng minh hierarchy/weights đúng; thiếu normals cũng cần kiểm tra shading dự định.

## Các mẫu cụ thể đã khảo sát sâu

Nhãn NPC dưới đây lấy từ mapping workbook lịch sử, chưa xác nhận danh tính qua ảnh của mọi mẫu. Aether lấy từ gói đã audit. MiB = 1.048.576 byte; “texture mip” là dữ liệu ảnh lưu trong TXD, không phải VRAM runtime đo được.

| Mẫu | DFF+TXD MiB | Tam giác | Vertex | Texture mip MiB | Texture | Material slots | Trạng thái sử dụng |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| ReiAyanami2 | 0,130 | 1.601 | 1.553 | 0,016 | 2 | 2 | Đã thay LS police; người dùng báo hoạt động ổn |
| hanekawa | 0,356 | 3.622 | 3.113 | 0,125 | 1 | 4 | Đã thay SWAT; người dùng báo hoạt động ổn |
| senjo | 0,360 | 3.696 | 3.154 | 0,125 | 1 | 9 | Đã thay army; chưa có báo cáo thử trong game |
| shinobu | 0,354 | 3.740 | 2.904 | 0,125 | 1 | 3 | Nguồn nhẹ đáng review; chưa cài Eagle |
| Alita | 0,644 | 6.659 | 5.241 | 0,250 | 2 | 1 | File nhỏ nhưng mesh cao hơn nhóm ≤5k; chưa cài |
| REM | 1,366 | 11.836 | 7.731 | 0,750 | 2 | 2 | Mesh cần cân nhắc khi nhân nhiều NPC; chưa cài |
| Ganyu | 2,093 | 21.244 | 18.067 | 0,750 | 3 | 7 | Texture vừa phải nhưng mesh nặng; chưa cài |
| ZeroTwo | 2,762 | 16.867 | 11.859 | 1,842 | 7 | 28 | Audit cũ có parent mapping khác baseline; cần kiểm tra rig, chưa cài |
| Aether shadeless đang dùng | 2,281 | 17.706 | 15.487 | 1,250 | 4 | 18 | F2 đã được người dùng thử; nhân vật chính |
| Aether standard | 5,958 | 17.706 | 15.487 | 4,750 | 4 | 18 | Variant so sánh; không phải cặp đang cài |

**Aether là ví dụ vì sao phải tách mesh/texture.** Bản đang dùng giảm tổng file khoảng 61,7% và payload texture khoảng 73,7% so với standard, nhưng **tam giác và vertex không giảm**. Body 1024² của standard lưu 32-bit, 4 MiB; bản hiện tại lưu DXT1, 0,5 MiB. Hai variant còn khác shading/normals, nên không xem đây là phép benchmark chỉ thay compression hay bảo đảm hình ảnh giống hệt.

30 instance senjo tương ứng 110.880 tam giác model; 30 instance Ganyu tương ứng 637.320 tam giác, khoảng 5,75 lần. Đây là phép nhân lượng geometry tĩnh, chưa tính LOD, visibility, nhiều pass/alpha hoặc pipeline skinning; không đổi trực tiếp thành FPS.

## Tính ngân sách cho roster

Tách ba con số: **slot đã thay trên đĩa**, **model/TXD riêng đang được giữ trong bộ nhớ**, và **NPC instance đang xử lý/vẽ**. Nhiều NPC cùng ID có thể dùng chung asset; công việc animation/vẽ vẫn tăng theo instance. Hai ID khác nhau cùng char không mặc định được engine gộp tài nguyên.

| Kịch bản giả định cho danh sách | Tổng dung lượng cặp |
| --- | ---: |
| 403 slot × 0,5 MiB | 201,5 MiB |
| 403 slot × 2 MiB | 806 MiB |
| 403 slot × 4 MiB | 1.612 MiB |
| 64 slot favorite × 4 MiB + 339 slot × 0,5 MiB | 425,5 MiB |

Kịch bản phối hợp giảm tổng file khoảng 73,6% so với mọi slot 4 MiB. Tuy nhiên nếu 64 slot favorite có mesh nặng và cùng thường xuất hiện, chúng vẫn có thể chiếm phần lớn công việc vẽ. “Favorite” nên ưu tiên phiên bản tối ưu, không tự động dành bản nặng nhất.

Các số này là tổng **cặp nguồn dự kiến**, không phải toàn bộ IMG sau cài, không phải mọi skin đều đồng thời nạp và không phải mapping char đã chốt. Cách cài pilot append payload còn giữ dữ liệu cũ trong archive; archive/backup tăng dung lượng khác với tổng cặp, cần tính theo phương thức cài thật. 403 candidate slots hiện dùng khoảng 62,37 MiB sector allocation ở Eagle (gồm ba pilot); đối chiếu geometry gốc dùng backup trước pilot để tránh trộn trạng thái.

Ví dụ texture 1024² một mức mip: DXT1 khoảng 0,5 MiB, DXT5 khoảng 1 MiB, RGBA32 khoảng 4 MiB. Hạ chiều rộng và chiều cao cùng một nửa làm pixel count còn một phần tư. Mip đầy đủ thêm khoảng một phần ba cho texture vuông lớn, nhưng phục vụ hiển thị xa; không mặc định bỏ mip để tiết kiệm. Căn cứ compression 4×4 từ [Microsoft Direct3D 9](https://learn.microsoft.com/en-us/windows/win32/direct3d9/compressed-texture-formats); kích thước mip là phép tính từ từng mức. DXT1 chỉ có alpha giới hạn; chọn format theo hình ảnh/alpha, kiểm tra mặt/tóc/viền sau khi chuyển.

TXD byte, compressed mip payload và hypothetical RGBA32 tương đương là ba đại lượng khác nhau. D3D9 managed resources có thể có bản system/video memory, nhưng chưa xác minh pool Eagle dùng; **không nhân đôi mọi TXD hoặc coi mip payload là toàn bộ VRAM**. [Microsoft: Managing Resources](https://learn.microsoft.com/en-us/windows/win32/direct3d9/managing-resources).

## Giới hạn của máy và cách nghiệm thu

Máy được đọc tại thời điểm khảo sát: Ryzen 7 4800H, khoảng 15,37 GiB RAM visible, GTX 1650 **4.096 MiB VRAM** theo nvidia-smi; cũng có GPU AMD tích hợp. Chưa xác nhận GPU Eagle thực tế dùng hay bộ nhớ còn trống lúc chơi. `gta_sa.exe` là PE32 x86, cờ Large Address Aware bật. Trên Windows x64, LAA cho 4 GiB **không gian địa chỉ ảo của process**, phải dùng chung cho game/map/xe/script/buffer/skin; không phải 4 GiB dành riêng cho NPC. [Microsoft: WOW64 memory](https://learn.microsoft.com/en-us/windows/win32/winprog64/performance-and-memory-consumption).

PECore cấu hình cap 80 FPS và các giá trị ped density/population 1,5; chưa đo hiệu quả các multiplier, không nhân thành 2,25×. `stream.ini` có `memory 13500`, nhưng đơn vị và override hữu hiệu chưa xác minh; không dùng nó làm ngân sách MB hoặc tăng cấu hình ở bước này.

Bước review tiếp theo nên ghi: char mong muốn, hình ảnh chấp nhận, basename nguồn, DFF/TXD byte, tam giác/vertex/material, texture format/size/mip, rig/texture warnings và slot Eagle dự kiến. Chọn 5–10 char P1, ưu tiên version mesh nhẹ, rồi thử cùng đường chạy/camera/thời điểm tại vùng ưu tiên. So cảnh trước/sau theo frametime/FPS, working set, VRAM, khựng khi road trip và lỗi rig/texture; lưu resolution/settings và chú ý cap FPS. Việc LS police/SWAT hiện hoạt động ổn chưa chứng minh bộ skin lớn hơn có cùng hiệu năng.

## Dữ liệu và khả năng làm lại

- [Số liệu ghép của đủ 1.721 skin và 13 mẫu sâu](evidence/skin-budget-analysis.json), [script ghép và tạo shortlist](evidence/build_skin_budget_analysis.py).
- [125 mẫu ít tài nguyên nên kiểm tra trước](skin-review-shortlist.md).
- [Census dung lượng](evidence/skin-size-census.md), [JSON đầy đủ](evidence/skin-size-census.json), [script](evidence/build_skin_size_census.py).
- [Census geometry/texture](evidence/skin-resource-census.md), [JSON đầy đủ](evidence/skin-resource-census.json), parser `staging/project-eagle/skin-budget/inspect_resource_census.py`.
- [Phần cứng, PE header và cấu hình runtime](evidence/skin-runtime-budget-context.md), [JSON bằng chứng](evidence/skin-runtime-budget-context.json).
- [Audit sâu 11 NPC](evidence/npc-reuse-audit.json), `staging/project-eagle/aether/asset-audit.json`, [người dùng báo thử police/SWAT](evidence/user-runtime-observations.json).

Không chỉnh sửa candidate list, review fields, archive, loader, population hoặc lựa chọn nhân vật trong đợt phân tích này.

Kiểm tra cuối: các tổng 1.721/403/64 và shortlist 125 khớp JSON; 16 liên kết dữ liệu cục bộ trong báo cáo/shortlist tồn tại. Bộ so sánh tương tác đã được kiểm tra phép tính, đổi mẫu/số lượng, lưu/khôi phục lựa chọn và layout 736/320 px, không có lỗi JavaScript. SHA256 hiện tại của `COMPONENTPEDS.img` và cặp Aether khớp trạng thái đã cài trước đợt khảo sát; không chạy benchmark game. Chi tiết QA giao diện nằm trong `staging/project-eagle/skin-budget/visual-verification.json`.
