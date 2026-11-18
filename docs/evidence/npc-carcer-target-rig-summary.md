# Carcer City law-enforcement targets: rig results and selector gap

Ngày kiểm tra: 13/10/2026. Các candidate đã có (ReiAyanami2, hanekawa, senjo) được đối chiếu với toàn bộ model COP Carcer đang có trong `COMPONENTPEDS.img`. Đây là phép đọc archive và cấu hình; không launch game và không ghi vào game.

`data/peds.ide` định nghĩa sáu model COP `CC_CCPD1`–`CC_CCPD6` (IDs 48523–48528, dòng 866–871) và `CC_SWAT` (ID 48578, dòng 921). Catalog xác nhận các cặp DFF/TXD có trong `COMPONENTPEDS.img`. Không có model `CC_ARMY`.

| Defined Carcer model | ID | DFF/TXD bytes | Vertices / triangles | Source skeleton matches |
|---|---:|---:|---:|---|
| CC_CCPD1 | 48523 | 100,265 / 87,768 | 1,265 / 1,382 | ReiAyanami2, hanekawa, senjo |
| CC_CCPD2 | 48524 | 100,263 / 87,768 | 1,265 / 1,382 | ReiAyanami2, hanekawa, senjo |
| CC_CCPD3 | 48525 | 100,263 / 87,768 | 1,265 / 1,382 | ReiAyanami2, hanekawa, senjo |
| CC_CCPD4–6 | 48526–48528 | 94,070 / 87,768 each | 1,173 / 1,312 each | ReiAyanami2, hanekawa, senjo |
| CC_SWAT | 48578 | 96,763 / 87,768 | 1,227 / 1,306 | ReiAyanami2, hanekawa, senjo |

All listed targets match the three surveyed sources on 33-frame count, 32 bone IDs, numeric hierarchy, and nearest-parent bone mapping. The source candidates also pass static weight and texture-link checks. CC_CCPD2 and CC_CCPD3's original target DFFs have weight check warnings in the parser; this is a note about the existing baselines, not the source candidates.

**No Carcer replacements are staged.** `data/variation.dat` includes `CC` in its header but has no active `CC COPPED`, `CC SWPED`, or `CC ARPED` rows. `peds.ide` membership proves the models are defined; it does not prove wanted dispatch selects them. The catalog search found no other mapping that establishes such a dispatch. Until a real selector is identified, mapping a new skin to these IDs would risk replacing a Carcer cop that never appears during wanted play. There is no CC army model to map.

The existing `ready` set `lapd1/swat/army` remains a separate Los Santos/mainland provisional set. No `ready-carcer` directory was created.

Detailed evidence, including exact member hashes, skeleton contracts and the zero-selector check: [npc-carcer-target-rig-audit.json](npc-carcer-target-rig-audit.json). Read-only script: [inspect_carcer_targets.py](../../../staging/project-eagle/law-enforcement/inspect_carcer_targets.py).
