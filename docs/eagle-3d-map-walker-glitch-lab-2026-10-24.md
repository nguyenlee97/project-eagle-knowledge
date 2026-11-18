# Eagle 3D Map Walker & Glitch Lab — Công Cụ Kiểm Thử Di Chuyển, Walkability & Geometry Glitch 3D (24/10/2026)

## 1. Mục tiêu & Tổng quan kiến trúc

Khi xây dựng và ghép nối các phân khu bản đồ 3D lớn (như **Mondstadt City `M0` + Mondstadt Wilds `M1`** và các vùng Teyvat/Multiverse tiếp theo trong **Project Eagle**), việc đi bộ thủ công trong game hoặc trên trình xem 3D thông thường tốn nhiều thời gian và dễ bỏ sót các điểm lỗi hình học ẩn.

**`Eagle 3D Map Walker & Glitch Lab`** kết hợp hai lớp công cụ trong một quy trình duy nhất:
1. **Bộ Quét Hình Học & Vật Lý Đa Tầng (`Offline Python 3D Geometry & Capsule Physics Engine`)** — [`tools/map-glitch-lab/eagle_map_glitch_lab.py`](file:///c:/Users/LENOVO/Desktop/GTA/tools/map-glitch-lab/eagle_map_glitch_lab.py):
   - Đọc trực tiếp toàn bộ lưới hiển thị Near `.DFF` (`143,441` tam giác / `43` model), lưới va chạm vật lý `.COL3` (`36,558` tam giác / `43` model) và `2,554` vật thể thảm thực vật (`Foliage`).
   - Thực thi **5 bộ quét chuyên sâu (`Scanners A–E`)** trong `~28 giây`, có **bộ lọc bề mặt lộ thiên (`is_buried_underground`)** để loại bỏ `913` mặt đáy vách ngầm (`internal HLOD skirts`) nằm sâu dưới lòng đất, chỉ giữ lại **117 điểm lỗi thực sự lộ thiên trên bề mặt chơi**.
2. **Phòng Thí Nghiệm 3D Tương Tác Độc Lập (`Standalone WebGL Glitch Lab Studio`)** — [`docs/project-eagle/eagle-3d-map-walker-glitch-lab-2026-10-24.html`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/eagle-3d-map-walker-glitch-lab-2026-10-24.html):
   - Nhúng sẵn toàn bộ scene 3D, báo cáo kiểm định `117` điểm lỗi, bản đồ nhiệt vùng đi bộ (`Walkability Heatmap`), đàn robot dò đường trực tiếp (`Live Swarm Bots`), kính X-Ray độ dốc/pháp tuyến (`Phím V`), chế độ bay xuyên tường (`Noclip - Phím G`), súng bắn tia chẩn đoán (`Crosshair Glitch Gun - Phím F / Click phải`), và bảng căn chỉnh/vá vị trí model (`Live Model Nudge & Ground Snap`) xuất trực tiếp ra JSON Patch.

---

## 2. Năm Bộ Quét Tự Động (`Automated Scanners A–E`)

| Bộ quét | Mã phân loại (`type` / `subtype`) | Cơ chế kiểm thử vật lý & hình học | Số điểm lộ thiên phát hiện |
| :--- | :--- | :--- | :---: |
| **Scanner A: Multi-Layer 2.5D Swarm Capsule Walker** | `WALKABILITY_BARRIER` (`SUBMERGED_UNDER_WATER`, `MISSING_COL_VOID`) | Xây dựng đồ thị đi bộ đa tầng `(gx, gy, layer_idx)` bước lưới `2.5m` (để vòm đá/cầu không che khuất đường đi bên dưới). Thả capsule vật lý (`r = 0.32m, h = 1.72m, maxStep = 0.45m, slope <= 45°`) từ Cầu Cổng Thành Mondstadt `(321.0, -93.1)` và Quảng trường `(115.0, -35.0)`, đối chiếu với chế độ nhảy (`jumpStep = 0.95m`), tách các đảo cô lập (`Isolated Islands`) và bắn tia dọc theo khe ngăn cách ngắn nhất để tìm chính xác tọa độ đứt đường. | **4** tuyến chính bị đứt |
| **Scanner B: Multi-Point Footprint Raycast** | `FLOATING_MODEL` (`FULL_FLOATING`, `SLOPE_CORNER_OVERHANG`) | Tách từng model `.DFF` thành các cụm lưới liên thông (`Connected Components`), lọc bỏ các vỏ đá ngầm dưới lòng đất, sau đó bắn tia từ 5 điểm chân đế (`Tâm + 4 góc cực trị X/Y`) xuống lưới `.COL3` bên dưới để đo độ hở chân đế (`min_gap_m`, `max_gap_m`). | **25** cụm vật thể bay lơ lửng |
| **Scanner C: Visual `.DFF` vs Physical `.COL3` Mismatch** | `COLLISION_MISMATCH` (`INVERTED_COL_NORMAL`, `GHOST_FLOOR`, `INVISIBLE_WALL`) | Kiểm tra độ lệch giữa bề mặt `.DFF` và `.COL3` lộ thiên; phát hiện các tam giác va chạm `.COL3` lộ thiên bị lật ngược pháp tuyến xuống đất (`nz < -0.65`) khiến nhân vật bước vào bị lọt xuyên hoặc kẹt chân. | **25** cụm lệch va chạm / ngược pháp tuyến |
| **Scanner D: Void Freefall Traps & Seam Chasms** | `VOID_TRAP` (`BIGWORLD_SEAM_CHASM`, `SEAM_STEP_DISCONTINUITY`, `VOID_FREEFALL_HOLE`) | Quét dọc các đường biên chia mảnh `BigWorld` (`E = +241m`, `N = -227m`, biên `M0 ↔ M1`) và bề mặt đi bộ để phát hiện khe nứt rỗng không có tam giác `.COL3` gây rơi tự do hoặc bậc lệch cao độ đột ngột giữa 2 mảnh địa hình. | **30** điểm (`8` hố nứt biên + `18` bậc lệch biên + `4` lỗ thủng nội bộ) |
| **Scanner E: Path Traps (Step-Lips & Low Headroom)** | `PATH_TRAP` (`STEP_LIP_BLOCKER`, `LOW_HEADROOM_TRAP`) | Phát hiện các gờ bậc thang cao `0.46m–1.25m` (đi bộ thường bị khựng, bắt buộc bấm `Space` để nhảy) và các vị trí khoảng sáng trần `< 1.72m` gây vướng đầu capsule. | **33** điểm (`18` gờ bậc cao + `15` bẫy trần thấp) |

---

## 3. Phát Hiện Cốt Lõi Trên Bản Đồ `Mondstadt M0 + M1`

### 3.1. Chẩn đoán 6 tuyến hành trình tiêu chuẩn (`Swarm Bot Routes`)

| Tuyến kiểm thử (xuất phát từ Cầu Cổng Thành `321.0, -93.1, -55.34`) | Trạng thái | Quãng đường đi được | Khoảng cách còn lại | Tọa độ điểm đứt (`From -> To`) | Nguyên nhân gốc rễ (`Root Cause`) |
| :--- | :---: | :---: | :---: | :--- | :--- |
| **1. Quảng Trường Phong Thần Barbatos (`M0`)** | **PASS** | `212.7m` | `0.0m` | — | Thông suốt hoàn toàn qua cổng thành và cầu thang nội đô `M0`. |
| **2. Đại Giáo Đường Mondstadt (`M0`)** | **PASS** | `284.8m` | `0.0m` | — | Thông suốt hoàn toàn lên đỉnh đồi Đại Giáo Đường `M0`. |
| **3. Rừng Thì Thầm (`Whispering Woods - M1`)** | **BLOCKED** | `363.1m` | `18.2m` | `(515.0, 122.5, -57.47)` $\rightarrow$ `(517.5, 127.5, -57.76)` (dài `5.59m`) | **`SUBMERGED_UNDER_WATER`**: Bot đi bộ trên đường mòn mặt đất xuyên dưới vòm đá `(513, 123)` tới sát đích `18.2m` thì mặt đường tại `(515.42, 123.33)` trũng xuống `Z = -58.13m` (thấp hơn mực nước `-58.00m` đúng **`17.9 cm`**). Chỉ cần nâng cốt mặt đường tại đây lên `+0.35m` là thông tuyến! |
| **4. Thanh Tuyền (`Springvale - M1`)** | **BLOCKED** | `242.9m` | `474.4m` | `(245.0, -210.0, -57.87)` $\rightarrow$ `(240.0, -227.5, -53.65)` (dài `18.2m`) | **`MISSING_COL_VOID` (`BigWorld Seam Chasm`)**: Dọc đường biên Đông–Tây `N = -227m .. -222m` (ranh giới `X_obj = -2048.0` giữa cụm mảnh Bắc `2_-1`/`2_-2` và cụm mảnh Nam `1_-1`/`1_-2`), có một **khe rỗng thiếu tam giác `.COL3` rộng `5m–18m`** (`35/36` mẫu raycast không có mặt đất) kèm độ lệch bậc cao độ `dZ = +4.21m`. Đường nứt này cắt toàn bộ nửa Nam `M1` thành đảo cô lập `Island #1` (`962,637 m²`). |
| **5. Bờ Nam Hồ Cider (`South Cider Lake - M1`)** | **BLOCKED** | `242.9m` | `294.1m` | `(245.0, -210.0, -57.87)` $\rightarrow$ `(240.0, -227.5, -53.65)` (dài `18.2m`) | **`MISSING_COL_VOID` (`BigWorld Seam Chasm`)**: Cùng nguyên nhân với tuyến Thanh Tuyền — bị chặn bởi khe đứt gãy biên `BigWorld` tại `N = -227m`. |
| **6. Bờ Bắc Hồ Cider (`North Cider Lake - M1`)** | **BLOCKED** | `304.5m` | `393.6m` | `(-137.5, 137.5, -13.98)` $\rightarrow$ `(-100.0, 512.5, -7.31)` (dài `376.9m`) | **`MISSING_COL_VOID`**: Vùng bờ Bắc Hồ Cider (`Island #3`, `99,031 m²`) bị ngăn cách với đảo thành phố `M0` bởi lòng hồ Cider và dải bờ Đông/Tây chưa có cầu hoặc dải đất nối trên cao độ `> -58.0m`. |

### 3.2. Phân tích khe đứt gãy biên `BigWorld` (`BIGWORLD_SEAM_CHASM` & `SEAM_STEP_DISCONTINUITY`)
- **Đường biên Đông–Tây `N = -227m .. -222m` (`X_obj = -2048.0`)**:
  - Ngăn cách các mảnh `Stages_BigWorld_2_-1` / `2_-2` (phía Bắc) với `1_-1` / `1_-2` (phía Nam).
  - Phát hiện **8 cụm hố rơi tự do dọc biên (`BIGWORLD_SEAM_CHASM`)** và **18 điểm vênh bậc cao độ (`SEAM_STEP_DISCONTINUITY`, chênh lệch từ `0.8m` đến `5.4m`)**.
  - **Cách khắc phục trong pipeline**: Khi cắt/xuất các mảnh `Stages_BigWorld_*_Constant_HLOD_Lod0`, cần giữ dải chồng lấn (`seam overlap skirt >= 6.0m`) hoặc khâu nối (`stitch seam vertices`) dọc theo đường `X_obj = -2048.0` (`N = -225m`) và `Z_obj = -1024.0` (`E = +241m`).

### 3.3. Top các vật thể bay lơ lửng lộ thiên (`FLOATING_MODEL`)
Bộ quét chân đế đa điểm (`Scanner B`) đã lọc sạch các vách đá ngầm bên dưới mặt đất và chỉ ra **25 cụm vật thể lộ thiên** bị hở chân đế:
- Các cụm đá và công trình phụ trên sườn đồi `M1` thuộc `COL/DFF #6740`, `#6738`, `#6746`, `#6731` có khoảng hở từ điểm thấp nhất của chân đế tới mặt đất `.COL3` bên dưới từ **`0.35m` đến `5.80m`**.
- Trong giao diện `Glitch Lab Studio`, chỉ cần nhấp vào từng mục trong tab **`Lơ lửng (25)`**, camera sẽ dịch chuyển tới sát chân vật thể và bạn có thể bấm nút **`🧲 Tự động hạ chạm mặt đất COL (Snap to Ground)`** để tính ngay độ dịch chuyển `dU` cần vá vào IPL/DFF.

---

## 4. Hướng Dẫn Sử Dụng `Interactive 3D Glitch Lab Studio`

Mở trực tiếp file HTML độc lập (không cần server):
- **Đường dẫn**: [`docs/project-eagle/eagle-3d-map-walker-glitch-lab-2026-10-24.html`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/eagle-3d-map-walker-glitch-lab-2026-10-24.html)

### Các chế độ và phím tắt chính:
1. **1-Click Glitch Playlist & Teleport (Cột trái)**:
   - Lọc nhanh theo nhóm lỗi: `Tất cả (117)`, `Đứt đường (4)`, `Hố rơi / Khe nứt (30)`, `Lơ lửng (25)`, `Lệch COL/DFF (25)`, `Bẫy kẹt / Bậc cao (33)`.
   - Nhấp vào bất kỳ thẻ lỗi nào để **bay camera tới tận nơi**, đóng khung vật thể lỗi và xem thông số chẩn đoán + gợi ý sửa ở cột phải.
2. **Kính X-Ray Độ Dốc & Pháp Tuyến (`Phím V` hoặc checkbox `Kính X-Ray Độ Dốc`)**:
   - Phủ lớp màu chẩn đoán trực tiếp lên toàn bộ lưới va chạm `.COL3`:
     - **Xanh lục**: Mặt đất đi bộ bình thường (`<= 45°`).
     - **Vàng cam**: Sườn dốc gắt phải nhảy (`45°–54.5°`).
     - **Đỏ**: Vách tường chặn đứng (`> 54.5°`).
     - **Tím**: Tam giác `.COL3` bị **lật ngược pháp tuyến (`nz < -0.2`)**.
     - **Xanh dương**: Bề mặt bị ngập dưới mực nước (`< -58.0m`).
3. **Đi Bộ Vật Lý `.COL3` vs Bay Xuyên Tường `Noclip` (`Phím G`)**:
   - Chế độ **Đi bộ (`WALK`)**: Mô phỏng đúng capsule nhân vật GTA SA (`WASD` di chuyển, `Shift` chạy nhanh, `Space` nhảy vượt bậc `<= 0.95m`).
   - Nhấn **`Phím G`** bất kỳ lúc nào để bật **`NOCLIP (Bay xuyên tường)`** giúp thoát khỏi hố kẹt, bay xuyên qua vách núi hoặc kiểm tra mặt dưới địa hình, rồi nhấn **`G`** lần nữa để đáp xuống mặt đất `.COL3`.
4. **Đàn Robot Bầy Đàn Đa Hạt Giống (`Multi-Seed Swarm: 10 Seeds · 100 Bot` + `Phím B` / `Phím H`)**:
   - Thay vì chỉ thả 6 bot đi theo đường thẳng nối mốc, hệ thống gieo **10 Hạt giống (`SEED-01 .. SEED-10`)** khắp các khu vực (`Cầu Cổng Thành M0`, `Quảng Trường M0`, `Đại Giáo Đường M0`, `Tường Thành Đông M0`, `Ngã Ba Rừng Thì Thầm M1`, `Bờ Bắc Đứt Gãy Hồ Cider M1`, `Đảo Đông Bắc Rừng Thì Thầm M1`, `Đảo Nam Hồ Cider M1`, `Thung Lũng Thanh Tuyền M1`, `Cao Nguyên Vách Bắc M1`).
   - Từ 10 hạt giống này, hệ thống phóng ra **100 Bot tự hành** (`20` bot đi theo các tuyến hành trình đích + `80` bot tỏa tròn 8 hướng la bàn `0°..315°` có cảm biến né vật cản nhỏ `±28°`).
   - Kết quả thực tế trên bản đồ `M0 + M1`: Dù 20 tuyến đường chính đã thông suốt (`PASS`), **50 / 80 bot tỏa nhánh (`Radial Swarm`)** khi rẽ khỏi trục đường chính đã bắt sống **50 điểm lỗi địa hình phụ**:
     - `19` bot rơi xuống khe rỗng thiếu `.COL3` (`MISSING_COL_VOID`)
     - `10` bot vướng gờ bậc cao đột ngột (`STEP_LIP_BLOCKER`)
     - `9` bot đụng vách dốc đứng (`STEEP_SLOPE_BARRIER`)
     - `8` bot hụt chân xuống vực sâu không rào chắn (`VOID_CLIFF_DROP`)
     - `4` bot lội xuống vùng trũng ngập nước (`SUBMERGED_UNDER_WATER`)
   - **Thả Hạt Giống Tùy Ý (`Phím H` / `🌱 Thả Seed Mới Tại Tâm Ngắm`)**: Bất kỳ lúc nào bạn đang xem bản đồ, chỉ cần trỏ chuột vào một sườn đồi/ngõ hẹp và nhấn **`Phím H`**, công cụ sẽ lập tức cắm một `SEED-CUSTOM` mới ngay tại đó và phóng **24 Bot vật lý tỏa ra 360°** theo thời gian thực để vạch trần mọi khe hở quanh điểm đó!
5. **Dựng Lại Hành Trình 3D & Đầu Tua Replay DVR (`Bot Journey Replay DVR`)**:
   - Khi nhấp vào bất kỳ Bot nào trong danh sách **`3. ĐÀN BOT ĐA HẠT GIỐNG & DỰNG LẠI HÀNH TRÌNH`** (hoặc nhấp trực tiếp vào hình trụ con Bot trên cảnh 3D):
     - **Chuỗi Vết Chân 3D (`3D Footprint Breadcrumb Trail`)**: Dựng lại toàn bộ từng bước chân `Bước #1 -> #N` của con bot trên mặt đất với mã màu vật lý trực quan:
       - 🟢 **Cầu xanh lục**: Bước đi bộ êm (`WALK_OK`)
       - 🟡 **Cầu vàng cam**: Bước phải nhảy vượt bậc / leo dốc (`JUMP_SCRAMBLE`)
       - 🟣 **Khối bát diện tím hồng + đuôi rơi thẳng đứng**: Điểm hụt chân rơi tự do xuống hố Void (`VOID_FREEFALL`)
       - 🔵 **Khối xanh dương**: Điểm sụt ngập dưới mặt nước (`WATER_SUBMERGED`)
       - 🔴 **Khối đỏ cam + vết bật lùi**: Điểm đụng tường dốc / gờ bậc cao (`STEEP_WALL / STEP_LIP`)
     - **Thanh Điều Khiển Tua Lại (`Replay DVR Dock`)**:
       - Có đầy đủ nút `⏮ Đầu`, `⏪ -1 Bước`, `⏸ Tạm dừng / ▶ Phát`, `⏩ +1 Bước`, thanh kéo Timeline từng bước, và đặc biệt là nút **`💥 Tới Lúc Gặp Lỗi`** (nhảy tới đúng 4 bước trước khi bot gặp nạn để bạn quan sát cận cảnh khoảnh khắc nó bước vào điểm lỗi).
       - Hỗ trợ **3 góc máy quay Replay**: **`🎥 Sau Lưng Bot (Chase Cam)`**, **`👀 Mắt Bot (First-Person POV)`**, và **`🛸 Tự Do (Orbit)`**.
6. **Súng Bắn Tia Chẩn Đoán & Ghim Lỗi (`Click phải` hoặc `Phím F`)**:
   - Nhấp chuột phải vào bất kỳ vị trí nào trên màn hình (hoặc nhấn `Phím F` khi đang đi bộ) để bắn tia kiểm tra tức thì:
     - Khoảng lệch dọc giữa mặt hiển thị `.DFF` và mặt va chạm `.COL3` (`|dZ|`).
     - Góc dốc mặt đất (`Slope °`) và pháp tuyến `nz`.
     - Khoảng sáng trần (`Headroom m`).
   - Tự động lưu tọa độ preview + tọa độ quy đổi `GTA SA World` và xuất ra `eagle_3d_glitch_patch.json`.

---

## 5. Kiểm Chứng Thực Chiến: Debug Bản Build `Sector M1 Enhanced` & Đối Chiếu Chéo Với Agent Sinh Map

Sau khi hội thoại [**Nâng Cấp Sector M1 Enhanced**](conversation://a5424577-8251-4efa-b2d5-cb54893080c1) hoàn tất bản nâng cấp `M1 Enhanced` (`80,052` tam giác `.COL3`, đường vòng quanh đảo + 10 `PAD-01..10`, báo cáo `A* Walkability 17/17 PASS`), chúng ta đã dùng **`Eagle 3D Map Walker & Glitch Lab` (`10 Seeds · 100 Swarm Bots`)** quét độc lập và gửi câu hỏi đối chiếu sang agent `a5424577-8251-4efa-b2d5-cb54893080c1`.

**Kết quả: Agent `Nâng Cấp Sector M1 Enhanced` đã xác nhận ĐÚNG 100% cả 3 nhóm lỗi địa hình phụ mà Đàn Bot Swarm bắt được, chỉ rõ từng dòng code sinh lỗi trong [`builder.py`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-wilds-m1-2026-10-23/builder.py):**

| Nhóm lỗi do `Glitch Lab` & `Swarm Bots` phát hiện | Tọa độ & Mã Bot / Glitch bằng chứng | Xác nhận từ Agent `M1 Enhanced` & Nguyên nhân gốc trong [`builder.py`](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-wilds-m1-2026-10-23/builder.py) | Hướng khắc phục triệt để |
| :--- | :--- | :--- | :--- |
| **1. Hố rơi tự do dọc biên khoét lỗ `M0 ↔ M1` (`MISSING_COL_VOID` / `BIGWORLD_SEAM_CHASM`)** | `GLITCH-039` (`236, -200, -43.65m`), `GLITCH-040` (`236, +200, -40.34m`), `SWARM-056..058`, `SWARM-073` (`E ≈ 366m`), `SWARM-062..064` (`N ≈ -198.2m`) | **ĐÚNG 100%** ([`builder.py` dòng 467–470](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-wilds-m1-2026-10-23/builder.py#L467-L470)): Code dùng hình chữ nhật `in_m0_island = (-230 <= cx <= 364) and (-200 <= cy <= 200)` để cắt lỗ cho `M0`. Vì đa giác `M0` nhỏ hơn hình chữ nhật này, khoảng trống giữa mép hình chữ nhật (`E = 364m`, `N = ±200m`) và đa giác `M0` bị khuyết hoàn toàn `.COL3`, khiến mặt đất `M1` ở `U = -40m..-55m` bị cắt cụt lơ lửng trên mặt hồ. | Thay cắt bỏ hình chữ nhật `in_m0_island` bằng việc hạ cao độ phần lòng hồ xuống đáy hồ `U = -61.5m` nối kín tới đúng biên đa giác thực của `M0`. |
| **2. Vách taluy cắt-đắp `52°–69°` sát rìa `PAD-04` & `PAD-02` (`STEEP_SLOPE_BARRIER` / `STEP_LIP_BLOCKER`)** | `SWARM-077, 082..084` tại `(205..210, -480..-483)` (`dZ = +7.26m..+7.52m`, dốc `65°–69°`); `SWARM-069, 075..076` tại `(525..546, 111..151)` (`51.9°–54.3°`) | **ĐÚNG 100%** ([`builder.py` dòng 429–457](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-wilds-m1-2026-10-23/builder.py#L429-L457)): Cả `is_pad_vertex` (ép phẳng `PAD-04` ở `U = -42.0m`) và `road_dist <= 8.5` (tuyến đèo `Route_South_Touge` đang leo lên `U = -34.5m` ngay sát rìa Đông-Nam Pad) đều bị đưa vào mặt nạ `locked`, nên bộ làm mượt Laplacian (`~locked`) bỏ qua vùng giáp ranh giữa Pad và đường đèo, tạo ra bậc tường dựng đứng `7.5m`. | Thêm bước vát mép chuyển tiếp (`joint pad-road chamfer`) hoặc mở khóa vành đai biên `PAD` nơi giao cắt với đường đèo. |
| **3. Gờ chắn hướng Đông & Hố khuyết mép Nam đầu cầu `SEED-01` (`321.0, -93.1`)** | `SWARM-021` tại `(339.2, -92.5, U = -51.87m)` (`dZ = +5.42m`); `SWARM-028` tại `(349.42, -121.92, U = -55.78m)` (`MISSING_COL_VOID`) | **ĐÚNG 100%**: (a) Tại `(339.2, -92.5)` thuộc quyền sở hữu của `M0` (`model 6716`) có mỏm đá gốc nhô từ `-55.38m` lên `-47.68m`; `M1` đã phải bắc dải nối cầu `in_apron` (`N ∈ [-122, -108]`) lách qua mép Nam mỏm đá này. (b) Tại `(349.42, -121.92)`, bot `SWARM-028` đi chéo vượt qua giới hạn Nam `cy >= -120.0` của `in_apron` ([`builder.py` dòng 468](file:///D:/GTA%20Archive/Staging/teyvat-mondstadt-wilds-m1-2026-10-23/builder.py#L468)) nên rơi xuống vùng cắt của `in_m0_island`. | Mở rộng `in_apron` về phía Nam (`cy >= -135.0`) kết hợp hạ taluy bờ hồ xuống dưới `-58.0m`. |

### Kết quả sau Vòng Lặp Fix ↔ Retest Vòng 1 (Đạt chuẩn 100% ngay ở Vòng 1 — Không bị phẳng hóa bản đồ):
- **Số điểm lỗi hình học trong Sector `M1` (`6730..6765`)**: Giảm từ `2` cụm `BIGWORLD_SEAM_CHASM` + `19` điểm rơi tự do về **`0` lỗi (`M1 glitches = []`)**!
- **Kết quả Đàn 100 Bot Bầy Đàn Đa Hạt Giống (`10 Seeds · 100 Swarm Bots`)**:
  - **`0 / 100` Bot gặp lỗi thật (`Remaining failed bots = []`)**!
  - **`75 / 100` Bot `PASS` hoàn toàn** (`74 PATROL_OK` + `1 MAP_BOUNDARY_OK`; tăng từ `50` lên `75` nhờ vát mép `pad_collar` quanh `PAD-04` và `PAD-02` cùng mở rộng `apron_mask`).
  - **`25 / 100` Bot `INTENDED` (Dừng tại địa hình tự nhiên có chủ đích — không tính là bug)**:
    - `12` bot `INTENDED_LAKE_SHORE`: Đi xuống mặt nước Hồ Cider và xác nhận có đáy hồ `.COL3` liên tục ở `U = -61.5m` bên dưới.
    - `10` bot `INTENDED_CLIFF_OVERLOOK` + `1` bot `INTENDED_MOUNTAIN_SLOPE`: Chạm mép vách núi cao tự nhiên (`U > -28m`).
    - `2` bot `INTENDED_CITY_WALL`: Chạm tường đá nội đô `M0`.
- **Kiểm chứng Anti-Pancake (Bảo toàn độ cao đồi núi & lòng hồ)**:
  - Độ phủ đi bộ liên thông tăng lên **`98.23%`** (`348,525 / 354,816` ô lưới).
  - Toàn bộ 4 đỉnh núi giữ nguyên 100% độ cao thiết kế (`East Peak +12.0m`, `South Peak +28.0m`, `West Peak +24.0m`, `North Peak +36.0m`) cùng đáy hồ `-61.5m` (tổng biên độ cao độ `97.5m`).

---

## 6. Danh Mục File Bàn Giao & Hash Kiểm Chứng

| Vai trò | Đường dẫn file | Kích thước | SHA-256 |
| :--- | :--- | :---: | :--- |
| **Interactive 3D Glitch Lab Studio (HTML độc lập)** | [`docs/project-eagle/eagle-3d-map-walker-glitch-lab-2026-10-24.html`](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/eagle-3d-map-walker-glitch-lab-2026-10-24.html) | `18,719,173 bytes` | `bc140e8fc70b42ef91b6c5bf52b578165f085b186666424a38a7c70296a8ca76` |
| **Báo cáo JSON kiểm định chi tiết (`117` lỗi + đồ thị đi bộ)** | [`staging/project-eagle/map-walker-glitch-lab-2026-10-24/glitch_audit_report.json`](file:///c:/Users/LENOVO/Desktop/GTA/staging/project-eagle/map-walker-glitch-lab-2026-10-24/glitch_audit_report.json) | `4,296,812 bytes` | `9985a8eb3fa664667fc40804557dc594dc9f99096c003217f8ab5c9cb671c51c` |
| **Bộ máy phân tích 3D & Đóng gói HTML (Python)** | [`tools/map-glitch-lab/eagle_map_glitch_lab.py`](file:///c:/Users/LENOVO/Desktop/GTA/tools/map-glitch-lab/eagle_map_glitch_lab.py) | `65,412 bytes` | — |
| **Template giao diện WebGL Glitch Lab Studio** | [`tools/map-glitch-lab/glitch_lab_viewer_template.html`](file:///c:/Users/LENOVO/Desktop/GTA/tools/map-glitch-lab/glitch_lab_viewer_template.html) | `54,890 bytes` | — |
