# Project Eagle current skin resource census

Current mounted manifests resolve to **61 unique IMG archives** and 1687 actor rows (1687 unique IDs). The inventory reads the current IMG indexes and payload bytes; it does not use old archive offsets.

## Scope and method

- Game root: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`
- Reads active `IDE` and `IMG` lines from `data/default.dat` and `data/gta.dat`, then current VER2 indexes.
- MiB uses 1,048,576 bytes. IMG allocation is sectors × 2,048 and includes alignment padding. RenderWare payload is declared root chunk length plus its 12-byte header. Current Eagle originals have no known RAR source byte length.
- Duplicate basename candidates are preserved and individually parsed. No Mod Loader precedence is inferred. Aggregate pair totals include only unambiguous single DFF/TXD pairs.
- Geometry material slots come from chunk 8 material-list struct declarations, including reused slots; chunk 7 material definitions are counted separately.
- This is static evidence only. Parse failures remain unknown; no FPS/runtime, appearance, or rig-fit claim follows from these counts.

## Actor and role counts

- Actor rows: 1687; unique IDs: 1687; regular declared rows excluding ID 0 and 10 mission-special IDs: 1676 (includes player-coded actors); ambient-role subset: 1638.
- Role classes: {"criminal-ambient": 31, "gang": 324, "mission-special": 10, "ordinary-civilian": 1105, "player-coded-model": 38, "player-placeholder": 1, "police-emergency": 136, "prostitute-ambient": 42}
- Master list replacement candidates: 403; favorite-slot candidates: 64.
- Region memberships: {"vice_city": 225, "carcer_city": 226, "los_santos": 180}; these lists overlap.

## Current pair summary (unambiguous pairs only)

- Parsed unique pairs: 1676; pair payload total 332.89 MiB, allocated 336.24 MiB.
- Payload byte stats DFF/TXD/pair: {'count': 1676, 'min': 51734, 'median': 92439.0, 'max': 502091, 'mean': 102584.73}; {'count': 1676, 'min': 3496, 'median': 32936.0, 'max': 5145896, 'mean': 105683.33}; {'count': 1676, 'min': 58046, 'median': 153778.5, 'max': 5355260, 'mean': 208268.06}.
- Triangle bands: {'≤5k': 1676}; pair payload bands: {'≤0.5 MiB': 1656, '4–8 MiB': 6, '2–4 MiB': 3, '0.5–1 MiB': 11}.
- Total TXD textures among unique parsed TXD payloads: 4019; formats: {'DXT1': 3565, 'uncompressed-32': 407, 'DXT3': 30, 'DXT5': 15, 'DXT4': 2}.
- Material slots: 4491; unique material definitions: 4491.

## Heaviest 20 unambiguous pairs

| ID | Model | Pair MiB | Triangles | Vertices | Stored mips MiB |
|---:|---|---:|---:|---:|---:|
| 48048 | VCS_CS_RENOP | 5.11 | 2038 | 3080 | 4.91 |
| 48111 | VCS_MENDEZ2 | 4.90 | 2034 | 2950 | 4.70 |
| 48110 | VCS_MENDEZ1 | 4.89 | 1936 | 2781 | 4.70 |
| 48046 | VCS_CS_PED1 | 4.83 | 1926 | 2812 | 4.64 |
| 48043 | VCS_CS_LOUISE3 | 4.54 | 1954 | 3019 | 4.34 |
| 48041 | VCS_CS_FORBES | 4.40 | 2004 | 3098 | 4.20 |
| 48049 | VCS_CS_TROY | 3.88 | 1970 | 2924 | 3.69 |
| 48047 | VCS_CS_PHCOLLINS2 | 3.45 | 2020 | 3062 | 3.25 |
| 48044 | VCS_CS_MAN1 | 2.84 | 1805 | 2500 | 2.67 |
| 48245 | LCS_SINDACCO03 | 0.73 | 1984 | 3180 | 0.53 |
| 48614 | BW_CH_JIMMY | 0.64 | 3831 | 2597 | 0.43 |
| 48647 | BW_J_BOB | 0.59 | 1382 | 1080 | 0.50 |
| 48439 | LC_CURLY | 0.56 | 4248 | 5999 | 0.18 |
| 48682 | BW_POORWOMAN | 0.54 | 1540 | 1362 | 0.44 |
| 49265 | LC_MARIA | 0.54 | 4680 | 6170 | 0.13 |
| 49104 | MH2_SCARECROW | 0.53 | 3408 | 8202 | 0.05 |
| 48518 | LC_TONY | 0.53 | 4060 | 5410 | 0.18 |
| 48663 | BW_N_BEATRICE | 0.51 | 2718 | 2365 | 0.33 |
| 48680 | BW_PNKBARBER | 0.50 | 1837 | 1736 | 0.38 |
| 48737 | BW_T_ZOEU | 0.50 | 2060 | 1615 | 0.38 |

## Highest triangle counts (unambiguous pairs)

| ID | Model | Triangles | Pair MiB |
|---:|---|---:|---:|
| 49265 | LC_MARIA | 4680 | 0.54 |
| 48439 | LC_CURLY | 4248 | 0.56 |
| 48518 | LC_TONY | 4060 | 0.53 |
| 48614 | BW_CH_JIMMY | 3831 | 0.64 |
| 48475 | LC_KENJI | 3829 | 0.46 |
| 48421 | LC_CAT | 3799 | 0.41 |
| 287 | army | 3696 | 0.36 |
| 48495 | LC_OJG2 | 3644 | 0.32 |
| 48889 | ul_cop | 3628 | 0.37 |
| 49160 | UL_POLICE | 3628 | 0.42 |
| 285 | swat | 3622 | 0.36 |
| 48506 | LC_SALVATORE | 3588 | 0.48 |
| 48490 | LC_MISTY | 3523 | 0.37 |
| 48482 | LC_LOVE2 | 3486 | 0.36 |
| 49104 | MH2_SCARECROW | 3408 | 0.53 |
| 48503 | LC_RAY | 3367 | 0.43 |
| 48489 | LC_MIGUEL | 3354 | 0.36 |
| 48494 | LC_OJG_P | 3346 | 0.37 |
| 48472 | LC_JOEY | 3316 | 0.36 |
| 48488 | LC_MICKY | 3293 | 0.36 |

## All current COMPONENTPEDS pairs

- 2110 complete pairs parsed; 434 complete pairs have DFF basenames not named by active peds.ide. They remain an unclassified supplemental resource cohort.
- Pair payload total 419.07 MiB; allocation 423.4 MiB. Payload bands: {'≤0.5 MiB': 2083, '0.5–1 MiB': 18, '4–8 MiB': 6, '2–4 MiB': 3}; triangle bands: {'≤5k': 2110}.

Direct-name checks flagged 8 actor pair combinations for verification; masks are excluded from required texture names. Nonzero allocation tails occur in 15 DFF and 2 TXD actor candidates. These are review flags, not broken/safe classifications.

## Largest current individual members

| Member | Archive | Payload MiB | Allocation MiB |
|---|---|---:|---:|
| VCS_CS_RENOP.txd | COMPONENTPEDS.img | 4.91 | 4.91 |
| VCS_MENDEZ1.txd | COMPONENTPEDS.img | 4.70 | 4.71 |
| VCS_MENDEZ2.txd | COMPONENTPEDS.img | 4.70 | 4.71 |
| VCS_CS_PED1.txd | COMPONENTPEDS.img | 4.64 | 4.64 |
| VCS_CS_LOUISE3.txd | COMPONENTPEDS.img | 4.34 | 4.35 |
| VCS_CS_FORBES.txd | COMPONENTPEDS.img | 4.20 | 4.21 |
| VCS_CS_TROY.txd | COMPONENTPEDS.img | 3.69 | 3.69 |
| VCS_CS_PHCOLLINS2.txd | COMPONENTPEDS.img | 3.25 | 3.25 |
| VCS_CS_MAN1.txd | COMPONENTPEDS.img | 2.67 | 2.67 |
| LCS_SINDACCO03.txd | COMPONENTPEDS.img | 0.53 | 0.53 |
| mp_f1drivera.txd | COMPONENTPEDS.img | 0.50 | 0.50 |
| mp_f1driverb.txd | COMPONENTPEDS.img | 0.50 | 0.50 |
| mp_f1driverc.txd | COMPONENTPEDS.img | 0.50 | 0.50 |
| mp_f1driverd.txd | COMPONENTPEDS.img | 0.50 | 0.50 |
| BW_J_BOB.txd | COMPONENTPEDS.img | 0.50 | 0.50 |
| MH2_SCARECROW.dff | COMPONENTPEDS.img | 0.48 | 0.48 |
| cm_scarecrow.dff | COMPONENTPEDS.img | 0.48 | 0.48 |
| BW_POORWOMAN.txd | COMPONENTPEDS.img | 0.44 | 0.44 |
| BW_CH_JIMMY.txd | COMPONENTPEDS.img | 0.43 | 0.43 |
| LC_MARIA.dff | COMPONENTPEDS.img | 0.40 | 0.40 |

## Largest TXD texture mip chains

| Texture | TXD member | Dimensions | Format | Stored mip MiB |
|---|---|---:|---|---:|
| cs_forbes_head | VCS_CS_FORBES.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_forbes_jacket_back | VCS_CS_FORBES.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_forbes_jacket_front | VCS_CS_FORBES.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_louise_head_x | VCS_CS_LOUISE3.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_louise_limbs | VCS_CS_LOUISE3.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_louise_top | VCS_CS_LOUISE3.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_embracing_man_head | VCS_CS_MAN1.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_embracing_man_top | VCS_CS_MAN1.txd | 512x512 | uncompressed-32 | 1.00 |
| csped1_head | VCS_CS_PED1.txd | 512x512 | uncompressed-32 | 1.00 |
| csped1_jacket_back | VCS_CS_PED1.txd | 512x512 | uncompressed-32 | 1.00 |
| csped1_jacket_front | VCS_CS_PED1.txd | 512x512 | uncompressed-32 | 1.00 |
| csped1_shirt | VCS_CS_PED1.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_phcollins_jumper_back | VCS_CS_PHCOLLINS2.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_phcollins_jumper_front | VCS_CS_PHCOLLINS2.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_reniop_jacket_front | VCS_CS_RENOP.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_renop_head | VCS_CS_RENOP.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_renop_jacket_back | VCS_CS_RENOP.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_renop_trousers | VCS_CS_RENOP.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_troy_head | VCS_CS_TROY.txd | 512x512 | uncompressed-32 | 1.00 |
| cs_troy_t_shirt | VCS_CS_TROY.txd | 512x512 | uncompressed-32 | 1.00 |

## Aether loose pair

- 2,391,382 file bytes; 17,706 triangles, 15,487 vertices; 1,310,720 stored mip bytes. The DFF has 35,087 nonzero bytes after its declared root; see JSON for hashes and full texture metadata.

## Current pilot payloads in COMPONENTPEDS.img

- ID 280 `lapd1.dff`: 119618 payload bytes, 120832 allocated bytes, SHA-256 `bfcba19f3a3aa3a0d275dab4511993ec72dfed5cfde78973f707aa3661bd8c69`. 1601 triangles.
- ID 280 `lapd1.txd`: 16680 payload bytes, 18432 allocated bytes, SHA-256 `e5529523acf3f4bacacc1f065c0f2be8b69853220e61b1e5efbc6b099010f7bc`.
- ID 285 `swat.dff`: 241530 payload bytes, 241664 allocated bytes, SHA-256 `4616d87afa30c132b90b3c3d2609f6600687f71811bb695a7c86d91b38733b3c`. 3622 triangles.
- ID 285 `swat.txd`: 131240 payload bytes, 133120 allocated bytes, SHA-256 `7f6b31fea52e37de7860308c759b44930f030845aef61df7914970a534c8624c`.
- ID 287 `army.dff`: 246082 payload bytes, 247808 allocated bytes, SHA-256 `da7f391b79e93bae2d7b9b7792535f981e35164832bbd0442cca2e81c04be43d`. 3696 triangles.
- ID 287 `army.txd`: 131240 payload bytes, 133120 allocated bytes, SHA-256 `531287f4a52bb25d35edd055b5612dfc21070b322b400d53aee77bad9c269b8d`.

## Exact data

The complete per-ID rows, all current member candidates, per-asset hashes, texture names/dimensions/formats/mip sizes, DFF-to-TXD missing-name checks, distributions and unknowns are in `docs\project-eagle\evidence\eagle-current-skin-census.json`.
