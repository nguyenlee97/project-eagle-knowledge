# In-Game Forensic Snapshot & Camera X-Ray (`BUG-014-20261116-110623`)

- **Timestamp**: `2026-11-16 11:06:23` (`181 ms`)
- **Player Coords**: `(-4266.72, -3010.04, -0.93)` | Heading: `165.1°` | In Vehicle: `False`
- **Camera Eye & Ray**: Eye `(-0.00, 0.01, 0.00)` -> Front `(-0.395, 0.917, -0.059)` (Heading `23.3°`, Pitch `-3.4°`, FOV `-0.1°`)
- **Screenshot**: [`bug-snapshots/BUG-014-20261116-110623.png`](bug-snapshots/BUG-014-20261116-110623.png) (`1920x1080`, `1087.7 KB`, `BitBlt_ScreenDC`)

## 1. Primary Camera Crosshair Target (Look-At X-Ray)
- **Target**: **`cxreffencesld.dff`** (Model ID `3276`, TXD `country_breakable.txd`)
- **Type / Source**: `STATIC_IPL` — `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl`
- **Distance & Alignment**: `12.76m` away | Angle from crosshair: `17.0°` (Perp offset `1.49m`)
- **Live RAM State**: DFF Loaded=`False` | TXD Loaded=`False` | COL Loaded=`False` (`0F / 0B`, RefCount=`0`)

## 2. Top Entities in Camera View Cone
| # | Kind | Model ID | DFF / TXD | Dist | Angle | RAM DFF/TXD/COL | Source |
| :---: | :--- | :---: | :--- | :---: | :---: | :--- | :--- |
| 1 | `STATIC_IPL` | `3276` | `cxreffencesld` / `country_breakable` | `12.76m` | `17.0°` | `DFF:NO TXD:NO COL:0F/0B` | `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl` |
| 2 | `STATIC_IPL` | `3375` | `CE_dblbarn01` / `CE_farmxref` | `44.69m` | `13.7°` | `DFF:NO TXD:NO COL:0F/0B` | `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl` |
| 3 | `STATIC_IPL` | `3276` | `cxreffencesld` / `country_breakable` | `16.24m` | `37.4°` | `DFF:NO TXD:NO COL:0F/0B` | `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl` |
| 4 | `STATIC_IPL` | `3374` | `SW_haybreak02` / `CE_farmxref` | `103.55m` | `5.3°` | `DFF:NO TXD:NO COL:0F/0B` | `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl` |
| 5 | `STATIC_IPL` | `3374` | `SW_haybreak02` / `CE_farmxref` | `99.56m` | `6.0°` | `DFF:NO TXD:NO COL:0F/0B` | `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl` |
| 6 | `STATIC_IPL` | `12919` | `sw_tempbarn06` / `sw_farm1` | `41.97m` | `24.2°` | `DFF:NO TXD:NO COL:0F/0B` | `S&S/Cdimages/andreas/GAME_SA.img::countrye_stream5.ipl` |

## 3. Nearby Dynamic Pools (`80m` radius: `12` Peds, `0` Vehicles, `9` Objects)
- **PED** ID `253` (`id_253`) at `(-4336.85, -3024.08, 1.39)` — `71.56m`, RwObject=`0x4B88E350`, HP=`0.0`
- **PED** ID `171` (`id_171`) at `(-4218.5, -2970.5, 11.36)` — `63.56m`, RwObject=`0x4B88E010`, HP=`100.0`
- **PED** ID `49444` (`id_49444`) at `(-4244.65, -3008.15, 13.38)` — `26.37m`, RwObject=`0x70B1A750`, HP=`2000.0`
- **PED** ID `70` (`id_70`) at `(-4240.8, -3010.2, 13.38)` — `29.61m`, RwObject=`0x4B88DF10`, HP=`100.0`
- **PED** ID `193` (`id_193`) at `(-4239.0, -3020.0, 13.38)` — `32.75m`, RwObject=`0x4B88DF50`, HP=`100.0`
- **PED** ID `49438` (`id_49438`) at `(-4242.0, -3028.5, 13.38)` — `34.01m`, RwObject=`0x58A19B80`, HP=`2000.0`
