# GTA SA và Eagle có hỗ trợ hội thoại nhân vật tới đâu?

Ngày khảo sát: **22/10/2026 (Asia/Saigon)**. Target: `Project Eagle/gta sa gameplay-lab`. Phạm vi: tài liệu/API, source công khai, source UI hiện có, inventory và loader log. **Không cài mod, không sửa game, không gọi AI, không khởi động hoặc điều khiển game.**

> **Kế hoạch tích hợp tiếp theo:** [Source audit, lựa chọn adapter/Sidecar và các mốc triển khai](npc-dialogue-integration-plan-2026-10-22.md). Người dùng đã chốt hội thoại bằng **tiếng Anh**; chưa triển khai chuyển toàn bộ data game sang English.

## Kết luận và thay đổi thứ tự công việc

**GTA San Andreas có bộ máy hội thoại có kịch bản, phát lời thoại và hành vi nhân vật. Hội thoại gõ/nói tự do cần lớp nhập liệu và quản lý cuộc trò chuyện do mod bổ sung.** Có dự án mã nguồn mở triển khai lớp này cho SA PC single-player, nên chưa có lý do kỹ thuật để loại bỏ hướng NPC AI. Tuy nhiên, chưa có bằng chứng hội thoại tùy ý chạy hoàn chỉnh trên chính Eagle hiện tại.

Đề xuất trước đã đi quá sớm sang persona/memory. Prerequisite tiếp theo nên là **một cuộc hội thoại trực tiếp với NPC trên gameplay-lab, trả lời bằng câu cố định hoặc backend giả lập, chưa dùng LLM**. Chỉ sau khi chứng minh chọn đúng NPC, nhập được, trả lời được và thoát an toàn mới nối AI.

## 1. Năng lực native và extension

Đối chiếu [Sanny Builder Library của tác giả](https://github.com/sannybuilder/library) với database thực tế `cleo/.config/sa.json` của lab:

| Lớp | Lệnh đã đối chiếu | Vai trò |
| --- | --- | --- |
| SA mặc định | `0717`, `0719`, `09A4` | Thiết lập/finalize hội thoại, câu hỏi và hai câu trả lời với GXT/audio ID |
| SA mặc định | `05C1 TASK_SAY` | Chọn lời thoại từ bảng âm thanh |
| SA mặc định | `0677 TASK_CHAT_WITH_CHAR` | Giao task trò chuyện giữa hai nhân vật |
| CLEO | `0AD2 GET_CHAR_PLAYER_IS_TARGETING` | Lấy handle của ped đang ngắm |
| CLEO text | `0ACD PRINT_STRING_NOW` | Hiện chuỗi tùy ý |
| Audio extension | `0AC1`, `0AC4` | Nạp stream 3D và gắn vị trí vào ped |

Nguồn định nghĩa: [sa.json chính thức](https://raw.githubusercontent.com/sannybuilder/library/master/sa/sa.json). `TASK_SAY` nhận SpeechId, không nhận câu văn để tự đọc thành tiếng. `TASK_CHAT_WITH_CHAR` không tự cung cấp ô nhập hoặc AI. Voice tùy ý cần audio/TTS riêng. Tên opcode không đủ chứng minh khả năng: database đánh dấu `0718` và `071B` là no-op; không xây thiết kế chỉ dựa trên tên hàm.

Các primitive này đủ làm nền cho scripted dialogue/subtitle và tổ chức ped. Cửa sổ chat, văn bản nhiều lượt, chọn nhân vật, gửi/hủy, lưu lịch sử và điều phối backend là phần mod phải tích hợp. Đồng bộ môi/giọng gốc, font tiếng Việt và nhiều nhân vật cùng nói cần xác minh riêng; âm thanh phát tại vị trí ped không tự chứng minh lip-sync.

## 2. Bằng chứng trên gameplay-lab

Codex kiểm trực tiếp source, metadata DLL và phần log liên quan. Luna bổ sung khảo sát inventory/source UI; không decompile `.cs` hoặc binary. Game đang sinh log trong lúc khảo sát; các dòng dưới là **bằng chứng khởi tạo loader ở phiên của người dùng**, không phải bài test hội thoại do agent thực hiện.

| Bằng chứng cục bộ | Kết quả |
| --- | --- |
| `cleo.log:3,10`, lúc 21:16:27 | CLEO **5.0.3**, nhận diện **SA 1.0 US** |
| `cleo.log:55` | `0AD2` đã đăng ký |
| `cleo.log:86,90` | Nạp `SA.Text.cleo`, đăng ký `0ACD` |
| `cleo.log:229,238,241` | Nạp `SA.Audio.cleo`, đăng ký `0AC1` và `0AC4` |
| `cleo.log:713-714` | `cleo/ChatCar.cs` được nạp, đăng ký thread `ChatCar`; chưa phân tích nội dung hay xác nhận hành vi của script |
| `cleo5.dll` FileVersion | **5.0.3**, khớp loader log |
| Kiểm đường dẫn/inventory | Không thấy `cleo_redux.asi`, log Redux, thư mục MoonLoader hoặc `sa.d.ts` ở các vị trí chuẩn đã kiểm |
| `cleo/.config/sa.json` | Có định nghĩa của toàn bộ opcode trong bảng trên; định nghĩa không tương đương runtime test |

Source điện thoại chưa có luồng chat NPC: `EagleCompanion.py:1439-1447,1503-1513` có hotkey/nhập số; `:395-452` lấy player telemetry. `hud.lua:1875-1888` vẽ hướng dẫn/keypad. Đây là các thành phần giao diện có thể tái dùng; chưa chứng minh được text entry tự do và chọn ped cho hội thoại. Kết quả khảo sát không loại trừ mọi hành vi bên trong các script đã biên dịch chưa được phân tích.

Tài liệu `deep-gameplay/06-gameplay-lab-and-poc-guide.md:56` từng gắn nhãn “tương thích cao” cho mod RDR2 talk, nhưng không có test tương ứng trong hồ sơ đã đọc. Nhãn này chỉ được coi là đánh giá sơ bộ; không dùng để tuyên bố đã cài/chạy được. `deep-gameplay/02-eagle-feature-map-and-scm.md:70` mô tả free NPC chat là phần còn thiếu; những nội dung khác trong tài liệu cũ có thể đã được bổ sung ở các phase sau nên vẫn phải đối chiếu source hiện tại.

## 3. Mod và source có thể tham khảo

Các ứng viên dưới đây dành cho SA PC classic single-player; không dùng SA-MP/MTA, GTA V, Android hoặc Definitive Edition làm bằng chứng tương thích cho Eagle.

### SAtella — đúng loại tương tác đang cần kiểm

[Repository tác giả](https://github.com/ne-ogoz/SAtella), source đã kiểm ở commit `1b905248099c661f039fa0233253ef7572f80b4d` (31/05/2026 UTC).

CLEO Redux JS có `findNearestPedHandle`, `getPlayerInput`, `runConversation`, `displayBubble` và `startNpcVoice`: chọn ped gần, nhận chữ, trao đổi với Python và hiển thị/phát lời đáp. README yêu cầu SA 1.0 US, CLEO 5.4.0 và Redux 1.4.3; có backend `stub` để thử offline. Đây là bằng chứng source của lớp hội thoại trong world, chưa phải xác nhận nó chạy trên Eagle.

[JS đã đọc](https://github.com/ne-ogoz/SAtella/blob/1b905248099c661f039fa0233253ef7572f80b4d/cleo/SAtella_sa%5Bfs%5D%5Bmem%5D.js) dùng địa chỉ ped pool và stride cố định, cùng bảng virtual-key cho input. Vì Eagle có PECore/FLA và runtime khác, cần kiểm bridge/keys; input này chưa chứng minh hỗ trợ IME tiếng Việt. GPL-3.0: cần xem nghĩa vụ license nếu tái sử dụng/phân phối code.

### GTA SA AI NPC Companion — hội thoại với ped đã tuyển

[Repository tác giả](https://github.com/bio-colab/gta-sa-ai-companion). Dự án CLEO Redux + Python, MIT; README mô tả recruit một ped rồi nói hoặc gõ trong HUD, có memory và hành vi companion. Luna đã đọc bridge/source liên quan; đây không chỉ là chatbot console. Phạm vi gần với bạn đồng hành, nhưng nhiều cơ chế được gộp chung nên không cần mang toàn bộ vào Eagle. Các cam kết performance/độ ổn định trong README là tuyên bố của tác giả, chưa được kiểm lại.

### Talk with people like in RDR2 — chào hỏi/trêu chọc

[Trang đăng của tác giả ArtemQa146](https://www.gtainside.com/sanandreas/mods/cleo-modifications/188771-talk-with-people-like-in-rdr2): chọn phản ứng tích cực/tiêu cực khi ngắm ped, với các phản ứng mood/hành vi. Mô tả không chứng minh chat gõ tự do hoặc LLM; source và phiên bản CLEO cụ thể chưa được xác minh. Có ích để tham khảo thao tác bắt chuyện, không đủ đáp ứng toàn bộ hội thoại.

### Random Car Talk — lời thoại theo tình huống

[Trang tác giả Junior_Djjr](https://www.mixmods.com.br/2022/06/sa-random-car-talk/) và [source tác giả](https://gist.github.com/JuniorDjjr/b12b2087d3fc11da0795584557bb686b). Dùng các lời thoại có sẵn giữa CJ và hành khách; không phải nhập câu và nhận đáp án. Không tự đồng nhất script `ChatCar.cs` của lab với gói này khi chưa đối chiếu.

## 4. Phần có thể tái dùng và phần phải tích hợp

**Có nền sẵn:** ped handles/tasks, lời thoại thu âm, text rendering, 3D audio qua CLEO và các plugin đã được loader đăng ký. Eagle cũng có sidecar và đường state → HUD. Source mod bên ngoài cung cấp ví dụ cho target selection/input/session/audio.

**Cần ghép hoặc xây:** UI nhập câu, chọn người nói đáng tin cậy, vòng đời session, gửi/nhận dữ liệu bất đồng bộ, phụ đề có speaker rõ, phản hồi lỗi/hủy/timeout. Chưa cần nhân cách, trí nhớ dài hạn hoặc model để kiểm những khối này. Nếu viết CLEO script nhỏ trên runtime hiện có có thể tránh thêm Redux ở bước đầu, nhưng đây là phương án cần thử, chưa phải kết quả đã đạt.

**Cần kiểm riêng cho Eagle:** địa chỉ/pool layout khi có PECore/FLA, hotkey đang bị chiếm, scripted/mission peds, task ownership, NPC streamed out/chết/đi xe, HUD Aether, GXT formatting và font/IME tiếng Việt. Không mặc định cài Redux hoặc nâng CLEO chỉ vì một README yêu cầu; phải khảo sát tương thích và giữ thay đổi tối thiểu.

## 5. Bản thử prerequisite được đề xuất

Không triển khai trong lượt này. Khi được giao làm, đăng ký phạm vi, staging và backup riêng theo shared workflow; giữ khóa ghi lúc tích hợp runtime.

1. Dùng một NPC thử nghiệm không thuộc mission. Đứng gần/ngắm để chọn, hiển thị đúng người đang được chọn; ban đầu tránh sửa trực tiếp task của ped nhiệm vụ.
2. Bấm một phím đã rà xung đột. Mở input trong game; nếu vướng Unicode có thể kiểm đường ASCII trước và ghi rõ hạn chế. Nhập, gửi và hủy đều phải hoạt động, không để phím chat kích hoạt di chuyển/bắn.
3. Nhận một câu trả lời cố định, có tên người nói. Lặp ít nhất hai lượt. Chứng minh cả đường gửi và nhận thật, chưa cần API hay key.
4. Bổ sung trả lời từ backend giả lập ngoài game để kiểm cùng giao thức sẽ nối AI; cố ý trì hoãn/mất backend để kiểm timeout và việc game vẫn điều khiển được.
5. Kiểm đi xa, đổi target, ped mất hiệu lực, đóng/mở lại hội thoại và load game. Nếu cần voice, phát một WAV cố định gắn vào đúng ped rồi kiểm pause/stop/cleanup.

**Điều kiện chuyển sang AI NPC:** demo trên chính gameplay-lab đạt chọn NPC → nhập câu → trả lời → tiếp tục/hủy, không còn kẹt input/task và có đường timeout. Tiếng Việt có dấu, audio và lip-sync có trạng thái nghiệm thu riêng. Sau đó mới thay backend giả bằng LLM; identity bền/save sync vẫn cần trước khi thêm memory/quan hệ.

## Kiểm chứng và bàn giao

- Chỉ đọc file/source/API/log; không gọi endpoint điều khiển game hoặc backend AI.
- Đã xác minh registration của target/text/audio trong loader log, chưa thực thi các lệnh bằng script thử nghiệm.
- Không tải/cài/chạy executable của các mod tham khảo; source được đọc qua HTTPS, không import.
- Không sửa runtime, save, archive hoặc deployment metadata; không giữ game-write.lock.
- Cập nhật báo cáo định hướng trước để ghi rõ prerequisite. Phiếu: `work-items/2026-10-22-codex-npc-dialogue-feasibility.md`.
