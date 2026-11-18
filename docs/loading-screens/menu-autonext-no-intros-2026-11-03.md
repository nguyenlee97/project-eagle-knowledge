# Menu tự đổi bài và bỏ hai intro video — 03/11/2026

**Nghiệm thu03/11:** người dùng báo “mọi thứ đã work hoàn hảo rồi”; task hoàn tất. [State/source/cleanup](../presentation-current-state.md). Các mục kiểm tra bên dưới là bằng chứng/kịch bản lưu lại.

Đã cài vào `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`. Chỉ thay `WibuMenu.asi` và cập nhật record/hash trong install-state thuộc Wibu. **Kiểm offline đạt; người dùng đã xác nhận runtime PASS03/11/2026. Agent không tự mở game.**

## Hành vi

- Nhạc menu phát hết bài thì chọn ngẫu nhiên một bài khác trong playlist hiện có, không lặp ngay bài vừa nghe khi có từ hai bài hợp lệ. Với một bài thì phát lại bài đó. F3/F4 vẫn đổi thủ công; tự chuyển bài không ghi lại `default_track`. Random khi mở game,7 bài,volume0.25 và mọi thiết lập INI giữ nguyên.
- Hai trạng thái Logo/Title movie được chuyển vào frontend-loading trước khi gọi trình phát. Giữ Project Wibu splash và luồng loading/menu. Không tạo video mới, không xóa/đổi tên hai MPEG và không sửa executable/PECore trên đĩa. Các clip0.2s cũ vẫn còn nhưng đường khởi động được bypass khi guard tương thích đạt.
- Giữ toàn bộ178TXD (89loading/89menu), timer2s/4s, F6, favorite, nhạc pause/main menu, private BASS và radio.

## Cơ chế và bằng chứng

Audio bỏ cờ loop của stream, polling `BASS_ChannelIsActive` trên thread menu. Chỉ trạng thái stopped hợp lệ mới chuyển bài; playing/stalled/paused giữ nguyên. Handle lỗi được dọn và retry, không quay playlist vì lỗi query. Stop/free stream cũ trước tạo stream mới; không tạo audio callback chạy engine. [BASS ChannelIsActive](https://www.un4seen.com/doc/bass/BASS_ChannelIsActive.html) phân biệt trạng thái và mã lỗi; [StreamCreateFile](https://www.un4seen.com/doc/bass/BASS_StreamCreateFile.html) mô tả cờ loop. DLL private thực tế có export cần dùng.

Startup dùng hai entry của switch table trong bộ nhớ process (`0x748EF8`, entry1 và3). Synchronous bootstrap chạy đầu `DllMain`, kiểm PE identity, state0, dispatcher/case signatures và đủ10 pointer gốc. CAS thay riêng hai aligned dword, giữ entry2 và các entry khác; mở quyền ghi tạm nhưng giữ execute vì table cùng page với code, trả lại protection và rollback pointer của mình nếu lỗi/race. Naked jump stub chỉ MOV state5/EAX rồi tail-jump handler5 `0x748C0D`, giữ stack/flags/EBX/EDI. Handler gốc null-check video graph rồi tiếp tục frontend initialization. Đối chiếu [gta-reversed WinMain](https://github.com/gta-reversed/gta-reversed/blob/master/source/app/platform/win/WinMain.cpp) và mã máy cả hai executable lab. Không dùng polling-thread để sửa game state hoặc hook giữa hàm không rõ ABI.

Điều kiện nạp sớm được kiểm ở loader thực tế `vorbisFile.dll`: loader sửa entrypoint để hook GetStartupInfo; wrapper gọi LoadPlugins đồng bộ rồi trả về CRT startup. Game gọi GetStartupInfoA tại0x8246C6 trước WinMain0x748710 ở0x8246EC. Không phải worker late-loader. [Evidence local](../../../staging/project-eagle/menu-autonext-no-intros-20261103/qa/loader-entry-evidence.json), đối chiếu [Silent ASI loader source](https://github.com/GTAmodding/ASI-Loader/blob/master/vorbisFile.cpp). Evidence là pefile/Capstone offline, không có target process chạy. Bootstrap không gọi engine/COM/LoadLibrary/logging; init thread sau đó pin module và khởi tạo các hook cũ.

## Build, cài và kiểm tra

Nguồn mới nhất: `staging/project-eagle/menu-autonext-no-intros-20261103/plugin/src/wibu_menu.cpp`, cùng hai helper header. ASI SHA256 `550f9508855d845ef850e8e78a9da1840d8ed72dd192a0a2f0f57fb63ae459af`.

- [Build QA](../../../staging/project-eagle/menu-autonext-no-intros-20261103/qa/plugin-build.json): cả hai exe/hash/PE/table/case/loading/menu signatures đạt; naked stub đúng machine code, BASS export có, x86PE32 chỉ import kernel32/user32; không có loop flag.
- Native `audio_probe` gọi hàm thật với stub BASS: EOF/playing/stalled/paused/device-pause/mute/disabled/invalid-handle/empty/single playlist, không lặp ngay và cờ stream0. Exit0; fixture INI không đổi.
- Native `intro_probe` gọi helper thật với fake VirtualProtect: đủ10 mismatches, thành công chỉ đổi slot1/3, lỗi protect đầu/cuối, foreign slot race, null/unaligned. Exit0; không chạy game hoặc ghi table game trong probe.
- [Live QA](../../../staging/project-eagle/menu-autonext-no-intros-20261103/qa/live-install.json): plugin/state hash khớp,228file bảo vệ nguyên hash gồm178TXD, toàn INI, hai movie, loader, exe, PECore, audio. Radio Studio vẫn nhận persistence/random và7bài. Khóa ghi chung đã nhả.
- [Transaction](../../../staging/project-eagle/menu-autonext-no-intros-20261103/plugin-update.json) ghi baseline/hash/protected/after-state; before-images tại `runtime-before/`. Rollback preflight đạt, rollback thực tế chưa chạy.

Log lúc mở game nên có `startup video states bypassed before decoder`; nếu guard không đạt sẽ ghi `startup video bypass inactive (identity/state/table guard)` và giữ luồng gốc. Người dùng đã xác nhận toàn bộ hoạt động hoàn hảo; log live có bootstrap bypass active và EOF đổi bài.

## Phục hồi

Thoát game, chạy từ workspace:

```powershell
C:/Python310/python.exe -X utf8 staging/project-eagle/menu-autonext-no-intros-20261103/deploy_plugin.py rollback-preflight
C:/Python310/python.exe -X utf8 staging/project-eagle/menu-autonext-no-intros-20261103/deploy_plugin.py rollback
```

Chỉ phục hồi plugin/state về bản178ảnh ngay trước update, không gỡ ảnh hoặc thay playlist. Guard từ chối nếu state/plugin thay đổi sau cài. Muốn rollback cả thư viện03/11 phải rollback update này trước, rồi mới dùng transaction art-library; không chạy lại rollback clean/merge.

Người dùng test: mở gameplay-lab xem vào thẳng Project Wibu thay vì hai movie; ở menu nghe hết một bài để kiểm bài mới, thử F3/F4 và pause/resume. Không thêm batch tạo hình.
