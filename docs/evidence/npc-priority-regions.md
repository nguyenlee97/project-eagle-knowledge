# Project Eagle regional ped priority crosswalk

Read-only mapping for the requested road-trip regions. A regional group filename is candidate-association evidence; it does not prove runtime zone selection. Group list multiplicity is retained as source evidence and is not spawn probability.

Favorite-character candidates require membership in at least 2 of these 5 distinct broad civilian category labels: `CASUAL_AVERAGE`, `CASUAL_POOR`, `CASUAL_RICH`, `BUSINESS`, and `CLUBBERS`. Suffix variants such as `(SF)` and `(VEGAS)` do not add a category; repeated member tokens do not add breadth. Breadth 1 and 0 are other-character candidates. This is a static prioritization aid, not a frequency estimate.

Los Santos has a complete `pedgrp.dat` view and a focused view excluding explicit `(SF)` / `(VEGAS)` suffix rows only for `POPCYCLE_GROUP_*` civilian labels. VC and CC retain all rows without this filter.

## Vice City (VC)

Source association: `data/pedgrp_vc.dat`; legacy COPPED/SWPED/ARPED rows: 3; all ped-bearing selector rows: 11; selector-only IDs outside ambient groups: 19; unresolved source/prefix candidates: 242.

### Full File

Rows: 57; unique matched models: 206; memberships including repeats: 687; unmatched token occurrences: 0.

Top 10 civilian breadth candidates:

| ID | Model | Ped role | Animation | Voice | Favorite-group breadth | Group labels | Source |
|---:|---|---|---|---|---:|---|---|
| 48033 | `VCS_BMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYRI / VOICE_GEN_BMYRI | 5 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (SF); POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:376` |
| 48087 | `VCS_HFYBU` | CIVFEMALE / ordinary-civilian | busywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 4 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:430` |
| 48103 | `VCS_HMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_HMYRI / VOICE_GEN_HMYRI | 4 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (SF); POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:446` |
| 48282 | `VC_BMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 4 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (SF); POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS) | `DATA\PEDS.IDE:625` |
| 48310 | `VC_HFYBU` | CIVFEMALE / ordinary-civilian | busywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 4 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:653` |
| 48034 | `VCS_BMYST` | CIVMALE / ordinary-civilian | gang2 | VOICE_GEN_BMYST / VOICE_GEN_BMYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (SF); POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:377` |
| 48323 | `VC_HMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 3 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (SF); POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS) | `DATA\PEDS.IDE:666` |
| 48377 | `VC_WFYBU` | CIVFEMALE / ordinary-civilian | busywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 3 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS) | `DATA\PEDS.IDE:720` |
| 48384 | `VC_WFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 3 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS) | `DATA\PEDS.IDE:727` |
| 48389 | `VC_WMOBU` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | 3 | POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (SF); POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS) | `DATA\PEDS.IDE:732` |

Priority counts: `{"other_character_candidate": 177, "favorite_character_candidate": 29}`; favorite-group breadth counts (0–5): `{"0": 126, "1": 51, "2": 16, "3": 8, "4": 4, "5": 1}`.

### All ped-bearing role selectors

Includes the selected ped-bearing types from `variation.dat`; vehicle selector rows are excluded.

| Selector | Model IDs and names | Source |
|---|---|---|
| COPBKR | 48015 `VCS_BCOP` | `data/variation.dat:151` |
| COPPED | 48037 `VCS_COP`, 48289 `VC_COP` | `data/variation.dat:153` |
| COPPILOT | 48911 `vcpdh1` | `data/variation.dat:154` |
| NEWSPILOT | 49212 `VCNEWS` | `data/variation.dat:156` |
| NEWSREPORT | 48145 `VCS_WMYBU`, 48396 `VC_WMYBU` | `data/variation.dat:157` |
| SWPED | 48358 `VC_SWAT`, 48119 `VCS_SWAT` | `data/variation.dat:160` |
| FBIPED | 48055 `VCS_FBI`, 48297 `VC_FBI` | `data/variation.dat:162` |
| ARPED | 48014 `VCS_ARMY`, 48066 `VCS_GANG4A`, 48067 `VCS_GANG4B`, 48259 `VC_ARMY` | `data/variation.dat:165` |
| FFPED | 48298 `VC_FIREMEN` | `data/variation.dat:166` |
| MDCPED | 48332 `VC_MEDIC`, 48109 `VCS_MEDIC` | `data/variation.dat:168` |
| CABPED | 48097 `VCS_HMOCA`, 48139 `VCS_WMOCA`, 48317 `VC_HMOCA`, 48359 `VC_TAXI_D`, 48390 `VC_WMOCA` | `data/variation.dat:171` |

Selector-only IDs outside the full ambient list: 48015 `VCS_BCOP`, 48037 `VCS_COP`, 48055 `VCS_FBI`, 48066 `VCS_GANG4A`, 48067 `VCS_GANG4B`, 48097 `VCS_HMOCA`, 48109 `VCS_MEDIC`, 48119 `VCS_SWAT`, 48139 `VCS_WMOCA`, 48289 `VC_COP`, 48297 `VC_FBI`, 48298 `VC_FIREMEN`, 48317 `VC_HMOCA`, 48332 `VC_MEDIC`, 48358 `VC_SWAT`, 48359 `VC_TAXI_D`, 48390 `VC_WMOCA`, 48911 `vcpdh1`, 49212 `VCNEWS`.

### Unresolved defined-region candidates

These are IDE lexical/source-role leads without ambient membership in this regional file. Prefixes and section labels do not establish region assignment or mission rarity; verify before replacement.

| ID | Model | Ped role | Animation | Voice | IDE source and section | Candidate basis |
|---:|---|---|---|---|---|---|
| 48012 | `VCS_ALBERTO` | CIVMALE / ordinary-civilian | oldman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:355` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48013 | `VCS_ARMANDO` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:356` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48015 | `VCS_BCOP` | COP / police-emergency | swat | VOICE_EMG_MCOP1 / VOICE_EMG_MCOP6 | `DATA\PEDS.IDE:358` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48018 | `VCS_BFOST` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:361` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48019 | `VCS_BFOTR` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:362` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48024 | `VCS_BMOBE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:367` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48026 | `VCS_BMOST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMOST / VOICE_GEN_BMOST | `DATA\PEDS.IDE:369` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48028 | `VCS_BMYBB` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:371` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48029 | `VCS_BMYBE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:372` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48035 | `VCS_BURGER` | CIVMALE / ordinary-civilian | man | VOICE_GFD_WMYPIZZ / VOICE_GFD_WMYPIZZ | `DATA\PEDS.IDE:378` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48036 | `VCS_COKHED` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:379` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48037 | `VCS_COP` | COP / police-emergency | swat | VOICE_EMG_LAPD1 / VOICE_EMG_LAPD8 | `DATA\PEDS.IDE:380` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48038 | `VCS_CS_DASS1` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:381` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48039 | `VCS_CS_DASS2` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:382` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48040 | `VCS_CS_DIAZ` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:383` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48041 | `VCS_CS_FORBES` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:384` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48042 | `VCS_CS_JANET` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:385` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48043 | `VCS_CS_LOUISE3` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:386` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48044 | `VCS_CS_MAN1` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:387` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48045 | `VCS_CS_MARYJ` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:388` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48046 | `VCS_CS_PED1` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:389` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48047 | `VCS_CS_PHCOLLINS2` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:390` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48048 | `VCS_CS_RENOP` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:391` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48049 | `VCS_CS_TROY` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:392` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48050 | `VCS_CWMYHB2` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:393` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48051 | `VCS_DEA1` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:394` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48052 | `VCS_DEA2` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:395` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48053 | `VCS_DIAZ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:396` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48054 | `VCS_DIEGO` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:397` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48055 | `VCS_FBI` | COP / police-emergency | swat | VOICE_EMG_FBI2 / VOICE_EMG_FBI6 | `DATA\PEDS.IDE:398` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48056 | `VCS_FILMCRW` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:399` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48057 | `VCS_FIREMEN` | FIREMAN / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:400` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48060 | `VCS_GANG1C` | GANG3 / gang | gang2 | VOICE_GNG_VLA1 / VOICE_GNG_VLA2 | `DATA\PEDS.IDE:403` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48061 | `VCS_GANG1D` | GANG3 / gang | gang1 | VOICE_GNG_VLA3 / VOICE_GNG_VLA4 | `DATA\PEDS.IDE:404` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48066 | `VCS_GANG4A` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:409` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48067 | `VCS_GANG4B` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:410` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48068 | `VCS_GANG5A` | COP / police-emergency | swat | VOICE_EMG_MCOP1 / VOICE_EMG_MCOP2 | `DATA\PEDS.IDE:411` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48069 | `VCS_GANG5B` | COP / police-emergency | swat | VOICE_EMG_MCOP1 / VOICE_EMG_MCOP2 | `DATA\PEDS.IDE:412` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48078 | `VCS_GON_GOONA` | GANG3 / gang | gang2 | VOICE_GNG_VLA1 / VOICE_GNG_VLA2 | `DATA\PEDS.IDE:421` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48079 | `VCS_GON_GOONB` | GANG3 / gang | gang1 | VOICE_GNG_VLA3 / VOICE_GNG_VLA4 | `DATA\PEDS.IDE:422` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48080 | `VCS_GTR1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:423` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48081 | `VCS_GTR2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:424` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48082 | `VCS_HFOBE` | CIVFEMALE / ordinary-civilian | oldfatwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:425` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48084 | `VCS_HFOST` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_HFOST / VOICE_GEN_HFOST | `DATA\PEDS.IDE:427` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48086 | `VCS_HFYBE` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_HFYBE / VOICE_GEN_HFYBE | `DATA\PEDS.IDE:429` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48088 | `VCS_HFYCG` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:431` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48089 | `VCS_HFYMD` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:432` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48095 | `VCS_HITMAN` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:438` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48097 | `VCS_HMOCA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_VWMYCD / VOICE_GEN_VWMYCD | `DATA\PEDS.IDE:440` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48101 | `VCS_HMYAP` | CIVMALE / ordinary-civilian | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:444` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48102 | `VCS_HMYBE` | CIVMALE / ordinary-civilian | gang2 | VOICE_GEN_HMYBE / VOICE_GEN_HMYBE | `DATA\PEDS.IDE:445` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48105 | `VCS_JERRY` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:448` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48106 | `VCS_JFOTO` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:449` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48107 | `VCS_JMOTO` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:450` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48108 | `VCS_MALE01` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:451` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48109 | `VCS_MEDIC` | MEDIC / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:452` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48110 | `VCS_MENDEZ1` | GANG3 / gang | gang2 | VOICE_GNG_VLA1 / VOICE_GNG_VLA2 | `DATA\PEDS.IDE:453` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48111 | `VCS_MENDEZ2` | GANG3 / gang | gang1 | VOICE_GNG_VLA3 / VOICE_GNG_VLA4 | `DATA\PEDS.IDE:454` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48112 | `VCS_MENGGA` | GANG3 / gang | gang2 | VOICE_GNG_VLA1 / VOICE_GNG_VLA2 | `DATA\PEDS.IDE:455` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48113 | `VCS_MENGGB` | GANG3 / gang | gang1 | VOICE_GNG_VLA3 / VOICE_GNG_VLA4 | `DATA\PEDS.IDE:456` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48114 | `VCS_PHIL` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:457` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48115 | `VCS_PHILC1` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:458` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48116 | `VCS_ROBBER` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:459` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48117 | `VCS_SARGE` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:460` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48118 | `VCS_SHOPKPR` | CIVMALE / ordinary-civilian | man | VOICE_GFD_WMYAMMO / VOICE_GFD_WMYAMMO | `DATA\PEDS.IDE:461` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48119 | `VCS_SWAT` | COP / police-emergency | swat | VOICE_EMG_SWAT1 / VOICE_EMG_SWAT6 | `DATA\PEDS.IDE:462` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48120 | `VCS_VICE1` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:463` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48121 | `VCS_VICE2` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:464` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48123 | `VCS_WFOGO` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:466` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48126 | `VCS_WFOST` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_WFOST / VOICE_GEN_WFOST | `DATA\PEDS.IDE:469` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48127 | `VCS_WFOTR` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:470` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48128 | `VCS_WFYBE` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_WFYBE / VOICE_GEN_WFYBE | `DATA\PEDS.IDE:471` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48130 | `VCS_WFYJG` | CIVFEMALE / ordinary-civilian | jogwoman | VOICE_GEN_WFYJG / VOICE_GEN_WFYJG | `DATA\PEDS.IDE:473` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48132 | `VCS_WFYPR` | PROSTITUTE / prostitute-ambient | pro | VOICE_GEN_WFYPRO / VOICE_GEN_WFYPRO | `DATA\PEDS.IDE:475` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48139 | `VCS_WMOCA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:482` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48140 | `VCS_WMOGO` | CIVMALE / ordinary-civilian | oldman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:483` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48142 | `VCS_WMOST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMOST / VOICE_GEN_WMOST | `DATA\PEDS.IDE:485` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48143 | `VCS_WMOTR` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:486` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48147 | `VCS_WMYCW` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:490` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48148 | `VCS_WMYJG` | CIVMALE / ordinary-civilian | jogger | VOICE_GEN_WMYJG / VOICE_GEN_WMYJG | `DATA\PEDS.IDE:491` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48154 | `VCS_ZOMA` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:497` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48258 | `VC_APOULET` | CIVFEMALE / ordinary-civilian | oldfatwoman | VOICE_GEN_WFOST / VOICE_GEN_WFOST | `DATA\PEDS.IDE:601` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48260 | `VC_AVERY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMYTX1 / VOICE_GEN_WMYTX2 | `DATA\PEDS.IDE:603` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48263 | `VC_BFOST` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_BFOST / VOICE_GEN_BFOST | `DATA\PEDS.IDE:606` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48264 | `VC_BFOTR` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:607` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48269 | `VC_BGA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMYBOUN / VOICE_GEN_WMYBOUN | `DATA\PEDS.IDE:612` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48270 | `VC_BGB` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMYBOUN / VOICE_GEN_WMYBOUN | `DATA\PEDS.IDE:613` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48284 | `VC_BUDDY` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:627` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48285 | `VC_BURGER` | CIVMALE / ordinary-civilian | man | VOICE_GFD_WMYPIZZ / VOICE_GFD_WMYPIZZ | `DATA\PEDS.IDE:628` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48286 | `VC_C_WORKER` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:629` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48287 | `VC_CHEF` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:630` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48288 | `VC_COLONEL` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:631` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48289 | `VC_COP` | COP / police-emergency | swat | VOICE_EMG_LAPD1 / VOICE_EMG_LAPD8 | `DATA\PEDS.IDE:632` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48290 | `VC_CSDEAL` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:633` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48291 | `VC_CSPAPA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:634` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48297 | `VC_FBI` | COP / police-emergency | swat | VOICE_EMG_FBI2 / VOICE_EMG_FBI6 | `DATA\PEDS.IDE:640` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48298 | `VC_FIREMEN` | FIREMAN / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:641` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48299 | `VC_FSFA` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:642` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48304 | `VC_HAITIAN03` | GANG1 / gang | man | VOICE_GEN_SBMYST / VOICE_GEN_SBMYST | `DATA\PEDS.IDE:647` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48307 | `VC_HFOST` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:650` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48311 | `VC_HFYCG` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:654` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48312 | `VC_HFYMD` | CIVFEMALE / ordinary-civilian | busywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:655` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48313 | `VC_HFYPR` | PROSTITUTE / prostitute-ambient | pro | VOICE_GEN_SBFYPRO / VOICE_GEN_SBFYPRO | `DATA\PEDS.IDE:656` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48317 | `VC_HMOCA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:660` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48321 | `VC_HMYAP` | CIVMALE / ordinary-civilian | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:664` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48327 | `VC_KENTPAUL` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:670` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48328 | `VC_LAWYER` | GANG2 / gang | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:671` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48330 | `VC_MBA` | GANG4 / gang | gang1 | VOICE_GNG_VMAFF1 / VOICE_GNG_VMAFF2 | `DATA\PEDS.IDE:673` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48331 | `VC_MBB` | GANG4 / gang | gang2 | VOICE_GNG_VMAFF3 / VOICE_GNG_VMAFF4 | `DATA\PEDS.IDE:674` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48332 | `VC_MEDIC` | MEDIC / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:675` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48333 | `VC_PLAY10` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:676` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48334 | `VC_PLAY11` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:677` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48335 | `VC_PLAY12` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:678` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48336 | `VC_PLAYER` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:679` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48337 | `VC_PLAYER2` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:680` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48338 | `VC_PLAYER3` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:681` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48339 | `VC_PLAYER4` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:682` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48340 | `VC_PLAYER5` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:683` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48341 | `VC_PLAYER6` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:684` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48342 | `VC_PLAYER7` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:685` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48343 | `VC_PLAYER8` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:686` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48344 | `VC_PLAYER9` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:687` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48345 | `VC_PSYCHO` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:688` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48346 | `VC_S_KEEP` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:689` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48347 | `VC_SAM` | CIVMALE / ordinary-civilian | man | VOICE_GFD_WMYAMMO / VOICE_GFD_WMYAMMO | `DATA\PEDS.IDE:690` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48351 | `VC_SONNYGOONA` | GANG4 / gang | gang2 | VOICE_GNG_VMAFF1 / VOICE_GNG_VMAFF2 | `DATA\PEDS.IDE:694` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48352 | `VC_SONNYGOONB` | GANG4 / gang | gang1 | VOICE_GNG_VMAFF3 / VOICE_GNG_VMAFF4 | `DATA\PEDS.IDE:695` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48353 | `VC_SPANDXA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:696` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48354 | `VC_SPANDXB` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:697` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48355 | `VC_STRIPA` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:698` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48356 | `VC_STRIPB` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:699` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48357 | `VC_STRIPC` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:700` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48358 | `VC_SWAT` | COP / police-emergency | swat | VOICE_EMG_SWAT1 / VOICE_EMG_SWAT6 | `DATA\PEDS.IDE:701` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48359 | `VC_TAXI_D` | CIVMALE / ordinary-civilian | man | VOICE_GEN_VBMOCD / VOICE_GEN_VBMOCD | `DATA\PEDS.IDE:702` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48362 | `VC_VICE1` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:705` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48363 | `VC_VICE2` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:706` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48364 | `VC_VICE3` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:707` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48365 | `VC_VICE4` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:708` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48366 | `VC_VICE5` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:709` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48367 | `VC_VICE6` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:710` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48368 | `VC_VICE7` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:711` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48369 | `VC_VICE8` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:712` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48370 | `VC_WFOBE` | CIVFEMALE / ordinary-civilian | oldfatwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:713` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48371 | `VC_WFOGO` | CIVFEMALE / ordinary-civilian | oldwoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:714` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48373 | `VC_WFOSH` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:716` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48374 | `VC_WFOST` | CIVFEMALE / ordinary-civilian | oldfatwoman | VOICE_GEN_WFOST / VOICE_GEN_WFOST | `DATA\PEDS.IDE:717` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48375 | `VC_WFOTR` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:718` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48378 | `VC_WFYCST` | GANG2 / gang | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:721` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48383 | `VC_WFYPR` | PROSTITUTE / prostitute-ambient | pro | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:726` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48387 | `VC_WFYST` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:730` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48390 | `VC_WMOCA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_VBMOCD / VOICE_GEN_VBMOC | `DATA\PEDS.IDE:733` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48391 | `VC_WMOGO` | CIVMALE / ordinary-civilian | oldman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:734` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 48393 | `VC_WMOST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:736` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49282 | `VC_UMBERTO` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1625` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49283 | `VC_VICTOR` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1626` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49284 | `VC_ASS1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1627` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49285 | `VC_ASS2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1628` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49286 | `VC_ASS3` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1629` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49287 | `VC_BJ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1630` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49288 | `VC_CANDY` | PROSTITUTE / prostitute-ambient | pro | VOICE_GEN_HFYPRO / VOICE_GEN_HFYPRO | `DATA\PEDS.IDE:1631` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49289 | `VC_CGOON01` | GANG1 / gang | gang1 | VOICE_GNG_BALLAS1 / VOICE_GNG_BALLAS2 | `DATA\PEDS.IDE:1632` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49290 | `VC_CGOON02` | GANG1 / gang | gang2 | VOICE_GNG_BALLAS3 / VOICE_GNG_BALLAS4 | `DATA\PEDS.IDE:1633` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49291 | `VC_CGOON03` | GANG1 / gang | gang1 | VOICE_GNG_BALLAS5 / VOICE_GNG_BALLAS5 | `DATA\PEDS.IDE:1634` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49292 | `VC_COURIER` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1635` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49293 | `VC_DGOON2` | GANG2 / gang | gang2 | VOICE_GNG_VMAFF1 / VOICE_GNG_VMAFF2 | `DATA\PEDS.IDE:1636` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49294 | `VC_DIAZ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1637` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49295 | `VC_DICK` | CIVFEMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1638` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49296 | `VC_DIRECTOR` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1639` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49297 | `VC_DLOVE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1640` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49298 | `VC_DORIS` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1641` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49299 | `VC_DWAYNE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1642` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49300 | `VC_GONZALEZ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1643` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49301 | `VC_HILARY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1644` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49302 | `VC_HILARY2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1645` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49303 | `VC_JETHRO` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1646` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49304 | `VC_JEZZ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1647` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49305 | `VC_JUGGZ` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1648` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49306 | `VC_JZGIRL` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1649` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49307 | `VC_KELLY` | CIVFEMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1650` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49308 | `VC_KEN` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1651` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49309 | `VC_LANCE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1652` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49310 | `VC_LANCE2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1653` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49311 | `VC_LANCE3` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1654` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49312 | `VC_MAUDE` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1655` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49313 | `VC_MERCEDES` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1656` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49314 | `VC_MERCEDES2` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1657` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49315 | `VC_MGOONA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1658` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49316 | `VC_MIKE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1659` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49317 | `VC_MIKE2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1660` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49318 | `VC_MITCH` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1661` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49319 | `VC_PAPA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1662` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49320 | `VC_PERCY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1663` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49321 | `VC_PHIL` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1664` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49322 | `VC_PHIL2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1665` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49323 | `VC_PHIL3` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1666` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49324 | `VC_RICHARDS` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1667` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49325 | `VC_SERV` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1668` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49326 | `VC_SHRUB` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1669` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49327 | `VC_SHRUB2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1670` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49328 | `VC_SONNY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_MALE01 / VOICE_GEN_MALE01 | `DATA\PEDS.IDE:1671` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49368 | `VCS_BARRY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1711` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49369 | `VCS_CSPED1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1712` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49374 | `VCS_FORBES1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1717` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49375 | `VCS_FORBES2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1718` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49376 | `VCS_FORBES3` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1719` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49377 | `VCS_FRANK` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1720` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49378 | `VCS_GANG9A` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1721` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49379 | `VCS_GANG9B` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1722` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49380 | `VCS_GONZALEZ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1723` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49381 | `VCS_HANK` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1724` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49382 | `VCS_JANET` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1725` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49383 | `VCS_JAVIER` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1726` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49384 | `VCS_LANCE1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1727` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49385 | `VCS_LANCE2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1728` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49386 | `VCS_LOUISE1` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1729` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49387 | `VCS_LOUISE2` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1730` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49388 | `VCS_LOUISE3` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1731` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49389 | `VCS_LOUISE4` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1732` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49390 | `VCS_MARTY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1733` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49391 | `VCS_MARYJ` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1734` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49392 | `VCS_PHILC2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1735` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49393 | `VCS_PINATA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1736` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49394 | `VCS_RENI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1737` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49395 | `VCS_RENIOP` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1738` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49396 | `VCS_TROY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1739` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49397 | `VCS_UMBERTO` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1740` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49398 | `VCS_VIC1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1741` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49399 | `VCS_VIC10` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1742` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49400 | `VCS_VIC11` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1743` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49401 | `VCS_VIC12` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1744` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49402 | `VCS_VIC13` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1745` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49403 | `VCS_VIC14` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1746` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49404 | `VCS_VIC15` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1747` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49405 | `VCS_VIC2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1748` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49406 | `VCS_VIC3` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1749` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49407 | `VCS_VIC4` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1750` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49408 | `VCS_VIC5` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1751` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49409 | `VCS_VIC6` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1752` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49410 | `VCS_VIC7` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1753` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49411 | `VCS_VIC8` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1754` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49412 | `VCS_VIC9` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1755` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |
| 49413 | `VCS_WFOM` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1756` / no section label | model basename has VC_ or VCS_ prefix (lexical lead) |

## Carcer City (CC)

Source association: `data/pedgrp_cc.dat`; legacy COPPED/SWPED/ARPED rows: 0; all ped-bearing selector rows: 0; selector-only IDs outside ambient groups: 0; unresolved source/prefix candidates: 58.

### Full File

Rows: 57; unique matched models: 226; memberships including repeats: 477; unmatched token occurrences: 0.

Top 10 civilian breadth candidates:

| ID | Model | Ped role | Animation | Voice | Favorite-group breadth | Group labels | Source |
|---:|---|---|---|---|---:|---|---|
| 40 | `HFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_HFYRI / VOICE_GEN_HFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (SF); POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:78` |
| 46 | `HMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_HMYRI / VOICE_GEN_HMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (SF); POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:84` |
| 12 | `BFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_BFYRI / VOICE_GEN_BFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS); Wives | `DATA\PEDS.IDE:50` |
| 58 | `OMOST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_OMOST / VOICE_GEN_OMOST | 3 | Husbands; POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:96` |
| 60 | `OMYST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_OMYST / VOICE_GEN_OMYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:98` |
| 91 | `WFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_WFYRI / VOICE_GEN_WFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS); Wives | `DATA\PEDS.IDE:129` |
| 93 | `WFYST` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_WFYST / VOICE_GEN_WFYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS); Wives | `DATA\PEDS.IDE:131` |
| 20 | `BMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYRI / VOICE_GEN_BMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:58` |
| 22 | `BMYST` | CIVMALE / ordinary-civilian | gang2 | VOICE_GEN_BMYST / VOICE_GEN_BMYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:60` |
| 56 | `OFYST` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_OFYST / VOICE_GEN_OFYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:94` |

Priority counts: `{"other_character_candidate": 191, "favorite_character_candidate": 35}`; favorite-group breadth counts (0–5): `{"0": 142, "1": 49, "2": 13, "3": 22, "4": 0, "5": 0}`.

### All ped-bearing role selectors

Includes the selected ped-bearing types from `variation.dat`; vehicle selector rows are excluded.

| Selector | Model IDs and names | Source |
|---|---|---|
| None | No rows for this region in current `variation.dat` for the selected ped-bearing types | `data/variation.dat` |

Selector-only IDs outside the full ambient list: none.

### Unresolved defined-region candidates

These are IDE lexical/source-role leads without ambient membership in this regional file. Prefixes and section labels do not establish region assignment or mission rarity; verify before replacement.

| ID | Model | Ped role | Animation | Voice | IDE source and section | Candidate basis |
|---:|---|---|---|---|---|---|
| 48521 | `CC_BUNNY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:864` / no section label | model basename has CC_ prefix (lexical lead) |
| 48522 | `CC_CASH` | PLAYER1 / player-coded-model | player | VOICE_PLY_CR / VOICE_PLY_CR | `DATA\PEDS.IDE:865` / no section label | model basename has CC_ prefix (lexical lead) |
| 48523 | `CC_CCPD1` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:866` / no section label | model basename has CC_ prefix (lexical lead) |
| 48524 | `CC_CCPD2` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:867` / no section label | model basename has CC_ prefix (lexical lead) |
| 48525 | `CC_CCPD3` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:868` / no section label | model basename has CC_ prefix (lexical lead) |
| 48526 | `CC_CCPD4` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:869` / no section label | model basename has CC_ prefix (lexical lead) |
| 48527 | `CC_CCPD5` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:870` / no section label | model basename has CC_ prefix (lexical lead) |
| 48528 | `CC_CCPD6` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:871` / no section label | model basename has CC_ prefix (lexical lead) |
| 48533 | `CC_HOOD1` | GANG3 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:876` / no section label | model basename has CC_ prefix (lexical lead) |
| 48534 | `CC_HOOD2` | GANG3 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:877` / no section label | model basename has CC_ prefix (lexical lead) |
| 48535 | `CC_HOOD3` | GANG3 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:878` / no section label | model basename has CC_ prefix (lexical lead) |
| 48536 | `CC_HOOD4` | GANG3 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:879` / no section label | model basename has CC_ prefix (lexical lead) |
| 48537 | `CC_HOOD5` | GANG3 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:880` / no section label | model basename has CC_ prefix (lexical lead) |
| 48538 | `CC_HOOD6` | GANG3 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:881` / no section label | model basename has CC_ prefix (lexical lead) |
| 48539 | `CC_HOOD7` | GANG3 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:882` / no section label | model basename has CC_ prefix (lexical lead) |
| 48540 | `CC_HOOD8` | GANG3 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:883` / no section label | model basename has CC_ prefix (lexical lead) |
| 48541 | `CC_HOOD9` | GANG3 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:884` / no section label | model basename has CC_ prefix (lexical lead) |
| 48542 | `CC_HOSTAGE1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:885` / no section label | model basename has CC_ prefix (lexical lead) |
| 48543 | `CC_HOSTAGE2` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:886` / no section label | model basename has CC_ prefix (lexical lead) |
| 48544 | `CC_HOSTAGE3` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:887` / no section label | model basename has CC_ prefix (lexical lead) |
| 48545 | `CC_HOSTAGE4` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:888` / no section label | model basename has CC_ prefix (lexical lead) |
| 48546 | `CC_INOCENTZ1` | GANG4 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:889` / no section label | model basename has CC_ prefix (lexical lead) |
| 48547 | `CC_INOCENTZ2` | GANG4 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:890` / no section label | model basename has CC_ prefix (lexical lead) |
| 48548 | `CC_INOCENTZ3` | GANG4 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:891` / no section label | model basename has CC_ prefix (lexical lead) |
| 48549 | `CC_INOCENTZ4` | GANG4 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:892` / no section label | model basename has CC_ prefix (lexical lead) |
| 48550 | `CC_INOCENTZ5` | GANG4 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:893` / no section label | model basename has CC_ prefix (lexical lead) |
| 48551 | `CC_INOCENTZ6` | GANG4 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:894` / no section label | model basename has CC_ prefix (lexical lead) |
| 48552 | `CC_INOCENTZ7` | GANG4 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:895` / no section label | model basename has CC_ prefix (lexical lead) |
| 48553 | `CC_INOCENTZ8` | GANG4 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:896` / no section label | model basename has CC_ prefix (lexical lead) |
| 48554 | `CC_INOCENTZ9` | GANG4 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:897` / no section label | model basename has CC_ prefix (lexical lead) |
| 48555 | `CC_JOURNALIST` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:898` / no section label | model basename has CC_ prefix (lexical lead) |
| 48556 | `CC_MONKEY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:899` / no section label | model basename has CC_ prefix (lexical lead) |
| 48557 | `CC_PIGGSY` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:900` / no section label | model basename has CC_ prefix (lexical lead) |
| 48558 | `CC_RAMIREZ` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:901` / no section label | model basename has CC_ prefix (lexical lead) |
| 48559 | `CC_SKINZ1` | GANG5 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:902` / no section label | model basename has CC_ prefix (lexical lead) |
| 48560 | `CC_SKINZ2` | GANG5 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:903` / no section label | model basename has CC_ prefix (lexical lead) |
| 48561 | `CC_SKINZ3` | GANG5 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:904` / no section label | model basename has CC_ prefix (lexical lead) |
| 48562 | `CC_SKINZ4` | GANG5 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:905` / no section label | model basename has CC_ prefix (lexical lead) |
| 48563 | `CC_SKINZ5` | GANG5 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:906` / no section label | model basename has CC_ prefix (lexical lead) |
| 48564 | `CC_SKINZ6` | GANG5 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:907` / no section label | model basename has CC_ prefix (lexical lead) |
| 48565 | `CC_SKINZ7` | GANG5 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:908` / no section label | model basename has CC_ prefix (lexical lead) |
| 48566 | `CC_SKINZ8` | GANG5 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:909` / no section label | model basename has CC_ prefix (lexical lead) |
| 48567 | `CC_SKINZ9` | GANG5 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:910` / no section label | model basename has CC_ prefix (lexical lead) |
| 48577 | `CC_STARKWEATHER` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:920` / no section label | model basename has CC_ prefix (lexical lead) |
| 48578 | `CC_SWAT` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:921` / no section label | model basename has CC_ prefix (lexical lead) |
| 48579 | `CC_TRMP` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:922` / no section label | model basename has CC_ prefix (lexical lead) |
| 48580 | `CC_TRUMP` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:923` / no section label | model basename has CC_ prefix (lexical lead) |
| 48581 | `CC_WARDOG1` | GANG7 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:924` / no section label | model basename has CC_ prefix (lexical lead) |
| 48582 | `CC_WARDOG2` | GANG7 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:925` / no section label | model basename has CC_ prefix (lexical lead) |
| 48583 | `CC_WARDOG3` | GANG7 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:926` / no section label | model basename has CC_ prefix (lexical lead) |
| 48584 | `CC_WARDOG4` | GANG7 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:927` / no section label | model basename has CC_ prefix (lexical lead) |
| 48585 | `CC_WARDOG5` | GANG7 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:928` / no section label | model basename has CC_ prefix (lexical lead) |
| 48586 | `CC_WARDOG6` | GANG7 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:929` / no section label | model basename has CC_ prefix (lexical lead) |
| 48587 | `CC_WARDOG7` | GANG7 / gang | gang2 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:930` / no section label | model basename has CC_ prefix (lexical lead) |
| 48588 | `CC_WARDOG8` | GANG7 / gang | gang1 | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:931` / no section label | model basename has CC_ prefix (lexical lead) |
| 48589 | `CC_ZOMBIE` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:932` / no section label | model basename has CC_ prefix (lexical lead) |
| 49213 | `CC_CCSWAT2` | COP / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1556` / no section label | model basename has CC_ prefix (lexical lead) |
| 49330 | `CC_AMMUCLERK` | CIVMALE / ordinary-civilian | man | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:1673` / no section label | model basename has CC_ prefix (lexical lead) |

## Los Santos (LS)

Source association: `data/pedgrp.dat`; legacy COPPED/SWPED/ARPED rows: 3; all ped-bearing selector rows: 11; selector-only IDs outside ambient groups: 11; unresolved source/prefix candidates: 37.

### Full File

Rows: 57; unique matched models: 218; memberships including repeats: 470; unmatched token occurrences: 0.

Top 10 civilian breadth candidates:

| ID | Model | Ped role | Animation | Voice | Favorite-group breadth | Group labels | Source |
|---:|---|---|---|---|---:|---|---|
| 40 | `HFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_HFYRI / VOICE_GEN_HFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (SF); POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:78` |
| 46 | `HMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_HMYRI / VOICE_GEN_HMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (SF); POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (SF); POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:84` |
| 12 | `BFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_BFYRI / VOICE_GEN_BFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS); Wives | `DATA\PEDS.IDE:50` |
| 58 | `OMOST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_OMOST / VOICE_GEN_OMOST | 3 | Husbands; POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:96` |
| 60 | `OMYST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_OMYST / VOICE_GEN_OMYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (SF); POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:98` |
| 91 | `WFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_WFYRI / VOICE_GEN_WFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS); Wives | `DATA\PEDS.IDE:129` |
| 93 | `WFYST` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_WFYST / VOICE_GEN_WFYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS); Wives | `DATA\PEDS.IDE:131` |
| 20 | `BMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYRI / VOICE_GEN_BMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_BUSINESS (VEGAS); POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CASUAL_RICH (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:58` |
| 22 | `BMYST` | CIVMALE / ordinary-civilian | gang2 | VOICE_GEN_BMYST / VOICE_GEN_BMYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:60` |
| 56 | `OFYST` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_OFYST / VOICE_GEN_OFYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_AVERAGE (VEGAS); POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CASUAL_POOR (VEGAS); POPCYCLE_GROUP_CLUBBERS; POPCYCLE_GROUP_CLUBBERS (VEGAS) | `DATA\PEDS.IDE:94` |

Priority counts: `{"other_character_candidate": 183, "favorite_character_candidate": 35}`; favorite-group breadth counts (0–5): `{"0": 134, "1": 49, "2": 13, "3": 22, "4": 0, "5": 0}`.

### Focused Civilian Labels Excluding Sf Vegas

Rows: 39; unique matched models: 167; memberships including repeats: 256; unmatched token occurrences: 0.

Top 10 civilian breadth candidates:

| ID | Model | Ped role | Animation | Voice | Favorite-group breadth | Group labels | Source |
|---:|---|---|---|---|---:|---|---|
| 12 | `BFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_BFYRI / VOICE_GEN_BFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CLUBBERS; Wives | `DATA\PEDS.IDE:50` |
| 58 | `OMOST` | CIVMALE / ordinary-civilian | man | VOICE_GEN_OMOST / VOICE_GEN_OMOST | 3 | Husbands; POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:96` |
| 91 | `WFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_WFYRI / VOICE_GEN_WFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CLUBBERS; Wives | `DATA\PEDS.IDE:129` |
| 93 | `WFYST` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_WFYST / VOICE_GEN_WFYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CLUBBERS; Wives | `DATA\PEDS.IDE:131` |
| 20 | `BMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYRI / VOICE_GEN_BMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:58` |
| 22 | `BMYST` | CIVMALE / ordinary-civilian | gang2 | VOICE_GEN_BMYST / VOICE_GEN_BMYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:60` |
| 40 | `HFYRI` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_HFYRI / VOICE_GEN_HFYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:78` |
| 46 | `HMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_HMYRI / VOICE_GEN_HMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:84` |
| 56 | `OFYST` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_OFYST / VOICE_GEN_OFYST | 3 | POPCYCLE_GROUP_CASUAL_AVERAGE; POPCYCLE_GROUP_CASUAL_POOR; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:94` |
| 59 | `OMYRI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_OMYRI / VOICE_GEN_OMYRI | 3 | POPCYCLE_GROUP_BUSINESS; POPCYCLE_GROUP_CASUAL_RICH; POPCYCLE_GROUP_CLUBBERS | `DATA\PEDS.IDE:97` |

Priority counts: `{"other_character_candidate": 146, "favorite_character_candidate": 21}`; favorite-group breadth counts (0–5): `{"0": 122, "1": 24, "2": 8, "3": 13, "4": 0, "5": 0}`.

### All ped-bearing role selectors

Includes the selected ped-bearing types from `variation.dat`; vehicle selector rows are excluded.

| Selector | Model IDs and names | Source |
|---|---|---|
| COPBKR | 284 `lapdm1` | `data/variation.dat:55` |
| COPPED | 280 `lapd1` | `data/variation.dat:57` |
| COPPILOT | 280 `lapd1` | `data/variation.dat:58` |
| NEWSPILOT | 255 `WMYCH` | `data/variation.dat:60` |
| NEWSREPORT | 147 `WMYBU` | `data/variation.dat:61` |
| SWPED | 285 `swat` | `data/variation.dat:64` |
| FBIPED | 286 `fbi` | `data/variation.dat:66` |
| ARPED | 287 `army` | `data/variation.dat:69` |
| FFPED | 277 `lafd1` | `data/variation.dat:70` |
| MDCPED | 274 `laemt1` | `data/variation.dat:72` |
| CABPED | 182 `VBMOCD`, 220 `SBMOCD`, 234 `SWMOCD`, 261 `WMYCD1`, 262 `BMOCD` | `data/variation.dat:75` |

Selector-only IDs outside the full ambient list: 220 `SBMOCD`, 255 `WMYCH`, 261 `WMYCD1`, 262 `BMOCD`, 274 `laemt1`, 277 `lafd1`, 280 `lapd1`, 284 `lapdm1`, 285 `swat`, 286 `fbi`, 287 `army`.

### Unresolved defined-region candidates

These are IDE lexical/source-role leads without ambient membership in this regional file. Prefixes and section labels do not establish region assignment or mission rarity; verify before replacement.

| ID | Model | Ped role | Animation | Voice | IDE source and section | Candidate basis |
|---:|---|---|---|---|---|---|
| 11 | `VBFYCRP` | CIVFEMALE / ordinary-civilian | woman | VOICE_GEN_BFYCRP / VOICE_GEN_BFYCRP | `DATA\PEDS.IDE:49` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 23 | `WMYBMX` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMYBMX / VOICE_GEN_WMYBMX | `DATA\PEDS.IDE:61` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 49 | `OMOKUNG` | CIVMALE / ordinary-civilian | oldman | VOICE_GEN_OMOKUNG / VOICE_GEN_OMOKUNG | `DATA\PEDS.IDE:87` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 62 | `WMOPJ` | CIVMALE / ordinary-civilian | oldman | VOICE_GEN_WMOPJ / VOICE_GEN_WMOPJ | `DATA\PEDS.IDE:100` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 66 | `BMYPOL1` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYPOL1 / VOICE_GEN_BMYPOL1 | `DATA\PEDS.IDE:104` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 67 | `BMYPOL2` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYPOL2 / VOICE_GEN_BMYPOL2 | `DATA\PEDS.IDE:105` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 68 | `WMOPREA` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMOPREA / VOICE_GEN_WMOPREA | `DATA\PEDS.IDE:106` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 70 | `WMOSCI` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMOSCI / VOICE_GEN_WMOSCI | `DATA\PEDS.IDE:108` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 80 | `VBMYBOX` | CIVMALE / ordinary-civilian | man | VOICE_GEN_BMYBOX / VOICE_GEN_BMYBOX | `DATA\PEDS.IDE:118` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 81 | `VWMYBOX` | CIVMALE / ordinary-civilian | man | VOICE_GEN_WMYBOX / VOICE_GEN_WMYBOX | `DATA\PEDS.IDE:119` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 87 | `VWFYST1` | CIVFEMALE / ordinary-civilian | sexywoman | VOICE_GEN_VWFYST1 / VOICE_GEN_VWFYST1 | `DATA\PEDS.IDE:125` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 97 | `WMYLG` | CIVMALE / ordinary-civilian | jogger | VOICE_GEN_WMYLG / VOICE_GEN_WMYLG | `DATA\PEDS.IDE:135` / normal peds | IDE row has a source section label (general SA source-role lead) |
| 274 | `laemt1` | MEDIC / police-emergency | swat | VOICE_EMG_EMT1 / VOICE_EMG_EMT5 | `DATA\PEDS.IDE:312` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 275 | `lvemt1` | MEDIC / police-emergency | swat | VOICE_EMG_EMT1 / VOICE_EMG_EMT5 | `DATA\PEDS.IDE:313` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 276 | `sfemt1` | MEDIC / police-emergency | swat | VOICE_EMG_EMT1 / VOICE_EMG_EMT5 | `DATA\PEDS.IDE:314` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 277 | `lafd1` | FIREMAN / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:316` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 278 | `lvfd1` | FIREMAN / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:317` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 279 | `sffd1` | FIREMAN / police-emergency | swat | VOICE_GEN_NOVOICE / VOICE_GEN_NOVOICE | `DATA\PEDS.IDE:318` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 280 | `lapd1` | COP / police-emergency | swat | VOICE_EMG_LAPD1 / VOICE_EMG_LAPD8 | `DATA\PEDS.IDE:321` / cop peds | IDE row has a source section label (general SA source-role lead) |
| 281 | `sfpd1` | COP / police-emergency | swat | VOICE_EMG_SFPD1 / VOICE_EMG_SFPD5 | `DATA\PEDS.IDE:322` / cop peds | IDE row has a source section label (general SA source-role lead) |
| 282 | `lvpd1` | COP / police-emergency | swat | VOICE_EMG_LVPD1 / VOICE_EMG_LVPD5 | `DATA\PEDS.IDE:323` / cop peds | IDE row has a source section label (general SA source-role lead) |
| 283 | `csher` | COP / police-emergency | swat | VOICE_EMG_RCOP1 / VOICE_EMG_RCOP4 | `DATA\PEDS.IDE:324` / cop peds | IDE row has a source section label (general SA source-role lead) |
| 284 | `lapdm1` | COP / police-emergency | swat | VOICE_EMG_MCOP1 / VOICE_EMG_MCOP6 | `DATA\PEDS.IDE:325` / cop peds | IDE row has a source section label (general SA source-role lead) |
| 285 | `swat` | COP / police-emergency | swat | VOICE_EMG_SWAT1 / VOICE_EMG_SWAT6 | `DATA\PEDS.IDE:330` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 286 | `fbi` | COP / police-emergency | swat | VOICE_EMG_FBI2 / VOICE_EMG_FBI6 | `DATA\PEDS.IDE:331` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 287 | `army` | COP / police-emergency | swat | VOICE_EMG_ARMY1 / VOICE_EMG_ARMY3 | `DATA\PEDS.IDE:332` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 288 | `dsher` | COP / police-emergency | swat | VOICE_EMG_RCOP1 / VOICE_EMG_RCOP4 | `DATA\PEDS.IDE:333` / other special peds | IDE row has a source section label (general SA source-role lead) |
| 290 | `special01` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:336` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 291 | `special02` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:337` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 292 | `special03` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:338` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 293 | `special04` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:339` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 294 | `special05` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:340` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 295 | `special06` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:341` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 296 | `special07` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:342` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 297 | `special08` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:343` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 298 | `special09` | CIVMALE / mission-special | man | 0 / 0 | `DATA\PEDS.IDE:344` / special character slots | IDE row has a source section label (general SA source-role lead) |
| 299 | `special10` | CIVMALE / mission-special | fatman | 0 / 0 | `DATA\PEDS.IDE:345` / special character slots | IDE row has a source section label (general SA source-role lead) |

## Limits

The evidence does not connect a map zone to a particular pedgrp file, and does not show which candidates the game selects at runtime. The catalog is a saved IDE and archive-index snapshot; it does not enumerate script-created or cutscene-only actor uses. Selector membership in `variation.dat` is configuration evidence, not proof of live dispatch. No game was launched.

Full per-model records, every membership occurrence, source row references, and unmatched names are in `npc-priority-regions.json`.
