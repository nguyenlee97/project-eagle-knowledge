# Hạng mục 4 (Kỳ 2) — Báo Cáo Bóc Tách Thực Chiến Các Khu Phố Nhật Bản, Đô Thị Gacha & Tòa Nhà Lẻ (`Urban Districts & Standalone Buildings`) Cho `Project Eagle` (`gta sa gameplay-lab`)

- **Ngày lập**: `2026-10-23`
- **Tác giả**: `Antigravity`
- **Phạm vi**: `docs/project-eagle` (Khảo sát, tải gói đầy đủ & mổ xẻ cấu trúc nhị phân `read-only` — **không ghi đè bất kỳ file nào trong `gta sa gameplay-lab`**)
- **Kho lưu trữ bản gốc đã tải & giải nén (`Donor Archive`)**: `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\`
- **Chiến lược điều phối theo thống nhất của người dùng**: **Bóc tách và kiểm toán xung đột toàn bộ các bản mod trước (Kỳ 1 $\rightarrow$ Kỳ 4), sau đó mới đóng gói hợp nhất một lần duy nhất ở bước cuối cùng (`Unified Packaging`)**.
- **Tài liệu liên quan**:
  - [Kỳ 1 — Báo cáo bóc tách Project Japan 3.1 Full (`2.03 GB`)](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/item4-mod-decomposition-project-japan-2026-10-23.md)
  - [Danh mục tổng thể Map & Kiến trúc Anime/Wibu](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/item4-public-anime-wibu-mods-catalogue-2026-10-23.md)
  - [Quy hoạch kỹ thuật Hạng mục 4 (`WIBU-01`..`WIBU-07`)](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/item4-wibu-genshin-expansion-feasibility-2026-10-22.md)

---

## 1. Tại Sao Phải "Bóc Tách Xong Hết Rồi Mới Đóng Gói"?

1. **Khái niệm "Bóc tách" (`Mod Decomposition & Forensic Audit`)**:
   - Là quá trình tải bản đầy đủ của từng mod về kho đệm trên ổ `D:\`, giải nén và quét nhị phân từng file (`.dff`, `.txd`, `.col`, `.ide`, `.ipl`) để:
     - **Lọc bỏ 100% rác phi kiến trúc**: Loại bỏ xe cộ, vũ khí, skin NPC, animation, âm thanh, script `.cs`/`.asi`, hoặc các file cấu hình hệ thống làm hỏng `Project Eagle`.
     - **Phát hiện bẫy ghi đè `.IPL`/`.IDE` gốc**: Rất nhiều modder GTA SA khi thêm chỉ 5–10 prop ghế ngồi hoặc bảng hiệu đã đính kèm **nguyên file `LAn.IPL` hoặc `LAwn.IPL` của GTA SA vanilla**. Nếu chép đè vào `Project Eagle`, chúng sẽ làm sống lại hàng chục cái cây mà `Stars & Stripes (S&S)` đã hạ ngầm xuống `Z = -37m` và xóa sổ các chỉnh sửa bản đồ của `Project Eagle`.
     - **Phát hiện xung đột ID và xung đột chéo giữa các Mod**: Ví dụ, `Akihabara Electronic Town` (`#155560`) dùng dải ID `2..3141` đè trực tiếp lên **12 ID nhân vật trong `peds.ide`** (bao gồm cả cảnh sát `265, 266, 267`), còn `Japanese Castle CJ House` (`#101385`) đụng trực tiếp 3 file `.txd` của `Project Japan 3.1` và 1 file LOD của `008 Ramen Shop`.
2. **Khái niệm "Đóng gói" (`Unified Packaging`) ở bước cuối cùng**:
   - Sau khi đã bóc tách xong toàn bộ các bản mod từ **Kỳ 1 đến Kỳ 4**, chúng ta có **danh sách 100% các tài nguyên sạch có thể dùng được** cùng bảng cấp phát ID tổng thể (không trùng nhau và không trùng với `64,617` ID của `Project Eagle`).
   - Lúc đó, bước **Đóng gói** sẽ gom tất cả tài nguyên đã chuẩn hóa vào **một bộ cài đặt hợp nhất duy nhất**:
     - `CUSTOM\WIBU_WORLD_BUILDINGS.IMG` (chứa toàn bộ `.dff`, `.txd`, `.col` của các khu đô thị mới, tòa nhà độc lập, đèo núi và kỳ quan anime).
     - `CUSTOM\WIBU_BASE_OVERRIDES.IMG` (chứa các file `.txd`/`.dff` thay thế mặt tiền/biển hiệu tại Los Santos, San Fierro, Las Venturas đã qua bước **Raster-Merge** bảo toàn nội thất `GROUP_A_MODS.IMG`).
     - Bộ file `data\maps\wibu\wibu_*.ide` & `wibu_*.ipl` đã được cấp phát ID sạch và dịch chuyển tọa độ (`Coordinate Offset`) vào đúng các phân khu `WIBU-01`..`WIBU-07`.

---

## 2. Kiểm Toán Giải Phẫu Nhị Phân 9 Gói Mod Đã Tải Về Kho `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\`

| Mã Mod | Tên Bản Mod & Nguồn | Dung Lượng Nén / Giải Nén | Cấu Trúc File Thực Tế Trong Archive | Phát Hiện Xung Đột Với `Project Eagle` & `Project Japan 3.1` | Quyết Định Bóc Tách |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`KY2-01`** | **Kerorin Capital 1.0** ([GTAinside #153898](https://www.gtainside.com/sanandreas/maps/153898-kerorin-capital-1-0) / ZZPuma) | `32.38 MB` ZIP $\rightarrow$ `57` files | `kero.ide` (`49` models), `kero.IPL` (`80` instances, `bad_quats = 0`), `kero.col` (`6.07 MB`), `zero.col` (`78 B`), `kero.txd` (`100.3 MB`), `49` `.dff` (`kero_part_0`..`48`) | Dùng dải ID `14901..14982` $\rightarrow$ **đụng trực tiếp `16` ID đang dùng trong `Project Eagle`** (`14901, 14902, 14903, 14950, 14972..14982`). Tọa độ gốc `X = [-65.6..398.8], Y = [201.5..615.3], Z = [-17.5..70.7]` nằm đè lên vùng đồi Red County! | **GIỮ 100% (`49` `.dff` + `kero.txd` + `kero.col`)** — Cấp lại dải ID sạch **`11800..11848`** và dịch tọa độ (`Offset`) sang đảo đô thị **`WIBU-01` (`MKLAS`)** |
| **`KY2-02`** | **Akihabara Electronic Town** ([GTAinside #155560](https://www.gtainside.com/en/sanandreas/maps/155560-akihabara-electronic-town-for-android/) / Ponzu & ZZPuma) | `135.19 MB` ZIP $\rightarrow$ `943` files | `akihabara.ide` (`75` models), `akihabara.IPL` (`75` instances, `bad_quats = 0`), `akihabara.col` (`1.63 MB`), `75` `.dff` (`gigo.dff`, `laox.dff`, `ishimaru.dff`, `radio_center.dff`, `station_dept.dff`, `passers_*.dff`, `signals_*.dff`, `trees_*.dff`), kèm `860` texture `.png`/`.txt` | **CẢNH BÁO NGHIÊM TRỌNG**: `akihabara.ide` dùng dải ID `2..3141` $\rightarrow$ **đè trực tiếp lên `12` ID nhân vật trong `peds.ide` (bao gồm cả Cảnh sát `265, 266, 267` và các ID `2..8`)**! Tọa độ gốc `X = [2561.5..3000.5], Y = [-2879.3..-2628.6]` (`439m × 251m` ngoài khơi Ocean Docks). | **GIỮ `75` `.dff` + `akihabara.col` + bộ Texture** — Cấp lại dải ID sạch **`11850..11924`** (`0` đụng chạm `peds.ide`), đóng gói các `.png` thành file `akihabara_town.txd` chuẩn PC (DXT1/DXT5) và đặt tại **`WIBU-01` (`MKLAS`)** |
| **`KY2-03`** | **Little Akihabara V1 (`JapBlock`)** ([GTAinside #155181](https://www.gtainside.com/sanandreas/mods/buildings/155181-little-akihabara)) | `6.84 MB` RAR $\rightarrow$ `6` files | `lanblokb.txd` (`18.58 MB`), kèm bản chép đè `LAn.ide` và `LAn.IPL` | `lanblokb.txd` nằm trong `GROUP_B1_TEXTURES.IMG` và **`0` trùng với `Project Japan 3.1`**. Tuy nhiên file `LAn.IPL` đi kèm chỉ thêm **9 dòng prop** (ghế chờ, hàng rào ở `X ≈ 1529, Y ≈ -1475`) nhưng lại **khôi phục nhầm `13` cái cây `veg_bevtree1` mà `S&S` đã hạ ngầm xuống `Z = -37.24m`**! | **CHỈ LẤY `lanblokb.txd` + `9` dòng `inst` prop trong `LAn.IPL`**; **LOẠI BỎ** file `LAn.ide` và phần còn lại của `LAn.IPL` |
| **`KY2-04`** | **Little Akihabara V2 (`Updated`)** ([GTAinside #221340](https://www.gtainside.com/sanandreas/mods/buildings/221340-little-akihabara)) | `5.73 MB` ZIP $\rightarrow$ `11` files | `lanblokb2.txd` (`6.08 MB`), kèm thư mục tùy chọn `Roofstuff (install at your own risk)\LAn.ide` & `LAn.IPL` | `lanblokb2.txd` nằm trong **`GROUP_A_MODS.IMG` (`EHI`)** và **`0` trùng với `Project Japan 3.1`**! Bản `LAn.IPL` trong `Roofstuff` thêm **22 dòng prop sân thượng** (bàn ghế, máy bán nước, cây cọ ở `Z ≈ 44.6m`) nhưng cũng làm trồi lại `13` cây `veg_bevtree1` của `S&S`. | **GIỮ `lanblokb2.txd` (dùng Raster-Merge với `GROUP_A`) + trích xuất đúng `22` dòng `inst` sân thượng**; **LOẠI BỎ** file `LAn.IPL` gốc |
| **`KY2-05`** | **Japanese Building V1 (`OtakuShoppu`)** ([GTAinside #159896](https://www.gtainside.com/sanandreas/mods/buildings/159896-japanese-building)) | `6.62 MB` ZIP $\rightarrow$ `6` files | `sunrise09_lawn.txd` (`12.22 MB`), kèm `LaWn.ide` và `LAwn.IPL` | `sunrise09_lawn.txd` nằm ở `GAME_LA.img` (`0` đụng `GROUP_A`, `0` đụng `GROUP_B1`, `0` đụng `Project Japan 3.1`). Nhưng file `LAwn.IPL` đi kèm chỉ thêm **5 dòng prop** (`dyn_table_02`, `dyn_ramp` tại `X ≈ 1152, Y ≈ -1188`) mà lại **làm sống lại `58` cái cây `tree_hipoly` đã bị `S&S` hạ ngầm xuống `Z = -29m..-38m`**! | **GIỮ `sunrise09_lawn.txd` + `5` dòng `inst` prop**; **TUYỆT ĐỐI KHÔNG** chép đè `LaWn.ide` / `LAwn.IPL` |
| **`KY2-06`** | **Japanese Building V.02 (`Kawaiiboutique`)** ([GTAinside #175652](https://www.gtainside.com/sanandreas/mods/buildings/175652-japanese-building-v-02)) | `2.52 MB` RAR $\rightarrow$ `6` files | `sunrise09_lawn.txd` (`5.14 MB`), kèm `LaWn.ide` và `LAwn.IPL` | Thay thế **cùng một file `sunrise09_lawn.txd`** như bản V1 (`#159896`), thêm **23 dòng prop** (`telgrphpole02`, `PARKBENCH1`, `bollardlight` tại `X ≈ 1110..1152, Y ≈ -1202..-1166`) và cũng làm hỏng `58` cây `tree_hipoly` của `S&S`. | Dùng `sunrise09_lawn.txd` của V1 cho tòa nhà gốc tại Temple, và **nhân bản `.dff` tòa nhà sang ID độc lập `3199` (`kawaiiboutique_lawn`)** kèm `sunrise09_kawaii.txd` để đặt cả 2 cửa hàng (`OtakuShoppu` + `Kawaiiboutique`) cùng tồn tại! |
| **`KY2-07`** | **Japanese Castle In San Fierro** ([GTAinside #188900](https://www.gtainside.com/sanandreas/mods/buildings/188900-japanese-castle-in-san-fierro)) | `1.01 MB` RAR $\rightarrow$ `9` files | `transmitter_sfs.dff`, `lodnsmitter_sfs01.dff`, `tvtower_sfs.txd`, `lod_sfs5.txd`, `sfs_1.col` | Thay thế tháp truyền hình trên đỉnh đồi Missionary Hill (San Fierro) bằng **Lâu đài cổ Nhật Bản + cổng Torii đỏ**. Kiểm tra chéo: **`0` đụng `GROUP_A_MODS.IMG`, `0` đụng `GROUP_B1_TEXTURES.IMG`, `0` đụng `Project Japan 3.1`**! | **TƯƠNG THÍCH 100% (`READY TO USE`)** — Có thể dùng trực tiếp trên đỉnh đồi Missionary Hill (SF) hoặc cấp ID độc lập đặt tại `WIBU-03`/`WIBU-05` |
| **`KY2-08`** | **Japanese Castle CJ House** ([GTAinside #101385](https://www.gtainside.com/sanandreas/mods/modifications/101385-japanese-castle-cj-house)) | `3.26 MB` RAR $\rightarrow$ `9` files | `carlshou1_lae2.dff`, `lodlshou1_lae2.dff`, `contachou1_lae2.txd`, `laeast2_lod.txd`, `ganghouse1_lax.txd`, `hub_alpha.txd`, `lae2_2.col` | **XUNG ĐỘT CHÉO VỚI KỲ 1**: Đụng trực tiếp `3` file `.txd` của `Project Japan 3.1` (`contachou1_lae2.txd`, `ganghouse1_lax.txd`, `hub_alpha.txd`) và đụng `laeast2_lod.txd` của module `008 Ramen Shop`! | **KHÔNG GHI ĐÈ NHÀ CJ Ở GANTON** — Tách `carlshou1_lae2.dff` + collision riêng thành **Model độc lập ID `3198` (`jp_castle_ganton`)** đặt tại Đảo Đền Thờ `WIBU-05` (`Pera Loca`) |
| **`KY2-09`** | **Hatsune Miku New Sign (Las Venturas)** ([GTAinside #180718](https://www.gtainside.com/sanandreas/maps/other-maps/180718-hatsune-miku-new-sign)) | `8.66 MB` RAR $\rightarrow$ `5` files | `vegcandysign1.dff`, `lodcandysign1.dff`, `vgnfremntsgn.txd`, `vegasnlod1.txd`, `vegasn_4.col` | Thay biển hiệu tại Las Venturas bằng bảng hiệu đèn Neon Hatsune Miku V2 (`Alan74`). Kiểm tra chéo: **`0` đụng `GROUP_A`, `0` đụng `GROUP_B1`, `0` đụng `Project Japan 3.1`**! | **TƯƠNG THÍCH 100% (`READY TO USE`)** — Đưa thẳng vào lớp override của Las Venturas |

> [!NOTE]
> Trong quá trình quét thử nghiệm thêm trên GTAinside, hai gói `Dogenzaka Street (#101189)` và `7-Eleven With Parking (#192641)` cũng đã được tải về để kiểm tra và **bị loại bỏ ngay ở vòng lọc kỹ thuật** vì:
> - `Dogenzaka Street (#101189)` (`2.00 MB`) chỉ chứa 2 file `.max` (3ds Max source) và texture `.bmp` thô, chưa được xuất ra `.dff`/`.col`/`.ipl`.
> - `7-Eleven With Parking (#192641)` (`5.05 MB`) chép đè trực tiếp `savehousestudio.dff` + `LAw2.ipl` + `LAwn.ipl` kèm 2 script CLEO `.cs`.

---

## 3. Phân Tích Chi Tiết Các Khu Phố Đô Thị Lớn Khác Trong Kỳ 2 (`Utagawa Machi Ex`, `Sixth Street ZZZ` & Nhóm Storefronts LibertyCity)

### 3.1. `Utagawa Machi Ex` (`ZZPuma` & `Kelorin Jo BTA` — `45.0 MB`)
- **Nguồn**: [ZZPuma Blogspot](https://zzpumazone.blogspot.com/2021/12/utagawa-machi-ex.html) (`UtagawaEx_fla_1.1.zip` trên ShareMods / Google Drive).
- **Đặc trưng kỹ thuật**:
  - Là khu đô thị Nhật Bản hoàn chỉnh được nâng cấp từ bản gốc của `Kelorin Jo BTA`, có sẵn **đường đi cho NPC (`ped paths`), luồng xe chạy (`car paths`), hiệu ứng ánh sáng đèn đường ban đêm (`2dfx`) và prelight ngày/đêm**.
  - Tuy nhiên, gói gốc sử dụng hệ thống `fastman92limitAdjuster` riêng (`UtagawaEx_fla_1.1`) và ghi đè các file `nodes*.dat` nếu cài trực tiếp.
- **Quy tắc bóc tách cho `Project Eagle`**:
  1. **Chỉ giữ**: Các file `.dff`, `.txd`, `.col` và tọa độ đặt vật thể trong `.ide`/`.ipl` của `Utagawa Machi Ex`.
  2. **Loại bỏ**: Các file cấu hình `.ini` của `fastman92limitAdjuster` đi kèm (để không đè lên cấu hình `fastman92limitAdjuster_GTASA.ini` của `Project Eagle` `S&S`).
  3. **Về AI Path (`Nodes.dat`)**: Đặt khu phố `Utagawa Machi Ex` khớp lên mạng lưới **`2,106` node đường bộ có sẵn trên Đảo `MKLAS` (`WIBU-01`)** hoặc nạp bổ sung bằng định dạng `.navi` của `S&S` (`S&S\Paths\`) thay vì ghi đè `Nodes.dat` gốc của San Andreas.

### 3.2. `Sixth Street Map — Zenless Zone Zero` (`tatara_hisoka` — [LibertyCity #222933](https://libertycity.net/files/gta-san-andreas/222933-sixth-street-map-zenless-zone-zero.html), `188.01 MB`)
- **Cấu trúc kỹ thuật đã xác minh**:
  - Tác giả `tatara_hisoka` (cùng tác giả với `Tracen Academy #245280`) đóng gói khu phố **Sixth Street (Janus Quarter, New Eridu)** dưới dạng **bộ Map độc lập nạp qua `ModLoader`** (`.dff`, `.txd`, `.col`, `.ide`, `.ipl`), bao gồm:
    - Tiệm băng đĩa **Random Play** (nhà của Belle & Wise),
    - Quán mì **Waterfall Soup** của General Chop,
    - Tiệm cà phê **Coff Cafe**, sạp báo **Howl's Newsstand**, tiệm đĩa nhạc **Bardic Needle** và phòng game thùng **Godfinger Arcade**.
- **Quy tắc bóc tách cho `Project Eagle`**:
  - Vì `Sixth Street` là một cụm khu phố khép kín (alleyway block) không thay thế bất kỳ tòa nhà gốc nào của Los Santos, ta cấp riêng cho khu phố này dải **ID `11925..12049` (`125` slots)** trong vùng trống `11754..12799` và đặt làm **Phân khu trung tâm Gacha (Phố Random Play)** ngay trên Đảo `WIBU-01` (`MKLAS`).

### 3.3. Nhóm Tòa Nhà Cửa Hàng Anime Trên LibertyCity (`#243182`, `#243570`, `#242437`, `#232338`)
1. **`New Anime Store` ([LibertyCity #243182](https://libertycity.net/files/gta-san-andreas/243182-new-anime-store.html) — `2.65 MB`)**:
   - Thay thế cửa hàng tại Los Santos bằng mặt tiền Anime/Manga Store (`.dff`, `.txd`). Cấp ID độc lập hoặc kiểm tra `.txd` với `GROUP_A_MODS.IMG` trước khi đưa vào `WIBU_BASE_OVERRIDES.IMG`.
2. **`Animated Building` ([LibertyCity #243570](https://libertycity.net/files/gta-san-andreas/243570-animated-building.html) — `4.54 MB`)**:
   - Tòa nhà gắn bảng hiệu chuyển động UV-scroll (`.dff`, `.txd`). Giữ nguyên hiệu ứng UV animation trong `.dff`, không cần script CLEO.
3. **`Shopping Center near Glen Park` ([LibertyCity #242437](https://libertycity.net/files/gta-san-andreas/242437-shopping-center-near-glen-park.html) — `25.19 MB`)**:
   - Khu trung tâm thương mại gần Glen Park trang trí banner Anime. Kiểm tra giao cắt tọa độ với `003 Mapping by Ains` (`Project Japan 3.1`) tại khu vực `LAe` / `LAn` trước khi gộp.
4. **`GTA: Tokyo City` ([LibertyCity #232338](https://libertycity.net/files/gta-san-andreas/232338-gta-tokyo-city.html) — `462.66 MB`)**:
   - Là gói tổng hợp (modpack) chứa nhiều thành phần trùng lặp với `Project Japan 3.1` kèm xe cộ/timecyc. **Quy tắc bóc tách**: Chỉ rút các file `.txd` mặt tiền tòa nhà chưa có trong `Project Japan 3.1`, loại bỏ toàn bộ xe cộ, script và `gta.dat` đi kèm.

---

## 4. Giải Phẫu Dòng Dữ Liệu `.IPL` Đã Trích Xuất Sạch Từ `Little Akihabara V1/V2` & `Japanese Building V1/V2`

Như đã phát hiện ở Mục 2, cả 4 gói mod của `w3_Mods_Reborn` đều đính kèm nguyên file `LAn.IPL` và `LAwn.IPL` của GTA SA gốc, vô tình làm trồi lên mặt đất **`13` cái cây `veg_bevtree1` ở `LAn.IPL`** và **`58` cái cây `tree_hipoly` ở `LAwn.IPL`** mà đội ngũ `Stars & Stripes (S&S)` đã hạ ngầm xuống `Z = -29m..-38m`.

Bằng công cụ diff tự động (`inspect_ky2_deep.py`), chúng ta đã **tách riêng chính xác các dòng `inst` prop mới** của 4 bản mod này mà **không chạm vào bất kỳ cái cây nào của `S&S`**:

1. **`Little Akihabara V1` (`#155181`) — `9` dòng prop ngoại cảnh tại Downtown LS (`LAn`)**:
   - Gồm `3` hàng rào `bar_barrier10` (`ID 1640`), `4` cụm ghế chờ `chair_1` (`ID 2723`) và `2` máy bán hàng `vendmachfd` (`ID 955`) quanh tọa độ `X ≈ 1522..1536, Y ≈ -1479..-1461, Z ≈ 12.55m`.
2. **`Little Akihabara V2` (`#221340`) — `22` dòng prop khu vực sân thượng (`Roofstuff`) tại Downtown LS (`LAn`)**:
   - Gồm ghế băng, bàn ghế sân thượng (`cj_table_03`, `chair_1`), máy bán nước (`vendmachfd`, `cj_ext_vend`), đèn trang trí và cây cảnh trên tầng thượng tòa nhà `lanblokb2` tại `X ≈ 1509..1535, Y ≈ -1481..-1461, Z ≈ 44.6m`.
3. **`Japanese Building V1 (`OtakuShoppu` #159896) & V2 (`Kawaiiboutique` #175652)` — `23` dòng prop vỉa hè tại Temple (`LAwn`)**:
   - Gồm bàn ghế quán cà phê ngoài trời (`dyn_table_02`, `PARKBENCH1`), cột điện (`telgrphpole02`) và đèn trụ (`bollardlight`) dọc vỉa hè tòa nhà `sunrise09_lawn` tại `X ≈ 1110..1153, Y ≈ -1202..-1166, Z ≈ 17.5m..22.8m`.

Toàn bộ `9 + 22 + 23 = 54` dòng `inst` prop sạch này sẽ được lưu vào file độc lập `data\maps\wibu\wibu_ls_shops_props.ipl` khi đóng gói, giữ nguyên 100% file `data\maps\LA\LAn.IPL` và `LAwn.IPL` của `Project Eagle`.

---

## 5. Bảng Quy Hoạch Cấp Phát Model ID & Tọa Độ Của Kỳ 2 (Tích Hợp Với Kỳ 1)

Để chuẩn bị cho bước **Đóng gói hợp nhất (`Unified Packaging`)** ở cuối lộ trình, dưới đây là bảng phân bổ dải Model ID trống của `Project Eagle` cho toàn bộ các tài nguyên đã bóc tách ở **Kỳ 1** và **Kỳ 2**:

| Dải Model ID Cấp Phát | Thuộc Khối ID Trống Của `Project Eagle` | Số Lượng ID | Module / Bản Mod Sử Dụng | Phân Khu Đặt Tọa Độ (`Zone`) |
| :--- | :--- | :--- | :--- | :--- |
| **`3194..3197`** | Khối `3194..3213` (`20` IDs) | `4` IDs | **[Kỳ 1]** Tháp `TorreTokyo` (`Tokyo Tower` — `012 TorreTokyo`) | Downtown Los Santos (`X = 1480.7, Y = -1790.3`) |
| **`3198`** | Khối `3194..3213` (`20` IDs) | `1` ID | **[Kỳ 2]** Lâu đài cổ Nhật Bản (`Japanese Castle #101385` tách độc lập) | `WIBU-05` (Đảo Đền Thờ `Pera Loca`) |
| **`3199`** | Khối `3194..3213` (`20` IDs) | `1` ID | **[Kỳ 2]** Tòa nhà `Kawaiiboutique` (`Japanese Building V.02 #175652` nhân bản độc lập) | `WIBU-01` (Phố thương mại Đảo `MKLAS`) |
| **`3200..3213`** | Khối `3194..3213` (`20` IDs) | `14` IDs | **[Kỳ 1]** Bộ 14 cây Hoa Anh Đào độc lập (`011 Cherry tree` — bảo vệ cây cọ Vice City/Leonida) | `WIBU-01`, `WIBU-03`, `WIBU-05`, `WIBU-06` |
| **`11800..11848`** | Khối `11754..12799` (`1,046` IDs) | `49` IDs | **[Kỳ 2]** Quần thể đô thị `Kerorin Capital 1.0` (`#153898` — thay cho dải `14901..14982` bị trùng) | `WIBU-01` (Phân khu Bắc Đảo `MKLAS`) |
| **`11850..11924`** | Khối `11754..12799` (`1,046` IDs) | `75` IDs | **[Kỳ 2]** Khu phố điện tử `Akihabara Electronic Town` (`#155560` — thay cho dải `2..3141` đụng `peds.ide`!) | `WIBU-01` (Phân khu Đông Nam Đảo `MKLAS`) |
| **`11925..12049`** | Khối `11754..12799` (`1,046` IDs) | `125` IDs | **[Kỳ 2]** Khu phố `Sixth Street — Zenless Zone Zero` (`#222933`) & `Utagawa Machi Ex` | `WIBU-01` (Phân khu Trung tâm Đảo `MKLAS`) |
