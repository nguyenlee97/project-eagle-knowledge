# Báo Cáo Kiểm Thử Thực Tế Trong Game (In-Game Forensic Audit) — Quần Đảo Nhật Bản `WIBU-01` & Đại Cầu Seto Ohashi

- **Ngày thực hiện**: `2026-10-25`
- **Hội thoại kiểm thử**: `7251e9e7-9b8c-48c0-8cee-c5d25efec8dc` (kiểm thử sản phẩm của hội thoại `ccf7de5c-1bef-4e05-8b2b-ddc63edbe1e1` — *Xây Dựng Quần Đảo Nhật Bản WIBU-01*)
- **Môi trường**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\gta_pe.exe` (`PID 11356`, `gGameState = 9 GS_PLAYING_GAME`, `CPlayerPed = 0x22BFF7E4`)
- **Công cụ sử dụng**: Bộ [`eagle_doctor.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_doctor.py) & [`eagle_ingame_tester.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ingame_tester.py) (Pre-Flight Doctor, Live RAM Scene & Streaming Auditor, Bot Physics Route Crawler, Visual Contact Sheet, Camera Look-At X-Ray).

---

## 1. Tóm Tắt Kết Quả Thực Tế Trong Game (`In-Game Verdict`)

| Hạng mục kiểm thử In-Game | Khu vực / Tọa độ | Kết quả | Bằng chứng thực tế trong RAM & Engine |
| :--- | :--- | :---: | :--- |
| **1. Pre-Flight Doctor (11 bước)** | Toàn bộ `gameplay-lab` | **`11/11 PASS`** | `0 WARN, 0 FAIL` (`128 ms`), `CUSTOM\wibu01_japan_island.img` + `.ide` + `.ipl` đồng bộ `100%`. |
| **2. Live RAM Scene Audit (5 phân khu)** | Cầu Seto Ohashi -> Ocean Citadel -> Akihabara -> Sakura Blvd -> Kerorin | **`5/5 PASS`** (`55` static models) | `100%` model `.DFF`, `.TXD`, `.COL` trong bán kính `60m` đã nạp vào bảng `CModelInfo::ms_modelInfoPtrs` (`0x03F28020`) và `CStreaming::ms_aInfoForModel` (`0x041AB020`) với `0` lỗi thiếu mesh/texture/collision. |
| **3. Vá lỗi `BUG-011` (`wb_gg_n03` Invisible Wall)** | Nhịp Bắc Cầu Seto Ohashi `(-1402.56, -3404.41 -> -3416.76, Z=56.15m)` | **`PASS (100% Đã thông)`** | Bot điều khiển Aether chạy thẳng qua tọa độ `(-1402.56, -3407.39, 56.02)` (`PASS \| Smooth traversal OK`), chứng minh bức tường tàng hình `Face 271` (do lỗi lệch header `COL3` `116B` cũ) đã biến mất hoàn toàn trong vật lý GTA SA thực tế. |
| **4. Giao thông NPC & Xe cộ (`FLA4` `nodes1822..1630.dat`)** | Trạm thu phí Bắc/Nam & Đại lộ Akihabara `Chuo-dori` | **`PASS`** | Quét `CPedPool` và `CVehiclePool` trong RAM tại `Chuo-dori` ghi nhận **`11` NPC động** (ped anime/custom đi bộ đúng trên vỉa hè) và **xe NPC** (Rancher SUV `ID 489` chạy qua trạm thu phí), không có xe nào lao xuyên tường tòa nhà. |
| **5. Camera Look-At X-Ray & Mỹ thuật 3D** | Đại lộ Akihabara `Chuo-dori` `(-1390.38, -4615.00, 24.40)` | **`PASS`** | Tia nhìn Camera khóa trúng `laox_thedigitalkan.dff` (`ID 11860`, TXD `akihabara_town`, `COL=1218F/0B`), hàng đèn đường `lamppost2` (`ID 1290`) và cây hoa anh đào `sakura_tree_01..02` hiển thị sắc nét, đúng cao độ mặt đường. |
| **6. Phát hiện Bug Mới Chỉ Xuất Hiện In-Game (`BUG-WIBU-RADAR-01`)** | **11 Tile Radar 2D `radar5133..5613.txd`** trong `S&S\Cdimages\default\radar.img` | **`FAIL (Phát hiện In-Game)`** | Cả **11 tile radar 2D** của `WIBU-01` mang header RenderWare version **`0x3FFFFFFF`** (`6.7.63` > giới hạn `0x1803FFFF` `3.6.0.3` của GTA SA). Khi vào khu vực `WIBU-01`, hàm `RwStreamFindChunk` (`0x007ED2D0`) từ chối nạp với lỗi `E_RW_BADVERSION`, khiến: **(a)** Minimap 2D từ `Y < -2500` hiển thị toàn màu nước biển xanh rỗng, và **(b)** `CRadar::StreamRadarSections()` + `CStreaming` rơi vào **vòng lặp nạp lại vô tận mỗi khung hình (`876,000+` lần)**, ghi tràn **`33.29 MB`** vào `fastman92limitAdjuster.log` và gây nghẽn I/O luồng chính khi đứng lâu tại trung tâm Akihabara! |

---

## 2. Phân Tích Chi Tiết Bug In-Game Mới Phát Hiện: `BUG-WIBU-RADAR-01` (`rw_ver = 0x3FFFFFFF` Streaming Thrash Loop)

Đây là minh chứng điển hình cho việc **tại sao kiểm thử offline không thể thay thế kiểm thử In-Game**:

### 2.1. Tại sao bộ test offline trước đó báo `PASS`?
- Trong quy trình đóng gói `WIBU-01`, 11 tile radar (`radar5133.txd`, `radar5228.txd`, `radar5229.txd`, `radar5324.txd`, `radar5325.txd`, `radar5420.txd`, `radar5421.txd`, `radar5516.txd`, `radar5517.txd`, `radar5612.txd`, `radar5613.txd`) có kích thước chuẩn `34,816 bytes`, đúng chunk type `0x16` (`rwID_TEXDICTIONARY`), đúng 1 texture `DXT1 256×256` (`32,768 bytes`). Vì vậy các trình kiểm tra cấu trúc `.IMG`/`.TXD` tĩnh đều báo hợp lệ.

### 2.2. Điều gì thực sự xảy ra bên trong `gta_pe.exe` khi chơi?
1. Khi quét toàn bộ **9,216** mục trong `S&S\Cdimages\default\radar.img`:
   - **9,205** tile gốc của Project Eagle có RenderWare Version Stamp = **`0x1803FFFF`** (`RenderWare 3.6.0.3` chuẩn GTA SA).
   - Duy nhất **11 tile `WIBU-01`** (`radar5133..5613.txd`) có RenderWare Version Stamp = **`0x3FFFFFFF`** (tương ứng version giải nén `0x3FFFF` = `6.7.63`).
   - Lưu ý: Toàn bộ `178` file `.dff` và `10` file `.txd` trong `CUSTOM\wibu01_japan_island.img` đều dùng đúng `0x1803FFFF`, nên cảnh vật 3D hiển thị hoàn hảo.
2. Khi nhân vật chính Aether đi vào cầu Seto Ohashi và đảo Akihabara (`Y = -2700..-5500`):
   - Mỗi frame, `CRadar::StreamRadarSections()` yêu cầu nạp các tile radar xung quanh người chơi (`ID 212528` = `radar5133.txd`, ..., `ID 212847..213061` = `radar5420..5613.txd`).
   - `CStreaming` đọc dữ liệu từ `radar.img` và gọi `CTxdStore::LoadTxd` -> `RwTexDictionaryStreamRead` -> `RwStreamFindChunk` (`0x007ED2D0`).
   - Tại `0x007ED2D0`, RenderWare kiểm tra `if (version > 0x36003) return FALSE (E_RW_BADVERSION)`.
   - Do `CTxdStore::LoadTxd` trả về `false`, `CStreaming::ConvertBufferToObject` hủy nạp và đặt lại `m_nLoadState = 0` (`LOADSTATE_NOT_LOADED`).
3. **Hậu quả kép trong Runtime**:
   - **Lỗi hiển thị (Visual Bug)**: Trên góc trái màn hình (xem ảnh chụp thực tế tại Trạm Thu Phí Bắc và Akihabara `Chuo-dori`), phần bản đồ radar 2D phía Bắc `Y > -2500` (`radar5037.txd`, `0x1803FFFF`) vẫn vẽ bờ biển bình thường, nhưng toàn bộ phần cầu Seto Ohashi và đảo `WIBU-01` phía Nam `Y < -2500` (`radar5133..5613.txd`) bị rỗng (chỉ hiện nền nước biển xanh).
   - **Lỗi hiệu năng / Treo I/O (Streaming Thrash Loop)**: Vì `m_nLoadState` luôn quay về `0`, ngay ở frame kế tiếp (`16.6ms` sau), `CRadar::StreamRadarSections()` lại gọi `CStreaming::RequestModel()` cho cả 6 tile (`radar5420, 5421, 5516, 5517, 5612, 5613`). Trong 3 phút chạy thử nghiệm, `fastman92limitAdjuster.asi` đã ghi đồng bộ **`876,000+` dòng** lặp đi lặp lại vào `fastman92limitAdjuster.log` (làm phình file log lên **`33,290,621 bytes` / `33.29 MB`**):
     ```text
     Loaded ID 212847, file radar5420.txd
     Loaded ID 212848, file radar5421.txd
     Loaded ID 212953, file radar5516.txd
     Loaded ID 212954, file radar5517.txd
     Loaded ID 213060, file radar5612.txd
     Loaded ID 213061, file radar5613.txd
     ```

### 2.3. Hướng khắc phục (Chỉ 1 thao tác vá 6-chunk header)
- Trong 11 file `radar5133..5613.txd` thuộc `S&S\Cdimages\default\radar.img`, thay đúng 6 vị trí version stamp `ff ff ff 3f` (`0x3FFFFFFF` ở các offset byte `8, 20, 36, 48, 32920, 32932` của mỗi file `34,816` byte) thành **`ff ff 03 18`** (`0x1803FFFF`, giống hệt `radar5132.txd`).
- Bộ công cụ [`eagle_ingame_tester.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ingame_tester.py) đã được bổ sung thêm bộ dò tự động `RADAR_TXD_BAD_RW_VERSION_STREAMING_THRASH` trong `audit_live_scene_streaming` để tự động bắt lỗi này ở mọi vùng bản đồ mới về sau.

---

## 3. Chi Tiết Kiểm Thử 5 Phân Khu Trong RAM (`eagle_doctor.py --audit-scene`)

1. **Nhịp Bắc Cầu Seto Ohashi & Điểm Vá `BUG-011` (`-1402.56, -3404.41, 56.15`)**:
   - `wb_gg_n03.dff` (`ID 11930`, TXD `wb_goldengate`): `ram_dff_loaded = True`, `ram_txd_loaded = True`, `ram_col_loaded = True` (`col_triangles = 308`).
2. **Đài Ngắm Cảnh Giữa Biển — Central Ocean Citadel (`-1395.00, -3745.60, 36.05`)**:
   - `7/7` static models (`abase1..3`, `wb_gg_n06..s06`, `lamppost2`...) đều `DFF=OK, TXD=OK, COL=OK`.
3. **Đại Lộ Trung Tâm Akihabara `Chuo-dori` (`-1390.38, -4650.00, 24.40`)**:
   - `24/24` static models (`akihabara_road`, `laox_thedigitalkan`, `sega_akihabara_building`, `sofmap_building`, `gamers_main_store_akihabara`, `sakura_tree_01..02`, `lamppost2`...) đều `DFF=OK, TXD=OK, COL=OK`.
   - `11/11` NPC động trong `CPedPool` và `1/1` xe trong `CVehiclePool` đều có `rw_object != 0` (`ram_rendered = True`) và `ram_txd_loaded = True`.
4. **Đại Lộ Hoa Anh Đào, Kawaiiboutique & Lâu Đài Nhật Bản (`-1390.38, -4860.00, 24.25`)**:
   - `13/13` static models (`kawaiiboutique_wibu`, `jp_castle_wibu`, `sakura_tree_01..03`, `akihabara_road`...) đều `DFF=OK, TXD=OK, COL=OK`.
5. **Khu Đô Thị Nam Đảo Kerorin Capital (`-1390.38, -5020.00, 24.45`)**:
   - `10/10` static models (`kero_road`, `kero_bldg*`, `lamppost2`...) đều `DFF=OK, TXD=OK, COL=OK`.
