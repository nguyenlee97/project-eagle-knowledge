# Radio custom trên Project Eagle

Ngày khảo sát: 13/10/2026  
Phạm vi: chỉ đọc bộ cài `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`; không chạy game, phát âm thanh, sửa file game hay cài/tải mod.

## Kết luận

Eagle có hai khái niệm khác nhau:

- **User Tracks** là một playlist người dùng trên station gốc của GTA SA. Rockstar mô tả nó như MP3 player và cho chọn Radio / Random / Sequential; đây không phải nhiều kênh mang tên riêng.
- **RadioEx của Eagle** có cấu hình region và các station có tên riêng trong `data\radio.dat`. Đây là hướng phù hợp nếu muốn vài kênh anime/game khác nhau để đổi khi lái xe. Cấu hình khai báo một file audio cho mỗi station, nên playlist nhiều bài nên được dựng thành một file dài/loop hoặc cần xác nhận khả năng playlist nhiều file trước khi triển khai.

Cấu hình cục bộ bật RadioEx. Tuy nhiên, phần lớn đường dẫn OGG mà `radio.dat` nêu không hiện diện tại vị trí đã khai báo trong thư mục game được khảo sát; `audio\PE` cũng không có. Vì vậy, có thể xác nhận feature/config tồn tại, nhưng chưa thể xác nhận các station hoạt động trong runtime hay rằng bản cài có đủ audio assets. Không nên sửa `radio.dat` hoặc thay audio trước khi xác định asset layout/khả năng đọc cấu hình thực tế.

## Bằng chứng trong bản Eagle được chọn

| Quan sát | Nguồn cục bộ | Ý nghĩa và giới hạn |
|---|---|---|
| PECore bật RadioEx; chú thích gọi rõ custom stations/dynamic music và cấu hình sprite. Có hai dòng `RadioEx = true` trong `[FEATURES]`. | `PECore.ini:24-26,44-46` | Cấu hình hiện tại bật hệ thống; INI không chứng minh runtime hoạt động. |
| PECore log phát hiện GTA SA v1.0 HOODLUM và liệt kê `RadioEx` trong feature đã bật. | `PECore.log:4,32` | Bằng chứng khởi tạo feature theo log đã có trong thư mục; không phải thử nghe/chuyển station trong game. |
| `data\radio.dat` tự mô tả format region: `Region`, `RegionName`, `TxdName`, mỗi `Station=Name,AudioFile,SpriteName,Duration`; audio path tương đối game, duration 0 tự dò. | `data\radio.dat:4-15` | Đây là cấu trúc config thực tế có sẵn, không phải đoán từ Underground. |
| Config có 7 section vùng và 63 dòng Station; các section tiêu biểu là `[LibertyCity]`, `[ViceCity]`, `[Cheyenne]`, `[Praire]`, `[Cordillera]`, `[Anneland]`, `[Neijas]`. | `data\radio.dat:20-...` (file 154 dòng) | Bản cài đã cấu hình nhiều kênh mang tên riêng theo vùng. Những vùng này là vùng của Eagle; việc gắn station vào một vùng để dùng khi đi dạo ở đâu cần cân nhắc trải nghiệm/region map. |
| File audio được khai báo ví dụ `AUDIO\PE\RADIO\REGION8\HEAD.OGG`; không có thư mục `audio\PE` và không thấy OGG trong cây game ở đường dẫn đã khảo sát. | `data\radio.dat:24` và listing `audio\` | Config có tham chiếu nhưng file không thấy ở đường dẫn chuẩn. Có thể asset nằm ngoài layout đã kiểm tra/đóng gói nơi khác; chưa kết luận thiếu toàn bộ audio. |
| Thư mục User Tracks của PE tồn tại và rỗng tại thời điểm khảo sát. | `C:\Users\LENOVO\Documents\GTA PE User Files\User Tracks` | Đây là path User Files quan sát được của Eagle trên máy này; không suy từ Underground. Chưa có playlist người dùng. |
| Changelog Eagle ghi RadioEx có thể thêm station cho map region và hỗ trợ sprite/text display. | `data\Changelog.txt:111-112` | Tài liệu release đi kèm bản cài mô tả khả năng, vẫn chưa phải runtime verification. |
| Chỉ có `scripts\global.ini` trong thư mục scripts và không thấy file CLEO có tên radio/audio/station. | `scripts\global.ini`; inventory `scripts\` | Không có script CLEO radio rõ tên trong cây đó. RadioEx được khai báo như PECore feature; không cần kết luận từ CLEO. |

## Nguồn tài liệu bên ngoài

- [Project Eagle: The Evolution of Project Eagle’s Radio System](https://www.projecteaglemod.games/news/6), đăng 10/01/2026, nhất là phần RadioEx (lines 81-122): mô tả hệ song song theo vùng, config `radio.dat`, mỗi station khai báo audio/sprite và khả năng cấu hình nhiều station/vùng. Bài viết cũng nói station hiện tại là stream liên tục; DJ/playlist segment là hướng mở rộng tương lai (lines 146-153). Đây là cam kết/tài liệu của dự án, không xác nhận chính xác revision đang chạy cục bộ.
- [Rockstar Support: Enabling the MP3 player in GTA: San Andreas](https://support.rockstargames.com/articles/4tCqWlOXlZd2dE1xxHUFQg/enabling-the-mp3-player-in-gta-san-andreas), cập nhật 22/04/2024: mô tả shortcut hoặc MP3/WMA trong User Tracks, scan trong Audio Setup, chọn usertracks; ghi chú tùy chọn áp dụng cho Steam PC/Mac và iOS. Log cục bộ lại nhận diện executable là v1.0 HOODLUM, nên hướng dẫn Rockstar không đủ để khẳng định menu/codec tương thích trên build này.
- [Project Eagle home](https://www.projecteaglemod.games/) xác nhận đây là total conversion GTA SA; trang chủ không định danh version cụ thể của thư mục local.
- [Project Eagle Releases](https://www.projecteaglemod.games/releases) liệt kê v1.3.0 (06/2026, 1.6 GB) và yêu cầu base game GTA SA 1.0; listing không nói RadioEx audio pack có được phát hành riêng hay không. [FAQ chính thức](https://www.projecteaglemod.games/world/faq) không có mục radio/audio. Bài radio mô tả cần cung cấp audio files cùng config nhưng không nêu package path hay nơi tải audio. Vì vậy, nguồn chính thức hiện xem được không xác nhận có audio pack tải riêng hoặc loader layout khác; trạng thái này vẫn unknown.

Không dùng URL browser `pe-1.3.0` làm bằng chứng version. Theo xác nhận của người điều phối tác vụ, local changelog nhận diện Eagle v1.3 và ModLoader 0.3.7; phát hiện này chưa được kiểm tra độc lập trong khảo sát này.

## Đánh giá các hướng

| Hướng | Kết quả mong muốn | Mức phù hợp |
|---|---|---|
| User Tracks | Một playlist custom ở station User Tracks, có chế độ Radio/Random/Sequential theo bản SA hỗ trợ. | Cách nhanh nhất nếu chỉ cần nghe một danh sách. Nhưng documentation Rockstar chỉ khẳng định cho các bản nêu trên; executable local được log nhận diện HOODLUM nên cần kiểm tra riêng khi triển khai. Không tạo nhiều station có tên anime riêng. |
| Thay audio station đang có | Giữ tên/sprite/kênh, thay nội dung audio được station đó trỏ tới. | Số thay đổi khái niệm thấp, nhưng ảnh hưởng station đó và có thể làm thay đổi nội dung vùng Eagle. Không phù hợp nếu muốn giữ radio Eagle nguyên trạng; cũng chưa biết mọi đường dẫn audio đang được đóng gói ở đâu. |
| Thêm station RadioEx có tên riêng | Một hoặc vài station xuất hiện trong danh sách RadioEx tại vùng khai báo, mỗi station có tên, audio path, sprite và duration. | **Khuyến nghị** cho trải nghiệm nhiều kênh anime/game. Cục bộ đã có config format và feature enabled; tài liệu Eagle nói hệ thống data-driven và mở rộng station. Cần xác minh parser ở bản v1.3 chấp nhận thêm dòng, xử lý station mới khi chọn vùng muốn lái, sprite hợp lệ hoặc chế độ text, và format audio/loop trước khi ghi file. |

### Đề xuất trải nghiệm

Bắt đầu bằng 2-3 kênh có cá tính rõ thay vì thay cả lineup Eagle: ví dụ một kênh J-pop/anime opening, một kênh instrumental/lo-fi để lái thư thái, và một kênh game soundtrack. RadioEx cho tên station riêng giúp người chơi chọn kênh như radio trong game. Nếu mục tiêu chỉ là playlist phát ngẫu nhiên và không quan trọng tên kênh, User Tracks ít cấu hình hơn, nhưng sẽ là một kênh user playlist duy nhất.

## Cần chốt trước khi triển khai

Mặc định theo mục tiêu hiện tại là **nhiều station custom có tên riêng qua RadioEx**. Khi chuyển sang triển khai, chỉ cần chốt:

1. Tên/nhãn và số lượng kênh, cùng màu nhạc muốn nghe (ví dụ anime opening, J-pop, Vocaloid, game OST, lo-fi hoặc city pop).
2. Phạm vi vùng phủ: tất cả vùng thường lái xe hay một số region Eagle cụ thể.
3. Audio asset sẽ dùng: file do người dùng chọn/cung cấp, hay cần khảo sát nguồn trước; đồng thời chọn sprite/text phù hợp. Cấu hình hiện bật sprite HUD.

Cơ chế virtual position/background playback được bài Eagle mô tả, nhưng vẫn cần runtime check ở đúng build trước khi xem là hành vi đã xác nhận.

## Ranh giới xác nhận

Đã đọc file cấu hình, log, changelog, danh sách thư mục audio/scripts/User Files và tài liệu web nêu trên. Không launch game, không nghe thử, không sửa game, không thêm playlist, không xác nhận chuyển kênh hay UI trong runtime. Kết luận “nhiều station có tên riêng khả thi” dựa trên cấu hình local và tài liệu Eagle; kết quả hoạt động trong đúng build vẫn cần kiểm chứng ở giai đoạn triển khai.
