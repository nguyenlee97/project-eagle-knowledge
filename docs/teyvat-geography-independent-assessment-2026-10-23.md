# Teyvat: nhận định độc lập về địa lý, hướng trục và phạm vi dữ liệu

Ngày: 23/10/2026, Asia/Saigon. Người thực hiện: Codex. Đây là nhận định riêng phục vụ review với Antigravity; không sửa master plan, atlas, game hoặc staging Mondstadt. Review kỹ thuật sáu mục trước đó vẫn tạm ngưng.

## Kết luận cần đưa vào lần review tới

**Tôi chưa đồng ý dùng bảng tọa độ và anchor cũ làm cơ sở triển khai toàn đại lục. Vấn đề đầu tiên là hướng trục và cách chuẩn hóa nguồn.** Đối chiếu bốn thành phố dễ nhận diện cho thấy bảng cũ sai quan hệ địa lý; tam giác Mondstadt–Liyue–Fontaine còn có thứ tự ngược chiều so với ảnh. Chỉ dời anchor hoặc xoay toàn đại lục không giải quyết được dấu hiệu phản chiếu này.

Cơ sở địa lý ứng viên phù hợp ảnh hơn là **Đông = −Y cũ, Bắc = −X cũ**. Đây là kết quả kiểm tra thô ở mức thành phố, chưa phải công thức xuất mọi OBJ. Sau khi xác nhận cơ sở này, cần tính lại footprint và chọn vị trí đặt GTA. Đồng thời, **196 block và 291 nhóm `city_hlod` chưa chứng minh có đủ toàn bộ Teyvat trong ảnh hoặc có đủ tài nguyên để tái tạo hoàn chỉnh 1:1**.

![So sánh cơ sở trục cũ và cơ sở phù hợp ảnh](teyvat-geography-evidence-2026-10-23/orientation-comparison.png)

## 1. Bố cục địa lý tôi đọc được từ ảnh

Ảnh người dùng cung cấp nằm ở `C:\Users\LENOVO\Downloads\image.png`, kích thước 10.593 × 9.079 px, SHA-256 `bfc08e11b508601dd0c3ac3755ee0833fda4c6c7362b334fadf8685991689e5b`. Ảnh có watermark cộng đồng, không có lưới tọa độ, thước đo hoặc số phiên bản được xác nhận trong lượt này. Vì vậy, tôi dùng nó để kiểm tra hình dạng và vị trí tương đối; không suy ra tọa độ mét chỉ từ pixel.

Đọc theo hướng bắc ở trên, được hỗ trợ bởi mô tả vùng chính thức:

| Vùng | Quan hệ địa lý cần giữ | Ý nghĩa khi dựng lại |
| --- | --- | --- |
| Mondstadt | Phía đông bắc cụm vùng quen thuộc; đảo thành nằm trong hồ | Thành, hồ, bờ và cầu phải đúng hướng với nhau; một thành đẹp riêng lẻ chưa xác nhận ngoại ô đúng |
| Liyue Harbor | Tây nam Mondstadt, ở ven biển phía đông của Liyue | Bảng tọa độ đặt cảng đông bắc Mondstadt cần sửa |
| Sumeru | Về phía tây của Liyue; rừng ở đông, sa mạc ở tây trong ảnh | Giữ trình tự rừng → sa mạc → vùng phía Natlan; không gắn tên từ mã file chưa được nhận diện |
| Fontaine | Tây bắc Mondstadt/Liyue, phía bắc Sumeru | Độ lệch chủ yếu về tây so với Mondstadt là phép kiểm tra hướng trục hữu ích |
| Natlan | Phía tây/tây nam Sumeru trong ảnh | Cần nối đúng đầu phía sa mạc; xác nhận từng công trình trước khi gắn nhãn “Stadium” |
| Inazuma | Quần đảo tách biệt về đông nam cụm đất liền | Giữ khoảng biển và bố trí đảo; không ghép thành phần đất liền liên tục |
| Cụm đảo phía tây bắc và vùng tuyết trên cùng | Ảnh thể hiện một nhánh kéo dài lên phía bắc | Cần đối chiếu tên vùng và phiên bản nguồn trước khi gọi toàn bộ nhánh này là Nod-Krai hoặc toàn Snezhnaya |

HoYoverse mô tả Natlan nằm phía tây sa mạc Sumeru, phù hợp thứ tự quan sát trên ảnh. Đây là một kiểm tra bằng nguồn chính thức; không xác nhận mọi đường viền hoặc kết nối trong ảnh cộng đồng. [Thông báo Natlan của HoYoverse](https://www.hoyoverse.com/en-us/news/125574?mdrv=www.hoyoverse.com), [trang giới thiệu các vùng](https://genshin.hoyoverse.com/en/map).

**Các nét đứt trắng trên biển không được dùng làm đường giao thông.** Chưa có chú giải để xác nhận ý nghĩa của chúng. Tương tự, đường cyan bao cả một số vùng biển không thể mặc định là đường bờ vật lý; nền tối không chứng minh nơi đó là biển sâu. Giới hạn khám phá, phần chưa lập bản đồ, lớp hiển thị và đất/nước thực tế phải được kiểm riêng. Ảnh 2D cũng không xác định được hang ngầm, nội thất hay quan hệ cao độ giữa hồ, biển và cao nguyên.

MapGenie không được kiểm chứng trực tiếp: công cụ web không mở được trang, và trình duyệt từ chối truy cập theo chính sách an toàn. Tôi không tìm cách vượt chặn. Nhận định này dựa vào ảnh đã được người dùng cung cấp, snapshot HoyoMap trên đĩa và các nguồn độc lập của HoYoverse.

## 2. Bảng cũ có dấu hiệu phản chiếu, không chỉ đặt sai vị trí

Tôi chọn Mondstadt, Liyue Harbor, Court of Fontaine và Inazuma/Tenshukaku vì có công trình dễ nhận ra trên ảnh và manifest tương ứng. Vị trí tâm trên ảnh được chọn xấp xỉ bằng mắt; không dùng những tên file chưa chắc chắn như HJCHS làm điểm hiệu chuẩn.

Từ các anchor manifest, bảng cũ cho vị trí tương đối sau:

| Địa danh | `(X, Y)` tương đối trong kế hoạch cũ | Quan hệ nhìn trên ảnh | Cơ sở ứng viên `(Đông, Bắc) = (−Y, −X)` |
| --- | ---: | --- | ---: |
| Mondstadt | `(0, 0)` | Gốc so sánh | `(0, 0)` |
| Liyue Harbor | `(+2885, +1073)` | Tây nam | `(−1073, −2885)` |
| Court of Fontaine | `(−1125, +5502)` | Chủ yếu về tây, hơi lên bắc | `(−5502, +1125)` |
| Inazuma | `(+5387, −3641)` | Đông nam, lệch nam khá lớn | `(+3641, −5387)` |

Helper thử tám cách hoán vị/đổi dấu hai trục, mỗi cách chỉ được fit một tỷ lệ pixel đồng nhất dương và một phép tịnh tiến. Cơ sở `(-Y, -X)` cho sai lệch RMS khoảng **9,87 px**, so với **191,01 px** của cơ sở cũ, khi quy ảnh về bề rộng tham chiếu 1.717 px. Sai lệch từng điểm của cơ sở ứng viên khoảng 5–15 px. Các con số chỉ đánh giá hướng trục ở mức thành phố; tâm mesh và điểm ảnh chọn có thể khác nhau. Chúng không chứng minh sai số centimet, tỷ lệ vật lý tuyệt đối hoặc tính đúng của mọi vùng.

Kiểm tra quan trọng hơn không cần fit: tích có hướng của hai vectơ Mondstadt→Liyue và Mondstadt→Fontaine là `+17.080.395` trong bảng cũ, nhưng âm trong hệ Đông/Bắc của ảnh (`−111.558` theo pixel tham chiếu). Thứ tự ba điểm bị đảo chiều. Phép xoay và tịnh tiến toàn bản đồ giữ dấu này; vì vậy **không thể giải thích sự khác biệt chỉ bằng việc cố ý xoay Teyvat để vừa chỗ trống GTA**.

Kết quả và điểm chọn nằm trong [JSON kiểm tra cơ sở trục](teyvat-geography-evidence-2026-10-23/map-basis-audit.json); có thể chạy lại bằng [helper](teyvat-geography-evidence-2026-10-23/map-basis-audit.py).

## 3. Cơ sở tọa độ ứng viên và giới hạn áp dụng

Với **tọa độ OBJ toàn cục đã được chuẩn hóa đúng**, lấy tâm Mondstadt `(-2275, 263, -783)`, ứng viên phù hợp bố cục ảnh là:

```text
East_rel  = -(Z_obj + 783)
North_rel = -(X_obj + 2275)
Up_rel    =  Y_obj - 263
```

Với **anchor manifest** có tâm Mondstadt `(+2275, 263, -783)`, phép so sánh ở mức điểm anchor tương ứng là:

```text
East_rel  = -(manifest.z + 783)
North_rel =   manifest.x - 2275
```

Không thay trực tiếp hai loại đầu vào cho nhau. Quan sát file thật cho thấy Mondstadt Lod0 có X khoảng `[-137,7 .. 135,8]`, Z khoảng `[-187,1 .. 187,3]`, tức mesh quanh gốc cục bộ; Lod1/Lod2 lại có X khoảng `[-2412,7 .. -2139,2]`, Z khoảng `[-970,1 .. -595,7]`, tức đã ở một khung tọa độ khác. Đưa cùng một offset vào tất cả sẽ làm lệch cả nghìn đơn vị.

HoyoMap còn dùng các đường đặt khác nhau: city lấy vị trí manifest, block HLOD được đặt theo lưới và tâm bounding box; `overrides.json` chứa 13 điều chỉnh vị trí. Mã nguồn công khai thể hiện các cơ chế này, nhưng không chứng minh mỗi file raw của snapshot có cùng quy ước. [HoyoMap: đặt block](https://github.com/flatypus/hoyomap/blob/main/public/index.html#L430-L438), [đặt city](https://github.com/flatypus/hoyomap/blob/main/public/index.html#L465-L500), [overrides](https://github.com/flatypus/hoyomap/blob/main/overrides.json).

Tôi đề nghị mỗi mesh/LOD có hồ sơ ghi rõ: tọa độ cục bộ hay toàn cục; phép đưa vào hệ nguồn chuẩn; anchor/pivot; override có áp dụng hay không; bounds sau chuyển; và đối chiếu đúng công trình. Sau đó mới áp dụng một phép đặt cả đại lục vào GTA. Khi thay cơ sở trục, phải đánh giá lại normals, thứ tự mặt và tọa độ collision. Một quaternion xoay IPL thông thường không thực hiện được phép phản chiếu, nên lời hứa “chỉ đổi IPL, không cần build lại” không đủ để sửa lỗi hướng nếu mesh đã được xuất theo cơ sở sai.

## 4. Anchor phía tây phải tính lại sau khi chốt hướng

Đây là phép tính **có điều kiện**, dùng envelope danh nghĩa trong atlas cũ, chưa thay bằng đường bờ hay bounds mesh toàn bộ đã khảo sát:

```text
Khung tương đối cũ:
X = [-7965 .. +9443], Y = [-4337 .. +17167]

Sau cơ sở ứng viên, nếu Bắc Teyvat trùng Bắc GTA:
East = [-17167 .. +4337], North = [-9443 .. +7965]
```

Chiều ngang lúc này là **21.504**, chiều dọc **17.408** đơn vị nguồn. Nếu vẫn đặt Mondstadt ở `(-13500, -3500)`, envelope sẽ thành:

```text
X_gta = [-30667 .. -9163]
Y_gta = [-12943 .. +4465]
```

Tức vượt biên X=−24.000 khoảng **6.667 đơn vị**. Do đó không thể giữ đồng thời hướng bắc này, tỷ lệ hiện tại và anchor cũ mà vẫn dùng chính envelope đó.

Một khả năng khác là xoay **toàn bộ đại lục đã chuẩn hóa đúng** 90° có chủ ý. Ví dụ xoay 90° ngược chiều kim đồng hồ trong mặt phẳng Đông/Bắc, rồi dùng anchor cũ, cho envelope danh nghĩa `X=[-21465..-4057]`, `Y=[-20667..837]`, nằm trong biên ±24.000. Đây chỉ là kiểm tra envelope; chưa xét vật thể GTA, nước, hệ thống đường/radar hoặc trải nghiệm trong game. Nếu chọn hướng xoay này, atlas và chú giải hướng bắc Teyvat phải thể hiện rõ.

Không chốt một anchor mới trong lượt này. Thứ tự hợp lý là **xác nhận địa lý → chuẩn hóa mesh → chọn hướng đặt → đo footprint → kiểm va chạm với Eagle → chốt anchor**. Nếu muốn giữ bắc Teyvat trùng bắc GTA, riêng hành lang giả định `X=[-24000..-3000]` chỉ rộng 21.000, nhỏ hơn envelope ngang 21.504; điều này loại trừ một lời bảo đảm đơn giản “toàn bộ nằm phía tây X=−3000”, chứ chưa chứng minh không có vị trí phù hợp theo đường bờ thực tế.

## 5. “196 block” chưa đồng nghĩa với “toàn Teyvat 1:1”

Kiểm manifest trên đĩa cho thấy:

- `android_manifest.hlod`: **196 khóa**, nằm trong envelope **17 × 21 = 357** vị trí lưới; **161 vị trí không có khóa**. Chưa biết từng chỗ trống là nước, khu chưa cần mesh, cảnh khác hay thiếu dữ liệu. Không tô tất cả thành đất hoặc biển từ số đếm này.
- Chỉ **193/196** block có Lod0; ba khóa `-2_10`, `0_10`, `0_13` cần lựa chọn LOD/biến thể phù hợp.
- `all_hlod_manifest`: **291 city_hlod**, cùng **18 area**, **10 ares**, **8 cavern**, **2 home**, **35 tunnel**, tổng **364 nhóm**. Một nhóm không nhất thiết là một thành phố hoặc một công trình độc lập.
- Trong 291 nhóm city, **97 anchor là (0,0,0)** và **34 nhóm không có Lod0**. Có các phần Building/Leaf/Stone và biến thể Festival cùng anchor; không thể đặt tất cả thành một lượt mà không chọn cảnh/LOD.
- HoyoMap dùng regex để chọn màu vùng, không phải bảng định danh địa lý. `HJC` và `BGC` nằm chung một nhóm màu; điều đó không đủ xác nhận HJCHS là “Đấu trường Lửa Thánh”, hoặc phân biệt chính xác Natlan và Nod-Krai. Mã `XKC02` không nằm trong regex Sumeru cũng không chứng minh nó thuộc vùng khác. Cần nhận diện mesh/texture và đối chiếu địa danh.

Đặc biệt, chưa xác định snapshot HoyoMap khớp phiên bản nào của ảnh người dùng. Một vùng có tên trong manifest chưa chứng minh có đủ mesh, đúng texture, đúng vị trí và đường đi. Tỷ lệ hình học 1:1 cũng khác với mức đầy đủ kiến trúc/cây cối/nước/địa hình gần của game gốc. README của tác giả HoyoMap nêu giới hạn trong việc tìm texture ngoài Mondstadt và các mặt đất; cần tính điều này khi mô tả độ hoàn chỉnh của nguồn. [HoyoMap README](https://github.com/flatypus/hoyomap#readme).

Chi tiết và dữ liệu có thể chạy lại: [kiểm manifest và các khung tọa độ](teyvat-geography-evidence-2026-10-23/coordinate-manifest-review.md).

## 6. Điều tôi muốn thấy trong bản thiết kế kế tiếp

1. **Một bản đồ đối chiếu có các mốc xác nhận.** Tối thiểu Mondstadt, Liyue Harbor, Fontaine, Inazuma và vài điểm ở Sumeru/Natlan/Nod-Krai. Ghi nguồn xác định tên, điểm nguồn và vị trí trên bản đồ tham chiếu. Để riêng các tên còn nghi ngờ.
2. **Bảng chuyển tọa độ theo loại nguồn và LOD.** Kiểm ít nhất một city local, một city/global LOD, một block terrain và một asset cần override; xuất bounds để chúng ghép đúng trước khi bàn về GTA anchor.
3. **Footprint theo hình học thật và mức độ phủ dữ liệu.** Có lớp hiện diện/thiếu/chưa xác định; phân biệt đất, nước và vùng chưa có dữ liệu. Envelope chữ nhật chỉ hỗ trợ bố trí sơ bộ.
4. **Một lựa chọn hướng đặt rõ ràng.** Có thể giữ bắc Teyvat hoặc xoay cả đại lục để vừa Eagle; phép xoay phải giữ đúng quan hệ các vùng. Sau đó tính lại anchor, nước và atlas.
5. **M1 được đặt tên và chia phạm vi từ các địa danh đã định vị.** Chưa mặc định một vuông 1.536 × 1.536 quanh thành chắc chắn chứa đủ Springvale và Whispering Woods. Trước hết xác nhận cầu ra thành, bờ hồ, đường tới từng làng/rừng; rồi mới chốt ranh giới sector.
6. **Phần đường xe/cầu bổ sung được vẽ như một lớp thiết kế riêng.** Bản gốc có nhiều địa hình đi bộ, núi và quần đảo. Nhu cầu lái xe của Project Eagle không biến nét đứt trong ảnh thành đường xe có sẵn, và không đòi hỏi tự lấp biển/nối mọi đảo khi đang kiểm tính đúng địa lý.

## Bằng chứng, trạng thái và bàn giao

- Phân tích ảnh, manifest, số học và hình học điểm anchor đều thực hiện offline; không chạy game, không build lại mesh, không sửa archive hay staging.
- [Bằng chứng địa lý và nguồn chính thức](teyvat-geography-evidence-2026-10-23/geographic-layout.md).
- [Dữ liệu fit hướng trục và hash nguồn](teyvat-geography-evidence-2026-10-23/map-basis-audit.json), [script](teyvat-geography-evidence-2026-10-23/map-basis-audit.py).
- [Dữ liệu manifest](teyvat-geography-evidence-2026-10-23/coordinate-manifest-review.json), [script](teyvat-geography-evidence-2026-10-23/coordinate-manifest-review.py).
- Nhận định đủ để yêu cầu sửa/giải thích lại cơ sở bản thiết kế; chưa đủ để phê duyệt một phép chuyển tất cả tài nguyên hoặc vị trí cài mới. Không khẳng định Antigravity đã đọc báo cáo này.
