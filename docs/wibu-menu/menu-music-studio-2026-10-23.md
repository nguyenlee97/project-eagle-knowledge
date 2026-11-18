# Menu Music trong Radio Studio — 23/10/2026

**Cập nhật:** đã có option random bài mở đầu mỗi lần launch và đang bật cho người dùng, giữ playlist 7 bài. [Hành vi, hash và kiểm tra bản mới](random-music-2026-10-23.md).

**Đã cài vào gameplay-lab và lưu playlist thật, ngày 23/10/2026.** Người dùng báo game đã đóng và không lưu được; đã cài candidate, bật nút Save và lưu đúng 7 bài đang soạn, chọn **Clock Towers Beneath the Sea (Dream World)** làm bài mở đầu. Chưa chạy GTA để nghiệm thu. Target duy nhất là `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`; không thay bản clean lưu trữ.

## Người dùng có thể làm gì

Radio Studio có tab **Menu Music** tại `http://127.0.0.1:8790`. Plugin mới đã cài; nút Save hiện được bật khi game đóng:

1. Tích bài trong kho D:\Music rồi bấm **+ Menu Music**, hoặc dùng **Add files** trong tab Menu Music.
2. Dùng ↑/↓ để đổi thứ tự, **Remove** để bỏ bài khỏi danh sách, ▶ để nghe thử.
3. Tích radio button ở cột **Opening track** để chọn bài phát đầu tiên khi mở game. Có chỉnh enable/mute/volume riêng.
4. Thoát GTA rồi bấm **Save menu music to game**. Không cần Build Radio, không đổi các station RadioEx.

Hỗ trợ tối đa **64 bài**. MP3 / OGG Vorbis / WAV có codec phù hợp được chép trực tiếp; M4A, FLAC, AAC, Opus, WMA và codec chưa được runtime nhận sẽ được FFmpeg chuyển thành MP3 trước khi cài. File gốc giữ nguyên. Công cụ chép bài vào thư mục audio menu riêng bằng tên ASCII theo hash, tránh đường dẫn có Unicode mà plugin ANSI không đọc được. Các file audio cũ không bị xóa, để giữ khả năng phục hồi. Cache chuyển đổi có hash nguồn/kết quả và probe codec; lỗi chuyển đổi xảy ra trước khi ghi runtime.

Trong game, **F6 → F3/F4** đổi bài và tự lưu bài mới làm mặc định cho lần khởi động sau. Mỗi bài phát lặp cho đến khi đổi bài; đây chưa phải chế độ tự chuyển bài khi hết track. Bài mặc định được lưu bằng đường dẫn `audio.default_track`, nên đổi thứ tự playlist vẫn giữ đúng bài, thay vì chỉ ghi index.

## Nguyên nhân và thay đổi

Plugin cũ có `gTrackIndex = 0` khi load config, và `ChangeTrack` không ghi cấu hình; vì vậy F3/F4 chỉ có tác dụng trong phiên. Đã tách loader audio, đọc `default_track` với fallback track0 cho config cũ, tăng giới hạn lên 64 và tạo track10..track63 bằng số đầy đủ. ChangeTrack lưu đường dẫn hiện tại qua API INI đang dùng.

Source native chuẩn: `staging/project-eagle/wibu-menu/plugin/src/wibu_menu.cpp`. Candidate được build riêng tại `staging/project-eagle/menu-music-studio-20261023/plugin/build/WibuMenu.asi`; không chép đè gói build/manifest cũ dành cho clean.

Radio Studio: mới `core/menu_music.py` và `static/menu-music.js`; thêm GET/POST `/api/menu-music` và tab/nút nối từ kho nhạc. Backend kiểm đúng hai exe lab và ownership/hash ASI, từ chối plugin cũ, config stale, game chạy, khóa ghi bị chiếm hoặc reparse trên đường ghi. Chỉ sửa block audio INI; giữ comments, favorite, các nhân vật và provenance merge.

Mỗi lần lưu dùng khóa ghi chung, kiểm lại hash ngay trước thay file, backup config/state và ghi transaction tại `tools/eagle-radio-studio/data/menu_music/history/<id>/`. Metadata title lưu trong install-state riêng; không sửa project radio. Khi lỗi, chỉ phục hồi file có hash chứng minh thuộc transaction; nếu có thay đổi ngoài dự kiến thì giữ audio được tham chiếu và ghi `partial_rollback`, không xóa mù.

## Kết quả kiểm tra

- x86 build thành công; verifier kiểm đúng cả hai executable lab và ABI helper hiện tại.
- Native harness gọi chính `LoadAudioConfig` / `ChangeTrack`: **13 assertion đạt**, gồm lưu/đọc lại qua lần mở, playlist trên 8 bài, track63, default thiếu, reorder giữ bài, favorite không đổi. Harness chạy muted, không gọi game/BASS.
- Backend: **12 pytest đạt** trên game giả, gồm save/reopen, title, provenance, stale config/state, old plugin, chuyển đổi M4A/Opus, nguồn giữ nguyên, game/lock, lỗi giữa chừng và bảo toàn dữ liệu concurrent.
- Cài/rollback plugin: **7 pytest đạt** trên thư mục tạm. Hai bài lifecycle Radio Studio có sẵn cũng đạt. Không chạy test cũ ghi vào lab thật.
- Python compile, Node syntax, API GET và kiểm tra tab trực tiếp đều đạt. Giao diện có cảnh báo plugin chưa cập nhật, nút Save khóa đúng.
- Đã kiểm 39 file owned sau cài và lưu playlist: toàn bộ khớp hash, giữ provenance merge và 6 file core/exe/radio được bảo vệ. Khóa ghi đã trả. Playlist có 7 bài, bài mở đầu đúng lựa chọn và hash các file nguồn không đổi. `Pluie sur la ville.m4a` đã được chuyển sang MP3. Chưa nghiệm thu trong GTA.

Bằng chứng: `staging/project-eagle/menu-music-studio-20261023/qa/verification.json`, `qa/native-config/`, `qa/test_plugin_deploy.py`, `qa/menu-music-preview.png`.

## Lịch sử tích hợp và phục hồi

Plugin transaction đã có `status=installed` trong `staging/project-eagle/menu-music-studio-20261023/plugin-update.json`; before-images của ASI/state ở `runtime-before/`. Playlist transaction: `tools/eagle-radio-studio/data/menu_music/history/20261022T191843-5be165d0` (ID theo UTC), gồm config/state before-image, 7 asset và hash sau lưu. Draft gốc trước làm mới UI nằm tại `qa/user-draft.json`.

Giao diện thêm **Check game status** và tự kiểm lại quyền lưu khi quay về tab, giữ danh sách đang soạn thay vì bắt reload mất draft. Lượt cài này giữ nguyên lựa chọn 7 bài trước khi tải lại giao diện. API đã đọc lại đúng playlist/default sau lưu.

Candidate ASI SHA-256: `c2ed6161289a23f0da0a1af4d2ae12c3f547215822a0b0b9ef1f17f55a4f35b0`.
Baseline ASI lab: `e88457bba9fe2e71ae361bc99903c9225e2524759f0c6da49457427ef17fb0d6`.

Sau khi GTA đã đóng và người dùng muốn cài, đọc lại phiếu/ownership rồi tạo plan mới từ state hiện tại:

```powershell
C:\Python310\python.exe staging\project-eagle\menu-music-studio-20261023\deploy_plugin.py prepare
C:\Python310\python.exe staging\project-eagle\menu-music-studio-20261023\deploy_plugin.py preflight
C:\Python310\python.exe staging\project-eagle\menu-music-studio-20261023\deploy_plugin.py apply
```

Các lệnh prepare/preflight/apply phía trên mô tả bước đã chạy, không chạy lại trên transaction đã installed. Plugin transaction chỉ thay ASI và record ASI trong install-state, giữ `merge_origin` / `merge_transaction`; playlist được lưu trong transaction riêng sau đó. Không chạy installer/rollback clean hoặc rollback merge cho feature này.

Gỡ riêng plugin update sau khi đã cài: cùng script với `rollback`; chặn game chạy, hash ASI/state thay đổi và backup không khớp. Nếu người dùng đã lưu playlist mới khiến state thay đổi, không tự ghi đè bằng before-image cũ; cần plan phục hồi hẹp từ state hiện tại. Nhạc menu đã lưu bằng Radio Studio có config/state before-images ở transaction riêng.

Radio Studio được mở sẵn tại `http://127.0.0.1:8790` (process do tác vụ khởi chạy). Sau khi cài plugin, bấm **Reload from game** trong tab Menu Music để mở nút lưu. Người dùng tự thử qua hai lần khởi động GTA; agent không mở/điều khiển game.
