# Wibu World / Project Wibu — art direction hiện hành

## Bổ sung sau M07 — đa dạng loại trang phục

User duyệt M07 nhưng yêu cầu **không lặp váy xẻ cho mọi nhân vật**. Giữ thành thị, thanh lịch, nóng bỏng cho nhân vật trưởng thành nhưng đa dạng silhouette/chất liệu/phong cách: sporty, streetwear, denim, leather, phối áo/váy hoặc shorts, jumpsuit, cocktail hay resort theo tính cách/palette/motif gốc. Trong từng batch chủ động phân bổ loại outfit khác nhau, tránh cùng một công thức rồi đổi màu. Giữ tạo hình nhỏ tuổi trong trang phục/hành động phù hợp. Chỉ áp dụng các ảnh tiếp theo; không gen lại M07 đã pass.

## Cập nhật 01/11/2026 — thời trang nhân vật nữ trưởng thành

Người dùng duyệt L07 và Arlecchino v2, xác nhận hướng **thành thị nóng bỏng, tự tin, quyến rũ nhưng vẫn thanh lịch** cho nhân vật nữ trưởng thành. Ưu tiên biến thể cocktail/nightlife, đường cắt và phụ kiện hợp tính cách, tránh mặc định suit/trang phục nam tính khi không hợp brief. Giữ tóc, mắt, palette và chi tiết nhận diện gốc; không biến mọi người thành cùng một bộ đầm hoặc cùng pose. Arlecchino v2 và Candace/Nilou L06 v3 là mẫu tham chiếu đã duyệt. Hướng này áp dụng cho nhân vật trưởng thành; nhóm tạo hình nhỏ tuổi tiếp tục giữ trang phục và hành động phù hợp. Không tự gen lại các ảnh đã được duyệt để áp rule mới.

Cập nhật **14/10/2026**. Brief này đã được triển khai thành 14 poster và branding startup/title, thay thế các đề xuất Aether/nam trước. **Bản đầy đủ đã cài; người dùng đã tự test và xác nhận hoạt động tốt.** Xem [biên bản triển khai](wibu-world-implementation.md).

**Style revision mới nhất:** logo trắng–đen; artwork anime 2D phẳng, không dùng rendering 2.5D/ánh kim. Xem [revision 2D](style-revision-2d.md).

## Yêu cầu đã chốt từ người dùng

- **Artwork phong cách anime, bố cục poster GTA.** Vẽ cả nhân vật, xe và bối cảnh thành một cảnh thống nhất.
- **Chỉ nhân vật nữ Genshin.** Đủ 23 tên đã đưa; không dùng Aether hoặc nhân vật nam trong batch này. Không thêm người đi đường/driver vô danh làm loãng yêu cầu.
- **Outfit thời trang đô thị** nhưng giữ tóc, palette và các chi tiết nhận diện Genshin. Đây là lựa chọn người dùng đã trả lời, thay cho phương án giữ nguyên costume game.
- Chữ trên poster đổi thành **“Grand Theft Auto Wibu World”**, lettering gợi wordmark Genshin Impact.
- Nhận diện **“Project Wibu”** dùng **silhouette Hu Tao**, thay đại bàng ở cả title trong TXD và startup splash PECore được nghiên cứu riêng.

Việc chọn Aether F2 làm nhân vật chơi nằm ngoài batch artwork này; brief không đổi skin/player/trainer.

## Coverage 23 nhân vật trên 14 poster

**9 khung đôi + 5 khung đơn = 23 nhân vật**, mỗi tên có một khung chính. [Mapping JSON](wibu-world-screen-map.json) ghi screen, ID, nhân vật, scene, palette và đích export. Danh sách nguồn official ở [character-reference-research.md](character-reference-research.md), gồm cả Tsaritsa, Columbina và Vesna. Nguồn nhận diện đã được tìm; trước khi tạo từng ảnh vẫn cần xem đúng portrait/frame làm visual reference, không suy chi tiết trang phục từ tên hoặc snippet.

Một lượt loading cơ sở chọn sáu poster trong 14, nên coverage của cả bộ không đồng nghĩa mọi nhân vật xuất hiện trong mỗi lần mở game. Giữ nguyên renderer/randomization; không thêm hook để ép slideshow.

| Screen / manifest ID | Nhân vật | Scene, pose và outfit đề xuất | Palette | Đích đóng gói |
| --- | --- | --- | --- | --- |
| LOADSC1 / T0044 | **Yelan + Clorinde** | Boulevard buổi tối, sedan cạnh phố thương mại; Yelan ngoái vai tiền cảnh phải; Clorinde đứng cạnh cửa xe ở midground. Yelan: jacket navy có trim nhận diện; Clorinde: blazer/trench với mũ và phụ kiện đặc trưng. | Olive/cream, navy, ánh vàng | 3840×2160, DXT1 |
| LOADSC2 / T0045 | **Mavuika + Beidou** | Trạm dừng ven đường, motorcycle và pickup, palm sunset; Mavuika cạnh motorcycle; Beidou tựa pickup, hai silhouette chéo. Mavuika: biker jacket; Beidou: bomber/coat ven cảng, giữ eyepatch và màu đỏ/đen. | Cam hoàng hôn, đen/đỏ, vàng ấm | 3840×2160, DXT1 |
| LOADSC3 / T0046 | **Keqing + Ganyu** | Coupe và bridge đô thị, chuyến lái xe đêm; Keqing cạnh ghế lái tiền cảnh; Ganyu bên cửa hành khách, xe là đường chéo. Keqing: áo khoác đô thị tím; Ganyu: streetwear xanh/đen, giữ tóc và sừng nhận diện. | Cobalt/indigo, violet, cyan | 3840×2160, DXT1 |
| LOADSC4 / T0047 | **Chiori + Kirara** | Boutique trên phố dốc, xe delivery nhỏ; Chiori chính ở phải; Kirara mang hộp giao hàng ở lớp sau, logo trống trái dưới. Chiori: tailoring đen/vàng; Kirara: outfit giao hàng xanh/beige, giữ tai/đuôi đặc trưng. | Tím/đỏ nền, đen/vàng và xanh mint | 1920×1080, DXT1 |
| LOADSC5 / T0048 | **Jean + Lumine** | Garage sang, chuẩn bị roadtrip; Jean sửa cổ tay áo blazer; Lumine cầm chìa khóa bên coupe, hai người ở nửa phải. Jean: blazer trắng/navy; Lumine: ivory/gold street dress + jacket, giữ tóc/phụ kiện Traveler. | Charcoal, ivory/gold, burgundy | 1920×1080, DXT1 |
| LOADSC6 / T0049 | **Furina + Mona** | Rooftop lounge nhìn cảng, xe dưới phố; Furina ngoái vai tiền cảnh; Mona ngồi cạnh lan can, cùng ánh neon. Furina: fashion cape/jacket xanh trắng; Mona: jacket tím và phụ kiện sao, giữ dấu hiệu mũ/tóc. | Magenta/violet, navy, highlight trắng | 1920×1080, X8R8G8B8 |
| LOADSC7 / T0050 | **Raiden Shogun + Shenhe** | Đường ven biển đêm, sedan và gió mạnh; Raiden nửa thân phải; Shenhe đứng bên xe phía sau, áo/tóc tạo diagonal. Raiden: long jacket tím, giữ bím tóc/ornament; Shenhe: coat trắng/đen, điểm dây đỏ. | Violet, cyan băng, đỏ trầm | 1920×1080, DXT1 |
| LOADSC8 / T0051 **pilot** | **Hu Tao + Citlali** | Phố lễ hội đêm, đèn ấm và compact coupe; Hu Tao chính nửa phải với mũ/đuôi tóc đặc trưng; Citlali bên cạnh, tương tác tự nhiên. Hu Tao: coat burgundy/đen với mũ hoa; Citlali: layer/jacket lilac, giữ tóc/phụ kiện đặc trưng. | Burgundy/amber, lilac/pink, indigo | 1920×1080, DXT1 |
| LOADSC9 / T0052 | **Ayaka + Kokomi** | Overlook/boardwalk ven biển, xe đỗ lúc chạng vạng; Ayaka tựa cạnh xe; Kokomi ở lan can, silhouette lệch phải và horizon thấp. Ayaka: pleated street dress/jacket xanh bạc; Kokomi: coastal jacket/knit pastel giữ palette và tóc. | Blue hour, pearl, coral, violet | 1920×1080, DXT1 |
| LOADSC10 / T0053 | **Tsaritsa** | Đại lộ mùa đông, khách sạn và xe sang; Một nhân vật chính nửa phải; urban formal lấy dấu hiệu nhận diện từ trailer official. Urban formal mùa đông; chốt tóc/ornament từ trailer Tsaritsa trước khi dựng hình. | Ice blue, silver, charcoal | 1920×1080, DXT1 |
| LOADSC11 / T0054 | **Vesna** | Đoàn sedan trước khách sạn/thương cảng; Vesna phía phải cạnh xe chính; xe vẫn chiếm foreground, thiết kế dựa teaser official. Urban tailoring/coat; màu và silhouette nhận diện lấy từ teaser/trailer Vesna. | Cream/teal, plum và đỏ nền | 2000×1124, DXT1 |
| LOADSC12 / T0055 | **Columbina** | Nhà hát hoặc lounge về đêm, limousine phía sau; Portrait nửa thân phải, pose tĩnh và bàn tay đọc rõ; nhận diện theo official trailer. Street formal ivory/đen/đỏ; giữ mắt/phụ kiện và silhouette từ official Columbina. | Ivory, đen/đỏ, indigo | 1920×1080, DXT1 |
| LOADSC13 / T0057 | **Xiangling** | Night market/food truck, hộp đồ ăn và xe; Xiangling mở hộp đồ ăn ở foreground phải, biển hiệu/xe giảm chi tiết phía sau. Work jacket/apron thời trang đỏ/amber, giữ tóc và motif nhận diện Xiangling. | Amber, đỏ ấm, teal/neon | 1920×1080, DXT1 |
| LOADSC14 / T0056 | **Barbara** | Pier/đại lộ ven biển, convertible và radio; Barbara portrait nửa phải với portable player/earphones; ánh biển ở background. Idol streetwear trắng/xanh; giữ tóc/phụ kiện Barbara, outfit phù hợp cảnh radio ven biển. | Sky blue, ivory, pink sunset | 1920×1080, DXT1 |

Tất cả đích TXD giữ native **D3D9**, **một mip**, raster opaque theo nguồn hiện tại. Kích thước trên là đích trong game; composition master có thể lớn hơn và được kiểm ở ratio cuối trước khi export. Không đổi toàn bộ về 1920×1080, không áp DXT1 cho LOADSC6 đang X8R8G8B8. LOADSC7/14 gốc trùng pixel payload nhưng bộ mới chủ động dùng hai cảnh khác nhau để đủ roster.

## Ngôn ngữ hình ảnh

Giữ foreground lệch phải và khoảng trống trái dưới cho logo như bộ gốc. Với khung đôi, một nhân vật chính ở foreground và một nhân vật ở midground; cả hai phải nhận diện được ở preview. Tránh nhét thêm nhóm đông hoặc để nhân vật phụ chỉ còn khuôn mặt vài pixel.

Lineart rõ, flat fills và một cấp hard-edged cel shadow cho mỗi vật liệu; mắt/tóc/shading theo anime. Bối cảnh có đường đô thị, xe, garage, biển hiệu, palm trees, ven biển và neon được minh họa cùng perspective/ánh sáng với nhân vật. Dùng mảng nền giản lược như GTA poster; không dựng một fantasy wallpaper rồi đặt logo GTA lên.

Khóa identity từ nguồn official trước mỗi prompt: tóc/màu mắt/phụ kiện đặc trưng; chỉ thay outfit theo brief đô thị đã chốt. Tsaritsa/Vesna/Columbina dùng official footage/portrait tương ứng, không coi fan design là canonical. Không thêm tên nhân vật hoặc khẩu hiệu lên poster nếu brief không yêu cầu.

Mặt/tay/phụ kiện chính nằm trong vùng trung tâm an toàn; đáy có khoảng ít chi tiết dự phòng cho UI. Safe area 12–15% chỉ là dự phòng art, chưa phải tọa độ đo runtime. **Loading bar, status và fade do renderer vẽ, không bake vào tranh.**

## Wordmark Grand Theft Auto Wibu World

- Chuỗi chữ chính xác: **Grand Theft Auto Wibu World**. Có thể dàn “GRAND THEFT AUTO” nhỏ hơn bên trên và “WIBU WORLD” lớn hơn bên dưới; bố cục vẫn ở vùng logo trái dưới của từng khung.
- Lettering serif fantasy có tương phản nét dày/mảnh, đầu nét sắc và ornament nhỏ gợi wordmark Genshin. Tham khảo logo trên [website chính thức](https://genshin.hoyoverse.com/en/home); không gán một tên font “chính thức” chưa có bằng chứng.
- Thiết kế wordmark một lần thành asset compositing riêng, rồi dùng thống nhất trên 14 poster. Logo dùng chữ trắng và viền đen, phẳng; không vàng/ánh kim, bevel hoặc gradient.
- Trong bản đã triển khai, mỗi prompt dùng master wordmark trắng/đen làm reference cùng pilot style đã duyệt; sinh toàn poster trong một cảnh thống nhất. Kiểm spelling và hình logo ở từng output; không tuyên bố pixel logo giống hệt master.
- Logo GTA/S&S cũ đang bake, nên poster mới cần xuất toàn raster hoàn chỉnh với logo Wibu World. Không có một config string để đổi logo này.
- Title Project Wibu là asset riêng, không thay nó bằng dòng Grand Theft Auto Wibu World.

## Project Wibu + silhouette Hu Tao: hai bề mặt khác nhau

[Research branding](project-wibu-branding-research.md) đã trace cụ thể resource startup. Có ba phần nhận diện hiển thị cần phân biệt:

| Đích | Nguồn hiện tại | Thiết kế mới / route dự kiến |
| --- | --- | --- |
| 14 poster | LOADSCS.txd / LOADSC1…14 | Grand Theft Auto Wibu World, chữ gợi Genshin; whole-dictionary override qua std.sprites sau pilot. |
| Title trong game | LOADSCS.txd / title_pc_US, T0058, 3800×2048 DXT1 | Project Wibu + silhouette Hu Tao; member title trong cùng TXD. Giữ vùng legal/credit gốc, không bỏ credit khi thay wordmark. |
| Splash khởi động core | PECore.asi / RCDATA 10/200/1033, E0001, 640×640 PNG RGBA | Project Wibu + silhouette Hu Tao, alpha trong suốt; resource-aware PE update trên bản sao staging, tách khỏi ModLoader TXD. |

Silhouette Hu Tao ưu tiên hình khối đọc rõ: mũ hoa, mái tóc và hai đuôi tóc dài, coat/pose đặc trưng. Đặt chữ **Project Wibu** thành hai dòng, giữ khoảng trống để đọc; dùng silhouette đen với keyline trắng và chữ trắng–đen phẳng. Silhouette không cần mắt/chi tiết face như portrait; nhận diện phải đến từ outline và phụ kiện. Với title lớn có thể dùng mark master lớn hơn, không phóng một bitmap 640×640 lên toàn title.

PECore còn vẽ riêng **“Project Eagle is loading”** bằng GDI+; dòng đó không nằm trong PNG. Để branding startup nhất quán, đưa **“Project Wibu is loading”** vào checklist triển khai tương lai như một thay đổi text data riêng, sau khi kiểm đúng literal và đường vẽ. Không đổi class name, tên executable/ASI, thư mục cài, save path hay core hook theo yêu cầu branding.

PNG resource cũ chỉ có 3 byte khoảng trống trước resource tiếp theo. Vì vậy ảnh mới khác kích thước byte phải dùng PE resource-aware update, không ghi đè blob tại offset cũ. Research tĩnh đã chứng minh resource-to-render chain; runtime về alpha, bounding box, caption và thời lượng còn chưa thử.

## Trình tự production ban đầu

1. **Pilot artwork LOADSC8: Hu Tao + Citlali**, scene lễ hội phố đêm, outfit đô thị, target 1920×1080. Đây là pilot mới theo roster nữ, thay cho pilot Aether/LOADSC3 trước.
2. Tạo wordmark **Grand Theft Auto Wibu World** và mark **Project Wibu / Hu Tao silhouette**; kiểm spelling, đọc ở thumbnail và alpha. Tạo ảnh dùng ImageGen built-in khi có yêu cầu tạo; chưa gọi ImageGen trong lượt cập nhật brief này.
3. Review một poster hoàn chỉnh và hai mark trước khi nhân rộng 13 poster còn lại. Coverage JSON phải còn đúng 23/23, không có nam hoặc nhân vật ngoài brief.
4. Chuẩn bị title riêng (3800×2048), giữ legal/credits; chuẩn bị startup PNG 640×640 với alpha thật. Đây là hai output, không dùng cùng canvas full screen.
5. Sau yêu cầu cài: thử overlay một member trong bản copy LOADSCS trước, rồi mới đưa đủ 14 poster + title để branding đồng bộ. Resource PECore/caption thử trong pha riêng, backup và rollback riêng. Không bật std.stream hoặc đổi core hooks để cài artwork.

Trình tự trên là kế hoạch production ban đầu. Người dùng đã yêu cầu triển khai và duyệt pilot 2D cho cả bộ; tất cả poster, title, startup PNG và caption đã tạo/đóng gói/cài. Tài nguyên gốc, draft bị từ chối, manifest và contact sheet trích xuất vẫn giữ để đối chiếu. Người dùng đã tự thực hiện test và xác nhận hoạt động tốt ngày 14/10/2026.


# Bổ sung 01/11/2026 — phân biệt tư thế trong ảnh nhóm

Hai nhân vật trong cùng artwork phải khác rõ tư thế, hướng thân và vị trí/hành động tay. Không dùng hai dáng đứng cùng trục hoặc đối xứng rồi chỉ đổi vật cầm. Ưu tiên đứng–ngồi, làm việc–nghỉ, hoặc hai hành động có silhouette khác nhau. Giữ nhân vật lớn và style anime 2D đã duyệt. User yêu cầu gen lại L04 theo rule này; không tự áp dụng lại các batch đã pass.

