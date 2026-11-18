# M4 Mondstadt Round-3 Overhaul & 8 Authentic Genshin Interiors — Handover & Verification Report (2026-11-17)

- **Date:** 2026-11-17
- **Agent:** Antigravity (`58ec5ee3-3fb5-4cba-becc-912ab6e8f1c4`)
- **Work-Item:** [2026-11-17-fix-m4-mondstadt-round3-and-interiors.md](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/work-items/2026-11-17-fix-m4-mondstadt-round3-and-interiors.md)
- **Staging & Rollback Root:** `D:\GTA Archive\Staging\fix-m4-round3-20261117\`
- **Target Runtime:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

---

## 1. Summary of Round-3 Fixes & Architectural Upgrades

### 1.1 Zero-Decimation Mondstadt City Mesh & Collision (`mondstadt_m0_city.{ide,ipl,col,img}`)
- **Root Cause Eliminated:**
  - Removed all architectural `DECIMATE (COLLAPSE, ratio=0.026..0.16)` passes on the 70 structural/building/stair/fountain/windmill/stall objects from `蒙德城.blend` (`1,281,337` near triangles preserved at `float32` precision, `0` vertex grid quantization).
  - Removed the `+0.018m` upward nudge on horizontal stone/stair triangles (`V[horiz_pave, :, 2] += 0.018`) that previously ripped stair treads away from vertical risers; instead depressed only overlapping `Stages_Grass_Plane_01_T4` corners by `-0.025m`.
  - Restoring undecimated `Area_MdBuild_Column01` eliminated the **2 floating stone caps** at the Knights of Favonius HQ stair foot (`0` floating bricks remain; both carved balustrade pedestals sit solidly on the `Z = 32.40m` plaza).
- **Multi-Chunk ID Layout (`101` models / `101` instances):**
  - Primary Near (`6710..6719`, `draw_dist = 295.0`) at IPL lines `0..9` -> paired 1-to-1 to full-district silhouette LODs (`6720..6729`, `draw_dist = 1500.0`) at IPL lines `10..19`.
  - Overflow near visual (`mv0_*`) & static collision (`mc0_*`) chunks at IPL lines `20..100` (`lod = -1`): IDs `12390..12470` (`81` IDs).
  - Watertight `COL3` archive (`358,284` faces, max chunk `82,824 B < 92,768 B`) embedded inside `mondstadt_m0_city.img`.

### 1.2 Exact Doorways & Behind-Gate Chest Relocation (`mondstadt_m1_wilds.ipl`)
- **Building #2 Main-Street Tavern Doorway (`MD_TAI` — Screenshot 1 Red Arrow):**
  - Moved yellow `ENEX` cone from Building #1 (`-4218.75, -3041.55, 8.48`) to Building #2's front doorway beneath the green tavern sign & red awning at the top of the first stairs:
    - Cone: `(-4238.220, -3035.890, 12.481)`
    - Step-out exit: `(-4237.050, -3033.600, 12.473, hdg = 333.0)`
    - Synced `Margaret` (`-4238.50, -3031.90, 12.48, hdg = 210.0`), `Diona` `outdoor_gps`, radar blip `48`, and GG Map POI `[Mondstadt INT-05]`.
- **Mona's Astrological House Doorway (`MD_MON` — South Mondstadt):**
  - Added paired `ENEX` `"MD_MON"` right on the arched wooden doorway of Mona's sealed house in South Mondstadt:
    - Cone: `(-4224.379, -3069.129, 6.718)`
    - Step-out exit: `(-4225.065, -3067.039, 6.374, hdg = 18.2)`
    - Placed `Mona` beside her front porch steps at `(-4221.60, -3065.20, 6.374, hdg = 18.0)` (`4.81m` clear of cone) and added GG Map POI `[Mondstadt INT-08] Nha Chiem Tinh Mona (M0)`.
- **Main Gate Exquisite Chest (`CHEST_02`, Model `6692`):**
  - Relocated in-place (preserving 100% of M1 IPL LOD indices `148..206`) from the middle of the Main Gate road `(-4193.50, -3048.50, 6.41)` onto the grassy flowerbed lawn behind the North gate wall at `(-4192.80, -3033.80, 6.374, hdg = 180.0)`.

### 1.3 All 8 Authentic Genshin Impact 3D Interiors (`INT-01..INT-08`)
All procedural/kitbashed interiors were replaced with human-scale-calibrated (`1.0x / 0.95x / 0.92x / 0.46x`), zero-decimated RenderWare `.dff` + dedicated mipmapped `BC1_UNORM` `.txd` + watertight walkable `COL3` chunks (`max_col3 = 69,804 B`):

| Tag | IDs (`Primary` + `Sub-Parts`) | Dedicated TXD | Source `.blend` | Highlights & Indoor NPCs |
|---|---|---|---|---|
| `MD_WIN` | `6696` + `12551..12553` | `int_winery.txd` | `晨曦酒庄.blend` | Authentic Dawn Winery manor hall, chandelier, rugs, walkable 1F + grand staircase + 2F gallery. |
| `MD_ANG` | `6697` + `12554..12556` | `int_angels.txd` | `天使的馈赠.blend` | Authentic Angel's Share tavern bar, stools, wine barrels, hearth & 2F balcony. |
| `MD_CAT` | `6698` + `12557..12564` | `int_cathed.txd` | `西风大教堂-白天 2.93.blend` | Authentic Favonius Grand Cathedral (`0.46x` human-calibrated pews, gothic nave, glowing stained glass). |
| `MD_KNI` | `6699` + `12565` | `int_knights.txd` | `团长办公室.blend` | Acting Grand Master Office (`Jean` at `-3949.55, -3498.45, 1500.05`; `Lisa` at `-3951.84, -3501.95, 1500.05`). |
| `MD_TAI` | `6700` + `12566` | `int_catstail.txd` | `七圣召唤3.3Ver.blend` | Authentic Cat's Tail TCG Lounge (`Diona` at `-4851.65, -3197.85, 1500.07`). |
| `MD_ALC` | `6701` + `12567..12583` | `int_alchemy.txd` | `水仙十字结社.blend` + `MSR` | Arcane Study Rotunda with rose astrolabe clockwork, bookcases, Crafting Bench & Alchemic Devices. |
| `MD_MON` | `12550` + `12584..12592` | `int_mona.txd` | `星纬殿堂.blend` (`0.46x` + study props) | **Mona's Astrological House**: intimate starry hydromancy astrolabe sanctum with tall overflowing bookshelves, scholar desks & candelabras. |
| `MD_ABY` | `12150` + `12593..12603` | `int_abyss.txd` | `星纬殿堂.blend` (`1.00x`) | Colossal Celestial Spiral Abyss Arena at Musk Reef (`mondstadt_m2_east`). |

### 1.4 Connected City Pedestrian Network (`paths.img`) & Active Multi-Waypoint Strollers (`MondstadtLifeAndBlips.cs`)
- Solved an 18-route 3D `COL3` A* pedestrian footpath graph (`162` connected `FLA4` `PedNodes` with `flags_base = 0x000F1000` across `nodes1754.dat` + `nodes1818.dat` + `8` bridge sidewalk nodes in `nodes1753.dat`) from Stone Bridge -> Main Gate -> Mona's House / Lower Market -> Building #2 Cat's Tail -> Fountain Plaza -> Angel's Share Alley -> Central Stairs -> Mid Terrace -> Knights HQ -> South Windmill -> Barbatos Statue Plaza -> Favonius Cathedral.
- Upgraded `MondstadtLifeAndBlips.cs` (`41,571 B`) with **14 active multi-waypoint ping-pong city strollers** (`0->1->2->3->2->1->0` via `05D3`) plus `16` lively shopkeepers/guards (`0` duplicate Kaeya/HuTao/Joker skins).

### 1.5 Continuous Dvalin Overhead Flight (`MondstadtDvalinFlight.cs`)
- Re-centered Dvalin's 60 FPS articulated 5-model figure-8 orbit directly above Mondstadt City at `(-4310.0, -2995.0, Z = 106.0 + 11.0*sin(2*theta))` (`rx = 142m`, `ry = 108m`) so 3D distance from every plaza stays `< 294m < 299m` draw distance, and kept `6812` + `6703..6706` pinned in streaming memory while inside Mondstadt.

---

## 2. Round-4 Addendum — Universal `COL3` `TBounds` Sector & Frustum-Culling Fix (`2026-11-17`)

- **Work-Item:** [2026-11-17-fix-m4-round4-frustum-culling-tbounds.md](file:///c:/Users/LENOVO/Desktop/GTA/docs/project-eagle/work-items/2026-11-17-fix-m4-round4-frustum-culling-tbounds.md)
- **Staging & Rollback Root:** `D:\GTA Archive\Staging\fix-m4-round4-culling-20261117\`
- **Root Cause & Fix:**
  - In GTA San Andreas, `CWorld::Add` (`50m x 50m` sector registration) and `CRenderer::SetupEntityVisibility` (`0x554230` frustum culling) read `m_pColModel->m_boundBox` and `m_pColModel->m_boundSphere` from the 40-byte `COL3` `TBounds` header (`offset 32..71`) rather than `.DFF` vertices.
  - Across Round-3 archives, `197` visual models (`69` in `mondstadt_m0_city`, `79` in `mondstadt_m1_wilds`, `49` in `mondstadt_m2_east`) had `.DFF` vertices extending outside their `COL3` `TBounds` (e.g., `mv0_6717_01` at Fountain Plaza and `mv0_6711_01`/`mv0_6711_02` at Lower Plaza stairs carried unrelated `28m` `col_batches` `80–90m` SW, causing floors/stairs/walls to vanish when rotating the camera away from the SW quadrant, while `6719` foliage, `6720..6729` LODs, `int_angels_p4`, and Dvalin wings `6703..6706` carried `R = 0.2..1.5m` dummy bounds).
  - **Fix Applied (`0` `.DFF`-outside-`COL3` `TBounds` mismatches across all `M0`, `M1`, `M2` models; `0.000m` collision drift):**
    1. Spun off all `48` `COL3` batches on `mv0_*` visual chunks in `mondstadt_m0_city` onto dedicated `mc0_sp_01..48` collision helpers (`12471..12518`, within reserved `12390..12549`) using exact `int16 * 128` midpoint shifts (`0.0000m` world collision drift), upgraded `mv0_*` `draw_dist` from `260.0 -> 299.0m`, and gave every `mv0_*`, `6719`, and `6720..6729` a tight `.DFF`-enclosing `COL3` `TBounds` (`+1.5m` margin).
    2. Patched `COL3` `TBounds` across `100%` of `mondstadt_m0_city.col`, `mondstadt_m1_wilds.col` (including all 7 M1 interiors, Dvalin wings `6703..6706`, and 36 terrain tiles), and `mondstadt_m2_east.col` (`12150 int_spiral_abys` + sub-parts + 30 terrain tiles) to strictly enclose `UNION(DFF_verts, COL_verts) + 1.5m`, and re-embedded all three `.col` files into their matching `.img` archives.

---

## 3. Layered Rollback Commands (Newest First)

```powershell
# Layer 1 (Newest): Round-4 Culling Fix
python -X utf8 "D:\GTA Archive\Staging\fix-m4-round4-culling-20261117\rollback_m4_round4_culling.py" --preflight
python -X utf8 "D:\GTA Archive\Staging\fix-m4-round4-culling-20261117\rollback_m4_round4_culling.py" --apply

# Layer 2: Round-3 Zero-Decimation M0 + 8 Authentic Interiors
python -X utf8 "D:\GTA Archive\Staging\fix-m4-round3-20261117\rollback_m4_round3.py" --preflight
python -X utf8 "D:\GTA Archive\Staging\fix-m4-round3-20261117\rollback_m4_round3.py" --apply
```
