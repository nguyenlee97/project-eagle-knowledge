# Hệ thống Debugger, Automated Tester, Unified Logging & Crash/Error Reporting (Theo Yêu Cầu — Zero-Overhead Default)

- **Ngày triển khai**: `23/10/2026`
- **Target**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (đồng bộ sang `staging\project-eagle\gameplay-lab-poc`)
- **Staging & Backup**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\debugger-tester-2026-10-23`
- **Phiếu bàn giao**: [`work-items/2026-10-23-antigravity-debugger-tester-logging-system.md`](work-items/2026-10-23-antigravity-debugger-tester-logging-system.md)

---

## 1. Nguyên Tắc Thiết Kế Cốt Lõi: `0%` Ảnh Hưởng FPS Khi Chơi Bình Thường (`LITE` Mode Mặc Định)

Theo đúng yêu cầu thiết kế cho giai đoạn phát triển tiếp theo:
1. **Không gây ảnh hưởng tới performance của game (`0%` Overhead trong chế độ mặc định)**:
   - Toàn bộ hệ thống chạy **ngoài tiến trình game** (Out-of-process trong Python Sidecar [`EagleCompanion.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/EagleCompanion.py) + [`eagle_debug_system.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_debug_system.py)), không gắn hook nặng vào vòng lặp render D3D9 của `gta_pe.exe`.
   - Khi mở game, hệ thống luôn khởi động ở chế độ **`LITE [0% OVERHEAD]`**:
     - **Chỉ bật**: Báo Bug Map nhanh (`Ctrl + F11`), Cứu hộ nhanh `-3s` (`F12`), Bắt lỗi thụ động chống trùng lặp (`EagleSafeCall` trong `hud.lua` — khi không có lỗi sẽ tốn `0` byte I/O đĩa), và **Post-Mortem Crash Correlator** (chỉ gom log và phân tích **sau khi** game đã tắt hoặc văng).
     - **Tắt hoàn toàn**: Quét các bảng `CPool` trong RAM, đọc đuôi `fastman92limitAdjuster.log` liên tục hay ghi trace log.
2. **Chỉ bật `DEEP DEBUG` & `AUTO-PROBE TESTER` khi cần điều tra chuyên sâu**:
   - Người chơi (hoặc Agent) có thể bật/tắt tức thì chế độ **`DEEP DEBUG [LIVE RAM]`** bất cứ lúc nào bằng:
     - Phím tắt trong game: **`Ctrl + Shift + F11`**
     - Trên điện thoại trong game (`F7` $\rightarrow$ **App 8 `8.BUG`** $\rightarrow$ dùng `J/L` ở Dòng 4 chuyển sang **Trang `3/3 DEBUG`** $\rightarrow$ bấm `F9` ở Dòng 1).
     - Trên giao diện Web Smartphone (`http://127.0.0.1:8765` $\rightarrow$ App 8 $\rightarrow$ nút **`🔬 Toggle LITE ⇄ DEEP DEBUG`**).
     - Qua dòng lệnh CLI: `python eagle_doctor.py --mode deep` (và chuyển về nhẹ bằng `python eagle_doctor.py --mode lite`).

---

## 2. Chi Tiết 4 Mô-đun Đã Triển Khai

### Mô-đun 1: Unified Logging & Zero-Cost Lua/Python Error Trap
- **Trong [`hud.lua`](../../Project%20Eagle/gta%20sa%20gameplay-lab/hud.lua#L730-L756)**:
  - Thay thế các lệnh `pcall(...)` nuốt lỗi âm thầm bằng `EagleSafeCall(where, fn)`.
  - Bình thường khi hàm chạy thành công (`ok == true`), không phát sinh bất kỳ cấp phát chuỗi hay ghi file nào (`0%` overhead).
  - Nếu xảy ra lỗi runtime Lua, `EagleLogLuaError` kiểm tra bảng băm `EagleLuaErrorSeen[msg]` để **chỉ ghi mỗi lỗi duy nhất 1 lần** vào `cleo/EagleLuaErrors.log` (chống spam đĩa tuyệt đối ngay cả khi lỗi nằm trong hàm vẽ 60fps).
- **Trong [`eagle_debug_system.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_debug_system.py) (`EagleUnifiedLogger`)**:
  - Ghi log cấu trúc vào `logs/eagle_unified.jsonl` và các cảnh báo/lỗi vào `logs/eagle_errors.log`.
  - Có cơ chế **xoay vòng file tự động (`2 MiB` cap)** và **chống trùng lặp theo cửa sổ thời gian (`30s–60s` deduplication)** cho mọi `except Exception` trong `EagleCompanion.py`.
  - Tự động đồng bộ lỗi mới từ `cleo/EagleLuaErrors.log` vào bộ đếm `Lua Err` trên UI.

### Mô-đun 2: Post-Mortem Crash & Freeze Correlator (Tự Động Ghép Nối Ngữ Cảnh)
- Khi `gta_pe.exe` đóng hoặc xuất hiện file dump mới trong `ProjectEagle_crashes/` (hoặc khi bấm **`💥 Correlate Latest Crash`** / chạy `python eagle_doctor.py --analyze-crash`):
- Hệ thống tự động ghép nối:
  1. **Native Crash Dump (`ProjectEagle_crashes/*.log`)**: Địa chỉ lệnh (`EIP`), module gây lỗi (`std.data.dll`, `PECore.asi`, `gta_pe.exe`, `CLEO.asi`...), mã lỗi (`0xC0000005`), `Last file loaded`, `Last library loaded` và `Backtrace`.
  2. **Hộp Đen Gameplay (`Flight Recorder`)**: Tọa độ `(X, Y, Z)` cuối cùng trước khi văng, góc quay, vận tốc, khu vực/thành phố, vệt di chuyển 5 giây cuối (`trail_5s`), và mức RAM Streaming (`ms_memoryUsed / 2800 MiB`).
  3. **Đuôi các file Log Engine**: 15–30 dòng cuối của `fastman92limitAdjuster.log`, `cleo.log`, `PECore.log`, `EagleLuaErrors.log`.
  4. **Phân loại tự động**: Phân biệt rõ **`EXIT_CLEANUP_HARMLESS`** (lỗi dọn bộ nhớ của `std.data.dll (+0x0016F6DD)` sau lệnh `ExitProcess`/`LdrShutdownProcess` khi người chơi bấm Quit Game — chiếm 13/15 file log gần nhất, hoàn toàn vô hại với quá trình chơi!) với các lỗi thật trong lúc chơi (`MODEL_STREAMING_OR_RIG_FAULT`, `CLEO_OR_SCM_SCRIPT_FAULT`, `RUNTIME_MODULE_EXCEPTION`).
- Báo cáo xuất tự động tại:
  - [`docs/project-eagle/crash-reports/crash-audit-latest.md`](crash-reports/crash-audit-latest.md)

### Mô-đun 3: On-Demand Deep Engine Debugger (`DEEP DEBUG` Mode)
Khi bật `DEEP DEBUG` (`Ctrl + Shift + F11`), `EagleDebugSystem.sample_deep_telemetry()` đọc trực tiếp các cấu trúc nội bộ của GTA SA 1.0 US mỗi `2.0s` (thời gian đọc `< 1ms`):
- **Real-Time FPS & Hang Watchdog**: Tính FPS thực từ `CTimer::m_FrameCounter (0x00B7CB4C)`. Nếu `FrameCounter` đứng yên $\ge 6.0$ giây khi không mở Menu Pause, tự động chụp **Live Hang Snapshot** (`docs/project-eagle/crash-reports/hang-*.json`).
- **Live Streaming Memory**: Đọc `CStreaming::ms_memoryUsed (0x008E4CB4)`, `CStreaming::ms_memoryAvailable (0x008A5A80)` và `CStreaming::ms_numModelsRequested (0x008E4CB8)`.
- **Incremental Streaming Thrashing Detector**: Đọc phần đuôi mới sinh ra của `fastman92limitAdjuster.log`; nếu phát hiện 1 model bị nạp lặp lại $\ge 6$ lần liên tiếp trong 1 chu kỳ (như lỗi tự trục xuất ở `BUG-007`), lập tức báo động tên file `.dff`/`.txd` thủ phạm.
- **Live GTA SA Pools Utilization**: Đọc `CPool::m_byteMap` và `m_nSize` tại tốc độ C (`bytes.translate`) cho 8 Pool quan trọng:
  - `PedPool` (`0x00B74490`), `VehiclePool` (`0x00B74494`), `BuildingPool` (`0x00B74498`), `ObjectPool` (`0x00B7449C`), `DummyPool` (`0x00B744A0`), `ColModelPool` (`0x00B744A4`), `TaskPool` (`0x00B744A8`), `EntryInfoNodePool` (`0x00B7448C`).

### Mô-đun 4: Hệ Thống Tester 2 Tầng (`eagle_doctor.py` & In-Game `Auto-Probe Tour`)
1. **Tầng 1 — Pre-Flight Static Doctor ([`eagle_doctor.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_doctor.py))**:
   - Kiểm tra 10 hạng mục sức khỏe toàn diện của `gta sa gameplay-lab` trong `~45ms`:
     - `01_CORE_BINARIES`, `02_STREAMING_BUDGET`, `03_GPS_GRAPH_PEGG`, `04_MAP_MOUNTS_CACHE`, `05_LUA_HUD_HEALTH`, `06_UI_TEXTURES`, `07_PAIMON_COMPANION`, `08_VISUAL_POSTFX`, `09_WRITE_LOCK`, `10_CRASH_AUDIT`.
   - Xuất báo cáo tại [`docs/project-eagle/crash-reports/latest-doctor-report.md`](crash-reports/latest-doctor-report.md).
2. **Tầng 2 — In-Game Automated Smoke Probe (`Auto-Probe Tour`)**:
   - Chạy theo yêu cầu từ **App 8 Trang 3/3 (Dòng 3)**, Web UI hoặc CLI (`python eagle_doctor.py --probe CORE_CITIES`).
   - 3 gói lộ trình kiểm thử:
     - `CORE_CITIES`: 6 điểm nóng tại Los Santos, San Fierro, Las Venturas, Vice City, Biên giới Carcer–Keystone (`BUG-006`) và Hầm Liberty City Porter Tunnel (`BUG-007`).
     - `ISLAND_OUTPOSTS`: 4 ốc đảo 3D (`Chicago / Windy Bay`, `Bullworth`, `Dublin`, `Pera Loca`).
     - `BUG_REGRESSION`: Kiểm thử lại các tọa độ đã lưu trong `map-bug-reports.json`.
   - Tự động lưu vị trí xuất phát của người chơi, dịch chuyển qua từng điểm (`~3s`/điểm), kiểm tra rơi xuyên sàn (`vz` / `dz`), đo RAM Streaming, kiểm tra Thrashing và quét `.IPL/.COL` bán kính `15m`, sau đó **trả người chơi về đúng vị trí ban đầu** và xuất báo cáo ra `docs/project-eagle/crash-reports/smoke-test-latest.md`.
   - Có thể bấm **`F12`** bất cứ lúc nào để dừng tour ngay lập tức và quay về vị trí xuất phát.

---

## 3. Hướng Dẫn Sử Dụng Nhanh & Phục Hồi (Rollback)

### Sử dụng hàng ngày (Trong Game & CLI)
- **Khi chơi bình thường**: Không cần thao tác gì — hệ thống tự ở chế độ `LITE [0% OVERHEAD]`. Dùng `Ctrl + F11` khi muốn báo bug map và `F12` khi cần cứu hộ nhanh `-3s`.
- **Khi muốn bật/tắt Deep Debug**: Bấm **`Ctrl + Shift + F11`** (hoặc vào `F7` $\rightarrow$ `App 8` $\rightarrow$ `Trang 3/3 DEBUG`).
- **Chạy kiểm toán sức khỏe từ Terminal**:
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py"
  python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --analyze-crash
  ```

### Phục hồi (Rollback)
Nếu muốn gỡ bỏ bản nâng cấp Debugger/Tester này và khôi phục `EagleCompanion.py`, `hud.lua`, `eagle_phone_ui.py` về trạng thái trước đó (vẫn giữ nguyên Paimon `app11` và mọi tính năng khác):
```powershell
python "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\debugger-tester-2026-10-23\rollback_debugger_tester.py" rollback
```
Hoặc chạy trực tiếp [`Rollback_Debugger_Tester.bat`](../../staging/project-eagle/debugger-tester-2026-10-23/Rollback_Debugger_Tester.bat).
