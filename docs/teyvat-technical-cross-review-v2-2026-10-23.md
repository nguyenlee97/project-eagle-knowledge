# Review Teyvat V2: vị trí mới có thể giữ 1:1, pipeline cần sửa trước khi ghép M1

Ngày 23/10/2026, Asia/Saigon. Codex kiểm tra độc lập bản yêu cầu mới trong attachment `2577fd6e-007f-446a-9790-95b32e90c5d6/Pasted text.txt`, master plan cập nhật 23:16:28 và atlas cập nhật 23:09:11. Chỉ đọc game và staging; các file tạo mới nằm dưới docs. Không chạy game, installer hoặc builder Mondstadt.

## Kết luận

**Tôi đồng ý với hướng trục mới và xác nhận phép tính đặt anchor `(-6500,-3500,59.5)` nằm trong khung 48×48 km. Hiện chưa cần scale nhỏ để giải quyết chỗ đặt.** Kết luận lần trước rằng anchor cũ vượt biên chỉ áp dụng cho `(-13500,-3500)` sau khi đổi hướng trục; không có nghĩa toàn Teyvat không thể đặt vừa Eagle.

Tuy nhiên, chưa nên coi V2 là đặc tả có thể đưa ngay vào build. Bảng thành phố còn trộn tọa độ raw/manifest/viewer; mẫu IPL vẫn ghi anchor cũ; code staging chưa chuyển hệ trục. Hai lỗi nhị phân trong COL hiện tại vẫn tồn tại. Các khẳng định “không bao giờ hụt collision”, “0,00 mm” và “0% chồng mọi đảo 3D” mạnh hơn bằng chứng hiện có.

| Hạng mục | Kết luận review |
| --- | --- |
| Trục Đông=−Z, Bắc=−X, Up=Y và phép tính anchor mới | Đồng thuận ở mức cơ sở địa lý và envelope danh nghĩa |
| Không chồng map Eagle | Chưa thấy chồng ô có vật thể trong atlas; cần kiểm kê runtime/bounds model ngoài phạm vi atlas |
| Chia ô 256 m | Phù hợp làm mặc định M1; cách diễn giải ba “giới hạn cứng” cần sửa |
| BaseMap + prelight + texture chi tiết | Khả thi về cấu trúc RenderWare; chưa có bake địa lý hoặc nghiệm thu màu SkyGfx trong game |
| Khớp đảo/cầu với M1 | Cần manifest ownership kèm biến dạng đỉnh; chỉ loại trừ face chưa đủ |
| Nước | Có dữ liệu nước ra tới biên tây; phải thiết kế nước hồ thật, không dựa vào alpha mesh để bơi |
| ID/IMG/RAM | Không có dấu hiệu thiếu ID cho quy mô này; cách đóng gói và bộ nhớ resident cần ngân sách riêng |

## 1. Anchor mới, hướng trục và trạng thái bản đồ Eagle

### 1.1. Phép tính mới đúng ở mức envelope

Với OBJ toàn cục đã chuẩn hóa:

```text
X_gta = -Z_obj - 7283
Y_gta = -X_obj - 5775
Z_gta =  Y_obj - 203.5
```

Tâm nguồn `(-2275,263,-783)` trở thành `(-6500,-3500,59.5)`. Envelope lưới danh nghĩa cho kết quả:

```text
X = [-23667 .. -2163], Y = [-12943 .. +4465]
Kích thước = 21504 × 17408 đơn vị, theo tỷ lệ kế hoạch là 21,504 × 17,408 km.
Khoảng cách mép tây tới X=-24000 = 333 m.
```

Tất cả bốn biên đều nằm trong ±24000. Chiều ngang 21,5 km không cần nằm trọn trong một dải chữ nhật hoàn toàn phía tây X=−3000: một phần phía đông của envelope có thể là nước hoặc ô lưới không có nguồn. Vì vậy, phải kiểm giao của các mảnh thật, không kết luận va chạm chỉ vì hai bounding rectangle giao nhau.

![Kiểm tra vị trí Teyvat V2 với snapshot Eagle](teyvat-cross-review-v2-evidence-2026-10-23/placement-overview.png)

Helper riêng đã kiểm 196 rectangle của atlas mới với 1086 ô 500 m có vật thể GTA: **0 cặp giao nhau**. Giới hạn quan trọng: Teyvat chạm 959 ô 500 m nhưng **không ô nào có record tường minh trong tập atlas đã lọc**; phần lớn nằm ngoài vùng khảo sát `X=[-6000,19000],Y=[-12000,16000]`. Do đó đây là kết quả đối chiếu snapshot, không phải chứng nhận rằng mọi vị trí trống đều đã được khảo sát. Model có thể vươn qua ô chứa pivot; dữ liệu script/binary khác có thể chưa nằm trong atlas. [Dữ liệu và hash snapshot](teyvat-cross-review-v2-evidence-2026-10-23/placement-check.json), [helper](teyvat-cross-review-v2-evidence-2026-10-23/placement-check.py).

Kiểm trực tiếp thêm **272 IPL được config hiện tại tham chiếu**: có 84386 dòng `inst`, lấy được interior/XYZ số của 84375 dòng. **0 origin nằm trong hợp 196 rectangle**, dù 1550 origin nằm trong bounding rectangle bao chúng. Điều này hỗ trợ mạnh hơn việc phương án bố trí có chỗ cho 1:1. Nó vẫn chưa kiểm bounds mesh, các dòng không parse được, binary IPL trong IMG hoặc đối tượng sinh bằng script. Không đổi kết quả thành lời bảo đảm “mọi geometry đều không chồng”. [Kết quả origin audit](teyvat-cross-review-v2-evidence-2026-10-23/ipl-origin-overlap-audit.json), [phương pháp và source consistency](teyvat-cross-review-v2-evidence-2026-10-23/coordinate-budget.md).

### 1.2. Tôi có dữ liệu về Eagle, nhưng chưa có kiểm kê bounds hoàn chỉnh

Target hiện tại là gameplay-lab ở C. INI đặt world map 48000, world sector 50 m, LOD sector 200 m. FLA log của lần chạy ngày 22/10 lúc 18:48 UTC ghi nhận áp dụng các kích thước này cho executable được nhận diện là GTA SA 1.0 US HOODLUM; đó là bằng chứng lần chạy đã ghi, không phải thử game mới trong lượt review.

Snapshot atlas có 1533 ô đáng chú ý, trong đó 1086 ô có vật thể, tương đương **271,5 km² ô có placement**, không phải diện tích bề mặt đất được đo chính xác. Các ô đó nằm trong envelope `[-4500,18000] × [-11000,13500]`; gồm San Andreas, Vice City/Leonida, Liberty/Upstate, Carcer, Cottonmouth, Bullworth, Dublin và các vùng đường trường. Báo cáo atlas ghi các cầu/GPS đã được bổ sung; cần phân biệt bằng chứng asset với nghiệm thu gameplay.

Hiện `gta.dat` đã tham chiếu IMG/IDE/IPL `CUSTOM/wibu01_japan_island` (dòng 11/294/380) và các file có trên đĩa: WIBU-01 đã hiện diện trong cấu hình runtime, khác trạng thái “chỉ staging” ở README cũ. Chưa xác nhận load thành công bằng một phiên chơi mới. Ngược lại, chưa thấy directive Mondstadt/Teyvat trong gta.dat đang đọc. Con số 147231 vật thể trong atlas và 84386 dòng text IPL là hai tập đếm khác nhau; không dùng thay thế nhau như tổng occupancy đã kiểm chứng.

Vì cách đếm là “ô có placement”, con số khoảng 85–88% trống chỉ là chỉ báo quy hoạch. Nó không có nghĩa từng mét vuông đã được chứng nhận an toàn, hoặc mọi khoảng trống ghép thành một hình chữ nhật. Ngược lại, quy hoạch V2 hiện đã cho một ví dụ số học vừa trong world mà giữ 1:1.

Ở mép tây chỉ còn 333 m, cần kiểm bounds mesh thực tế sau cắt/skirts, nơi di chuyển của người chơi và camera, collision/streaming tại góc ngoài. Binary32 ở tọa độ lớn cỡ 16–32 km có bước biểu diễn khoảng 1,953 mm; điều này không tự gây lỗi vật lý nghiêm trọng, nhưng loại trừ lời bảo đảm số học “0,00 mm” nếu không đo lại sau lượng tử hóa. Không có bằng chứng thực nghiệm mới rằng camera/physics mất ổn định ở anchor này.

World repeat sectors 16×16 là cấu trúc tra cứu lặp/hash của engine; không được diễn giải thành thế giới chỉ mô phỏng được trong một hình vuông 800 m. Radar/paths/cull vẫn cần dữ liệu phù hợp với vùng Teyvat; tăng map size không tự tạo đường NPC, giao thông hoặc bản đồ radar.

### 1.3. Những điểm tọa độ chưa thống nhất trong V2

- Công thức global dùng gốc raw Mondstadt X=−2275. Nhưng hàng Liyue dùng `world X=1634`, đúng dạng `-manifest.x+1024`, trong khi manifest Liyue là X=−610. Theo chuẩn hóa raw tương đối với Mondstadt, North_rel là −2885; bảng lại ghi −3909, lệch đúng 1024. Inazuma tương tự: −5387 theo anchor nguồn và −6411 trong bảng. Nếu có một phép bù hợp lệ theo mesh, cần ghi rõ và áp dụng nhất quán; không trộn world của viewer với raw của Mondstadt.
- Các điểm Sumeru/BGCWBM khác dữ liệu anchor manifest nhiều hơn một offset 1024; chưa có đủ mesh/nguồn biến đổi để duyệt chúng thành tọa độ triển khai. Cần bằng chứng đặt đúng công trình, không chỉ nhìn bố cục ảnh hợp lý.
- Mục “Zero-Rebuild Relocation” vẫn ghi `-13500 + cx` cho bản tây, trái anchor mới −6500. Đây là lỗi cần sửa trước khi biến tài liệu thành script.
- City Lod0/Lod1 có thể khác khung tọa độ. Ví dụ Mondstadt Lod0 quanh gốc cục bộ, Lod1 đã gần `(-2275,263,-783)`. Chuẩn hóa từng file/LOD trước rồi mới dùng công thức global.

### 1.4. Không đổi riêng parser

`parse_obj_to_gta` hiện vẫn tạo `(ux,uz,uy)`. Đổi riêng nó thành `(-uz,-ux,uy)` sẽ để lại classifier quận, cửa sổ cắt đảo, cầu thủ tục, pivot, prop, tọa độ A* và NPC trong hệ cũ. Cách ít làm xáo trộn nhất là giữ hệ authoring cũ trong thuật toán hiện có, rồi chuyển **mọi đầu ra không gian** cùng một lần tại biên export:

```text
p_new = (-p_old.y, -p_old.x, p_old.z)
```

Chuyển vị trí/normal, đảo winding đúng một lần cho phép phản chiếu từ hệ cũ, tính lại bounds, COL, pivot/IPL, props và các node. Một phương án khác là refactor toàn bộ thuật toán sang hệ mới trong cùng một candidate; không trộn hai cách.

File NPC hiện tại có **5 route, 381 waypoint, 28 spawn** (snapshot 23:04), vẫn chứa tọa độ hệ cũ; Lua sinh từ verifier vẫn đặt origin `(6200,-3200,59.5)`. Các con số 332 waypoint trong tài liệu cũ không phải snapshot hiện tại. Sau migration phải chuyển/regenerate các file này cùng model, không chỉ đổi origin Lua. [Chi tiết code và bằng chứng nhị phân](teyvat-cross-review-v2-evidence-2026-10-23/render-collision.md).

Xoay PNG BaseMap 90° CCW phù hợp mục đích hiển thị bản đồ bắc lên trên với công thức UV đang nêu. Với DFF, giữ ảnh gốc và UV tương ứng cũng có thể đúng sau khi chuyển geometry. Không vừa xoay ảnh vừa giữ/đổi UV theo hai lần chuyển độc lập mà không kiểm tra điểm mốc.

## 2. Chia ô: 256 m phù hợp, nhưng ba lập luận giới hạn cần sửa

**COL size là byte của một entry, không phải số face cố định.** Writer hiện tại dùng khoảng `120 + align4(6V) + 28*ceil(F/48) + 4 + 8F` byte với V đỉnh đã gộp và F face; không thể suy ra mọi COL tối đa khoảng 3200 face. Ngay COL khu cổng hiện có hơn 3200 face vẫn nhỏ hơn 92768 byte. Phải đo entry serialize thật, cùng số đỉnh/index và FaceGroup.

**int16/128 giới hạn từng thành phần local X/Y/Z.** Bán kính cầu 255,99 m không phải giới hạn định dạng. Tile 256 m centered có X/Y khoảng ±128 nên an toàn theo hai trục đó. Nếu chiều cao chênh 350 m và pivot Z ở giữa, thành phần Z khoảng ±175; bán kính góc khoảng 251,78 m, vẫn nhỏ hơn 255,99. Với chênh 400 m, bán kính có thể lớn hơn 255,99 nhưng từng trục vẫn encode được. Cần chia tầng Z khi span thành phần thực sự vượt khoảng 512 m hoặc ngân sách byte/hiệu năng yêu cầu; không chia chỉ vì sphere radius vượt 256.

**DrawDistance 295 và FLA LOD distance 300 không chứng minh collision luôn resident.** Chúng tham gia cơ chế visibility/LOD; collision store và streaming có đường xử lý riêng. Không dùng mệnh đề “295 < 300 nên không bao giờ rơi” làm điều kiện nghiệm thu.

Đo offline bốn OBJ hiện có, cắt chính xác theo biên danh nghĩa và lưới M1, loại mặt đang thuộc đảo: **36 ô vẫn có hình học**, 99–1458 face/ô; entry COL ước theo writer khoảng **1536–20156 byte**; chênh cao tối đa khoảng **193,32 m**, radius tối đa khoảng **197,01 m**. Đây là phép cắt trong bộ nhớ, không phải build gói M1 hoàn thiện; còn gồm phần ngập nước và chưa stitch biến dạng đảo. Phản chiếu hệ trục không đổi các đại lượng độ dài này. Chưa có lý do chia Z thêm cho tập M1 đã đo, nhưng không suy rộng cho Dragonspine/toàn đại lục. [Dữ liệu đo](teyvat-cross-review-v2-evidence-2026-10-23/geometry-audit.json).

## 3. Texture/prelight: hướng kỹ thuật đúng, không bảo đảm tự động giữ màu

RenderWare/GTA SA có cấu trúc prelight và day/night ExtraVertColour phù hợp ý tưởng texture × vertex color. Writer đang có geometry flags gồm PRELIT/TEXTURED/MODULATE, material trắng, day color chuẩn và extension night. Đây là kiểm tra cấu trúc, không phải chứng nhận SkyGfx đã render đúng trong game.

Trên đĩa, `skygfx1.ini` có buildingPipe=PS2, ps2Modulate=0, dualPass=1; override ps2ModulateBuilding đang comment. Tùy chọn riêng SkyGfx không đồng nhất với bit MODULATEMATERIALCOLOR của RenderWare. Chưa kiểm trực tiếp preset/pipeline active trong game.

Những tinh chỉnh cần đưa vào M1:

1. Giữ bbox UV của **OBJ nguồn trước khi cắt**, không tự normalize mỗi subtile hoặc bbox sau bỏ mặt; nếu không, BaseMap bị kéo lệch.
2. Bake địa lý phải thực sự dùng RGB BaseMap. Hàm prelight hiện tại sinh day color từ normal/height/AO; sampled RGB chủ yếu dùng phân loại cửa sổ ban đêm. Nó chưa thực hiện bake địa lý đề xuất.
3. Dùng texture detail có màu nền được chuẩn hóa; cỏ xanh nhân màu cỏ xanh có thể làm tối/bão hòa. Vertex color nội suy theo tam giác cũng không giữ được một lối mòn hẹp nếu không có đủ đỉnh tại ranh màu. Không hứa “giữ 100% mảng màu”.
4. Giữ sắc độ địa lý trong cả day/night; khớp màu trung bình và ánh sáng với LOD, tránh bake BaseMap vào near rồi nhân BaseMap lần nữa ở LOD. Kiểm handoff ở nhiều giờ/timecyc.
5. Cần mipmap/filter và wrap đúng cho UV lặp; writer TXD hiện tại là raw 32-bit, một mip level, không phải bằng chứng DXT1/DXT5 đã có. Với vách dốc, dùng phép chiếu theo mặt/vật liệu phù hợp; UV phẳng ngang dễ kéo texture. Triplanar trong shader không có sẵn chỉ nhờ thêm cờ DFF.

1500 m và 2900 m cũng không phải hai lựa chọn tương đương về tải: diện tích vùng xét theo bán kính tăng khoảng 3,74 lần. Đo resident memory/draw calls trong game trước khi chọn LOD radius cho toàn đại lục.

## 4. Đường nối M1 và hai lỗi hiện có cần sửa trước

### 4.1. Ownership phải chứa cả biến dạng đỉnh

Điều kiện trong `build_island_and_bridge_mesh` không chỉ là hai cửa sổ XY. Một face phải có **mọi đỉnh** nằm trong cửa sổ, Z≥−82, mọi cạnh≤75 m; sau đó còn bị loại theo bản đồ footprint thành và cao độ centroid. Một số đỉnh được hạ về `city_floor_z−0.8`.

Tái lập độc lập trên nguồn hiện tại cho **556 mặt từ 2_-1 và 121 mặt từ 2_-2** được chọn. Có **34 đỉnh nguồn** của 2_-1 bị hạ, tối đa **21,102747 m**, và chúng nằm trên boundary của tập mặt chọn. Vì vậy, phần bù M1 dùng cùng OBJ gốc chưa chỉnh đỉnh có thể hở dù không trùng face.

Cần manifest dùng chung có source hash, phiên bản filter, source face/vertex ID, tọa độ sau biến dạng và boundary loops. M1 phải tái dùng biến dạng ở các đỉnh chung hoặc có vòng chuyển tiếp được thiết kế rõ. Clip tam giác qua lưới thật; không chỉ lọc centroid/all-vertices rồi bỏ cả tam giác cắt biên. Đo đường nối sau cả lượng tử hóa COL và đặt pivot/IPL; mục tiêu là dung sai được đo, không phải chuỗi “0,00 mm” trong báo cáo.

### 4.2. ID 6715: clipping collision đã xảy ra

COL snapshot mới lúc 23:03:38 vẫn có bounds Y khoảng **±299,678 m**, nhưng writer kẹp component về **±255,9921875 m**. Có **105 component Y bị kẹp**, biến dạng ở đầu tới khoảng **43,686 m**. Entry chỉ 16896 byte, nên kiểm “nhỏ hơn 92768” không phát hiện lỗi này. Phải chia/recenter geometry sao cho từng thành phần encode được, và thay clamp thầm lặng bằng lỗi validation. Do tổng span Y gần 600 m, chỉ dời một pivot không thể đưa toàn entry này vào một span khoảng 512 m.

### 4.3. ID 6713: tên collision không khớp

Model là `md_city_barbatos_plaza` (22 ký tự), nhưng COL ghi `md_city_barbatos_plaz` do writer cắt [:21]. Loader tham chiếu còn kiểm key tên khi dùng ID, nên có nguy cơ không gắn đúng collision dù header ID=6713. Cần thống nhất tên ngắn an toàn trên DFF/IDE/IPL/COL và xác nhận binding thật; chưa thử runtime trong review này.

### 4.4. A* offline chưa thay thế kiểm physics

Verifier có đọc COL nhị phân để tạo graph, là một điểm tốt. Tuy nhiên graph dùng lưới 1,5 m, cho barycentric tới −0,06, gộp layer trong 0,85 m và nối neighbor theo chênh cao. Phần đã đọc không thực hiện capsule sweep để kiểm thân người, tường hoặc khoảng không trên đầu. “20/20 landmark reachable” chứng minh kết nối của graph theo tiêu chí đó, không chứng minh Aether đi được mọi chỗ trong GTA hoặc collision của từng ID đã được loader gắn.

## 5. Nước: dùng water system cho khả năng bơi

Water map size được cấu hình 48000; water.dat hiện có hình học vươn tới X/Y=±24000. Vị trí mép tây mới nằm trong lớp nước ngoài, không chỉ trong một ảnh bản đồ biển. INI có water triangles=999, quads=30100, combo-list=9999, vertices=15200.

Phân tích hiện tại cho 2025 record gồm **2019 quad và 6 triangle**, 8094 lượt tham chiếu đỉnh. Đếm mô phỏng theo khóa vertex của source cho khoảng **6425 đỉnh**, dưới giới hạn cấu hình; chưa có số đếm runtime được xác nhận. Combo-list của nước là danh sách theo block/nhóm, nên không lấy 2025 polygon để tuyên bố còn `9999−2025` slot.

Đề xuất:

- Với Cider Lake và hồ cao nguyên có thể bơi/lái thuyền: cần vùng nước native ở cao độ, biên và độ sâu được author đúng. `water.dat` hỗ trợ cao độ khác nhau; không bắt mọi hồ phải về Z=0.
- Z≈1,5 của Cider Lake cần đo từ asset nước/bờ thực tế; không chọn chỉ vì gần mặt biển. Cao độ anchor toàn đại lục phải bảo toàn quan hệ đất/nước đã chọn.
- Mesh Alpha DXT5 chỉ bổ sung hình ảnh, không tự cung cấp query mực nước/buoyancy/swimming. Nó phù hợp lớp trang trí, nước chảy/hiệu ứng hoặc bề mặt cần mỹ thuật bổ sung, với sorting/collision được xử lý phù hợp.
- Khi hồ cao nằm trên ocean Z=0, thiết kế vùng native để truy vấn đúng tầng; tránh thêm hai lớp phủ nhau rồi mặc định engine sẽ luôn chọn mặt mong muốn. Kiểm cả bơi, thuyền, camera dưới nước và chỗ nối bờ.

Không cần sửa water.dat trong lượt này. Bảng nước hiện tại chưa có nghĩa đã có hồ Cider hay Fontaine đúng hình dạng.

## 6. Ngân sách ID, IMG và RAM

Inventory active trước đó đọc từ gta.dat/default.dat ghi 63322 model ID khai báo, không tính 2dfx. Với không gian DFF=200000, có **136678 ID chưa khai báo**; trừ những claim được tìm thấy còn **136431** trong snapshot này. Đây là số candidate, không phải giấy cấp phát vượt các work-item khác. Riêng dưới 65536 có khoảng **17927 ID chưa khai báo**, trước khi trừ reservation.

`196×16×2 = 6272` ID terrain, cộng giả định 291 cụm mỗi cụm near+LOD là 6854: không phải thiếu ID về số lượng. Phân nhóm city thực tế có nhiều phần/biến thể nên đây chỉ là budget sơ bộ. `Object info entries=2048` là bảng object.dat/thuộc tính object, **không phải chỉ còn 2048 model tĩnh có thể đặt**. IDE Objects Type1 và FILE_TYPE_DFF hiện đều 200000.

Không giao thẳng dải >65535 cho writer hiện tại: COL header ID đang được pack bằng `<H`; FLA hỗ trợ ID cao không tự sửa mọi công cụ xuất. Có thể ưu tiên pool dưới 65536 sau kiểm claim, hoặc sửa định dạng/binding/exporter có kiểm chứng trước khi dùng ID cao.

Snapshot cấu hình có 66 directive IMG, 65 archive duy nhất; cần tính thêm loader khác khi đánh giá số slot thật. Nếu tách mỗi 196 block và mỗi 291 cụm thành một archive, tổng tối thiểu `65+196+291=552` sẽ vượt max512. Đóng gói theo sector/region với vài TXD dùng chung và COL có kiểm soát, không mở archive cho từng mảnh nhỏ.

Gộp LOD xa thành 512/1024 m hoặc dùng mesh Lod1 là hướng tốt. Nhưng near 512×512 centered sẽ chạm ±256 m và có thể tràn component COL; Lod1 ít face hơn không sửa được span tọa độ. Có thể giữ collision chia nhỏ và dùng visual LOD lớn. Giữ 16 near, gộp 16 LOD thành4 chỉ giảm tổng ID từ32 xuống20, tức **37,5%**, không phải75%; giảm75% chỉ đúng khi cả hai tầng cùng giảm từ16 xuống4 và mọi ràng buộc khác đều qua.

`Memory available=2800` là cấu hình streaming, không phải phép đo RAM còn trống. FLA ghi tiến trình WIN_X86; model/TXD resident, plugin và tài nguyên đồ họa vẫn chia sẻ ngân sách tiến trình. Giảm scale hình học cũng không tự giảm triangle, ID, archive hoặc dung lượng texture. Muốn tối ưu cần LOD/mesh/material/TXD và bán kính nạp phù hợp, rồi đo trong game.

## Đề nghị chốt bước tiếp theo

Giữ mục tiêu **1:1**, xem anchor mới là candidate hợp lý. Trước khi build M1: thống nhất tọa độ từng nguồn/LOD và sửa bảng/mẫu IPL; sửa hai lỗi COL hiện tại; xuất ownership+deformation dùng chung; chuyển geometry/props/node cùng một phép; sau đó tạo candidate riêng cho M1 với validation sau encode. Chưa cài vào runtime từ kết quả review này.

Nếu sau đo mesh thật vẫn thiếu khoảng đệm, ưu tiên dời anchor hoặc xoay cả đại lục đúng hình học. Scale đồng nhất 90% sẽ cho envelope khoảng19,354×15,667 km, nhưng ảnh hưởng chiều rộng đường, bậc thang và khoảng không so với nhân vật/xe cố định. Hiện chưa có bằng chứng buộc phải nhận đánh đổi đó.

## Bằng chứng và giới hạn

- [Placement snapshot](teyvat-cross-review-v2-evidence-2026-10-23/placement-check.json), [script](teyvat-cross-review-v2-evidence-2026-10-23/placement-check.py).
- [Đo hình học, source hash, COL nhị phân](teyvat-cross-review-v2-evidence-2026-10-23/geometry-audit.json), [helper chỉ ghi evidence](teyvat-cross-review-v2-evidence-2026-10-23/geometry-audit-v2.py), [mask tái lập](teyvat-cross-review-v2-evidence-2026-10-23/ownership-6715-reconstructed.json).
- [Chuyển trục, COL và rendering](teyvat-cross-review-v2-evidence-2026-10-23/render-collision.md), có dẫn nguồn primary về loader/streaming/RenderWare/FLA.
- [Tọa độ, ID và snapshot runtime](teyvat-cross-review-v2-evidence-2026-10-23/coordinate-budget.md); [engine và nước](teyvat-cross-review-v2-evidence-2026-10-23/engine-water.md), có dẫn nguồn primary về repeat-sector hash, loader và water queries.
- Các số liệu trên là snapshot read-only. Chưa đo FPS/resident memory, chưa kiểm nước/physics/radar/NPC trong game và chưa reverse-engineer đầy đủ patch của gta_pe.exe. Không coi việc parse nhị phân đạt là nghiệm thu gameplay.
