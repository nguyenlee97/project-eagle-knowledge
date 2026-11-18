# Carcer City heavy-skin test candidates — 2026-10-21

This read-only survey pairs ten kept, optimization-enabled heavy skins with ten NPC slots whose Carcer City relevance is supported by the current Project Eagle configuration. The game and source libraries were not modified by this survey. Catalog, review, and NPC API observations were captured on 2026-10-21; see the JSON companion for complete paths, source URLs, per-file hashes, population groups, and API provenance.

## Heavy skin set

Selection filters: `optimize=true`, `excluded=false`, no catalog policy hold, both source files present, and ten distinct displayed characters. Ranked by original DFF+TXD bytes descending, while favoring reliably parsed pairs; all selected effective ratings are not “love.” Total source size is **512,178,971 bytes (488.45 MiB)**. **7/10** are catalog-warning-free.

| Rank | ID | Character | Total bytes | MiB | DFF bytes | TXD bytes | Review | Catalog warning |
|---:|---:|---|---:|---:|---:|---:|---|---|
| 1 | 2050 | Ikuyo Kita | 94,844,002 | 90.45 | 1,939,654 | 92,904,348 | — | missing_material_textures |
| 2 | 105 | Ororon | 52,736,711 | 50.29 | 2,404,639 | 50,332,072 | slight | None |
| 3 | 148 | Kinich | 52,651,955 | 50.21 | 2,319,883 | 50,332,072 | like | None |
| 4 | 1235 | ellen | 52,463,463 | 50.03 | 2,131,391 | 50,332,072 | — | None |
| 5 | 1533 | Koleda | 52,193,546 | 49.78 | 1,861,474 | 50,332,072 | — | missing_material_textures |
| 6 | 1718 | Noa | 51,941,467 | 49.54 | 1,609,395 | 50,332,072 | — | None |
| 7 | 533 | Narita Brian | 47,575,240 | 45.37 | 4,582,944 | 42,992,296 | — | None |
| 8 | 1064 | Castorice | 37,138,418 | 35.42 | 3,910,386 | 33,228,032 | like | None |
| 9 | 133 | Fuuka Yamagishi | 35,615,787 | 33.97 | 990,103 | 34,625,684 | like | None |
| 10 | 745 | Cyrene | 35,018,382 | 33.4 | 4,880,554 | 30,137,828 | like | pairing_by_texture_names_match |

IDs **2050 Ikuyo Kita** and **1533 Koleda** have `missing_material_textures`; ID **745 Cyrene** has `pairing_by_texture_names_match`. Inspect those three if optimization/build output shows a mismatch. The other seven candidate pairs are warning-free. Full distinct hashes are recorded in JSON; selected source TXD SHA-256 values are unique.

## Carcer City NPC slots

The selected set is 3 service models plus 7 ordinary street models. `peds.ide` line numbers are one-based. Street counts are the number of matching CC population-group lines and total appearances within those groups; they describe configuration-list frequency, **not spawn probability**.

| ID | Model | `peds.ide` line | Role | Carcer evidence | CC groups / appearances | `pedgrp_cc.dat` lines | Baseline TXD member |
|---:|---|---:|---|---|---:|---|---|
| 48523 | CC_CCPD1 | 866 | police-emergency | CC-labelled COP/emergency entry; no CC population selector | 0 / 0 | — | `CC_CCPD1.txd` |
| 48524 | CC_CCPD2 | 867 | police-emergency | CC-labelled COP/emergency entry; no CC population selector | 0 / 0 | — | `CC_CCPD2.txd` |
| 48578 | CC_SWAT | 921 | police-emergency | CC-labelled COP/emergency entry; no CC population selector | 0 / 0 | — | `CC_SWAT.txd` |
| 40 | HFYRI | 78 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 9 / 12 | 12, 13, 14, 16, 17, 18, 28, 29, 30 | `hfyri.txd` |
| 46 | HMYRI | 84 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 9 / 12 | 12, 13, 14, 16, 17, 18, 28, 29, 30 | `hmyri.txd` |
| 12 | BFYRI | 50 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 7 / 9 | 12, 14, 16, 18, 28, 30, 97 | `bfyri.txd` |
| 93 | WFYST | 131 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 7 / 9 | 16, 18, 32, 34, 36, 38, 97 | `wfyst.txd` |
| 60 | OMYST | 98 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 7 / 9 | 16, 17, 18, 32, 34, 36, 38 | `omyst.txd` |
| 147 | WMYBU | 186 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 8 / 8 | 12, 13, 14, 28, 29, 30, 91, 93 | `wmybu.txd` |
| 91 | WFYRI | 129 | ordinary-civilian | Carcer City region tag + direct membership in data/pedgrp_cc.dat | 7 / 8 | 12, 14, 16, 18, 28, 30, 97 | `wfyri.txd` |

The street IDs have explicit Carcer City region tags and direct membership in `data/pedgrp_cc.dat`. Their matching group lines are listed above; the JSON lists each exact group name and per-group occurrence count. Some models are also configured in other regions.

### Practical test trigger

- **Street models:** enter Carcer City and let ambient populations stream. The metadata does not resolve an exact zone, spawn chance, or live appearance.
- **CC_CCPD1, CC_CCPD2, CC_SWAT:** raise the wanted level in Carcer City and observe whether these exact models are dispatched. This is a practical trigger, not proof that the dispatch mapping selects these slots.

The service models are defined as `COP` with `PED_TYPE_EMG` in `peds.ide` and have active DFF/TXD assets. However, the indexed NPC data has no `pedgrp_cc.dat` membership or selected `variation.dat` selector for them; their `regionTags` are empty. Their Carcer label is supported by the `CC_` model definitions, but regional service dispatch remains unverified. Active alternatives in the API snapshot are `48525 CC_CCPD3` (line 868), `48526 CC_CCPD4` (869), `48527 CC_CCPD5` (870), `48528 CC_CCPD6` (871), and `49213 CC_CCSWAT2` (1556), under the same dispatch caveat.

## TXD collision check

For the ten selected target slots, the pre-test active TXD member basenames and SHA-256 hashes were unique. There are no duplicate target TXD names or identical TXD payloads among these ten slots, so they do not form a shared-TXD replacement group that must be avoided. This is a narrow audit of the ten chosen destinations, not a claim that no aliases exist elsewhere in the game.

| Target | Baseline TXD member | Bytes | Baseline SHA-256 |
|---|---|---:|---|
| 48523 CC_CCPD1 | `CC_CCPD1.txd` | 87,768 | `49698c899c7b3ac1f5d657bc0f74e95ba3300bae8219a881cb3dcdfc784966c6` |
| 48524 CC_CCPD2 | `CC_CCPD2.txd` | 87,768 | `25eac932efcfc84ff4b648a6381eb90edf7e3b0e1f16f5bdb035e308aef23e61` |
| 48578 CC_SWAT | `CC_SWAT.txd` | 87,768 | `81f75b18a927a767daddebef1b3efc3bfb6c100c1eeb19d83db144a9d9e27386` |
| 40 HFYRI | `hfyri.txd` | 164,136 | `dae94d43de02c00c27b5821a1351da24ac596d0984f8668c4f38a991c102a271` |
| 46 HMYRI | `hmyri.txd` | 164,136 | `5b946ae3648bdc25ca090869b8d757eec51b45f64c8945f87a31ef5f6737cf98` |
| 12 BFYRI | `bfyri.txd` | 164,136 | `e121c12fd0621a2db7dca6beec189c16d41368f231fa5d9949a2628f77a14378` |
| 93 WFYST | `wfyst.txd` | 147,752 | `810461f7910bab00013f00af6a650af4656454d144bad8ab61839a55fb7dd080` |
| 60 OMYST | `omyst.txd` | 131,240 | `39b1de9647d1bcc7dac9125e2cd770a8e9da73c3ee9d685f28eef8c8684781b0` |
| 147 WMYBU | `wmybu.txd` | 131,240 | `6eb85835285b0a58ed20aacf06605d5dafb8eee0a1a2763234adffbd2bc3444d` |
| 91 WFYRI | `wfyri.txd` | 164,136 | `38943068cf7e2874ae7635c8a3ec2e427c44eee436443f693aec75f5ed36f1ce` |

## Evidence and limitations

- Game root: `Project Eagle/gta sa clean/gta sa clean`.
- NPC evidence: `data/peds.ide`, `data/pedgrp_cc.dat`, `data/variation.dat`, active model members in `S&S/CDimages/default/COMPONENTPEDS.img`, and `/api/npcs`.
- Skin evidence: `/api/catalog`, `/api/reviews`, and SHA-256 hashes of the selected source files.
- `/api/npcs` reports 1,638 records and indexes current game definitions, active manifests, population group files, and `variation.dat`. API state times and full paths are in the JSON.
- No in-game dispatch, ambient appearance, deterministic direct-spawn command, or performance result was tested in this survey.

