# Initial prompt: xây Radio Studio end-to-end cho Project Eagle

Tôi muốn bạn đảm nhận một tác vụ mới cho project GTA: **xây một công cụ có UI hoàn chỉnh để quản lý, chỉnh sửa và đưa radio custom vào Project Eagle**. Tôi muốn thêm bài vào playlist bằng thao tác đơn giản, tạo/sửa các kênh và chọn nơi chúng phát, thay vì mỗi lần phải ghép nhạc, đổi tên file và sửa config bằng tay.

Đây là yêu cầu **nghiên cứu rồi triển khai một sản phẩm dùng được từ đầu đến cuối**, không dừng ở tài liệu, script dòng lệnh, UI mock hoặc một kênh nhạc cài thủ công. Tên làm việc của tool là **Eagle Radio Studio**; bạn có thể đặt tên phù hợp hơn.

Prompt cập nhật ngày **14/10/2026**, múi giờ **Asia/Saigon**. Tôi đang dùng AI khác để nghiên cứu và làm gameplay mod sâu cho Eagle. Nếu bạn chính là AI đó, hãy tận dụng kiến thức, source, công cụ và gameplay-lab đã có, đồng thời kiểm tra lại trạng thái hiện tại. Nếu là một chat mới, dùng các đường dẫn bàn giao bên dưới để bắt đầu.

## 1. Trải nghiệm tôi muốn

Tôi đang làm một thế giới GTA có không khí anime: Aether là nhân vật chính, NPC từ game/anime, lái xe dạo phố và nghe các kênh nhạc tôi chọn.

Với radio, tôi muốn:

- Có nhiều station mang tên riêng, mỗi station có playlist của nó.
- Thêm bài bằng chọn file hoặc kéo thả; nghe thử, sắp xếp và sửa playlist trong UI.
- Có các kênh chung cho nhiều vùng, và một số kênh chỉ xuất hiện ở những vùng nhất định. Không bắt mọi nơi có lineup giống hệt nhau.
- Tôi đã để ý trong game có sự khác nhau về radio theo vùng. Hãy kiểm tra cơ chế thực tế, không chỉ dựa vào cảm nhận này hoặc chú thích config.
- Khi tôi sửa playlist, tool tự xử lý audio/config cần thiết và giúp cập nhật vào game, có cách phục hồi.
- Tôi sử dụng như một ứng dụng bình thường. Chi tiết codec, IMG/TXD, region ID và cấu trúc config thuộc phần kỹ thuật/advanced, không phải thứ tôi phải thao tác thủ công để thêm một bài hát.

Ví dụ minh họa ý tưởng, **chưa phải danh sách station đã chốt**: một kênh anime/J-pop dùng ở nhiều vùng; một kênh city pop riêng cho một vùng đô thị; một kênh instrumental/OST ở vùng khác. Các tên, nội dung và vùng phủ phải chỉnh được trong tool.

## 2. Workspace, game và trạng thái cần bảo toàn

Workspace:

```text
C:\Users\LENOVO\Desktop\GTA
```

Game chính:

```text
C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean
```

Mục tiêu là **Project Eagle trên GTA San Andreas PC**, không phải GTA SA vanilla hoặc GTA Underground. Khảo sát cũ ghi Eagle **v1.3**, PECore build **Jun 15 2026**, nền **GTA SA v1.0 US HOODLUM/x86**, ModLoader **0.3.7** và CLEO **5.0.3**. Xác minh identity/config/module đang dùng trước khi can thiệp; không mặc định mọi binary hoặc API của SA gốc phù hợp.

Trạng thái chúng tôi đã có:

- Aether qua F2/RZL, với cặp `modloader\RZL-Skin\AETHER.dff/txd`. Thử nghiệm tự nạp Aether đã được gỡ; không phục hồi lại nó.
- Bộ thử NPC cảnh sát/SWAT/quân đội đã đổi sáu member trong `S&S\Cdimages\default\COMPONENTPEDS.img`, có backup. Task NPC vẫn phát triển riêng.
- Nghiên cứu gameplay sâu và PoC mới đang được AI khác làm. Có tài liệu mô tả game-lab cách ly, `EagleLifePoC.cs` và `EagleCompanion.py`; hãy đọc trạng thái thật trước khi tái sử dụng hoặc chạy.

Không ghi đè Aether, bộ NPC, gameplay mods, core/plugin, save hoặc cấu hình không liên quan. Bản game có chữ `clean` trong tên không còn là baseline chưa mod.

Đọc:

```text
C:\Users\LENOVO\Desktop\GTA\AGENTS.md
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\README.md
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\radio.md
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\installation.md
```

Nghiên cứu engine có sẵn dưới:

```text
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\deep-gameplay
```

Trong đó ưu tiên `README.md`, `01-identity-and-engine-architecture.md`, `03-extension-points-and-community-mods.md`, `04-target-architecture-and-feasibility.md`, `06-gameplay-lab-and-poc-guide.md` và các evidence liên quan RadioEx. Đọc chọn lọc theo câu hỏi; kiểm chứng các kết luận cần dùng thay vì lặp lại toàn bộ nghiên cứu engine.

Tài liệu trước mô tả lab tại:

```text
C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab
```

Nếu lab hiện tồn tại và phù hợp, ưu tiên dùng để nghiệm thu radio trước khi áp dụng vào game chính. Tool phải hiển thị rõ target đang thao tác để tránh cài nhầm giữa main và lab.

Nếu không có quyền đọc ổ đĩa/tools trên máy, nói rõ và yêu cầu bộ dữ liệu tối thiểu cần thiết. Không coi các path trên là file bạn đã đọc. Không giả vờ có thể cài hoặc kiểm thử game từ một môi trường chỉ có chat.

## 3. Những gì đã biết về radio — và những gì chưa biết

Các file trọng tâm trong game:

```text
PECore.ini
PECore.log
data\radio.dat
S&S\ZON\radio.zon
data\gta.dat
data\default.dat
audio\
```

Các khảo sát/config quan sát ngày 13–14/10/2026 cho thấy:

- `[FEATURES]` của `PECore.ini` bật `RadioEx`; `[RadioEx]` có `UseVisualRadioSprites = true`.
- `data\radio.dat` có section vùng, `Region`, `RegionName`, `TxdName`, và nhiều dòng `Station` lặp cùng key.
- Header mô tả mỗi station là `Name,AudioFile,SpriteName,Duration`, đường audio tương đối root game, duration 0 để tự dò.
- Snapshot ghi 7 region sections / 63 station được cấu hình. Đây không phải số station đã nghiệm thu phát thành công.
- `radio.zon` có các zone type 5 và numeric region ID. Header `radio.dat` chỉ rõ nguồn region này.
- Có sự khác nhau giữa tên section, tên hiển thị, region ID và tên folder audio: ví dụ `[LibertyCity]` có `Region=5` nhưng audio trỏ folder `REGION8`. **Không lấy tên folder audio làm ID vùng.**
- Chưa thấy `audio\PE` tại vị trí được cấu hình tham chiếu trong lần đọc thư mục gần nhất. Chưa xác định asset nằm ở layout khác, cần gói riêng hay baseline đang thiếu. RadioEx enabled không chứng minh mọi file radio có sẵn.
- User Tracks từng được quan sát tại `C:\Users\LENOVO\Documents\GTA PE User Files\User Tracks`. Đó là cơ chế playlist một kênh; không tự thay thế yêu cầu nhiều station theo vùng của tôi.

Nguồn web để đối chiếu với build thực tế:

- [Project Eagle](https://www.projecteaglemod.games/).
- [PE 1.3 changelog](https://www.projecteaglemod.games/changelog/pe-1.3.0).
- [Bài về RadioEx](https://www.projecteaglemod.games/news/6).
- [Releases](https://www.projecteaglemod.games/releases).
- [FAQ](https://www.projecteaglemod.games/world/faq).

Tài liệu RadioEx đã khảo sát mô tả một stream liên tục cho mỗi station; các playlist segment/DJ được nói như hướng phát triển. **Phải kiểm tra parser/player của đúng build**, không biến mô tả tương lai thành tính năng hiện tại.

## 4. Discovery cần làm trước khi chốt game adapter

Giải quyết các câu hỏi sau bằng source/binary/config/runtime thích hợp:

1. RadioEx đọc file nào, khi nào? Cơ chế nạp lại, cache hoặc yêu cầu restart là gì?
2. Station audio thực sự được resolve từ đâu? Vì sao các path baseline chưa thấy file? Các station thiếu audio tác động thế nào đến khởi tạo/player?
3. Codec/container, sample rate, channel layout, duration, loop và seek nào được hỗ trợ? Có giới hạn số region/station/path/size/memory không?
4. Một station có playlist nhiều file native không, hay chỉ nhận một stream? Có random/shuffle runtime, next-track, metadata bài hoặc virtual playback position không?
5. Region được chọn theo zone/player/vehicle bằng luồng nào? Làm gì ở vùng không có RadioEx section, nhất là nơi dùng radio SA gốc? Các zone chồng lấn hoặc chuyển ranh giới được xử lý thế nào?
6. Có thể dùng một station/audio source cho nhiều region không? Danh tính station và playback position có giữ được khi chuyển vùng không?
7. Game hiển thị tên/sprite như thế nào? TXD/sprite được nạp từ đâu? Text/default sprite có làm fallback hợp lệ mà không phá UI radio hiện có không?
8. ModLoader/plugin hiện tại có hỗ trợ overlay các file cần dùng không? Đừng coi ModLoader được bật là bằng chứng streamed replacement hoạt động: khảo sát NPC từng phát hiện stream plugin bị tắt.

Ưu tiên dùng RadioEx và các điểm mở rộng sẵn có. Chỉ viết adapter/plugin bổ sung khi có gap thật, với version binding và phạm vi rõ; không mặc định sửa PECore binary hoặc thay cả hệ radio bằng một audio player ngoài game.

REA skill có tại:

```text
C:\Users\LENOVO\.agents\skills\reverse-engineer-anything\SKILL.md
```

Đọc skill nếu dùng. Kiểm tra tools/providers thực tế, reuse evidence của research trước, chọn target theo câu hỏi. Không setup lại hạ tầng chỉ vì skill được nhắc đến. Tách source analysis, static binary/config và runtime; ghi Evidence ID khi có. Với source đầy đủ, đọc source thông thường trước.

Phần tìm kiếm rộng/khảo sát nặng ưu tiên giao GPT Luna nếu nền tảng hỗ trợ, theo AGENTS.md; model chính chọn kiến trúc, kiểm tra bằng chứng và điều phối triển khai.

## 5. Sản phẩm cần có: UI và luồng sử dụng

UI tiếng Việt mặc định, dễ đọc và dùng được trên Windows. Bạn chọn stack phù hợp với môi trường, khả năng bảo trì và cách đóng gói. Có thể là desktop app hoặc local web app, nhưng phải thực sự đọc/ghi filesystem, xử lý audio và cài vào game qua backend phù hợp. Không chỉ giao một trang HTML phát nhạc demo.

### Game target và thư viện radio

- Chọn/nhận diện root Eagle; hiển thị tên build và trạng thái target main/lab.
- Import cấu hình radio hiện có, hiện station/vùng và tình trạng audio/sprite đã tìm thấy hoặc đang thiếu.
- Phân biệt radio native không chỉnh được bằng adapter hiện tại với station RadioEx/custom có thể chỉnh.
- Giữ các station và cấu hình không liên quan. Không tự xóa các station baseline thiếu audio để làm bảng trông sạch.

### Station editor

- Tạo, đổi tên, nhân bản, bật/tắt hoặc gỡ station do tool quản lý.
- Có tên hiển thị và một identity nội bộ ổn định; playlist không mất liên kết chỉ vì đổi tên kênh.
- Sửa tên/assignment của station sẵn có trong phạm vi adapter hỗ trợ; ghi rõ nếu audio gốc chỉ là một stream, không có danh sách bài riêng để dựng lại.
- Logo/sprite là phần tùy chọn nếu cơ chế đã xác minh; có fallback hợp lệ để vẫn tạo kênh mà không phải làm TXD bằng tay.

### Playlist editor

- Thêm nhiều file qua file picker và drag-and-drop; các định dạng phổ biến như MP3/WAV/OGG/FLAC được probe/convert theo khả năng đã xác minh.
- Đọc duration và metadata phù hợp; sửa nhãn hiển thị khi metadata thiếu.
- Preview play/pause/seek ngoài game; reorder bằng kéo thả, xóa bài, thêm lại, lựa chọn thứ tự phát.
- Hiển thị số bài/tổng thời lượng, file lỗi hoặc mất nguồn và trạng thái thay đổi chưa build/chưa cài.
- Giữ nguyên file nhạc nguồn; import/build không ghi đè hoặc xóa chúng.
- Lưu project, mở lại và tiếp tục sửa. Không bắt tôi nhập lại playlist mỗi lần mở tool.

### Region editor

- Hiển thị region từ cấu hình/zone thật, với tên có nghĩa và liên kết numeric ID ở phần advanced.
- Gán station vào một hoặc nhiều vùng bằng thao tác rõ ràng; có góc nhìn **vùng → các kênh** và **kênh → các vùng**.
- Hỗ trợ mô hình **kênh dùng chung + kênh đặc thù từng vùng**; những vùng khác nhau có thể có lineup khác nhau.
- Cho chỉnh thứ tự kênh trong từng vùng nếu engine hỗ trợ. Không tự mở rộng vùng phủ của kênh riêng khi cập nhật playlist.
- Nếu tool có khái niệm “mọi vùng”, giải thích và compile theo các region được engine thực sự hỗ trợ. Không giả định có một global wildcard/native region 0 khi chưa xác minh.
- Preview lineup của từng vùng trước khi export/apply. Một bảng/matrix dễ đọc là đủ; bản đồ chỉ thêm nếu giúp thao tác và mapping tọa độ đã đúng.

### Build, apply và recovery

- Từ UI có thể validate project, build radio, xem phần sẽ thay, apply vào target và phục hồi bản trước.
- Có progress/cancel/error cụ thể, trạng thái source → build → installed. Không báo “đã cài” chỉ vì một request trả HTTP 200.
- Không yêu cầu người dùng tự chạy FFmpeg, sửa `radio.dat`, copy asset hoặc rebuild TXD cho mỗi lần thêm bài.
- Có launcher/cách mở đơn giản, tài liệu sử dụng ngắn và dependencies được phát hiện rõ. Không để một loạt terminal command thành luồng sử dụng chính.

## 6. Playlist trong UI và playlist trong game là hai lớp

Chốt adapter sau discovery:

- Nếu RadioEx hỗ trợ nhiều file/playlist thật, tận dụng khả năng đó và thử cơ chế play/shuffle/seek tương ứng.
- Nếu chỉ nhận một stream cho mỗi station, **tool vẫn quản lý các bài riêng trong project**, rồi tự convert/ghép/build ra audio tương thích. Lưu manifest thứ tự bài và offset để preview/debug; việc build không biến dữ liệu project thành một file mix không thể sửa lại.
- Chỉ rebuild station chịu ảnh hưởng, cache kết quả convert theo nội dung/options; một station dùng ở nhiều vùng không nên buộc build nhiều bản audio giống nhau.
- Xử lý transition, tổng duration, loop, mức âm lượng và clipping hợp lý. Preset cơ bản dùng được trước; không mở rộng thành một DAW đầy đủ.
- Không hứa “shuffle từng bài mỗi lần đang lái” nếu thực tế chỉ xáo trộn thứ tự lúc export. UI phải gọi đúng khả năng và thời điểm áp dụng.
- Không hứa live update/hot reload nếu build yêu cầu game restart. UI chỉ rõ lúc nào playlist mới có hiệu lực.
- Tên bài trong tool không đồng nghĩa game đã hiển thị now-playing metadata. Nếu engine không hỗ trợ, ghi rõ thay vì dựng UI giả trong game.

Build pipeline phải chạy ngoài game loop; không để game tick thực hiện transcode/file I/O lớn. Một thư viện nhạc lớn không được làm toàn bộ UI treo hoặc buộc build lại mọi kênh.

## 7. Data model, config và trạng thái cần xử lý đúng

Thiết kế dữ liệu riêng cho tool để tách: track/source asset, playlist/order, station identity, region assignments/order, build outputs/options và installed manifest/target/version.

- Một station có thể dùng chung ở nhiều vùng nhưng vẫn là cùng một đối tượng trong editor. Cách xuất sang engine phụ thuộc parser đã xác minh.
- Import `radio.dat` phải giữ được **nhiều dòng `Station=` lặp cùng key**, thứ tự, section và các trường cần bảo toàn. Không dùng parser INI chỉ giữ giá trị cuối rồi vô tình mất station.
- Giữ comment/section/entry không thuộc tool nếu đang chỉnh config hiện có; không serialize lại theo schema thiếu rồi xóa nội dung khác.
- Kiểm tra encoding, dấu phẩy, tên hiển thị, tên path có khoảng trắng/tiếng Việt và khả năng hiển thị trong game. UI có thể hỗ trợ Unicode, nhưng output phải theo parser/renderer thực tế.
- Playlist có thể chứa cùng một bài nhiều lần nếu người dùng chủ ý. Không deduplicate chỉ theo filename hoặc làm mất thứ tự đã chọn.
- Với file nguồn bị đổi/mất sau khi lưu project, hiển thị vấn đề và cho relink; không coi cached output cũ là playlist mới đã build thành công.
- Nếu game/config thay đổi sau lần import hoặc cài trước, phát hiện xung đột. Không áp baseline cũ lên các thay đổi mới của gameplay AI/task khác.

## 8. Apply/rollback phải là một phần của tool

Quá trình cài cần có candidate/staging đã validate, manifest file tool quản lý và backup trạng thái target **ngay trước lần apply đó**.

- Xác định file cần thay và hash trạng thái hiện có; không dùng một backup cũ có thể xóa các gameplay mod mới.
- Không thay asset đang bị game giữ/mở nếu chưa xác minh cách cập nhật an toàn. UI hướng dẫn đóng/restart game khi cần.
- Tránh trạng thái nửa audio mới/nửa config cũ khi lỗi hoặc cancel. Cần rollback được nếu một bước cài thất bại.
- Gỡ station/build chỉ tác động file tool sở hữu và entry tương ứng; không xóa cả thư mục audio, playlist nguồn hoặc station không liên quan.
- Preserve save, Aether, NPC archive, gameplay/AI mods và các file gốc ngoài phạm vi radio. Nếu cần đổi flag hoặc sprite setting chung, phải giải thích ảnh hưởng và chỉ thay phần cần thiết.
- Phục hồi/cài lại phải được thử và ghi rõ kết quả; không chỉ tạo một nút Restore chưa có backend thực hiện.

Tool cần chạy độc lập hoặc coexist rõ với `EagleCompanion`/gameplay-lab nếu tái sử dụng chúng. Không đổi protocol, port, cấu hình hoặc lifecycle của PoC cũ một cách ngầm định để làm radio.

## 9. Phạm vi triển khai và cách làm

Lượt này là yêu cầu xây tool, nên sau discovery hãy chọn kiến trúc rồi thực hiện phần đã rõ; không dừng sau một kế hoạch và hỏi lại từng thao tác phát triển thông thường. Được viết frontend/backend, data/build pipeline và adapter bổ sung khi cần trong phạm vi radio.

Tách code tool khỏi root game, với source và dữ liệu/staging được tổ chức rõ trong workspace. Ưu tiên nghiệm thu trên lab phù hợp. Apply vào game chính qua luồng được kiểm soát và bản phục hồi; không dùng nó làm nơi thử những thay đổi native chưa kiểm chứng. Giữ bản main hiện tại và các task khác ngoài phạm vi.

Không cần danh sách nhạc cuối cùng của tôi để xây editor. Làm sao để tôi tự chọn file trong UI. Có thể dùng asset test phù hợp để chứng minh pipeline; không trình bày nhạc/sound test là radio production tôi đã chọn.

Chỉ hỏi khi thật sự cần một đầu vào hoặc quyết định vượt phạm vi; chọn các mặc định hợp lý cho phần còn lại và ghi lại. Nếu có giới hạn runtime/tools, hoàn thành phần làm được và nêu đúng khoảng chưa nghiệm thu. Không gọi toàn bộ yêu cầu end-to-end hoàn thành khi chưa chứng minh được đường output → radio trong Eagle.

## 10. Nghiệm thu cần chứng minh

Phải có một vòng thao tác thực qua UI:

1. Chọn đúng target Eagle/lab và import cấu hình, giữ station không liên quan.
2. Tạo station custom, thêm vài bài từ file bằng picker/drag-drop, preview và đổi thứ tự.
3. Lưu/đóng/mở lại project mà playlist và assignment còn đúng.
4. Tạo ít nhất hai lineup khác nhau cho hai region đã xác minh: có một station chung và một station riêng vùng.
5. Build output đúng codec/config; apply thực sự tới target với manifest/backup.
6. Trong game, chọn station mới, nghe được audio và kiểm tra việc đổi lineup khi qua vùng. Kiểm tra vùng không được gán kênh riêng không có nó. Preview ngoài game không thay phép thử này.
7. Sửa playlist trong UI, build/apply lại; chứng minh thay đổi có hiệu lực sau chu kỳ reload/restart cần thiết và các vùng khác không bị ghi đè sai.
8. Restore/gỡ bằng tool, đối chiếu trạng thái trước cài và các file không liên quan; không phá Aether/NPC/gameplay mods.

Các kiểm tra failure quan trọng: config có repeated keys/field lạ; source mất hoặc decode lỗi; path khoảng trắng/Unicode; playlist rỗng; build cancel/lỗi; target game đang mở; config thay đổi bởi tác vụ khác; apply lỗi giữa chừng; loop/end-of-stream và chuyển vùng; station baseline thiếu audio.

Test phải kiểm tra hành vi và output thật. Không dùng screenshot UI đẹp, unit test frontend, mock backend hoặc file tồn tại làm bằng chứng radio đã phát trong game. Nếu tôi là người thử gameplay, ghi rõ đó là phản hồi của tôi và phạm vi đã thử, không gán thành agent tự quan sát.

## 11. Tài liệu bàn giao

Lưu dưới một nhánh phù hợp, ví dụ:

```text
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\radio-studio
```

Tôi cần:

- Discovery radio/region thực tế, nguồn và những giới hạn đã xác minh.
- Kiến trúc ngắn gọn, vị trí source, cách mở app và dependencies.
- Hướng dẫn người dùng: tạo kênh → thêm nhạc → chọn vùng → build/apply → restore.
- Project/config/output schema và manifest cần để bảo trì hoặc mở rộng sau.
- Bản phục hồi, danh sách file thay đổi và kết quả nghiệm thu UI/backend/game riêng biệt.

Đừng chỉ giao một demo: kết quả mong muốn là lần sau tôi muốn thêm bài, tôi **mở tool, thêm bài vào playlist, chọn build/apply và dùng được radio mới trong game**, với các station đặc thù theo vùng do tôi quản lý.

## 12. Bắt đầu

Đọc tài liệu radio và research engine đã có, xác minh target hiện tại, tìm các gap ảnh hưởng đến adapter và region. Trình bày hướng kỹ thuật/luồng UI ngắn gọn, rồi triển khai theo các bước có thể kiểm chứng. Tập trung làm trọn một đường end-to-end có station chung/riêng vùng trước, sau đó hoàn thiện việc quản lý, sửa và phục hồi cho dùng hằng ngày.
