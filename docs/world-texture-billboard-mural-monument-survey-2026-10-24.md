# Báo Cáo Khảo Sát Toàn Diện Các Vị Trí & Hạng Mục Công Trình Có Thể Thay Đổi Texture (Billboard, Mural, Tượng Đài, Poster, Biển Hiệu, Nội Thất) Trên Thế Giới `gta sa gameplay-lab`

- **Ngày khảo sát**: `2026-10-24`
- **Tác giả**: `Antigravity` (`f700a3ad-8aae-437a-8b96-ef20a9a45cbe`)
- **Đích khảo sát (chỉ đọc 100%)**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Dữ liệu bằng chứng nhị phân trích xuất**: [`evidence/world-texture-billboard-mural-survey-2026-10-24.json`](evidence/world-texture-billboard-mural-survey-2026-10-24.json)
- **Phiếu công việc điều phối**: [`work-items/2026-10-24-antigravity-world-texture-billboard-mural-survey.md`](work-items/2026-10-24-antigravity-world-texture-billboard-mural-survey.md)

> **Phạm vi tài liệu**: Đây là **báo cáo khảo sát thực địa (Read-Only Ground-Truth Survey)** toàn bộ dữ liệu `.IDE`, `.IPL` (text + binary stream), `.IMG` và `.TXD` (`RwRaster`) của bản `gta sa gameplay-lab` để liệt kê **tất cả các nơi và các loại bề mặt công trình** có thể biến đổi thành phong cách Wibu / Anime / Gacha song song với luồng thêm map mod mới. Tài liệu này chỉ khảo sát **có những gì, nằm ở đâu, quy mô bao nhiêu**, chưa bàn về giải pháp kỹ thuật hay quy trình đóng gói.

---

## 1. Quy Mô Tổng Thể Của Thế Giới `gta sa gameplay-lab` Qua Quét Nhị Phân

Khác với GTA San Andreas gốc chỉ có 1 bang, `gta sa gameplay-lab` (**Project Eagle / Stars & Stripes `S&S`**) là một siêu lục địa `48 km × 48 km`. Kết quả quét toàn bộ file cấu hình (`data/default.dat`, `data/gta.dat`), `195+` file `.IDE`, `613+` file `.IPL` và `59` kho `.IMG` bản đồ/kiến trúc/nội thất (đã loại trừ các kho nhân vật `COMPONENTPEDS.img`, xe cộ `vehicles.img`, vũ khí `weapons.img` và hoạt ảnh `cuts.img`):

| Chỉ số thực tế trong `gta sa gameplay-lab` | Số lượng | Ý nghĩa đối với việc khảo sát bề mặt công trình |
|---|---:|---|
| **Tổng số định nghĩa Model (`.IDE` `objs` + `tobj`)** | **`59,635` models** | Toàn bộ nhà cửa, biển quảng cáo, tượng đài, đèn neon, nội thất và prop đường phố trên toàn bản đồ. |
| **Tổng số vật thể đặt trên bản đồ (`.IPL` `inst`)** | **`147,407` vị trí** | Gồm `84,568` vị trí trong file `.IPL` văn bản và `62,839` vị trí trong file `bnry` `.IPL` nhị phân đóng gói trong `.IMG`. |
| **Tổng số kho `.IMG` thế giới/kiến trúc/prop đã quét** | **`59` kho `.IMG`** | Bao gồm San Andreas, Liberty City, Vice City, Carcer City, Cottonmouth, Bullworth, Chicago, Leonida, các bang S&S và lớp phủ `CUSTOM\`. |
| **Tổng số thư viện `.TXD` thế giới (`RwTexDictionary`)** | **`4,857` file `.TXD`** (`4,365` tên duy nhất) | Chứa toàn bộ hình ảnh bề mặt của thế giới. |
| **Tổng số Texture đơn lẻ (`RwTextureNative` / `RwRaster`)** | **`101,147` rasters** | Trong đó có **`15,641` rasters** (trải trên **`1,497` file `.TXD` cận cảnh** + các file LOD đi kèm) thuộc nhóm Biển quảng cáo, Tranh tường, Đèn Neon, Poster, Mặt tiền cửa hàng, Tượng đài và Nội thất! |
| **Tổng số vật thể phát sáng theo giờ đêm (`tobj`)** | **`607` models** (`628` vị trí) | Các bảng đèn Neon, màn hình tòa nhà, biển hiệu sòng bạc/khách sạn tự động bật sáng khi trời tối (`20h–6h` hoặc `21h–5h`). |

### Phân bổ `147,407` vị trí vật thể 3D theo 14 Đại Khu Vực Địa Lý:

| STT | Đại Khu Vực / Bang / Thành Phố | Kho `.IMG` & Thư mục `.IDE`/`.IPL` chính | Số lượng vị trí vật thể (`.IPL`) | Đặc trưng không gian công trình có thể Wibu hóa |
|---:|---|---|---:|---|
| 1 | **Los Santos (San Andreas)** | `GAME_LA.img`, `data/maps/LA/*` | **`15,105`** | Đại lộ Vinewood, Downtown cao ốc, Rodeo/Market sang trọng, Ganton/East LS đầy tranh tường graffiti, Santa Maria Pier, Pershing Square. |
| 2 | **San Fierro (San Andreas)** | `GAME_SF.img`, `data/maps/SF/*` | **`8,944`** | Khu phố Tàu Chinatown (cổng chào, đèn lồng, cờ phướn), Pier 69, Hashbury, khu thương mại Queens & Downtown SF, trạm tàu điện `tramstop_SF`. |
| 3 | **Las Venturas (San Andreas)** | `GAME_LV.img`, `data/maps/vegas/*` | **`11,405`** | **Thiên đường đèn Neon & Tượng đài**: Đại lộ The Strip, Kim tự tháp & Tượng Nhân Sư (`Camel's Toe`), Tàu Hải Tặc, Lâu đài `Excalibur`, `Visage`, `Caligula's`, `Four Dragons`, biển `Vegas Cowboy`. |
| 4 | **Ngoại Ô & Sa Mạc San Andreas** | `GAME_SA.img`, `GAME_GRAP.img`, `GAME_GAV.img`, `game_eastsa.img` | **`13,625`** | Pano dọc quốc lộ, trạm dừng xe tải, thị trấn nhỏ (Dillimore, Palomino, Fort Carson, Bayside), tượng Gà khổng lồ (`BIG_COCK_SIGN`), đập Sherman (`dam_statues`). |
| 5 | **Liberty City & Upstate NY** | `GAME_LC.img`, `fortstaunton.img`, `misslib.ide`, `game_ups.img` | **`21,416`** | **Quảng trường Thời Đại (Star Junction / Bedford Point)** ngập tràn pano cao ốc (`tenmnt*ad`), Tượng Nữ Thần Tự Do (`Miss Liberty`), Khu Phố Tàu (`chinabanner`), Nhà hát Opera, Bảo tàng Nghệ thuật, ga tàu điện ngầm (`postersub.txd`). |
| 6 | **Vice City, Bang Leonida & Florida Keys** | `GAME_VC.img`, `GAME_BINVC.img`, `game_leored.img`, `game_leo.img`, `game_gator.img` | **`18,270`** | Dãy khách sạn Art Deco & đèn Neon dọc biển **Ocean Drive**, **Vice Point Mall** (`malltotal.txd`), Sân vận động Hyman, Phòng hòa nhạc (`concerth`, `stagestuff.txd`), Vòng đu quay (`starferriswheel_vcs`), và khu công viên chủ đề **`disney.IPL` (`disney_tex.txd`)** tại Leonida! |
| 7 | **Carcer City & Đèo Keystone** | `game_cc.img`, `GAME_KEY.img`, `S&S/MAPS/CC/*` | **`12,154`** | Thành phố công nghiệp/đô thị lớn (`759 MB` `.IMG` — lớn nhất trong các thành phố!): Khu Downtown (`dwntbuild.txd`), Khu Sân vận động (`stadareabuild.txd`), Mall, Casino, Bảo tàng (`jou_museum`), Đài thiên văn (`est_observatry`), hệ thống ga tàu điện ngầm (`cc_subway.ide`). |
| 8 | **Cottonmouth & Peachtree** | `game_cm.img` (`503 MB`), `game_peach.img`, `S&S/MAPS/CM/*` | **`7,496`** | Khu phố đêm miền Nam (`smnightclub`, `brothel`, `2tolerancezone`), Quảng trường trung tâm (`plaza.ipl`), **Phim trường Truyền hình (`tvstudio.ipl`)**, Bảo tàng (`cms_museum`), tượng Thiên thần (`angelstatuea`). |
| 9 | **Thị Trấn & Học Viện Bullworth** | `GAME_BW.img`, `S&S/MAPS/BW/*` | **`1,156`** | Khuôn viên trường học **Bullworth Academy (`tschool.IPL` — `316` models)**, Khu phố thương mại (`tbusines.IPL`), Khu hội chợ/công viên giải trí (**`tcarni.IPL`**) và đường đua Go-Kart (`tgokart.IPL`). |
| 10 | **Chicago (Windy Bay) & Prairie** | `game_pra.img`, `S&S/MAPS/PRA/CHICAGO/*` | **`563`** | Quần thể cao ốc Downtown Chicago & tháp **Sears Tower** (`wb_sears*`), hệ thống biển quảng cáo dùng chung `pr_billbshare.txd` (`pr_billb1..5`) và tường áp phích `Bow_posterwallold`. |
| 11 | **Nội Thất Toàn Cục, Sân Vận Động & Prop Đường Phố** | `Interiors.img` (`148 MB`), `Generic.img`, `sasprops.img`, `LCisland.img` | **`3,662`** | Hơn `185` không gian nội thất (siêu thị 24/7, quán ăn, bar, club, casino, nhà riêng CJ, gym, tiệm quần áo, sân vận động) và hàng ngàn bốt điện thoại, trạm xe buýt, sạp báo, máy bán nước tự động. |
| 12 | **Các Bang S&S Khác (`Anneland`, `Cheyenne`, `Rose`, `Dublin`, `Cordillera`, `Independence`, `Robada`, `Lincoln`, `Jackalope`, `Argal`, `Perra Loca`)** | `game_anne.img`, `game_cy.img`, `game_rc.img`, `game_ir.img`, `game_ic.img`, `game_rob.img`... | **`31,260`** | Cổng chào Phố Tàu ở Rose City (`rcchinatowngate`), Bảo tàng UFO ở Robada (`ufo_museum`), Ngọn hải đăng đảo Perra Loca (`sp_lighthouse`), cùng hàng trăm biển quảng cáo quốc lộ (`aw_billb00_grp19.txd`, `frostwater.txd`, `rosecity.txd`, `new_ireland.txd`). |
| 13 | **Lớp Phủ Đang Cài Trong `CUSTOM\` (`GROUP_A`, `GROUP_B1`, `wibu01`)** | `GROUP_A_MODS.IMG` (`442 MB`), `GROUP_B1_TEXTURES.IMG` (`310 MB`), `wibu01_japan_island.img` (`135 MB`) | **`2,351`** | `GROUP_B1` đang giữ `269` file `.TXD` (`6,057` rasters) biển hiệu/quảng cáo Mỹ thập niên 90 tại LS/SF/LV; `GROUP_A` giữ `269` file `.TXD` (`3,507` rasters) cửa hàng mở rộng EHI, Commercial Mod & Street Art; `wibu01` là đảo Akihabara/Kerorin mới. |

---

## 2. Phân Loại Chi Tiết 7 Hạng Mục Bề Mặt Công Trình Có Thể Thay Đổi Texture

Qua giải phẫu toàn bộ `59,635` models và `101,147` rasters, mọi vị trí có thể "Wibu hóa" bằng cách thay đổi texture (hoặc mặt phẳng gắn trên công trình) được chia làm **7 hạng mục lớn** dưới đây:

---

### Hạng Mục 1: Hệ Thống Biển Quảng Cáo Cỡ Lớn — `Billboards, Highway Gantries & Rooftop Signs`
- **Quy mô thực tế**:
  - **`168` Model khung biển quảng cáo độc lập** (`140` Near + `28` LOD) với **`695` vị trí dựng sẵn** trên khắp các đại lộ và cao tốc.
  - **`33` file `.TXD` chuyên biệt chỉ chứa biển quảng cáo** (`224` rasters) + **`178` file `.TXD` khu phố** chứa **`410` rasters biển quảng cáo** gắn trực tiếp trên sườn hoặc nóc các tòa nhà.
- **Các khu vực và đối tượng tiêu biểu**:
  1. **Khung Pano Tiêu Chuẩn Dùng Chung Toàn Bang (`Generic.img` / `dynamic.ide`)**:
     - `BillBd1` (`ID 1259`, `77` vị trí), `BillBd2` (`ID 1267`, `82` vị trí), `BillBd3` (`ID 1260`, `83` vị trí) và `BigBillBrd` (`ID 1309`, `5` vị trí) kèm bộ ba LOD `LODlBd1..3` (`193` vị trí) — dùng chung thư viện `BillBrd.txd` (`11` rasters). Tổng cộng **247 khung pano lớn** dọc các trục đường chính!
  2. **Quần Thể Pano Đại Lộ & Nóc Nhà Los Santos (`GAME_LA.img` + `GROUP_B1_TEXTURES.IMG`)**:
     - **Khu trung tâm & Thương mại (`LAn.ide`, `LAn2.ide`)**: `billbrdlan_03..11` và `billbrdlan2_01..05` dùng `billbrd01_lan.txd` & `billbrd01_lan2.txd` (chứa các tấm pano lớn `diderSachs01`, `heat_02`, `cokopops_1`, `eris_1`, `hardon_1`, `homies_2`, `prolaps01`, kèm LOD trong `lanlod.txd` & `billbrdlod_lan.txd`).
     - **Khu Sunset Strip / Vinewood / Rodeo / Mulholland (`LAw2.ide`, `LAwn.ide`, `LAhills.ide`)**: `sunbill_law2.txd` (`SunBillB01..03`, `diderSachs01`), `billbrdlawn.txd`, `lawnbillbrd.txd`, và `LAhBoards_LAh1` (`ID 13890`, dùng `lahillsads.txd` chứa `Victim_bboard`, `heat_02`, `diderSachs01` ngay trên đồi Vinewood).
     - **Khu East Los Santos (`LAe2.ide`)**: `lae2billbrds2..6` (`ID 17915..17919`) và `furnsign1_LAe2` (`ID 17535`) dùng `lae2billboards.txd` (kèm LOD `lod_billbrds` trong `laeast2_lod.txd`).
  3. **Hệ Thống Pano Las Venturas & Cao Tốc Sa Mạc (`GAME_LV.img` + `GROUP_B1_TEXTURES.IMG`)**:
     - `vgebillboards.txd` (`11` rasters: `prolaps02`, `cokopops_2`, `eris_5`, `bobobillboard1`, `diderSachs01`), `vgsn_billboard.txd` (`homies_1_128`, `Victim_bboard`, `cokopops_2`), và `vgwestbillbrd15` (`ID 7914`, `vgwestabats.txd`).
  4. **Hệ Thống Pano Liberty City (`GAME_LC.img`)**:
     - **Khung pano ngoại ô & công nghiệp**: `sub_billboard1` (`ID 21253`, `50` vị trí), `sub_tripbboard` (`ID 21254`, `21` vị trí — biển 3 mặt lật!), `mak_billboardsrvc` (`ID 21260`, `13` vị trí), `mak_billboard` (`ID 23503`, `3` vị trí), `dr_billboard1` (`ID 21029`, `2` vị trí) dùng `billboard.txd`.
     - **Pano khổng lồ khu thương mại Staunton Island / Bedford Point (`comNbtm.ide`, `comSW.ide`)**:
       - `tenament1ad` (`ID 21336`), `tenement2ad` (`ID 21339`), `tenament3ad` (`ID 21337`), `tenmnt6ad` (`ID 21335`) gắn dọc mặt tiền các tòa cao ốc (kèm LOD `lodament1ad..lodmnt6ad` trong `comlod2.txd`).
       - `comsbilboard02.txd` (`billbrd_opra` `ID 22061` & `art_glry_bboard` `ID 22062` — chứa `PunkNoodle128`, `Libertyarmy128`, `Ammunation128`, `HappyBlimp128`), `comsbilboard05.txd` (`Squidboard128`), và `calahan_bboard` (`ID 22078` ngay đầu cầu Callahan).
  5. **Hệ Thống Pano Vice City & Bang Leonida (`GAME_VC.img`, `game_leored.img`)**:
     - **Downtown & Sân bay Escobar Vice City**: `doontoon13_billbrd.txd` (`10` rasters `beach289..428`) và `ap_billboard.txd` (`9` rasters `ap_billb1..4`, `ap_logos2`).
     - **Bang Leonida**: `leobill.txd` (`13` rasters pano cao tốc: `Sandario`, `FrancisVC`, `14todoelboard`, `Aloisiaboard`, `mamitasboard`).
  6. **Hệ Thống Pano Các Bang Mở Rộng (`S&S`)**:
     - **Chicago / Prairie (`game_pra.img`)**: `pr_billbd1` (`ID 83357`, `5` vị trí) và thư viện `pr_billbshare.txd` (`11` rasters `pr_billb1..5`).
     - **Anneland (`game_anne.img`)**: `aw_billb00_grp19.txd` (`16` rasters).
     - **Frostwater (`game_fw.img`)**: `billbdfw3` (`ID 42566`) & `frostwater.txd` (`ap_billb1`).
     - **Carcer City (`game_cc.img`)**: Các raster `ap_billb1..3`, `BBoardBack`, `billdetaily` nằm trong `lacwbuilds1.txd`, `lacwbuilds2.txd`, `clark.txd`, `ramirez.txd`.

---

### Hạng Mục 2: Tranh Tường Khổng Lồ, Băng Rôn Dọc Cao Ốc & Graffiti Đường Phố — `Murals, Facade Banners & Street Art`
- **Quy mô thực tế**:
  - **`119` Model tranh tường / băng rôn / graffiti độc lập** với **`374` vị trí đặt**.
  - **`49` file `.TXD` chuyên biệt về băng rôn / graffiti** (`154` rasters) + **`234` file `.TXD` kiến trúc** chứa **`750` rasters** tranh tường, cờ phướn và họa tiết mặt đứng tòa nhà.
- **Các nhóm bề mặt tiêu biểu**:
  1. **Tranh Tường Nghệ Thuật & Tranh Tường Khu Phố (`Murals & Wall Art`)**:
     - **East Los Santos / Ganton / Idlewood / El Corona**:
       - Các tòa nhà `barrio3B_LAe` (`ID 3698`, `10` vị trí) và `barrio6a_LAe2` (`ID 3704`, `4` vị trí) dùng `comedbarrio1_la.txd`, `barrio1_lae.txd` và `chicano10_lae.txd` — chứa các bức tranh tường lớn vẽ kín mặt bên các dãy nhà 1–2 tầng.
       - Gói **Street Art** đã tích hợp sẵn trong `CUSTOM\GROUP_A_MODS.IMG` cũng bổ sung các mảng tranh tường đường phố tại Los Santos.
     - **Tranh Tường Ghép & Băng Rôn Dọc Tòa Nhà Cao Tầng (Downtown LS, Rodeo, Market, SF)**:
       - Các cao ốc ở Downtown LS (`lanblokb2.txd`, `lan2.ide`) và Rodeo (`rodeo01_law2.txd`, `rodeo02_law2.txd`) có những tấm băng rôn/tranh dọc cao từ 3 đến 10 tầng nhà.
  2. **Hệ Thống `100+` Điểm Xịt Sơn Graffiti / Gang Tags (`dynamic2.ide` & `GAME_LC.img`)**:
     - **Tại Los Santos & San Fierro**: `tag_vagos` (`ID 1530`, `25` vị trí), `tag_kilo` (`ID 1525`, `18` vị trí), `tag_rollin` (`ID 1527`, `13` vị trí), `tag_front` (`ID 1524`, `12` vị trí), `tag_temple` (`ID 1529`, `11` vị trí), `tag_azteca` (`ID 1531`, `11` vị trí), `tag_01` (`ID 1490`, `6` vị trí), `tag_rifa` (`ID 1526`, `5` vị trí), `tag_seville` (`ID 1528`, `4` vị trí), `tag_danang` (`ID 3870`, `4` vị trí) — nằm trong các file `tags_LA*.txd` (`Generic.img` / `custom_mods.img`). Đây là các tấm decal phẳng (`decal mesh`) áp sát tường khắp thành phố, cực kỳ dễ thay bằng граffiti/sticker/art Anime!
     - **Tại Liberty City (`comSW.ide`)**: `tag1..tag5` (`ID 22070..22074`) dùng `comhilo_tags.txd` (`8` rasters `tag_gaz1..7`).
  3. **Băng Rôn Treo Đường Phố, Phố Tàu & Sự Kiện (`Banners, Lanterns & Bunting`)**:
     - **Liberty City Chinatown (`temppart.ide`)**: `chinalanterns` (`ID 21093`, `22` vị trí), `iten_chinatown2` (`ID 21039`, `12` vị trí), `chinabanner1..3` (`ID 21080..21083`, `25` vị trí), `iten_chinatown4` (`ID 21040`, `4` vị trí) dùng chung `chinabanner.txd` (`6` rasters).
     - **Băng rôn giải đua & sự kiện ngoài trời**: `mtb_banner1` (`ID 3281`, `29` vị trí tại vùng núi Mount Chiliad / Countryside, dùng `mtb_banners.txd`), dây cờ `des_bunting` tại cầu cảng Santa Maria (`pierc_law2.txd`).
     - **Băng rôn treo trong Trung tâm thương mại & Cửa hàng (`props2.ide`)**: `CJ_BANNER01..16` (`ID 2656..2720`, hơn `60` vị trí treo trần) dùng `cj_banner.txd`, `cj_banner2.txd`, `cj_banner3.txd`, `cj_base5.txd`, `skate_shop.txd`.
     - **Băng rôn sân khấu ban nhạc (`GAME_VC.img`)**: `stagestuff.txd` (`19` rasters) và `lf_mediastage.txd` (`15` rasters: `lfbanner`, `lovefistlogo`, `tshirtfront`).

---

### Hạng Mục 3: Biển Đèn Neon Ban Đêm (`tobj`), Màn Hình LED Điện Tử & Đại Lộ Sòng Bạc — `Neon Signs, Electronic Screens & Timed Night Objects`
- **Quy mô thực tế**:
  - **`607` Model phát sáng theo giờ đêm (`tobj` trong `.IDE`)** với **`628` vị trí đặt**, cộng thêm **`236` Model biển đèn Neon/Casino tĩnh** (`288` vị trí).
  - **`166` file `.TXD` chuyên về Neon / Strip / Biển sáng** (`1,338` rasters).
- **Phân bổ các "Kinh đô ánh sáng" trong game**:
  1. **Đại Lộ Sòng Bạc Las Venturas (`VegasN.ide` `29` `tobj`, `vegasE.ide` `27` `tobj`, `VegasW.ide`)**:
     - Các bảng đèn chữ chạy, màn hình điện tử và biển hiệu khổng lồ: `vgnfremnt2.txd` (`vgsn_scrollsgn`, `casinolit2_128`, `vgsN_casadd01`, `girlsneon_256`), `vgnbballsign2.txd` (`scoreboardvgn_256`, `ws_xenon_1`), `vegasneon.txd` (`visageneon` `ID 7892`), `miragecasino2.txd` (`visagesign1` `ID 7583`), `ab_caligulasfront.txd` (`sign_Caligulas2`).
  2. **Dải Khách Sạn Art Deco & Phố Đêm Vice City (`washintn.ide` `24` `tobj`, `downtown.ide` `22` `tobj`, `washints.ide` `22` `tobj`, `littleha.ide` `20` `tobj`, `oceandrv.ide` `19` `tobj`, `oceandn.ide` `18` `tobj`, `empire.ide` `17` `tobj`, `nbeachbt.ide` `17` `tobj`)**:
     - Tổng cộng **hơn `175` vật thể đèn Neon ban đêm (`tobj`) chỉ riêng tại Vice City**!
     - Tiêu biểu: `nbwneon01..02` (`ID 28341..28342`), `starblocks03neonvcs` (`ID 28343`), `nbwmidland_neon` (`ID 28344`, dùng `nbw_neon_vcs.txd`), `xod_leslie_neon` (`ID 27871`) & `xod_macalpin_neon` (`ID 27870`, dùng `xrefhotels.txd`), cùng bộ thư viện mặt tiền phố biển `ocmiamistrip5.txd`, `ocmiamistrip7.txd`, `ocmiamistrip9.txd`, `washmiamistrip4.txd`.
  3. **Liberty City — Khu Thương Mại Staunton Island & Phố Đỏ Portland (`industNE.ide` `25` `tobj`, `comSE.ide` `16` `tobj`, `comNbtm.ide` `11` `tobj`)**:
     - Hệ thống hộp đèn cao ốc `comlights01..09` (`ID 21935..21949`, dùng `comlights.txd`), đèn pha chiếu trời `com_spotbeams` (`ID 21950`, `casino.txd`) và đèn đỉnh tòa nhà Flatiron `flatironlt` (`ID 21547..21548`).
  4. **Carcer City, Peachtree & Cottonmouth (`game_peach.ide` `35` `tobj`, `lacE.ide` `32` `tobj`, `smnightclub.ipl`)**:
     - `67` mô hình chiếu sáng ban đêm tại Peachtree và Đông Carcer City, cùng khu hộp đêm `smnightclub` (`155` vị trí prop/biển đèn) ở Cottonmouth.

---

### Hạng Mục 4: Áp Phích (Posters), Mặt Tiền Cửa Hàng (Storefronts), Nhà Chờ Xe Buýt, Sạp Báo & Máy Bán Hàng Tự Động — `Posters, Storefronts, Transit & Vending`
- **Quy mô thực tế**:
  - Đây là **hạng mục có mật độ xuất hiện dày đặc nhất ở tầm mắt người chơi đi bộ**: **`1,279` Model trực tiếp** (`3,410` vị trí đặt) và **`9,089` rasters** nằm trong **`1,308` file `.TXD`** khắp các thành phố!
- **Chi tiết từng nhóm vật thể tầm mắt (`Eye-Level Street & Shop Surfaces`)**:
  1. **Nhà Chờ Xe Buýt, Trạm Tàu Điện, Bốt Điện Thoại & Sạp Báo (`dynamic.ide` / `dynamic2.ide`)**:
     - **Nhà chờ xe buýt có khung kính quảng cáo (`bustopm`, `ID 1257`)**: **`152` vị trí** khắp các thành phố, dùng chỉ **1 file `bustopm.txd` duy nhất**! (Đổi 1 texture trong `bustopm.txd` là toàn bộ 152 trạm xe buýt biến thành hộp đèn poster Anime/Gacha!).
     - **Trạm tàu điện San Fierro (`tramstop_SF`, `ID 1375`)**: **`25` vị trí**, dùng `tramstop.txd`.
     - **Bốt điện thoại công cộng**: `phonebooth1` (`ID 1216`, **`190` vị trí**, dùng `dynphn.txd`) và `CJ_PHONE_KIOSK2` (`ID 1346`, **`60` vị trí**, dùng `Roadside.txd`).
     - **Sạp báo & Hộp bán báo tự động**: `newstandnew1..5` (`ID 1285..1289`, tổng cộng **`233` sạp báo** trên vỉa hè, dùng chung `newstand.txd`!) và máy bán báo `papermachn01` (`ID 1293`, **`69` vị trí**, dùng `dynnewstnd2.txd`).
  2. **Máy Bán Nước Tự Động, Máy Bán Kẹo, Cây ATM & Xe Bán Đồ Ăn Dạo**:
     - **Máy bán nước ngọt & kẹo tự động**: `CJ_EXT_SPRUNK` (`ID 955`, `33` vị trí ngoài trời, `CJ_EXT_VEND.txd`), `CJ_EXT_CANDY` (`ID 956`, `15` vị trí ngoài trời, `CJ_EXT_VEND2.txd`), `CJ_SPRUNK1` (`ID 1775`, `16` vị trí trong nhà, `CJ_COMMERCIAL.txd`), `CJ_CANDYVENDOR` (`ID 1776`, `16` vị trí, `CJ_COMMERCIAL.txd`), `vendmach` & `vendmachfd` (`ID 1209` & `1302`, `vend.txd`).
     - **Xe đẩy bán đồ ăn vỉa hè (`foodKarts.txd`)**: `chillidogcart` (`ID 1340`, `15` vị trí), `noodlecart_prop` (`ID 1342`, `9` vị trí — quầy mì kéo!), `icescart_prop` (`ID 1341`, `7` vị trí — xe kem!).
  3. **Áp Phích Dán Tường, Khung Tranh, Tạp Chí & Poster Cửa Hàng (`Posters, Frames & Print Media`)**:
     - **Poster cửa hàng tiện lợi 24/7 & Siêu thị**: `7_11_posters.txd`, `711_sfw.txd`, `711c.txd`, `7_11_door.txd` (`Gen_doorEXT7_11L/R`).
     - **Poster nhà ga tàu điện ngầm Liberty City**: `postersub.txd` (`41` rasters poster quảng cáo dưới lòng đất: `ZIP_128lit`, `SUMO_128lit`, `Squidboard128`, `PETROL_128lit`...).
     - **Tường dán đầy áp phích ở Chicago / Prairie & Carcer City**: Raster `Bow_posterwallold`, `bandposter1_64` trong `pr_props.txd`, `upstate.txd`, `ramirez.txd`.
     - **Khung tranh & Poster treo tường nội thất (`props.ide`, `props2.ide`)**: `Frame_Clip_1..6` (`ID 2254..2259`, `Picture_frame_clip.txd`), `Frame_WOOD_1..5` & `Frame_Thick_1..5` (`Picture_frame.txd`), `CJ_BURGER_POSTER` (`ID 2641`, `CJ_BURG_SIGN2.txd`), tạp chí trên bàn `gb_magazines01.txd` (`Interiors.img`).
  4. **Mặt Tiền Cửa Hàng, Chuỗi Thương Hiệu & Trung Tâm Thương Mại (`Storefronts & Malls`)**:
     - **Tại Los Santos, San Fierro, Las Venturas**: Đang được gom tập trung tới **`269` file `.TXD` (`6,057` rasters)** trong `CUSTOM\GROUP_B1_TEXTURES.IMG` và **`269` file `.TXD`** trong `CUSTOM\GROUP_A_MODS.IMG` (`lashops93_las2.txd`, `lashops1b_las2.txd`, `cuntwshopscs_t.txd`, `smallertxd.txd`...).
     - **Tại Vice City (`GAME_VC.img`)**: Hệ thống cửa hàng rất rõ ràng theo từng cụm file `.TXD`: `dt_shops13.txd` (`73` rasters), `shops1_vcs_verdi.txd` (`62` rasters), `dts_shops.txd` (`58` rasters), `malltotal.txd` (`56` rasters — toàn bộ đại siêu thị **Vice Point Mall**), `shops1_vcs_gorilla.txd` (`52` rasters), `dt_shops14.txd` (`51` rasters), `od_bigshops2.txd` (`47` rasters), `shops1_vcs_clothes.txd` (`44` rasters), `dt_shops3.txd` (`37` rasters), `dt_shops5_vcs.txd` (`34` rasters).
     - **Tại Liberty City (`GAME_LC.img`)**: `posh_shop_lcs.txd` (`44` rasters), `comshopinc.txd`, `comhilo3shps.txd`, tiệm Internet `tw@t_cafe` (`ID 22095`, `tw@t.txd`).
     - **Tại Carcer City (`game_cc.img`)**: `dwntbuild.txd` (`77` rasters biển hiệu), `lacwbuilds1.txd` (`71` rasters), `lacwbuilds2.txd` (`88` rasters), `stadareabuild.txd` (`67` rasters), `centralbuild.txd` (`48` rasters), `drugstore.txd` (`34` rasters), `ramirez.txd` (`34` rasters).

---

### Hạng Mục 5: Tượng Đài, Điêu Khắc, Cổng Chào, Công Trình Biểu Tượng & Kỳ Quan — `Monuments, Statues & Iconic Landmarks`
- **Quy mô thực tế**:
  - **`130` Model tượng đài / điêu khắc trực tiếp** (`221` vị trí) và tổng cộng **`551` Model quần thể công trình biểu tượng (Landmarks)** trên khắp các thành phố.
  - **`24` file `.TXD` chuyên biệt cho Tượng đài / Kỳ quan** (`455` rasters) + **`50` file `.TXD`** chứa **`300` rasters** phù điêu, tượng đá, cổng chào.
- **Danh mục các Tượng Đài & Biểu Tượng Đáng Chú Ý Nhất Theo Từng Thành Phố**:
  1. **Liberty City (`GAME_LC.img`)**:
     - **Tượng Nữ Thần Tự Do (`Miss Liberty` — `S&S/Cdimages/liberty/misslib.ide` & `misslib.ipl`)**:
       - Gồm `mlb1` (`ID 33000`), `mlb2` (`ID 33001` — phần thân & đầu tượng ở độ cao `Z = 107.6m`), `mlst1` (`ID 33002` — bệ tượng), `liisle` (`ID 33003` — đảo), kèm 4 model LOD `lodmlb1..lodliisle` (`ID 33004..33007`) tại tọa độ `(14915.0, 6523.6)`. Tất cả dùng chung **`missliberty.txd` (`44` rasters)**!
     - **Tòa nhà Empire State (`empirestate`, `ID 21957`, `cempirest.txd`) & Flatiron (`flatiron1..1c`, `ID 21390..21392`)** tại Staunton Island.
     - **Nhà hát Opera (`opera_house`, `ID 21974`, `operahouse.txd`), Bảo tàng Nghệ thuật (`artglry_stn`, `ID 21978`, `comartgaly.txd`), Viện Bảo tàng (`museum`, `ID 21853`, `comsky3.txd`), Tòa Thị Chính (`townhallbig`, `ID 21405`, `newtownhall.txd`) & Đại Giáo Đường (`clnm_cthdrlfcde`, `ID 21976`, `church.txd`)**.
     - **Quần thể Cổng Chào & Kiến Trúc Phố Tàu (`iten_chinatown37..38`, `chinabuildorn`, `china2big.txd`, `chinatowns.txd` `60` rasters)**.
  2. **Las Venturas (`GAME_LV.img`)**:
     - **Tượng Nhân Sư & Kim Tự Tháp Ai Cập (`Camel's Toe` — `vegasE.ide`)**: `sphinx02_lvs` (`ID 8396`, `sphinx01.txd`), `luxorpillar01..04_lvs` (`ID 8397, 3441, 3494` — `46` cột trụ khắc chữ tượng hình Ai Cập, dùng `luxorpillar1..04.txd`) và `luxorland01_lvS` (`ID 8398`, `luxorland.txd`) tại `(2216.8, 1285.7)`.
     - **Tàu Hải Tặc Khổng Lồ & Đầu Lâu (`Pirates in Men's Pants`)**: `pirtehtl01..02_lvS` (`ID 8421..8422`, `pirateland.txd`) và `prtskllsgn02_lvs` (`ID 8423`, `pirateship01.txd` `28` rasters).
     - **Lâu Đài Hiệp Sĩ & Ngọn Đuốc (`Come-A-Lot / Excalibur`)**: `excalibur.txd` (`24` rasters) & `exbrtorch01` (`ID 3525`, `16` vị trí, `excaliburtorch.txd`).
     - **Biển Hiệu Cao Bồi Khổng Lồ (`vegascowboy1..3`, `ID 7072..7073`, `vgnfremntsgn.txd`)** tại `(2169.8, 2160.3, 50.0)`.
     - **Tượng Gà Trống Khổng Lồ Giữa Sa Mạc (`BIG_COCK_SIGN`, `ID 3334`, `3` vị trí, `cxref_desert.txd`)** & **Tượng Đập Thủy Điện Sherman (`dam_statues`, `ID 11489`, `desertdam.txd`)**.
  3. **Los Santos & San Fierro (`GAME_LA.img`, `GAME_SF.img`)**:
     - **Quảng trường Pershing Square & Đài phun nước trung tâm LS**: `PershingSq1..2_LAn` (`ID 3985, 4186`) & `PershingPool_LAn` (`ID 4206`), dùng `pershingsq.txd` (`13` rasters, có cả phù điêu đại bàng `posh_eagle13_sfe`).
     - **Đài Thiên Văn Griffith (`griffithoblas`, `ID 4825`, `griffobs_las.txd`)** tại `(1146.0, -2037.0, 65.5)`.
     - **Vòng Đu Quay Cầu Cảng Santa Maria (`ferris01_LAw2`, `ID 6298`, `pierb_law2.txd`)** tại `(389.8, -2028.5)`.
     - **Cầu Cảng Pier 69 & Phố Tàu San Fierro**: `pier69.txd` (`30` rasters) và `chinatownsfe.txd` (`38` rasters: `chtown4_sf..chtown8_sf`).
     - **Các bức tượng trong dinh thự & Atrium (`props2.ide`, `int_LA.ide`)**: Bộ tượng rời `CJ_S1_base / Head / torso / Larm / Rarm / legs` (`ID 2756..2761`, `cj_statue_2.txd`), `CJ_STAT_2` (`ID 2744`, `cj_statue_1.txd`), và `carter_statue` (`ID 14467`, `Carter_block_2.txd`).
  4. **Vice City & Bang Leonida (`GAME_VC.img`, `game_leored.img`)**:
     - **Khu Công Viên Chủ Đề `Disney` tại Bang Leonida (`S&S/MAPS/LEO/disney.IPL` & `game_leored.ide`)**:
       - Gồm **`22` mảnh kiến trúc độc lập `disney00..disney21` (`ID 92877..92898`)** tại tọa độ `(13122.2, -5645.6)`, tất cả dùng chung thư viện **`disney_tex.txd` (`60` rasters)**!
     - **Vòng Đu Quay Vice City (`nbw_ferriswheel_vcs`, `ID 28219..28220`, `starferriswheel_vcs.txd`)** và **Ngọn Hải Đăng Ocean Drive (`od_lightext`, `ID 26990`, `od_lighthouse.txd`)**.
  5. **Bullworth, Chicago, Carcer City, Cottonmouth, Rose City & Robada (`S&S`)**:
     - **Học Viện Bullworth (`tschool.IPL`, `bw_tschool.txd`) & Khu Hội Chợ Carnival (`tcarni.IPL`)**: Biểu tượng huy hiệu trường học, tháp đồng hồ, cờ hiệu và cổng hội chợ.
     - **Tháp Sears Tower tại Chicago (`wb_searsmain / top / bits`, `ID 83014..83018`, `pr_WBsearstow.txd`)** cao tới `Z = 402.6m`.
     - **Cổng Chào Phố Tàu tại Rose City (`rcchinatowngate`, `ID 36908`, `rosecity.txd`)**.
     - **Bảo Tàng UFO tại Robada (`ufo_museum`, `ID 38086`, `nrtdesgen.txd`)**, **Bảo Tàng Carcer City (`jou_museum`, `ID 152525`)**, **Đài Thiên Văn Carcer (`est_observatry`, `ID 151441`)** và **Bảo Tàng Cottonmouth (`cms_museum`, `ID 95863`, có tượng `angelstatuea`)**.

---

### Hạng Mục 6: Không Gian Nội Thất, Sân Vận Động, Phim Trường, Sân Bay & Ga Tàu Điện Ngầm — `Interiors, Stadiums, TV Studios, Subways & Airports`
- **Quy mô thực tế**:
  - **`1,449` Model nội thất/sân vận động/nhà ga trực tiếp** (`1,597` vị trí) và **`4,261` rasters** trong **`338` file `.TXD`** nội thất/đấu trường.
- **Các không gian nổi bật**:
  1. **Phim Trường Truyền Hình Cottonmouth (`S&S/MAPS/CM/levels/tvstudio.ipl` — `80` vị trí, `ID 111300..`)**: Một phim trường TV hoàn chỉnh bên trong nội thất (`interior = 8`) với các phông nền sân khấu, bảng hiệu studio và phòng quay.
  2. **Sân Vận Động & Trường Đua (`stadint.ide`, `stadiumint_vcs.ide`, `clnm_stadium` LC, `stadareabuild.txd` Carcer)**: Chứa hàng loạt dải băng rôn quảng cáo quanh khán đài (`stad_tag.txd`, `ring_ad`, `scoreboard`).
  3. **Hệ Thống Máy Chơi Game Thùng (Arcade Cabinets) & Màn Hình TV (`props2.ide` + `GROUP_A_MODS.IMG`)**:
     - `CJ_COIN_OP`, `CJ_COIN_OP_1`, `NEIL_SLOT` (`ID 2681, 2778, 2640`) cùng bộ `new_cabinets.txd`, `new_cabinets2.txd`, `new_cabinets3.txd` đang nằm trong `CUSTOM\GROUP_A_MODS.IMG` — có thể thay vỏ thùng máy điện tử và màn hình game bằng các tựa game Anime/Gacha.
  4. **Ga Tàu Điện Ngầm Liberty City (`subway.txd`, `subway_comtop.txd`, `comsub_b/c.txd`, `postersub.txd`) & Tàu Điện Ngầm Carcer City (`cc_subway.ide`)**: Các dãy hành lang ngầm có khung treo bảng thông báo và poster quảng cáo.

---

### Hạng Mục 7: Biển Báo Giao Thông, Cổng Chào Thành Phố, Mái Hiên & Cờ Phướn — `Flags, Road Gantries & Canopies`
- **Quy mô thực tế**:
  - **`138` Model trực tiếp** (`782` vị trí) và **`422` rasters** trong **`171` file `.TXD`**.
- **Ví dụ điển hình**:
  - Hệ thống biển chỉ dẫn cao tốc trên cao (`gen_roadsign1..2`, `cm_roadsign100..105`, `samproadsigns.txd` `50` rasters), biển chào mừng sân bay (`airwelcomesign_sfse`), mái hiên cửa hàng (`chinawning69`, `ws_canopy1..2`, `mallcanopy`), cờ hiệu và cột đèn treo phướn (`dynsigns.txd`, `streetlights.txd`).

---

## 3. Ba Kiến Trúc Lưu Trữ Texture Thực Tế Trong `gta sa gameplay-lab` (Cần Lưu Ý Khi Khảo Sát)

Qua việc quét toàn bộ `4,857` file `.TXD`, cần ghi nhận một đặc điểm kiến trúc rất quan trọng của bản `gta sa gameplay-lab` (kết hợp giữa nền GTA SA gốc, đại bản đồ `S&S` và các gói `GROUP_A` / `GROUP_B1`):

| Kiểu cấu trúc `.TXD` trong game | Tỷ trọng & Phạm vi | Đặc điểm nhận diện thực tế | Ví dụ điển hình trong `gta sa gameplay-lab` |
|---|---|---|---|
| **Kiểu 1: Thư viện `.TXD` Chuyên Biệt Theo Đạo Cụ (`Dedicated Prop / Billboard TXD`)** | Toàn bản đồ (`Generic.img`, `Interiors.img`, `LA/SF/LV/LC/VC`) | Toàn bộ file `.TXD` chỉ phục vụ cho 1 hoặc một nhóm biển quảng cáo / trạm xe buýt / sạp báo / tượng đài. Đổi 1 raster trong đây sẽ tự động cập nhật hàng chục đến hàng trăm vị trí giống nhau trên phố. | • `bustopm.txd` (`152` trạm xe buýt)<br>• `BillBrd.txd` (`247` pano lớn)<br>• `newstand.txd` (`233` sạp báo)<br>• `billbrd01_lan.txd`, `lae2billboards.txd`, `vgebillboards.txd`<br>• `missliberty.txd` (Tượng Nữ Thần Tự Do)<br>• `disney_tex.txd` (Khu Disney Leonida)<br>• `postersub.txd` (`41` poster tàu điện ngầm LC) |
| **Kiểu 2: Thư viện `.TXD` Theo Ô Phố / Cụm Tòa Nhà (`District / Building Block TXD`)** | San Andreas (`LA/SF/LV`), Vice City (`GAME_VC.img`), Liberty City (`GAME_LC.img`) | Một file `.TXD` chứa `15–75` rasters của một dãy phố (gồm tường gạch, cửa sổ, mái nhà **VÀ** vài tấm biển quảng cáo/tranh tường/biển hiệu cửa hàng gắn liền vào mesh tòa nhà đó). | • `chicano10_lae.txd` (`46` rasters East LS)<br>• `vgnfremnt2.txd` (`52` rasters phố đêm LV)<br>• `ocmiamistrip9.txd` (`51` rasters Ocean Drive VC)<br>• `dt_shops13.txd` (`73` rasters Downtown VC)<br>• `tenblock6a.txd` (Pano cao ốc Star Junction LC) |
| **Kiểu 3: Đại Thư Viện `.TXD` Dùng Chung Toàn Thành Phố (`City-Wide Mega-Atlas TXD` của `S&S`)** | Các thành phố mở rộng của `S&S` (`Carcer`, `Cottonmouth`, `Upstate`, `Peachtree`, `Dublin`, `Cheyenne`, `Rose`, `Independence`) | Các modder `S&S` gom **hàng trăm tới gần 1,800 rasters** của cả một bang/thành phố vào 1–3 file `.TXD` khổng lồ! Bên trong các file này chứa lẫn cả mặt đường, tường nhà lẫn toàn bộ biển quảng cáo (`ap_billb*`), cửa hàng (`247sign*`, `bincosign*`), poster (`bandposter*`) và tượng đài (`angelstatuea`). | • `upstate.txd` (`1,790` rasters, `175` rasters biển hiệu/poster)<br>• `new_ireland.txd` (`1,656` rasters, `116` biển hiệu)<br>• `cotton_s.txd` (`1,505` rasters) & `cotton_n.txd` (`1,001` rasters)<br>• `peachkt.txd` (`1,155` rasters)<br>• `lacwbuilds2.txd` (`976` rasters Carcer City)<br>• `independence.txd` (`969` rasters)<br>• `cheyene.txd` (`960` rasters) & `rosecity.txd` (`955` rasters) |

### Lưu ý đi kèm về Cặp Texture Cận Cảnh (`Near TXD`) & Tầm Xa (`LOD TXD`):
- Trong `gta sa gameplay-lab`, các biển quảng cáo lớn (như `billbrdlan_*`, `lae2billbrds*`, `BillBd1..3`, `tenament*ad`) và các tòa nhà có tranh tường lớn luôn có **1 model cận cảnh (`DrawDist < 300m`)** và **1 model LOD tầm xa (`DrawDist = 400m..1500m`)**.
- Các file LOD `.TXD` (như `lanlod.txd`, `lod_lan2.txd`, `laeast2_lod.txd`, `lodlawnsmall.txd`, `comlod1.txd`, `comlod2.txd`, `comSW_LOD.txd`, `LODodrive.txd`) chứa các bản thu nhỏ (`64×64` hoặc `128×128`, thường có hậu tố `LOD` như `diderSachs01LOD`, `heat_02LOD`, `bobobillboard1LOD`) của chính những tấm biển quảng cáo đó.
- Hiện tại, cả `CUSTOM\GROUP_B1_TEXTURES.IMG` (`269` `.TXD` — đang đè lên LS/SF/LV) và `CUSTOM\GROUP_A_MODS.IMG` (`269` `.TXD` — đang giữ nội thất EHI, cửa hàng Commercial Mod và Street Art) đều được nạp ở đầu `data/default.dat`.


---

## 4. Khảo Sát Chi Tiết Dung Lượng File (`.TXD` File Size) Trên Toàn Thế Giới `gta sa gameplay-lab`

Để đảm bảo việc thay đổi texture (Billboard, Mural, Tượng đài, Poster, Cửa hàng) **không làm phình bộ nhớ `CStreaming` (giới hạn `2,800 MB`) hoặc gây giật/khựng (stutter) khi lái xe tốc độ cao**, toàn bộ `4,857` file `.TXD` (`3,524.85 MB` tổng dung lượng thực) trên `59` kho `.IMG` thế giới đã được đo đạc từng byte.

### 4.1. Phân Phối Dung Lượng Của `4,857` File `.TXD` Thế Giới
- **Tổng dung lượng `.TXD` thế giới**: **`3,524.85 MB`** (`~3.44 GiB`)
- **Trung vị (`Median P50`)**: **`144.16 KB` / file `.TXD`** (một nửa số file `.TXD` trong game nhỏ hơn `145 KB`!)
- **Trung bình (`Mean`)**: **`743.14 KB` / file `.TXD`** (bị kéo lên bởi 45 file Mega-Atlas của `S&S`)
- **Các mốc phân vị (`Percentiles`)**:
  - `P25`: **`40.29 KB`** | `P50`: **`144.16 KB`** | `P75`: **`385.34 KB`** | `P90`: **`852.04 KB`** | `P95`: **`1.82 MB`** | `P99`: **`13.73 MB`** | `Max`: **`92.92 MB`** (`jackalope.txd`).

| Phân khúc dung lượng `.TXD` | Số lượng file `.TXD` | Tỷ lệ (%) | Bản chất các file trong phân khúc này |
|---|---:|---:|---|
| **1. `< 64 KB` (Siêu nhẹ)** | `1,559` | **`32.1%`** | Các file `.TXD` đạo cụ đơn lẻ (`newstand.txd` `16 KB`, `tags_la*.txd` `32 KB`, `dynphn.txd` `8 KB`), biển hiệu gốc (`billbrd01_lan.txd` gốc `68 KB`) và LOD nhỏ. |
| **2. `64 KB – 256 KB` (Nhẹ — Chuẩn GTA SA gốc)** | `1,597` | **`32.9%`** | Các file `.TXD` biển quảng cáo chuẩn (`BillBrd.txd` `82 KB`, `bustopm.txd` `123 KB`, `sunbill_law2.txd` gốc `139 KB`, `sphinx01.txd` `154 KB`) và các cụm nhà vừa. |
| **3. `256 KB – 512 KB` (Trung bình)** | `775` | **`16.0%`** | Các file `.TXD` ô phố đô thị, tượng đài lớn (`missliberty.txd` `513 KB`, `pershingsq.txd` `340 KB`, `pirateship01.txd` `291 KB`) và LOD toàn khu vực (`laeast2_lod.txd` `326 KB`). |
| **4. `512 KB – 1 MB` (Tiêu chuẩn khu phố đông)** | `510` | **`10.5%`** | Các khu phố sầm uất nhiều biển đèn (`vgnfremnt2.txd` `975 KB`, `ocmiamistrip9.txd` `822 KB`, `pier69.txd` `822 KB`, `chinatownsfe.txd` `880 KB`, `malltotal.txd` `1,001 KB`). |
| **5. `1 MB – 2 MB` (Lớn)** | `193` | **`4.0%`** | Thư viện poster tàu điện ngầm LC (`postersub.txd` `1.93 MB`), biển quảng cáo Chicago (`pr_billbshare.txd` `1.50 MB`) và một số file `GROUP_B1`. |
| **6. `2 MB – 5 MB` (Nặng — chủ yếu do `GROUP_B1`)** | `112` | **`2.3%`** | Các file `.TXD` biển quảng cáo bị gói `GROUP_B1_TEXTURES.IMG` phóng lên `1024×512` `DXT3` (`billbrd01_lan.txd` `3.33 MB`, `billbrd01_lan2.txd` `4.00 MB`, `lae2billboards.txd` `3.42 MB`, `vgebillboards.txd` `2.88 MB`) và khu `disney_tex.txd` (`3.03 MB`). |
| **7. `5 MB – 15 MB` (Rất nặng)** | `66` | **`1.4%`** | Các khu phố bị `GROUP_B1` / `GROUP_A` nâng lên `1024px–2048px` (`sunrise05_lawn.txd` `22.3 MB`, `lashops93_las2.txd` `10.85 MB`, `mall_law.txd` `8.18 MB`). |
| **8. `> 15 MB` (Mega-Atlas của `S&S` & Lỗi không nén)** | `45` | **`0.9%`** | Các đại thư viện gom cả thành phố của `S&S` (`jackalope.txd` `92.92 MB`, `cotton_s.txd` `69.49 MB`, `new_ireland.txd` `68.44 MB`, `cheyene.txd` `68.30 MB`, `rosecity.txd` `55.80 MB`, `lacwbuilds2.txd` `48.94 MB`) + 2 file bị tác giả `S&S` quên nén `DXT` (`apolicest.txd` `38.05 MB` & `leobill.txd` `32.37 MB`). |

---

### 4.2. Phát Hiện Quan Trọng Về Hiệu Năng: Sự Phình To Của `GROUP_B1_TEXTURES.IMG` & `GROUP_A_MODS.IMG` So Với Bản Gốc `S&S`

Khi đối chiếu trực tiếp **`269` file `.TXD` của `CUSTOM\GROUP_B1_TEXTURES.IMG`** và **`212` file `.TXD` kiến trúc của `CUSTOM\GROUP_A_MODS.IMG`** với chính các file `.TXD` cùng tên nằm trong `GAME_LA.img`, `GAME_SF.img`, `GAME_LV.img`, `GAME_SA.img` và `Interiors.img`:

| Lớp Archive đang có trong `gameplay-lab` | Số file `.TXD` đối chiếu | Tổng dung lượng gốc (`S&S Base`) | Tổng dung lượng hiện tại (`Custom Overlay`) | Hệ số phình to | Nguyên nhân kỹ thuật thực tế |
|---|---:|---:|---:|---:|---|
| **`CUSTOM\GROUP_B1_TEXTURES.IMG`** *(Biển hiệu & Quảng cáo Mỹ thập niên 90)* | `269` files | **`89.34 MB`** *(TB `340 KB`/file)* | **`309.49 MB`** *(TB `1,178 KB`/file)* | **`3.46×` (cá biệt `25× – 49.7×`)** | Các tấm biển quảng cáo gốc chỉ `256×128` hoặc `128×64` (`DXT1`) đã bị `GROUP_B1` nâng đồng loạt lên **`1024×512` hoặc `1024×1024`**, lại còn lưu ở định dạng **`DXT3` (tốn gấp đôi dung lượng `DXT1` dù biển đặc không có kênh trong suốt Alpha)** kèm đầy đủ mipmaps! |
| **`CUSTOM\GROUP_A_MODS.IMG`** *(Cửa hàng EHI, Commercial Mod, Street Art)* | `212` files | **`53.07 MB`** *(TB `250 KB`/file)* | **`202.76 MB`** *(TB `956 KB`/file)* | **`3.82×` (cá biệt `19.3×`)** | Nâng độ phân giải cửa hàng/poster lên `512×512` – `1024×512`, và riêng file `lashops93_las2.txd` (`10.85 MB`) bị nhét thêm nhiều ảnh **Non-POT** kích thước lẻ (`3000×512`, `1800×512`, `1400×600`). |

#### Bảng Đối Chiếu Trực Tiếp Dung Lượng & Kích Cỡ Các File `.TXD` Biển Quảng Cáo / Đạo Cụ Điển Hình:

| Tên file `.TXD` | Hạng mục & Khu vực | Bản gốc `S&S` (Dung lượng & Kích cỡ `W×H`) | Bản `GROUP_B1` / `GROUP_A` đang cài (Dung lượng & Kích cỡ `W×H`) | Chênh lệch |
|---|---|---|---|---:|
| **`billbrd01_lan.txd`** | `5` Pano Downtown LS | **`68.7 KB`** (`4× 256×128`, `1× 128×64`, `DXT1`) | **`3,414.4 KB` (`3.33 MB`)** (`5× 1024×512`, `DXT3`) | **`+49.7×`** |
| **`billbrd01_lan2.txd`** | `6` Pano Thương mại LS | **`90.1 KB`** (`5× 256×128`, `1× 128×64`, `DXT1`) | **`4,097.2 KB` (`4.00 MB`)** (`6× 1024×512`, `DXT3`) | **`+45.5×`** |
| **`lahillsads.txd`** | `3` Pano Đồi Vinewood | **`41.8 KB`** (`2× 256×128`, `1× 128×64`, `DXT1`) | **`2,048.6 KB` (`2.00 MB`)** (`3× 1024×512`, `DXT3`) | **`+49.0×`** |
| **`lae2billboards.txd`** | `5` Pano East LS | **`80.7 KB`** (`2× 256×256`, `2× 128×64`, `DXT1`) | **`3,499.7 KB` (`3.42 MB`)** (`3× 1024×512`, `1× 1024×1024`, `DXT3`) | **`+43.4×`** |
| **`vgebillboards.txd`** | `11` Pano Las Venturas | **`119.4 KB`** (`5× 128×64`, `4× 256×128`, `DXT1`) | **`2,945.4 KB` (`2.88 MB`)** (`9× 1024×512`, `1× 1024×1024`, `DXT1`) | **`+24.7×`** |
| **`vgsn_billboard.txd`** | `4` Pano Bắc Las Venturas | **`31.9 KB`** (`2× 128×64`, `1× 256×128`, `DXT1`) | **`896.5 KB` (`0.88 MB`)** (`3× 1024×512`, `1× 512×512`, `DXT1`) | **`+28.1×`** |
| **`sunbill_law2.txd`** | `8` Pano Sunset Strip LS | **`139.0 KB`** (`3× 256×256`, `2× 256×128`, `DXT1`) | **`1,923.0 KB` (`1.88 MB`)** (`5× 1024×512`, `1× 1024×1024`, `DXT1`) | **`+13.8×`** |
| **`sunrise05_lawn.txd`** | Cụm nhà & Pano Vinewood | **`711.0 KB`** (`max 256px`, `DXT1`) | **`22,842.2 KB` (`22.31 MB`!)** (`max 1024px`, `DXT3/DXT1`) | **`+32.1×`** |
| **`7_11_posters.txd`** | `4` Poster siêu thị 24/7 | **`72.5 KB`** (`2× 128×128`, `1× 256×256`, `1× 256×128`) | **`576.5 KB`** (`GROUP_A`: `2× 512×512`, `1× 1024×512`) | **`+8.0×`** |
| **`cj_ext_vend.txd`** | Máy bán nước Sprunk (`33` chỗ) | **`16.3 KB`** (`2× 128×128`, `DXT1`) | **`256.3 KB`** (`GROUP_A`: `2× 512×512`, `DXT1`) | **`+15.7×`** |
| **`bustopm.txd`** | Nhà chờ xe buýt (`152` chỗ) | **`123.2 KB`** (`2× 128×128`, `2× 256×256`, `DXT1/3`) | **`112.5 KB`** (`GROUP_B1`: giữ nguyên `128×128` & `256×256`) | `0.9×` |
| **`BillBrd.txd`** | Khung Pano quốc lộ (`247` chỗ) | **`82.1 KB`** (`7× 64×64`, `3× 128×128`, `1× 256×256`) | *(Chưa bị đè)* | `1.0×` |
| **`newstand.txd`** | Sạp báo vỉa hè (`233` chỗ) | **`16.4 KB`** (`2× 128×64`, `1× 128×128`, `DXT1`) | *(Chưa bị đè)* | `1.0×` |

> 💡 **Hệ quả trực tiếp cho chiến lược Mod Wibu**:
> Hiện tại `gameplay-lab` đang gánh **`309.49 MB`** của `GROUP_B1_TEXTURES.IMG` (do tác giả mod thập niên 90 dùng `1024×512` `DXT3`). Nếu khi làm Wibu World, chúng ta chuẩn hóa các tấm Billboard về **`512×256` `DXT1`** (`64 KB`/tấm không mipmap hoặc `85 KB`/tấm có mipmap — sắc nét gấp 4 lần bản gốc `256×128` nhưng **nhẹ hơn `8 lần` so với `1024×512` `DXT3` của `GROUP_B1`**!), thì việc Wibu hóa toàn bộ biển quảng cáo Los Santos / San Fierro / Las Venturas **không những KHÔNG làm nặng game thêm, mà còn GIẢM tới `60% – 75%` dung lượng bộ nhớ `CStreaming` so với trạng thái hiện tại của `gameplay-lab`!**

---

## 5. Khảo Sát Kích Cỡ (`Width × Height` — Dài × Rộng), Tỷ Lệ Khung Hình (`Aspect Ratio`) Và Định Dạng Nén Của `101,147` Rasters

### 5.1. Phân Bố Kích Cỡ (`Width × Height`) Toàn Cục Trên `101,147` Rasters Thế Giới

| Hạng | Kích cỡ `Dài × Rộng` (`Width × Height` px) | Số lượng Raster | Tỷ lệ (%) | Tỷ lệ khung (`Aspect Ratio`) | Dung lượng chuẩn 1 tấm (`DXT1` / `DXT3-5` không mipmap) | Vai trò chính trong thế giới game |
|---:|---|---:|---:|---|---|---|
| 1 | **`128 × 128`** | `30,560` | **`30.21%`** | `1:1` (Vuông) | `8 KB` / `16 KB` | Kích cỡ phổ biến số 1: Tường, cửa hàng nhỏ, graffiti (`tags_LA*`), khung tranh (`Picture_frame.txd`), tượng đài. |
| 2 | **`256 × 256`** | `25,303` | **`25.02%`** | `1:1` (Vuông) | `32 KB` / `64 KB` | Kích cỡ phổ biến số 2: Mặt tiền cửa hàng, poster nhà chờ xe buýt (`CJ_BS_MENU5`), tạp chí (`GB_magazine*`), biển vuông (`SunBillB01`), tượng Nhân Sư (`sphinxface01_256`). |
| 3 | **`64 × 64`** | `18,589` | **`18.38%`** | `1:1` (Vuông) | `2 KB` / `4 KB` | Chi tiết phụ, khung sắt mặt sau biển quảng cáo (`BBoardBack`), texture LOD tầm xa (`comlod1/2.txd`, `lanlod.txd`). |
| 4 | **`32 × 32`** | `5,551` | **`5.49%`** | `1:1` (Vuông) | `0.5 KB` / `1 KB` | Texture LOD tầm xa (`vegaselod1.txd`, `lododrive.txd`) và bóng đèn/dây điện nhỏ. |
| 5 | **`512 × 512`** | `5,251` | **`5.19%`** | `1:1` (Vuông) | `128 KB` / `256 KB` | Biển quảng cáo vuông độ nét cao (`pr_billbshare.txd`, `akihabara_town.txd`), tranh tường lớn (`barrio1_lae.txd`), mặt máy bán nước (`GROUP_A`). |
| 6 | **`256 × 128`** | `3,060` | **`3.03%`** | **`2:1` (Ngang chuẩn)** | `16 KB` / `32 KB` | **Kích cỡ chuẩn gốc của Pano/Billboard ngang** (`billbrd01_lan.txd`, `lahillsads.txd`, `vgebillboards.txd`, `idlewood6_lae.txd`). |
| 7 | **`128 × 256`** | `2,212` | **`2.19%`** | **`1:2` (Đứng chuẩn)** | `16 KB` / `32 KB` | Poster dán tường đứng, cửa ra vào, cột trụ (`luxorpillar2.txd`), biển đèn dọc (`vgnfremnt2.txd`). |
| 8 | **`128 × 64`** | `2,144` | **`2.12%`** | **`2:1` (Ngang nhỏ)** | `4 KB` / `8 KB` | Biển hiệu tên cửa hàng, bảng sạp báo (`newstand.txd`), pano cỡ nhỏ (`diderSachs01` gốc). |
| 9 | **`64 × 128`** | `1,833` | **`1.81%`** | **`1:2` (Đứng nhỏ)** | `4 KB` / `8 KB` | Cờ phướn dọc, cột trang trí, bia bắn. |
| 10 | **`512 × 256`** | `1,200` | **`1.19%`** | **`2:1` (Ngang HD)** | `64 KB` / `128 KB` | **Kích cỡ vàng cho Billboard/Poster ngang sắc nét**: Đang dùng trong `postersub.txd` (`18` poster tàu điện ngầm LC), `pr_billbshare.txd` (Chicago), `disney_tex.txd`. |
| 11 | **`64 × 32`** | `698` | `0.69%` | `2:1` (Ngang LOD) | `1 KB` / `2 KB` | Bản thu nhỏ LOD của các tấm biển quảng cáo `2:1`. |
| 12 | **`256 × 512`** | `564` | `0.56%` | **`1:2` (Đứng HD)** | `64 KB` / `128 KB` | Băng rôn treo dọc tòa nhà cao tầng, poster đứng cỡ lớn. |
| 13 | **`256 × 64` & `512 × 128`** | `698` | `0.69%` | **`4:1` (Băng rôn ngang)** | `8–32 KB` | Băng rôn ngang dài trên trán cửa hàng (`storefront fascia`), bảng tên đường/cầu cảng. |
| 14 | **`64 × 256` & `128 × 512`** | `278` | `0.27%` | **`1:4` (Phướn dọc)** | `8–32 KB` | Phướn treo dọc cột đèn hoặc sườn cao ốc (`cj_banner.txd`: `CJ_SUBURBAN_1`, `CJ_HEAT2`). |
| 15 | **`1024 × 1024` & `1024 × 512`** | `549` | `0.54%` | `1:1` & `2:1` | `512 KB – 1 MB` (`DXT3`) | Hầu hết nằm trong `GROUP_B1_TEXTURES.IMG` và `GROUP_A_MODS.IMG` (các tấm pano `1024×512`). |

---

### 5.2. Hồ Sơ Kích Cỡ (`Dài × Rộng`) & Tỷ Lệ Khung Hình Theo Từng Hạng Mục Công Trình (Cận Cảnh — `Near Only`)

Khi bóc tách riêng từng hạng mục bề mặt công trình (đã lọc bỏ các file LOD tầm xa), chúng ta thấy quy luật tỷ lệ khung hình (`Aspect Ratio`) rất rõ ràng của từng loại:

| Hạng mục bề mặt công trình | Tổng số Raster cận cảnh | Dung lượng trung bình / Raster | Top kích cỡ `Dài × Rộng` (`Width × Height`) thực tế trong game | Phân bố Tỷ lệ khung hình (`Aspect Ratio`) | Đặc điểm kỹ thuật cần nhớ |
|---|---:|---:|---|---|---|
| **1. `BILLBOARDS` (Pano & Biển quảng cáo lớn)** | `457` | `207.5 KB` *(do `GROUP_B1` kéo lên; bản gốc chỉ `16–32 KB`)* | • `256×128` (`20.4%` — gốc)<br>• `1024×512` (`17.7%` — `GROUP_B1`)<br>• `64×64` (`17.7%` — mặt lưng `BBoardBack`)<br>• `128×64` (`9.2%`)<br>• `512×512` (`8.1%`)<br>• `512×256` (`7.7%`) | • **`2:1` Ngang (`56.0%`)**<br>• **`1:1` Vuông (`38.9%`)**<br>• `1:2` Đứng (`1.8%`) | Hơn một nửa số Billboard có **tỷ lệ ngang chuẩn `2:1`** (`256×128`, `512×256`, `1024×512`). Phần còn lại (`38.9%`) lưu trong ảnh vuông `1:1` (`256×256`, `512×512`) nhưng mesh 3D cắt UV lấy phần chữ nhật! |
| **2. `MURALS, BANNERS & GRAFFITI` (Tranh tường, Phướn & Graffiti)** | `782` | `39.7 KB` | • `128×128` (`37.0%` — Graffiti `tags_LA*`)<br>• `256×256` (`22.1%` — Tranh tường `barrio1`)<br>• `64×64` (`10.7%`)<br>• `256×128` (`8.1%`)<br>• `512×512` (`6.1%`)<br>• `64×256` / `128×512` (Phướn `cj_banner`) | • **`1:1` Vuông (`78.0%`)**<br>• **`2:1` Ngang (`12.1%`)**<br>• **`1:2` & `1:4` Đứng (`7.8%`)** | Toàn bộ Graffiti đường phố (`tag_*`) là ảnh vuông **`128×128` hoặc `256×256` có nền trong suốt (`DXT3`/`DXT5`)**. Phướn treo (`cj_banner`) dùng tỷ lệ dọc **`1:4`** (`64×256` hoặc `128×512`). |
| **3. `NEON SIGNS, LED & CASINOS` (Biển đèn Neon & Màn hình)** | `830` | `34.0 KB` | • `256×256` (`28.2%` — `girlsneon_256`)<br>• `128×128` (`24.0%` — `casinolit2_128`)<br>• `64×64` (`12.3%`)<br>• `128×64` (`6.4%`)<br>• `256×128` (`5.9%`)<br>• `128×32` (`5.5%` — Dải chữ `4:1`) | • **`1:1` Vuông (`70.8%`)**<br>• **`2:1` Ngang (`15.7%`)**<br>• **`4:1` & `16:1` Dải chữ (`7.5%`)**<br>• `1:2` Đứng (`4.8%`) | Nhiều biển đèn chữ chạy (`vgsn_scrollsgn` `256×16`) hoặc bảng hiệu neon ngang dùng tỷ lệ dải hẹp **`4:1` (`128×32`, `256×64`)** hoặc **`16:1` (`256×16`)**. Có `27%` dùng kênh Alpha (`DXT3`/`DXT5`) để phát sáng nền trong suốt. |
| **4. `POSTERS, SHOPS, TRANSIT & VENDING` (Áp phích, Cửa hàng, Trạm buýt, Máy bán nước)** | `8,147` | `33.1 KB` | • `128×128` (`31.1%` — Tranh treo tường, cửa hàng)<br>• `256×256` (`28.1%` — Poster trạm buýt `bustopm`, tạp chí)<br>• `64×64` (`13.1%`)<br>• `256×128` (`5.3%`)<br>• `512×512` (`3.8%`)<br>• `512×256` (`3.3%` — Poster tàu điện ngầm `postersub`) | • **`1:1` Vuông (`79.8%`)**<br>• **`2:1` Ngang (`11.6%`)**<br>• **`1:2` Đứng (`5.3%`)**<br>• `4:1` Ngang dài (`2.1%`) | Lưu ý đặc biệt: Poster nhà chờ xe buýt (`bustopm.txd: CJ_BS_MENU5`) dù ngoài đời là khung đứng nhưng trong GTA SA lại được lưu trong texture vuông **`256×256`** (do UV giãn theo khung chữ nhật đứng)! |
| **5. `MONUMENTS, STATUES & LANDMARKS` (Tượng đài & Kỳ quan)** | `545` | `24.9 KB` | • `128×128` (`35.4%` — `missliberty`, `pier69`)<br>• `256×256` (`29.7%` — `sphinx01`, `disney_tex`, `pershingsq`)<br>• `64×64` (`17.2%`)<br>• `512×256` (`1.3%` — `disney_tex`) | • **`1:1` Vuông (`86.4%`)**<br>• `2:1` Ngang (`6.2%`)<br>• `1:2` Đứng (`5.5%`) | Tượng đài (như `Miss Liberty`, `Sphinx`, `Carter Statue`) chủ yếu dùng các tấm texture bề mặt đá/đồng/phù điêu kích thước nhỏ gọn **`128×128` và `256×256` (`DXT1`)**. |

---

### 5.3. Phân Bố Định Dạng Nén (`Compression Format`), `Mipmaps` & Các Điểm Bất Thường (`Anomalies`) Đang Tồn Tại Trong Game

1. **Định dạng nén trên toàn bộ `101,147` rasters**:
   - **`DXT1` (`89.13%` — `90,156` rasters)**: Nén `4 bits/pixel` (tỷ lệ nén `8:1` so với 32-bit), chuẩn vàng cho mọi bề mặt không cần độ trong suốt bán phần (Billboard, Tranh tường kín, Mặt tiền cửa hàng, Poster đóng khung, Tượng đài).
   - **`DXT3` (`4.70%` — `4,755` rasters)** & **`DXT5` (`3.86%` — `3,908` rasters)**: Nén `8 bits/pixel` (tỷ lệ nén `4:1`, nặng gấp đôi `DXT1`), dùng cho các vật thể có nền trong suốt như **Graffiti (`tags_LA*`), Đèn Neon chữ rời, Kính cửa hàng hoặc Lưới rào**.
   - **`RGBA32_UNCOMPRESSED` (`1.97%` — `1,990` rasters chưa nén)**: Nặng gấp **`8 lần` `DXT1`** (`32 bits/pixel`). Đáng chú ý nhất là **2 file lỗi nặng trong `S&S` gốc**:
     - `S&S/Cdimages/carcer/game_cc.img :: apolicest.txd` (**`38.05 MB`** chỉ cho `127` rasters vì `120` rasters để ở dạng `RGBA32_UNCOMPRESSED`!).
     - `S&S/Cdimages/leonida/game_leored.img :: leobill.txd` (**`32.37 MB`** chỉ cho `13` tấm biển quảng cáo vì `11` tấm để ở dạng `RGBA32_UNCOMPRESSED`!).
2. **Tỷ lệ sử dụng Mipmaps**:
   - **`56.75%` (`57,403` rasters)** chỉ có **`1` level (No Mipmaps)**.
   - **`43.25%` (`43,744` rasters)** có **Mipmaps (`levels > 1`, tăng thêm `~33%` dung lượng file đổi lại không bị nhấp nháy `shimmering/aliasing` khi nhìn từ xa)**.
3. **Các Raster Sai Chuẩn Lũy Thừa Của 2 (`Non-Power-Of-Two / Non-POT` — `547` rasters)**:
   - Trong `101,147` rasters, có **`547` rasters (`0.54%`)** có chiều dài/rộng không phải lũy thừa của 2 (`64, 128, 256, 512, 1024`), tập trung chủ yếu ở:
     - `custom/GROUP_A_MODS.IMG :: lashops93_las2.txd` (chứa các ảnh `3000×512`, `1800×512`, `1744×392`, `1400×600`, `700×700`, `300×600`).
     - `S&S/Cdimages/leonida/game_leored.img :: leobill.txd` (`1024×585`, `835×484`, `1024×490`, `915×408`).
     - `S&S/Cdimages/liberty/GAME_LC.img :: billboard.txd` (`460×423`).
   - Trên engine RenderWare DirectX 9 (`gta_pe.exe`), kích thước Non-POT buộc driver GPU phải pad bộ nhớ ngầm hoặc không tạo được chuỗi mipmap chuẩn, gây tốn VRAM và giảm hiệu năng nạp.

---

## 6. Bảng Tiêu Chuẩn Thông Số Kỹ Thuật Khuyến Nghị (Để Mod Wibu World Đạt `0%` Ảnh Hưởng Performance)

Từ toàn bộ số liệu thực nghiệm trên, chúng ta đúc kết được **Bảng Khung Thông Số Chuẩn (Safe Performance Envelope)** cho từng hạng mục khi bắt tay vào thiết kế texture ở giai đoạn sau:

| Hạng mục bề mặt | Tỷ lệ gốc cần giữ (`Aspect Ratio`) | Độ phân giải khuyến nghị (`Width × Height`) | Định dạng nén chuẩn | Dung lượng mục tiêu / 1 Raster | Ghi chú sống còn để không lệch UV hoặc tụt FPS |
|---|---|---|---|---:|---|
| **1. Billboard / Pano Cao Tốc Cỡ Lớn (Cận cảnh)** | **Giữ đúng tỷ lệ của raster gốc** (`2:1` hoặc `1:1`) | • Gốc `2:1` $\rightarrow$ **`512 × 256`** *(hoặc tối đa `1024×512` cho đại cảnh)*<br>• Gốc `1:1` $\rightarrow$ **`512 × 512`** | **`DXT1`** *(+ Mipmaps)* | **`64 KB – 170 KB`** | ⚠️ **Tuyệt đối giữ nguyên tỷ lệ khung hình (`2:1` vs `1:1`) của từng tên raster gốc** vì tọa độ UV trên mesh `.DFF` đã khóa cứng; nếu raster gốc là `256×256` (dù hiển thị trên bảng chữ nhật) thì ảnh mới cũng phải là `256×256` hoặc `512×512`! |
| **2. Billboard / Tòa Nhà Ở Tầm Xa (`LOD TXD`)** | Giữ nguyên tỷ lệ gốc (`2:1` hoặc `1:1`) | **`64 × 32`** hoặc **`64 × 64`** *(tối đa `128×64`)* | **`DXT1`** *(1 level)* | **`1 KB – 4 KB`** | Giữ file `*_lod.txd` luôn dưới **`350 KB`** để engine nạp tức thì từ khoảng cách `1,500m`. |
| **3. Tranh Tường Lớn (`Murals`) & Băng Rôn Cao Ốc (`Banners`)** | • Mural: `1:1` / `2:1`<br>• Phướn dọc: `1:4` / `1:2` | • Mural: **`512 × 512`** / **`512 × 256`**<br>• Phướn dọc: **`128 × 512`** / **`256 × 512`** | **`DXT1`** *(hoặc `DXT5` nếu rách viền)* | **`32 KB – 170 KB`** | Không vượt quá `512px` trên các file `.TXD` dùng chung cho cả khu phố. |
| **4. Decal Graffiti / Sticker Đường Phố (`tags_LA*`, `comhilo_tags`)** | `1:1` Vuông | **`256 × 256`** *(gốc là `128×128`)* | **`DXT5`** *(có nền Alpha mượt)* | **`64 KB`** | Cả file `tags_LA*.txd` (2 rasters) chỉ nặng **`~128 KB`**, sắc nét gấp 4 lần gốc mà không ảnh hưởng FPS. |
| **5. Nhà Chờ Xe Buýt (`bustopm`), Sạp Báo (`newstand`), Máy Bán Nước (`vend`)** | • `bustopm`: `1:1` (`256×256`)<br>• `newstand`: `2:1` (`128×64`)<br>• `vend`: `1:1` (`128×128`) | • `bustopm`: **`256 × 256`** hoặc **`512 × 512`**<br>• `newstand`: **`256 × 128`**<br>• `vend`: **`256 × 256`** | **`DXT1`** | **`16 KB – 128 KB`** | Chỉ cần tổng dung lượng mỗi file `.TXD` đạo cụ dưới **`250 KB`** là có thể phủ hàng trăm vị trí khắp bản đồ với chi phí RAM bằng 0. |
| **6. Đèn Neon Ban Đêm (`tobj`) & Hộp Đèn Sòng Bạc** | `1:1`, `2:1` hoặc dải chữ `4:1` / `16:1` | **`256 × 256`**, **`256 × 128`**, **`256 × 64`** | **`DXT1`** *(hộp đèn đặc)* hoặc **`DXT5`** *(chữ phát sáng nền trong)* | **`16 KB – 64 KB`** | Không dùng `RGBA32` không nén cho đèn neon để tránh lỗi ngốn RAM như `apolicest.txd`. |
| **7. Đại Thư Viện `S&S Mega-Atlas` (`30 MB – 92 MB`)** | Giữ nguyên `100%` kích thước `W×H` gốc của từng raster | **`128 × 128`** hoặc **`256 × 256`** *(bằng đúng kích thước raster cũ)* | **`DXT1` / `DXT5`** *(bằng đúng format cũ)* | **Không tăng size file `.TXD`** | Với các file Mega-Atlas (`cotton_s.txd` `69 MB`, `lacwbuilds2.txd` `49 MB`, `upstate.txd` `25 MB`), **không được phóng to độ phân giải của các raster bên trong** để giữ nguyên dung lượng file `.TXD` gốc, tránh vượt ngưỡng `CStreaming`. |
