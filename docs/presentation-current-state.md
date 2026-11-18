# Project Wibu presentation & radio shuffle — trạng thái hiện tại

**07/11/2026: đã nâng cấp cơ chế Fisher–Yates Shuffle Bag + chống lặp xuyên các lần mở game cho Loading/Menu/Music và random mốc thời gian Radio khi vào New Game ngay trong `WibuMenu.asi`** (trên nền bộ 178 ảnh + intro bypass ngày 03/11 đã được người dùng test PASS).

- Target duy nhất: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
- **Loading & Main Menu Artwork (`178/178` ảnh giữ nguyên hash)**: `89` ảnh loading đổi mỗi `2s`, `89` ảnh menu đổi mỗi `4s` theo **Fisher–Yates Shuffle Bag + Cooldown chống lặp `16` ảnh gần nhất** lưu qua `plugins/wibu-menu/wibu-shuffle.dat` (không còn chạy tuần tự `+1`). `F6` mở bảng chọn tạm dừng slideshow, `F7/F8` chọn tay, `F9` lưu favorite, `F10` đổi mode giữ nguyên.
- **Main Menu Music (`7` bài MP3 hiện có, hỗ trợ tối đa `64` bài)**: dùng **Shuffle Bag + Cooldown chống lặp bài gần nhất xuyên các lần mở game** (`K = 3` với 7 bài); tự sang bài tiếp theo trong bag khi hết bài (EOF) **và** khi thoát menu vào gameplay (nếu `random_music_per_launch=1`) để bấm `ESC` mở Pause Menu phát bài mới thay vì lặp lại từ `0:00`; không tự ghi đè `default_track`; `F3/F4` lùi/tiến theo hàng đợi shuffle; tương thích 100% với Eagle Radio Studio.
- **Radio (`RadioEx` trong `PECore.asi`)**: không sửa `PECore.asi` hay `data/radio.dat` trên đĩa. `WibuMenu.asi` kiểm chữ ký PE + relocation của `PECore.asi` (`TimeDateStamp = 0x6A309C20`, `SizeOfImage = 0x00377000`) trong RAM và hook `RadioEx::Init` + `reInitGameEvent` để reseed `srand` của `PECore` và gán `m_VirtualPosition` ngẫu nhiên đều trong `[1.0s, m_Duration - 1.0s)` cho toàn bộ `84` mục đài mỗi lần New Game / Load Game (đồng bộ cùng mốc cho file `.OGG` dùng chung như `ST_G01.OGG`).
- **Startup Intro Bypass**: giữ nguyên bỏ qua hai trạng thái intro video trước decoder, vào thẳng splash Project Wibu; hai file MPEG và executable trên đĩa không bị sửa.

Machine-readable state: [`data/project-eagle/coordination/presentation-state.json`](../../data/project-eagle/coordination/presentation-state.json).

## Điểm vào cho agent nhận việc

1. Đọc `AGENTS.md`, shared workflow và state trên trước khi sửa. Nguồn plugin mới nhất là [`presentation-radio-shuffle-20261107/plugin/src/wibu_menu.cpp`](../../staging/project-eagle/presentation-radio-shuffle-20261107/plugin/src/wibu_menu.cpp), cùng `shuffle_deck.h`, `radio_randomizer.h`, `rotation_state.h`, `intro_table_patch.h`; build bằng `plugin/build/build-x86.cmd` bên cạnh.
2. ASI đang cài SHA256 `c8106951f4b72bf5e320d2b42fe6c0b37ae7f1e0dd3e12e947fc522d0c7332d6` (nâng cấp từ bản 03/11 `550f9508855d845ef850e8e78a9da1840d8ed72dd192a0a2f0f57fb63ae459af`). Luôn kiểm hash live/state mới trước update. `wibu-menu.ini` và `wibu-shuffle.dat` thay đổi hợp lệ khi chạy game hoặc Radio Studio.
3. Selection/gallery: [thư viện 178 ảnh](../../staging/project-eagle/art-library-review-20261101/gallery.html), [inventory](../../staging/project-eagle/art-library-review-20261101/inventory.json). Giữ Alice LSS01 bản gốc, Fischl V4, Clorinde crop V2, EXC06 Danica/Vodyanitsa V2.
4. Texture pack và provenance: [`art-library-install-20261103/package`](../../staging/project-eagle/art-library-install-20261103/package/qa/texture-package.json). Runtime dùng `plugins/wibu-menu/assets/library-20261103/{loading,menu}`.
5. Không chạy lại candidate/installer của clean, menu 23 ảnh hoặc clip 0.2s cũ. Không đổi bản archive D. Mọi update mới phải giữ ownership và khóa ghi chung `tools/eagle_coord_lock.py`.

## Báo cáo, nghiệm thu, phục hồi

[Optimal Shuffle & Radio New-Game Timestamp (07/11)](loading-screens/presentation-and-radio-shuffle-2026-11-07.md) · [Auto-next và true intro bypass (03/11)](loading-screens/menu-autonext-no-intros-2026-11-03.md) · [Cài 178 ảnh và timer (03/11)](loading-screens/library-install-2026-11-03.md).

Rollback theo thứ tự mới nhất trước:
1. `staging/project-eagle/presentation-radio-shuffle-20261107/deploy_plugin.py rollback-preflight` rồi `rollback` (về bản 03/11 `550f9508...`).
2. `staging/project-eagle/menu-autonext-no-intros-20261103/deploy_plugin.py rollback-preflight` rồi `rollback`.
3. `staging/project-eagle/art-library-install-20261103/deploy_library.py rollback-preflight` rồi `rollback`.
