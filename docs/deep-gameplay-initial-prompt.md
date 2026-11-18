# Initial prompt: nghiên cứu mod gameplay sâu cho GTA San Andreas / Project Eagle

Tôi muốn bạn làm đối tác nghiên cứu kỹ thuật cho một project mod GTA trên máy của tôi. Mục tiêu của lượt đầu là hiểu đủ sâu bản game thực tế, engine, hệ thống script/plugin và các thay đổi của Project Eagle để lập một kiến trúc có thể triển khai các ý tưởng gameplay bên dưới. Tôi cần nghiên cứu có bằng chứng, chủ động đọc tài nguyên cục bộ, tìm tài liệu trên internet và dùng reverse engineering khi cần.

Đây là prompt bàn giao cập nhật ngày **14/10/2026**, múi giờ **Asia/Saigon**. Các task khác vẫn có thể tiếp tục cập nhật workspace. Hãy kiểm tra lại trạng thái hiện tại trước khi kết luận; phân biệt điều được ghi trong báo cáo cũ với file đang cài và kết quả runtime.

## 1. Tôi đang muốn tạo ra trò chơi gì?

Tôi muốn một thế giới GTA có không khí anime để chơi lâu dài: điều khiển Aether từ Genshin Impact, lái xe đi dạo, nghe các kênh nhạc tôi thích, ngắm phố phường và gặp NPC từ game/anime.

Nhưng tôi muốn đi xa hơn thay skin, xe hoặc radio. Những hướng tôi muốn nghiên cứu gồm:

- **Life sim kiểu The Sims:** có nhà, ngủ, thức dậy, đi làm, nhận lương, đi siêu thị, mua đồ, ăn uống, đổ xăng, tắm rửa và sinh hoạt hằng ngày. Có thể mở rộng sang nhu cầu cơ thể, lịch sinh hoạt, quan hệ với NPC, tài sản, công việc và đời sống xã hội.
- **Kinh tế trong game:** thu nhập, chi tiêu, tài khoản, nghề nghiệp, tài sản; thị trường chứng khoán và crypto mô phỏng, danh mục đầu tư và các sự kiện tác động tới thị trường. Có thể dùng giá giả lập trước rồi nghiên cứu dữ liệu bên ngoài nếu hữu ích.
- **Vé số và sports betting trong game:** mua vé, kỳ quay, kết quả, trả thưởng; cược bóng đá, bóng rổ và các sự kiện thể thao bằng tiền trong game. Nghiên cứu cả kết quả mô phỏng và việc dùng lịch/kết quả ngoài internet làm đầu vào.
- **AI và internet trong game:** NPC có thể trò chuyện, nhớ tương tác, có tính cách/lịch sinh hoạt; AI có thể tạo hội thoại, công việc hoặc sự kiện; có tin tức, thời tiết, dữ liệu thị trường/thể thao hoặc nội dung mạng phù hợp được đưa vào thế giới game.

Đó là các hướng dài hạn, không phải yêu cầu cài tất cả trong một lượt. Tôi muốn hiểu nền tảng, mức khả thi, các phụ thuộc và thứ tự triển khai hợp lý. Giữ trải nghiệm lái xe, dạo phố và sinh hoạt mượt; không để hệ thống mới gây stutter, crash hoặc phá thế giới Eagle.

## 2. Game mục tiêu và môi trường

Workspace Windows/PowerShell:

```text
C:\Users\LENOVO\Desktop\GTA
```

Game mục tiêu:

```text
C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean
```

**Đây là Project Eagle, một bản mod/conversion của GTA San Andreas.** Không coi nó là GTA SA vanilla. Trước đây tôi dùng GTA Underground nhưng đã chuyển hẳn sang Eagle. Underground chỉ còn là nguồn tài nguyên và lịch sử khảo sát, không phải game để tiếp tục thay đổi.

Nhận diện từ các khảo sát và log đã lưu:

- `data\Changelog.txt` ghi **Project Eagle v1.3**, release June 2026.
- `PECore.log` ghi core build **Jun 15 2026** và executable **GTA SA v1.0 HOODLUM**.
- Log nhận diện **ModLoader 0.3.7**, **CLEO 5.0.3**; config RZL Trainer mang nhãn **5.CBT1.3**.
- Trong root có `gta_sa.exe`, `gta_pe.exe`, `PECore.asi`, `$fastman92limitAdjuster.asi`, `CLEO.asi`, `modloader.asi`, `Modloader_Patch.asi`, `SilentPatchSA.asi`, `skygfx.asi`, `SanViveLuaHudSA.asi` và các plugin khác. Hãy lập lại danh mục/version/hash cần thiết cho nghiên cứu, không coi tên file là bằng chứng về API hoặc hành vi.
- Đây là môi trường GTA SA PC 32-bit theo khảo sát trước; hãy xác nhận kiến trúc từng target/provider khi làm binary analysis.

Tên thư mục có chữ `clean` là tên bộ cài ban đầu. **Trạng thái hiện nay đã có Aether và bộ thử skin NPC**, không còn là một baseline Eagle nguyên trạng. Các thành phần vốn đi kèm distribution phải được phân biệt với các mod chúng tôi đã thêm.

## 3. Những gì chúng tôi đã làm và cần giữ nguyên

### Task 1: Aether làm nhân vật chính — đã kết thúc

- Đã cài Aether v3.0 của FadXploit, biến thể **Shadeless DFF & Smaller TXD (for non-ENB)**.
- Hai file: `modloader\RZL-Skin\AETHER.dff` và `AETHER.txd`.
- Cách dùng: **F2 → Player Options → Change Player → ModLoader Actors → AETHER**.
- Tôi đã báo tự thử cách F2 hoạt động ổn. Điều này không tương đương nghiệm thu từng animation, save/load hoặc cutscene.
- Kiểm tra tĩnh cho thấy skeleton cơ sở của Aether khớp player Eagle; tóc/vạt áo không có hệ physics riêng được xác nhận, và biểu cảm mặt CJ chưa được hỗ trợ đầy đủ theo kiểm tra weights. Đừng mô tả nó là đã support mọi animation/chức năng chỉ vì bone table khớp.
- Có thử nghiệm tự nạp Aether lúc bắt đầu/load game, tôi yêu cầu gỡ vì có vẻ không hoạt động. Thử nghiệm đã được gỡ và `default.dat` được phục hồi; **không cài lại cơ chế tự nạp đó** trong tác vụ nghiên cứu này.

### Task 2: ped ID, phân bố NPC và thay skin — đang tiếp tục

- Đã có catalog ped và inventory population từ các manifest/IDE/IMG/file dữ liệu Eagle. Một snapshot ghi 1.687 ped records, 186 IDE files được khai báo và 61 archive được parse. Đọc summary trước, không dump JSON nhiều MB vào context.
- Sau giai đoạn lập kế hoạch, task này đã cài thử ba model law enforcement bằng skin nhẹ từ bộ Underground sẵn có: **280/lapd1**, **285/swat**, **287/army**.
- Theo biên bản cài: thay đúng sáu member DFF/TXD trong `S&S\Cdimages\default\COMPONENTPEDS.img`, có backup và đã thử phục hồi/cài lại. Không sửa AI, pedtype, wanted logic hoặc population chỉ để thay appearance.
- Bản ghi phản hồi người dùng ngày 14/10/2026 nói cảnh sát và SWAT tại Los Santos đã trigger và skin hoạt động ổn. Quân đội 287 chưa có kết quả runtime được ghi trong bản đó; chưa có benchmark FPS hoặc nghiệm thu mọi animation.
- Task 2 vẫn đang truy vết nhóm ped/vùng và lựa chọn NPC. Không tranh chấp file hoặc viết đè kết quả của nó.
- Điểm kỹ thuật cần giữ: khảo sát phát hiện plugin stream của ModLoader bị tắt. Vì thế **ModLoader có mặt không chứng minh mọi loại streamed asset replacement đều hoạt động**. Aether qua RZL và bộ NPC qua archive là hai đường đã dùng khác nhau; kiểm tra trạng thái mới nhất.

### Radio — mới khảo sát

- PECore có `RadioEx`; `data\radio.dat` khai báo station theo region với dạng `Station=Name,AudioFile,SpriteName,Duration`.
- Snapshot trước ghi 7 vùng/63 station được cấu hình. Chưa được coi là 63 kênh phát thành công.
- Khảo sát chưa thấy audio ở các đường `audio\PE\RADIO` được tham chiếu. Chưa giải thích được gói audio riêng hay layout/loader khác; kiểm tra lại nếu nghiên cứu liên quan.
- `C:\Users\LENOVO\Documents\GTA PE User Files\User Tracks` được quan sát là thư mục User Tracks của Eagle và khi khảo sát còn trống.

## 4. Tài nguyên và tài liệu sẵn có

Đọc quy định project trước:

```text
C:\Users\LENOVO\Desktop\GTA\AGENTS.md
```

Thư mục báo cáo:

```text
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle
```

Ưu tiên đọc:

- `README.md`: mục lục và trạng thái tổng hợp; có thể chứa đoạn lịch sử chưa cập nhật đồng bộ, cần đối chiếu tài liệu cụ thể.
- `installation.md`: build, core/plugin, loader và manifest.
- `cj-aether.md`, `aether-autoload-rollback.md`: trạng thái Aether và rollback.
- `skins.md`, `npc-ped-plan.md`: khảo sát skin, ped và phân bố.
- `npc-law-enforcement-installed.md`: thay đổi archive, backup, phạm vi kiểm chứng NPC.
- `radio.md`: RadioEx, User Tracks và những phần chưa xác minh.
- `teleport-guide.md`: thao tác dịch chuyển phục vụ khảo sát trong game.

Dữ liệu lớn dưới `docs\project-eagle\evidence`:

- `ped-catalog-summary.md` / `ped-catalog.json`.
- `population-summary.md` / `population-catalog.json`.
- `npc-replacement-disposition.md` / `.json`.
- `npc-priority-regions.md` / `.json`.
- `npc-group-opportunity.md` / `.json`.
- `user-runtime-observations.json`: phản hồi người dùng, cần tách khỏi agent tự quan sát.
- Các audit rig/manifest/cài đặt của bộ NPC.

Ngoài game có các thư mục **`staging\project-eagle`** và **`backups\project-eagle`** để giữ asset, công cụ kiểm tra, candidate và bản phục hồi. Hãy dùng chúng làm bằng chứng/tham khảo, không tự chạy script cài/gỡ.

Nguồn Underground còn trên máy:

```text
C:\Users\LENOVO\Desktop\GTA\R.G. Catalyst\Grand Theft Auto - San Andreas
C:\Users\LENOVO\Desktop\GTA\[SA-MP.VN] GTA Online
```

Trong đó có `gtaug.rar`, bộ 1.721 cặp DFF/TXD và các tool IMG/SAAT/Ped Editor. Lịch sử nằm ở `docs\gta-underground-modding.md` và `docs\evidence`. Đây không phải baseline code của Eagle. Không suy ra compatibility, ID, offset hoặc cách cài của Eagle từ Underground.

Các điểm bắt đầu web đã dùng, cần kiểm tra lại khi nghiên cứu:

- [Project Eagle](https://www.projecteaglemod.games/).
- [PE 1.3 changelog](https://www.projecteaglemod.games/changelog/pe-1.3.0).
- [Releases](https://www.projecteaglemod.games/releases).
- [FAQ](https://www.projecteaglemod.games/world/faq).
- [Bài RadioEx](https://www.projecteaglemod.games/news/6).
- Discord channel đã được nhắc: `https://discord.com/channels/1335713270232907776/1335713789856972841`.

Tôi có thể đang mở Discord trong Codex browser, nhưng các phiên trước không phải lúc nào cũng nhìn thấy tab qua tools. Hãy kiểm tra khả năng truy cập thực tế. Không nói đã đọc Discord nếu chưa đọc được. Chỉ đọc hướng dẫn; không gửi tin nhắn, join/react hoặc đăng bài.

Nếu bạn chỉ là model chat bên ngoài và **không truy cập được ổ đĩa/tools của tôi**, nói rõ ngay. Các path trên là vị trí để tôi cung cấp dữ liệu, không phải tài liệu bạn đã đọc. Vẫn tiến hành phần research web độc lập; yêu cầu một bộ tài liệu/manifest nhỏ thật sự cần thiết cho bước tiếp theo, thay vì yêu cầu toàn bộ game hoặc giả vờ đã inspect binary.

## 5. Tôi muốn bạn hiểu engine và các thay đổi Eagle tới mức nào?

Hãy dựng bản đồ kiến trúc của **bộ game đang cài**, gồm:

- Executable game, PECore và các plugin; cách chúng được nạp và phụ thuộc nhau.
- Script/SCM/CLEO, opcode, event/hook, vòng cập nhật và các điểm có thể thêm logic gameplay.
- Player/ped/vehicle tasks, interactions, world clock, weather, zone/region, interiors, streaming và model variations.
- Tiền, inventory/item, shop, job/mission, wanted/law enforcement và các state liên quan nếu game/extension có chúng.
- Save/load, khởi tạo phiên game, chuyển map/interior, reset/restart và nơi lưu state do mod thêm.
- UI/HUD/menu/input/audio và khả năng hiển thị nội dung động.
- Các giới hạn tài nguyên, thread, performance và version compatibility có ảnh hưởng đến mod sâu.

Không cần giải nghĩa toàn bộ engine trước khi tạo ra điều hữu ích. Bắt đầu từ entry point và các tính năng phục vụ mục tiêu của tôi; đi theo các luồng cụ thể tới state và kết quả. Ví dụ: bắt đầu/load game → player state; tương tác một địa điểm → giao dịch tiền; world clock → lịch làm việc; vào xe → fuel state; event bên ngoài → UI/event trong game.

Về câu hỏi “Project Eagle đã change gì trong source”: **trước hết xác định source nào thật sự có**. Tôi chưa cung cấp source đầy đủ của GTA SA hoặc PECore, và không biết các repo công khai có khớp build này không.

- Nếu có source, ghi repo/tag/commit, dependencies và căn cứ liên hệ nó với binary cục bộ.
- Nếu chỉ có binary/config/script, dùng chúng và reverse engineering để dựng feature map/pseudocode có giới hạn. Không gọi đó là source gốc hoặc diff source đầy đủ.
- So sánh các lớp: GTA SA nền → các thành phần Eagle/S&S → plugin bên thứ ba → mod chúng tôi thêm. Không quy mọi khác biệt cho PECore.
- Chỉ dùng baseline đã xác định identity/version. Bản Underground cũ hoặc `gta orgi.rar` chưa được xác nhận không tự trở thành baseline GTA SA phù hợp.
- Phân biệt thay đổi resource/data, script, native hook/patch và logic mới. Không suy ra tính năng chỉ từ string, tên section INI hoặc changelog.

## 6. Học cách cộng đồng thực sự mod game

Chủ động tìm nguồn chính thức của công cụ, source repo, tài liệu tác giả và các mod liên quan. Các chủ đề để tìm gồm CLEO/Sanny Builder, plugin-sdk, ASI/hooking, ModLoader, fastman92 Limit Adjuster, các dự án phân tích/reimplementation GTA SA nếu phù hợp, và tài liệu Eagle/S&S/PECore.

Đây là các hướng tìm kiếm, không phải tuyên bố mọi công cụ đều tương thích với Eagle hiện tại. Lua trong tên một plugin HUD cũng không chứng minh có Lua API gameplay tổng quát.

Tìm các ví dụ có thể học được cơ chế: needs/life simulation, houses/interiors, jobs, fuel, shops/inventory, economy/banking, mini-games, persistence, UI, NPC tasks/dialogue, networking/AI bridge. Với mỗi ví dụ đáng dùng:

1. Xác định nó chạy trên phiên bản nào và thực sự làm gì.
2. Tìm source/tài liệu/manifest để hiểu cơ chế, thay vì chỉ dựa vào video hoặc lời quảng cáo.
3. Chỉ ra phần nào có thể tái sử dụng, phần nào cần port/viết lại cho Eagle và phần nào chưa xác minh.
4. Ghi nguồn, version, phụ thuộc và các điểm có thể đụng core/script/loader hiện có.

Tôi cần kiến thức để xây dựng, không chỉ một danh sách mod để tải. Nếu source không công khai, ghi rõ những gì bạn quan sát được và giới hạn; reverse engineer target có liên quan khi nó giúp trả lời câu hỏi cụ thể.

## 7. Reverse Engineer Anything

Máy có skill tại:

```text
C:\Users\LENOVO\.agents\skills\reverse-engineer-anything\SKILL.md
```

Hãy đọc skill khi áp dụng. Skill được cài không có nghĩa MCP, CLI, Ghidra/IDA hoặc provider runtime đã sẵn sàng. Trong phiên điều phối ban đầu chưa có REA MCP tools và shell chưa tìm thấy `rea` trên PATH; đó là kết quả cũ, cần kiểm tra khả năng hiện tại nếu thực sự cần REA.

- Khi có tools, dùng schema/catalog thật của server; chọn target đúng path/identity và kiểm tra provider có hỗ trợ binary x86 trên host này không.
- Với source repository đầy đủ, phân tích source thông thường trước. Với shipped binary, script đóng gói hoặc hành vi chưa được source xác lập, dùng REA khi phù hợp.
- Native targets có thể là executable và ASI/DLL liên quan, nhưng chọn theo câu hỏi cụ thể, không mở mọi binary để decompile hàng loạt.
- Giữ Evidence ID khi REA cung cấp; nếu dùng shell/parser thông thường, ghi đó là bằng chứng shell/parser, không gắn nhãn REA giả.
- Tách static analysis, suy luận và runtime observation. Pseudocode/strings/graph không chứng minh code đã thực thi.
- Reuse session/evidence phù hợp; giữ summary/index trước rồi đọc từng nhánh. Không dump graph/JSON lớn hoặc phân tích lặp cùng target vì preview bị cắt.
- Nếu tool/provider thiếu, chẩn đoán blocker cụ thể và tiếp tục phần khảo sát làm được. Không tự nâng cấp toolchain hoặc sửa cấu hình Codex diện rộng. Nếu cần sửa setup, chuẩn bị phương án cụ thể với path và backup trong phạm vi được cho phép.
- Với runtime, xác định probe và target/lifecycle rõ trước; tôn trọng công cụ thực tế, không điều khiển game tiếp khi tôi dừng thao tác. Không overwrite save đang chơi.

Không để việc setup REA trở thành toàn bộ project. Mỗi lần reverse engineering cần trả lời một câu hỏi kỹ thuật giúp chọn kiến trúc hoặc xác nhận cơ chế mod.

## 8. Các câu hỏi kiến trúc cần trả lời

Đừng chọn CLEO, ASI/C++, Lua, overlay hoặc backend chỉ theo sở thích. So sánh theo khả năng và bằng chứng trong build này, rồi đề xuất một cấu trúc dễ mở rộng:

### Life sim và world state

Logic nào có thể làm ở script, logic nào cần native hook/plugin? Có thể theo dõi clock, needs, jobs, houses, shop transactions và NPC schedules qua API/event nào? State nào cần sống qua save/load hoặc qua việc ped/interior bị unload? Cách mô phỏng ngoài vùng streaming để không giữ mọi NPC active là gì? Xử lý mission/player state đặc biệt ra sao?

### Kinh tế và mini-games

Phân tách sổ giao dịch, balance, inventory/assets, lịch sự kiện và UI như thế nào? State tiền/tài sản của hệ thống mới liên hệ với tiền game thế nào? Cần model thị trường giả lập nào cho bản đầu? Vé số/cược giải quyết kết quả, lịch và trả thưởng ra sao khi save/load, tua thời gian, offline hoặc dữ liệu ngoài cập nhật trễ? Không mặc định gắn API dữ liệu thật trước khi cần.

### AI và internet

Nghiên cứu cả AI local và dịch vụ ngoài, với khả năng, latency, chi phí và tài nguyên được kiểm tra từ nguồn phù hợp. AI ở mức hội thoại khác với AI được phép tác động gameplay; đề xuất ranh giới rõ.

So sánh tích hợp trực tiếp trong plugin với **một chương trình companion/sidecar chạy ngoài game**. Đây là phương án cần đánh giá, không phải kiến trúc đã chốt. Cần làm rõ:

- Cách gửi snapshot/event và nhận kết quả: IPC/local HTTP/socket hay cơ chế nào thật sự dùng được.
- Cách đưa kết quả trở lại thread/vòng cập nhật phù hợp, có queue/time budget; tránh gọi mạng hoặc inference đồng bộ trong game tick.
- Timeout, retry, offline/cache, pending/stale response và fallback để game tiếp tục chơi bình thường.
- Context NPC, memory, giới hạn số NPC gọi AI và mô phỏng ngoài màn hình.
- AI chỉ đề xuất hành động được game adapter kiểm tra và cho phép; không thực thi trực tiếp nội dung lấy từ web hoặc câu trả lời model thành lệnh/script.
- Lưu cấu hình/API key ngoài asset phân phối và tránh lộ qua log; không tự tạo tài khoản hoặc phát sinh chi phí khi chưa được yêu cầu.
- Tách lỗi/crash của dịch vụ ngoài khỏi sự ổn định của game; tương thích restart/save/load và version protocol.

### Tính tương thích và performance

Tìm các điểm đụng PECore, FLA, CLEO, trainer, HUD và map/zone logic. Không dùng địa chỉ memory hoặc struct layout của SA vanilla mà chưa xác minh với executable/plugin đang chạy. Có kế hoạch đo frame time, stutter, streaming pressure và tải CPU/RAM phù hợp; số liệu chưa đo phải để là chưa đo.

## 9. Phạm vi lượt nghiên cứu đầu tiên

Được đọc tài nguyên game/báo cáo, khảo sát web, dùng công cụ phân tích phù hợp và viết script phân tích chỉ đọc/tài liệu vào thư mục nghiên cứu riêng. Giữ nguyên game và save đang dùng, Aether, bộ NPC, trainer và radio. Không cài gameplay mod, thay binary/archive/script hoặc chạy các script install/rollback trong lượt đầu.

Nếu cần runtime để trả lời một gap, mô tả phép thử, dữ liệu quan sát và ảnh hưởng trước khi làm trong phạm vi được phép; ưu tiên quan sát không ghi state và môi trường test riêng. Task 2 đang chạy: tránh tranh chấp target, file hoặc session phân tích.

Hội thoại điều phối của project ưu tiên dùng **GPT Luna cho tìm kiếm rộng/khảo sát nặng**, nếu nền tảng của bạn có subagent/model selection. Model chính giữ việc xác định giả thuyết, đọc code khó, reverse engineering cần suy luận và kiểm tra/tổng hợp kết quả. Nếu nền tảng không hỗ trợ delegation, nói rõ rồi làm với khả năng có sẵn; không giả vờ đã có agent phụ.

Chỉ hỏi khi một thiếu hụt thật sự ngăn bước tiếp theo hoặc cần quyết định ngoài phạm vi. Vẫn tiến hành các phần độc lập đang làm được. Giữ cập nhật ngắn về kết luận/gap, không kể lại mọi lệnh đã chạy.

## 10. Kết quả tôi cần nhận

Nếu có filesystem, lưu kiến thức có thể dùng lại dưới:

```text
C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\deep-gameplay
```

Nếu không có filesystem, trả tài liệu tương đương trong chat. Tôi cần:

1. **Identity và kiến trúc bản cài:** phiên bản/hash cần thiết, cây thành phần và luồng script/native/data/runtime. Có sơ đồ khi nó giúp giải thích.
2. **Feature map của Eagle:** tính năng nào có sẵn, thành phần nào thực hiện, nguồn bằng chứng, khác biệt với baseline phù hợp và những gì chưa biết vì thiếu source/version match.
3. **Bản đồ điểm mở rộng:** API/opcode/event/hook/data/UI/persistence có thể dùng cho từng hướng; status support thực tế và rủi ro tương thích.
4. **Bảng mod tham khảo:** ví dụ cộng đồng đáng học, cơ chế, version, source và khả năng port/reuse; không chỉ link tải.
5. **Đánh giá khả thi các nhóm life sim, kinh tế, vé số/sports betting, AI/internet:** cái làm được bằng dữ liệu/script hiện có, cái cần plugin/companion, cái còn thiếu bằng chứng hoặc quá sâu so với lợi ích.
6. **Kiến trúc đề xuất:** module boundaries, state/persistence, event flow, UI, game adapter và integration ngoài nếu có; giải thích tradeoff dựa trên bằng chứng.
7. **Roadmap theo các lát cắt nhỏ có thể chơi được:** phụ thuộc, điều kiện nghiệm thu và lựa chọn ưu tiên. Chuẩn bị kế hoạch một PoC cụ thể để tôi chọn, thay vì cài toàn bộ hệ thống. Ví dụ một vòng sinh hoạt/công việc đơn giản hoặc một tích hợp AI hẹp; lựa chọn phải dựa trên kết quả khảo sát.
8. **Evidence ledger và gap list:** mỗi kết luận quan trọng gắn path/dòng hoặc symbol/address/hash/Evidence ID/URL; phân biệt source, static binary, config, runtime do agent quan sát, phản hồi người dùng và giả thuyết. Ghi phạm vi tìm kiếm để lần sau không lặp.

Đừng viết roadmap chỉ dựa vào kiến thức chung về GTA modding. Tôi cần nó bám vào **Project Eagle thực tế trên máy**, các khả năng đã xác lập và những phép thử sẽ giải quyết các gap còn lại.

## 11. Hãy bắt đầu như sau

Trước tiên xác định bạn có những quyền truy cập/tools nào: filesystem, web, browser/Discord, subagents, REA/providers và runtime. Sau đó đọc các summary/tài liệu nền, kiểm tra identity tối thiểu và chia các câu hỏi nghiên cứu theo phụ thuộc.

Cho tôi biết hướng nghiên cứu ngắn gọn rồi bắt đầu thực hiện các phần được phép, không dừng ở lời hứa hoặc danh sách công nghệ. Ưu tiên câu hỏi giúp chọn điểm mở rộng và một PoC khả thi; mở rộng điều tra theo gap thật. Ở cuối lượt đầu, bàn giao kết quả, mức chắc chắn, nguồn và phương án triển khai cụ thể để chúng ta quyết định bước tiếp theo.
