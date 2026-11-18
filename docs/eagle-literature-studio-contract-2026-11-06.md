# Hợp Đồng Kỹ Thuật Liên Dự Án: `EagleLit Pack v1.0` (Dual-Mode Cinema & Library)

- **Ngày ban hành:** `2026-11-06`
- **Workspace Sản Xuất Nội Dung (Literature Factory):** `D:\Eagle Literature Studio`
- **Workspace Đích Tích Hợp Game (Runtime Target):** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Mục tiêu cốt lõi:** Mọi bộ phim chuyển thể từ Fanfic / Truyện ngắn / IF Route (**Rạp phim — `cinema`**) và mọi bộ Light Novel dài kỳ (**Thư viện — `library`**) được sản xuất độc lập 100% tại `D:\Eagle Literature Studio`, đóng gói theo chuẩn **`EagleLit Pack v1.0`** tại `D:\Eagle Literature Studio\packages\<work_id>\`, để khi đưa sang Project Eagle (`gameplay-lab`) thì engine Rạp phim & Thư viện tự động nạp **Plug-and-Play (0 dòng code sửa tay)** và tiêu tốn **`0 MB` trên ổ `C:`** (nhờ nối NTFS Junction trực tiếp từ `gameplay-lab\ui_assets\literature_packs` sang `D:\Eagle Literature Studio\packages`).

---

## 1. Kiến Trúc Chế Độ Đọc Kép (`Dual-Mode Synchronized Reader`)

Mỗi gói `EagleLit Pack v1.0` bắt buộc phục vụ đồng thời **2 chế độ trình chiếu/đọc** trong game (người chơi có thể bấm phím chuyển chế độ tức thì ngay giữa câu đang đọc mà không bị lệch vị trí):

1. **Chế độ 1 — `adv_cinema` (Fullscreen 16:9 Visual Novel / Cinema Mode):**
   - Giống giao diện `Story Quest` hiện tại: Ảnh CG màu phủ toàn màn hình `16:9` (`1920x1080` qua khe Ping-Pong TXD `1376x768`), hộp thoại kính mờ nằm ở chân màn hình (`~22%` dưới cùng), hiện nhãn `Speaker` + lời thoại/dẫn chuyện + dòng độc thoại nội tâm (`inner_thought` nếu có).
   - Hỗ trợ bấm tay qua nhịp (`[SPACE]` / `[ENTER]` / `LMB`) hoặc bật **Auto-Play `[A]`** tự lật câu theo `auto_hold_ms` (`1.0x / 1.5x / 2.0x`).
   - **Độ giữ nguyên văn:** **`95% - 100%` nguyên văn bản dịch gốc**. Tuyệt đối không tóm tắt lược bỏ tình tiết hay cắt xén văn chương; chỉ tách các đoạn văn quá dài thành các nhịp (`vn_beats`) vừa khung hộp thoại (`120 - 240` ký tự/beat) và bóc tách tên người nói (`speaker`) khi có lời thoại trực tiếp.

2. **Chế độ 2 — `nvl_book` (Split-Screen Illustrated Book Mode):**
   - **Nửa trái màn hình (`~46%` chiều ngang):** Hiển thị bức CG màu minh hoạ của phân đoạn hiện tại kèm thẻ tên Chương/Cảnh và thanh nhạc nền `BGM` tinh gọn bên dưới. **Tự động chuyển đổi mượt bức CG (`cg_id`) và nhạc nền (`bgm_id`) ngay khi người đọc cuộn trang hoặc bấm đọc tới đoạn văn tương ứng bên phải.**
   - **Nửa phải màn hình (`~54%` chiều ngang):** Trình bày như trang sách thực thụ (chia đoạn văn rõ ràng, giữ nguyên lời thoại trong ngoặc kép, dấu ngắt cảnh `---`), cho phép **cuộn mượt bằng con lăn chuột (`Mouse Wheel`)** hoặc bấm phím đọc từng đoạn xuống dưới (`Down/Space/PgDn`), kèm tuỳ chọn **Auto-Scroll**.
   - **Độ giữ nguyên văn:** **Giữ `100%` nguyên văn (`verbatim`)** từng đoạn văn của bản dịch gốc trong trường `book_text` (sau khi đã chuẩn hoá ký tự an toàn `CFont` ASCII).

3. **Cơ chế đồng bộ Không Lệch Giữa 2 Chế Độ (`Block <-> Beat Anchor`):**
   - Đơn vị gốc trong file dữ liệu là **`block`** (mỗi `block` = 1 đoạn văn nguyên bản cho Chế độ 2 `book_text`).
   - Bên trong mỗi `block` chứa mảng **`vn_beats`** (`1..N` nhịp thoại tách ra từ chính đoạn `book_text` đó cho Chế độ 1).
   - Nhờ cấu trúc lồng `block -> vn_beats`, khi đang ở `block #45, beat #2` ở Chế độ 1 mà bấm đổi sang Chế độ 2, trang sách tự cuộn tới đúng đoạn `block #45`; ngược lại đang cuộn đọc `block #60` ở Chế độ 2 mà bấm sang Chế độ 1, màn chiếu mở đúng `vn_beats[0]` của `block #60` với cùng CG và BGM!

---

## 2. Cấu Trúc Thư Mục Chuẩn Của `D:\Eagle Literature Studio`

```text
D:\Eagle Literature Studio\
├── AGENTS.md                           # Quy tắc bắt buộc cho mọi agent trong workspace
├── GEMINI.md                           # Điểm vào quy tắc cho Antigravity / Gemini
├── .agents\
│   └── skills\                         # Các skill chuyên biệt cho dây chuyền chuyển thể
│       ├── source-harvester\SKILL.md
│       ├── dual-mode-adapter\SKILL.md
│       ├── cg-art-director\SKILL.md
│       └── pack-validator-previewer\SKILL.md
├── bootstrap\
│   └── GTA_EAGLE_LIT_CONTRACT_V1.md    # Tài liệu hợp đồng gốc này
├── prompts\
│   ├── 01-init-project-rules-skills.md
│   └── 02-rezero-pride-if-cinema.md
├── sources\                            # Lưu bản thô UTF-8 nguyên gốc tải về (để đối chiếu 100% word coverage)
│   └── <work_id>\
│       ├── raw_chapters\
│       └── source_metadata.json
├── references\                         # Ảnh tham chiếu nhân vật, bối cảnh & art style chính gốc
│   └── <franchise_slug>\
│       ├── style_guide.md
│       ├── characters\
│       ├── locations\
│       └── official_art_samples\
├── bgm_pool\                           # Kho OST nguyên bản thô tải về trước khi cắt/chuẩn hoá
│   └── <franchise_slug>\
├── tools\                              # Các công cụ Python kiểm định & sinh trình xem thử
│   ├── cfont_sanitizer.py
│   ├── audio_mci_normalizer.py
│   ├── validate_pack.py
│   └── build_preview_html.py
└── packages\                           # ĐẦU RA CUỐI CÙNG ĐỂ ĐƯA SANG GTA (Plug-and-Play)
    └── <work_id>\
        ├── manifest.json               # Metadata, dàn nhân vật, danh mục CG, danh mục BGM, mục lục chương
        ├── poster.jpg                  # Poster dọc 2:3 (832x1248) treo ở Sảnh Rạp Phim / Bìa Sách Thư Viện
        ├── banner_16x9.jpg             # Ảnh bìa ngang 16:9 (1376x768) cho bảng chọn suất chiếu / mục lục
        ├── chapters\
        │   ├── ch01.json               # Dữ liệu Dual-Mode (scenes -> blocks -> vn_beats) từng chương
        │   └── ...
        ├── cgs\
        │   ├── cg_ch01_sc01_base.jpg   # Toàn bộ ảnh CG màu 16:9 (1376x768, baseline RGB JPEG)
        │   └── ...
        ├── bgm\
        │   ├── bgm_01_dread.mp3        # Nhạc nền không lời chuẩn Win32 MCI (192kbps, stripped ID3v2)
        │   └── ...
        ├── cg_generation_manifest.json # Sổ theo dõi tiến độ vẽ CG & quota (done / pending)
        ├── validation_report.json      # Báo cáo kiểm định tự động (phải PASS 100% trước khi xuất xưởng)
        └── preview.html                # Trình chiếu thử nghiệm Dual-Mode (Mode 1 + Mode 2 + Auto + BGM) trên trình duyệt
```

---

## 3. Đặc Tả JSON Schema Chi Tiết (`EagleLit Pack v1.0`)

Xem chi tiết các trường bắt buộc của `manifest.json` và `chapters/<chapter_id>.json` tại bản sao đồng bộ `D:\Eagle Literature Studio\bootstrap\GTA_EAGLE_LIT_CONTRACT_V1.md` (hai file đồng nhất 100% về cấu trúc `schema_version = "eagle_lit_v1"`, luật sạch ký tự `CFont` `32..126` không chứa `~ | * @`, ảnh `1376x768` RGB JPEG vẽ bằng `image-generator` nội bộ, và âm thanh MP3 `192kbps` gỡ sạch ID3v2 cho Win32 MCI).

### Quy ước Phía GTA (`gameplay-lab`) Khi Tích Hợp Module Rạp Phim & Thư Viện:
1. **Đường dẫn gắn kết Không Tốn Ổ `C:`:**
   - Tạo NTFS Junction `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\ui_assets\literature_packs` trỏ thẳng về `D:\Eagle Literature Studio\packages`.
   - Engine Python (`eagle_literature_engine.py`) tự động quét mọi thư mục con `*/manifest.json` có `schema_version == "eagle_lit_v1"` (và `validation_report.json` đạt `passed == true` hoặc đủ tài nguyên hợp lệ).
2. **Phân phối tự động theo `venue_type`:**
   - `venue_type in ("cinema", "both")` -> Đưa vào **Lịch chiếu xoay tua theo tuần (7 ngày in-game dựa trên `eagle_savegame_sync.py`)** của các Rạp Phim, tự sinh `4-5` suất chiếu/ngày (khung giờ linh hoạt `+-60` phút in-game), hiển thị `poster.jpg` ngoài Sảnh Rạp và mở mặc định ở `adv_cinema` (phím `[V]` chuyển qua lại `nvl_book` tức thì).
   - `venue_type in ("library", "both")` -> Đưa vào **Kệ Sách / Quầy Thuê Mua của Thư Viện** (`rent_price_usd` theo tuần hoặc `buy_price_usd` vĩnh viễn), lưu Bookmark tự động theo từng cuốn sách + slot save, mở mặc định ở `nvl_book` khi ngồi vào bàn đọc sách (phím `[V]` chuyển qua lại `adv_cinema` tức thì).
3. **Không Gian 3D Nối Tiếp Đúng Chuẩn Thực Tế:**
   - **Rạp phim:** `Đường phố -> Sảnh rạp (Quầy vé + Quầy bắp nước) -> Phòng chiếu (Đi tới hàng ghế bấm [E] xem phim)`. Xem hết phim hoặc bấm `[Backspace]` dừng giữa chừng **chỉ đóng lớp HUD 2D, giữ nguyên Aether đứng tại ghế trong Phòng chiếu**; người chơi tự đi bộ ra cửa `Exit Phòng chiếu -> Sảnh rạp -> Exit Sảnh rạp -> Đường phố`.
   - **Thư viện:** `Đường phố -> Nội thất Thư viện (Quầy thuê/mua sách + Kệ sách + Bàn đọc sách [E])`. Đóng trang sách giữ nguyên Aether tại bàn đọc trong Thư viện, đi bộ ra cửa chính mới về lại đường phố.
