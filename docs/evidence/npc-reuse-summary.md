# Khảo sát tái sử dụng NPC từ bộ skin Underground

Ngày khảo sát: 13/10/2026. Đây là phép đo tĩnh, chỉ đọc nguồn Underground và bộ Eagle. Bốn cặp DFF/TXD ban đầu và bảy cặp shortlist được trích riêng từ `C:\Users\LENOVO\Desktop\GTA\[SA-MP.VN] GTA Online\gtaug.rar` vào `staging\project-eagle\npc-reuse-survey`; không archive nào trong game bị thay đổi và không mở game.

Tên Alita, REM, Ganyu và ZeroTwo lấy từ các dòng đổi tên lịch sử trong `docs\evidence\source-skin.xlsx`, Sheet2. Workbook ghi tên nguồn và tên đích nhưng không ghi URL nguồn ở các dòng này. Vì vậy tên là bằng chứng lịch sử về mapping, không phải xác nhận bằng mắt rằng DFF hiện tại biểu diễn đúng nhân vật đó. Các target dưới đây chỉ là target Underground trong mapping cũ; không phải đề xuất ID sẽ dùng ở Eagle.

| Tên lịch sử trong workbook | Basename Underground | ID ped Underground trong audit | DFF + TXD | Vertices / triangles | Texture dictionary |
|---|---|---:|---:|---:|---|
| Alita | MACCER | không có dòng peds.ide trực tiếp | 674,810 B | 5,241 / 6,659 | 2 texture 512×512, tổng file TXD 262,440 B |
| REM | VMAFF1 | 124 | 1,432,227 B | 7,731 / 11,836 | body 1024×1024 và lace 1024×512, TXD 786,728 B |
| Ganyu | WMOPREA | 68 | 2,194,199 B | 18,067 / 21,244 | body 1024×1024, face/hair 512×512, TXD 786,856 B |
| ZeroTwo | WMYPIZZ | 155 | 2,896,257 B | 11,859 / 16,867 | 7 texture, TXD 1,932,312 B |

Để so sánh nhẹ, Aether trong staging có 15,487 vertices / 17,706 triangles: cặp standard DFF+TXD là 6,247,242 B; cặp shadeless là 2,391,382 B. Alita và REM nhỏ hơn về mesh và tổng bytes; Ganyu vượt mẫu mesh này; ZeroTwo thấp hơn một chút về số hình học nhưng có TXD lớn nhất trong bốn ứng viên. Đây chỉ là so sánh dung lượng và hình học đã giải mã, không dự đoán FPS.

## Shortlist tài nguyên nhẹ cho NPC

Đã thêm bảy mapping anime/game lịch sử để tìm tài nguyên nhẹ hơn. Tên nguồn trong workbook không kèm URL; do đó đây là nhãn lịch sử, chưa xác nhận nhân vật bằng hình ảnh. Dung lượng bên dưới là số byte của cặp DFF/TXD trích ra; cột allocation là tổng slot IMG, đã tính sector padding 2,048 byte.

| Tên nguồn lịch sử | Target cũ / ped ID Underground | Pair raw / IMG allocation | Vertices / triangles | Kiểm tra tĩnh |
|---|---|---:|---:|---|
| `ReiAyanami2.dff` | DNB3 / 123 | 136,298 / 139,264 B | 1,553 / 1,601 | Không lỗi weight, thiếu texture, trailing data hay noncanonical header được báo |
| `shinobu.dff` | HFYBE / 140 | 370,688 / 370,688 B | 2,904 / 3,740 | Weight/texture checks qua; DFF có 4,733 byte sau clump chưa được parser diễn giải |
| `hanekawa.dff` | VIMYELV / 84 | 372,770 / 374,784 B | 3,113 / 3,622 | Không lỗi weight, thiếu texture, trailing data hay noncanonical header được báo |
| `senjo.dff` | WFYBE / 138 | 377,322 / 380,928 B | 3,154 / 3,696 | Không lỗi weight, thiếu texture, trailing data hay noncanonical header được báo |
| `nadeko.dff` | VLA2 / 115 | 553,002 / 555,008 B | 6,306 / 3,832 | Weight/texture checks qua; DFF có 20 byte sau clump chưa được parser diễn giải |
| `bkisshot.dff` | VBFYCRP / 11 | 1,543,642 / 1,546,240 B | 9,434 / 13,568 | Không lỗi weight, thiếu texture, trailing data hay noncanonical header được báo; pair nhỉnh hơn 1.5 MB thập phân |
| `Itsuwa Original.dff` | WFYRI / 91 | 1,867,631 / 1,869,824 B | 18,447 / 17,360 | Weight/texture checks qua; lớn hơn ngưỡng nhẹ và mesh gần Ganyu |

`ReiAyanami2` là ứng viên nhẹ nhất đã kiểm tra: cặp 136 KB và 1,601 triangles. `hanekawa` cũng qua các kiểm tra tĩnh với 3,622 triangles. Cả hai đều nhỏ hơn Ganyu (21,244) và ZeroTwo (16,867) về mesh, và cùng `senjo` tạo thành ba ứng viên sạch dưới 5,000 triangles. Các target lịch sử của Rei và Hanekawa lần lượt là GANG5 và CIVMALE; target Eagle vẫn cần được chọn theo danh sách NPC. Chưa xác nhận bằng hình ảnh rằng tên workbook trùng nhân vật thực tế. `shinobu` và `nadeko` không được gọi là hoàn toàn sạch vì có byte cuối chưa diễn giải.

Không đưa raw Alita và REM vào pilot: Alita có 220 vertices dùng 4 influences trong khi header khai báo tối đa 3; REM có 68 vertices với weight sum ngoài tolerance. Ganyu và ZeroTwo không có các lỗi đó trong phép đo này, nhưng mesh của chúng có 21,244 và 16,867 triangles nên không gọi là low-poly.

### Đối chiếu với các target Eagle

Đã đọc chính xác `BFYST.dff/.txd`, `WFYST.dff/.txd`, `WFYRI.dff/.txd` trong `Project Eagle\gta sa clean\gta sa clean\S&S\Cdimages\default\COMPONENTPEDS.img`. Các DFF lần lượt có 1,171 / 1,261; 1,100 / 1,087; và 1,215 / 1,118 vertices / triangles. DFF+TXD gốc lần lượt là 223,972 B, 233,466 B, và 256,457 B. Cả ba target có cùng skeleton 33 frame: 32 bone IDs, cùng hierarchy và cùng quan hệ bone cha gần nhất. Cả bảy ứng viên mới khớp đủ bộ IDs và mapping cha này, nên có bằng chứng tương thích cấu trúc mạnh hơn việc chỉ so frame count.

Các dòng `peds.ide` Eagle đang ghi BFYST là `CIVFEMALE / woman`, WFYST là `CIVFEMALE / sexywoman`, và WFYRI là `CIVFEMALE / sexywoman`. Các dòng này không dùng nhãn `Casual_Average`; nếu nhãn đó đến từ loader hoặc catalog khác thì cần đối chiếu riêng. Chỉ thay DFF/TXD giữ nguyên các trường ped/voice/animation đang có.

Toàn bộ 11 cặp trong audit đã được so byte với IMG payload theo đúng source file size, bỏ sector padding. File trích RAR và payload IMG khớp byte/hash; CRC32 tính lại khớp metadata RAR từ audit cũ, gồm cả bốn cặp ban đầu Alita/REM/Ganyu/ZeroTwo. Các file trích ở staging để đối chiếu lại; nguồn RAR và Eagle vẫn chỉ đọc.

Hai model Eagle `male01.dff` và `bmycr.dff` cũng được đọc làm mẫu dân sự. Chúng có 33 frame và cùng hierarchy/bone IDs số như các ứng viên. Mỗi geometry khai báo skin 32 bone; các kiểm tra không thấy bone index hoạt động sai hoặc vertex zero-weight. Đây là bằng chứng cấu trúc, chưa chứng minh biến dạng tốt trong animation hay phù hợp mọi vai trò.

Hai mục weight của mẫu đầu cần xem lại trước khi tái sử dụng: header Alita khai báo tối đa 3 influences nhưng 220 vertices có 4 influences dương; REM có 68 vertices có weight sum lệch khỏi 1 quá tolerance 1e-4. Ganyu và ZeroTwo không có các lỗi này trong kiểm tra. Tên texture material mà parser đọc được đều có trong TXD cặp; không báo thiếu tên. Texture ZeroTwo có `body00_MikuAp_b` và `face_MikuAp_b`, cho thấy nhãn workbook không đủ để xác nhận hình ảnh.

Audit JSON giữ liên kết material theo geometry, histogram bone, kiểm tra weight, kích thước texture, hash, đường dẫn member RAR và đối chiếu Eagle. Decoder dùng lại có thể không hỗ trợ mọi raster format RenderWare; parse sạch không thay cho kiểm tra render runtime. Chưa thử animation, tầm nhìn, tải population hoặc hiệu năng trong game. Target và đường nạp Eagle cần chọn riêng khỏi mapping Underground cũ.

Evidence: [npc-reuse-audit.json](npc-reuse-audit.json). Extraction and inspection script: [npc_reuse_inspect.py](../../../staging/project-eagle/npc_reuse_inspect.py). Extracted pairs and previews are under `staging\project-eagle\npc-reuse-survey`.
