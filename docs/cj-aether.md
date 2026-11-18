# CJ → Aether trong Project Eagle

> [!IMPORTANT]
> **Cập nhật trạng thái ngày 06/11/2026 — ĐÃ HOÀN TẤT THAY THẾ TRỰC TIẾP TRÊN `model_id = 0` + BỘ ĐỒ 3D GENSHIN MẶC ĐỊNH TÁCH RỜI 3 MÓN (`gameplay-lab`):**
> Hạng mục tạm dừng dưới đây (vốn chỉ chọn Aether thủ công qua `F2` `RZL-Trainer` trên bản `clean` lưu trữ cũ và chưa hỗ trợ quần áo/mập ốm) nay đã được **khởi động lại và hoàn tất toàn diện cả Phase 1 lẫn Phase 2 theo Hướng C + Cách 1 (`models/player.img` + `data/clothes.dat` + `cleo/EagleAetherDefaultOutfit.cs`)** trên bản chơi chính thức `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
> - **Hiện trạng mới:** Aether spawn tự nhiên ngay ở **`model_id = 0`** khi vào **New Game** và **tự động mặc sẵn Bộ Trang Phục 3D Genshin Impact Gốc tách rời 3 món chuẩn native `CClothes`** (**Áo Genshin `painter` `Slot 0` + Quần Thụng Genshin `leathertr` `Slot 2` + Bốt Chiến Giáp Genshin `biker` `Slot 3`**, mở khóa sẵn trong tủ đồ Safehouse, `0` vòng lặp chạy ngầm), hỗ trợ phối lẻ tự do với toàn bộ **`258` trang phục cửa hàng**, biến hình **Mập / Ốm / Cơ bắp (`Fat` / `Normal` / `Ripped`)**, **`33` kiểu tóc/nhuộm nguyên tố Barbershop**, **`48` hình xăm**, đội mũ/nón bảo hiểm không xuyên tóc (`flatears`), **`8` đồ đặc biệt** và **`22` model cắt cảnh `cs_*.dff`**.
> - **Tài liệu bàn giao, SHA-256 & Rollback hiện hành:** Xem [`aether-full-player-img-overhaul-2026-11-06.md`](aether-full-player-img-overhaul-2026-11-06.md). Nội dung bên dưới được giữ nguyên để lưu lịch sử khảo sát ngày 13/10/2026.

Ngày thực hiện: **13/10/2026**. Game duy nhất được xử lý:

```text
C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean
```

## Trạng thái bàn giao

**Kết thúc tác vụ ngày 13/10/2026:** người dùng báo cách chọn Aether qua F2 đã thử ổn. Sau đó đã thử bổ sung tự nạp khi bắt đầu/load game; người dùng báo có vẻ không hoạt động và yêu cầu gỡ. Phần tự nạp đã được gỡ hoàn toàn: xóa gói `modloader\Aether-Autoload`, khôi phục `data\default.dat` đúng hash trước thử nghiệm. Giữ nguyên cặp AETHER trong RZL-Skin để tiếp tục dùng F2. Cả 12 file đối chiếu đều khớp baseline trước thử nghiệm tự nạp. [Biên bản phục hồi](aether-autoload-rollback.md).

**Đã cài cặp skin Aether vào cơ chế chọn nhân vật của RZL.** Bản cài dùng Aether v3.0 của FadXploit, biến thể **Shadeless DFF & Smaller TXD (for non-ENB)**. Cặp file đã được kiểm tra hash và thử gỡ/cài lại thành công. Người chơi cần chọn Aether trong trainer khi vào game; tác vụ này chưa thêm cơ chế tự chọn skin mỗi lần khởi động.

**Phạm vi kiểm chứng gameplay:** người dùng đã báo tự thử qua F2 ổn, nhưng chưa cung cấp kết quả riêng cho từng dòng checklist bên dưới. Agent chưa trực tiếp nghiệm thu gameplay. Trong lượt cài ban đầu, đã mở đúng executable Eagle, tới cửa sổ `GTA: Project Eagle`, nhưng công cụ chụp hình bị timeout; người dùng sau đó dừng Computer Use bằng phím Escape. Không tiếp tục điều khiển game sau tín hiệu đó. Người dùng báo đã tắt game; đã kiểm tra process Eagle không còn chạy trước khi cài. Không coi kết quả kiểm tra tĩnh dưới đây là bằng chứng đã thử đầy đủ animation, save/load, nhiệm vụ hay cutscene.

## Kích hoạt và trở lại CJ

1. Mở game từ đúng thư mục trên, vào một phiên single-player/freeroam.
2. Nhấn **F2**, theo đường **Player Options → Change Player → ModLoader Actors**, chọn **AETHER**, nhấn **Enter**. Dùng phím mũi tên để di chuyển, **Backspace** để quay lại.
3. Để trở lại CJ, tìm **Change Player → Normal Actors → 000_DEFAULT**. Đường này có trong chuỗi menu của trainer local; chức năng phục hồi CJ chưa được thử trực tiếp.

Đường dẫn menu là bằng chứng từ `cleo\RZL-Trainer.cs` local, chưa phải ảnh menu đã mở trong game. Trainer config ghi **5.CBT1.3**, không gán nhãn nó thành release 5.0.0/5.0.1 từ các listing khác. ModLoader **0.3.7**, CLEO **5.0.3** được nhận diện từ log. File rules local giới hạn basename 7 ký tự; `AETHER` có 6 ký tự.

Nếu skin không giữ sau load/restart, chọn lại bằng F2. Thử nghiệm tự nạp đã được gỡ theo yêu cầu; hiện không có cơ chế tự chọn Aether đang cài. Không dùng chức năng Save Game của trainer để ghi đè slot đang chơi khi chưa thử bằng slot riêng.

## Lựa chọn asset

Nguồn chính: [GTAinside — Aether from Genshin Impact, FadXploit](https://www.gtainside.com/en/sanandreas/skins/156646-aether-from-genshin-impact/). Archive v3.0: [file gốc](https://files.gtainside.com/202012/1677955155_FadXploit%20Aether%203.0.7z). Readme trong archive ghi model **HoYoverse (miHoYo)**, rig/convert/port **FadXploit**, năm **2023**, và mô tả biến thể shadeless dành cho GTA SA non-ENB/thiết bị nhẹ. Credit và readme gốc được giữ trong staging. [Báo cáo so sánh ứng viên](aether-candidates.md) có nguồn và giới hạn của ứng viên Miyata Lee chưa tải được archive hợp lệ.

| Thuộc tính | Bản thường | Bản shadeless đã cài |
| --- | ---: | ---: |
| DFF | 1.265.954 byte | 1.080.110 byte |
| TXD | 4.981.288 byte | 1.311.272 byte |
| Cặp file | 6.247.242 byte | 2.391.382 byte |
| Vertex / tam giác | 15.487 / 17.706 | 15.487 / 17.706 |
| Skeleton / trọng số | 32 bone, 1–3 ảnh hưởng/vertex | Cùng bảng HAnim và cùng dữ liệu indices/weights |
| Normal trên mesh | Có | Không |
| Texture body | 1024×1024, XRGB không nén | 1024×1024, DXT1 |
| Texture face / hair | 512×512 DXT1 | 512×512 DXT1 |

Không thấy `enb*`, `d3d9.dll` hoặc `dxgi.dll` ở root Eagle trong lần kiểm tra này. Vì thế chọn biến thể non-ENB do tác giả cung cấp: giữ hình dáng, chi tiết texture ở cùng độ phân giải và rig, với shading phẳng phù hợp phong cách anime. Cặp file giảm khoảng **62% dung lượng lưu trữ**, nhưng **không giảm số tam giác** và chưa có benchmark FPS/VRAM. DXT1 nén mất dữ liệu; không khẳng định ảnh đẹp ngang bản body không nén trong mọi góc nhìn. Bản thường được giữ nguyên trong staging để có thể so sánh sau, không cài ENB hay thay shader của Eagle.

Ảnh showcase trong archive và texture giải mã đã được xem. Showcase có hậu kỳ mạnh, nên không coi nó là hình ảnh kết quả tại Eagle. Texture body, tóc và mặt có đủ tên khớp vật liệu; không có texture tham chiếu bị thiếu. Hình dáng Aether, màu tóc, mặt và hoa văn quần áo được bảo toàn ở mức asset. Chất lượng hiển thị, ánh sáng ngày/đêm, độ rõ ở khoảng cách chơi và clipping còn cần thử.

## Kiểm tra rig và tài nguyên thực tế

Script chỉ đọc: `staging\project-eagle\aether\inspect_assets.py`; kết quả đầy đủ: `staging\project-eagle\aether\asset-audit.json`. Layout RenderWare đối chiếu với mã nguồn [DragonFF DFF](https://github.com/Parik27/DragonFF/blob/master/gtaLib/dff.py) và [TXD](https://github.com/Parik27/DragonFF/blob/master/gtaLib/txd.py).

- Đọc `player.dff` thực tế từ `S&S\Cdimages\default\COMPONENTPEDS.img` của Eagle, chỉ trong bộ nhớ; không thay archive. `models\player.img` chứa các phần quần áo/texture, không có member `player.dff` trong directory đã đọc.
- Cả Aether và player Eagle có **33 frame** và **32 bone HAnim**. Bảng **bone ID/index/flags khớp hoàn toàn**. Thứ tự frame lưu trong file khác nhau; sau mapping theo bone ID, quan hệ parent-bone khớp hoàn toàn. Đây là bằng chứng tương thích skeleton cơ sở, chưa chứng minh từng animation.
- Có vai/cánh tay/cẳng tay/bàn tay/ngón tay, đùi/cẳng chân/bàn chân/ngón chân. Vertex của Aether có ảnh hưởng 1 bone: **9.330**; 2 bone: **4.833**; 3 bone: **1.324**. Không có active index vượt 32 bone, vertex không trọng số, trọng số âm/NaN/Inf, ma trận không hữu hạn, hoặc tổng trọng số lệch 1 quá `1e-4`.
- Hai biến thể có **cùng hash dữ liệu indices/weights**, cùng số tam giác và gần như cùng bounds; mesh shadeless không phải bản giảm polygon. Một geometry, một atomic, **18 material entry**. GPU/draw call thực tế chưa đo.
- Tóc/bím tóc/vạt áo **không có hệ bone riêng của Genshin** trong bảng HAnim này. Chưa có bằng chứng cloth/hair physics. Chúng đi theo rig SA, nên clipping khi ngồi xe, chạy, crouch hoặc leo còn phải đánh giá.
- Bone jaw/brow tồn tại nhưng không có vertex ảnh hưởng tới chúng; mặt chủ yếu đi theo head. **Không thể coi biểu cảm miệng/lông mày của CJ là được hỗ trợ đầy đủ.** Không có tài nguyên biểu cảm hay animation Genshin riêng được cài.
- Bốn texture trong TXD shadeless đều là **D3D9/DXT1**, gồm body/logo 1024×1024 và face/hair 512×512, mỗi texture chỉ **1 mip level**. Giải mã không thấy pixel alpha trong suốt/bán trong suốt; 18 màu material đều alpha 255. Tóc/lông mi/vạt áo dựa vào geometry, không có alpha-card được xác nhận. Cần nhìn từ hai phía và xa để phát hiện mặt mất/cạnh răng cưa/shimmering. Ở bản thường, body dùng XRGB: byte alpha lưu bằng 0 nhưng cờ texture không bật alpha, không được diễn giải thành body trong suốt.

**Giới hạn decoder:** cả hai DFF có Struct đầu khai báo size `0x0100000C`; parser chỉ diễn giải low 24 bit thành 12 byte trong bộ nhớ để đọc layout, và chỉ kiểm tra clump đầu, còn **35.087 byte trailing data** chưa giải nghĩa. DFF cài vào game giữ nguyên byte từ archive; không sửa header hay loại trailing data. Vì vậy việc parser đọc được skeleton/geometry không chứng minh game sẽ nạp file thành công. Đây là điểm cần xác minh đầu tiên khi chọn AETHER.

## Thay đổi và bản phục hồi

Chỉ thêm hai file vào game, trước đó cả hai đều không tồn tại:

| File tương đối tại root Eagle | Byte | SHA-256 |
| --- | ---: | --- |
| `modloader\RZL-Skin\AETHER.dff` | 1.080.110 | `1E94D607E25C8BA40FC7E87C6647DBE623B138DD7EF4502FA4A9ACE65E78668C` |
| `modloader\RZL-Skin\AETHER.txd` | 1.311.272 | `F1D1CE9F8D79502D9EA901EFC0033B371B626545312432A6C7BC2341F97AE404` |

Tên nguồn `Aether_SL.dff/txd` được đổi basename thành `AETHER`, nội dung file không đổi. Không sửa player.img, componentpeds.img, cutscene archive, NPC, radio, script gameplay hay animation hệ thống. Không thay trainer/version/loader.

Thư mục phục hồi:

```text
C:\Users\LENOVO\Desktop\GTA\backups\project-eagle\cj-aether-20261013
```

Có bản sao cấu hình RZL/ModLoader và file rules trước tác vụ, `baseline.json`, `installed.json`, `protected-files-after.json`, cùng hai script:

- **Remove-Aether.ps1**: game phải tắt; kiểm tra đúng path và hash rồi chỉ xóa cặp AETHER đã cài. Nếu file đã được đổi sau tác vụ, script từ chối xóa để tránh gỡ nhầm bản mới.
- **Reinstall-Aether.ps1**: game phải tắt; lấy cặp đã xác minh từ staging `ready`, không ghi đè file khác hash. Có thể chạy lại khi cặp đúng đã tồn tại.

Đã chạy lượt **gỡ → kiểm tra hai file vắng mặt → cài lại → kiểm tra SHA-256**, thành công. Trạng thái cuối cùng là cặp skin **đang được cài**.

Để gỡ hoàn toàn, ưu tiên chuyển về `000_DEFAULT` và chỉ save vào slot riêng đã kiểm tra, thoát game, rồi chạy Remove-Aether.ps1 trong PowerShell. Vì hai file trước đó không tồn tại, phục hồi cài đặt không cần ghi đè archive hoặc toàn bộ cấu hình. Với save thử đang lưu custom model, không mặc định xóa file là đủ phục hồi save; hãy dùng slot CJ gốc hoặc chọn default trước khi save.

Hash sau tác vụ khớp baseline cho **9 file được bảo vệ**: hai executable, player.img, gta.dat, default.dat, peds.ide, RZL-Trainer.ini, modloader.ini và rules của RZL-Skin. COMPONENTPEDS.img chỉ được mở bằng chế độ đọc. Không tạo hoặc ghi đè save người dùng; thư mục `Documents\GTA PE User Files` không có save file được quan sát trước/sau phép thử mở game.

## Checklist thử thủ công để nghiệm thu

**Agent chưa trực tiếp thử các dòng bên dưới trong Eagle.** Người dùng đã báo thử cách F2 ổn; chưa có kết quả chi tiết cho từng mục. Checklist được giữ làm tài liệu tham khảo, không phải công việc tiếp tục chờ thực hiện sau khi tác vụ đã kết thúc. Dùng slot test riêng, không overwrite save đang chơi.

| Nhóm | Thao tác cụ thể | Điều kiện đạt |
| --- | --- | --- |
| Nạp/ngoại hình | Mở F2, chọn AETHER; xoay camera; nhìn ngày/đêm, gần/xa | Nạp xong, đúng Aether, đủ mặt/tóc/quần áo, không mất mặt ở góc sau |
| Đi bộ/chạy/sprint | Di chuyển thẳng, chéo, xoay hướng, sprint rồi dừng | Chân/tay đúng, không kéo giãn mesh hoặc kẹt pose |
| Crouch | Crouch đứng yên/di chuyển, crouch aim | Hông/gối/vạt áo chấp nhận được, thao tác vẫn hoạt động |
| Nhảy/leo | Nhảy, qua hàng rào thấp, leo bám/leo lên vật cản | Tay/chân hoạt động, không méo vai/torso; không dùng ladder mod ngoài phạm vi |
| Melee | Đấm, combo, cầm melee, nhận hit/ngã/đứng dậy | Tay/ngón tay đúng tương đối, không mesh nổ hoặc lỗi animation |
| Vũ khí | Pistol + rifle/shotgun: cầm, aim, bắn, reload; thêm crouch aim | Tay đặt gần grip, nòng/aim đúng, reload không méo tay |
| Bơi | Bơi mặt nước, lặn, nổi lên, lên bờ | Tay/chân/body ổn, không đứng sai pose hoặc mất texture |
| Ô tô | Vào/ra hai phía, ngồi lái, rẽ, lùi; nếu dùng thì drive-by | Tay/vô-lăng, chân/ghế và cape clipping chấp nhận được |
| Motorbike | Vào/ra, lái chậm/nhanh, nghiêng rẽ, ngã/đứng dậy | Pose tay/chân đúng, không vạt áo xuyên nghiêm trọng |
| Bicycle | Lên/xuống, đạp thường/sprint, rẽ | Chân quay theo pedaling, grip đúng, không kéo giãn mesh |
| Tương tác | Nhặt vật/vũ khí, ngồi/các tương tác đang có, vào interior | Input/task hoạt động; ghi riêng biểu cảm mặt tĩnh |
| Save/load | Chọn Aether, save slot test, load slot đó từ menu | Ghi rõ còn Aether hay trở lại CJ, thử chọn lại nếu cần |
| Restart | Thoát game sạch, mở lại, load slot test | Ghi rõ skin có cần chọn lại; không kết luận từ một lần chọn |
| Nhiệm vụ/cutscene | Thử một nhiệm vụ bằng save test; quan sát trước/trong/sau cutscene | Ghi rõ cutscene có dùng CJ riêng hay Aether; freeroam sau đó còn hoạt động |
| Phục hồi CJ | Chọn Normal Actors/000_DEFAULT, thử đi/lái, save test và restart | CJ trở lại ổn, không phụ thuộc cặp AETHER sau khi gỡ |

Cutscene có thể dùng actor/model riêng của script. Gói này không thay `csplay.dff` hoặc archive cutscene, nên chưa hứa Aether xuất hiện trong toàn bộ phim cắt cảnh. Không hứa hỗ trợ quần áo/tattoo/body morph của CJ trên skin toàn thân. Multiplayer không thuộc phạm vi nghiệm thu này.

## Tài liệu và artifact liên quan

- [Ứng viên và nguồn asset](aether-candidates.md).
- [Cơ chế RZL local và offset bằng chứng](rzl-aether-workflow.md).
- Staging: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\aether` — archive gốc, extracted, ready, script/audit và texture-preview.
- Archive SHA-256: `CFC3D6129B8E493703579683E21DD2593B054B2A7F2F7E06A38EC2EE939F4F2B`.

Trạng thái cuối cùng: **giữ Aether chọn qua F2; người dùng báo đã thử ổn; tự nạp đã gỡ và tác vụ đã kết thúc.** Skeleton/weights có bằng chứng phù hợp player Eagle; chưa có nghiệm thu chi tiết toàn bộ checklist.
