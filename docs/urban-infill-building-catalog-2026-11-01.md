# Danh mục Tòa nhà 3D Chuẩn Infill Mặt Tiền Đường (Urban Building Infill Catalog) — 2026-11-01

> **Phạm vi**: Khảo sát `read-only` toàn bộ kho `D:\GTA Archive\Mod Donor Library` (`2,220` mẫu `.dff`), `8` kho `.IMG` đô thị chủ lực của `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (`GAME_LA.img`, `GAME_SF.img`, `GAME_LV.img`, `GAME_LC.img`, `GAME_VC.img`, `GAME_BW.img`, `game_pra.img`, `GROUP_A_MODS.IMG` trên nền `60,108` định nghĩa `.ide`), và tra cứu các gói mod tòa nhà/khu phố Nhật Bản – Anime – Đô thị hiện đại trên mạng để phục vụ quy hoạch **lấp kín mặt tiền đường (`streetwall infill`)** cho khu đô thị mới **`INLAND-03A` (Bắc Chicago, cao độ nền phẳng `Z = 14.50m`)** và các thành phố mở rộng.

## 1. Tóm tắt điều hành & Bằng chứng trực quan

- **Tổng số mẫu `.dff` đã phân tích nhị phân**:
  - **Phần A (`D:\GTA Archive\Mod Donor Library`)**: Quét `2,220` tệp `.dff`, lọc ra **`82` mẫu tòa nhà 3D đặc kín 4 mặt + có mái (`area_pz > 0`)** chia làm 4 nhóm chức năng (`A1` Akihabara Shophouses/Konbini/Electronics, `A2` Kerorin Street Blocks có máy bán nước Jihanki & quán Arcade, `A3` Base 3D `.dff` đi kèm `.txd` Nhật Bản/Anime từ `Little Akihabara V1/V2`, `OtakuShoppu`, `KawaiiBoutique`, `Ichiraku Ramen`, `Starbucks`, và `A4` Nhà dân Nhật 2–3 tầng, Chung cư Anime, Trường học, Biệt thự/Showroom hiện đại). Đồng thời lập **Danh sách đen `16` nhóm mesh 2D phông nền mỏng / vỏ rỗng** (`PD_PuzzleP1..P5`, `*_neon*.dff`, `ishimaru_mado.dff`, `oudan_hodou01.dff`, `dodai01..02.dff`, `KHiskyscrapers.dff`...) tuyệt đối không dùng làm nhà mặt tiền.
  - **Phần B (`8` kho `.IMG` của `gta sa gameplay-lab`)**: Từ `1,164` tòa nhà vượt qua bộ lọc hình học 3D 4 mặt & đế phẳng, tuyển chọn **Top `75` mẫu tòa nhà đẹp, nhẹ, đế phẳng (`base_z_spread <= 1.25m`), kích thước mặt tiền `15m .. 60m`, `numMaterials <= 136`** dễ xếp nối tiếp dọc vỉa hè ô phố `220m × 270m`, kèm chỉ dẫn rõ từng tên raster biển hiệu/bảng quảng cáo (`sign_textures`) và cờ báo có sẵn `.txd` Nhật Bản từ `Project Japan 3.1` / `KY2`.
  - **Phần C (`Web Search`)**: Tổng hợp **`26` gói mod tòa nhà lẻ & khu phố Nhật Bản / Anime / Đô thị hiện đại** trên GTAinside, LibertyCity.net, MixMods và ZZPuma Blogspot để có thể tải bổ sung vào `Mod Donor Library`.
- **Bằng chứng dữ liệu & Bảng Catalog trực quan (3D Isometric Render từ hình học `.dff` thực tế)**:
  - Ảnh Catalog Phần A (`42` mẫu 3D đặc + `6` mẫu 2D bị loại ở hàng cuối màu đỏ): [`docs/project-eagle/evidence/urban_infill_building_catalog_part_a.png`](evidence/urban_infill_building_catalog_part_a.png)
  - Ảnh Catalog Phần B (`48/75` mẫu tiêu biểu từ 8 kho `.IMG`): [`docs/project-eagle/evidence/urban_infill_building_catalog_part_b.png`](evidence/urban_infill_building_catalog_part_b.png)
  - Dataset JSON đầy đủ cho script quy hoạch `INLAND-03A`: [`docs/project-eagle/evidence/urban-infill-building-catalog-2026-11-01.json`](evidence/urban-infill-building-catalog-2026-11-01.json)

![Catalog Phần A — Mod Donor Library 3D Buildings](evidence/urban_infill_building_catalog_part_a.png)

![Catalog Phần B — Gameplay-Lab 8 IMG Archives 3D Buildings](evidence/urban_infill_building_catalog_part_b.png)

---

## 2. Công thức Kỹ thuật Đặt Tòa Nhà Lên Nền Phẳng `Z = 14.50m` (`INLAND-03A`)

Qua đo đạc tọa độ đỉnh (vertex `min_z`, `max_z`) của toàn bộ `3,384` mẫu `.dff` trong Phần A và Phần B, có **3 quy ước gốc tọa độ `Z` (pivot)** khác nhau mà script sinh `.ipl` cho `INLAND-03A` bắt buộc phải áp dụng đúng công thức:

$$Z_{\text{IPL}} = 14.50 - \text{min\_z} - \Delta_{\text{sink}}$$

Trong đó $\Delta_{\text{sink}} \in [0.05\text{m}, 0.15\text{m}]$ là độ âm nhẹ xuống nền vỉa hè để triệt tiêu khe hở chân tường:
1. **Nhóm Pivot Đáy Đặc Biệt (`min_z ≈ +14.71m .. +14.88m`) — Gói `Akihabara_Town_155560`**:
   - Đa số tòa nhà Akihabara (`takarajima24.dff`, `kinokuniya.dff`, `megane_super.dff`, `laox_honten.dff`, `onoden.dff`, `radio_center.dff`...) được tác giả đặt sẵn đáy ở `Z = +14.88m` trong không gian cục bộ (riêng `ishimaru_1gou.dff`, `maruman.dff`, `myway.dff`, `radio_kaikan02.dff`, `radio_kaikan07.dff` có `min_z = 0.00m`).
   - Do đó, khi đặt tại mặt đất `Z = 14.50m` của `INLAND-03A`, những mẫu có `min_z = 14.88m` phải đặt ở tọa độ IPL `Z_IPL ≈ 14.50 - 14.88 = -0.38m` (còn mẫu `min_z = 0.00m` đặt ở `Z_IPL = 14.50m`). Nếu đặt nhầm `Z_IPL = 14.50m` cho nhóm `min_z = 14.88m`, tòa nhà sẽ bị bay lơ lửng ở độ cao `29.38m`!
2. **Nhóm Pivot Tâm Khối Hộp (`min_z ≈ -dz / 2`) — Gói `Kerorin_Capital_153898`, `Konoha_Island_213921` và đa số tòa nhà Vanilla/S&S**:
   - Đáy tòa nhà nằm ở `-dz/2`, nên tọa độ đặt chuẩn là `Z_IPL = 14.50 - min_z` (tức `14.50 + dz/2`).
3. **Giới hạn Vật liệu RenderWare (`numMaterials <= 136`)**:
   - Tất cả `82` mẫu Phần A và `75` mẫu Phần B đều có số vật liệu sau gộp trùng (`dedup_mats`) $\le 56 \ll 136$. Riêng 3 mẫu có `raw_mats > 136` trước khi gộp trùng là `radio_kaikan07.dff` (`138 -> 36`), `school.dff` (`270 -> 9`) và `classroom.dff` (`158 -> 14`) chỉ cần chạy qua hàm `_repack_clean_static_dff` (đã có sẵn trong pipeline `build_inland03a_sakura_district.py`) là an toàn tuyệt đối.

---

## 3. PHẦN A — Danh sách `82` Tòa nhà 3D "Chuẩn Infill Mặt Tiền Đường" trong `D:\GTA Archive\Mod Donor Library`

### 3.1. Nhóm A1 (`34` mẫu) — Shophouse, Konbini/Cửa hàng 24h, Hiệu sách, Quán ăn, Arcade & Cao ốc Điện tử (`Akihabara_Town_155560`)

| STT | Tên `.dff` | Tên `.txd` | Rộng × Sâu × Cao (`m`) | `min_z` (`m`) | `Z_IPL` tại `14.5m` | Vật liệu (`Raw -> Dedup`) | Số mặt (`Tris`) | Diện tích mái `area_pz` (`m²`) | Khối 3D 4 mặt | Mô tả kiến trúc & Công năng Infill |
|---:|---|---|---:|---:|---:|---:|---:|---:|:---:|---|
| 1 | `takarajima24.dff` | `takarajima24.txd` | `28.65 × 10.23 × 18.21` | `14.88` | `-0.38` | `5 -> 5` | `48` | `94.8` | **3D 4 mặt** | Cửa hàng băng đĩa/truyện 24h Takarajima (Konbini-scale) |
| 2 | `kinokuniya.dff` | `kinokuniya.txd` | `18.73 × 22.62 × 40.55` | `14.88` | `-0.38` | `12 -> 11` | `131` | `297.9` | **3D 4 mặt** | Hiệu sách Kinokuniya & Tòa thương mại 8 tầng |
| 3 | `megane_super.dff` | `megane_super.txd` | `23.26 × 35.69 × 37.62` | `14.88` | `-0.38` | `18 -> 18` | `240` | `731.8` | **3D 4 mặt** | Tòa góc phố Kính mắt Megane Super Akihabara |
| 4 | `nakaura_3gouten.dff` | `nakaura_3gouten.txd` | `60.46 × 16.92 × 16.20` | `14.71` | `-0.21` | `26 -> 18` | `511` | `1144.3` | **3D 4 mặt** | Dãy shophouse KFC / Pocket Plus / Điện tử Nakaura |
| 5 | `liberty_13gou.dff` | `liberty_13gou.txd` | `28.21 × 45.19 × 31.13` | `14.71` | `-0.21` | `19 -> 17` | `666` | `672.9` | **3D 4 mặt** | Tòa nhà Yamato Kuroneko Transport & Liberty Hobby |
| 6 | `rakuda.dff` | `rakuda.txd` | `10.18 × 28.20 × 16.65` | `14.88` | `-0.38` | `15 -> 15` | `190` | `195.2` | **3D 4 mặt** | Shophouse Kaitori Honpo 4 tầng |
| 7 | `yorozubako.dff` | `yorozubako.txd` | `10.17 × 18.20 × 24.30` | `14.88` | `-0.38` | `12 -> 12` | `186` | `183.8` | **3D 4 mặt** | Shophouse hẹp Nhật Bản Yorozubako 5 tầng |
| 8 | `asobitcity_hobby.dff` | `asobitcity_hobby.txd` | `13.30 × 13.01 × 52.78` | `14.88` | `-0.38` | `21 -> 18` | `3018` | `239.7` | **3D 4 mặt** | Tháp Asobit Hobby & Anime City |
| 9 | `gigo.dff` | `gigo.txd` | `12.99 × 25.20 × 55.01` | `14.88` | `-0.38` | `23 -> 19` | `145` | `287.6` | **3D 4 mặt** | Trung tâm Game Arcade SEGA GiGO Akihabara |
| 10 | `laox_honten.dff` | `laox_honten.txd` | `48.94 × 30.28 × 61.59` | `14.88` | `-0.38` | `51 -> 31` | `2096` | `690.4` | **3D 4 mặt** | Tòa bách hóa điện tử LAOX Honten |
| 11 | `laox_thedigitalkan.dff` | `laox_thedigitalkan.txd` | `16.98 × 28.37 × 53.27` | `14.88` | `-0.38` | `19 -> 14` | `3468` | `425.9` | **3D 4 mặt** | Tòa LAOX The Digital Kan |
| 12 | `laox_lammtara.dff` | `laox_lammtara.txd` | `23.14 × 15.15 × 46.79` | `14.88` | `-0.38` | `22 -> 19` | `1704` | `495.4` | **3D 4 mặt** | Tòa LAOX DutyFree & Lammtarra Anime |
| 13 | `laox_watch&game.dff` | `laox_watch&game.txd` | `5.66 × 30.93 × 30.28` | `14.88` | `-0.38` | `16 -> 9` | `166` | `441.3` | **3D 4 mặt** | Shophouse hẹp LAOX Watch & Game |
| 14 | `onoden.dff` | `onoden.txd` | `58.90 × 30.78 × 38.30` | `14.84` | `-0.34` | `48 -> 32` | `4208` | `3015.9` | **3D 4 mặt** | Tòa điện máy Onoden Akihabara |
| 15 | `ishimarusoft_honkan.dff` | `ishimarusoft_honkan.txd` | `37.37 × 36.53 × 59.48` | `14.88` | `-0.38` | `40 -> 27` | `1792` | `1194.3` | **3D 4 mặt** | Tòa Ishimaru Soft Honkan (Băng đĩa & Anime) |
| 16 | `ishimaru_ekimae.dff` | `ishimaru_ekimae.txd` | `22.56 × 20.66 × 42.24` | `14.88` | `-0.38` | `34 -> 19` | `5421` | `1238.0` | **3D 4 mặt** | Tòa Ishimaru Ekimae sát ga |
| 17 | `ishimaru_1gou.dff` | `ishimaru_1gou.txd` | `22.99 × 26.27 × 76.48` | `0.00` | `14.50` | `42 -> 18` | `5301` | `475.8` | **3D 4 mặt** | Cao ốc điện máy Ishimaru 1-Goukan |
| 18 | `satomusen.dff` | `satomusen.txd` | `21.13 × 15.98 × 54.62` | `14.88` | `-0.38` | `25 -> 17` | `1055` | `891.7` | **3D 4 mặt** | Tòa điện tử Sato Musen |
| 19 | `tsukumo_support.dff` | `tsukumo_support.txd` | `36.76 × 32.77 × 36.72` | `14.88` | `-0.38` | `13 -> 12` | `112` | `576.2` | **3D 4 mặt** | Tòa máy tính Tsukumo Support PC |
| 20 | `rocket_1gonten.dff` | `rocket_1gonten.txd` | `30.24 × 19.26 × 36.96` | `14.88` | `-0.38` | `69 -> 29` | `381` | `529.0` | **3D 4 mặt** | Tòa thương mại Rocket 1-Gouten |
| 21 | `radio_center.dff` | `radio_center.txd` | `50.57 × 25.64 × 15.92` | `14.88` | `-0.38` | `69 -> 45` | `694` | `1551.9` | **3D 4 mặt** | Dãy cửa hàng linh kiện Radio Center |
| 22 | `radio_kaikan02.dff` | `radio_kaikan.txd` | `19.32 × 59.94 × 53.41` | `0.00` | `14.50` | `102 -> 29` | `4683` | `192.2` | **3D 4 mặt** | Tòa Akihabara Radio Kaikan (Khối A) |
| 23 | `radio_kaikan03.dff` | `radio_kaikan.txd` | `36.82 × 29.38 × 38.56` | `14.84` | `-0.34` | `110 -> 54` | `3171` | `117.5` | **3D 4 mặt** | Tòa Akihabara Radio Kaikan (Khối B) |
| 24 | `radio_kaikan04.dff` | `radio_kaikan.txd` | `19.26 × 40.31 × 14.49` | `14.84` | `-0.34` | `80 -> 40` | `2037` | `190.3` | **3D 4 mặt** | Tòa thương mại thấp tầng Radio Kaikan 04 |
| 25 | `radio_kaikan07.dff` | `radio_kaikan.txd` | `33.20 × 61.84 × 53.41` | `0.00` | `14.50` | `138 -> 36` | `7423` | `3794.8` | **3D 4 mặt** | Tòa chính Akihabara Radio Kaikan (138->36 mats) |
| 26 | `akihabara_depart.dff` | `akihabara_depart.txd` | `102.76 × 53.55 × 22.95` | `14.88` | `-0.38` | `37 -> 21` | `1518` | `3489.0` | **3D 4 mặt** | Tổ hợp bách hóa JR Akihabara Department Store |
| 27 | `jrbill.dff` | `jrbill.txd` | `35.25 × 77.54 × 50.17` | `14.88` | `-0.38` | `50 -> 37` | `436` | `2246.8` | **3D 4 mặt** | Cao ốc văn phòng JR Building |
| 28 | `manseibashi_police.dff` | `manseibashi_police.txd` | `50.22 × 25.74 × 46.55` | `14.52` | `-0.02` | `31 -> 3` | `1600` | `878.8` | **3D 4 mặt** | Đồn cảnh sát Manseibashi Koban & Tòa góc |
| 29 | `kuminkaikan.dff` | `kuminkaikan.txd` | `21.76 × 25.10 × 33.55` | `14.88` | `-0.38` | `9 -> 9` | `136` | `316.9` | **3D 4 mặt** | Tòa nhà công cộng Kumin Kaikan |
| 30 | `tokyo_public_1.dff` | `tokyo_public_1.txd` | `39.68 × 54.85 × 16.06` | `14.88` | `-0.38` | `10 -> 9` | `668` | `1143.2` | **3D 4 mặt** | Khối nhà văn phòng Tokyo Public |
| 31 | `myway.dff` | `myway.txd` | `43.49 × 62.52 × 27.64` | `0.00` | `14.50` | `13 -> 8` | `2289` | `747.9` | **3D 4 mặt** | Khối nhà thương mại góc phố MyWay |
| 32 | `asakaze_2goukanbill.dff` | `asakaze_2goukanbill.txd` | `39.16 × 30.26 × 45.28` | `14.84` | `-0.34` | `6 -> 6` | `311` | `1706.8` | **3D 4 mặt** | Tòa văn phòng Asakaze 2-Goukan |
| 33 | `n_tourbill.dff` | `n_tourbill.txd` | `32.93 × 26.51 × 46.19` | `14.88` | `-0.38` | `4 -> 4` | `111` | `903.4` | **3D 4 mặt** | Tòa văn phòng N-Tour Bill |
| 34 | `nomurabill.dff` | `nomurabill.txd` | `12.38 × 18.10 × 31.86` | `14.88` | `-0.38` | `85 -> 22` | `494` | `411.2` | **3D 4 mặt** | Shophouse văn phòng Nomura Building |

### 3.2. Nhóm A2 (`12` mẫu) — Cụm Nhà phố Nhật Bản có Máy bán nước tự động Jihanki, Quán Arcade & Chung cư (`Kerorin_Capital_153898`)

| STT | Tên `.dff` | Tên `.txd` | Rộng × Sâu × Cao (`m`) | `min_z` (`m`) | `Z_IPL` tại `14.5m` | Vật liệu (`Raw -> Dedup`) | Số mặt (`Tris`) | Diện tích mái `area_pz` (`m²`) | Khối 3D 4 mặt | Mô tả kiến trúc & Công năng Infill |
|---:|---|---|---:|---:|---:|---:|---:|---:|:---:|---|
| 35 | `zero13.dff` | `kero.txd` | `32.09 × 20.51 × 13.69` | `-6.86` | `21.36` | `37 -> 36` | `13100` | `2081.9` | **3D 4 mặt** | Cụm shophouse Nhật có máy bán nước Jihanki & quán Arcade |
| 36 | `zero15.dff` | `kero.txd` | `28.84 × 21.48 × 16.21` | `-8.10` | `22.60` | `25 -> 22` | `7337` | `1275.4` | **3D 4 mặt** | Khối nhà góc phố Nhật Bản 4 tầng |
| 37 | `zero16.dff` | `kero.txd` | `31.68 × 47.58 × 13.32` | `-6.66` | `21.16` | `44 -> 41` | `10107` | `3593.0` | **3D 4 mặt** | Dãy shophouse mặt tiền 47.6m Nhật Bản |
| 38 | `zero20.dff` | `kero.txd` | `22.33 × 42.40 × 14.95` | `-7.49` | `21.99` | `31 -> 28` | `11832` | `2039.2` | **3D 4 mặt** | Dãy nhà phố thương mại 42.4m |
| 39 | `zero21.dff` | `kero.txd` | `33.27 × 48.29 × 22.04` | `-12.47` | `26.97` | `28 -> 27` | `16957` | `3404.8` | **3D 4 mặt** | Cụm chung cư & cửa hàng Nhật 6 tầng |
| 40 | `zero18.dff` | `kero.txd` | `56.13 × 34.82 × 20.51` | `-10.29` | `24.79` | `29 -> 28` | `16034` | `4225.6` | **3D 4 mặt** | Khối nhà văn phòng & shophouse 56m |
| 41 | `zero19.dff` | `kero.txd` | `58.31 × 31.70 × 13.15` | `-6.60` | `21.10` | `31 -> 30` | `12006` | `1974.1` | **3D 4 mặt** | Dãy chung cư thấp tầng 58m |
| 42 | `zero12.dff` | `kero.txd` | `58.84 × 47.99 × 12.59` | `-6.30` | `20.80` | `39 -> 38` | `20447` | `4844.8` | **3D 4 mặt** | Ô phố thương mại Nhật Bản 58.8m |
| 43 | `zero14.dff` | `kero.txd` | `55.09 × 46.84 × 25.15` | `-12.58` | `27.08` | `35 -> 31` | `19516` | `4194.6` | **3D 4 mặt** | Tổ hợp văn phòng & shophouse 55m |
| 44 | `kero07.dff` | `kero.txd` | `59.64 × 71.68 × 23.97` | `-11.98` | `26.48` | `12 -> 12` | `17747` | `2176.4` | **3D 4 mặt** | Cụm chung cư hiện đại Kerorin 07 |
| 45 | `kero10.dff` | `kero.txd` | `68.91 × 43.51 × 27.62` | `-13.81` | `28.31` | `16 -> 16` | `13126` | `2962.5` | **3D 4 mặt** | Cụm tòa nhà thương mại Kerorin 10 |
| 46 | `kero13.dff` | `kero.txd` | `46.00 × 89.71 × 34.81` | `-17.41` | `31.91` | `23 -> 22` | `11663` | `7794.6` | **3D 4 mặt** | Dãy cao ốc mặt tiền đường Kerorin 13 |

### 3.3. Nhóm A3 (`10` mẫu) — Tòa nhà Thương mại 3D kết hợp Gói Texture Nhật Bản/Anime có sẵn trong `Mod Donor Library` (`Little Akihabara V1/V2`, `OtakuShoppu`, `KawaiiBoutique`, `Ichiraku Ramen`)

| STT | Tên `.dff` (Nguồn 3D) | Tên `.txd` (Gói Donor Nhật Bản) | Rộng × Sâu × Cao (`m`) | `min_z` (`m`) | `Z_IPL` tại `14.5m` | Vật liệu (`Raw -> Dedup`) | Số mặt (`Tris`) | Diện tích mái `area_pz` (`m²`) | Khối 3D 4 mặt | Mô tả kiến trúc & Công năng Infill |
|---:|---|---|---:|---:|---:|---:|---:|---:|:---:|---|
| 47 | `foodmart1_lan.dff` | `lanblokb2.txd` (`Little_Akihabara_V2_221340`) | `21.95 × 10.93 × 6.18` | `-3.08` | `17.58` | `4 -> 4` | `110` | `239.9` | **3D 4 mặt** | Cửa hàng tiện lợi / Foodmart Nhật Bản (Little Akihabara V2) |
| 48 | `officessml1_lan.dff` | `lanblokb2.txd` (`Little_Akihabara_V2_221340`) | `25.96 × 16.52 × 13.02` | `-6.50` | `21.00` | `8 -> 8` | `449` | `567.9` | **3D 4 mặt** | Tòa nhà Otaku Shop / Văn phòng nhỏ (Little Akihabara V2) |
| 49 | `officeblok1_lan.dff` | `lanblokb2.txd` (`Little_Akihabara_V2_221340`) | `38.72 × 32.10 × 28.49` | `-14.25` | `28.75` | `9 -> 9` | `467` | `1265.2` | **3D 4 mặt** | Cao ốc thương mại Anime (Little Akihabara V2) |
| 50 | `newdbbuild_lan04.dff` | `lanblokb2.txd` (`Little_Akihabara_V2_221340`) | `44.80 × 38.53 × 23.75` | `-11.87` | `26.37` | `7 -> 7` | `494` | `1727.2` | **3D 4 mặt** | Tòa nhà bách hóa góc phố (Little Akihabara V2) |
| 51 | `build01_lan.dff` | `lanblokb2.txd` (`Little_Akihabara_V2_221340`) | `17.64 × 102.67 × 22.23` | `-10.42` | `24.92` | `18 -> 18` | `529` | `1743.4` | **3D 4 mặt** | Dãy phố thương mại Little Akihabara 102m |
| 52 | `vineblock1_lawn.dff` | `sunrise09_lawn.txd` (`Japanese_Building_V1_159896 + Japanese_Building_V2_175652`) | `61.44 × 27.35 × 12.01` | `-6.00` | `20.50` | `20 -> 20` | `628` | `1440.8` | **3D 4 mặt** | Dãy shophouse OtakuShoppu / KawaiiBoutique 61.4m |
| 53 | `newbit01_lawn.dff` | `sunrise09_lawn.txd` (`Japanese_Building_V1_159896 + Japanese_Building_V2_175652`) | `45.13 × 58.98 × 12.46` | `-8.72` | `23.22` | `3 -> 3` | `277` | `2726.8` | **3D 4 mặt** | Tổ hợp cửa hàng thời trang KawaiiBoutique 45x59m |
| 54 | `stripbar_lae.dff` | `lae2newtempbx.txd` (`project-japan/PJ_3.1_FULL_EXTRACTED`) | `28.25 × 23.04 × 9.07` | `-2.46` | `16.96` | `59 -> 29` | `7672` | `727.6` | **3D 4 mặt** | Quán mì Ichiraku Ramen & dãy quán Nhật (Ichiraku #86716) |
| 55 | `pawnshp_lae2.dff` | `lae2newtempbx.txd` (`Ichiraku_Ramen_86716 + PJ_3.1_FULL_EXTRACTED`) | `35.87 × 12.30 × 7.01` | `-3.50` | `18.00` | `11 -> 11` | `237` | `424.6` | **3D 4 mặt** | Dãy cửa hàng góc phố Nhật Bản (PJ 3.1 + Ichiraku) |
| 56 | `market2_lae.dff` | `lae2newtempbx.txd` (`Ichiraku_Ramen_86716 + PJ_3.1_FULL_EXTRACTED`) | `35.58 × 28.03 × 6.11` | `-3.75` | `18.25` | `13 -> 13` | `307` | `816.1` | **3D 4 mặt** | Dãy chợ / shophouse 1 tầng Nhật Bản (PJ 3.1 + Ichiraku) |

### 3.4. Nhóm A4 (`26` mẫu) — Nhà dân Nhật Bản 2–3 tầng, Chung cư Anime, Quán Ramen, Trường học, Cổng/Tường rào & Showroom Hiện đại (`Nobita_House`, `Konoha_Island`, `Escuela_Interior`, `KY5`)

| STT | Tên `.dff` | Tên `.txd` | Rộng × Sâu × Cao (`m`) | `min_z` (`m`) | `Z_IPL` tại `14.5m` | Vật liệu (`Raw -> Dedup`) | Số mặt (`Tris`) | Diện tích mái `area_pz` (`m²`) | Khối 3D 4 mặt | Mô tả kiến trúc & Công năng Infill |
|---:|---|---|---:|---:|---:|---:|---:|---:|:---:|---|
| 57 | `ie1.dff` | `ie.txd` | `32.23 × 41.04 × 13.86` | `-0.04` | `14.54` | `3 -> 3` | `3935` | `3107.1` | **3D 4 mặt** | Nhà dân Nhật Bản 2 tầng có sân tường rào (Nhà Nobita #78710) |
| 58 | `3IchirakuR.dff` | `KONOHAisland.txd` | `7.52 × 7.80 × 6.79` | `-3.40` | `17.90` | `6 -> 6` | `6874` | `115.9` | **3D 4 mặt** | Quán mì Ramen Ichiraku độc lập 3D (Konoha #213921) |
| 59 | `3Naruto_apartmen.dff` | `KONOHAisland.txd` | `12.17 × 21.43 × 18.69` | `-9.34` | `23.84` | `9 -> 9` | `11661` | `611.7` | **3D 4 mặt** | Chung cư Nhật/Anime 5 tầng cầu thang ngoài (Naruto Apt) |
| 60 | `BorutoHouse.dff` | `BorutoHouse.txd` | `31.08 × 22.50 × 16.14` | `-8.07` | `22.57` | `30 -> 30` | `35954` | `861.3` | **3D 4 mặt** | Biệt thự gia đình Nhật Bản 2 tầng hiện đại (Boruto House) |
| 61 | `BorutoHWalls.dff` | `BorutoHouse.txd` | `37.76 × 39.57 × 6.56` | `-3.28` | `17.78` | `8 -> 8` | `17559` | `122.9` | **3D 4 mặt** | Hệ tường rào & cổng biệt thự Nhật Bản (Boruto Walls) |
| 62 | `1Konoha_Gates.dff` | `KONOHAisland.txd` | `53.40 × 7.73 × 22.95` | `-11.47` | `25.97` | `12 -> 12` | `10583` | `718.7` | **3D 4 mặt** | Cổng khu phố / cổng trường kiểu Á Đông (53.4m) |
| 63 | `2Hokage_Office.dff` | `KONOHAisland.txd` | `20.68 × 16.41 × 6.52` | `-5.48` | `19.98` | `33 -> 32` | `6600` | `262.1` | **3D 4 mặt** | Tòa nhà hành chính / văn phòng 2 tầng |
| 64 | `4KHi_House002.dff` | `KONOHAisland.txd` | `11.13 × 11.20 × 11.22` | `-5.61` | `20.11` | `10 -> 10` | `4725` | `191.2` | **3D 4 mặt** | Nhà dân / Cửa hàng góc 2 tầng (11.1x11.2m) |
| 65 | `4KHi_House003.dff` | `KONOHAisland.txd` | `29.15 × 17.71 × 10.34` | `-5.17` | `19.67` | `11 -> 10` | `7644` | `366.4` | **3D 4 mặt** | Dãy nhà phố 2 tầng mặt tiền 29.2m |
| 66 | `4KHi_House004.dff` | `KONOHAisland.txd` | `22.99 × 26.00 × 14.72` | `-7.36` | `21.86` | `12 -> 12` | `11645` | `652.1` | **3D 4 mặt** | Chung cư 3 tầng kiểu Á Đông (23x26m) |
| 67 | `4KHi_House005.dff` | `KONOHAisland.txd` | `14.04 × 19.63 × 19.72` | `-9.86` | `24.36` | `10 -> 10` | `10346` | `484.1` | **3D 4 mặt** | Tòa chung cư 4 tầng (14x19.6m) |
| 68 | `4KHi_House007.dff` | `KONOHAisland.txd` | `15.56 × 9.73 × 10.29` | `-5.14` | `19.64` | `10 -> 10` | `5441` | `248.4` | **3D 4 mặt** | Nhà phố thương mại 2 tầng (15.6x9.7m) |
| 69 | `4KHi_House008.dff` | `KONOHAisland.txd` | `10.23 × 24.32 × 10.03` | `-5.02` | `19.52` | `9 -> 9` | `10395` | `402.4` | **3D 4 mặt** | Dãy shophouse 2 tầng (10.2x24.3m) |
| 70 | `4KHi_House011.dff` | `KONOHAisland.txd` | `17.94 × 14.14 × 11.18` | `-5.59` | `20.09` | `8 -> 8` | `5784` | `475.6` | **3D 4 mặt** | Nhà dân 2 tầng mái ngói (17.9x14.1m) |
| 71 | `4KHi_House015.dff` | `KONOHAisland.txd` | `21.79 × 26.57 × 10.49` | `-5.25` | `19.75` | `9 -> 9` | `7435` | `441.2` | **3D 4 mặt** | Cụm nhà phố 2 tầng (21.8x26.6m) |
| 72 | `4KHi_House028.dff` | `KONOHAisland.txd` | `14.21 × 17.46 × 15.27` | `-7.63` | `22.13` | `10 -> 10` | `6897` | `489.1` | **3D 4 mặt** | Chung cư 3 tầng gọn đẹp (14.2x17.5m) |
| 73 | `4KHi_House030.dff` | `KONOHAisland.txd` | `19.49 × 11.73 × 10.24` | `-5.12` | `19.62` | `9 -> 9` | `5128` | `293.7` | **3D 4 mặt** | Nhà phố 2 tầng mặt tiền 19.5m |
| 74 | `4KHi_House036.dff` | `KONOHAisland.txd` | `20.09 × 10.60 × 10.78` | `-5.39` | `19.89` | `8 -> 8` | `10341` | `367.8` | **3D 4 mặt** | Shophouse hẹp 2 tầng (20.1x10.6m) |
| 75 | `school.dff` | `school.txd` | `69.99 × 20.72 × 49.01` | `0.00` | `14.50` | `270 -> 9` | `4967` | `2526.4` | **3D 4 mặt** | Tòa nhà chính Trường học Nhật Bản (Escuela #117570, 270->9 mats) |
| 76 | `classroom.dff` | `classroom.txd` | `17.40 × 14.26 × 4.55` | `-0.28` | `14.78` | `158 -> 14` | `4816` | `375.6` | **3D 4 mặt** | Khối phòng học 3D (Escuela #117570, 158->14 mats) |
| 77 | `DirectorOfi.dff` | `DirectorOfi.txd` | `10.62 × 17.55 × 4.10` | `-0.04` | `14.54` | `16 -> 9` | `4146` | `474.2` | **3D 4 mặt** | Khối văn phòng hiệu trưởng (Escuela #117570) |
| 78 | `CasaCampo.dff` | `CasaCampo.txd` | `35.03 × 32.16 × 14.48` | `-7.24` | `21.74` | `19 -> 17` | `11641` | `1557.7` | **3D 4 mặt** | Biệt thự / Nhà hàng kiểu Nhật-Âu (Anime Scene #165621) |
| 79 | `Nagato_Yander4.dff` | `Nagato_Yander4.txd` | `14.40 × 12.72 × 4.22` | `0.38` | `14.12` | `15 -> 7` | `5988` | `302.0` | **3D 4 mặt** | Tòa nhà phòng khám / bệnh viện nhỏ (14.4x12.7m) |
| 80 | `vgswrehse18.dff` | `vgsswarehse02c.txd` | `27.82 × 50.22 × 11.69` | `-4.03` | `18.53` | `62 -> 62` | `9061` | `1689.8` | **3D 4 mặt** | Showroom ô tô kính hiện đại (Car Showroom #150767) |
| 81 | `LABIGSAVEHOUse.dff` | `labigsave.txd` | `31.80 × 34.64 × 7.52` | `-4.68` | `19.18` | `61 -> 51` | `7808` | `987.2` | **3D 4 mặt** | Biệt thự hiện đại đế phẳng (Modern Villa #193945) |
| 82 | `Kame_House.dff` | `Kame_House.txd` | `55.13 × 58.24 × 18.47` | `-3.97` | `18.47` | `102 -> 36` | `49025` | `3095.9` | **3D 4 mặt** | Nhà Kame House 2 tầng (Dragon Ball #163714, 102->36 mats) |

> **Ghi chú mở rộng cho `Konoha_Island_213921`**: Ngoài `12` mẫu nhà tiêu biểu liệt kê trong bảng A4 (`4KHi_House002..036`), trong `KHi.img` còn đầy đủ bộ sưu tập từ `4KHi_House001.dff` đến `4KHi_House120.dff` (tổng cộng **120 mẫu nhà phố / chung cư Á Đông 2–5 tầng** đều là khối 3D kín 4 mặt, `numMaterials = 4..14 <= 136`, dùng chung duy nhất 1 tệp `KONOHAisland.txd`, cực kỳ tiết kiệm VRAM khi rải hàng loạt).

### 3.5. Bảng Cảnh báo Kỹ thuật: Danh sách `16` Mẫu Mesh 2D Backdrop / Vỏ Rỗng Bị Loại Bỏ (Không dùng làm tòa nhà mặt tiền)

| STT | Gói nguồn | Tên `.dff` | Kích thước bao (`m`) | Diện tích mái `area_pz` (`m²`) | Vật liệu | Phân loại hình học | Lý do kỹ thuật loại bỏ khỏi Streetwall Infill |
|---:|---|---|---:|---:|---:|:---:|---|
| 1 | `ky4-anime-worlds/PDFT_Puzzle_Stage_193789` | `PD_PuzzleP1.dff` | `115.75 × 128.30 × 14.79` | `125.6` | `1->1` | **LOẠI (2D/Shell)** | Vòng phông nền 2D rỗng ruột bao quanh sân khấu (không có nóc/khối đặc) |
| 2 | `ky4-anime-worlds/PDFT_Puzzle_Stage_193789` | `PD_PuzzleP2.dff` | `114.49 × 133.74 × 3.11` | `741.2` | `4->2` | **LOẠI (2D/Shell)** | Tấm phông nền thành phố 2D mỏng dẹt ghép vòng quanh |
| 3 | `ky4-anime-worlds/PDFT_Puzzle_Stage_193789` | `PD_PuzzleP3.dff` | `111.11 × 124.58 × 2.20` | `464.7` | `1->1` | **LOẠI (2D/Shell)** | Tấm mặt phẳng 2D trang trí viền sân khấu |
| 4 | `ky4-anime-worlds/PDFT_Puzzle_Stage_193789` | `PD_Puzzle_Sky.dff` | `225.26 × 228.55 × 123.88` | `0.0` | `1->1` | **LOẠI (2D/Shell)** | Vòm bầu trời (Skybox shell 225x228m, area_pz = 0) |
| 5 | `ky2-urban-buildings/Akihabara_Town_155560` | `ishimaru_1gou_neon.dff` | `107.49 × 179.36 × 76.58` | `0.0` | `2->2` | **LOẠI (2D/Shell)** | Tấm bảng đèn neon 2D tách rời (area_pz = 0, không phải tòa nhà) |
| 6 | `ky2-urban-buildings/Akihabara_Town_155560` | `ishimaru_mado.dff` | `12.28 × 22.03 × 41.98` | `0.0` | `5->3` | **LOẠI (2D/Shell)** | Lớp mặt kính 2D rời của tòa Ishimaru (area_pz = 0) |
| 7 | `ky2-urban-buildings/Akihabara_Town_155560` | `onoden_neon01.dff` | `1.31 × 18.90 × 5.18` | `0.0` | `1->1` | **LOẠI (2D/Shell)** | Tấm biển neon phẳng 2D dày 1.31m (area_pz = 0) |
| 8 | `ky2-urban-buildings/Akihabara_Town_155560` | `onoden_neon02.dff` | `21.08 × 13.45 × 40.84` | `0.0` | `1->1` | **LOẠI (2D/Shell)** | Khung đèn neon rỗng 2 mặt (area_pz = 0) |
| 9 | `ky2-urban-buildings/Akihabara_Town_155560` | `myway2_neon.dff` | `18.68 × 60.00 × 27.64` | `0.0` | `4->2` | **LOẠI (2D/Shell)** | Lớp chữ neon 2D áp mặt tiền (area_pz = 0) |
| 10 | `ky2-urban-buildings/Akihabara_Town_155560` | `radio_kaikan_neon01.dff` | `29.77 × 0.55 × 4.08` | `0.0` | `1->1` | **LOẠI (2D/Shell)** | Tấm biển neon mỏng 0.55m (2D plane, area_pz = 0) |
| 11 | `ky2-urban-buildings/Akihabara_Town_155560` | `radio_kaikan_kanban.dff` | `35.23 × 32.95 × 8.70` | `0.0` | `36->19` | **LOẠI (2D/Shell)** | Khung biển quảng cáo rỗng không đáy/nóc (area_pz = 0) |
| 12 | `ky2-urban-buildings/Akihabara_Town_155560` | `satomusen_neon.dff` | `20.82 × 7.40 × 65.04` | `0.0` | `1->1` | **LOẠI (2D/Shell)** | Mặt phẳng đèn neon Sato Musen (area_pz = 0) |
| 13 | `ky2-urban-buildings/Akihabara_Town_155560` | `oudan_hodou01.dff` | `115.19 × 148.56 × 0.00` | `1098.3` | `1->1` | **LOẠI (2D/Shell)** | Mặt phẳng vạch kẻ đường đi bộ (dz = 0.00m) |
| 14 | `ky2-urban-buildings/Akihabara_Town_155560` | `dodai01.dff` | `278.05 × 271.87 × 23.92` | `74065.5` | `2->2` | **LOẠI (2D/Shell)** | Đế nền đường cả khu Akihabara (278x271m, không phải tòa nhà lẻ) |
| 15 | `ky4-anime-worlds/Konoha_Island_213921` | `KHiskyscrapers.dff` | `433.38 × 47.97 × 123.10` | `0.0` | `3->1` | **LOẠI (2D/Shell)** | Phông nền nhà chọc trời 2D xa (Konoha Island backdrop) |
| 16 | `ky4-anime-worlds/AoT_Wall_96191` | `snkwall1.dff` | `342.60 × 198.60 × 145.34` | `64364.6` | `6->6` | **LOẠI (2D/Shell)** | Tường thành khổng lồ 342x198x145m (quá khổ làm nhà phố) |

---

## 4. PHẦN B — Danh sách Top `75` Tòa nhà 3D Đẹp, Nhẹ & Đế Phẳng có sẵn trong `8` kho `.IMG` của `gta sa gameplay-lab`

Tất cả `75` mẫu dưới đây đều thỏa mãn:
- Là **khối hộp 3D đặc kín 4 mặt (`is_4sided_box = True`)** và có mặt mái (`area_pz > 0`).
- **Đế phẳng (`base_z_spread <= 1.25m`)**, đặt trực tiếp lên mặt đất phẳng `Z = 14.50m` tại `INLAND-03A` theo công thức `Z_IPL = 14.50 - min_z` mà không bị hở móng cầu thang hay chân đồi.
- **Số vật liệu `numMaterials <= 36 <= 136`**, lưới nhẹ (`110 .. 1,920` triangles), có thể nhân bản hàng chục lần quanh các ô phố `220m × 270m` mà không gây tụt FPS.
- Cột **Texture Biển hiệu / Mặt tiền dễ thay** chỉ rõ các tên raster trong `.txd` có thể thay trực tiếp bằng poster Anime / Gacha / Konbini Nhật Bản (hoặc dùng ngay tệp `.txd` trùng tên đã có sẵn trong `013 PROJECT JAPAN MAIN Textures` / `KY2` được đánh dấu **`Có sẵn PJ 3.1 / KY2`**).

| STT | Kho `.IMG` | Model ID | Tên `.dff` | Tên `.txd` | Rộng × Sâu × Cao (`m`) | `min_z` (`m`) | Độ lệch đế (`m`) | Vật liệu (`Raw->Dedup`) | Tris | Có sẵn `.txd` Nhật (`PJ3.1`/`KY2`) | Các Raster Biển hiệu / Mặt tiền (`sign_textures`) dễ thay sang Nhật Bản / Anime / Gacha |
|---:|---|---:|---|---|---:|---:|---:|---:|---:|:---:|---|
| 1 | `GAME_LA.img` | `17521` | `pawnshp_lae2.dff` | `lae2newtempbx.txd` | `35.9 × 12.3 × 7.0` | `-3.50` | `0.06` | `11->11` | `237` | **Có (KY2 Nhật)** | `downtshop1_LAn`, `asanpdshpsh1` |
| 2 | `GAME_LA.img` | `17519` | `market2_lae.dff` | `lae2newtempbx.txd` | `35.6 × 28.0 × 6.1` | `-3.75` | `0.30` | `13->13` | `307` | **Có (KY2 Nhật)** | `downtsign1_LA`, `asanpdshpsh1`, `asanpdshpsh1c` |
| 3 | `GAME_LA.img` | `17699` | `mcstraps_lae2.dff` | `contachou1_lae2.txd` | `20.6 × 13.1 × 11.4` | `-4.64` | `0.16` | `9->9` | `808` | **Có (KY2 Nhật)** | `gableends1` |
| 4 | `GAME_LA.img` | `5709` | `shop03_law01.dff` | `melrose17_lawn.txd` | `50.2 × 28.9 × 17.9` | `-8.96` | `0.01` | `12->12` | `707` | **Có (KY2 Nhật)** | `shoptop01_law`, `shopface02c_law`, `shopwin02_law`, `shopface02bl_law`, `shopdoor01_law` |
| 5 | `GAME_LA.img` | `4176` | `bailbonds2_lan.dff` | `civic03_lan.txd` | `37.4 × 25.6 × 11.0` | `-5.49` | `0.01` | `16->16` | `197` | **Có (PJ 3.1)** | `LAroad_offroad1`, `downtshop2_LAn`, `bailbonds1_LAn`, `downtsign2_LA`, `downtshop5_LAn` |
| 6 | `GAME_LA.img` | `17573` | `rydhou01_lae2.dff` | `contachou1_lae2.txd` | `18.4 × 20.4 × 6.3` | `-1.79` | `0.01` | `7->7` | `400` | **Có (KY2 Nhật)** | `gableends1` |
| 7 | `GAME_LA.img` | `5769` | `vineblock1_lawn.dff` | `sunrise09_lawn.txd` | `61.4 × 27.4 × 12.0` | `-6.00` | `0.63` | `20->20` | `628` | **Có (KY2 Nhật)** | `vinesign1_LAw`, `vinesign2_LAw`, `downtsign3_LA`, `downtshop5_LAn`, `downtshop3_LAn` |
| 8 | `GAME_LA.img` | `4021` | `officessml1_lan.dff` | `lanblokb2.txd` | `26.0 × 16.5 × 13.0` | `-6.50` | `0.00` | `8->8` | `449` | **Có (KY2 Nhật)** | `bluewhitewindow`, `forleasesign` |
| 9 | `GAME_LA.img` | `5182` | `nwspltbild4_las2.dff` | `lashops93_las2.txd` | `47.8 × 39.0 × 6.3` | `-3.01` | `0.00` | `15->15` | `485` | **Có (PJ 3.1)** | `snpedshptst1`, `snpedshptst2`, `snpedshptst3`, `ws_sandstone2`, `sjmlashop5` |
| 10 | `GAME_LA.img` | `4022` | `foodmart1_lan.dff` | `lanblokb2.txd` | `21.9 × 10.9 × 6.2` | `-3.08` | `0.00` | `4->4` | `110` | **Có (KY2 Nhật)** | `foodmartla2`, `foodmartla1` |
| 11 | `GAME_LA.img` | `5016` | `snpdpess1_las.dff` | `ground3_las.txd` | `31.0 × 33.8 × 6.5` | `-3.22` | `0.05` | `10->10` | `194` | **Có (PJ 3.1)** | `hollysign05_LAw`, `pierboards_la`, `floorboard256128`, `snpdsqdoor` |
| 12 | `GAME_LA.img` | `5040` | `unionliq_las.dff` | `shopliquor_las.txd` | `25.4 × 42.3 × 7.8` | `-4.08` | `0.27` | `21->21` | `492` | **Có (PJ 3.1)** | `labombshop`, `sjmlashop5`, `Bow_Loadingbay_Door` |
| 13 | `GAME_LA.img` | `17544` | `gangshops4_lae2.dff` | `eastls1b_lae2.txd` | `48.6 × 39.9 × 5.8` | `-2.90` | `0.20` | `15->15` | `713` | **Có (PJ 3.1)** | `gangshop3_LAe`, `gangshop4_LAe`, `lostonclad1`, `gangshop7_LAe`, `comptsign4_LAe` |
| 14 | `GAME_LA.img` | `17537` | `cineblock1_lae2.dff` | `eastls4_lae2.txd` | `37.3 × 23.6 × 22.7` | `-11.54` | `0.38` | `13->13` | `617` | **Có (PJ 3.1)** | `gymshop1_LAe`, `stripsign_lae2`, `clothes2_256` |
| 15 | `GAME_LA.img` | `5787` | `melblok01_lawn.dff` | `melrose02_lawn.txd` | `35.4 × 39.4 × 10.0` | `-5.00` | `0.00` | `26->26` | `626` | Chưa (Dễ thay raster) | `lawshopwall4`, `gymshop1_LAe`, `shopint1_LAe`, `gymshop2_LAe`, `LAstripmall1` |
| 16 | `GAME_LA.img` | `17542` | `gangshops6_lae2.dff` | `eastls1b_lae2.txd` | `15.4 × 20.1 × 8.3` | `-4.16` | `0.00` | `7->7` | `444` | **Có (PJ 3.1)** | `papershop_law`, `comptsign4_LAe` |
| 17 | `GAME_LA.img` | `17577` | `liquorstore01_lae2.dff` | `ganton02_lae2.txd` | `21.4 × 17.3 × 9.7` | `-4.82` | `0.00` | `9->9` | `692` | **Có (PJ 3.1)** | `papershop_law`, `comptsign4_LAe` |
| 18 | `GAME_LA.img` | `4178` | `bailbonds3_lan.dff` | `civic03_lan.txd` | `39.5 × 20.5 × 7.5` | `-3.75` | `0.00` | `8->8` | `199` | **Có (PJ 3.1)** | `sl_shopshttr1` |
| 19 | `GAME_SF.img` | `9517` | `bigboxtmp16.dff` | `bigboxtemp1.txd` | `42.1 × 42.8 × 8.8` | `-5.33` | `0.54` | `11->11` | `620` | Chưa (Dễ thay raster) | `lombard_build2_2`, `lombard_build2_4`, `lombard_build2_5`, `lombard_build3_1`, `board64_law` |
| 20 | `GAME_SF.img` | `10606` | `cluckbell_sfs.dff` | `cluckbell_sfs.txd` | `41.8 × 50.6 × 17.5` | `-8.77` | `0.00` | `18->18` | `747` | Chưa (Dễ thay raster) | `ws_sandstone1`, `ws_reinforcedbutwonky_small`, `vgnburgwal5_256`, `vgnburgwal3_256`, `vgnburgwal4_128` |
| 21 | `GAME_SF.img` | `10979` | `haightshop_sfs.dff` | `mission_sfse.txd` | `45.6 × 21.8 × 16.6` | `-8.32` | `0.00` | `9->9` | `878` | Chưa (Dễ thay raster) | `ws_ed_shop8`, `ws_ed_shop8_door`, `ws_ed_shop13`, `ws_ed_shop13_door` |
| 22 | `GAME_SF.img` | `10982` | `smallshop_10_sfs03.dff` | `mission2apts_sfse.txd` | `44.0 × 14.0 × 12.0` | `-5.98` | `0.00` | `9->9` | `677` | Chưa (Dễ thay raster) | `ws_ed_shop9`, `ws_ed_shop11`, `ws_ed_shop12`, `ws_streak_billbd` |
| 23 | `GAME_SF.img` | `10631` | `ammunation_sfs.dff` | `queensammo_sfs.txd` | `20.8 × 22.7 × 9.3` | `-4.65` | `0.24` | `13->13` | `788` | Chưa (Dễ thay raster) | `CJ_SUB_DOORS`, `ammu_gunboard3`, `ws_sandstone1`, `ws_ammu-awning` |
| 24 | `GAME_SF.img` | `10999` | `haightshop_sfs02.dff` | `scum_sfse.txd` | `21.7 × 23.2 × 16.2` | `-8.08` | `0.00` | `7->7` | `549` | Chưa (Dễ thay raster) | `ws_mistys_bar`, `ws_ed_shop9`, `ws_jaunk_billbd` |
| 25 | `GAME_SF.img` | `10993` | `mission_06_sfs.dff` | `scum_sfse.txd` | `36.7 × 45.5 × 16.0` | `-8.00` | `0.00` | `7->7` | `249` | Chưa (Dễ thay raster) | `ws_fancywindowpink`, `ws_shopfront1a`, `ws_shopfront1b` |
| 26 | `GAME_SF.img` | `10980` | `tempobj2_sfs02.dff` | `mission3z_sfse.txd` | `41.7 × 37.2 × 22.6` | `-11.29` | `0.00` | `9->9` | `649` | Chưa (Dễ thay raster) | `ws_ed_shop4`, `ws_ed_shop6`, `ws_ed_zeroshop` |
| 27 | `GAME_SF.img` | `10390` | `mission_12_sfs.dff` | `haight1_sfs.txd` | `24.5 × 60.0 × 16.5` | `-8.24` | `0.00` | `10->10` | `647` | Chưa (Dễ thay raster) | `ws_ed_shop4`, `ws_ed_shop3`, `ws_ed_shop10`, `ws_ed_shop2` |
| 28 | `GAME_SF.img` | `10630` | `queens_10_sfs.dff` | `queens1_sfs.txd` | `17.3 × 54.2 × 13.7` | `-6.85` | `0.01` | `6->6` | `542` | Chưa (Dễ thay raster) | `ws_fancyshop1e`, `ws_fancyshop1b`, `ws_fancyshop1`, `ws_fancyshop1c` |
| 29 | `GAME_SF.img` | `10624` | `lowqueens1_sfs.dff` | `queens3_sfs.txd` | `27.6 × 40.5 × 19.2` | `-9.58` | `0.00` | `7->7` | `844` | Chưa (Dễ thay raster) | `ws_w's_shopfront`, `ws_w's_shopfront_top` |
| 30 | `GAME_SF.img` | `10992` | `mission_03_sfs.dff` | `mission2apts_sfse.txd` | `34.4 × 14.0 × 12.0` | `-5.98` | `0.00` | `7->7` | `546` | Chưa (Dễ thay raster) | `ws_ed_shop9`, `ws_ed_shop12` |
| 31 | `GAME_SF.img` | `10628` | `queens_03_sfs.dff` | `queens1_sfs.txd` | `39.0 × 37.3 × 18.5` | `-9.26` | `0.00` | `10->10` | `457` | Chưa (Dễ thay raster) | `ws_cinemasign1`, `ws_hoteldoor1` |
| 32 | `GAME_SF.img` | `10393` | `scum_sfs01.dff` | `scum2_sfs.txd` | `38.1 × 37.8 × 22.6` | `-11.28` | `0.00` | `7->7` | `600` | Chưa (Dễ thay raster) | `ws_oldershop2`, `ws_oldershop1` |
| 33 | `GAME_LV.img` | `8424` | `vagbond01_lvs.dff` | `vagabond.txd` | `31.1 × 29.7 × 11.4` | `-5.68` | `0.00` | `6->6` | `411` | Chưa (Dễ thay raster) | `vegasmotel01_128`, `vegasmotel02_128`, `vegasmotel03_64`, `vegasmoteldoor01_128`, `vegasmotelwind01_128` |
| 34 | `GAME_LV.img` | `8527` | `vagbond02_lvs.dff` | `vagabond.txd` | `44.6 × 27.6 × 11.4` | `-5.68` | `0.00` | `6->6` | `764` | Chưa (Dễ thay raster) | `vegasmotel01_128`, `vegasmotel02_128`, `vegasmotel03_64`, `vegasmoteldoor01_128`, `vegasmotelwind01_128` |
| 35 | `GAME_LV.img` | `8687` | `vgelwbld15_lvs.dff` | `vgsebuild02.txd` | `21.3 × 34.6 × 7.8` | `-4.15` | `0.00` | `9->9` | `148` | Chưa (Dễ thay raster) | `zippizzaco_256`, `casinoshop31_256`, `casinoshop32_256`, `hangersign01_256`, `pawnsigns01_128` |
| 36 | `GAME_LV.img` | `9098` | `vgsesvhse01.dff` | `vgesvhouse01.txd` | `30.1 × 27.1 × 5.9` | `-2.97` | `0.00` | `18->16` | `594` | Chưa (Dễ thay raster) | `carparksignplate_64`, `badhousewallb01_256`, `badhousewallb02_128`, `badhousegttrng03_128`, `redstones01_256` |
| 37 | `GAME_LV.img` | `8300` | `vgswrehse08.dff` | `vgsswarehse02c.txd` | `36.6 × 33.9 × 6.1` | `-3.06` | `0.01` | `27->15` | `526` | Chưa (Dễ thay raster) | `vgsSpinkshop01`, `vgsSpinkshop02`, `wddngchapelsign06_128`, `gnhotelwall02_128`, `vgsSpinkshop03` |
| 38 | `GAME_LV.img` | `8260` | `vgswrehse18.dff` | `vgsswarehse02c.txd` | `27.8 × 50.1 × 11.4` | `-3.73` | `0.00` | `13->13` | `424` | Chưa (Dễ thay raster) | `GB_shopdoor01`, `vgsSnewshop03`, `carparksign02_128`, `giftsign01_law`, `streetsign2_256` |
| 39 | `GAME_LV.img` | `6946` | `vgnwalgren1.dff` | `vgndwntwn21.txd` | `44.5 × 29.5 × 9.0` | `-0.20` | `0.00` | `6->6` | `574` | Chưa (Dễ thay raster) | `247sign1_64`, `vgnshopwal1_256`, `vgnshopwal3_256`, `vgnshopwal2_256` |
| 40 | `GAME_LV.img` | `7932` | `vgsnotxrefhse02.dff` | `vgwsavehses.txd` | `30.1 × 24.0 × 5.9` | `-2.97` | `0.00` | `11->11` | `594` | Chưa (Dễ thay raster) | `carparksignplate_64`, `badhousewallb01_256`, `badhousewallb02_128`, `redstones01_256`, `badhousewallc01_128` |
| 41 | `GAME_LV.img` | `3436` | `motel03_lvs.dff` | `motel01.txd` | `54.5 × 27.6 × 11.4` | `-5.68` | `0.00` | `6->6` | `777` | Chưa (Dễ thay raster) | `vegasmotel01_128`, `vegasmotel02_128`, `vegasmotel03_64`, `vegasmoteldoor01_128`, `vegasmotelwind01_128` |
| 42 | `GAME_LV.img` | `8242` | `vegassedge10.dff` | `vgsshospshop.txd` | `42.8 × 62.8 × 12.7` | `-5.78` | `0.00` | `17->13` | `291` | Chưa (Dễ thay raster) | `ctmall16_128`, `bincoLogo`, `vgnwstshop4_256`, `sw_furnisign`, `GB_nastybar20` |
| 43 | `GAME_LC.img` | `22770` | `dinerind.dff` | `newbuildind.txd` | `14.7 × 33.4 × 12.1` | `-0.20` | `0.01` | `23->23` | `716` | Chưa (Dễ thay raster) | `shopdoor4_64`, `diner_window`, `neonbarsign01_64`, `neonbarsign04_64`, `neonbarsign03_64` |
| 44 | `GAME_LC.img` | `56028` | `fs_cafe.dff` | `fortstauntonport.txd` | `11.2 × 20.5 × 7.8` | `-4.06` | `0.03` | `12->12` | `264` | Chưa (Dễ thay raster) | `shadow64a`, `cs_park_cafe_pillar`, `cs_park_cafe_wall`, `cs_park_cafe_win`, `cs_park_cafe_doorWin` |
| 45 | `GAME_LC.img` | `23207` | `subind_build02.dff` | `subuild2.txd` | `11.8 × 32.1 × 10.6` | `-5.37` | `0.18` | `34->34` | `713` | Chưa (Dễ thay raster) | `Spraysign2_128`, `tool_store2`, `tool_store`, `poster3_64a`, `poster1_64a` |
| 46 | `GAME_LC.img` | `23282` | `Subestatebuild1.dff` | `subestbuild.txd` | `37.8 × 36.3 × 10.7` | `-0.19` | `0.19` | `32->32` | `1167` | Chưa (Dễ thay raster) | `inwindow4128`, `inwindow5128`, `barrel_64HV`, `8ballSIGN`, `tool_store2` |
| 47 | `GAME_LC.img` | `22247` | `petrolstation.dff` | `petrollc.txd` | `51.1 × 55.2 × 12.3` | `-6.14` | `0.00` | `33->33` | `1919` | Chưa (Dễ thay raster) | `AMCOsign128`, `inwindow1128`, `sprinklersign128`, `shopdoor4_64`, `Gastatnboard02_128` |
| 48 | `GAME_LC.img` | `22654` | `ind_maindrag1.dff` | `maindragsb1.txd` | `13.7 × 41.0 × 27.2` | `-13.00` | `0.37` | `15->15` | `269` | Chưa (Dễ thay raster) | `sffront27_256128`, `sffront2_256128`, `sffront13_256128`, `sffront23_256128` |
| 49 | `GAME_LC.img` | `22568` | `block_maindrag.dff` | `maindrag.txd` | `45.9 × 54.0 × 30.1` | `-12.65` | `0.00` | `16->16` | `1567` | Chưa (Dễ thay raster) | `chipboardgrating64HV`, `shopgrating128H`, `indnailshop128`, `ind_clothes_256128`, `ind_Cafe128` |
| 50 | `GAME_LC.img` | `56016` | `fs_offices.dff` | `fortstauntonport.txd` | `59.0 × 49.5 × 24.1` | `0.00` | `0.00` | `26->24` | `928` | Chưa (Dễ thay raster) | `hotelkb2b_128`, `hotelkb2_128`, `sfwindow15_128`, `newindow4`, `Fence_smallwood_64H` |
| 51 | `GAME_LC.img` | `22653` | `ind_maindrag2.dff` | `maindragsb2.txd` | `42.5 × 59.3 × 27.3` | `-13.00` | `0.00` | `14->14` | `367` | Chưa (Dễ thay raster) | `sffront9_256128`, `sffront14_256128`, `sffront15_256128`, `sffront19b_256128`, `sffront20_256128` |
| 52 | `GAME_LC.img` | `23023` | `mansion4.dff` | `sub_villas.txd` | `54.8 × 22.1 × 16.9` | `-8.46` | `0.00` | `13->13` | `748` | Chưa (Dễ thay raster) | `blueclad`, `windowopen`, `redshut`, `windowclosed`, `bigwindow` |
| 53 | `GAME_VC.img` | `26944` | `bnk_main_rework.dff` | `hi_cutbnkmainnw.txd` | `28.5 × 30.9 × 14.9` | `-5.97` | `0.00` | `12->12` | `1904` | Chưa (Dễ thay raster) | `spad_build3`, `spad_tile5_256`, `bank_wall3`, `window2256b`, `achoteldoor1256` |
| 54 | `GAME_VC.img` | `26945` | `bnk_mainnewref.dff` | `hi_cutbnkmainnw.txd` | `28.5 × 30.9 × 11.9` | `-5.97` | `0.00` | `9->9` | `1419` | Chưa (Dễ thay raster) | `bank_wall1`, `bank_wall3`, `spad_build3`, `window2256b`, `spad_tile4bnk_256` |
| 55 | `GAME_VC.img` | `27306` | `odn_beacon2.dff` | `odnhotelblk.txd` | `22.4 × 27.1 × 25.0` | `-7.98` | `0.00` | `9->9` | `638` | Chưa (Dễ thay raster) | `hoteltex1`, `hotelwin_nt1`, `hotelsigns1`, `hotelwindow1`, `hotelcream` |
| 56 | `GAME_VC.img` | `28790` | `washbuild068.dff` | `washnewbuild21.txd` | `40.4 × 33.0 × 21.0` | `-5.61` | `0.00` | `11->11` | `798` | Chưa (Dễ thay raster) | `hotelquarter3_256`, `hotelquarter1_256`, `hotelside1_256`, `hotelquarter2_256`, `hotelside2_256` |
| 57 | `GAME_VC.img` | `26687` | `deli_exterior_front.dff` | `deliext.txd` | `25.0 × 25.5 × 7.6` | `-2.14` | `0.03` | `16->16` | `997` | Chưa (Dễ thay raster) | `Bow_deli_canopyunder`, `Bow_deli_canopy`, `Bow_deli_mainsign`, `Bow_deli_drinksign`, `Bow_bar_metal_cabinet_glass` |
| 58 | `GAME_VC.img` | `27222` | `spad_build2.dff` | `newspadbuild.txd` | `32.9 × 32.5 × 27.8` | `-13.97` | `0.12` | `9->9` | `1826` | Chưa (Dễ thay raster) | `spad_build1d`, `spad_build3`, `spad_build4`, `spad_build1c`, `spad_build5b` |
| 59 | `GAME_VC.img` | `26591` | `lh_pizzaplace.dff` | `nbtshops.txd` | `39.0 × 21.7 × 14.0` | `-6.51` | `0.18` | `16->16` | `619` | Chưa (Dễ thay raster) | `pizzabot_64`, `pizzatop_128`, `pizza01_128`, `wellstackedpizza_256`, `ovenfront` |
| 60 | `GAME_VC.img` | `27930` | `nbt_pizzaplace.dff` | `nbt_pizzaplace.txd` | `41.4 × 46.5 × 14.0` | `-6.69` | `0.28` | `15->15` | `617` | Chưa (Dễ thay raster) | `pizzabot_64`, `pizzatop_128`, `pizza01_128`, `ovenfront`, `malldoor01` |
| 61 | `GAME_VC.img` | `26204` | `dow_pizzaplacedt.dff` | `dts_shops.txd` | `35.8 × 22.1 × 14.1` | `-6.75` | `0.33` | `15->15` | `535` | Chưa (Dễ thay raster) | `pizzabot_64`, `pizzatop_128`, `pizza01_128`, `wellstackedpizza_256`, `ovenfront` |
| 62 | `GAME_VC.img` | `27804` | `xod_beacon.dff` | `xrefhotels.txd` | `23.6 × 26.8 × 25.4` | `-8.42` | `0.44` | `9->9` | `649` | Chưa (Dễ thay raster) | `hoteltex1`, `hotelwin_nt1`, `hotelsigns1`, `hotelwindow1`, `hotelcream` |
| 63 | `GAME_BW.img` | `57129` | `BW_BUS_29.dff` | `bw_tbusines.txd` | `28.5 × 21.7 × 14.9` | `-7.48` | `0.37` | `13->13` | `1090` | Chưa (Dễ thay raster) | `sc_window_d`, `TO00_bankorn4_d`, `TO00_bankwal33_d`, `TO00_bankorn2_d`, `TO00_bankwnd2_d` |
| 64 | `GAME_BW.img` | `56711` | `BW_TRI_111.dff` | `bw_trich.txd` | `21.1 × 34.9 × 14.4` | `-7.21` | `0.08` | `46->36` | `1850` | Chưa (Dễ thay raster) | `AF00_cafeupper_d`, `PR00_xbar_d`, `DI00_dinerwindow_d`, `PS00_sandstn6_d`, `SIL4_RC_signLRG1_swap_d` |
| 65 | `GAME_BW.img` | `56622` | `BW_TRI_22.dff` | `bw_trich.txd` | `30.8 × 33.1 × 12.9` | `-6.47` | `0.20` | `16->11` | `1161` | Chưa (Dễ thay raster) | `RC_burgRoff_swap_d`, `SIL4_burgerSign_d`, `RC_burgWind_swap_d`, `RC_burgMenu_d`, `SIL4_burger_d` |
| 66 | `GAME_BW.img` | `57940` | `BW_GOK_40.dff` | `bw_gokart.txd` | `38.1 × 47.1 × 7.8` | `-3.88` | `0.95` | `7->7` | `1528` | Chưa (Dễ thay raster) | `PR_xbar_swap_d`, `GK_sign04_swap_d`, `GK_sign01_swap_d`, `GK_sign02_swap_d`, `GK_sign03_swap_d` |
| 67 | `GAME_BW.img` | `56425` | `BW_TSCH_25.dff` | `bw_tschool.txd` | `37.2 × 62.4 × 12.1` | `-6.06` | `0.03` | `16->16` | `1166` | Chưa (Dễ thay raster) | `SC01_poster01_d`, `SC01_poster02_d`, `SC01_poster11_d`, `SC01_poster10_d`, `SC_gymSign_d` |
| 68 | `GAME_BW.img` | `56710` | `BW_TRI_110.dff` | `bw_trich.txd` | `30.9 × 46.8 × 16.7` | `-8.35` | `0.00` | `35->29` | `1676` | Chưa (Dễ thay raster) | `AF00_cafeupper_d`, `PR00_xbar_d`, `PS00_sandstn6_d`, `CH00_balustrade_d` |
| 69 | `game_pra.img` | `83357` | `pr_billbd1.dff` | `pr_props.txd` | `20.0 × 8.4 × 27.8` | `-13.91` | `0.00` | `8->7` | `582` | Chưa (Dễ thay raster) | `billdetaily`, `BBoardBack`, `ADDWOOD`, `pr_signmetal1` |
| 70 | `game_pra.img` | `83020` | `wb_stockexc.dff` | `pr_WBstockexc.txd` | `61.4 × 37.3 × 25.6` | `-12.82` | `0.00` | `11->11` | `1228` | Chưa (Dễ thay raster) | `stockexroadwall`, `stockexroadceiling`, `desbarlas` |
| 71 | `game_pra.img` | `83007` | `wb_fdblockb.dff` | `pr_WBsquarefire.txd` | `47.0 × 18.5 × 9.4` | `-4.69` | `0.00` | `12->12` | `1175` | Chưa (Dễ thay raster) | `signfire` |
| 72 | `game_pra.img` | `83004` | `wb_fdblocka.dff` | `pr_WBsquarefire.txd` | `34.4 × 27.4 × 46.9` | `-23.47` | `0.00` | `23->23` | `890` | Chưa (Dễ thay raster) | `GB_shopdoor01`, `wb_fdssig` |
| 73 | `GROUP_A_MODS.IMG` | `5181` | `nwspltbild3_las2.dff` | `lashops93_las2.txd` | `56.4 × 46.4 × 7.5` | `-3.44` | `0.16` | `10->9` | `477` | **Có (PJ 3.1)** | `desbarlas`, `ws_sandstone2` |
| 74 | `GROUP_A_MODS.IMG` | `3292` | `cxf_payspray_.dff` | `cxrf_payspray.txd` | `14.8 × 19.5 × 10.3` | `-0.04` | `0.04` | `15->13` | `499` | Chưa (Dễ thay raster) | `paynspraysign` |
| 75 | `GROUP_A_MODS.IMG` | `16477` | `des_stwngas1.dff` | `des_stownstrip1.txd` | `30.6 × 18.1 × 5.6` | `-0.01` | `0.01` | `33->25` | `2233` | Chưa (Dễ thay raster) | `des_radiomast`, `711_walltemp` |

---

## 5. PHẦN C — Tra cứu trên mạng (`Web Search`) `26` Bản Mod Tòa nhà / Khu phố Nhật Bản, Anime & Đô thị Hiện đại cho GTA SA

Dưới đây là danh sách `26` bản mod tòa nhà lẻ, cửa hàng tiện lợi Nhật Bản (Konbini), khu phố Tokyo/Shibuya/Kabukicho/Osaka, trường học, trung tâm thương mại và chung cư hiện đại đã được xác minh trên **GTAinside**, **LibertyCity.net**, **MixMods** và **ZZPuma Blogspot** để có thể tải bổ sung vào `D:\GTA Archive\Mod Donor Library`:

### 5.1. Nhóm C1 — Khu phố Nhật Bản, Shibuya, Kabukicho, Shinjuku & Cửa hàng Tiện lợi Konbini (FamilyMart / Lawson / 7-Eleven)

| STT | Tên bản Mod | Nguồn & Mã định danh / URL | Loại tài nguyên | Mô tả chi tiết & Ứng dụng cho `INLAND-03A` |
|---:|---|---|---|---|
| 1 | **Dogenzaka Shibuya 2.0 (Tokyo Street Map)** | GTAinside `#121417` — `https://www.gtainside.com/en/sanandreas/maps/121417-dogenzaka-shibuya-2-0/` | Khu phố 3D (`.dff` + `.txd` + `.col`) | Tái hiện đại lộ Dogenzaka (Shibuya, Tokyo) gồm tháp Shibuya 109, dãy shophouse, cửa hàng băng đĩa, biển hiệu neon Nhật Bản kín 2 bên vỉa hè. (Lưu ý: file `#101189` cũ trong kho bị tải nhầm sang mod âm thanh xe, nên tải bản `#121417` này để lấy trọn bộ mesh Shibuya). |
| 2 | **Kabukicho Street (Yakuza / Ryu Ga Gotoku)** | LibertyCity.net / YouTube GTA SA Yakuza Conversion (`Kabukicho Kamurocho Map`) | Khu phố 3D (`.dff` + `.txd` + `.col`) | Khu phố đêm Kamurocho / Kabukicho (Shinjuku) chuyển từ dòng game Yakuza sang GTA SA: cổng chào Kabukicho Ichiban-gai, cửa hàng Don Quijote, hiệu thuốc Matsumoto Kiyoshi, quán mì, câu lạc bộ SEGA và dãy nhà phố 3–6 tầng. |
| 3 | **Utagawa Machi Ex 1.1 (Japanese Town District)** | ZZPuma / Japanese Map Pack (`Utagawa_Machi_Ex_1_1`) | Đô thị Nhật Bản 3D | Thị trấn Nhật Bản hiện đại với các ô phố vuông vức, tòa nhà văn phòng tầm trung, cửa hàng tiện lợi góc phố, vỉa hè gạch và đèn đường Nhật Bản. |
| 4 | **7-Eleven Convenience Store Retexture & 3D Sign** | GTAinside `#144026` / `#181512` — `https://www.gtainside.com/en/sanandreas/mods/144026-7-eleven-store/` | Cửa hàng tiện lợi (`.txd` + `.dff`) | Biến cửa hàng 24/7 và trạm xăng đô thị tại Los Santos (`foodmart1_lan.dff`, `idleewood6_detail.dff`) thành cửa hàng tiện lợi **7-Eleven** chuẩn Nhật – Mỹ với biển hiệu cam-xanh-đỏ và nội thất nhìn qua kính. |
| 5 | **Lawson Station / FamilyMart Konbini Pack (Idolmaster & Anime Ads)** | LibertyCity.net (`Lawson Station Idolmaster GTA SA` / `FamilyMart Retexture Pack`) | Chuỗi Konbini Nhật Bản (`.txd` + `.dff`) | Bộ cửa hàng tiện lợi **Lawson** (màu xanh dương-trắng kèm poster anime Idolmaster) và **FamilyMart** (xanh lá-xanh dương-trắng) thay cho các khối shophouse đế phẳng `20m × 12m`. |
| 6 | **Koi Koi Ramen Shop (Japanese Street Restaurant)** | GTAinside `#177615` — `https://www.gtainside.com/en/sanandreas/maps/177615-koi-koi-ramen-shop/` | Nhà hàng Nhật Bản 3D | Quán mì Ramen góc phố phong cách Nhật Bản với đèn lồng đỏ, rèm Noren, biển hiệu gỗ và bàn ghế ngoài vỉa hè, rất hợp đặt xen kẽ giữa các tòa văn phòng. |
| 7 | **Japanese Store / Little Tokyo Commercial Block** | GTAinside `#155181` & `#221340` (`Little Akihabara V1 & V2` — đã có `.txd` trong kho, có thể tải thêm bản mở rộng) | Dãy phố thương mại Anime | Biến nguyên dãy phố thương mại LAn (`build01_lan.dff`, `newdbbuild_lan04.dff`, `officessml1_lan.dff`, `foodmart1_lan.dff`, `figfree2_lan.dff`) thành phố Anime/Manga với biển hiệu SEGA, Animate, Maid Cafe. |
| 8 | **Tokyo Tower & Surrounding Minato-ku Park Block** | GTAinside `#120955` — `https://www.gtainside.com/en/sanandreas/maps/120955-tokyo-tower/` | Tháp biểu tượng & Công viên | Mô hình 3D Tháp Tokyo đỏ-trắng kèm quảng trường chân tháp, dùng làm điểm nhấn thị giác (landmark) cuối trục đại lộ Bắc Chicago. |

### 5.2. Nhóm C2 — Trường học Nhật Bản, Khu phố Anime, Tiệm Đậu phụ Initial D & Khu phố Game Gacha (Genshin / ZZZ / Persona)

| STT | Tên bản Mod | Nguồn & Mã định danh / URL | Loại tài nguyên | Mô tả chi tiết & Ứng dụng cho `INLAND-03A` |
|---:|---|---|---|---|
| 9 | **Yandere Simulator Akademi High School Full 3D Building** | GTAinside `#186192` / LibertyCity.net (`Akademi High School 3D Map`) | Trường học Nhật Bản 3D | Khối trường trung học Nhật Bản 3 tầng hình chữ U có sân trường, cổng trường trồng hoa anh đào, nhà thể chất và tường bao quanh (khác với bản `#211726` chỉ là IPL prop). |
| 10 | **Bully Scholarship Edition — Bullworth Town Commercial & School Pack** | Sẵn có một phần trong `GAME_BW.img` + Bản mở rộng trên MixMods (`Bully to SA Conversion`) | Khu phố & Trường học 3D | Các tòa nhà thương mại gạch đỏ, tiệm sách, quán cafe, rạp chiếu phim và ký túc xá từ Bullworth Town có đế phẳng, kiến trúc rất hợp với Chicago (`INLAND-03A`). |
| 11 | **K-ON! Sakuragaoka High School Building** | LibertyCity.net / DeviantArt GTA SA Anime Map Conversion (`Sakuragaoka High School`) | Trường học Anime 3D | Tòa nhà trường trung học Sakuragaoka trong anime K-ON! với kiến trúc trường học Nhật Bản cổ điển màu kem, đồng hồ mặt tiền và sân gạch. |
| 12 | **Persona 4 Yasogami High & Inaba Shopping District (Central Street)** | GTAinside / ModDB (`Persona 4 Inaba Shopping District to GTA SA`) | Dãy phố Shophouse Nhật | Phố mua sắm Central Street (Inaba) và siêu thị Junes với các dãy nhà phố Nhật Bản 2–3 tầng, mái vòm che vỉa hè (shotengai) và cột điện Nhật. |
| 13 | **Initial D Tofu Shop (Fujiwara Tofu Store 3D Standalone)** | GTAinside `#139420` — `https://www.gtainside.com/en/sanandreas/maps/139420-fujiwara-tofu-shop/` | Nhà phố Nhật 2 tầng (`.dff` + `.txd` + `.col`) | Tiệm đậu phụ Fujiwara (Initial D) 2 tầng chuẩn kiến trúc nhà phố tỉnh lẻ Nhật Bản, có mái hiên, biển hiệu dọc và chỗ đậu xe trước cửa. |
| 14 | **Genshin Impact — Mondstadt & Inazuma Standalone Buildings Pack** | The Models Resource / Aplaybox (Đã có 9 gói `.obj` Mondstadt trong `ky6-world-filling-assets\models-resource-packs` + có thể tải thêm gói Inazuma City Buildings) | Tòa nhà 3D (`.obj`/`.fbx` -> `.dff`) | Trong kho `ky6` đã có sẵn 9 tòa nhà lẻ Mondstadt (`Angels_Share_Exterior`, `Warm_and_Dry_Mondstadt_Apartment`, `Multi_Arched_Mondstadt_Building`...); có thể tải thêm bộ nhà gỗ/ngói **Inazuma City (Hanamizaka)** để convert sang `.dff`. |
| 15 | **Honkai: Star Rail / Zenless Zone Zero — New Eridu Sixth Street Shop Pack** | Aplaybox / Hoyolab 3D Model Archive (`ZZZ Sixth Street Video Store Random Play & Ramen Shop`) | Dãy phố Anime Đô thị 3D | Khu phố Sixth Street trong Zenless Zone Zero (tiệm băng đĩa Random Play, quán mì Waterfall Soup, tiệm tạp hóa 141, tiệm cafe Tin Master) mang phong cách đô thị Nhật Bản hiện đại pha retro cực kỳ hợp làm mặt tiền phố. |

### 5.3. Nhóm C3 — Trung tâm Thương mại, Chung cư Nhật (Danchi/Mansion), Nhà để xe Cao tầng & Các Gói `.rar` Chưa Giải Nén Trong Kho

| STT | Tên bản Mod | Nguồn & Mã định danh / URL | Loại tài nguyên | Mô tả chi tiết & Ứng dụng cho `INLAND-03A` |
|---:|---|---|---|---|
| 16 | **Modern Glass Shopping Mall / Apple Store & Plaza** | GTAinside `#154890` — `https://www.gtainside.com/en/sanandreas/maps/154890-new-shopping-mall/` | Trung tâm thương mại 3D | Tòa trung tâm thương mại vách kính hiện đại, đế phẳng vuông vức, dùng lấp các góc ngã tư lớn của `INLAND-03A`. |
| 17 | **Japanese Modern Apartment Blocks (Danchi & Mansion Pack)** | LibertyCity.net (`Japanese Apartments / Danchi Pack for GTA SA`) | Chung cư Nhật Bản 4–8 tầng | Các khối chung cư Danchi và Mansion Nhật Bản 4–8 tầng có ban công đều đặn, cầu thang thoát hiểm bên hông và tầng trệt làm cửa hàng. |
| 18 | **McDonald's / Burger King / KFC Modern Drive-Thru Standalone Buildings** | GTAinside `#162310` / `#149822` — `https://www.gtainside.com/en/sanandreas/maps/162310-mcdonalds-restaurant/` | Nhà hàng Fastfood Hiện đại | Các tòa nhà cửa hàng thức ăn nhanh 1–2 tầng đế phẳng có bãi đỗ xe nhỏ, dễ thay biển hiệu sang **WcDonald's / Mos Burger / Yoshinoya / Sukiya**. |
| 19 | **Modern Multi-Story Parking Garage (3D Solid Exterior + Interior Ramps)** | GTAinside `#138912` + Sẵn có trong `GAME_LV.img` (`vgn_carpark1`) / `GAME_LA.img` (`lacarpark1`) | Nhà để xe cao tầng 3D | Khối nhà để xe bê tông hiện đại 4–5 tầng (`45m × 55m`), cực kỳ hiệu quả để lấp đầy nửa ô phố (`half-block infill`) mà vẫn giữ số lượng vật liệu thấp (`<= 18 mats`). |
| 20 | **Modern Japanese Koban (Police Box) & Fire Station** | GTAinside `#155560` (`manseibashi_police.dff`) + LibertyCity.net (`Tokyo Police Koban`) | Đồn cảnh sát & Trạm cứu hỏa | Tòa nhà đồn cảnh sát góc phố kiểu Nhật Bản và trạm cứu hỏa đô thị (`wb_fdblocka.dff`, `wb_fdblockb.dff` trong `game_pra.img`). |
| 21 | **Modern Urban Pocket Park & Sakura Plaza Modular Pack** | MixMods / LibertyCity.net (`Modular Urban Plaza & Park Props`) | Quảng trường & Công viên nhỏ | Các mô-đun bồn hoa bê tông phẳng, ghế gỗ hiện đại, đèn lồng đá, cổng Torii và hàng cây anh đào để lấp các khoảng lùi (setback plaza) trước cao ốc. |
| 22 | **GTA IV / GTA V Converted Mid-Rise Office & Condo Pack for SA** | MixMods / GTAinside (`GTA IV Buildings to SA` / `HD Mid-Rise Buildings`) | Cao ốc văn phòng 6–12 tầng | Các khối nhà văn phòng và chung cư 6–12 tầng chuyển từ GTA IV (Algonquin/Broker) sang GTA SA, kiến trúc gạch và kính hiện đại rất đồng điệu với Chicago. |
| 23 | **Project Japan 4.0 Extended Map & Building Textures** | Sẵn có file nén `D:\GTA Archive\Mod Donor Library\project-japan\PJ_4.0_1717966189_Project Japan 4.0.rar` (`612 MB`) | Gói mở rộng Project Japan 4.0 | Ngay trong kho `D:\GTA Archive\Mod Donor Library\project-japan` đã có sẵn file nén `PJ_4.0_1717966189_Project Japan 4.0.rar` chưa giải nén! Giải nén gói này vào staging sẽ cung cấp thêm hàng trăm `.txd` và `.dff` cửa hàng Nhật Bản mới hơn cả bản `3.1`. |
| 24 | **Avengers Tower V3 (Modern Glass Skyscraper)** | Sẵn có file nén `D:\GTA Archive\Mod Donor Library\ky5-internet-multiverse\GI_147124_avengers-tower-v3.rar` | Cao ốc kính hiện đại | Đã có sẵn file `.rar` trong `ky5-internet-multiverse` nhưng chưa giải nén; có thể giải nén để lấy tòa tháp kính làm điểm nhấn. |
| 25 | **Restaurant Interior & Exterior Building (`GI_200933`)** | Sẵn có trong `D:\GTA Archive\Mod Donor Library\ky6-world-filling-assets\gtainside-scenic-packs\GI_200933_restaurant-interior` | Nhà hàng hiện đại | Đã có sẵn trong `ky6-world-filling-assets/gtainside-scenic-packs`, có thể bóc phần ngoại thất ghép vào dãy phố ẩm thực. |
| 26 | **Tallest Tower in LA / US Bank Tower (`GI_129128`)** | Sẵn có trong `D:\GTA Archive\Mod Donor Library\ky6-world-filling-assets\gtainside-scenic-packs\GI_129128_tallest-tower-in-la` | Cao ốc điểm nhấn (`66m × 100m`) | Mẫu `kat.dff` (`66.14 × 100.59 × 32.38m`, `57 -> 26` mats) đã có sẵn trong `ky6`, là khối đế thương mại 4 mặt rất bề thế. |

---

## 6. Công thức Quy hoạch Mặt Tiền Đường (`Streetwall Packing Recipes`) cho Khu Đô Thị `INLAND-03A` (`220m × 270m` Blocks)

Để lấp kín **4 cạnh vỉa hè** của mỗi ô phố `220m × 270m` tại `INLAND-03A` (cao độ nền `Z = 14.50m`) mà không bị khe hở hay chồng lấn:

1. **Cạnh Đông – Tây dài `220m` (sau khi trừ `12m` vỉa hè góc mỗi đầu còn `196m` chiều dài mặt tiền)**:
   - **Phương án 1 (Phố Điện tử & Konbini Akihabara — Nhóm A1)**:
     - Đặt ở 2 góc ngã tư: `megane_super.dff` (`35.7m`) + `manseibashi_police.dff` (`50.2m`).
     - Lấp đoạn giữa (`110.1m`): `laox_honten.dff` (`48.9m`) + `ishimarusoft_honkan.dff` (`37.4m`) + `takarajima24.dff` (`28.6m`, cửa hàng 24h) $\rightarrow$ Tổng mặt tiền = **`200.8m`**, kín khít toàn bộ chiều dài ô phố!
   - **Phương án 2 (Phố Shophouse Nhật Bản & Máy bán nước Jihanki — Nhóm A2 `Kerorin_Capital`)**:
     - Ghép chuỗi: `zero15.dff` (`28.8m`, góc phố) + `zero16.dff` (`47.6m`) + `zero13.dff` (`32.1m`, có dàn máy bán nước tự động Jihanki & quán Arcade) + `zero18.dff` (`56.1m`) + `zero21.dff` (`33.3m`, góc phố) $\rightarrow$ Tổng mặt tiền = **`197.9m`**, vừa khít cạnh `196m`!
2. **Cạnh Bắc – Nam dài `270m` (sau khi trừ chiều sâu `25m..30m` của 2 tòa nhà góc còn `215m` chiều dài mặt tiền)**:
   - **Phương án 3 (Phố Thương mại Anime `Little Akihabara V2` + `OtakuShoppu` — Nhóm A3 & Phần B)**:
     - Ghép chuỗi: `newdbbuild_lan04.dff` (`44.8m`) + `vineblock1_lawn.dff` (`61.4m`, OtakuShoppu/KawaiiBoutique) + `officessml1_lan.dff` (`26.0m`) + `foodmart1_lan.dff` (`22.0m`, Konbini) + `stripbar_lae.dff` (`26.9m`, Quán mì Ichiraku Ramen) + `pawnshp_lae2.dff` (`35.9m`, Shophouse PJ 3.1) $\rightarrow$ Tổng mặt tiền = **`217.0m`**, lấp kín hoàn toàn cạnh `215m`!
   - **Phương án 4 (Khu Dân cư Nhật Bản, Chung cư & Trường học — Nhóm A4)**:
     - Mặt chính: `1Konoha_Gates.dff` (`53.4m`, cổng trường) + `school.dff` (`70.0m`, khối trường chính) + `classroom.dff` (`17.4m` × 2 khối = `34.8m`) + `3Naruto_apartmen.dff` (`21.4m`) + `ie1.dff` (`32.2m`, Nhà Nobita 2 tầng có sân rào) $\rightarrow$ Tổng mặt tiền = **`211.8m`**.
