# Khảo sát skin CJ và NPC trong Project Eagle

Ngày khảo sát: 13-10-2026. Phạm vi chỉ đọc; không mở game, sửa game, tải skin hay thử cài đặt. GTA Underground đã bị loại khỏi mục tiêu. Mục tiêu đã chốt: chơi Aether (Genshin Impact) làm nhân vật chính; danh sách NPC sẽ được cung cấp sau.

## Kết luận từ bản cài

Bản game tại `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean` là Project Eagle 1.3: `data\Changelog.txt` mở đầu bằng “Version 1.3 Changelog” (dòng 1–2), còn `PECore.log` ghi Core build Jun 15 2026. [Changelog PE 1.3](https://www.projecteaglemod.games/changelog/pe-1.3.0) nói ModLoader được hỗ trợ lại và `componentpeds.img` được giải mã. Cấu hình `modloader\modloader.ini` đang chọn profile Default với `IgnoreAllMods=false` và `ExcludeAllMods=false` (dòng 4–9), vì vậy không thấy thiết lập tắt toàn bộ ModLoader.

`modloader\RZL-Skin` hiện không chứa skin nào, chỉ có `.File Name Rules.txt`. File rules ghi tên tối đa 7 ký tự, không dùng dấu chấm trong phần tên, và tránh `~` vì có thể làm game crash khi mở danh sách; xem chính file để biết danh sách ký tự cho phép. Đây là quy tắc cục bộ của thư mục RZL-Skin.

Tài liệu listing của [RZL-Trainer v5.0.0](https://www.gtainside.com/sanandreas/mods/207738-rzl-trainer-v5-0-0-cheat-menu) liệt kê các mục `Change Player > Modloader Skin`, `Change Player > Add-On Peds`, và `Change Player > Skin.IMG`. Tuy nhiên, config local chỉ ghi `[Version 5.CBT1.3]` tại `cleo\RZL-Trainer.ini:288-289`; chưa xác minh build trainer thực tế có đúng các menu/chức năng của listing v5.0.0 hay không. Vì vậy, Modloader Skin là workflow ứng viên cần kiểm tra trên trainer local khi triển khai, chưa thể khẳng định menu này hoạt động ở bản hiện tại.

### Aether làm nhân vật chính

Workflow ứng viên là cài gói Aether đã được xác nhận dành cho PC GTA SA vào `modloader\RZL-Skin`, tuân thủ quy tắc tên, rồi chọn ở `Change Player > Modloader Skin` nếu menu đó hiện diện trong trainer local. Listing v5.0.0 mô tả menu này, còn thư mục RZL-Skin và file rules có sẵn trong game; nhưng trainer config local mang nhãn 5.CBT1.3 và gói Aether chưa được kiểm tra. Do đó cần xác nhận cả hai trước khi chọn cách này.

`models\player.img` hiện tồn tại (66,738,176 byte). `cleo\RZL-Trainer\Portable Clothes.ini` có slot 2 và giá trị model/texture cho body parts (dòng 1–12 trở đi), cho thấy có dữ liệu portable clothes cục bộ. Thay quần áo trong `player.img`/portable clothes là một nhánh tùy chỉnh từng bộ phận; nó không chứng minh có thể thay toàn thân thành Aether. Nếu mục tiêu là Aether playable toàn thân, ưu tiên kiểm tra custom skin selector trước. Listing v5.0.0 còn nêu `Skin.IMG`, nhưng cũng chưa xác nhận tính năng đó ở trainer local.

Trang [Aether from Genshin Impact cho GTA San Andreas](https://www.gtainside.com/en/sanandreas/skins/156646-aether-from-genshin-impact/) ghi update 3.0 tháng 3-2023, kích thước 2.094 MB, model ghi công HoYoverse và rig/convert/port ghi công FadXploit. Trang không nêu manifest, phần mở rộng file hoặc cách dùng với RZL/Project Eagle. Đây là ứng viên để kiểm tra thủ công về sau, nhưng không tải archive trong khảo sát này và không kết luận tương thích.

## Workflow NPC sau khi có danh sách

Đổi ngoại hình NPC ambient thành anime có thể thực hiện bằng cách thay DFF/TXD của model ped hiện đang spawn, giữ đúng tên model mà game tham chiếu. Không cần thay đổi `pedgrp` chỉ để thay appearance cho cùng các model đang spawn. Chỉ cân nhắc `pedgrp`/`popcycle` khi người dùng muốn đổi loại ped nào xuất hiện, tần suất hoặc địa bàn xuất hiện.

Bản cài có `data\peds.ide` với 1,687 dòng và model ID đến 49,422 theo `unused_ids_and_description_of_IDEs.txt`; có `S&S\Cdimages\default\COMPONENTPEDS.img` (~444 MB), cùng các file `data\pedgrp*.dat` theo vùng. PE 1.3 changelog nói các khu vực dùng pedestrian group riêng. Khi nhận danh sách NPC, cần tra từng tên/model đến file DFF/TXD thực tế và đúng vị trí ModLoader/archive mà PE dùng; không nên sửa trực tiếp archive lớn trước khi xác định model và đường nạp. Nếu thay model đang dùng cho ped đặc biệt/nhiệm vụ thì diện mạo của ped đó cũng có thể đổi, nên cần đưa vào phạm vi thử nghiệm.

Các tài liệu đã xem chưa xác nhận model skin được lưu bền qua save/load, giữ qua restart, dùng ổn trong cutscene/nhiệm vụ, hoặc có rig/animation/tóc/vạt áo/alpha đúng. Đây là các điểm cần thử sau khi chốt asset và workflow. Multiplayer cũng chưa được khảo sát.

## Bằng chứng tại bản cài (local)

Các đường dẫn tương đối dưới đây lấy `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean` làm thư mục gốc.

- `data\Changelog.txt:1-2` — bản cài ghi Version 1.3; `PECore.log` ghi `Starting Project Eagle Core (Jun 15 2026)`.
- `modloader\modloader.ini:4-9` — profile Default và hai cờ ModLoader.
- `modloader\RZL-Skin\.File Name Rules.txt:1-12` — quy tắc đặt tên trong thư mục skin.
- `cleo\RZL-Trainer.ini:288-289` — nhãn version `5.CBT1.3`; không xác minh được chức năng tương ứng với listing v5.0.0.
- `cleo\RZL-Trainer\Portable Clothes.ini:1-12` — slot portable clothes và giá trị model/texture body part.
- `models\player.img` — archive hiện diện, 66,738,176 byte.
- `data\peds.ide:38-44,1343-1349,1757-1766` — schema, player ID 0 và ped IDs mở rộng.
- `unused_ids_and_description_of_IDEs.txt:1-19` — thống kê ID/range của `peds.ide` và các IDE liên quan.
- `S&S\Cdimages\default\COMPONENTPEDS.img` — archive hiện diện, 444,082,176 byte.
- `data\pedgrp*.dat` — các nhóm ped theo vùng hiện diện.
- `modloader\.data\Readme.md` — nguyên tắc ModLoader đặt nội dung mod trong thư mục con riêng; tài liệu này không mô tả cấu trúc archive dành riêng cho Project Eagle.

## Nguồn trực tuyến

- [Project Eagle PE 1.3 changelog](https://www.projecteaglemod.games/changelog/pe-1.3.0) — ModLoader compatibility được thêm lại; `componentpeds.img` được giải mã.
- [Project Eagle changelog 1.4.7](https://www.projecteaglemod.games/changelog/1.4.7) — bản cũ ghi ModLoader bị bỏ; thông tin đó không áp dụng cho bản cài PE 1.3.
- [RZL-Trainer v5.0.0 listing](https://www.gtainside.com/sanandreas/mods/207738-rzl-trainer-v5-0-0-cheat-menu) — mô tả các menu Modloader Skin, Add-On Peds và Skin.IMG; chưa xác nhận trainer local 5.CBT1.3 có cùng chức năng.
- [Aether from Genshin Impact cho GTA SA](https://www.gtainside.com/en/sanandreas/skins/156646-aether-from-genshin-impact/) — listing có thông tin update/credit, không có manifest file.

Discord Eagle: inventory browser trong phiên khảo sát không có tab Discord đang mở (Chrome chỉ liệt kê Google Search, Zalo, Facebook; Codex IAB không có tab), nên không đọc được bài/channel cộng đồng.
