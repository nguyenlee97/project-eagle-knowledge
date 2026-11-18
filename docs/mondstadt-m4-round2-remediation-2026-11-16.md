# Báo Cáo Bàn Giao — Mondstadt M4 Round-2 Remediation (16/11/2026)

- **Ngày thực hiện:** `2026-11-16`
- **Agent:** Antigravity (`58ec5ee3-3fb5-4cba-becc-912ab6e8f1c4`)
- **Work-Item:** `docs/project-eagle/work-items/2026-11-16-fix-m4-mondstadt-round2.md`
- **Staging & Rollback:** `D:\GTA Archive\Staging\fix-m4-round2-20261116`
- **Đích triển khai:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

---

## 1. Tóm Tắt 6 Hạng Mục Đã Xử Lý Triệt Để

### 1.1. Cửa quán rượu sát bên Hiệp Hội Mạo Hiểm & Xóa Ped trùng Kaeya / Joker / Hu Tao (Ảnh 1)
- **Nguyên nhân:** Mũi tên vàng `MD_TAI` (`Quán Rượu Đuôi Mèo`) trước đó đặt nhầm bên phải trục đường chính tại tiệm lưu niệm Marjorie (`-4210.15, -3028.15, 8.475`); ngoài ra `MondstadtLifeAndBlips.cs` (`STATIONARY_CITY_NPCS[7]`) dùng nhầm `Ped 211` (`wfyclot` = skin **Kaeya**), `Ped 274` (**Hu Tao**), và `Ped 172` (`LCS_HOODS02` = **Joker** vest đỏ).
- **Khắc phục:**
  - Chuyển `MD_TAI` trong `CUSTOM/mondstadt_m1_wilds.ipl` sang đúng bậc cửa trước **tòa nhà thứ 2 ngay sát bên quầy Hiệp Hội Mạo Hiểm**: vào `(-4218.750, -3041.550, 8.480)`, bước ra `(-4217.200, -3040.350, 8.380, hdg=325.0)`.
  - Đồng bộ blip radar trong `MondstadtLifeAndBlips.cs` (`48` Cat's Tail -> `-4218.75, -3041.55`; `17` Angel's Share -> đúng cửa hẻm bắc `MD_ANG` `-4215.87, -2968.47, 10.48`), tọa độ `Margaret`, `Diona` `outdoor_gps` và POI trên bản đồ.
  - Gỡ bỏ hoàn toàn `Ped 211` (Kaeya), `Ped 274` (Hu Tao), `Ped 172` (Joker) và thay bằng bộ skin ped anime/fantasy sạch đã kiểm chứng trong `deployment/state.json`.

### 1.2. Khôi phục 100% Collision Tường / Mái / Lan Can Nội Thành M0 (`BUG-013`, `BUG-014` & bay `rocketman`)
- **Nguyên nhân gốc rễ:**
  1. Trong `step3_blender_export_city.py`, hàm `has_alpha_link` bắt nhầm kênh `Alpha -> Fac` (chứa Specular/AO của vật liệu PBR Genshin trong Blender), khiến **~75% vật liệu tường đá đặc** (`Area_MdBuild_Wall08`, `Area_Mdbuild_Wall06`, `Area_MdBuild_House_Wall07`, `Area_MdBuild_KnightHQ02_Assembly01`, `Area_Mdbuild_Stage01`, `Area_MdBuild_Square01`) bị gắn cờ `tri_flags = 0` (không có collision).
  2. Trần cắt đơn chunk `4,700` mặt + lọc tường `> +5.5m` làm mất thêm các mảng tường tầng trên khi bay `rocketman`.
- **Khắc phục:**
  - Biên dịch đầy đủ **`169,476` mặt `COL3` đặc** (`99,310` mặt tường đứng + `66,420` mặt sàn/bậc thang/mái) cho toàn bộ thành Mondstadt M0, chia qua `7` model chính (`6710..6718`) + `37` static collision helper (`12390..12426`, `mc0_c*`), mỗi chunk `<= 4,450` mặt và `<= 83,924B < 92,768B` (`fastman92` safe).
  - Nhúng đồng bộ `mondstadt_m0_city.col` vào bên trong `mondstadt_m0_city.img` (chặn tuyệt đối lỗi `0x00534134` `_LinkLods`).

### 1.3. Cầu thang Trụ Sở Đội Kỵ Sĩ Tây Phong & Vị trí Noelle (Ảnh 2)
- **Nguyên nhân:** Cầu thang `6712` xoay góc `18.18°`, bên dưới tồn tại tấm cỏ sân lớn (`298668..298669` ở `Z = 32.51m`, thuộc `6713`) và tấm nền đá (`98750`, `118370` ở `Z = 32.40..32.65m`), trong khi mặt bậc thang `Area_Mdbuild_Stage01` bị mất collision do lỗi `Fac` ở mục 1.2 -> Aether và Noelle lọt xuống đứng ở `Z = 32.53m` ngang bụng dưới gầm bậc thang.
- **Khắc phục:**
  - Cắt sạch phần sàn ngầm `Z = 32.10..33.18m` nằm dưới chân cầu thang & hiên Đội Kỵ Sĩ bằng phép cắt đa giác chính xác theo hệ trục xoay `18.18°` (giữ nguyên 100% bãi cỏ hai bên hông).
  - Hàn liền mạch sân đá phẳng (`Z = 32.400m`) -> dốc trượt phẳng xoay đúng `18.18°` (`Z = 32.400m -> 35.046m`) -> sảnh hiên trên (`Z = 35.046m`) + vách chắn hai bên thành lan can; nâng mũi tên `MD_KNI` lên đúng mặt hiên `Z = 35.050m`.
  - Đưa `Noelle` (`-4345.60, -3028.80, 32.40`) và điểm bước ra của `MD_KNI` (`-4345.60, -3031.40, 32.42`) ra quảng trường đá phẳng phía trước chân cầu thang.

### 1.4. Chuyển toàn bộ 18 Rương Trang Trí Tĩnh thành Rương Mở Được `[E]` (Ảnh 3)
- **Nguyên nhân:** Có `18` rương (`3` ở M1 gồm `6815 m1_starfell_lk` trong Ảnh 3 + `15` ở M2) là submesh tĩnh (`MSR_543920..543924`) nướng cứng bên trong file `.dff` của landmark nên `MondstadtTreasureChests.cs` không nhận diện được; ngoài ra cổng thành có 2 rương `6692` xếp chồng lên nhau.
- **Khắc phục:**
  - Tách bỏ toàn bộ `18` submesh rương tĩnh khỏi cả near `.dff`, LOD `.dff` và `.col` của M1 (`6810, 6813, 6815`) và M2 (`12060..12062, 12064..12071, 12075..12078`).
  - Khử trùng lặp rương cổng thành (trả `CHEST_05` về đúng Springvale `-4176.0, -3442.0` ngay tại đúng dòng IPL cũ để không lệch bất kỳ chỉ số LOD nào) và đặt đầy đủ instance tương tác `6691..6695` (`chest_*`) -> tổng cộng **`40` rương mở được bằng `[E]` (`18` M1 + `22` M2), `0` rương trang trí chết**, tăng bán kính nhận `[E]` lên `3.45m`.

### 1.5. Đưa Fischl & Ped Cổng Thành Ra Khỏi Tường Thành (Ảnh 4)
- **Nguyên nhân:** Tọa độ cũ của `Fischl` (`-4185.93, -3044.59`) và `STATIONARY_CITY_NPCS[5]` (`Ped 172` tại `-4183.00, -3044.00, Z=8.26`) trùng đúng pháo đài cổng Bắc của mesh thành Blender mới.
- **Khắc phục:** Đưa `Fischl` + `Oz` ra quảng trường đá thoáng trước Hiệp Hội Mạo Hiểm (`-4206.80, -3045.20, 6.37`, cách tường `7.01m`), đồng thời rà soát toàn bộ `26` NPC dân thành phố đảm bảo cách tường `>= 1.57m` và đứng chuẩn trên mặt `.COL3`.

### 1.6. Đồng Bộ Hội Thoại NPC, Trí Nhớ RAG & Rương Theo Từng Slot Save / `New Game`
- **Nguyên nhân:** Phiên chơi `10:52–11:18` diễn ra trước khi `Fix M2` cài `eagle_savegame_sync.py` lúc `11:20`; đồng thời cần khóa chặt WAL checkpoint cho `conversations.sqlite3` và đồng bộ cả trạng thái rương `mondstadt_chests.ini`.
- **Khắc phục:**
  - Rebase trực tiếp trên `eagle_mondstadt_chat_bridge.py` & `eagle_savegame_sync.py` của `Fix M2` (giữ nguyên 100% WaifuLink & `tcg_poi_shop_09` của `M7`).
  - Bổ sung dọn nhánh phụ (`DELETE FROM branch WHERE parent_id IS NOT NULL`) + `PRAGMA wal_checkpoint(PASSIVE/TRUNCATE)` khi `New Game` / `Save` / `Load`, đảm bảo khi **New Game** toàn bộ 14 NPC Mondstadt trống 100% cả **hiển thị UI** (gặp trực tiếp & App #14 Contacts) lẫn **bộ nhớ LLM/RAG** (`turn`, `turn_search` FTS5, `memory`, `summaries`).
  - Gắn `cleo/EagleRide/mondstadt_chests.ini` (`sync_seq`) vào từng slot save `GTAPEsf{N}.b`; khi `New Game` hoặc đổi slot save, `MondstadtTreasureChests.cs` tự động ẩn/hiện lại các rương trong thế giới ngay lập tức mà không cần tắt game.

---

## 2. Kết Quả Kiểm Chứng & Thứ Tự Rollback

- `verify_m4_round2.py --target live`: **`7/7 GATES PASS`**
- `eagle_doctor.py`: **`11/11 PASS, 0 WARN, 0 FAIL`**
- `rollback_m4_round2.py --preflight`: **`PASS`** (`18` file code/archive/CLEO/cache + `1` file data)
- `eagle_coord_lock.py status`: **`{"game-write": null, "ingame-runtime": null}`**

### Thứ tự Rollback phân lớp trên `gameplay-lab` (mới nhất gỡ trước):
1. `python -X utf8 "D:\GTA Archive\Staging\fix-m4-round2-20261116\rollback_m4_round2.py" --apply`
2. `python -X utf8 "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\fix-m2-doors-and-savesync-20261116\rollback_m2_doors_and_savesync.py" --execute`
3. `python -X utf8 "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\fix-00534134-mondstadt-m0-col-img-20261116\rollback_00534134_fix.py" --apply`
4. `python -X utf8 "D:\GTA Archive\Staging\fix-m4-mondstadt-20261116\rollback_m4_mondstadt.py" --apply`
