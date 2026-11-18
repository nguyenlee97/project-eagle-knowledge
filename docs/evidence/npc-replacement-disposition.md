# Project Eagle NPC replacement disposition

This is a read-only planning index over all 1,687 catalog IDs. It assigns no character names and changes no game files.

## Disposition totals

| Disposition | IDs |
|---|---:|
| `otherworld_later` | 325 |
| `preserve_player_or_protagonist` | 39 |
| `preserve_special_mission_slot` | 10 |
| `replace_candidate` | 403 |
| `verify_usage_first` | 910 |

Unique IDs in requested base + Carcer City + Vice City group-file union: **373**.
Unique IDs in group-file union + full PED-bearing variation-selector union + user-reported working triggers 280/285, after excluding protected player/special slots: **403**. Full IDs and selector source rows are in the JSON.

| Priority selector region | Source selector rows | Selector types | Unique IDs referenced | IDs outside that region's group file |
|---|---:|---|---:|---:|
| Carcer City | 0 | none | 0 | 0 |
| Los Santos | 11 | ARPED, CABPED, COPBKR, COPPED, COPPILOT, FBIPED, FFPED, MDCPED, NEWSPILOT, NEWSREPORT, SWPED | 14 | 11 |
| Vice City | 11 | ARPED, CABPED, COPBKR, COPPED, COPPILOT, FBIPED, FFPED, MDCPED, NEWSPILOT, NEWSREPORT, SWPED | 23 | 19 |


Asset index cross-check: **1676** records have both DFF and TXD matches in indexed active archives; **11** do not. This is archive-index evidence, not live streaming/rendering proof.

| Population-group file | Priority view | Raw unique names | Raw token occurrences (repeats included) | Matched IDs | Matched token occurrences | Unmatched token occurrences |
|---|---|---:|---:|---:|---:|---:|
| `data/pedgrp.dat` | base | 218 | 470 | 218 | 470 | 0 |
| `data/pedgrp_at.dat` | other/later | 198 | 396 | 188 | 376 | 20 |
| `data/pedgrp_bw.dat` | other/later | 188 | 308 | 188 | 308 | 0 |
| `data/pedgrp_cc.dat` | Carcer City | 226 | 477 | 226 | 477 | 0 |
| `data/pedgrp_cm.dat` | other/later | 198 | 396 | 188 | 376 | 20 |
| `data/pedgrp_lc.dat` | other/later | 195 | 465 | 195 | 465 | 0 |
| `data/pedgrp_mll.dat` | other/later | 181 | 358 | 181 | 358 | 0 |
| `data/pedgrp_vc.dat` | Vice City | 206 | 687 | 206 | 687 | 0 |

Replace-candidate roles (exclusive by catalog role; full variation selectors add IDs beyond the group union; IDs 280/285 also have user-reported runtime confirmation):
- `criminal-ambient`: 19
- `gang`: 89
- `ordinary-civilian`: 256
- `police-emergency`: 24
- `prostitute-ambient`: 15

Optional police/emergency-role references in the combined priority candidate union: **24**; explicit police/emergency-role IDs overall: **136**. Their IDs and source memberships are in the JSON.

## How to read this

`replace_candidate` means a model token appears in at least one requested population-group file, a full PED-bearing variation selector names the ID in a priority-region roster, or the user reports it working in runtime (lapd1 ID 280 and SWAT ID 285). `otherworld_later` means it appears only in non-priority population-group files. `verify_usage_first` means there is no priority-group or PED-bearing selector reference and no reported working runtime trigger; unresolved regional prefix/source-section leads still require verification. It does not mean mission-only or rare. Player/protagonist variants and special mission slots have separate preserved dispositions.

File-to-region labels are inferred from filenames: `pedgrp.dat` as base, `pedgrp_cc.dat` as Carcer City, and `pedgrp_vc.dat` as Vice City. The catalog says none of the eight group files is explicitly mounted by the selected `data/gta.dat`; live file selection and region attachment remain unverified. Static membership and repeated token counts are not runtime spawn proof or spawn probabilities.

The JSON retains each ID's role classification, metadata pedtype, source section/path/line/raw row, asset-status summary, all linked population-group rows across all eight files, complete PED-bearing selector rows, unresolved regional leads, and blank character-review fields for later assignment. Source token repetitions are informational counts only.

User-reported runtime evidence covers only LS police `lapd1` (ID 280) and SWAT (ID 285), without a full animation/function test. The separate installation-verification record shows army (ID 287) files installed and archive payload checks matching; it records no game launch and no runtime appearance verification. Army remains a narrow ARPED configuration candidate, not a runtime-confirmed trigger.

For the next user-review phase, start with the combined group/selectors set and the two user-reported working triggers (lapd1 ID 280 and swat ID 285), then group by ambient, gang, and police/emergency tags. Army ID 287 is a narrow configuration candidate through ARPED, with installation recorded but runtime unverified. Treat otherworld-later and unresolved regional-prefix/source-section leads as separate review queues. Do not assign favorites until the user supplies a character list.

Detailed per-ID evidence: `npc-replacement-disposition.json`.
