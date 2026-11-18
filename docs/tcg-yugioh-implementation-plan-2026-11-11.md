# Kế Hoạch Triển Khai Chi Tiết: `TCG Card Shop Simulator × Dan's YuGiOh Expansion v4.1.1` Trên `gameplay-lab`

- **Ngày lập kế hoạch:** `2026-11-11`
- **Agent thực hiện:** Antigravity (`6a2335a6-d5d7-47e6-9128-fbc62404a3a8`)
- **Tài liệu TDD gốc:** [tcss-yugioh-detailed-technical-design-2026-11-11.md](tcss-yugioh-detailed-technical-design-2026-11-11.md)
- **Trạng thái:** Đang chờ người dùng duyệt Plan (`Awaiting Approval`).

---

## 1. Chiến Lược Điều Phối Thứ Tự & Song Song Hóa (4-Track Parallel DAG)

1. **`Phase 0` (Tuần tự — Làm đầu tiên):**
   - `T0.1`: Đăng ký phiếu công việc thực thi & khởi tạo `D:\GTA Archive\Staging\project-eagle\tcg-yugioh-20261111\` + `gameplay-lab/data/project-eagle/tcg_yugioh/`.
   - `T0.2`: Khóa cứng hợp đồng kỹ thuật chung (`tcg_contracts.py` / `tcg_schema.sql`: `15` bảng SQLite, `REST API` `/api/tcg/*` + `7` endpoint `YgoDuelTable`, dải Static Model ID `15250..15309`, tọa độ `Area Code = 1` `(2200..3550, -2650, 1650)`, khe nhớ `0x00CAFE80` `'ETCG'`, và mã `12` cửa hàng).
2. **`Phase 1` (4 Luồng Chạy SONG SONG Độc Lập 100% Ngoài Khóa — `0` Đụng File Chung):**
   - **`Track A` (`T1.A1..T1.A4` — Tài nguyên SSD `C:` & `ygo_catalog.db`):** Giải mã `136` UnityFS v8 LZ4 bundles của `Dan's YuGiOh Expansion v4.1.1` + phụ kiện thực tế/SFX của TCSS; nén đa luồng `13,544` mặt bài (`cards_webp/`), `7,529` `FoilMask` (`foils_webp/`), `136` vỏ gói (`packs_webp/`), copy `duel_web/` (`ocgcore` WASM MR5 + `cards.cdb` + `13,323` Lua scripts + `96` Anime `.ydk` decks) sang SSD `C:` (`~1.86 GB` / `39.05 GiB` trống) và tạo `ygo_catalog.db` theo công thức `PullRatePrices` EV.
   - **`Track B` (`T1.B1..T1.B5` — Lõi Python 64-bit `eagle_tcg_engine.py`):** Kho đồ 3 tầng `EagleInventory`, Gacha `SlotWeights` + khóa độc bản `tcg_pulled_1of1` + chấm điểm `TCG 1..10`, mô phỏng ngày `08:00–21:00` (tồn kho thật `qty == 0 -> $0`, `8` hạng ví + `Ultra-Whales`, năng suất `Cashier` + thuộc tính ngầm `OT`, tự động hóa `Restocker`, `Trade Inbox` có deadline `3–5` ngày, `shop_daily_logs`), chu kỳ tháng `30` ngày (`PriceChangeManager` + `shop_monthly_bills`), làm mới tiệm NPC theo vùng, giải đấu `8/16/32` người và kiểm thử toán học offline `10,000` pack + `90` ngày.
   - **`Track C` (`T1.C1..T1.C4` — Sidecar `WebView2` Borderless + Xé Pack 3D `60 FPS` + Đấu Bài UI):** Trình chứa Evergreen WebView2 (`157.0.4341.42`) bám khít `16:9` `gta_pe.exe`, `pack_ripper_webgl.js` (kéo chuột xé mép vỏ + shader GLSL `22` cấp Holo `FoilMask`), giao diện `Customer POV` & `Owner POV`, Sổ `Card Binder` + trình lắp Deck `.ydk` (`>= 40` lá) đấu nối thẳng bàn đấu `duel_web/`.
   - **`Track D` (`T1.D1..T1.D3` — `12` Địa điểm Bản đồ, `4` Interior Tĩnh `Tier 1..4` & Cầu CLEO/Lua):** Khảo sát raycast `.COL` `12` tiệm (`>= 50m` cách các cổng cũ), chuyển đổi kệ/tủ kính bài tĩnh/bàn đấu/máy xé/máy xịt/`Dueling Computer.glb`/Loa `RadioEx` qua Blender 5.0 sang `CUSTOM/eagle_tcg_interiors.{img,ide,ipl,col}`, biên dịch `cleo/EagleTcgBridge.cs` (`0x00CAFE80`) & `cleo/EagleTcgDirector.lua` (`9` nhân viên `fixed_ped_id`, khách Ambient `60` skin, đám đông xem giải đấu, bấm `[E]` đổi đài `RadioEx`).
3. **`Phase 2` (Tuần tự — Giữ `game-write.lock`):**
   - `T2.1`: Chụp SHA-256 `Before` & tạo sẵn `rollback_tcg_yugioh_integration.py` có guard.
   - `T2.2`: Đấu nối `App #15: EagleBiz` vào ô số `15` trên `EaglePhone OS v6.3` (`eagle_phone_ui.py`, `hud.lua`, `models/hud.txd`, `CUSTOM/EAGLEPHONE_UI.TXD`).
   - `T2.3`: Đấu nối `EagleCompanion.py` (`0x0053F509` khóa chuột camera, `NeoBank`/`WalletStore`) & `eagle_savegame_sync.py` (`EagleTcgSlot{1..8}.sqlite` + `New Game` reset).
   - `T2.4`: Khai báo `data/gta.dat`, đăng ký `12` POI vào `eagle_gg_map_pois.py` & `eagle_ride_engine.py`, kiểm tra `py_compile` và nhả ngay `game-write.lock`.
4. **`Phase 3` (Tuần tự — Kiểm Thử `Part A` + `Part B Live DirectX 9` dưới `ingame-runtime.lock`):**
   - `T3.1`: Gate `Part A Offline` + `rollback --preflight` + `eagle_doctor.py` (`11/11 PASS`).
   - `T3.2`: `Part B1` Live DirectX 9 `1920×1080` cho **`Customer POV`** (Ngày 1 mua Pack -> xé Pack 3D -> đủ 40 lá xếp Deck `.ydk` -> đánh thắng ván `8,000 LP` `ocgcore` & dự giải).
   - `T3.3`: `Part B2` Live DirectX 9 cho **`Shop Owner POV`** (Mua đứt tiệm -> nhập sỉ, định giá, thuê nhân viên kiểm chứng `fixed_ped_id` trong 3D, đổi nhạc Loa `RadioEx`, nâng cấp `Tier 1 -> 4`, kiểm chứng `shop_daily_logs` / `Trade Inbox` / Hóa đơn 30 ngày / Save-Load `GTAPEsf{N}.b`).
   - `T3.4`: Viết báo cáo bàn giao cuối cùng và đóng phiếu công việc.
