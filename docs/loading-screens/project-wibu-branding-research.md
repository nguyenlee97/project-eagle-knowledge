# Project Wibu branding research

Khảo sát tĩnh ngày **14/10/2026** trên bộ Project Eagle tại `Project Eagle/gta sa clean/gta sa clean`. Chỉ ghi tài liệu; không tạo artwork, sửa PECore/TXD/config, cài mod hay chạy game.

## Kết luận

Có hai đường branding khác nhau:

- Poster loading **Grand Theft Auto / Stars and Stripes** nằm bake trong các raster `LOADSC1`…`LOADSC14` của `models\txd\LOADSCS.txd`. Để thay chữ thành **Grand Theft Auto Wibu World** trên mọi poster có thể được chọn ngẫu nhiên, cần thiết kế lại đủ 14 member. Chữ không phải text riêng để sửa trong config. Các poster đã là ảnh hoàn chỉnh, nên typography Genshin và logo mới cần được compositing vào từng raster.
- Logo startup PECore là PNG nhúng `RCDATA/type 10, id 200, lang 1033` trong `PECore.asi`. Static trace lần này xác nhận mã PECore nạp PNG đó qua `FindResourceA`, giải mã bằng GDI+ rồi vẽ trong cửa sổ splash có nền alpha. Không thấy tùy chọn/đường dẫn ảnh ngoài nào trong config hoặc code path đã kiểm tra. Thay logo cần một thao tác resource-aware trên bản sao có backup, không thể cài như TXD hay đặt một PNG cạnh executable.

Hai nguồn ảnh được kiểm chứng và route kỹ thuật được tóm tắt dưới đây. Runtime vẫn chưa được thử, nên kết luận về vị trí hiển thị, alpha trên màn hình thật và overlay ModLoader là đánh giá tĩnh.

## Poster loading: Wibu World

`CLoadingScreen::LoadSplashes` trong PC-US executable mở `LOADSCS.txd`, dùng `title_pc_US` và sáu member được chọn từ `loadsc1`…`loadsc14`. Vì vậy chỉ thay một poster làm kết quả không nhất quán: sáu ảnh khác vẫn có thể hiện logo cũ. Mỗi member là một raster hoàn chỉnh, không có layer logo độc lập. Giữ nguyên kích thước, tên, codec và mip của từng member theo [manifest hiện tại](manifest.json); không chuẩn hóa các ảnh về cùng độ phân giải.

ModLoader hiện nạp `gta3.std.sprites`, trong khi `gta3.std.stream` bị tắt. Tài liệu đi kèm `std.sprites` mô tả dictionary trong `txd/` và ví dụ đúng file `modloader/my splash/txd/loadscs.txd`. Do đó overlay cả dictionary dưới một thư mục ModLoader riêng là route artwork có tài liệu hỗ trợ, còn khả năng hiển thị cuối cùng cần nghiệm thu runtime. Route này chỉ tác động TXD loading; nó không sửa ảnh startup nhúng PECore.

Đề xuất typography cho tranh mới: giữ nguyên đúng chuỗi **“Grand Theft Auto Wibu World”**, chia hierarchy thành “GRAND THEFT AUTO” và “WIBU WORLD” để đọc được ở thumbnail. Có thể gợi chất Genshin qua nét serif/cắt cạnh thanh, nhấn vàng ấm và đỏ trầm, nhưng giữ tương phản cao và không dùng chi tiết nhỏ chen vào logo. Giữ logo ở vùng đặt mark hiện tại trong từng poster, đồng thời vẽ lại cả cảnh để chữ mới không trông như miếng dán trên nền cũ. Loading bar/status là lớp UI riêng; đừng bake chúng vào ảnh.

`title_pc_US` là member khác trong cùng dictionary và có Project Eagle/legal art bake trong hình. Nếu mong muốn đổi branding ở cả title screen, hãy thiết kế riêng member này sau khi xác định rõ phần legal nào cần giữ. Thay 14 poster không tự thay đổi title image.

## Logo startup PECore: Project Wibu + silhouette Hu Tao

PECore nhúng PNG **640×640 RGBA**, resource `10/200/1033`, dài **166.605 byte**. PNG trích sẵn có nền trong suốt và anti-alias. Static call chain tìm đúng resource 200 trong module PECore, lấy payload, chuyển thành GDI+ image rồi vẽ lên cửa sổ layered. Code cũng vẽ riêng dòng **“Project Eagle is loading”** bằng GDI+; dòng này không nằm trong PNG. Nếu chỉ đổi bitmap thành “Project Wibu”, dòng trạng thái vẫn có thể hiện Eagle. Việc đổi dòng code/text này cần được tách ra thành scope riêng; khảo sát này không đề xuất patch core.

Brief hình ảnh phù hợp với canvas hiện tại:

- Dùng silhouette Hu Tao có thể nhận ra ở kích thước nhỏ: mũ tròn và phù hiệu hoa, mái/tóc dài thành hai đuôi, cùng một hoặc hai butterfly accent.
- Giữ hình chính gọn, viền rõ và ít khe nhỏ để alpha không mất khi render; cân palette than/đỏ san hô/vàng ấm thay cho gradient xanh-tím-đỏ của đại bàng hiện tại.
- Đặt chữ **“PROJECT WIBU”** thành hai dòng hoặc một wordmark rộng gọn ở giữa silhouette, với nét fantasy thanh và tương phản sáng/viền tối để đọc trên vùng trong suốt. Giữ nền RGBA trong suốt; chưa biết màu desktop phía sau cửa sổ thực tế nên cần kiểm tra sau khi cài staging.

Đây là hướng art, chưa phải asset đã tạo. Hãy giữ nguyên PNG alpha, kiểm tra ở kích thước thật và thu nhỏ trước khi thay resource.

## Rủi ro và route triển khai nếu được yêu cầu sau

Trong PECore.asi, resource PNG 200 kết thúc ở raw offset `0x2BD39D`; resource kế tiếp bắt đầu tại `0x2BD3A0`, chỉ cách **3 byte**. PNG mới dài hơn sẽ đè dữ liệu resource kế tiếp nếu ghi chồng trực tiếp tại offset hiện tại. PE không có Authenticode security directory trong snapshot này, nhưng chưa biết có launcher/integrity check bên ngoài hay không.

Nếu người dùng yêu cầu triển khai sau này: backup PECore.asi, dựng bản staging, sửa đúng resource 200 bằng PE resource-aware editor để công cụ cập nhật kích thước và vị trí trong `.rsrc`, rồi kiểm lại PE/resource table trước khi thử game. Với poster, dựng bản sao `LOADSCS.txd` có đủ 14 poster; chỉ thử overlay dưới thư mục ModLoader riêng sau khi kiểm tra toàn bộ member. Đánh giá runtime phải tách hai cửa sổ: startup PECore và loading sequence của game.

Không đổi tên executable, save, thư mục cài hay hook lõi theo scope hiện tại. `Project Eagle is loading` được ghi nhận là dòng code riêng nhưng chưa thay.

## Bằng chứng và giới hạn

- [PECore resource xref, offsets và điều kiện kích thước](evidence/branding-pecore-resource-xref.txt)
- [Kiểm tra tùy chọn override và loader hiện có](evidence/branding-external-path-check.txt)
- [Trace loading poster và log/config trước đó](loading-trace.md), [ảnh trích PECore](../../../staging/project-eagle/loading-screens/source/pe-resources/PECore-RCDATA-200.png)

Phân tích PE là static, dùng pefile/Capstone có sẵn; REA provider không sẵn trong phiên này. Log PECore, changelog, code và resource cho thấy PNG 200 được dùng trong splash, nhưng không có capture runtime để xác nhận thời lượng, bounding box, opacity trên desktop, final loading-screen selection sau mọi hook, hay hoạt động của overlay `std.sprites`. Không suy rộng kết quả âm tính từ phần config/code đã kiểm tra thành bằng chứng rằng không thể có mechanism ngoài khác.
