# 02. Kiến Trúc, Cấu Trúc Mã Nguồn & Schema Dữ Liệu — Eagle Radio Studio

- **Vị trí mã nguồn công cụ:** [`C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio`](file:///C:/Users/LENOVO/Desktop/GTA/tools/eagle-radio-studio)
- **Launcher mở nhanh (Double-click):**
  - [`C:\Users\LENOVO\Desktop\GTA\Start_Eagle_Radio_Studio.bat`](file:///C:/Users/LENOVO/Desktop/GTA/Start_Eagle_Radio_Studio.bat)
  - [`C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio\Start_Eagle_Radio_Studio.bat`](file:///C:/Users/LENOVO/Desktop/GTA/tools/eagle-radio-studio/Start_Eagle_Radio_Studio.bat)
- **Địa chỉ giao diện cục bộ:** `http://127.0.0.1:8790` (Tách biệt hoàn toàn với cổng `8765` của `EagleCompanion` / `eagle_phone_ui.py` trong `gameplay-lab`).

---

## 1. Kiến Trúc Mô-đun & Dependencies

### 1.1. Dependencies (Đã có sẵn trên máy, không cần cài thêm)
- **Python Runtime:** `C:\Python310\python.exe` (Python 3.10.2 với `fastapi`, `uvicorn`, `Pillow`, `pytest` có sẵn).
- **Audio Toolchain:** `C:\PATH_Program\ffmpeg.exe` & `C:\PATH_Program\ffprobe.exe` (FFmpeg dùng để probe thời lượng/codec và chuẩn hóa/ghép luồng OGG Vorbis `44100 Hz` Stereo).
- **Native Windows Dialogs:** Sử dụng trực tiếp Win32 `comdlg32.dll` (`GetOpenFileNameW`) qua `ctypes` chuẩn của Python — không phụ thuộc `tkinter` hay `python-multipart`.

### 1.2. Cấu Trúc Thư Mục (`tools\eagle-radio-studio\`)
```text
C:\Users\LENOVO\Desktop\GTA\tools\eagle-radio-studio\
├── Start_Eagle_Radio_Studio.bat       # Launcher khởi động nhanh bằng 1 cú nhấp chuột
├── app.py                             # FastAPI Backend Server (Port 8790)
├── core\
│   ├── __init__.py
│   ├── config_parser.py               # Bộ đọc/ghi AST bảo toàn nguyên trạng data\radio.dat, radio.zon, PECore.ini
│   ├── txd_manager.py                 # Bộ giải mã & đóng gói RenderWare D3D9 (models\txd\radio.txd + Auto-Badge)
│   ├── audio_pipeline.py              # FFprobe inspector, Content-Hash Cache & FFmpeg OGG stream compiler
│   ├── deployer.py                    # Kiểm tra tiến trình, phát hiện xung đột ngoài, Staging Diff, Backup & Rollback
│   ├── project_store.py               # Quản lý lưu trữ project.json, build_state.json và tạo nhạc mẫu test
│   └── win_dialogs.py                 # Hộp thoại chọn file/ảnh gốc của Windows Explorer (Win32 ctypes)
├── static\
│   ├── index.html                     # Giao diện chính Tiếng Việt (4 Tab + Trình phát nhạc Chapter Preview)
│   ├── styles.css                     # Giao diện Dark Mode hiện đại, rõ ràng
│   └── app.js                         # Logic điều khiển Frontend
├── tests\
│   └── test_end_to_end.py             # Bộ kiểm thử tự động End-to-End & các kịch bản lỗi (Failure Modes)
└── data\                              # Dữ liệu của tool (tách biệt 100% khỏi thư mục game)
    ├── project.json                   # Trạng thái Project hiện tại
    ├── build_state.json               # Manifest kết quả Build và Track Offsets của từng kênh
    ├── cache\                         # Bộ nhớ đệm đoạn nhạc chuẩn hóa (tracks\) và luồng kênh (stations\)
    ├── sprite_cache\                  # 75 ảnh PNG trích xuất từ models\txd\radio.txd để hiển thị trong UI
    ├── custom_logos\                  # Ảnh logo người dùng tải lên
    ├── sample_tracks\                 # 4 file nhạc mẫu [Test Asset] (.mp3, .flac, .wav, .ogg)
    ├── staging\                       # Bản nháp cấu hình trước khi Apply (staging\lab\, staging\main\)
    ├── manifests\                     # Manifest ghi nhận trạng thái đã cài (installed_lab.json, installed_main.json)
    └── backups\                       # Các bản sao lưu nguyên tử kèm SHA-256 theo từng lần Apply
```

---

## 2. Schema Dữ Liệu Bảo Trì & Mở Rộng

### 2.1. Project Schema (`data\project.json`)
Tách biệt hoàn toàn danh tính kênh (`id`: `st_...`), danh sách bài hát (`playlist`), cài đặt âm thanh và phân bổ vùng (`regions`, `region_order`):

```json
{
  "schema_version": 1,
  "name": "Thế Giới Anime & Dạo Phố — Project Eagle Radio",
  "selected_target_key": "lab",
  "selected_target_path": "C:\\Users\\LENOVO\\Desktop\\GTA\\Project Eagle\\gta sa gameplay-lab",
  "enable_sa_region_2": true,
  "use_visual_radio_sprites": true,
  "install_static_mp3": true,
  "region_position_mode": { "5": "prepend", "7": "prepend", "2": "prepend" },
  "baseline_overrides": {},
  "imported_target_hashes": {},
  "stations": [
    {
      "id": "st_teyvat_jpop",
      "name": "Teyvat Starlight FM (Anime & J-Pop)",
      "enabled": true,
      "sprite_mode": "auto_badge",
      "builtin_sprite": "LC_1",
      "badge_theme": "neon_anime",
      "badge_subtitle": "ANIME JPOP",
      "custom_image_path": "",
      "playback_order": "sequential",
      "shuffle_seed": 101,
      "transition_mode": "gapless",
      "normalize_loudness": true,
      "regions": [5, 7, 4, 1, 3, 8, 6, 2],
      "region_order": { "5": 10, "7": 10, "2": 10 },
      "playlist": [
        {
          "id": "trk_01",
          "source_path": "C:\\path\\to\\song.mp3",
          "title": "Song Title",
          "artist": "Artist Name",
          "duration_sec": 8.0,
          "codec_name": "mp3",
          "sample_rate": 44100,
          "channels": 2,
          "fingerprint": "a1b2c3d4..."
        }
      ]
    }
  ]
}
```

### 2.2. Compiled Stream & Track Offset Manifest (`data\build_state.json`)
Lưu vị trí bắt đầu và kết thúc (`start_sec`, `end_sec`) của từng bài hát bên trong file `.OGG` đã ghép, cho phép nghe thử và tua nhanh theo từng bài ngay trong UI:

```json
{
  "st_teyvat_jpop": {
    "station_id": "st_teyvat_jpop",
    "station_name": "Teyvat Starlight FM (Anime & J-Pop)",
    "success": true,
    "cache_hit": false,
    "output_cache_path": "...\\data\\cache\\stations\\st_teyvat_jpop_8f9a1b.ogg",
    "relative_game_audio_path": "AUDIO\\PE\\RADIO\\CUSTOM\\ST_TEYVAT_JPOP.OGG",
    "total_duration_sec": 15.0,
    "content_hash": "8f9a1b...",
    "station_signature": "8f9a1b...",
    "track_offsets": [
      {
        "order_index": 1,
        "track_id": "trk_01",
        "title": "[Test] Teyvat Starlight (Anime J-Pop Demo)",
        "start_sec": 0.0,
        "end_sec": 8.0,
        "duration_sec": 8.0
      }
    ]
  }
}
```

### 2.3. Backup Manifest (`data\backups\<target_slug>\<backup_id>\backup_manifest.json`)
Ghi lại trạng thái tồn tại (`existed: true/false`) và mã băm `SHA-256` của mọi file liên quan ngay trước thời điểm Apply để phục vụ Rollback tự động (khi lỗi giữa chừng) hoặc Restore theo yêu cầu người dùng.
