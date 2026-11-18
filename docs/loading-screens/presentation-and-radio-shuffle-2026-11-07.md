# Optimal Shuffle Randomization cho Loading, Main Menu, Menu Music & Radio New Game (07/11/2026)

## 1. Nguyên nhân gốc (Root Causes)

1. **Loading Screen Image (`89` TXD, `2000ms`) & Main Menu Image (`89` TXD, `4000ms`)**:
   - Phiên bản trước dùng `GetTickCount() % count` (độ phân giải tick ~`15.6ms`, dễ trùng khi mở game ở nhịp khởi động tương tự) để chọn vị trí đầu, sau đó hàm `TimedArtworkIndex` chỉ cộng tuần tự `(current + 1) % count` theo đúng thứ tự cố định trong INI/mảng `ids[89]`.
2. **Main Menu Music (`7` bài MP3, hỗ trợ tối đa `64` bài)**:
   - Khi mở game (`ChooseStartupMusic`) và khi hết bài (`NextMenuTrack`), plugin bốc ngẫu nhiên không nhớ lịch sử nên dễ lặp lại bài vừa nghe ở lần mở trước hoặc nhảy qua lại `A -> B -> A` thay vì đi hết một vòng hoán vị đủ 7 bài.
   - Khi rời Main Menu vào Gameplay (`!customMenu && gLastCustomMenu`), `StopBassStream()` dừng nhạc nhưng không đổi `gTrackIndex`, khiến mỗi lần bấm `ESC` mở Pause Menu trong lúc chơi lại phát lại đúng bài đó từ `0:00`.
3. **Radio (`RadioEx` trong `PECore.asi`) luôn phát từ `0:00` khi vào New Game**:
   - Disassembly `PECore.asi` (`TimeDateStamp = 0x6A309C20`, `SizeOfImage = 0x00377000`) cho thấy:
     - `RadioEx::Init` (`RVA 0x000F4670`, chạy ở lần New Game/Load Game đầu tiên) và `reInitGameEvent` (`RVA 0x000F8D70`, chạy ở các lần New Game/Load Game tiếp theo) đặt `station.m_VirtualPosition = 0.0f` (`[station + 0x50]`) cho toàn bộ 84 mục đài thuộc 8 vùng (`m_Regions` tại `RVA 0x0026F0E4`).
     - Ở frame đầu tiên của New Game, nhân vật đứng dưới đất (chưa lên xe). `RadioEx::Update` (`RVA 0x000F7670`) rẽ sang vòng lặp đồng hồ ảo nền (`RVA 0x000F7B07..0x000F7C0C`) và cộng ngay `dt` (`~0.016s`) vào `m_VirtualPosition` (`> 0.0f`).
     - Khi người chơi lên xe vài giây sau, `LoadRegionStreams` (`RVA 0x000F6B92: comiss xmm1, [esi+0x50]; jb 0x100F6BB5`) thấy `m_VirtualPosition > 0.0f` nên **bỏ qua hoàn toàn** nhánh chọn mốc ngẫu nhiên tại `RVA 0x000F6B98`. Ngoài ra `srand` tĩnh của `PECore` (`RVA 0x0015E4C6`) chỉ gọi 1 lần lúc khởi động bằng `time(0)` theo giây.

## 2. Giải pháp kỹ thuật đã triển khai

Toàn bộ nâng cấp được đóng gói gọn trong `WibuMenu.asi` tại `staging/project-eagle/presentation-radio-shuffle-20261107/plugin/` (`x86 PE32`, `/NODEFAULTLIB`, chỉ import `KERNEL32.dll` và `USER32.dll`, không sửa `PECore.asi` hay `data/radio.dat` trên đĩa):

- **`shuffle_deck.h` — PRNG 128-bit + Fisher–Yates Shuffle Bag + Cooldown xuyên các lần mở game**:
  - `WibuRng`: Xorshift128 kết hợp bộ trộn avalanche Murmur3 32-bit (`Mix32`) và lấy mẫu không lệch modulo (`NextBounded`), gieo mầm từ 8 nguồn entropy (`QueryPerformanceCounter` lo/hi, `rdtsc` lo/hi, `GetTickCount`, `PID`, `TID`, địa chỉ stack ASLR và `launchCounter`).
  - `ShuffleBag`: mỗi chu kỳ (epoch) sinh một hoán vị đầy đủ `0 .. N-1` bằng Fisher–Yates, đồng thời áp dụng cửa sổ chống lặp `K = min(maxCooldown, (N - 1) / 2)` (tái xáo trộn độc lập tiền tố `0..K-1` và hậu tố `K..N-1` để giữ phân phối đều toán học):
    - **Loading Screen Image (`N = 89`, `2000ms`)**: tráo đủ 89 ảnh ngẫu nhiên mỗi chu kỳ, chống lặp `K = 16` ảnh gần nhất giữa các chu kỳ và giữa các lần mở game.
    - **Main Menu Image (`N = 89`, `4000ms`)**: tráo đủ 89 ảnh bìa nhân vật ngẫu nhiên, chống lặp `K = 16` ảnh gần nhất; giữ nguyên `F6` tạm dừng slideshow, `F7/F8` chọn tay, `F9` lưu favorite, `F10` đổi chế độ.
    - **Main Menu Music (`N = 7`, hỗ trợ tới `64` bài)**: phát đủ cả 7 bài theo thứ tự xáo trộn mới trước khi lặp lại, chống lặp `K = 3` bài gần nhất xuyên các lần mở game; tự sang bài tiếp theo trong bag khi hết bài (EOF) **và** khi thoát menu vào gameplay (nếu `random_music_per_launch=1`) để mỗi lần bấm `ESC` mở Pause Menu nghe bài mới; `F4`/`F3` tiến/lùi theo hàng đợi shuffle; bảo toàn `default_track` và tương thích 100% với Eagle Radio Studio.
  - **Lưu trạng thái bền vững `plugins/wibu-menu/wibu-shuffle.dat` (`236` bytes)**: lưu `launchCounter`, lịch sử hash không phân biệt hoa/thường của ảnh/nhạc gần nhất và checksum FNV1a+Murmur3 (tự động ánh xạ an toàn kể cả khi thêm/xóa/đổi thứ tự bài trong Radio Studio; nếu file hỏng checksum sẽ tự reset sạch).
- **`radio_randomizer.h` — Random mốc thời gian Radio khi vào New Game / Load Game**:
  - Kiểm tra chặt chẽ `PECore.asi` trong RAM (`TimeDateStamp == 0x6A309C20`, `SizeOfImage == 0x00377000`, chữ ký byte bất biến với ASLR relocation tại `RadioEx::Init` `0x000F4670`, `reInitGameEvent` `0x000F8D70`, vòng lặp reset `StationConfig` stride `0x58` tại `0x000F8DE0`, và `srand` tại `0x0015E4C6`; kiểm cả toán hạng địa chỉ đã relocate trỏ đúng `m_Initialized` `base + 0x002FD65D`). Nếu `PECore.asi` khác phiên bản thì tự ngắt an toàn (fail-closed).
  - Đặt MinHook vào `RadioEx::Init` (lần vào game đầu sau khi mở `gta_pe.exe`) và `RadioEx::reInitGameEvent` (mọi lần New Game / Load Game tiếp theo):
    1. Gieo lại `srand` của `PECore` ngay trên main thread để xe mới bước lên cũng chọn đài ban đầu ngẫu nhiên thực sự.
    2. Duyệt `RadioEx::m_Regions` (`base + 0x0026F0E4`) và gán `m_VirtualPosition` phân phối đều 24-bit float trong khoảng `[1.0s, m_Duration - 1.0s)` cho tất cả các đài (`84` mục đài / `78` file `.OGG`). Các vùng dùng chung cùng tên file `.OGG` (như `ST_G01.OGG`) nhận cùng mốc thời gian trong phiên đó để đi xuyên ranh giới vùng không bị nhảy lùi/tiến bài.

## 3. Hash triển khai & Kiểm chứng

- Target: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- `WibuMenu.asi` trước khi cài (`menu-autonext-no-intros-20261103`): `550f9508855d845ef850e8e78a9da1840d8ed72dd192a0a2f0f57fb63ae459af`
- `WibuMenu.asi` sau khi cài (`presentation-radio-shuffle-20261107`, `34,304` bytes): `c8106951f4b72bf5e320d2b42fe6c0b37ae7f1e0dd3e12e947fc522d0c7332d6`
- `.wibu-menu-install-state.json`: `cb2d02bbf89ef0da2311ad2cabd0028c3c35eb9c4e79e6a419ecddb66695113c` -> `ba4ff4be444772c3558034c6df426d2c46bbcf8f6da21349d3836d3922107723`
- `228/228` file được bảo vệ (gồm `PECore.asi`, `PECore.ini`, `data/radio.dat`, `wibu-menu.ini`, `gta_sa.exe`, `gta_pe.exe`, `movies/*.mpg` và toàn bộ `178` file `.txd`) giữ nguyên `100%` SHA-256.
- Kiểm tra đã chạy PASS:
  - `qa/verify_plugin.py`: PASS chữ ký `gta_sa.exe`, `gta_pe.exe`, `PECore.asi`, `MinHook.x86.dll`, `wibu-bass.dll`, 89 character IDs, 3 loading hooks, intro jump stub, Radio Studio markers (`default_track`, `random_music_per_launch`), import tĩnh chỉ gồm `kernel32.dll` + `user32.dll`.
  - `qa/shuffle_and_radio_probe.cpp` (`exit=0`): PASS 400 chu kỳ x 89 ảnh (`35,600` lượt rút, 0 lặp trong chu kỳ, 0 vi phạm cooldown `K=16`), 1,000 chu kỳ x 7 bài nhạc (`7,000` lượt rút, 0 vi phạm cooldown `K=3`), 30 lần mở game liên tiếp qua `wibu-shuffle.dat`, tự hồi phục khi hỏng checksum, tự tiến bài khi rời Menu sang Gameplay, timer `2000ms`/`4000ms` + tràn `GetTickCount` 32-bit, guard `PECore.asi` relocate + 20 phiên New Game trên 8 vùng / 84 đài.
  - `qa/intro_probe.cpp` (`exit=0`): PASS vá nguyên tử bảng nhảy intro.
  - Eagle Radio Studio `core.menu_music.Manager.get_state()`: PASS (`track_count=7`, `persistence_supported=True`, `random_supported=True`).
  - `deploy_plugin.py rollback-preflight`: PASS.
  - `eagle_doctor.py`: `11/11 PASS, 0 WARN, 0 FAIL`.

## 4. Thứ tự Rollback

Nếu cần quay lui bản cập nhật 07/11 về bản 03/11 (`550f9508...`) khi GTA đã đóng:

```powershell
python staging\project-eagle\presentation-radio-shuffle-20261107\deploy_plugin.py rollback-preflight
python staging\project-eagle\presentation-radio-shuffle-20261107\deploy_plugin.py rollback
```

Chuỗi rollback xếp chồng hiện tại (từ mới nhất về cũ nhất):
1. `staging/project-eagle/presentation-radio-shuffle-20261107/deploy_plugin.py`
2. `staging/project-eagle/menu-autonext-no-intros-20261103/deploy_plugin.py`
3. `staging/project-eagle/art-library-install-20261103/deploy_library.py`
