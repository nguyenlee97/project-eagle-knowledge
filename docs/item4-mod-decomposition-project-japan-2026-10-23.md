# Phân Tích Tương Thích & Phẫu Thuật Phân Tách Mod (Mod Decomposition) Cho Project Eagle — Kỳ 1: Giải Phẫu Thực Tế Gói Đầy Đủ `Project Japan 3.1 (Updated)` (`2.03 GB` / `2,080` Files)

- **Ngày lập**: `2026-10-23`
- **Tác giả**: `Antigravity`
- **Đích tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Kho lưu trữ bản gốc đã tải & giải nén trên ổ `D:\`**:
  - File nén gốc (`794.60 MB`): `D:\GTA Archive\Mod Donor Library\project-japan\Project_Japan_3.1_FULL.rar`
  - Thư mục giải nén (`2.03 GB` — `2,080` files / `265` folders): `D:\GTA Archive\Mod Donor Library\project-japan\PJ_3.1_FULL_EXTRACTED`
  - Dữ liệu kiểm toán JSON: [`pj31_map_forensic_audit.json`](file:///C:/Users/LENOVO/.gemini/antigravity/brain/d35bd3b8-ebf2-426e-92ea-783156b8d787/scratch/pj31_map_forensic_audit.json)

---

## 1. Xác Minh Thực Tế Nguồn Tải Các Phiên Bản `Project Japan`

Khi tải trực tiếp cả 4 gói từ GTAinside và kiểm tra bên trong:
1. **`PROJECT JAPAN 4.0` (`13.61 MB` trên GTAinside `#198678` / LibertyCity `#209552`)**:
   - Giải nén ra thực chất chỉ gồm `14` tấm ảnh chụp màn hình `.jpg` và `LINK.txt` dẫn tới trang **Patreon trả phí (`$15 – $60 USD`)** của `SergioVanDykMods`. Không có file mod bên trong.
2. **`Project Japan 3.1 (Updated)` (`794.60 MB` RAR $\rightarrow$ `2,034,857,579 bytes` = `2.03 GB` giải nén)**:
   - Đây chính là **phiên bản đầy đủ nhất và nhiều nội dung nhất được phát hành công khai miễn phí 100%** (qua link MediaFire chính chủ từ blog `sergiovandyk.blogspot.com`).
   - Đã tải về ổ `D:\` (`990 GB` trống) và giải nén toàn bộ **`2,080` files (`265` thư mục)** để kiểm toán từng byte đối chiếu với **`72` archive `.img` (`93,779` members)** và **`64,617` Model IDs** của `gta sa gameplay-lab`.

---

## 2. Giải Phẫu Toàn Bộ `2,080` Files (`2.03 GB`) Của `Project Japan 3.1 (Updated)`

Cấu trúc thực tế sau khi giải nén `Project_Japan_3.1_FULL.rar` gồm **7 khối lớn**, trong đó **6 khối ngoài Map phải bị loại bỏ 100%** trước khi chạm vào `Project Eagle`:

| STT | Nhóm Thư Mục Trong `Project Japan 3.1` | Số Lượng File & Dung Lượng | Chứa Gì Bên Trong? | Tại Sao Phải Loại Bỏ / Giữ Lại Cho `Project Eagle`? | Quyết Định |
|---:|---|---|---|---|---|
| 1 | **`Mod\GTA San Andreas\` (Root & Plugins)** + **`Optional\Tower Tokyo Plugins Fix`** | `20` files (`22.18 MB`) | `gta_sa.exe`, `StreamMemFix.asi`, `StreamMemFix1.0.asi`, `limit_adjuster_gta3vcsa.asi`, `sa_draw_distance_changer.asi`, `No_more_haze.cs`, `Al_Planes.cs`... | ⚠️ **CỰC KỲ NGUY HIỂM**: Ghi đè `gta_sa.exe`/`gta_pe.exe` và xung đột trực tiếp với `fastman92limitAdjuster.asi` 7.7 + `EagleStreamingFix.asi` gây crash ngay khi bật game! | 🔴 **LOẠI BỎ 100%** |
| 2 | **`Modloader\Project Japan 3.1\Cars\` & `Planes\`** | `116` files (`568.50 MB`) | 20+ xe JDM/cảnh sát/taxi (`356.85 MB` gói `TURBO PRODUCTIONS`, Civic Type R, Evo VII, Supra...) + Máy bay `All Nippon Airways 744D` (`72.95 MB`). | Làm hỏng cân bằng gameplay, nặng `CStreaming` và xung đột `vehicles.img` của `S&S`. | 🔴 **LOẠI BỎ 100%** |
| 3 | **`Modloader\Project Japan 3.1\Peds\`** + **`Optional\NEW Women Animation`** | `127` files (`306.94 MB`) | 60+ skin NPC/bạn gái CJ/cảnh sát + `anim\cuts.img` (`10.44 MB`). | Xung đột trực tiếp với dàn `1,638` skin NPC Anime đã map trong `COMPONENTPEDS.img` và nhân vật chính **Aether**. | 🔴 **LOẠI BỎ 100%** |
| 4 | **`Modloader\Project Japan 3.1\Weapons\`** | `82` files (`35.64 MB`) | `40` model `.dff` + `40` `.txd` vũ khí. | Xung đột `GROUP_A_MODS.IMG` (`Immersive Weapons`) và trái mục tiêu chỉ lấy Map/Building. | 🔴 **LOẠI BỎ 100%** |
| 5 | **`Modloader\Project Japan 3.1\Sound\`** + **`Optional\Anime Music`** | `848` files (`278.40 MB`) | `838` file `.wav` (`GENRL` / `FEET` / `PAIN_A`) + `2` file `.mp3` (`155.61 MB`). | Xung đột âm thanh `GroupA_DataAndAudio` và đài RadioEx (`1.70 GB` `.ogg`) của `gameplay-lab`. | 🔴 **LOẠI BỎ 100%** |
| 6 | **`models\`** & **`Optional\Anime Menu and Loadscreen`** | `18` files (`56.72 MB`) | `fonts.txd`, `fronten1.txd`, `fronten2.txd`, `fronten_pc.txd`, `LOADSCS.txd`. | Xung đột trực tiếp với Main Menu Wibu World và `modloader\WibuWorldLoading\txd\loadscs.txd` đã cài trong `gameplay-lab`. | 🔴 **LOẠI BỎ 100%** |
| 7 | **⭐ `Modloader\Project Japan 3.1\Map\` (11 Module Con `001` $\rightarrow$ `013`)** | **`836` files (`611.17 MB`)** | Toàn bộ Texture Kiến trúc/Đường phố (`013`), Tháp Tokyo (`012`), Cây Hoa Anh Đào (`011`), Đèn đường Nhật (`010`), Quán Ramen (`008`), Samurai Sushi (`004`), Khu phố Little Tokyo (`003`), Đường sắt (`002`)... | **Đây là kho báu `611.17 MB` cần phẫu thuật phân tách chi tiết ở Mục 3 bên dưới!** *(Lưu ý: ngay trong thư mục `Map\` này tác giả vẫn để lẫn một số file xe/ped/đường sắt lỗi cần lọc bỏ bằng script)*. | 🟢 **PHẪU THUẬT BÓC TÁCH CHI TIẾT (Mục 3)** |

---

## 3. Kiểm Toán Pháp Y (Forensic Audit) Từng Module Trong `Map\` (`001` $\rightarrow$ `013`) Đối Chiếu Với `gta sa gameplay-lab`

Dưới đây là kết quả chạy script kiểm toán [`audit_pj31_map_modules.py`](file:///C:/Users/LENOVO/.gemini/antigravity/brain/d35bd3b8-ebf2-426e-92ea-783156b8d787/scratch/audit_pj31_map_modules.py) và [`check_torretokyo_and_lae2_diff.py`](file:///C:/Users/LENOVO/.gemini/antigravity/brain/d35bd3b8-ebf2-426e-92ea-783156b8d787/scratch/check_torretokyo_and_lae2_diff.py) trên toàn bộ **11 module con** của thư mục `Map\`:

### Module `013`: `PROJECT JAPAN MAIN Textures by SERGIO_VAN_DYK` (`275.45 MB` — `195` `.txd`, `32` `.dff`)
Đây là **trái tim của `Project Japan`**, biến đổi diện mạo kiến trúc, biển hiệu, cửa hàng và mặt đường tại **Los Santos (`145` files), San Fierro (`14` files), Las Venturas (`5` files), Countryside (`20` files) và Interiors (`25` files)**. Tuy nhiên, kiểm toán từng file phát hiện **4 bẫy ngầm** cần xử lý bằng script:
1. **Bẫy 1 — Có `9` file Xe cộ & Tàu hỏa bỏ nhầm vào thư mục Map**:
   - Gồm `4` file `.dff` (`Freight.dff`, `INFERNUS.dff`, `freiflat.dff`, `streak.dff`) và `5` file `.txd` (`freiflat.txd`, `freight.txd`, `infernus.txd`, `streak.txd`, `streakc.txd`).
   - 👉 **Xử lý**: **Cắt bỏ 100%** `9` file phương tiện này.
2. **Bẫy 2 — Có `17` file `.dff` Đường sắt & Hầm tàu hỏa**:
   - Gồm `coe_traintrax02..10.dff` (`9` files), `laerail6.dff`, `laerailtrack1..4.dff` (`5` files), `laetraintunn02..03.dff` (`2` files).
   - 👉 **Xử lý**: **Cắt bỏ 100%** để tránh lỗi thiếu prelight ban đêm.
3. **Bẫy 3 — Xung đột với `CUSTOM\GROUP_A_MODS.IMG` (`1` `.dff` + `24` `.txd`)**:
   - File `nwspltbild3_las2.dff` trùng trực tiếp với tòa nhà đã khoét cửa nội thất EHI của `GROUP_A_MODS.IMG` $\rightarrow$ **Cắt bỏ `nwspltbild3_las2.dff`** (giữ bản `GROUP_A`).
   - **`24` file `.txd` trùng với `GROUP_A_MODS.IMG`**:
     `['711c.txd', '7_11_posters.txd', 'barrio1_lae.txd', 'cj_commercial.txd', 'cj_sex.txd', 'cj_ss_1.txd', 'cj_ss_2.txd', 'cj_ss_3.txd', 'cj_ss_4.txd', 'dyn_cash.txd', 'furniture_lae2.txd', 'genintint711_1.txd', 'genintintsex.txd', 'hospital_lae.txd', 'idlewood3_lae.txd', 'idlewood6_lae.txd', 'jeffers5a_lae.txd', 'lashops93_las2.txd', 'new_cabinets.txd', 'new_cabinets2.txd', 'new_cabinets3.txd', 'shopliquor_las.txd', 'stolenbuild02.txd', 'templae2land.txd']`
   - 👉 **Xử lý**: Dùng thuật toán **Phẫu thuật Ghép Raster (`Raster-Level TXD Merge`)**: Lấy `.txd` của `GROUP_A` làm gốc (bảo toàn 100% các texture nội thất EHI) và ghi đè các raster mặt ngoài bằng texture Nhật Bản của `013`!
4. **Bẫy 4 — Giao thoa với `CUSTOM\GROUP_B1_TEXTURES.IMG` (`1` `.dff` + `40` `.txd`)**:
   - `40` file `.txd` biển hiệu/cửa hàng (`lae2billboards.txd`, `billbrd01_lan.txd`, `billbrdlawn.txd`, `lawnbillbrd.txd`, `sunbill_law2.txd`, `chicano10_lae.txd`, `glenpark7_lae.txd`...) hiện đang nằm trong `GROUP_B1_TEXTURES.IMG` (biển hiệu Mỹ thập niên 90).
   - 👉 **Xử lý**: Đóng gói toàn bộ `190` file `.txd` hợp lệ của `013` vào `CUSTOM\GROUP_WIBU_WORLD.IMG` và khai báo **trên dòng `GROUP_B1_TEXTURES.IMG`** trong `data\default.dat` để biển hiệu Nhật Bản/Anime hiển thị thay cho biển hiệu Mỹ!

---

### Module `012`: `TorreTokyo By Misaki Modding & MrAndres5555` (`15.02 MB` — Tháp Tokyo tại Los Santos)
- **Cấu trúc**: Đặt Tháp Tokyo (`Abase1.dff`, `Abase2.dff`, `lodabase1.dff`, `Abase3.dff`, `Abase.txd`, `Abase3.txd`, `abase.col`) tại tọa độ `(1753.0, -1358.0, 21.0)` ở Downtown / Glen Park Los Santos.
- **2 Lỗi Nghiêm Trọng Phát Hiện Khi Kiểm Toán Với `Project Eagle`**:
  1. **Đụng độ Model ID trong `001.IDE`**:
     - `001.IDE` dùng 4 ID `18631, 18632, 18633, 18634`.
     - Trong `gta sa gameplay-lab`, 4 ID này **ĐÃ BỊ CHIẾM** bởi `SAMP\SAMP.ide` (`18631 = NoModelFile`, `18632 = FishingRod`, `18633 = GTASAWrench1`, `18634 = GTASACrowbar1`)!
  2. **Lỗi Quaternion Chưa Chuẩn Hóa (`Unnormalized Quaternion`) trong `001.IPL`**:
     - Dòng IPL gốc: `18631, Abase1, 0, 1753.0, -1358.0, 21.0, 0, 0, 0.594822354205, 0.0, -1`
     - Độ dài vector quay $\sqrt{0^2 + 0^2 + 0.594822^2 + 0^2} = 0.594822 \neq 1.0$ (do tác giả gõ nhầm `rw = 0.0` thay vì `0.80385718`)! Trong `gta_pe.exe` (`0x005381D5`), quaternion có chuẩn khác `1.0` sẽ làm biến dạng ma trận va chạm `.col`!
- 👉 **Giải Pháp Phẫu Thuật**:
  - Đổi 4 ID `18631..18634` sang dải ID trống hoàn toàn của `Project Eagle`: **`3194, 3195, 3196, 3197`** (đã xác minh trống 100% trên toàn bộ `64,617` IDs của `gameplay-lab`).
  - Chuẩn hóa lại quaternion trong `.IPL` thành `0, 0, 0.59482235, 0.80385718` ($\|\mathbf{q}\| = 1.000000$).

---

### Module `008`: `RAMEN by TAKEI01` (`3.48 MB` — Quán Mì Ramen tại Ganton)
- **Phát hiện khi mổ xẻ**:
  - Thư mục con `PIZZA TO RAMEN&PIZZA` (`food.ifp`, `cj_pizza_1.dff`...) và 4 file `WFYBURG.dff/.txd`, `WMYPIZZ.dff/.txd` trong `RAMEN SHOP AT GANTON` là **mod nhân vật NPC & animation ăn pizza** (`GROUP_A` cũng đang giữ `wfyburg` và `wmypizz`).
  - Phần **Kiến trúc Quán Ramen thực sự** chỉ gồm đúng **4 files**:
    - `stripbar_lae.dff` + `lod1strpbar_lae.dff` (thay tòa nhà Pig Pen ở East LS thành Quán Ramen Nhật Bản)
    - `laeast2_lod.txd` (texture LOD của quán)
    - `lae2_4.col` (collision của khu `lae2_4` — **không trùng** với 4 file `.col` của `GROUP_A` là `lae_5.col`, `lan2_1.col`, `las2_4.col`, `laxref.col`!).
- 👉 **Giải Pháp Phẫu Thuật**: **Chỉ trích xuất đúng 4 file kiến trúc Quán Ramen** (`stripbar_lae.dff`, `lod1strpbar_lae.dff`, `laeast2_lod.txd`, `lae2_4.col`), vứt bỏ toàn bộ file NPC `WFYBURG`/`WMYPIZZ` và `food.ifp`.

---

### Module `003`: `JAPAN - Indonesia!!!! Mapping by Ains` (`70.27 MB` — Khu Phố Little Tokyo & Props Đường Phố)
- **Phát hiện khi mổ xẻ**:
  1. Chứa **xe đạp** (`jitensha\bike.dff/.txd`) và **3 skin băng đảng Grove Street** (`Little Tokyo Hashiriya Boyz\fam1..3.dff/.txd`) $\rightarrow$ **Cắt bỏ 100%**.
  2. Chứa `texture\pc\vegetasi\tanaman liar 1\vegepart.col` ghi đè collision cây cối toàn cục $\rightarrow$ **Cắt bỏ `vegepart.col`** để tránh lỗi tường tàng hình kiểu `BUG-006`.
  3. File `map\LAe2.ipl` (`672` dòng) ghi đè trực tiếp lên `data\maps\LA\LAe2.ipl` (`399` dòng) của `Project Eagle`:
     - Nếu chép đè nguyên file `LAe2.ipl`, nó sẽ **khôi phục nhầm 7 cái cây `veg_bevtree2` (`ID 714`)** mà `S&S` đã chủ động hạ ngầm xuống `Z = -77m..-88m` để giải phóng mặt bằng!
     - Khi chạy diff từng dòng, thực chất `003` chỉ thêm **`264` dòng `inst` đặt các vật thể trang trí đường phố Nhật Bản** (máy bán kẹo `CJ_CANDYVENDOR`, ghế công viên `parkbench1`, hàng rào gỗ, chậu cây cảnh `pot_02`, `Plant_Pot_10`, `kb_planter+bush`) quanh khu Ganton (`X ≈ 2513..2533, Y ≈ -1667..-1660`).
- 👉 **Giải Pháp Phẫu Thuật**:
  - **Không ghi đè `data\maps\LA\LAe2.ipl`**!
  - Chỉ trích xuất **`264` dòng `inst` prop mới** (bỏ 7 dòng cây `veg_bevtree2` bị xung đột `S&S`) đưa vào file `.IPL` mở rộng riêng, đồng thời lấy các `.txd`/`.dff` thùng rác, ghế đá, biển báo đường phố Nhật Bản.

---

### Module `001`, `004`, `006`, `010`: Các Gói Texture & Đèn Đường Nhỏ Gọn (`22.19 MB` tổng cộng)
- **`001 Graffitis Spray Dead Or Alive XVV` (`6.00 MB`)**: `9` file `.txd` thay thế tranh tường graffiti băng đảng bằng poster Anime/DOAXVV (`Generic.img`, `0` xung đột `GROUP_A`/`GROUP_B1`) $\rightarrow$ 🟢 **Giữ 100%**.
- **`004 LS_SAMURAI SUSHI V2` (`1.11 MB`)**: `1` file `tempo22_law.txd` biến tòa nhà ở West LS thành nhà hàng **Samurai Sushi** (đè lên `GROUP_B1`) $\rightarrow$ 🟢 **Giữ 100%**.
- **`006 Pillow dakimakura` (`0.85 MB`)**: Thay tạp chí trên bàn (`gb_magazines01.txd` + `.dff` trong `Interiors.img`) thành gối ôm Anime Dakimakura $\rightarrow$ 🟢 **Giữ 100%**.
- **`010 Street Lights By MR TanagoENJ7` (`11.14 MB`)**: `14` `.dff` + `7` `.txd` đèn đường Nhật Bản trong `Generic.img` (`0` xung đột với `GROUP_A` hay `GROUP_B1`). *(Lưu ý: Bỏ file `data\object.dat` đi kèm để không làm lệch bảng vật lý `object.dat` của `S&S`, chỉ lấy `14` `.dff` + `7` `.txd`)* $\rightarrow$ 🟢 **Giữ model/texture, bỏ `object.dat`**.

---

### Module `002` & `011`: Hai Module Quy Mô Quá Lớn Cần Xử Lý Đặc Biệt
1. **Module `002 High speed RAILWAY line by Jeka` (`110.08 MB` — `82` file `.dff` đường sắt)**:
   - Thay thế `82` mảnh địa hình đường sắt xuyên qua `GAME_LA` (`8`), `GAME_SF` (`17`), `GAME_LV` (`28`), `GAME_SA` (`28`) + 1 đầu tàu `streakc.dff`.
   - Bị lỗi mất *prelight* ban đêm và nguy cơ cắt ngang địa hình nối bang của `S&S`.
   - 👉 **Quyết định**: 🔴 **Loại bỏ toàn bộ `82` file `.dff` đường sắt này**.
2. **Module `011 Cherry tree by Miyata Lee` (`113.81 MB` — `286` `.dff`, `44` `.txd`, `plants.dat`, `procobj.dat`, `vegepart.ide`, `procobj.ide`)**:
   - Thực chất đây là toàn bộ đại dự án cây cối **BSOR (`Behind Space Of Realities`)** (`276` `.dff` đè lên `Generic.img`, kèm `16` file `bsor_*.txd` mới và file `vegepart.ide` / `procobj.ide` sửa đổi).
   - Nếu chép đè `vegepart.ide` và `276` cây vào `Generic.img`:
     1. Nó sẽ biến toàn bộ cây cọ nhiệt đới ở **Miami / Vice City & Leonida** thành cây Hoa Anh Đào hồng!
     2. `286` model cây BSOR có số đa giác (polygon) rất cao, dễ gây sụt FPS và tốn bộ nhớ `CStreaming` ở các đại đô thị.
   - 👉 **Quyết định Phẫu thuật cho `011`**:
     - **Tuyệt đối không ghi đè `vegepart.ide`, `procobj.ide`, `plants.dat` hay toàn bộ `276` cây trong `Generic.img`**.
     - Chỉ trích xuất **những model cây Hoa Anh Đào (`Cherry Blossom / Sakura`) đẹp nhất** từ `011`, cấp cho chúng **ID riêng trong dải trống `3200..3213` của `CUSTOM\CUSTOM_MODS.IDE`** để trồng tại các khu quy hoạch Wibu (`WIBU-01`..`WIBU-07`), quanh Tháp Tokyo (`012`) và công viên Glen Park Los Santos!

---

## 4. Tổng Kết Kết Quả Bóc Tách `Project Japan 3.1 (Updated)`: Từ `2.03 GB` Xuống Gói Tinh Hoa `~315 MB`

Nhờ giải phẫu từng file trong bản đầy đủ `2.03 GB` (`2,080` files), chúng ta lọc bỏ được **`1.71 GB` thành phần gây xung đột/hỏng gameplay** và thu được **Gói Tinh Hoa Kiến Trúc & Đô Thị `Project Japan` (`~315 MB`)** tương thích 100% với `Project Eagle`:

| Thành Phần Giữ Lại Sau Phẫu Thuật | Số Lượng File | Kỹ Thuật Đóng Gói Vào `Project Eagle` |
|---|---:|---|
| **1. Bộ Texture Đô thị, Tòa nhà & Biển hiệu Nhật Bản (`013` + `001` + `004` + `006`)** | **`201` `.txd`** | • `176` `.txd` đóng gói thẳng vào `CUSTOM\GROUP_WIBU_WORLD.IMG`.<br>• `25` `.txd` (`24` của `013` + `1` của `003`) chạy **Phẫu thuật Ghép Raster (`TXD Raster Merge`)** với `GROUP_A_MODS.IMG` để giữ 100% nội thất EHI. |
| **2. Tháp Tokyo (`012 TorreTokyo`)** | **`4` `.dff` + `2` `.txd` + `1` `.col`** | • Đổi ID từ `18631..18634` (đụng `SAMP.ide`) sang **`3194..3197`** trong `CUSTOM_MODS.IDE`.<br>• Sửa lỗi Quaternion chưa chuẩn hóa trong `.IPL` (`rw: 0.0` $\rightarrow$ `0.80385718`). |
| **3. Quán Mì Ramen Ganton (`008`) & Đèn Đường Nhật Bản (`010`)** | **`18` `.dff` + `8` `.txd` + `1` `.col`** | • Đã lọc bỏ hoàn toàn 2 skin NPC (`WFYBURG`, `WMYPIZZ`), `food.ifp` và `object.dat`. |
| **4. Khu Phố Little Tokyo & Props Đường Phố (`003`)** | **`20` `.dff` + `18` `.txd` + `264` dòng `.IPL`** | • Đã lọc bỏ xe đạp `bike`, 3 skin gang `fam1..3`, `vegepart.col` và 7 dòng cây xung đột `S&S` trong `LAe2.ipl`. |
| **5. Cây Hoa Anh Đào Tuyển Chọn (`011 Sakura Trees`)** | **`~10–15` `.dff`/`.txd` chọn lọc** | • Cấp ID mới (`3200..3213`) hoặc chỉ thay cây đường phố Los Santos, bảo toàn 100% rừng cây cọ nhiệt đới của Vice City / Leonida. |
