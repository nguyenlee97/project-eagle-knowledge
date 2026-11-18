# Báo Cáo Lỗi Map & Chẩn Đoán Tự Động (Project Eagle Auto-Inspector)

- **Cập nhật lần cuối**: `2026-11-16 11:06:23`
- **Tổng số điểm lỗi đã ghi nhận**: **14**
- **Cơ sở dữ liệu Auto-Inspector**: `60,190` IDE models | `85,905` Text IPL inst | `62,839` Binary Stream IPL inst | `42,324` COL models | `1,116` ENEX doors

---

## I. Bảng Tổng Hợp Các Lỗi Đã Ghi Nhận

| Mã Bug | Thời gian | Phân loại lỗi | Khu vực (Zone) | Tọa độ lúc bấm `(X, Y, Z)` | Mép trước khi rơi `(X, Y, Z)` | Nghi phạm chính (`.dff` / `.ipl` / `.col`) |
|---|---|---|---|---|---|---|
| **BUG-014** | `2026-11-16 11:06:23` | ✅ **FIXED (M4-R2)** — Missing Wall COL | Extended / Unknown Zone | `-4266.72, -3010.03, -0.94` | `-4266.31, -3009.75, 14.15` | `md_city_fountain.dff (ID 6717) — fixed: 18,202 solid COL3 faces across 1+4 chunks (<84KB/chunk)` |
| **BUG-013** | `2026-11-16 11:04:41` | ✅ **FIXED (M4-R2)** — Missing Wall COL | Extended / Unknown Zone | `-4342.94, -3040.82, 0.82` | `-4344.33, -3029.51, 17.01` | `md_city_mid_knights.dff (ID 6712) — fixed: 30,928 solid COL3 faces across 1+6 chunks + welded Knights HQ stairs` |
| **BUG-012** | `2026-10-25 23:50:05` | 1. Fall Through Floor / Road (Missing COL) | MKLAS | `-1384.92, -4788.58, 24.25` | `-1384.97, -4788.61, 24.26` | `lamppost2.dff (ID 1290) @ 7.5m | CUSTOM/wibu01_japan_island.ipl:250 | COL:dynamic.col(0F/1B) [OK_COL]` |
| **BUG-011** | `2026-10-25 07:23:35` | 1. Fall Through Floor / Road (Missing COL) | Extended / Unknown Zone | `-1402.56, -3407.39, 55.98` | `-1403.54, -3404.41, 56.07` | `wb_gg_n03.dff (ID 11930) @ 69.3m | CUSTOM/wibu01_japan_island.ipl:177 | COL:wibu01_japan_island.col(646F/0B) [OK_COL]` |
| **BUG-010** | `2026-10-24 00:57:42` | 5. Other Map Glitch | Las Venturas (SA) (Vegas) - Sector VE | `1777.38, 701.00, 15.20` | `1777.38, 701.00, 15.20` | `wrhsegrnd02_lvs.dff (ID 8071) @ 112.2m | S&S/maps/sa/LV/vegasS.ipl:84 | COL:vegass_3.col(251F/11B) [OK_COL]` |
| **BUG-009** | `2026-10-24 00:22:39` | 1. Fall Through Floor / Road (Missing COL) | Region #25 (RDREG05) - Sector ACZB | `6991.16, 4239.44, 27.69` | `6991.16, 4239.44, 27.69` | `trafficlight1.dff (ID 1315) @ 4.9m | CUSTOM/custom_mods.ipl:636 | COL:dynamic.col(0F/1B) [OK_COL]` |
| **BUG-008** | `2026-10-23 01:58:45` | 1. Fall Through Floor / Road (Missing COL) | Independence / Philadelphia (IC01) | `8685.79, 6259.74, 30.58` | `8685.79, 6259.74, 30.58` | `kywroad24.dff (ID 31358) @ 47.0m | S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:122 | COL:keystonew.col(1585F/0B) [OK_COL]` |
| **BUG-007** | `2026-10-22 21:33:12` | 1. Roi xuyen san / Mat duong (Missing COL) | Liberty City / New York (LC01) - Khu COL3 | `14794.77, 8013.17, -20.23` | `14810.28, 8026.06, -20.23` | `tunl_2_bend.dff (ID 21157) @ 7.9m | S&S/maps/lc/comn.ipl:106 | COL:LC_generics.col(130F/0B) [OK_COL]` |
| **BUG-006** | `2026-10-22 21:21:35` | 1. Roi xuyen san / Mat duong (Missing COL) | Carcer City (CC06) - Khu CARCER | `11092.78, 8207.60, 19.52` | `11092.78, 8207.60, 19.52` | `dlkytree125.dff (ID 31917) @ 17.4m | S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:693 | COL:tree.col(13F/0B) [OK_COL]` |
| **BUG-005** | `2026-10-16 03:43:05` | 1. Roi xuyen san / Mat duong (Missing COL) | Carcer City (CC06) - Khu CARCER | `10587.38, 9900.29, 15.60` | `10578.59, 9894.56, 20.70` | `cctjournotest.dff (ID 152523) @ 8.7m | S&S/maps/cc/lacElevels.IPL:166 | COL:jornochurch.col(556F/0B) [OK_COL]` |
| **BUG-004** | `2026-10-16 03:42:42` | 1. Roi xuyen san / Mat duong (Missing COL) | Carcer City (CC06) - Khu CARCER | `10556.70, 9727.70, 991.96` | `10556.70, 9727.70, 991.96` | `wheel_o_fortune.dff (ID 1895) @ 12.7m | CUSTOM/custom_mods.ipl:938 | COL:props.col(0F/0B) [EMPTY_COL_0_FACES]` |
| **BUG-003** | `2026-10-16 03:41:51` | 1. Roi xuyen san / Mat duong (Missing COL) | Carcer City (CC06) - Khu CARCER | `10582.83, 9899.60, 20.55` | `10582.83, 9899.60, 20.55` | `CJ_Dumpster2.dff (ID 1344) @ 14.5m | S&S/maps/cc/lac_props2.IPL:96 | COL:dynamic2.col(12F/0B) [OK_COL]` |
| **BUG-002** | `2026-10-15 23:58:15` | 1. Roi xuyen san / Mat duong (Missing COL) | Carcer City (CC06) - Khu CARCER | `10794.84, 10255.07, 24.34` | `10794.84, 10255.07, 24.34` | `CJ_BLOCKER_BENCH.dff (ID 1368) @ 6.0m | S&S/maps/cc/lac_props.IPL:2757 | COL:dynamic2.col(0F/2B) [OK_COL]` |
| **BUG-001** | `2026-10-15 02:44:13` | 1. Roi xuyen san / Mat duong (Missing COL) | Los Santos (SA) (LA01) - Khu LA | `1544.50, -1675.50, -6.40` | `1538.00, -1675.00, 13.55` | `Roads14_LAn.dff (ID 4150) @ 14.1m | S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:63 | COL:lan_2.col(62F/0B) [OK_COL]` |

---

## II. Chi Tiết Chẩn Đoán Từng Điểm Lỗi & Hướng Dẫn Sửa

### 🛠️ BUG-014: 1. Fall Through Floor / Road (Missing COL) — Extended / Unknown Zone
- **Thời điểm ghi nhận**: `2026-11-16 11:06:23`
- **Tọa độ hiện tại `(X, Y, Z)`**: `-4266.721, -3010.034, -0.942` (Heading: `165.1°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `-0.002, -0.007, 0.009` (Phát hiện rơi tự do: `True`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `-4266.310, -3009.750, 14.150` (`5.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `-4266.650, -3009.780, 0.280`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Check ENEX `MD_ALC` at `CUSTOM/mondstadt_m1_wilds.ipl:222` (Exit=(-4245.55, -3006.85, 12.38), TargetInt=0): If entering causes a freefall, verify that Interior 0 .IPL is mounted in gta.dat or raise exit Z by +0.5m. | Nearest object: `md_city_fountain` (ID `6717`) at `CUSTOM/mondstadt_m0_city.ipl:10` (DFF in `['custom/mondstadt_m0_city.img']`, COL `mondstadt_m0_city.col (4700 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `-4266.31` | `-3009.75` | **`14.15`** | `-0.032` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `-4266.65` | `-3009.78` | **`-0.37`** | `0.040` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `-4266.65` | `-3009.78` | **`0.95`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `-4266.65` | `-3009.78` | **`0.64`** | `-0.025` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `-4266.72` | `-3010.03` | **`-0.94`** | `0.009` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `24.44m` (XY `16.9m`, dZ `+17.5m`) | `6717` | **`md_city_fountain`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:10` | `CUSTOM/mondstadt_m0_city.ide:11` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=103.3m, **4700F/0B/0S**) | ✅ OK |
| `41.52m` (XY `40.6m`, dZ `+8.7m`) | `6711` | **`md_city_lower_plaza`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:4` | `CUSTOM/mondstadt_m0_city.ide:5` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=103.5m, **4700F/0B/0S**) | ✅ OK |
| `61.98m` (XY `61.4m`, dZ `+8.5m`) | `6710` | **`md_city_gate_walls`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:3` | `CUSTOM/mondstadt_m0_city.ide:4` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=101.4m, **4700F/0B/0S**) | ✅ OK |
| `68.57m` (XY `65.3m`, dZ `+21.0m`) | `6718` | **`md_city_north_qtr`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:11` | `CUSTOM/mondstadt_m0_city.ide:12` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=82.5m, **5100F/0B/0S**) | ✅ OK |
| `83.91m` (XY `77.8m`, dZ `+30.1m`) | `6712` | **`md_city_mid_knights`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:5` | `CUSTOM/mondstadt_m0_city.ide:6` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=90.7m, **4700F/0B/0S**) | ✅ OK |
| `126.27m` (XY `126.2m`, dZ `-20.4m`) | `6745` | **`mw1_t15`** | `mondstadt_wilds_m1` | `CUSTOM/mondstadt_m1_wilds.ipl:18` | `CUSTOM/mondstadt_m1_wilds.ide:35` | `custom/mondstadt_m1_wilds.img` | `mondstadt_m1_wilds.col` (`COL3`, R=181.6m, **2079F/0B/0S**) | ✅ OK |
| `141.89m` (XY `141.5m`, dZ `+1.4m`) | `6715` | **`md_island_north`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:8` | `CUSTOM/mondstadt_m0_city.ide:9` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=264.5m, **463F/0B/0S**) | ✅ OK |
| `145.10m` (XY `144.7m`, dZ `-14.8m`) | `6751` | **`mw1_t21`** | `mondstadt_wilds_m1` | `CUSTOM/mondstadt_m1_wilds.ipl:24` | `CUSTOM/mondstadt_m1_wilds.ide:47` | `custom/mondstadt_m1_wilds.img` | `mondstadt_m1_wilds.col` (`COL3`, R=181.5m, **2067F/0B/0S**) | ✅ OK |
| `148.04m` (XY `147.5m`, dZ `-20.4m`) | `6716` | **`md_island_bridge`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:9` | `CUSTOM/mondstadt_m0_city.ide:10` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=232.2m, **807F/0B/0S**) | ✅ OK |

#### 4. Các Cửa Ra/Vào Nội Thất (`ENEX`) Trong Bán Kính 25m
| Tên ENEX | Khoảng cách | Phía khớp | Tọa độ Vào `(x1, y1, z1)` | Tọa độ Đích `(x2, y2, z2)` | Target Interior | Nguồn `.IPL` |
|---|---|---|---|---|---|---|
| **`MD_ALC`** | `20.96m` | `EXIT_DEST` | `(-4243.1, -3005.05, 12.48)` | `(-4245.55, -3006.85, 12.38)` | `0` | `CUSTOM/mondstadt_m1_wilds.ipl:222` |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-014] 1. Fall Through Floor / Road (Missing COL) @ Extended / Unknown Zone
- Coords: X=-4266.72, Y=-3010.03, Z=-0.94 (Heading=165.1°, Interior=0)
- Pre-Fall Edge: X=-4266.31, Y=-3009.75, Z=14.15
- Nearest Object: md_city_fountain.dff (ID 6717) in CUSTOM/mondstadt_m0_city.ipl:10 [COL: mondstadt_m0_city.col]
- Note: md_city_fountain.dff (ID 6717) @ 24.4m | CUSTOM/mondstadt_m0_city.ipl:10 | COL:mondstadt_m0_city.col(4700F/0B) [OK_COL]
```

---

### 🛠️ BUG-013: 1. Fall Through Floor / Road (Missing COL) — Extended / Unknown Zone
- **Thời điểm ghi nhận**: `2026-11-16 11:04:41`
- **Tọa độ hiện tại `(X, Y, Z)`**: `-4342.935, -3040.815, 0.820` (Heading: `3.2°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `0.000, -0.000, -0.018` (Phát hiện rơi tự do: `True`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `-4344.330, -3029.510, 17.010` (`5.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `-4342.940, -3040.810, 1.600`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Check ENEX `MD_KNI` at `CUSTOM/mondstadt_m1_wilds.ipl:218` (Exit=(-4350.0, -3030.5, 32.53), TargetInt=0): If entering causes a freefall, verify that Interior 0 .IPL is mounted in gta.dat or raise exit Z by +0.5m. | Nearest object: `md_city_mid_knights` (ID `6712`) at `CUSTOM/mondstadt_m0_city.ipl:5` (DFF in `['custom/mondstadt_m0_city.img']`, COL `mondstadt_m0_city.col (4700 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `-4344.33` | `-3029.51` | **`17.01`** | `-0.490` | `0` | ⚠️ Đang rơi / Không ổn định |
| `-3.0s` | `-4342.94` | `-3040.81` | **`0.95`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `-4342.94` | `-3040.81` | **`0.95`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `-4342.94` | `-3040.81` | **`0.95`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `-4342.94` | `-3040.82` | **`0.82`** | `-0.018` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `28.25m` (XY `5.9m`, dZ `+27.3m`) | `6712` | **`md_city_mid_knights`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:5` | `CUSTOM/mondstadt_m0_city.ide:6` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=90.7m, **4700F/0B/0S**) | ✅ OK |
| `69.17m` (XY `69.2m`, dZ `-1.4m`) | `6715` | **`md_island_north`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:8` | `CUSTOM/mondstadt_m0_city.ide:9` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=264.5m, **463F/0B/0S**) | ✅ OK |
| `83.70m` (XY `82.2m`, dZ `+14.6m`) | `6717` | **`md_city_fountain`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:10` | `CUSTOM/mondstadt_m0_city.ide:11` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=103.3m, **4700F/0B/0S**) | ✅ OK |
| `87.11m` (XY `85.2m`, dZ `+18.1m`) | `6718` | **`md_city_north_qtr`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:11` | `CUSTOM/mondstadt_m0_city.ide:12` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=82.5m, **5100F/0B/0S**) | ✅ OK |
| `105.14m` (XY `103.0m`, dZ `+5.8m`) | `6711` | **`md_city_lower_plaza`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:4` | `CUSTOM/mondstadt_m0_city.ide:5` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=103.5m, **4700F/0B/0S**) | ✅ OK |
| `149.25m` (XY `149.1m`, dZ `-23.2m`) | `6745` | **`mw1_t15`** | `mondstadt_wilds_m1` | `CUSTOM/mondstadt_m1_wilds.ipl:18` | `CUSTOM/mondstadt_m1_wilds.ide:35` | `custom/mondstadt_m1_wilds.img` | `mondstadt_m1_wilds.col` (`COL3`, R=181.6m, **2079F/0B/0S**) | ✅ OK |
| `160.89m` (XY `160.8m`, dZ `-9.7m`) | `6744` | **`mw1_t14`** | `mondstadt_wilds_m1` | `CUSTOM/mondstadt_m1_wilds.ipl:17` | `CUSTOM/mondstadt_m1_wilds.ide:33` | `custom/mondstadt_m1_wilds.img` | `mondstadt_m1_wilds.col` (`COL3`, R=181.3m, **2097F/0B/0S**) | ✅ OK |
| `227.22m` (XY `226.9m`, dZ `-23.3m`) | `6716` | **`md_island_bridge`** | `mondstadt_city` | `CUSTOM/mondstadt_m0_city.ipl:9` | `CUSTOM/mondstadt_m0_city.ide:10` | `custom/mondstadt_m0_city.img` | `mondstadt_m0_city.col` (`COL3`, R=232.2m, **807F/0B/0S**) | ✅ OK |

#### 4. Các Cửa Ra/Vào Nội Thất (`ENEX`) Trong Bán Kính 25m
| Tên ENEX | Khoảng cách | Phía khớp | Tọa độ Vào `(x1, y1, z1)` | Tọa độ Đích `(x2, y2, z2)` | Target Interior | Nguồn `.IPL` |
|---|---|---|---|---|---|---|
| **`MD_KNI`** | `5.76m` | `EXIT_DEST` | `(-4354.32, -3031.41, 34.43)` | `(-4350.0, -3030.5, 32.53)` | `0` | `CUSTOM/mondstadt_m1_wilds.ipl:218` |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-013] 1. Fall Through Floor / Road (Missing COL) @ Extended / Unknown Zone
- Coords: X=-4342.94, Y=-3040.82, Z=0.82 (Heading=3.2°, Interior=0)
- Pre-Fall Edge: X=-4344.33, Y=-3029.51, Z=17.01
- Nearest Object: md_city_mid_knights.dff (ID 6712) in CUSTOM/mondstadt_m0_city.ipl:5 [COL: mondstadt_m0_city.col]
- Note: md_city_mid_knights.dff (ID 6712) @ 28.2m | CUSTOM/mondstadt_m0_city.ipl:5 | COL:mondstadt_m0_city.col(4700F/0B) [OK_COL]
```

---

### 🛠️ BUG-012: 1. Fall Through Floor / Road (Missing COL) — MKLAS
- **Thời điểm ghi nhận**: `2026-10-25 23:50:05`
- **Tọa độ hiện tại `(X, Y, Z)`**: `-1384.923, -4788.580, 24.245` (Heading: `43.6°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `True`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, 0.000` (Phát hiện rơi tự do: `False`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `-1384.970, -4788.610, 24.260` (`2.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `-1384.790, -4788.740, 24.910`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Nearest object: `lamppost2` (ID `1290`) at `CUSTOM/wibu01_japan_island.ipl:250` (DFF in `['S&S/Cdimages/default/Generic.img']`, COL `dynamic.col (0 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `-1385.56` | `-4802.36` | **`24.21`** | `-0.010` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `-1384.25` | `-4792.42` | **`24.22`** | `-0.001` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `-1384.97` | `-4788.61` | **`24.26`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `-1384.92` | `-4788.58` | **`24.24`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `-1384.92` | `-4788.58` | **`24.25`** | `0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `7.50m` (XY `5.7m`, dZ `+4.8m`) | `1290` | **`lamppost2`** | `dynsigns` | `CUSTOM/wibu01_japan_island.ipl:250` | `data/maps/generic/dynamic.ide:85` | `S&S/Cdimages/default/Generic.img` | `dynamic.col` (`COL3`, R=6.9m, **0F/1B/5S**) | ✅ OK |
| `5.53m` (XY `5.5m`, dZ `-0.9m`) | `3203` | **`sakura_tree_04`** *(LOD)* | `wibu_sakura_trees` | `CUSTOM/wibu01_japan_island.ipl:149` | `CUSTOM/wibu01_japan_island.ide:119` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=9.9m, **0F/1B/0S**) | ✅ OK |
| `34.40m` (XY `34.0m`, dZ `-5.1m`) | `11816` | **`kentry01`** *(LOD)* | `kero` | `CUSTOM/wibu01_japan_island.ipl:93` | `CUSTOM/wibu01_japan_island.ide:18` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=88.5m, **2461F/0B/0S**) | ✅ OK |
| `116.16m` (XY `115.1m`, dZ `-15.6m`) | `11851` | **`dodai02`** *(LOD)* | `akihabara_town` | `CUSTOM/wibu01_japan_island.ipl:2` | `CUSTOM/wibu01_japan_island.ide:49` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=183.3m, **31F/0B/0S**) | ✅ OK |
| `123.79m` (XY `122.8m`, dZ `-15.6m`) | `11851` | **`dodai02`** *(LOD)* | `akihabara_town` | `CUSTOM/wibu01_japan_island.ipl:75` | `CUSTOM/wibu01_japan_island.ide:49` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=183.3m, **31F/0B/0S**) | ✅ OK |
| `125.16m` (XY `124.2m`, dZ `-15.6m`) | `11882` | **`laox_honten`** *(LOD)* | `akihabara_town` | `CUSTOM/wibu01_japan_island.ipl:32` | `CUSTOM/wibu01_japan_island.ide:80` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=365.7m, **2096F/0B/0S**) | ✅ OK |
| `133.91m` (XY `133.7m`, dZ `+8.1m`) | `3196` | **`lodabase1`** *(LOD)* | `Abase` | `CUSTOM/wibu01_japan_island.ipl:128` | `CUSTOM/wibu01_japan_island.ide:112` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=133.0m, **5500F/0B/0S**) | ✅ OK |
| `153.42m` (XY `152.6m`, dZ `-15.6m`) | `11854` | **`douro`** *(LOD)* | `akihabara_town` | `CUSTOM/wibu01_japan_island.ipl:5` | `CUSTOM/wibu01_japan_island.ide:52` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=252.5m, **6374F/0B/0S**) | ✅ OK |
| `155.83m` (XY `155.8m`, dZ `-2.7m`) | `11846` | **`lights01`** *(LOD)* | `kero` | `CUSTOM/wibu01_japan_island.ipl:92` | `CUSTOM/wibu01_japan_island.ide:166` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=156.8m, **0F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-012] 1. Fall Through Floor / Road (Missing COL) @ MKLAS
- Coords: X=-1384.92, Y=-4788.58, Z=24.25 (Heading=43.6°, Interior=0)
- Pre-Fall Edge: X=-1384.97, Y=-4788.61, Z=24.26
- Nearest Object: lamppost2.dff (ID 1290) in CUSTOM/wibu01_japan_island.ipl:250 [COL: dynamic.col]
- Note: lamppost2.dff (ID 1290) @ 7.5m | CUSTOM/wibu01_japan_island.ipl:250 | COL:dynamic.col(0F/1B) [OK_COL]
```

---

### 🛠️ BUG-011: 1. Fall Through Floor / Road (Missing COL) — Extended / Unknown Zone
- **Thời điểm ghi nhận**: `2026-10-25 07:23:35`
- **Tọa độ hiện tại `(X, Y, Z)`**: `-1402.556, -3407.393, 55.976` (Heading: `202.7°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `-0.000, -0.000, -0.000` (Phát hiện rơi tự do: `False`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `-1403.540, -3404.410, 56.070` (`5.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `-1402.170, -3406.170, 56.660`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Nearest object: `wb_gg_n03` (ID `11930`) at `CUSTOM/wibu01_japan_island.ipl:177` (DFF in `['custom/wibu01_japan_island.img']`, COL `wibu01_japan_island.col (646 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `-1403.54` | `-3404.41` | **`56.07`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `-1402.81` | `-3404.91` | **`56.05`** | `-0.008` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `-1402.45` | `-3407.30` | **`55.98`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `-1402.45` | `-3407.30` | **`55.98`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `-1402.56` | `-3407.39` | **`55.98`** | `-0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `69.26m` (XY `48.5m`, dZ `+49.5m`) | `11930` | **`wb_gg_n03`** *(LOD)* | `wb_goldengate` | `CUSTOM/wibu01_japan_island.ipl:177` | `CUSTOM/wibu01_japan_island.ide:139` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=103.0m, **646F/0B/0S**) | ✅ OK |
| `124.73m` (XY `111.7m`, dZ `+55.5m`) | `11929` | **`wb_gg_n05`** *(LOD)* | `wb_goldengate` | `CUSTOM/wibu01_japan_island.ipl:175` | `CUSTOM/wibu01_japan_island.ide:137` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=108.3m, **726F/0B/0S**) | ✅ OK |
| `132.11m` (XY `130.6m`, dZ `+20.3m`) | `11931` | **`wb_gg_n01`** *(LOD)* | `wb_goldengate` | `CUSTOM/wibu01_japan_island.ipl:179` | `CUSTOM/wibu01_japan_island.ide:141` | `custom/wibu01_japan_island.img` | `wibu01_japan_island.col` (`COL3`, R=136.7m, **532F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-011] 1. Fall Through Floor / Road (Missing COL) @ Extended / Unknown Zone
- Coords: X=-1402.56, Y=-3407.39, Z=55.98 (Heading=202.7°, Interior=0)
- Pre-Fall Edge: X=-1403.54, Y=-3404.41, Z=56.07
- Nearest Object: wb_gg_n03.dff (ID 11930) in CUSTOM/wibu01_japan_island.ipl:177 [COL: wibu01_japan_island.col]
- Note: wb_gg_n03.dff (ID 11930) @ 69.3m | CUSTOM/wibu01_japan_island.ipl:177 | COL:wibu01_japan_island.col(646F/0B) [OK_COL]
```

---

### 🛠️ BUG-010: 5. Other Map Glitch — Las Venturas (SA) (Vegas) - Sector VE
- **Thời điểm ghi nhận**: `2026-10-24 00:57:42`
- **Tọa độ hiện tại `(X, Y, Z)`**: `1777.375, 701.000, 15.196` (Heading: `170.8°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `True`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, 0.000` (Phát hiện rơi tự do: `False`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `1777.380, 701.000, 15.200` (`3.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `1777.380, 701.000, 15.850`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Nearest object: `wrhsegrnd02_lvs` (ID `8071`) at `S&S/maps/sa/LV/vegasS.ipl:84` (DFF in `['S&S/Cdimages/andreas/GAME_LV.img']`, COL `vegass_3.col (251 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `1777.40` | `701.16` | **`15.19`** | `0.002` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `1777.38` | `701.00` | **`15.20`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `1777.38` | `701.00` | **`15.20`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `1777.38` | `701.00` | **`15.20`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `1777.38` | `701.00` | **`15.20`** | `0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `112.17m` (XY `112.1m`, dZ `-4.3m`) | `8071` | **`wrhsegrnd02_lvs`** | `vgsswarehse01` | `S&S/maps/sa/LV/vegasS.ipl:84` | `data/maps/vegas/VegasS.ide:95` | `S&S/Cdimages/andreas/GAME_LV.img` | `vegass_3.col` (`COL3`, R=150.2m, **251F/11B/0S**) | ✅ OK |
| `114.30m` (XY `108.8m`, dZ `-35.2m`) | `8470` | **`vgsEedge27`** | `vgsecoast` | `S&S/maps/sa/LV/vegasE.ipl:50` | `data/maps/vegas/vegasE.ide:81` | `S&S/Cdimages/andreas/GAME_LV.img` | `vegase_10.col` (`COL3`, R=194.4m, **457F/0B/0S**) | ✅ OK |
| `22.27m` (XY `22.1m`, dZ `-2.9m`) | `7995` | **`VegasSroad088`** | `vgsshiways` | `S&S/maps/sa/LV/vegasS.ipl:19` | `data/maps/vegas/VegasS.ide:19` | `S&S/Cdimages/andreas/GAME_LV.img` | `vegass_3.col` (`COL3`, R=106.6m, **133F/0B/0S**) | ✅ OK |
| `23.69m` (XY `23.7m`, dZ `-0.2m`) | `8380` | **`vegasSedge1919`** | `vgsshiways` | `S&S/maps/sa/LV/vegasS.ipl:369` | `data/maps/vegas/VegasS.ide:401` | `S&S/Cdimages/andreas/GAME_LV.img` | `vegass_3.col` (`COL3`, R=105.0m, **152F/0B/0S**) | ✅ OK |
| `112.02m` (XY `111.9m`, dZ `+5.9m`) | `8087` | **`vgstwires26_lvs`** | `vgsstwires` | `S&S/maps/sa/LV/vegasS.ipl:94` | `data/maps/vegas/VegasS.ide:111` | `S&S/Cdimages/andreas/GAME_LV.img` | `vegass_3.col` (`COL3`, R=110.1m, **0F/0B/0S**) | ✅ OK |
| `143.84m` (XY `140.0m`, dZ `-33.0m`) | `8002` | **`vegasSedge20`** | `vgssland02` | `S&S/maps/sa/LV/vegasS.ipl:26` | `data/maps/vegas/VegasS.ide:26` | `S&S/Cdimages/andreas/GAME_LV.img` | `vegass_3.col` (`COL3`, R=187.3m, **253F/0B/0S**) | ✅ OK |
| `250.66m` (XY `242.8m`, dZ `-62.2m`) | `4346` | **`sbvgsSseafloor04`** *(LOD)* | `seabed` | `S&S/maps/sa/leveldes/seabed.ipl:109` | `data/maps/leveldes/seabed.ide:108` | `S&S/Cdimages/andreas/GAME_SA.img` | `seabed7.col` (`COL2`, R=243.3m, **107F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-010] 5. Other Map Glitch @ Las Venturas (SA) (Vegas) - Sector VE
- Coords: X=1777.38, Y=701.00, Z=15.20 (Heading=170.8°, Interior=0)
- Pre-Fall Edge: X=1777.38, Y=701.00, Z=15.20
- Nearest Object: wrhsegrnd02_lvs.dff (ID 8071) in S&S/maps/sa/LV/vegasS.ipl:84 [COL: vegass_3.col]
- Note: wrhsegrnd02_lvs.dff (ID 8071) @ 112.2m | S&S/maps/sa/LV/vegasS.ipl:84 | COL:vegass_3.col(251F/11B) [OK_COL]
```

---

### 🛠️ BUG-009: 1. Fall Through Floor / Road (Missing COL) — Region #25 (RDREG05) - Sector ACZB
- **Thời điểm ghi nhận**: `2026-10-24 00:22:39`
- **Tọa độ hiện tại `(X, Y, Z)`**: `6991.161, 4239.437, 27.692` (Heading: `193.3°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `True`
- **Vận tốc `(vx, vy, vz)`**: `0.079, -0.391, -0.011` (Phát hiện rơi tự do: `False`)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `6991.160, 4239.440, 28.340`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Nearest object: `trafficlight1` (ID `1315`) at `CUSTOM/custom_mods.ipl:636` (DFF in `['S&S/Cdimages/default/Generic.img']`, COL `dynamic.col (0 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `6991.16` | `4239.44` | **`27.69`** | `-0.011` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `6991.16` | `4239.44` | **`27.69`** | `-0.011` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `6991.16` | `4239.44` | **`27.69`** | `-0.011` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `6991.16` | `4239.44` | **`27.69`** | `-0.011` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `6991.16` | `4239.44` | **`27.69`** | `-0.011` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `4.94m` (XY `4.3m`, dZ `+2.5m`) | `1315` | **`trafficlight1`** | `dyntraffic` | `CUSTOM/custom_mods.ipl:636` | `data/maps/generic/dynamic.ide:113` | `S&S/Cdimages/default/Generic.img` | `dynamic.col` (`COL3`, R=5.4m, **0F/1B/5S**) | ✅ OK |
| `6.25m` (XY `4.4m`, dZ `+4.5m`) | `61104` | **`smwtree102`** *(LOD)* | `lodsmwtree119_grp26` | `S&S/maps/anne/anneland.ipl:210` | `S&S/Cdimages/anneland/game_anne.ide:106` | `S&S/Cdimages/anneland/game_anne.img` | `somewhere.col` (`COL3`, R=60.0m, **48F/0B/0S**) | ✅ OK |
| `6.25m` (XY `4.4m`, dZ `+4.5m`) | `61714` | **`lodsmwtree102`** *(LOD)* | `lodsmwtree119_grp26` | `S&S/maps/anne/anneland.ipl:211` | `S&S/Cdimages/anneland/game_anne.ide:717` | `S&S/Cdimages/anneland/game_anne.img` | ❌ **MISSING COL** | ✅ OK |
| `42.27m` (XY `42.3m`, dZ `-0.2m`) | `63466` | **`smwbuild67`** *(LOD)* | `lodsmwbuild299_grp1` | `S&S/maps/anne/somewhere.ipl:134` | `S&S/Cdimages/anneland/game_smw.ide:68` | `S&S/Cdimages/anneland/game_anne.img` | `somewherebuild.col` (`COL3`, R=39.7m, **128F/0B/0S**) | ✅ OK |
| `42.28m` (XY `42.3m`, dZ `-0.8m`) | `63465` | **`smwbuild66`** *(LOD)* | `lodsmwbuild299_grp1` | `S&S/maps/anne/somewhere.ipl:132` | `S&S/Cdimages/anneland/game_smw.ide:67` | `S&S/Cdimages/anneland/game_anne.img` | `somewherebuild.col` (`COL3`, R=39.5m, **24F/0B/0S**) | ✅ OK |
| `57.49m` (XY `57.5m`, dZ `-0.2m`) | `63478` | **`smwbuild79`** *(LOD)* | `lodsmwbuild299_grp1` | `S&S/maps/anne/somewhere.ipl:158` | `S&S/Cdimages/anneland/game_smw.ide:80` | `S&S/Cdimages/anneland/game_anne.img` | `somewherebuild.col` (`COL3`, R=53.0m, **56F/0B/0S**) | ✅ OK |
| `57.50m` (XY `57.5m`, dZ `-0.9m`) | `63477` | **`smwbuild78`** *(LOD)* | `lodsmwagrocoop_grp6` | `S&S/maps/anne/somewhere.ipl:156` | `S&S/Cdimages/anneland/game_smw.ide:79` | `S&S/Cdimages/anneland/game_anne.img` | `somewherebuild.col` (`COL3`, R=52.6m, **125F/0B/0S**) | ✅ OK |
| `82.26m` (XY `82.3m`, dZ `-0.6m`) | `61562` | **`smwroad106`** *(LOD)* | `lodsmwbuild299_grp1` | `S&S/maps/anne/anneland.ipl:1126` | `S&S/Cdimages/anneland/game_anne.ide:564` | `S&S/Cdimages/anneland/game_anne.img` | `somewhere.col` (`COL3`, R=149.0m, **2501F/0B/0S**) | ✅ OK |
| `94.90m` (XY `94.8m`, dZ `+4.5m`) | `61085` | **`smwtree83`** *(LOD)* | `lodsmwtree119_grp26` | `S&S/maps/anne/anneland.ipl:172` | `S&S/Cdimages/anneland/game_anne.ide:87` | `S&S/Cdimages/anneland/game_anne.img` | `somewhere.col` (`COL3`, R=95.7m, **88F/0B/0S**) | ✅ OK |
| `125.70m` (XY `125.7m`, dZ `+2.4m`) | `61563` | **`smwroad107`** *(LOD)* | `lodsmwbuild299_grp1` | `S&S/maps/anne/anneland.ipl:1128` | `S&S/Cdimages/anneland/game_anne.ide:565` | `S&S/Cdimages/anneland/game_anne.img` | `somewhere.col` (`COL3`, R=151.9m, **4454F/0B/0S**) | ✅ OK |
| `128.72m` (XY `128.7m`, dZ `-1.0m`) | `61319` | **`smwgrass128`** *(LOD)* | `lodsmwbuild105_grp8` | `S&S/maps/anne/anneland.ipl:640` | `S&S/Cdimages/anneland/game_anne.ide:321` | `S&S/Cdimages/anneland/game_anne.img` | `somewhere.col` (`COL3`, R=148.1m, **109F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-009] 1. Fall Through Floor / Road (Missing COL) @ Region #25 (RDREG05) - Sector ACZB
- Coords: X=6991.16, Y=4239.44, Z=27.69 (Heading=193.3°, Interior=0)
- Velocity: vz=-0.011
- Nearest Object: trafficlight1.dff (ID 1315) in CUSTOM/custom_mods.ipl:636 [COL: dynamic.col]
- Note: trafficlight1.dff (ID 1315) @ 4.9m | CUSTOM/custom_mods.ipl:636 | COL:dynamic.col(0F/1B) [OK_COL]
```

---

### 🛠️ BUG-008: 1. Fall Through Floor / Road (Missing COL) — Independence / Philadelphia (IC01)
- **Thời điểm ghi nhận**: `2026-10-23 01:58:45`
- **Tọa độ hiện tại `(X, Y, Z)`**: `8685.794, 6259.736, 30.578` (Heading: `28.5°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `True`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, 0.000` (Phát hiện rơi tự do: `False`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `8685.790, 6259.740, 30.580` (`5.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `8685.790, 6259.740, 31.230`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Nearest object: `kywroad24` (ID `31358`) at `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:122` (DFF in `['S&S/Cdimages/keystone/GAME_KEY.img']`, COL `keystonew.col (1585 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `8685.79` | `6259.74` | **`30.58`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `8685.79` | `6259.74` | **`30.58`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `8685.79` | `6259.74` | **`30.58`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `8685.79` | `6259.74` | **`30.58`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `8685.79` | `6259.74` | **`30.58`** | `0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `47.04m` (XY `46.5m`, dZ `-6.9m`) | `31358` | **`kywroad24`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:122` | `S&S/Cdimages/keystone/game_key.ide:535` | `S&S/Cdimages/keystone/GAME_KEY.img` | `keystonew.col` (`COL3`, R=114.7m, **1585F/0B/0S**) | ✅ OK |
| `61.43m` (XY `61.4m`, dZ `-0.1m`) | `31778` | **`kywtree16`** *(LOD)* | `kytrees` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:554` | `S&S/Cdimages/keystone/game_key.ide:955` | `S&S/Cdimages/keystone/GAME_KEY.img` | `kywtree.col` (`COL3`, R=115.5m, **0F/0B/0S**) | ✅ OK |
| `82.04m` (XY `81.7m`, dZ `-7.9m`) | `31311` | **`kywgrass27`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:75` | `S&S/Cdimages/keystone/game_key.ide:488` | `S&S/Cdimages/keystone/GAME_KEY.img` | `keystonew.col` (`COL3`, R=98.6m, **35F/0B/0S**) | ✅ OK |
| `86.32m` (XY `82.7m`, dZ `-24.9m`) | `31433` | **`kywrock7`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:197` | `S&S/Cdimages/keystone/game_key.ide:610` | `S&S/Cdimages/keystone/GAME_KEY.img` | `keystonew.col` (`COL3`, R=105.1m, **150F/0B/0S**) | ✅ OK |
| `109.59m` (XY `109.2m`, dZ `-8.7m`) | `31312` | **`kywgrass28`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:76` | `S&S/Cdimages/keystone/game_key.ide:489` | `S&S/Cdimages/keystone/GAME_KEY.img` | `keystonew.col` (`COL3`, R=145.9m, **103F/0B/0S**) | ✅ OK |
| `125.22m` (XY `122.5m`, dZ `-25.9m`) | `31434` | **`kywrock8`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:198` | `S&S/Cdimages/keystone/game_key.ide:611` | `S&S/Cdimages/keystone/GAME_KEY.img` | `keystonew.col` (`COL3`, R=130.0m, **123F/0B/0S**) | ✅ OK |
| `198.32m` (XY `198.3m`, dZ `+0.4m`) | `31779` | **`kywtree17`** *(LOD)* | `kytrees` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:555` | `S&S/Cdimages/keystone/game_key.ide:956` | `S&S/Cdimages/keystone/GAME_KEY.img` | `kywtree.col` (`COL3`, R=204.3m, **0F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-008] 1. Fall Through Floor / Road (Missing COL) @ Independence / Philadelphia (IC01)
- Coords: X=8685.79, Y=6259.74, Z=30.58 (Heading=28.5°, Interior=0)
- Pre-Fall Edge: X=8685.79, Y=6259.74, Z=30.58
- Nearest Object: kywroad24.dff (ID 31358) in S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:122 [COL: keystonew.col]
- Note: kywroad24.dff (ID 31358) @ 47.0m | S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:122 | COL:keystonew.col(1585F/0B) [OK_COL]
```

---

### 🛠️ BUG-007: 1. Roi xuyen san / Mat duong (Missing COL) — Liberty City / New York (LC01) - Khu COL3
- **Thời điểm ghi nhận**: `2026-10-22 21:33:12`
- **Tọa độ hiện tại `(X, Y, Z)`**: `14794.773, 8013.167, -20.233` (Heading: `122.2°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `True`
- **Vận tốc `(vx, vy, vz)`**: `-0.367, -0.230, 0.000` (Phát hiện rơi tự do: `True`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `14810.280, 8026.060, -20.230` (`5.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `13632.440, 8298.490, -13.920`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Vat the gan nhat: `tunl_2_bend` (ID `21157`) tai `S&S/maps/lc/comn.ipl:106` (DFF trong `['S&S/Cdimages/liberty/GAME_LC.img']`, COL `LC_generics.col (130 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `14810.28` | `8026.06` | **`-20.23`** | `-0.000` | `0` | ⚠️ Đang rơi / Không ổn định |
| `-3.0s` | `14804.47` | `8020.04` | **`-20.24`** | `0.001` | `0` | ⚠️ Đang rơi / Không ổn định |
| `-2.0s` | `14799.57` | `8016.28` | **`-20.23`** | `-0.000` | `0` | ⚠️ Đang rơi / Không ổn định |
| `-1.0s` | `14798.09` | `8015.29` | **`-20.23`** | `-0.000` | `0` | ⚠️ Đang rơi / Không ổn định |
| `-0.0s` | `14794.77` | `8013.17` | **`-20.23`** | `0.000` | `0` | ⚠️ Đang rơi / Không ổn định |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `7.88m` (XY `7.6m`, dZ `+2.2m`) | `21157` | **`tunl_2_bend`** | `roadtunnel` | `S&S/maps/lc/comn.ipl:106` | `S&S/Cdimages/liberty/LC_generic.ide:27` | `S&S/Cdimages/liberty/GAME_LC.img` | `LC_generics.col` (`COL3`, R=48.9m, **130F/0B/0S**) | ✅ OK |
| `123.28m` (XY `119.6m`, dZ `+29.9m`) | `21659` | **`com_landnew23a`** | `comjetty` | `S&S/maps/lc/comn.ipl:413` | `S&S/Cdimages/liberty/comNtop.ide:111` | `S&S/Cdimages/liberty/GAME_LC.img` | `commerfull.col` (`COL3`, R=141.2m, **303F/0B/0S**) | ✅ OK |
| `100.36m` (XY `95.7m`, dZ `+30.4m`) | `21708` | **`comtop_tshad6`** | `treeshadow` | `S&S/maps/lc/comn.ipl:476` | `S&S/Cdimages/liberty/comNtop.ide:162` | `S&S/Cdimages/liberty/GAME_LC.img` | `commerfull.col` (`COL3`, R=193.7m, **0F/0B/0S**) | ✅ OK |
| `47.62m` (XY `36.0m`, dZ `+31.1m`) | `21556` | **`arc_bridge`** *(LOD)* | `comjetty` | `S&S/maps/lc/comn.ipl:46` | `S&S/Cdimages/liberty/comNtop.ide:8` | `S&S/Cdimages/liberty/GAME_LC.img` | `commerfull.col` (`COL3`, R=39.5m, **218F/6B/18S**) | ✅ OK |
| `73.31m` (XY `71.4m`, dZ `+16.5m`) | `23627` | **`seabed_lc28`** *(LOD)* | `indbeach` | `S&S/maps/lc/LC_seabed.ipl:136` | `S&S/Cdimages/liberty/LC_seabed.ide:29` | `S&S/Cdimages/liberty/GAME_LC.img` | `seabed1_lc.col` (`COL2`, R=284.0m, **139F/0B/0S**) | ✅ OK |
| `104.41m` (XY `101.0m`, dZ `+26.5m`) | `21581` | **`com_landnew23b`** *(LOD)* | `comjetty` | `S&S/maps/lc/comn.ipl:66` | `S&S/Cdimages/liberty/comNtop.ide:33` | `S&S/Cdimages/liberty/GAME_LC.img` | `commerfull.col` (`COL3`, R=120.8m, **282F/0B/0S**) | ✅ OK |
| `111.01m` (XY `105.7m`, dZ `+33.9m`) | `21743` | **`lc_comntoprd3`** *(LOD)* | `comroads` | `S&S/maps/lc/comn.ipl:23` | `S&S/Cdimages/liberty/comroad.ide:25` | `S&S/Cdimages/liberty/GAME_LC.img` | `commerfull.col` (`COL3`, R=158.6m, **227F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-007] 1. Roi xuyen san / Mat duong (Missing COL) @ Liberty City / New York (LC01) - Khu COL3
- Coords: X=14794.77, Y=8013.17, Z=-20.23 (Heading=122.2°, Interior=0)
- Pre-Fall Edge: X=14810.28, Y=8026.06, Z=-20.23
- Nearest Object: tunl_2_bend.dff (ID 21157) in S&S/maps/lc/comn.ipl:106 [COL: LC_generics.col]
- Note: tunl_2_bend.dff (ID 21157) @ 7.9m | S&S/maps/lc/comn.ipl:106 | COL:LC_generics.col(130F/0B) [OK_COL]
```

---

### 🛠️ BUG-006: 1. Roi xuyen san / Mat duong (Missing COL) — Carcer City (CC06) - Khu CARCER
- **Thời điểm ghi nhận**: `2026-10-22 21:21:35`
- **Tọa độ hiện tại `(X, Y, Z)`**: `11092.782, 8207.602, 19.522` (Heading: `232.0°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `True`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, 0.000` (Phát hiện rơi tự do: `False`)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `11092.780, 8207.600, 20.170`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Vat the gan nhat: `dlkytree125` (ID `31917`) tai `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:693` (DFF trong `['S&S/Cdimages/keystone/GAME_KEY.img']`, COL `tree.col (13 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `11092.78` | `8207.60` | **`19.52`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `11092.78` | `8207.60` | **`19.52`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `11092.78` | `8207.60` | **`19.52`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `11092.78` | `8207.60` | **`19.52`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `11092.78` | `8207.60` | **`19.52`** | `0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `17.45m` (XY `15.0m`, dZ `+9.0m`) | `31917` | **`dlkytree125`** *(LOD)* | `kytrees` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:693` | `S&S/Cdimages/keystone/game_key.ide:1094` | `S&S/Cdimages/keystone/GAME_KEY.img` | `tree.col` (`COL3`, R=28.0m, **13F/0B/0S**) | ✅ OK |
| `26.39m` (XY `24.3m`, dZ `+10.4m`) | `150700` | **`clk_trees25`** *(LOD)* | `carcertrees` | `S&S/maps/cc/clark_gen.IPL:38` | `S&S/Cdimages/carcer/clark_gen.ide:39` | `S&S/Cdimages/carcer/game_cc.img` | `clarkveg.col` (`COL3`, R=144.5m, **0F/0B/0S**) | ✅ OK |
| `27.29m` (XY `27.2m`, dZ `+1.6m`) | `150877` | **`clk_grass25`** *(LOD)* | `clarkgen` | `S&S/maps/cc/clark_gen.IPL:208` | `S&S/Cdimages/carcer/clark_gen.ide:221` | `S&S/Cdimages/carcer/game_cc.img` | `southconnections.col` (`COL3`, R=149.3m, **177F/0B/0S**) | ✅ OK |
| `41.58m` (XY `41.6m`, dZ `+0.0m`) | `150806` | **`clk_road33`** *(LOD)* | `clarkgen` | `S&S/maps/cc/clark_gen.IPL:144` | `S&S/Cdimages/carcer/clark_gen.ide:147` | `S&S/Cdimages/carcer/game_cc.img` | `southconnections.col` (`COL3`, R=73.6m, **503F/0B/0S**) | ✅ OK |
| `72.52m` (XY `72.5m`, dZ `+1.4m`) | `31628` | **`kydl_road59`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:404` | `S&S/Cdimages/keystone/game_key.ide:805` | `S&S/Cdimages/keystone/GAME_KEY.img` | `dlkycol.col` (`COL3`, R=83.0m, **78F/0B/0S**) | ✅ OK |
| `72.60m` (XY `72.6m`, dZ `-0.5m`) | `150805` | **`clk_road34`** *(LOD)* | `clarkgen` | `S&S/maps/cc/clark_gen.IPL:143` | `S&S/Cdimages/carcer/clark_gen.ide:146` | `S&S/Cdimages/carcer/game_cc.img` | `southconnections.col` (`COL3`, R=88.0m, **713F/0B/0S**) | ✅ OK |
| `86.21m` (XY `85.4m`, dZ `+11.9m`) | `31918` | **`dlkytree126`** *(LOD)* | `kytrees` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:694` | `S&S/Cdimages/keystone/game_key.ide:1095` | `S&S/Cdimages/keystone/GAME_KEY.img` | `tree.col` (`COL3`, R=97.2m, **143F/0B/0S**) | ✅ OK |
| `116.26m` (XY `113.0m`, dZ `+27.2m`) | `31911` | **`dlkytree119`** *(LOD)* | `kytrees` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:687` | `S&S/Cdimages/keystone/game_key.ide:1088` | `S&S/Cdimages/keystone/GAME_KEY.img` | `tree.col` (`COL3`, R=119.0m, **0F/0B/0S**) | ✅ OK |
| `147.25m` (XY `143.8m`, dZ `+31.8m`) | `31562` | **`kydl_grass66`** *(LOD)* | `keystonew` | `S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:338` | `S&S/Cdimages/keystone/game_key.ide:739` | `S&S/Cdimages/keystone/GAME_KEY.img` | `dlkycol.col` (`COL3`, R=160.9m, **196F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-006] 1. Roi xuyen san / Mat duong (Missing COL) @ Carcer City (CC06) - Khu CARCER
- Coords: X=11092.78, Y=8207.60, Z=19.52 (Heading=232.0°, Interior=0)
- Velocity: vz=0.000
- Nearest Object: dlkytree125.dff (ID 31917) in S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:693 [COL: tree.col]
- Note: dlkytree125.dff (ID 31917) @ 17.4m | S&S/Cdimages/keystone/GAME_KEY.img::wkey_stream0.ipl:693 | COL:tree.col(13F/0B) [OK_COL]
```

---

### 🛠️ BUG-005: 1. Roi xuyen san / Mat duong (Missing COL) — Carcer City (CC06) - Khu CARCER
- **Thời điểm ghi nhận**: `2026-10-16 03:43:05`
- **Tọa độ hiện tại `(X, Y, Z)`**: `10587.380, 9900.291, 15.604` (Heading: `273.8°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `0.106, 0.007, -0.280` (Phát hiện rơi tự do: `True`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `10578.590, 9894.560, 20.700` (`2.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `10583.120, 9900.190, 21.350`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Vat the gan nhat: `cctjournotest` (ID `152523`) tai `S&S/maps/cc/lacElevels.IPL:166` (DFF trong `['S&S/Cdimages/carcer/game_cc.img']`, COL `jornochurch.col (556 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `10574.74` | `9873.72` | **`19.99`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `10577.07` | `9886.02` | **`19.99`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `10578.59` | `9894.56` | **`20.70`** | `-0.065` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `10582.29` | `9899.14` | **`20.09`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `10587.38` | `9900.29` | **`15.60`** | `-0.280` | `0` | ⚠️ Đang rơi / Không ổn định |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `8.70m` (XY `7.0m`, dZ `+5.2m`) | `152523` | **`cctjournotest`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:166` | `S&S/Cdimages/carcer/lacElevels.ide:164` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=68.4m, **556F/0B/0S**) | ✅ OK |
| `11.91m` (XY `11.9m`, dZ `+0.6m`) | `152529` | **`cctjourno-grnd`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:172` | `S&S/Cdimages/carcer/lacElevels.ide:170` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=137.7m, **2730F/0B/0S**) | ✅ OK |
| `16.84m` (XY `11.3m`, dZ `+7.4m`) | `152506` | **`cctjourno_js-hata`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:149` | `S&S/Cdimages/carcer/lacElevels.ide:147` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=23.8m, **2747F/0B/0S**) | ✅ OK |
| `34.72m` (XY `32.9m`, dZ `+6.1m`) | `152511` | **`jou_wires`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:154` | `S&S/Cdimages/carcer/lacElevels.ide:152` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=75.7m, **0F/0B/0S**) | ✅ OK |
| `41.72m` (XY `34.4m`, dZ `+18.6m`) | `152518` | **`jou_builds01`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:161` | `S&S/Cdimages/carcer/lacElevels.ide:159` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=36.6m, **1458F/0B/0S**) | ✅ OK |
| `62.01m` (XY `62.0m`, dZ `-0.8m`) | `152516` | **`jou_ground02`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:159` | `S&S/Cdimages/carcer/lacElevels.ide:157` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=59.7m, **1751F/0B/0S**) | ✅ OK |
| `80.16m` (XY `80.1m`, dZ `-1.5m`) | `152528` | **`cctestroad001`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:170` | `S&S/Cdimages/carcer/lacElevels.ide:169` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=96.7m, **452F/0B/0S**) | ✅ OK |
| `85.61m` (XY `85.6m`, dZ `-1.0m`) | `152217` | **`lacE_manholes1`** *(LOD)* | `dwntbuild` | `S&S/maps/cc/lacE.IPL:759` | `S&S/Cdimages/carcer/lacE.ide:746` | `S&S/Cdimages/carcer/game_cc.img` | `dwtnbuild.col` (`COL3`, R=141.2m, **640F/0B/0S**) | ✅ OK |
| `88.17m` (XY `85.4m`, dZ `+21.9m`) | `152359` | **`Cc_nitelite26`** *(LOD)* | `txnitelites` | `S&S/maps/cc/lacE.IPL:903` | `S&S/Cdimages/carcer/lacE.ide:902` | `S&S/Cdimages/carcer/game_cc.img` | `cc_nitelites.col` (`COL3`, R=149.5m, **380F/0B/0S**) | ✅ OK |
| `101.37m` (XY `101.4m`, dZ `-1.4m`) | `151485` | **`lacE_grass08`** *(LOD)* | `lacEgrnd` | `S&S/maps/cc/lacE.IPL:16` | `S&S/Cdimages/carcer/lacE.ide:12` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=160.4m, **186F/0B/0S**) | ✅ OK |
| `102.68m` (XY `102.7m`, dZ `-1.3m`) | `152519` | **`jou_ground03`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:162` | `S&S/Cdimages/carcer/lacElevels.ide:160` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=108.1m, **62F/0B/0S**) | ✅ OK |
| `119.13m` (XY `114.4m`, dZ `+28.2m`) | `152358` | **`Cc_nitelite24`** *(LOD)* | `txnitelites` | `S&S/maps/cc/lacE.IPL:902` | `S&S/Cdimages/carcer/lacE.ide:901` | `S&S/Cdimages/carcer/game_cc.img` | `cc_nitelites.col` (`COL3`, R=130.3m, **318F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-005] 1. Roi xuyen san / Mat duong (Missing COL) @ Carcer City (CC06) - Khu CARCER
- Coords: X=10587.38, Y=9900.29, Z=15.60 (Heading=273.8°, Interior=0)
- Pre-Fall Edge: X=10578.59, Y=9894.56, Z=20.70
- Nearest Object: cctjournotest.dff (ID 152523) in S&S/maps/cc/lacElevels.IPL:166 [COL: jornochurch.col]
- Note: cctjournotest.dff (ID 152523) @ 8.7m | S&S/maps/cc/lacElevels.IPL:166 | COL:jornochurch.col(556F/0B) [OK_COL]
```

---

### 🛠️ BUG-004: 1. Roi xuyen san / Mat duong (Missing COL) — Carcer City (CC06) - Khu CARCER
- **Thời điểm ghi nhận**: `2026-10-16 03:42:42`
- **Tọa độ hiện tại `(X, Y, Z)`**: `10556.700, 9727.700, 991.964` (Heading: `359.0°`)
- **Interior / AreaCode**: `PedArea=7` | `GameCurrArea=7` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, -0.215` (Phát hiện rơi tự do: `True`)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `10574.010, 9805.640, 20.840`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Kiem tra ENEX `CC-cas` tai `S&S/Interior/ccn_enex.IPL:11` (Exit=(10556.7, 9727.7, 994.0), TargetInt=7): Neu buoc vao cua bi roi tu do, kiem tra xem file .IPL noi that cua Interior 7 da mount trong gta.dat chua hoac tang Z exit len +0.5m. | Model `wheel_o_fortune` (ID `1895`) đặt tại `CUSTOM/custom_mods.ipl:938` đang bị `EMPTY_COL_0_FACES`. Cần bổ sung/đóng gói lại `.col` cho `wheel_o_fortune` hoặc đặt tấm sàn collision ẩn dưới tọa độ `[10558.8, 9739.68, 995.43]`.

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `10572.83` | `9806.04` | **`20.20`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `10572.79` | `9806.31` | **`20.21`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `10573.33` | `9809.86` | **`20.30`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `10574.01` | `9805.64` | **`20.19`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `10556.70` | `9727.70` | **`991.96`** | `-0.215` | `7` | ⚠️ Đang rơi / Không ổn định |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `12.46m` (XY `6.7m`, dZ `+10.5m`) | `1978` | **`roulette_tbl`** | `kbroul1` | `CUSTOM/custom_mods.ipl:942` | `data/maps/interior/props.ide:280` | `S&S/Cdimages/default/Interiors.img` | `props.col` (`COL3`, R=2.7m, **0F/2B/0S**) | ✅ OK |
| `12.65m` (XY `12.2m`, dZ `+3.5m`) | `1895` | **`wheel_o_fortune`** | `kb_wheel1` | `CUSTOM/custom_mods.ipl:938` | `data/maps/interior/props.ide:197` | `S&S/Cdimages/default/Interiors.img` | `props.col` (`COL3`, R=1.0m, **0F/0B/0S**) | ⚠️ `EMPTY_COL_0_FACES` |
| `13.97m` (XY `9.2m`, dZ `+10.5m`) | `2188` | **`blck_jack`** | `kbblackjack` | `CUSTOM/custom_mods.ipl:941` | `data/maps/interior/props.ide:490` | `S&S/Cdimages/default/Interiors.img` | `props.col` (`COL3`, R=1.8m, **0F/2B/0S**) | ✅ OK |
| `17.85m` (XY `14.4m`, dZ `+10.5m`) | `1978` | **`roulette_tbl`** | `kbroul1` | `CUSTOM/custom_mods.ipl:943` | `data/maps/interior/props.ide:280` | `S&S/Cdimages/default/Interiors.img` | `props.col` (`COL3`, R=2.7m, **0F/2B/0S**) | ✅ OK |

#### 4. Các Cửa Ra/Vào Nội Thất (`ENEX`) Trong Bán Kính 25m
| Tên ENEX | Khoảng cách | Phía khớp | Tọa độ Vào `(x1, y1, z1)` | Tọa độ Đích `(x2, y2, z2)` | Target Interior | Nguồn `.IPL` |
|---|---|---|---|---|---|---|
| **`CC-cas`** | `0.00m` | `EXIT_DEST` | `[10573.9, 9805.7, 19.8]` | `[10556.7, 9727.7, 994.0]` | `7` | `S&S/Interior/ccn_enex.IPL:11` |
| **`CC-casi`** | `0.00m` | `ENTRANCE` | `[10556.7, 9727.7, 994.0]` | `[10573.9, 9805.7, 19.8]` | `0` | `S&S/Interior/ccn_enex.IPL:12` |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-004] 1. Roi xuyen san / Mat duong (Missing COL) @ Carcer City (CC06) - Khu CARCER
- Coords: X=10556.70, Y=9727.70, Z=991.96 (Heading=359.0°, Interior=7)
- Velocity: vz=-0.215
- Nearest Object: roulette_tbl.dff (ID 1978) in CUSTOM/custom_mods.ipl:942 [COL: props.col]
- Note: wheel_o_fortune.dff (ID 1895) @ 12.7m | CUSTOM/custom_mods.ipl:938 | COL:props.col(0F/0B) [EMPTY_COL_0_FACES]
```

---

### 🛠️ BUG-003: 1. Roi xuyen san / Mat duong (Missing COL) — Carcer City (CC06) - Khu CARCER
- **Thời điểm ghi nhận**: `2026-10-16 03:41:51`
- **Tọa độ hiện tại `(X, Y, Z)`**: `10582.830, 9899.603, 20.551` (Heading: `265.4°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, 0.000` (Phát hiện rơi tự do: `False`)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `10581.360, 9899.460, 20.760`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Vat the gan nhat: `CJ_Dumpster2` (ID `1344`) tai `S&S/maps/cc/lac_props2.IPL:96` (DFF trong `['S&S/Cdimages/default/Generic.img']`, COL `dynamic2.col (12 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `10578.74` | `9884.88` | **`20.13`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `10580.48` | `9898.43` | **`20.11`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `10582.08` | `9899.67` | **`20.10`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `10582.83` | `9899.60` | **`20.55`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `10582.83` | `9899.60` | **`20.55`** | `0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `14.53m` (XY `14.5m`, dZ `-0.4m`) | `1344` | **`CJ_Dumpster2`** | `CJ_BINS2` | `S&S/maps/cc/lac_props2.IPL:96` | `data/maps/generic/dynamic2.ide:19` | `S&S/Cdimages/default/Generic.img` | `dynamic2.col` (`COL3`, R=1.4m, **12F/0B/18S**) | ✅ OK |
| `12.43m` (XY `11.2m`, dZ `+5.3m`) | `152523` | **`cctjournotest`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:166` | `S&S/Cdimages/carcer/lacElevels.ide:164` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=68.4m, **556F/0B/0S**) | ✅ OK |
| `14.67m` (XY `14.7m`, dZ `+0.8m`) | `152529` | **`cctjourno-grnd`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:172` | `S&S/Cdimages/carcer/lacElevels.ide:170` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=137.7m, **2730F/0B/0S**) | ✅ OK |
| `17.58m` (XY `15.9m`, dZ `+7.5m`) | `152506` | **`cctjourno_js-hata`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:149` | `S&S/Cdimages/carcer/lacElevels.ide:147` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=23.8m, **2747F/0B/0S**) | ✅ OK |
| `35.88m` (XY `35.3m`, dZ `+6.3m`) | `152511` | **`jou_wires`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:154` | `S&S/Cdimages/carcer/lacElevels.ide:152` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=75.7m, **0F/0B/0S**) | ✅ OK |
| `42.06m` (XY `37.7m`, dZ `+18.7m`) | `152518` | **`jou_builds01`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:161` | `S&S/Cdimages/carcer/lacElevels.ide:159` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=36.6m, **1458F/0B/0S**) | ✅ OK |
| `83.72m` (XY `83.7m`, dZ `-1.3m`) | `152528` | **`cctestroad001`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:170` | `S&S/Cdimages/carcer/lacElevels.ide:169` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=96.7m, **452F/0B/0S**) | ✅ OK |
| `89.28m` (XY `89.3m`, dZ `-0.9m`) | `152217` | **`lacE_manholes1`** *(LOD)* | `dwntbuild` | `S&S/maps/cc/lacE.IPL:759` | `S&S/Cdimages/carcer/lacE.ide:746` | `S&S/Cdimages/carcer/game_cc.img` | `dwtnbuild.col` (`COL3`, R=141.2m, **640F/0B/0S**) | ✅ OK |
| `90.73m` (XY `88.0m`, dZ `+22.1m`) | `152359` | **`Cc_nitelite26`** *(LOD)* | `txnitelites` | `S&S/maps/cc/lacE.IPL:903` | `S&S/Cdimages/carcer/lacE.ide:902` | `S&S/Cdimages/carcer/game_cc.img` | `cc_nitelites.col` (`COL3`, R=149.5m, **380F/0B/0S**) | ✅ OK |
| `99.71m` (XY `99.7m`, dZ `-1.2m`) | `151485` | **`lacE_grass08`** *(LOD)* | `lacEgrnd` | `S&S/maps/cc/lacE.IPL:16` | `S&S/Cdimages/carcer/lacE.ide:12` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=160.4m, **186F/0B/0S**) | ✅ OK |
| `106.79m` (XY `106.8m`, dZ `-1.2m`) | `152519` | **`jou_ground03`** *(LOD)* | `journo` | `S&S/maps/cc/lacElevels.IPL:162` | `S&S/Cdimages/carcer/lacElevels.ide:160` | `S&S/Cdimages/carcer/game_cc.img` | `jornochurch.col` (`COL3`, R=108.1m, **62F/0B/0S**) | ✅ OK |
| `117.13m` (XY `113.6m`, dZ `+28.4m`) | `152358` | **`Cc_nitelite24`** *(LOD)* | `txnitelites` | `S&S/maps/cc/lacE.IPL:902` | `S&S/Cdimages/carcer/lacE.ide:901` | `S&S/Cdimages/carcer/game_cc.img` | `cc_nitelites.col` (`COL3`, R=130.3m, **318F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-003] 1. Roi xuyen san / Mat duong (Missing COL) @ Carcer City (CC06) - Khu CARCER
- Coords: X=10582.83, Y=9899.60, Z=20.55 (Heading=265.4°, Interior=0)
- Velocity: vz=0.000
- Nearest Object: CJ_Dumpster2.dff (ID 1344) in S&S/maps/cc/lac_props2.IPL:96 [COL: dynamic2.col]
- Note: CJ_Dumpster2.dff (ID 1344) @ 14.5m | S&S/maps/cc/lac_props2.IPL:96 | COL:dynamic2.col(12F/0B) [OK_COL]
```

---

### 🛠️ BUG-002: 1. Roi xuyen san / Mat duong (Missing COL) — Carcer City (CC06) - Khu CARCER
- **Thời điểm ghi nhận**: `2026-10-15 23:58:15`
- **Tọa độ hiện tại `(X, Y, Z)`**: `10794.840, 10255.070, 24.340` (Heading: `235.0°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, 0.000` (Phát hiện rơi tự do: `False`)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `10798.940, 10252.200, 23.990`

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Vat the gan nhat: `CJ_BLOCKER_BENCH` (ID `1368`) tai `S&S/maps/cc/lac_props.IPL:2757` (DFF trong `['S&S/Cdimages/default/Generic.img']`, COL `dynamic2.col (0 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `10798.94` | `10252.20` | **`23.34`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `10798.94` | `10252.20` | **`23.34`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `10798.94` | `10252.20` | **`23.34`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `10798.94` | `10252.20` | **`23.34`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-0.0s` | `10794.84` | `10255.07` | **`24.34`** | `0.000` | `0` | ✅ Đất liền an toàn |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `6.03m` (XY `4.2m`, dZ `-4.3m`) | `1368` | **`CJ_BLOCKER_BENCH`** | `CJ_BENCHES` | `S&S/maps/cc/lac_props.IPL:2757` | `data/maps/generic/dynamic2.ide:43` | `S&S/Cdimages/default/Generic.img` | `dynamic2.col` (`COL3`, R=1.8m, **0F/2B/0S**) | ✅ OK |
| `5.15m` (XY `4.5m`, dZ `-2.4m`) | `1232` | **`Streetlamp1`** | `dynsigns` | `S&S/maps/cc/lac_props.IPL:2718` | `data/maps/generic/dynamic.ide:27` | `S&S/Cdimages/default/Generic.img` | `dynamic.col` (`COL3`, R=2.9m, **0F/1B/3S**) | ✅ OK |
| `15.75m` (XY `15.7m`, dZ `-1.8m`) | `152090` | **`dwtn_fontn`** *(LOD)* | `dwntbuild` | `S&S/maps/cc/lacE.IPL:747` | `S&S/Cdimages/carcer/lacE.ide:620` | `S&S/Cdimages/carcer/game_cc.img` | `dwtnbuild.col` (`COL3`, R=15.4m, **342F/0B/0S**) | ✅ OK |
| `20.13m` (XY `19.4m`, dZ `-5.4m`) | `726` | **`tree_hipoly19`** *(LOD)* | `gtatreesh` | `S&S/maps/cc/lac_props.IPL:1835` | `data/maps/generic/vegepart.ide:106` | `S&S/Cdimages/default/Generic.img` | `vegepart.col` (`COL3`, R=18.9m, **0F/1B/0S**) | ✅ OK |
| `29.07m` (XY `28.6m`, dZ `-5.1m`) | `152221` | **`lacE_manholes8`** *(LOD)* | `dwntbuild` | `S&S/maps/cc/lacE.IPL:763` | `S&S/Cdimages/carcer/lacE.ide:750` | `S&S/Cdimages/carcer/game_cc.img` | `dwtnbuild.col` (`COL3`, R=95.8m, **10F/0B/0S**) | ✅ OK |
| `55.34m` (XY `55.1m`, dZ `-5.0m`) | `151500` | **`lacE_grass23`** *(LOD)* | `lacEgrnd` | `S&S/maps/cc/lacE.IPL:31` | `S&S/Cdimages/carcer/lacE.ide:27` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=50.8m, **18F/0B/0S**) | ✅ OK |
| `65.50m` (XY `65.5m`, dZ `-0.4m`) | `152247` | **`lacE_monorail14`** *(LOD)* | `dwntbuild` | `S&S/maps/cc/lacE.IPL:789` | `S&S/Cdimages/carcer/lacE.ide:776` | `S&S/Cdimages/carcer/game_cc.img` | `dwtnbuild.col` (`COL3`, R=76.2m, **4460F/0B/0S**) | ✅ OK |
| `70.90m` (XY `70.7m`, dZ `-5.0m`) | `151560` | **`lacE_conc05`** *(LOD)* | `lacEgrnd` | `S&S/maps/cc/lacE.IPL:91` | `S&S/Cdimages/carcer/lacE.ide:87` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=112.7m, **98F/0B/0S**) | ✅ OK |
| `71.50m` (XY `71.3m`, dZ `-4.8m`) | `151564` | **`lacE_conc09`** *(LOD)* | `lacEgrnd` | `S&S/maps/cc/lacE.IPL:95` | `S&S/Cdimages/carcer/lacE.ide:91` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=165.8m, **720F/0B/0S**) | ✅ OK |
| `85.06m` (XY `84.9m`, dZ `-5.0m`) | `151746` | **`dwtwn_road16`** *(LOD)* | `lacEroad` | `S&S/maps/cc/lacE.IPL:277` | `S&S/Cdimages/carcer/lacE.ide:273` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=94.7m, **1590F/0B/0S**) | ✅ OK |
| `86.48m` (XY `86.3m`, dZ `-5.1m`) | `151747` | **`dwtwn_road17`** *(LOD)* | `lacEroad` | `S&S/maps/cc/lacE.IPL:278` | `S&S/Cdimages/carcer/lacE.ide:274` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=115.8m, **2033F/0B/0S**) | ✅ OK |
| `89.09m` (XY `89.0m`, dZ `-5.0m`) | `151493` | **`lacE_grass16`** *(LOD)* | `lacEgrnd` | `S&S/maps/cc/lacE.IPL:24` | `S&S/Cdimages/carcer/lacE.ide:20` | `S&S/Cdimages/carcer/game_cc.img` | `lacEgrnd.col` (`COL3`, R=165.3m, **37F/0B/0S**) | ✅ OK |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-002] 1. Roi xuyen san / Mat duong (Missing COL) @ Carcer City (CC06) - Khu CARCER
- Coords: X=10794.84, Y=10255.07, Z=24.34 (Heading=235.0°, Interior=0)
- Velocity: vz=0.000
- Nearest Object: CJ_BLOCKER_BENCH.dff (ID 1368) in S&S/maps/cc/lac_props.IPL:2757 [COL: dynamic2.col]
- Note: CJ_BLOCKER_BENCH.dff (ID 1368) @ 6.0m | S&S/maps/cc/lac_props.IPL:2757 | COL:dynamic2.col(0F/2B) [OK_COL]
```

---

### 🛠️ BUG-001: 1. Roi xuyen san / Mat duong (Missing COL) — Los Santos (SA) (LA01) - Khu LA
- **Thời điểm ghi nhận**: `2026-10-15 02:44:13`
- **Tọa độ hiện tại `(X, Y, Z)`**: `1544.500, -1675.500, -6.400` (Heading: `90.0°`)
- **Interior / AreaCode**: `PedArea=0` | `GameCurrArea=0` | **Đang lái xe**: `False`
- **Vận tốc `(vx, vy, vz)`**: `0.000, 0.000, -0.450` (Phát hiện rơi tự do: `True`)
- **Tọa độ mép sàn trước khi rơi (Pre-Fall Edge)**: `1538.000, -1675.000, 13.550` (`5.0s` trước)
- **Điểm Cứu Hộ An Toàn (Safe Recall -3s)**: `1541.500, -1675.200, 14.200`
- **Ghi chú của người chơi**: Kiem thu tu dong Hang muc 1: Auto-Inspector + 5s Trail + Safe Recall Unstuck tai Pershing Square LSPD

#### 1. Gợi Ý Sửa Lỗi Tự Động (Agent Auto-Fix Hint)
> Kiem tra ENEX `POLICE1` tai `S&S/maps/sa/LA/LAn.ipl:175` (Exit=(1552.45, -1674.99, 15.33), TargetInt=0): Neu buoc vao cua bi roi tu do, kiem tra xem file .IPL noi that cua Interior 0 da mount trong gta.dat chua hoac tang Z exit len +0.5m. | Vat the gan nhat: `Roads14_LAn` (ID `4150`) tai `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:63` (DFF trong `['S&S/Cdimages/andreas/GAME_LA.img']`, COL `lan_2.col (62 faces)`).

#### 2. Lịch Sử Di Chuyển 5 Giây Trước Khi Bấm (`Position Trail Buffer`)
| Thời điểm | Tọa độ `X` | Tọa độ `Y` | Độ cao `Z` | Vận tốc `vz` | Interior | Trạng thái |
|---|---|---|---|---|---|---|
| `-5.0s` | `1538.00` | `-1675.00` | **`13.55`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-3.0s` | `1541.50` | `-1675.20` | **`13.55`** | `0.000` | `0` | ✅ Đất liền an toàn |
| `-2.0s` | `1543.00` | `-1675.40` | **`13.50`** | `-0.020` | `0` | ✅ Đất liền an toàn |
| `-1.0s` | `1544.50` | `-1675.50` | **`8.20`** | `-0.380` | `0` | ⚠️ Đang rơi / Không ổn định |
| `-0.0s` | `1544.50` | `-1675.50` | **`-6.40`** | `-0.450` | `0` | ⚠️ Đang rơi / Không ổn định |

#### 3. Các Vật Thể Map Trong Bán Kính 15m (`.IPL` / `.IDE` / `.IMG` / `.COL`)
| Khoảng cách | Model ID | Tên `.DFF` | `.TXD` | File `.IPL` gốc | File `.IDE` gốc | Archive `.IMG` chứa DFF | Trạng thái `.COL` (Faces/Boxes) | Chẩn đoán |
|---|---|---|---|---|---|---|---|---|
| `14.08m` (XY `14.0m`, dZ `-1.1m`) | `4150` | **`Roads14_LAn`** | `lanroad` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:63` | `data/maps/LA/LAn.ide:177` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=60.5m, **62F/0B/0S**) | ✅ OK |
| `29.46m` (XY `23.9m`, dZ `-2.7m`) | `4032` | **`carimp_LAn`** | `lanpolicecp` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:56` | `data/maps/LA/LAn.ide:59` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=52.7m, **314F/5B/0S**) | ✅ OK |
| `29.46m` (XY `23.9m`, dZ `-2.7m`) | `4232` | **`carimp2_LAn`** | `lanpolicecp` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:57` | `data/maps/LA/LAn.ide:248` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=45.3m, **185F/4B/0S**) | ✅ OK |
| `39.16m` (XY `34.0m`, dZ `-0.5m`) | `3975` | **`PoliceSt01_LAn`** | `lanbloke` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:74` | `data/maps/LA/LAn.ide:2` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=94.3m, **210F/19B/0S**) | ✅ OK |
| `40.24m` (XY `27.1m`, dZ `+22.1m`) | `3976` | **`PoliceSt02_LAn`** | `lanbloke` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:75` | `data/maps/LA/LAn.ide:3` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=66.6m, **22F/58B/1S**) | ✅ OK |
| `66.93m` (XY `58.7m`, dZ `+16.7m`) | `4230` | **`billbrdlan_08`** | `billbrd01_lan` | `S&S/maps/sa/LA/LAn.ipl:157` | `data/maps/LA/LAn.ide:246` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=117.1m, **10F/0B/0S**) | ✅ OK |
| `85.15m` (XY `78.8m`, dZ `+12.4m`) | `3991` | **`GSFreeway7_LAn`** | `lanroad` | `S&S/maps/sa/LA/LAn.ipl:3` | `data/maps/LA/LAn.ide:18` | `S&S/Cdimages/andreas/GAME_LA.img` | `lan_2.col` (`COL3`, R=76.2m, **122F/0B/0S**) | ✅ OK |
| `13.85m` (XY `13.8m`, dZ `+0.6m`) | `1229` | **`bussign1`** | `signs` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:59` | `data/maps/generic/dynamic.ide:24` | `S&S/Cdimages/default/Generic.img` | `dynamic.col` (`COL3`, R=1.6m, **0F/2B/1S**) | ✅ OK |
| `15.15m` (XY `14.9m`, dZ `+2.9m`) | `1226` | **`lamppost3`** | `dynsigns` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:61` | `data/maps/generic/dynamic.ide:21` | `S&S/Cdimages/default/Generic.img` | `dynamic.col` (`COL3`, R=4.6m, **0F/1B/4S**) | ✅ OK |
| `17.99m` (XY `11.5m`, dZ `+1.6m`) | `1536` | **`Gen_doorEXT15`** | `ext_doors2` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:58` | `data/maps/generic/dynamic2.ide:211` | `S&S/Cdimages/default/Generic.img` | `dynamic2.col` (`COL3`, R=1.5m, **0F/1B/2S**) | ✅ OK |
| `18.13m` (XY `11.5m`, dZ `+1.6m`) | `1536` | **`Gen_doorEXT15`** | `ext_doors2` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:54` | `data/maps/generic/dynamic2.ide:211` | `S&S/Cdimages/default/Generic.img` | `dynamic2.col` (`COL3`, R=1.5m, **0F/1B/2S**) | ✅ OK |
| `8.07m` (XY `3.5m`, dZ `+0.5m`) | `646` | **`veg_palmkb14`** | `gta_potplants` | `S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:62` | `data/maps/generic/vegepart.ide:33` | `S&S/Cdimages/default/Generic.img` | `vegepart.col` (`COL3`, R=1.8m, **0F/0B/1S**) | ✅ OK |

#### 4. Các Cửa Ra/Vào Nội Thất (`ENEX`) Trong Bán Kính 25m
| Tên ENEX | Khoảng cách | Phía khớp | Tọa độ Vào `(x1, y1, z1)` | Tọa độ Đích `(x2, y2, z2)` | Target Interior | Nguồn `.IPL` |
|---|---|---|---|---|---|---|
| **`POLICE1`** | `7.97m` | `EXIT_DEST` | `[1554.95, -1674.99, 15.33]` | `[1552.45, -1674.99, 15.33]` | `0` | `S&S/maps/sa/LA/LAn.ipl:175` |
| **`K_LSPD`** | `22.43m` | `ENTRANCE` | `[1565.0, -1684.6, 27.4]` | `[1565.0, -1686.6, 27.4]` | `0` | `CUSTOM/EHI.IPL:1156` |

#### 5. Mẫu Báo Bug Ngắn Gọn (Copy Gửi Discord Project Eagle)
```text
[BUG-001] 1. Roi xuyen san / Mat duong (Missing COL) @ Los Santos (SA) (LA01) - Khu LA
- Coords: X=1544.50, Y=-1675.50, Z=-6.40 (Heading=90.0°, Interior=0)
- Pre-Fall Edge: X=1538.00, Y=-1675.00, Z=13.55
- Nearest Object: Roads14_LAn.dff (ID 4150) in S&S/Cdimages/andreas/GAME_LA.img::lan_stream1.ipl:63 [COL: lan_2.col]
- Note: Kiem thu tu dong Hang muc 1: Auto-Inspector + 5s Trail + Safe Recall Unstuck tai Pershing Square LSPD
```

---
