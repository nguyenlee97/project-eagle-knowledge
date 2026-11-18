# Khảo sát bộ cài Project Eagle

Phạm vi: kiểm tra read-only thư mục `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`; không chạy game/công cụ. Quy định điều phối hiện được lưu tại `C:\Users\LENOVO\Desktop\GTA\AGENTS.md`.

## Nhận diện build

- Bản Project Eagle trong checkout này là **v1.3**, không phải GTA SA vanilla: `data/Changelog.txt:1-2` ghi “Version 1.3 Changelog”, phát hành June 2026. Các mục changelog xác nhận phạm vi map mở rộng ở `:4-10`, RadioEx ở `:111-113`, và multiplayer tích hợp ở `:206`.
- `PECore.ini` không khai báo số version. `PECore.log:1-4` cho biết core build ngày Jun 15 2026 và log gần nhất nhận dạng executable là GTA SA v1.0 HOODLUM; `fastman92limitAdjuster.log` ghi FLA 7.7 beta, GTA SA 1.0 US HOODLUM (log timestamp 2026-10-13). `modloader/modloader.log:1-3` xác nhận Mod Loader 0.3.7 / game GTA SA 1.0 US. Đây là dấu vết runtime đã lưu sẵn trong thư mục, không phải phép thử do khảo sát này chạy.
- Metadata file version không hiện trên PECore.asi, gta_sa.exe hoặc gta_pe.exe qua Windows VersionInfo. Hai executable có cùng kích thước 14,383,616 bytes và modified time gần nhau (2026-07-01), nên các metadata đó không xác định được biến thể riêng. `ReadMe/Readme.txt` mở đầu bằng V1.00 nhưng nội dung là readme gốc GTA SA, không dùng làm version Eagle (`:9`).
- Trang web đang mở PE1.3.0 là nguồn bên ngoài do điều phối cung cấp; thư mục cục bộ tự xác nhận **Version 1.3**, nhưng không có chuỗi `1.3.0` trong changelog/PECore.ini. Vì vậy kết luận vững nhất cho checkout là Eagle v1.3; không thể xác quyết nhãn patch “.0” từ nguồn cục bộ.

## Loader và mod đã có sẵn

- Core PE chạy qua `PECore.asi`, được nạp cùng nhiều ASI ở root: `SilentPatchSA.asi`, `skygfx.asi`, `GTASA.WidescreenFix.asi`, `ProperRadarSA.asi`, `SanViveLuaHudSA.asi`, fastman92 Limit Adjuster, CLEO, Mod Loader và các plugin khác. Changelog v1.3 mô tả PECore có RadioEx, GPS graph, radar, HUD, save sideloader, tính năng gameplay/UI; `PECore.ini:8-43` cho thấy đa số feature bật mặc định, RadioEx sprites bật ở `:44-46`, distant traffic tắt ở `:28`/`[DistantTraffic] Enabled=false`.
- CLEO có `cleo.log` ghi CLEO v5.0.3 và `cleo/` chứa script/plugin, gồm RZL Trainer, MapTeleporter, static car shadow, tank tracks, rich presence, v.v. Mod Loader 0.3.7 đang dùng profile Default; `modloader/modloader.ini:4-9,20-27` đặt IgnoreAllMods/ExcludeAllMods false. Log `:47-50` cho thấy quét mod `New Official Loading Themes`; cây thư mục còn có `RZL-Skin`. Đây là nội dung đã nằm trong distribution hiện tại, không phải trạng thái vanilla. Chưa có bằng chứng đủ để xác định thư mục nào do người dùng tự thêm sau khi giải nén.
- `custom/` có `custom_mods.ide`, `.ipl`, `.img`. `data/default.dat:5-6` mount `CUSTOM\\CUSTOM_MODS.IMG` và `modloader\\modloader.img`; file config này còn khai báo core item definitions (`:11+`).

## Cách nạp dữ liệu và ý nghĩa cho modding

- `data/gta.dat:4-10` mount archive path/carrec/script/cutscene/animation và `CUSTOM\\CUSTOM_MODS.img`; từ `:12` trở đi nạp IMG theo vùng San Andreas và hàng loạt bản đồ Stars & Stripes, Vice City, Liberty City, v.v. File có các entry bổ sung tới Cottonmouth/Dublin/Leonida/Jackalope/Wichska/Prairie (`gta.dat` phần sau). Changelog v1.3 cũng ghi các vùng mới như South Cordillera, Argal, Peachtree, Leonida, Carcer City và Upstate Liberty (`data/Changelog.txt:5-10`).
- `IMG BUILDER CONFIG.ini` là manifest build/archive creator: metadata ghi 61 folder; các entry nguồn cho thấy nhiều IMG chứa hàng nghìn file, trong đó cả archive bản đồ, vehicle, radar, interiors. Đây là bằng chứng cấu trúc distribution được đóng gói từ nhiều archive, không chỉ modloader overlay.
- So với GTA SA vanilla, Eagle đã thay đổi nội dung game và data manifest ở quy mô conversion/total conversion, đồng thời có loader nhiều tầng (ASI/PECore, CLEO, Mod Loader, FLA) để mở rộng. Mod xe/skin thường có thể đưa dạng thay thế file qua thư mục modloader; còn thay archive/IDE/IPL, map, số ID hay script cần kiểm tra tương thích với manifest/map và limit patch của Eagle. Không nên áp dụng mod hướng vanilla một cách mù quáng, nhất là khi nó sửa cùng data/IMG/script. Chưa thử nạp mod nào.
- Với mục tiêu anime + lái xe nghe nhạc: Eagle cung cấp khả năng mod và hệ thống radio mở rộng, nhưng changelog/PECore chỉ chứng minh framework RadioEx; không chứng minh distribution này đã cài nhạc anime. `PECore.ini` cho phép custom stations/dynamic music theo chú thích (`:24-26`), còn định dạng cụ thể và vị trí cấu hình RadioEx chưa được lập bản đồ đầy đủ trong lượt khảo sát này.

## Giới hạn

Chỉ đọc file text, danh sách thư mục và metadata file; không mở archive nhị phân để kiểm kê từng tài sản, không xác minh hash/chữ ký, không chạy launcher/game, không xác định nguồn gốc từng file mod trong thư mục. “gta sa clean” là tên thư mục, không phải bằng chứng vanilla hay clean-room distribution.
