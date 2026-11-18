# Random nhạc mỗi lần khởi động — 23/10/2026

**Đã cài vào gameplay-lab và bật cho người dùng.** Radio Studio > Menu Music có checkbox **Random opening track on each game launch**. Danh sách 7 bài, thứ tự, volume/mute và bài cố định trước đó giữ nguyên. Không mở GTA tự động; chưa có nghiệm thu nghe nhạc qua nhiều lần chạy game.

Khi random bật, plugin chọn một index trong playlist một lần tại khởi tạo, dùng entropy từ QueryPerformanceCounter và tick count. Đi qua trang con hoặc mở pause trong cùng phiên không chọn lại. F3/F4 vẫn đổi bài và lưu bài cố định dự phòng nhưng không tắt random. Khi tắt checkbox rồi Save, game mở đầu bằng bài đã chọn trong cột Opening track. Random có thể tình cờ trùng bài giữa hai lần chạy.

INI: `[audio] random_music_per_launch=1`. Khóa tách biệt với random artwork của nhân vật. Backend trả `random_per_launch` và `random_supported`, kiểm capability từ ASI đã xác minh hash; client cũ không gửi field sẽ giữ cờ hiện tại. Mặc định với config cũ là tắt, nhưng config thật của người dùng đã được bật.

Source: native Wibu Menu, kernel32 import/build (thêm QueryPerformanceCounter), Radio Studio core/menu_music.py + static/menu-music.js và các test. Candidate/build/backup/manifest riêng trong `staging/project-eagle/menu-music-random-20261023`; không tái dùng transaction clean hoặc candidate đã cài trước.

ASI trước: `c2ed6161289a23f0da0a1af4d2ae12c3f547215822a0b0b9ef1f17f55a4f35b0`.
ASI sau: `24256edbdac9c4ed4f538555cd2c20b83d11fcfaa3b5f9c6783eb48abb7f6fa1`.
Config sau bật: `e7bb81dcac042ec433c41db155369008aef49ca7219541fe08fbc0ed724ea9fd`.

Kiểm tra: 20 native assertion đạt (gồm range/variation, zero/single track, mode tắt giữ manual và F3/F4 không tắt cờ), 15 backend pytest, 7 scoped deployment pytest, build x86/verifier cho cả hai exe lab, Node syntax và API save/read lại. Kiểm 39 owned file khớp hash; core/exe/radio ngoài phạm vi, merge provenance và 7 bài giữ nguyên; khóa ghi đã trả. Bằng chứng: `qa/verification.json`, `qa/enable-random.json`, `qa/native-config/result.json` trong staging mới.

Plugin transaction: `plugin-update.json` (installed), before-image ASI/state ở `runtime-before/`. Cờ bật được lưu bằng transaction riêng trong `tools/eagle-radio-studio/data/menu_music/history/`; không thêm/chuyển đổi audio trong lượt này. Muốn trở lại chế độ bài cố định, bỏ checkbox và Save khi game đóng. Rollback ASI/state bằng utility riêng chỉ khi hash hiện tại còn đúng transaction; nếu state đã đổi sau save, giữ guard và chuẩn bị phục hồi hẹp từ state mới, không chép đè before-image cũ hoặc rollback merge.
