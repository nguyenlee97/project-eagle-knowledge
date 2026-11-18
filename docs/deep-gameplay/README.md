# Nghiên cứu Kỹ thuật & Kiến trúc Mod Gameplay Sâu — Project Eagle v1.3

> **Cập nhật quan trọng ngày 22/10/2026 (Sau Merge & Chuyển ổ):**
> - Bản chơi và đích phát triển feature mới duy nhất hiện nay là **[`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab)** (đã hợp nhất Loading Wibu World, Main Menu Wibu 32 file, NPC `COMPONENTPEDS.img` sửa rig 32/32, Aether, Radio Custom, `EaglePhone OS v5.0`, `GG Map` và các gói mod Nhóm A/B1/B3).
> - Bản `gta sa clean` và `Skin Library` đã chuyển vật lý sang ổ `D:\GTA Archive\...` (đường dẫn cũ trên C là NTFS junction chỉ để lưu trữ/tham chiếu, **không dùng `clean` làm đích build hay cài mod**).
> - Mọi tác vụ của **Codex** và **Antigravity** phải tuân thủ **[Quy ước phối hợp chung (`shared-agent-workflow.md`)](../shared-agent-workflow.md)**, đọc **[Bàn giao sau merge & chuyển ổ (`storage-migration-and-lab-handover-2026-10-22.md`)](../storage-migration-and-lab-handover-2026-10-22.md)**, **[Báo cáo Merge (`merge-clean-to-gameplay-lab-2026-10-22.md`)](../merge-clean-to-gameplay-lab-2026-10-22.md)** và **[Hồ sơ kỹ thuật Lab (`gameplay-lab-current-status-2026-10-22.md`)](../gameplay-lab-current-status-2026-10-22.md)**.

- **Ngày khảo sát ban đầu:** 14/10/2026 (Asia/Saigon)
- **Game mục tiêu hiện tại:** [`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab) (Project Eagle v1.3, build `Jun 15 2026`, trên nền `GTA SA v1.0 US HOODLUM` 32-bit)
- **Lưu ý lịch sử:** Các tài liệu `01` $\rightarrow$ `05` bên dưới được viết ở giai đoạn khảo sát ban đầu (14/10/2026) trên thư mục gốc trước khi lập Lab; kiến trúc binary/engine vẫn giữ nguyên giá trị tham khảo kỹ thuật.

---

## Mục lục Bộ Tài liệu Kỹ thuật (`docs\project-eagle\deep-gameplay\`)

1. **[`01-identity-and-engine-architecture.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/deep-gameplay/01-identity-and-engine-architecture.md)**
   - Bảng định danh binary & mã băm SHA-256 đầy đủ.
   - So sánh byte-by-byte giữa `gta_sa.exe` và `gta_pe.exe` (chứng minh `.text` giống hệt 100%, chỉ khác 780 bytes chuỗi cấu hình/save prefix `GTAPEsf` và icon).
   - Giải mã 38.083 symbols từ `gta_sa.pdb` đi kèm bộ cài.
   - Giải phẫu 22 mô-đun bên trong `PECore.asi` (bảng địa chỉ hook thực tế, Dear ImGui 1.90.5, `SaveSideloader`, `StatExtender`, `IplExt`, `RadioEx`, `ZoneEx`, và 6 custom CLEO opcodes `0x3200..0x3212`).
   - Giới hạn thực tế của `$fastman92limitAdjuster.asi` (FLA 7.7), lý do `modloader.asi` tắt `gta3.std.stream=0`, phạm vi HUD thuần túy của `SanViveLuaHudSA.asi` (`hud.lua`), và chẩn đoán 9 crash logs (`8/9` là lỗi thoát game `LdrShutdownProcess` trong `std.data.dll`).
2. **[`02-eagle-feature-map-and-scm.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/deep-gameplay/02-eagle-feature-map-and-scm.md)**
   - Giải phẫu `data\script\main.scm` (`4,849,743` B, `15,990` biến toàn cục, `255` luồng `03A4`, bảng symbol 5.598 biến Sanny Builder ở cuối file) và `data\script\script.img` (`89` streamed scripts).
   - Bản đồ đầy đủ các hệ thống gameplay đã tích hợp sẵn trong Project Eagle v1.3: `STARTGM`, `MENU_INTERACT` (phím `M`), sự nghiệp xe tải `ETS` (có sẵn tính năng ngủ qua ngày, thuê 3 tài xế, 3 gara xe, 4 hợp đồng), `pefoods.scm`, `usaplane.scm`, `X_ASSETS`, `PEBPROPERTY`, `X_HOTEL`, `X_PAGER` (`0x3200`), `OTB`.
   - **Đính chính quan trọng qua giải mã bytecode SCM:** Luồng `X_ATM` (`0x055946..0x05E05E`) chỉ là script đập vỡ cây ATM (`model 2942` $\rightarrow$ `3067`) rơi `\$300..\$500`, **không phải** hệ thống tài khoản ngân hàng.
3. **[`03-extension-points-and-community-mods.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/deep-gameplay/03-extension-points-and-community-mods.md)**
   - So sánh 6 tầng mở rộng kỹ thuật (C++ ASI `plugin-sdk`, `PECore.asi` API/opcodes, `CLEO 5.0.3`, `SanViveLuaHudSA.asi`, `main.scm`, và `External Sidecar Process`).
   - Ma trận phím tắt (Keybind Matrix) để tránh xung đột với `F2`, `M`, `Ctrl+K`, `Alt+V`, `Ctrl+M`, `Ctrl+P`.
   - Bảng khảo sát các bản mod tham khảo trong cộng đồng (`CLEO 5`, `plugin-sdk`, `Grinch_ Cheat-Menu`, `CLEOPlus / Inventory`, `Realistic Fuel`, `Bank/ATM`, `Inside Track / Stock GBM`, `Mantella Sidecar`).
4. **[`04-target-architecture-and-feasibility.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/deep-gameplay/04-target-architecture-and-feasibility.md)**
   - Đánh giá khả thi và giải pháp kỹ thuật cho cả 4 trụ cột: **Life Sim**, **Kinh tế / Chứng khoán / Crypto**, **Vé số & Cá cược Thể thao**, và **AI NPC & Internet**.
   - Thiết kế kiến trúc 3 tầng **`EagleLife` Hybrid Architecture**: `EagleLifeBridge` (trong game, $< 0.3\text{ ms}$/tick) + `EagleCompanion` (tiến trình 64-bit ngoài game xử lý SQLite, thị trường, quyết toán vé cược, LLM/Internet feed) + Cơ chế đồng bộ lưu trữ theo từng Save Slot (`GTAPEsf1..8.b`).
5. **[`05-roadmap-poc-and-evidence-ledger.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/deep-gameplay/05-roadmap-poc-and-evidence-ledger.md)**
   - Lộ trình triển khai 5 giai đoạn (Phase 0 $\rightarrow$ Phase 4) theo lát cắt chơi được ngay.
   - Đề xuất chi tiết **3 phương án PoC đầu tiên** (PoC A, PoC B, PoC C) kèm tiêu chí nghiệm thu.
   - Sổ cái bằng chứng (Evidence Ledger) và danh mục khoảng trống (Gap List).
6. **[`06-gameplay-lab-and-poc-guide.md`](file:///C:/Users/LENOVO/Desktop/GTA/docs/project-eagle/deep-gameplay/06-gameplay-lab-and-poc-guide.md)**
   - Biên bản tạo bản game cách ly 100% [`gta sa gameplay-lab`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20gameplay-lab) và thư mục save riêng [`Documents\GTA PE Lab Files`](file:///C:/Users/LENOVO/Documents/GTA%20PE%20Lab%20Files).
   - Hướng dẫn chạy và kiểm thử bản kết hợp **PoC A + PoC B (`EagleLifePoC.cs` + `EagleCompanion.py`)** kèm script rollback.
