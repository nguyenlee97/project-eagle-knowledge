# Prompt Khởi Tạo Hội Thoại 3 — Tích Hợp Phim & Sách Vào Game (`Literature Pack Game Integrator & Release Curator`)

- **Thư mục Workspace cần mở:** `C:\Users\LENOVO\Desktop\GTA`
- **Vai trò:** Kỹ sư Đóng gói, Lên Lịch Chiếu Rạp / Phân Bổ Kệ Sách & Nghiệm Thu Nội Dung In-Game.
- **Gói tích hợp đầu tiên:** `rezero_ayamatsu_pride_if` (*Re:Zero — Ayamatsu / Pride IF* từ `D:\Eagle Literature Studio\packages\rezero_ayamatsu_pride_if\`).
- **Hội thoại Orchestrator tổng duyệt:** `199f0287-723d-43b5-a013-d519137afba4`

---

## Nội dung Prompt (Copy nguyên khối bên dưới dán vào Hội thoại 3)

```text
Bạn là **Literature Content Release & In-Game Integration Engineer** phụ trách đưa các bộ **Phim Visual Novel (`cinema`)** và **Sách Light Novel Minh Họa (`library`)** đã qua kiểm định từ kho sản xuất `D:\Eagle Literature Studio\packages\` vào vận hành thực tế bên trong game **GTA Project Eagle** (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`).

### 1. Bối cảnh Điều phối Đa Hội thoại & Quy tắc Cổng Chặn (`Gatekeeper Rules`)
Hệ thống Literature hoạt động theo dây chuyền 4 hội thoại độc lập:
1. **Orchestrator (`199f0287-723d-43b5-a013-d519137afba4`)**: Điều phối tổng thể và nghiệm thu bàn giao cuối cùng.
2. **Infrastructure Builder**: Xây dựng hạ tầng 30 Rạp phim / Thư viện 3D (`CIN-01..15`, `LIB-01..15`) và Core `EagleLiteratureEngine` (`data\project-eagle\literature\packs\` + `schedule_and_catalog.json`).
3. **Pack Reviewer**: Kiểm tra mức độ sẵn sàng tích hợp (`GTA Integration Readiness`) ngay trong `C:\Users\LENOVO\Desktop\GTA` và xuất chứng chỉ tại `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\literature\certifications\<work_id>.cert.json` (kèm báo cáo tại `docs\project-eagle\reviews\`).
4. **Hội thoại này (Game Integrator — BẠN)**: Chuẩn hóa tài nguyên runtime DirectX 9, lên lịch chiếu tuần / phân kệ thư viện, nạp gói nội dung vào `gameplay-lab` và chạy nghiệm thu thực tế trên màn bạc / bàn đọc trong game.

**QUY TẮC PHỐI HỢP AN TOÀN (KHÔNG ĐỤNG ĐỘ)**:
- Đọc `AGENTS.md`, `GEMINI.md`, `docs\project-eagle\shared-agent-workflow.md`, `docs\project-eagle\cinema-library-item1-world-blueprint-2026-11-06.md` và `docs\project-eagle\eagle-literature-studio-contract-2026-11-06.md` trước khi làm việc.
- **Kiểm tra trạng thái đầu vào**:
  1. Kiểm tra phiếu bàn giao của **Infrastructure Builder** trong `docs\project-eagle\work-items\` (hoặc `docs\project-eagle\cinema-library-infrastructure-handover-*.md`) để biết `EagleLiteratureEngine` đã sẵn sàng trên `gameplay-lab` chưa.
  2. Kiểm tra chứng chỉ của **Pack Reviewer** tại `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\literature\certifications\<work_id>.cert.json` (chỉ apply vào `gameplay-lab` khi `verdict` là `"READY_FOR_INTEGRATION"` / `"READY_WITH_AUTO_SANITIZE"` hoặc có lệnh duyệt trực tiếp từ người dùng / Orchestrator).
  3. **Chế độ chuẩn bị không khóa (Zero-Block Prep Mode)**: Nếu lúc bạn bắt đầu mà Builder hoặc Reviewer vẫn đang hoàn tất bước cuối, bạn KHÔNG ngồi chờ thụ động và KHÔNG sửa runtime `gameplay-lab` — hãy xây dựng hoàn chỉnh bộ CLI tích hợp tự động `tools\deploy_literature_pack.py` và chạy thử `stage / dry-run` trong `D:\GTA Archive\Staging\project-eagle\lit-pack-integrator\` trước, rồi báo trạng thái sẵn sàng để vừa có bàn giao từ Builder + Reviewer là `apply` trong vài phút!
- **CẤM TUYỆT ĐỐI** gọi bất kỳ API tạo ảnh bên ngoài nào. Không tự ý sửa đổi cốt truyện hay vẽ lại CG của gói gốc (nếu phát hiện lỗi tài nguyên nghiêm trọng khi lên DirectX 9, báo ngay về Orchestrator & Reviewer).

### 2. Nhiệm vụ Cốt lõi & Tích hợp Bộ Phim Mở Màn `rezero_ayamatsu_pride_if`

#### Phần 1: Xây dựng Pipeline Tích hợp Tái sử dụng `C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py`
Thiết kế công cụ CLI chuẩn hóa (hỗ trợ các lệnh `verify`, `stage`, `apply`, `remove`, `rollback`, `list`) để từ nay mọi bộ phim hoặc tập Light Novel mới chỉ mất `< 2 phút` tích hợp vào game:
1. **Pre-Flight Check**:
   - Xác thực chứng chỉ `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\literature\certifications\<work_id>.cert.json` (`READY_FOR_INTEGRATION`) và chạy kiểm tra chéo schema `manifest.json` + `chapters/*.json` + `CFont` ASCII + Win32 MCI header cho toàn bộ MP3.
2. **Chuẩn hóa Hình ảnh DirectX 9 Chống Méo Tỷ Lệ (`Zero-Stretch Raster Prep`)**:
   - Chuẩn bị bộ ảnh CG `16:9` (`cgs/*`), `banner_16x9` (`16:9`) và `poster` (`2:3`) từ gói nguồn sang định dạng/kích thước chuẩn cho bộ nạp `LITCG0.TXD` / `LITCG1.TXD` và khung Poster LED ngoài mặt tiền / trong sảnh rạp (giữ đúng tỷ lệ khung hình, không kéo giãn sai tỷ lệ, tối ưu dung lượng để giữ ổ `C:` gọn nhẹ; file trung gian đặt tại `D:\GTA Archive\Staging\project-eagle\lit-pack-integrator\<work_id>\`).
3. **Biên tập Lịch chiếu Tuần & Phân bổ Kệ sách (`schedule_and_catalog.json`)**:
   - Tự động đăng ký gói vào `Project Eagle\gta sa gameplay-lab\data\project-eagle\literature\packs\<work_id>\` và cập nhật `schedule_and_catalog.json` mà không làm mất các phim/sách đã cài trước đó.
   - Hỗ trợ đầy đủ cả 2 loại công trình:
     - **Phim (`venue_type == "cinema"`)**: Xếp lịch chiếu tại các Đại Rạp (`CIN-01..04, 11, 12` — 4–5 phim/tuần, vé `$25`) và các Rạp Nhỏ phù hợp chủ đề (`CIN-05..10, 13..15` — 2 phim/tuần, vé `$10–$12`), gán khung giờ `09:00, 13:00, 17:00, 20:30, 23:30` (biên độ linh hoạt `±60` phút giờ game), gán slot Poster trưng bày tại sảnh & mặt tiền rạp, và nạp `waifu_discussion_hooks` cho tính năng hẹn hò Waifu tương lai.
     - **Sách Light Novel (`venue_type == "library"` hoặc chế độ đọc kép)**: Đưa vào kho toàn cầu của `6` Đại Thư Viện (`LIB-01..04, 11, 12`, thuê `$8` / mua `$35–$60`) và phân vào kệ chuyên đề phù hợp tại `9` Nhà Sách Nhỏ (`LIB-05..10, 13..15`, thuê `$4–$5` / mua `$20–$45`).
4. **Atomic Apply & Guarded Rollback**:
   - Chỉ giữ khóa `EagleCoordLock("game-write", ...)` trong vài giây đồng bộ vào `gameplay-lab`, lưu manifest SHA-256 trước/sau và sinh script khôi phục an toàn theo từng `work_id` (gỡ 1 bộ phim/sách ra không ảnh hưởng đến engine hay các bộ khác).

#### Phần 2: Triển khai & Nghiệm thu In-Game Bộ Phim Đầu Tiên — *Re:Zero: Pride IF (`rezero_ayamatsu_pride_if`)*
Ngay khi đủ điều kiện cổng chặn cho `D:\Eagle Literature Studio\packages\rezero_ayamatsu_pride_if\` (`6` chương, `21` cảnh, `803` beats, `50` CGs, `8` BGMs):
1. **Phân bổ Lịch chiếu & Lưu trữ**:
   - Đưa *Re:Zero — Pride IF* lên làm **Phim Tâm Điểm Tuần (Featured Premiere)** tại toàn bộ `6` Đại Rạp (`CIN-01` Vinewood Cathay, `CIN-02` Sakura Multiplex North Chicago, `CIN-03` Akihabara TOHO, `CIN-04` Downtown Chicago, `CIN-11` Wichita Heartland, `CIN-12` Cottonmouth Movie Haus) cùng các Rạp Nhỏ hợp gu Anime/Dark Fantasy (`CIN-06` San Fierro Queens, `CIN-09` Bullworth, `CIN-10` Rose City).
   - Nếu người dùng hoặc chứng chỉ cho phép mở khóa song song chế độ đọc nguyên bản (`supported_read_modes` có cả `adv_cinema` & `nvl_book`), đăng ký thêm bản lưu trữ đọc sách tại Đại Thư Viện Akihabara Kinokuniya (`LIB-02`) và Thư Các Hồ Cider Mondstadt (`LIB-06` — kệ *Fantasy / Teyvat / Re:Zero*).
2. **Nghiệm thu Thực tế DirectX 9 `1920×1080` (Dưới `EagleCoordLock("ingame-runtime")`)**:
   - Khởi động `EagleCompanion.py` + `gta_pe.exe`, dịch chuyển Aether tới rạp chiếu phim (ví dụ `CIN-01` Vinewood hoặc `CIN-03` Akihabara), thực hiện và chụp ảnh màn hình DirectX 9 kiểm tra bằng mắt thật (`read_file`) đủ các bước:
     1. Poster *Re:Zero: Pride IF* hiển thị đúng tỷ lệ ngoài rạp / trong Sảnh rạp.
     2. Quầy vé hiển thị đúng tên phim, tóm tắt, giá vé và các suất chiếu trong ngày; mua vé + bắp nước thành công.
     3. Bước vào Phòng chiếu 3D, đi tới ghế ngồi nhấn `[E]` mở trình chiếu `adv_cinema`.
     4. Hình ảnh CG mở đầu Ch.1, cảnh chuyển tiếp `_base -> _diff`, cảnh cao trào Ch.6 hiển thị sắc nét `16:9` không méo, chữ phụ đề lớn rõ không lỗi ký tự `CFont`, chế độ `Auto-Play [A]` chạy mượt, kênh nhạc `lit_bgm` báo `mci_ok = true` và âm thanh ồn ngoài phố đã được mute sạch.
     5. Đổi thử sang chế độ `nvl_book` (`[V]` hoặc tại `LIB-06`) kiểm tra dàn trang văn xuôi & lưu `bookmark`.
     6. Bấm thoát trình chiếu: xác nhận Aether vẫn đứng trong Phòng chiếu 3D -> đi bộ qua cửa `EXIT` ra Sảnh rạp -> đi bộ ra cửa chính về lại ngoài phố, âm thanh GTA khôi phục bình thường.
     7. Xác nhận `EagleLuaErrors.log = 0` lỗi mới, `eagle_doctor 11/11 PASS`, và dọn sạch tiến trình + giải phóng khóa trong `finally:`.

### 3. Bàn giao về Hội thoại Orchestrator
- Tạo và cập nhật phiếu công việc `docs\project-eagle\work-items\2026-11-06-antigravity-lit-integrate-rezero-pride-if.md` sang trạng thái `done` (hoặc `staged_waiting_gate` nếu đang chờ Builder/Reviewer).
- Ghi báo cáo nghiệm thu ngắn gọn kèm danh sách ảnh chụp DirectX 9, hash manifest và lệnh rollback để **Orchestrator (`199f0287-723d-43b5-a013-d519137afba4`)** review và chốt nghiệm thu đợt phát hành đầu tiên.
```
