# Loading artwork Project Eagle — inventory và kế hoạch review

Khảo sát ngày **14/10/2026**, giờ Asia/Saigon. Game mục tiêu: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`.

Nhận diện được đối chiếu lại với file hiện tại: `data\Changelog.txt` ghi **v1.3 / June 2026**; `PECore.log` đang lưu build **Jun 15 2026** và **GTA SA v1.0 HOODLUM**. Log này ghi phiên 13/10/2026, không phải một phép chạy mới ngày khảo sát.

**Chỉ đọc game, trích tài nguyên và lập kế hoạch. Chưa tạo artwork Genshin mới, rebuild/cài TXD, thay logo/menu/scene, hoặc chạy game để nghiệm thu.** Aether F2, NPC pilot, radio, trainer, loader config, save và Underground nằm ngoài phạm vi thay đổi.

## Kết luận cần dùng khi chọn artwork

- Đường loading trong executable hiện tại mở **`models\txd\LOADSCS.txd`**, chọn texture `title_pc_US` và các tên `loadsc1`…`loadsc14` **bên trong dictionary này**. Đây là bộ widescreen Stars & Stripes/Eagle, không phải 14 file SA vuông cùng tên bên cạnh. Kết luận dựa trên disassembly cục bộ; chưa đo file access hoặc hình cuối cùng sau mọi ASI hook trong runtime.
- **`New Official Loading Themes` là theme nhạc:** các file được log cài là WAV `GENRL\Bank_076\sound_001…008.wav`; không có TXD artwork trong thư mục này. Không chọn thư mục này làm đường cài ảnh.
- `gta3.std.stream` bị tắt nhưng **`gta3.std.sprites` vẫn được log nạp**. Vì thế phải kiểm tra đường thay ảnh qua sprites riêng; không bật lại streaming để thử loading.
- Ưu tiên nghệ thuật: **vẽ lại cả poster bằng anime/cel shading, giữ cấu trúc bố cục GTA và đặt nhân vật Genshin vào đời sống đô thị**. Aether dẫn bộ ảnh; các nhân vật khác trong bảng dưới chỉ là đề xuất để người dùng chọn. Không ghép nhân vật lên screenshot.
- Thử kỹ thuật sau khi có yêu cầu triển khai: **một member `LOADSC3` trong bản sao `LOADSCS.txd`**, chủ đề Aether lái xe. Không thay cả bộ trước khi xác minh nạp đúng, tỉ lệ và fade.

## Bộ ảnh và dữ liệu đối chiếu

- [Gallery toàn bộ texture đã decode](../../../staging/project-eagle/loading-screens/gallery.html) — mỗi ảnh có ID, source và thông số; các texture menu được tách để không nhầm phạm vi.
- [Manifest JSON](manifest.json) — đường nguồn, SHA-256 nguồn/bản trích, member/texture, codec, kích thước, mip và alpha.
- [Contact sheet bộ LOADSCS](../../../staging/project-eagle/loading-screens/previews/loadscs-posters.jpg) — 14 poster chính, đối chiếu texture ID và tên.
- [Trace loading/render và bằng chứng](loading-trace.md).
- [PNG startup nhúng trong PECore](../../../staging/project-eagle/loading-screens/source/pe-resources/PECore-RCDATA-200.png) — resource `E0001`, tách khỏi poster loading.
- [Staging index](../../../staging/project-eagle/loading-screens/README.md) — raw TXD, PNG và script chỉ đọc.

Đã trích **25 dictionary TXD, 75 texture/75 PNG**, tổng raw **43.162.812 byte**, không có gap decode trong các texture được chọn. Codec gặp: **71 DXT1, 3 DXT3, 1 X8R8G8B8**, native **D3D9**; tất cả texture trong inventory này có **một mip**. PNG là preview decode; native chunk, encoded raster và file TXD là những loại hash khác nhau. Raw source được copy nguyên byte, không phải TXD tái dựng. Decoder DXT1/DXT3 được đối chiếu với Pillow DDS: RGB lệch tối đa một mức do lượng tử RGB565, alpha khớp; uncompressed X8R8G8B8 khớp qua kiểm tra channel order độc lập. Xem [biên bản kiểm decoder](../../../staging/project-eagle/loading-screens/decode-validation.json).

Ngoài TXD có **một PNG nhúng** `PECore.asi::RCDATA/200/1033`, đã trích nguyên 166.605 byte: **640×640, RGBA 8-bit, có alpha**, không có mip theo nghĩa TXD. Manifest có mục `embedded_resources` riêng, không cộng nó thành texture thứ 76 trong TXD. Log/changelog mô tả splash khởi động PECore 5 giây; việc resource này được chính window đó vẽ vẫn chưa được chứng minh bằng call flow/runtime.

| Nhóm trên đĩa | Nội dung trích thực tế | Vai trò/độ xác minh |
| --- | --- | --- |
| `models\txd\LOADSCS.txd` | 17 texture: NVIDIA, EAX, `LOADSC1`…`LOADSC14`, `title_pc_US` | Dictionary được hàm loading cục bộ mở; poster và title là mục tiêu kỹ thuật chính. Hai vendor logo chưa được chứng minh hiển thị trong luồng đã trace. |
| `models\txd\loadsc0.txd`…`loadsc14.txd` | 15 ảnh 512×512, bộ GTA SA, logo/text bake trong tranh | Có file; luồng `LoadSplashes` đã trace không mở chúng riêng. Tham khảo bố cục; không tự cài từng file này. |
| `models\txd\LOADSUK.txd` | 15 texture SA 512×512, nhiều variant pose/background khác bộ loose | Variant có mặt; chưa xác minh đường chọn trong Eagle hiện tại. Không đồng nhất theo tên. |
| `models\txd\load0uk.txd` | Logo SA và legal, 512×512 | Candidate title variant, chưa chứng minh active. |
| `models\txd\splash1.txd`, `splash2.txd`, `splash3.txd` | Hai postcard “Greetings from Vice City”, 512×256; dictionary splash3 rỗng | Có file; chưa chứng minh là startup splash thực tế. Không gọi số 1/2/3 là trình tự. |
| `models\fronten1/2/3.txd`, `fronten_pc.txd` | 25 texture: logo radio/arrow, atlas nền menu/map, mảnh viền, cursor | `LoadAllTextures` có đường nạp riêng. Không phải 25 loading screen, ngoài phạm vi artwork. |
| `plugins\CustomStartScreenByDarkP1xel.asi` + INI XYZ | Plugin và thông số camera/điểm trong thế giới | Candidate scene 3D; không có bằng chứng nó là pack ảnh loading. Chi tiết static và gap trong trace. |
| `PECore.asi::RCDATA/200/1033` | PNG Project Eagle 640×640, nền trong suốt | Resource startup candidate tách riêng; PECore splash 5 giây có log/changelog, resource-to-window use chưa nghiệm thu. |

Inventory giới hạn ở candidate loading/menu được yêu cầu và lookup basename nhẹ trong `models`/`modloader`; không phải scan toàn bộ archive thế giới. `archive_member=null` nghĩa là source TXD loose, không phải member IMG. Trong TXD, tên texture được ghi ở từng entry `textures`; chữ hoa/thường phải được bảo toàn khi đóng gói lại.

## Những gì nhìn thấy trong ảnh trích

### Bộ chính: LOADSCS

Đây là poster đã ghép hoàn chỉnh, **một raster cho mỗi khung**, không có lớp nhân vật/background/logo riêng trong TXD. Ba khung đầu 3840×2160 thiên về phố, pickup và xe thể thao. Các khung sau chủ yếu 1920×1080 dùng nền gradient tím/xanh/đỏ, silhouette thành phố hoặc đồi và nhân vật lớn ở nửa phải. `LOADSC11` là 2000×1124; `title_pc_US` là 3800×2048. Không chuẩn hóa chúng về một kích thước chung chỉ vì gọi là widescreen.

Nhân vật có contour đen rõ, mảng shadow ít cấp, màu áo tách mạnh khỏi nền; background giảm chi tiết để đọc được silhouette. Logo **Grand Theft Auto / Stars and Stripes** đã bake vào phần trái dưới của poster. Title có biểu tượng **Project Eagle**, legal và các logo nhỏ bake trong raster khác. Không coi chúng là text được game vẽ động.

`LOADSC7` (`T0050`) và `LOADSC14` (`T0056`) có **encoded raster payload SHA-256 giống hệt nhau**, tức cùng pixel payload; native chunk hash khác vì metadata/tên member khác. Không tự xóa một texture hoặc coi hai số là hai cảnh khác nhau. Thứ tự member trong archive cũng không phải thứ tự hiển thị.

### Bộ SA và các phần ngoài mục tiêu

Bộ SA vuông dùng nền khói beige/green/teal, nhân vật lớn, đường phố/xe/nhà ít màu và logo góc trái dưới. `loadsc0` là collage với logo giữa và legal ở đáy. LOADSUK có những variant khác thực sự, ví dụ hai người/cảnh xe khác; không xem chúng là bản sao chỉ qua basename.

Các `back*` trong fronten2 là atlas/mảnh menu: preview có vùng nhiễu màu lớn và dải ảnh phong cảnh nhỏ phía dưới. Đây là nội dung raster đã decode, **chưa phải bằng chứng lỗi file hoặc vùng sẽ xuất hiện trên màn hình**; cần biết UV/rect của menu. Không dùng chúng làm tranh loading full screen. Hai postcard Vice City có chữ bake, còn sprite cursor/radio/arrow có chức năng UI riêng.

## Render và vùng cần giữ

Disassembly `CLoadingScreen::LoadSplashes` tại `0x5900B0` xác nhận directory `MODELS\TXD\`, slot `loadscs`, file `loadscs.txd`, title và tên `loadsc%d`. Hàm tạo permutation và gán **7 sprite: một title và sáu poster chọn trong các index 1…14**. Vì vậy bộ có 14 poster không có nghĩa mỗi lượt sẽ thấy cả 14 hay lần nào cũng bắt đầu ở `LOADSC1`.

PECore có module `[Splash]` khởi động riêng và log bản vá loading bar: expected file count tăng từ 100 lên 402. Cấu hình bật `TransparentMenu`, log ghi patch frontend background/scaling. Scan hẹp PECore/Modloader_Patch chưa thấy string hoặc direct reference thay `LOADSCS`/hàm loading cơ sở; kết quả âm tính này **không loại trừ hook gián tiếp/signature scanning**. REA provider không sẵn; phân tích dùng pefile/Capstone có sẵn, không setup thêm. Vì vậy source trên là đường cơ sở đã trace, không phải lời cam kết toàn bộ render sau hook đã được quan sát.

`CLoadingScreen::RenderSplash` tại `0x58FF60` vẽ rect phủ viewport `(-5,-5,width+5,height+5)`, clamp và có fade. Đường cơ sở này không có tile/layer cho từng nhân vật. **Kết quả aspect cuối cùng sau WidescreenFix và các ASI hook vẫn cần runtime**: INI `FrontendAspectRatio=16:9` là cấu hình, chưa đủ để kết luận mọi ảnh được center-crop, letterbox hay stretch. Không thiết kế artwork dựa trên một quy tắc crop chưa đo.

Loading bar, progress/status text và fade là phần renderer/UI riêng; **không bake chúng vào tranh mới**. Trước khi runtime xác định rect thật, có thể dùng vùng ít chi tiết ở dải đáy khoảng 12–15% như một *dự phòng thiết kế*, không gọi đó là safe area đã đo. Mặt, bàn tay và chi tiết nhận diện không chạm mép ngoài. Giữ khoảng trống logo ở trái dưới theo đúng raster đích, không mặc định vị trí giống nhau giữa SA và LOADSCS.

Logo đang bake nên khi vẽ lại cần tách thành lớp compositing được kiểm tra; chưa có sẵn alpha logo độc lập trong archive này. Bước artwork giữ nhận diện/logo gốc theo phạm vi hiện tại; thay logo hay title là lựa chọn riêng, chưa được duyệt. Không yêu cầu công cụ sinh ảnh tự viết lại các chữ trong logo.

## Hướng nghệ thuật ưu tiên

Giữ tóc, màu mắt, silhouette và chi tiết nhận diện của Genshin. Chuyển trang phục thành biến thể phố có chủ ý: áo khoác, bomber, vest, kính, dây chuyền hoặc trim gợi màu nhân vật; không bỏ mọi chi tiết đến mức thành nhân vật anime chung. Aether dùng tóc vàng, bím tóc và palette đen/trắng/vàng; trang phục có thể thích nghi để ngồi xe/đi phố nhưng vẫn nhận ra ngay.

Mỗi poster được vẽ như **một cảnh thống nhất**: nhân vật, xe, đường, ánh sáng và bóng cùng phối cảnh. Dùng pose đọc rõ ở thumbnail, contour đậm và 2–3 cấp cel shadow; background là hình khối đô thị có biển hiệu, đèn, palm trees, đường ven biển hoặc garage, không bê UI/screenshot gameplay vào tranh. Ưu tiên không khí lái xe dạo phố/nghe radio; vũ khí là lựa chọn props riêng nếu sau này muốn giữ mức action của khung gốc.

| Cách làm | Kết quả | Đánh đổi |
| --- | --- | --- |
| Giữ nguyên background/raster gốc, chỉ vẽ lại nhân vật vào đúng pose | Rất gần bộ hiện có, kiểm tra mapping nhanh | Dễ tạo cảm giác ghép lớp nếu style/ánh sáng khác; nền và trang phục ít đổi; logo vẫn bake. |
| **Vẽ lại toàn bộ khung, giữ nhịp bố cục GTA** — ưu tiên | Nhân vật/cảnh/xe thống nhất theo anime; mỗi khung có câu chuyện Genshin sống trong Eagle | Cần duyệt sketch/composition, kiểm tra nhận diện nhân vật và logo layer; khối lượng art cao hơn. |

Phương án ưu tiên giữ **vị trí trọng tâm, khoảng trống và palette tương phản** của khung cũ, nhưng cho phép đổi pose/phụ kiện đủ để nhân vật hòa vào cảnh. Không phải tracing từng nét, cũng không phải chèn render nhân vật lên một nền có sẵn.

## Mapping đề xuất cho bộ poster thực sự được đường loading tham chiếu

Tất cả nhân vật trừ trọng tâm Aether là **đề xuất chưa duyệt**, không lấy rating/ped roster làm artwork roster. Các bảng `npc-rosters` hiện để trống Char dự kiến nên không cung cấp một danh sách artwork đã chốt. Số `LOADSCn` là tên texture, không phải thứ tự slideshow.

Thông số trong cột cuối là **đích đóng gói giữ nguyên của texture hiện tại**, chưa phải yêu cầu sinh ảnh mới trong lượt khảo sát. Mỗi hàng dùng một PNG master RGB không bake bar/status/fade; bản TXD D3D9 giữ đúng name, dimensions, codec và mip count theo manifest. Với mục tiêu DXT1, không tự thêm alpha. `LOADSC6` đang là X8R8G8B8 nên không đổi sang DXT1 chỉ để đồng nhất.

| Texture / khung hiện tại | Nhân vật và cảnh đề xuất | Pose / màu / bố cục | Export và đóng gói |
| --- | --- | --- | --- |
| `T0044 / LOADSC1`: nữ ngoái vai, phố olive | **Yelan** đi qua phố thương mại sau chuyến lái xe | Ngoái vai nửa phải, jacket navy/trim xanh, nền olive/cream và cao ốc nhạt; logo trái dưới | 3840×2160, DXT1; member của LOADSCS |
| `T0045 / LOADSC2`: cowboy và pickup, palm sunset | **Dehya** cạnh pickup ở garage ven đường | Góc 3/4 phải, jacket đỏ/đen, chìa khóa hoặc radio; cam cát, palm/power line; logo trái dưới | 3840×2160, DXT1; cùng dictionary |
| **`T0046 / LOADSC3`: convoy xe thể thao, phố/bridge xanh** | **Aether**, xe coupe vàng/đen và xe bạn đồng hành — pilot ưu tiên | Aether ở ghế lái nhìn qua cửa hoặc đứng nửa phải cạnh xe; góc xe chéo giữ motion, nền cobalt/indigo, vàng làm accent, logo trái dưới | **3840×2160, DXT1; thay đúng một member trong bản copy LOADSCS** |
| `T0047 / LOADSC4`: người vest trắng, đồi tím/đỏ | **Kaeya** trước club trên sườn đồi | Vest trắng/trim xanh, cầm chìa khóa/điện thoại, trọng tâm phải; gradient tím/đỏ giữ nhịp gốc | 1920×1080, DXT1 |
| `T0048 / LOADSC5`: người vest sát mép phải | **Diluc** rời lounge, xe đỗ ở rìa phố | Nửa thân 3/4, tóc đỏ/tux đen, tay sửa cổ tay áo; mận đỏ/indigo, nhiều khoảng trống trái | 1920×1080, DXT1 |
| `T0049 / LOADSC6`: nữ với cocktail, skyline magenta | **Beidou** ở rooftop bar ven cảng | Ngoái vai, jacket khoác vai, ly nước/đồ uống tùy duyệt; magenta/violet và silhouette cảng | 1920×1080, **X8R8G8B8** |
| `T0050 / LOADSC7`: người áo khoác, prop chéo tiền cảnh | **Zhongli** bên sedan tại đường ven biển | Coat charcoal, tay cầm chìa khóa/điện thoại tạo đường chéo, mắt nhìn ngoài khung; violet/crimson | 1920×1080, DXT1 |
| `T0051 / LOADSC8`: nam vest đang chỉnh áo | **Diluc** trước garage đêm | Pose kéo/chỉnh jacket nửa phải, xe và biển hiệu silhouette; đỏ sâu/violet; không đổi thành wallpaper centered | 1920×1080, DXT1 |
| `T0052 / LOADSC9`: nhân vật cúi người, nền cây/đồi | **Kazuha** tựa xe thể thao ở overlook | Lean nghiêng thấp, jacket trắng/đỏ, radio portable; đường chân trời thấp, indigo/cam hoàng hôn | 1920×1080, DXT1 |
| `T0053 / LOADSC10`: hai người, nhân vật chính phía phải | **Keqing + Yelan** ở phố neon | Một người trước, một người nhỏ hơn phía sau trái, bất đối xứng giữ depth; lilac/blue, biển hiệu ít chi tiết | 1920×1080, DXT1 |
| `T0054 / LOADSC11`: ba sedan/limousine nhìn chéo | **Ningguang** và đoàn xe đón khách | Xe vẫn là chủ thể, nhân vật nhỏ cạnh xe ngoài cùng phải; pearl/cream, teal, đỏ/tím ở nền | **2000×1124**, DXT1; giữ kích thước riêng |
| `T0055 / LOADSC12`: nam vest chắp tay | **Zhongli** trước khách sạn/casino | Trọng tâm phải, tay chỉnh găng/khuy áo, vàng trim trên charcoal; burgundy/indigo, background rất giản lược | 1920×1080, DXT1 |
| `T0057 / LOADSC13`: nam mở vali, background xe | **Aether** mở vali đồ du lịch/đĩa nhạc trên xe | Nửa thân phải, vật dụng kể chuyện roadtrip; đen/vàng và neon xanh/tím, giữ silhouette vali | 1920×1080, DXT1 |
| `T0056 / LOADSC14`: pixel payload trùng khung 7 | **Zhongli** hoặc **Aether**, biến thể coastal dusk chỉ nếu muốn khung riêng | Dùng cùng brief của 7 để đồng nhất; hoặc duyệt biến thể mới; chưa mặc định tăng roster | 1920×1080, DXT1; vẫn giữ member riêng |

Để bộ không quá loãng, có thể chọn **Aether + 4–6 nhân vật** rồi tái sử dụng với outfit/cảnh khác. Không cần 14 nhân vật khác nhau cho 14 texture.

### Mapping phần được giữ làm tham khảo/ngoài đợt thay chính

| Screen/texture | Hướng dùng hoặc ý tưởng nếu người dùng mở rộng phạm vi | Thông số và route |
| --- | --- | --- |
| `loadsc1…14.txd` loose + `LOADSUK/loadsc1…14` | Tham khảo nhịp SA: bandana/nhân vật → Aether street jacket; người dựa xe → Aether roadtrip; officer/detective → Yelan/Keqing; BMX → Kazuha; portrait phố/beach → Dehya/Beidou; nhóm bên lowrider → Aether + Kazuha; vest/Chinatown → Zhongli + Ningguang. Chỉ lập mapping riêng nếu route này được chọn thực sự. | 512×512 DXT1 theo từng entry; **không cài vào route chính chỉ vì tên giống nhau**. Các variant phải đối chiếu từng preview. |
| `LOADSCS/title_pc_US` | Title Eagle hiện tại giữ nguyên. Collage Aether và các chuyến đi chỉ là hướng cho một yêu cầu title riêng. | 3800×2048 DXT1; title và legal cần approval phạm vi riêng. |
| `loadsc0`, `LOADSUK/loadscUK`, `load0uk` | Collage/logo/legal SA, giữ như source reference. | 512×512; activation chưa xác minh. |
| `LOADSCS/nvidia`, `eax` | Vendor startup logos; giữ nguyên. | 2048×1024 DXT1; route hiển thị chưa chứng minh. |
| `E0001 / PECore RCDATA/200/1033` | Logo startup Project Eagle nhúng; giữ nguyên, ngoài artwork batch. | 640×640 PNG/RGBA; không thay ASI/resource. |
| `splash1`, `splash2`, dictionary rỗng `splash3` | Postcard Vice City xanh/cam, giữ nguyên. Nếu được chọn sau này: silhouette Aether/xe ven biển với palm theo postcard. | 512×256 DXT1; không giả định thứ tự/active. |
| `fronten*` / scene CustomStartScreen | Menu atlas, radio icons, cursor hoặc scene 3D; không đưa vào artwork batch. | Cần tác vụ khác nếu người dùng muốn đổi. |

## Phép thử một screen sau yêu cầu triển khai

1. **Chốt artwork pilot và môi trường test:** duyệt brief Aether/LOADSC3, logo policy, một ảnh proof đúng ratio. Chọn bản thử riêng có save path đã xác minh và không bị agent gameplay/radio dùng; không chạy trên một lab đang được chỉnh đồng thời. Ghi resolution/aspect/settings đầu vào.
2. **Backup và build ngoài game:** dùng raw source có hash trong manifest; copy dictionary ra staging mới. Thay đúng texture `LOADSC3` trong bản copy, giữ name/case, native D3D9, 3840×2160, DXT1, mip count và opaque semantics. Giữ 16 member còn lại nguyên chunk nếu công cụ hỗ trợ; nếu tool tái serialize, phải so sánh pixel + metadata và báo khác biệt, không gọi là nguyên byte. Parse/decode lại output, so poster, mip/alpha và file size.
3. **Route ưu tiên cần nghiệm thu:** thư mục overlay riêng dạng `modloader\Genshin Loading Pilot\txd\loadscs.txd` qua `std.sprites`, dựa trên plugin docs/config/log đã trace. Đây là **whole dictionary replacement**, không phải đặt `LOADSC3.png` hay `loadsc3.txd` loose. Không sửa thư mục New Official Loading Themes, không bật std.stream, không ghi trực tiếp models\txd khi chưa thử overlay.
4. **Chứng minh đúng nguồn:** đọc log install của sprites và file-access trace nếu công cụ runtime có sẵn; chụp khi LOADSC3 thật sự được chọn. Sáu poster được chọn nên một lượt không xuất hiện pilot chưa chứng minh thất bại. Phân biệt overlay được nhận, file được mở, texture được chọn và hình đã render đúng. Nếu sprites route không hoạt động trên build này, dừng để review trace; fallback trực tiếp thay dictionary chỉ cân nhắc sau backup/approval triển khai, không tự bật plugin hoặc patch core.
5. **Visual/runtime test:** cold start/title, new game và load save thử riêng không ghi đè save; ghi nhận frame đang render và frame fade. Kiểm đúng nhân vật/logo, không méo mặt/bánh xe, không cắt đầu/tay, mép clamp, flash/đen, alpha halo, bar/status đọc được. Đo 16:9 trước; nếu dùng 4:3/ultrawide thì thử chúng riêng, không suy từ INI. So ít nhất một baseline với pilot về thời gian loading, peak RAM/VRAM nếu đo được và lỗi/crash; giữ dimensions/codec tránh tăng tài nguyên không cần thiết.
6. **Rollback:** gỡ/di chuyển đúng thư mục pilot ra ngoài modloader trong môi trường thử, cold start lại và xác minh trở về source gốc. Nếu đã dùng fallback direct replacement có duyệt, phục hồi TXD từ backup có hash. Hash config/exe/save phải giữ nguyên trong phạm vi phép thử. Chỉ nhân rộng sau một pilot đạt.

## Bằng chứng, giới hạn và quyết định còn lại

Local source/config/log/disassembly là nguồn quyết định; [loading-trace.md](loading-trace.md) ghi địa chỉ, path và nguồn tham khảo code. Community reverse-engineered source chỉ dùng để hỗ trợ tên/ý nghĩa hàm, không gọi là tài liệu chính thức Rockstar hoặc bằng chứng runtime Eagle.

[Audit đầu ra](evidence/root-audit.json) đối chiếu source/raw hash, dimensions 75 PNG, link local và hai vùng code loading của `gta_sa.exe`/`gta_pe.exe`. Snapshot hash của exe/config/plugin được giữ trong evidence; snapshot sau khảo sát không tự chứng minh chúng chưa từng đổi trước snapshot. Trong lượt này công cụ chỉ đọc game và ghi staging/docs.

**Đã trả lời:** inventory và decode candidate; phân biệt theme nhạc/ảnh; dictionary và tên texture của đường loading cơ sở; menu khác loading; bố cục/logo bake; kế hoạch art, packaging và rollback có phạm vi một member.

**Còn cần runtime:** hook/plugin cuối cùng và CustomStartScreen có active/scene gì; startup/movie/title ordering; ảnh từng lượt new/load save thật sự thấy; aspect/crop sau mọi hook; tọa độ UI safe area; hoạt động overlay std.sprites, thời gian/fade và chi phí tài nguyên. Khảo sát này không đưa ảnh tái tạo thay cho gap runtime.

**Người dùng chọn ở bước sau:** hướng vẽ lại toàn cảnh hoặc giữ nền; pilot Aether/LOADSC3; roster và outfit; giữ logo nào nếu mở rộng title/branding. Báo cáo dừng tại kế hoạch này.
