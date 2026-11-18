# Project Eagle: law enforcement and army ped targets

Read-only mapping from the current manifests, `data/variation.dat`, `data/peds.ide`, `PECore.ini`, and mounted IMG indices. No game was launched.

## Finding

For an explicitly selected Los Santos test, the smallest bundle covering the three mapped law-enforcement selector types is `lapd1` (ID 280), `swat` (285), and `army` (287). All three are actual Eagle IDs with one DFF and TXD match each in `S&S/CDimages/default/COMPONENTPEDS.img`; all use the `swat` animation group. This bundle is LS-specific for the base police role. The same `swat` and `army` IDs are mapped for CS, SF, and LV.

The user asked where a new game starts but has not confirmed a live location or save state. Local `Changelog.txt:84` says the start was shifted from Rose City to Carcer City; this is the expected new-game origin, not an observed runtime region. Although `variation.dat` lists CC in its city-code header, it contains no active CC selector rows. Carcer-specific definitions `CC_CCPD1`–`CC_CCPD6` and `CC_SWAT` exist in `peds.ide` and have archive assets, but these files do not show that wanted-level logic selects them; there is no `CC_ARMY`. Treat them as candidates requiring an actual selector/call-site confirmation.

## Active regional selector mappings

| Region code | COPPED | SWPED | ARPED | Source lines in `variation.dat` |
| --- | --- | --- | --- | --- |
| CS | csher (283) | swat (285) | army (287) | 33, 40, 45 |
| LS | lapd1 (280) | swat (285) | army (287) | 57, 64, 69 |
| SF | sfpd1 (281) | swat (285) | army (287) | 81, 88, 93 |
| LV | lvpd1 (282) | swat (285) | army (287) | 105, 112, 117 |
| LC | LC_COP (48432), LC_COP2 (49268), LCS_COP (49216) | LC_SWAT (48516), LCS_SWAT (49219) | LC_ARMY (48409), LCS_ARMY (49220) | 129, 136, 141 |
| VC | VCS_COP (48037), VC_COP (48289) | VC_SWAT (48358), VCS_SWAT (48119) | VCS_ARMY (48014), VCS_GANG4A (48066), VCS_GANG4B (48067), VC_ARMY (48259) | 153, 160, 165 |

For CS/LS/SF/LV, each selector has one mapped ID. Liberty City has multiple values per selector; Vice City has multiple police/SWAT/army IDs. If model variation chooses among those lists at runtime, a broad LC/VC replacement needs multiple target pairs; the current files do not justify reducing those lists to one model. Region codes RC/FW/IC/JP/CC/CM/UPS are in the header but have no active COPPED/SWPED/ARPED rows in this file. In particular, there is no Carcer mapping for the user's current region.

## Los Santos bundle details

| Selector | ID / model | IDE role and source | DFF/TXD in mounted archive | Shared TXD / duplicate basename |
| --- | --- | --- | --- | --- |
| COPPED | 280 / `lapd1` | `COP`, `STAT_COP`, anim `swat`, voice `VOICE_EMG_LAPD1` / `VOICE_EMG_LAPD8`; `data/peds.ide:321` | `S&S\CDimages\default\COMPONENTPEDS.img:lapd1.dff` (36 sectors); `lapd1.txd` (9 sectors) | no shared TXD; one archive match each |
| SWPED | 285 / `swat` | `COP`, `STAT_COP`, anim `swat`, voice `VOICE_EMG_SWAT1` / `VOICE_EMG_SWAT6`; `data/peds.ide:330` | `S&S\CDimages\default\COMPONENTPEDS.img:swat.dff` (40 sectors); `swat.txd` (65 sectors) | no shared TXD; one archive match each |
| ARPED | 287 / `army` | `COP`, `STAT_COP`, anim `swat`, voice `VOICE_EMG_ARMY1` / `VOICE_EMG_ARMY3`; `data/peds.ide:332` | `S&S\CDimages\default\COMPONENTPEDS.img:army.dff` (37 sectors); `army.txd` (65 sectors) | no shared TXD; one archive match each |

The pairs are mounted by `data/gta.dat:25`. `data/default.dat:18` declares `DATA\PEDS.IDE`; `PECore.ini:33` has `ModelVariation = true`. In `data/peds.ide`, `lapd1`, `swat`, and `army` have the role metadata `COP`/`STAT_COP`, animation group `swat`; voice fields distinguish LAPD, SWAT, and Army. `ModelVariation=true` plus the explicit `COPPED`, `SWPED`, and `ARPED` rows support role mapping; they do not establish a precise wanted-star threshold or prove a model was requested live.

## Carcer candidates and limits

| ID / model | Role | Source | Mounted DFF/TXD | Status |
| --- | --- | --- | --- | --- |
| 48523 / `CC_CCPD1` | COP / STAT_COP, anim swat | `data/peds.ide:866` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_CCPD1.dff` + `CC_CCPD1.txd` | no CC variation selector found |
| 48524 / `CC_CCPD2` | COP / STAT_COP, anim swat | `data/peds.ide:867` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_CCPD2.dff` + `CC_CCPD2.txd` | no CC variation selector found |
| 48525 / `CC_CCPD3` | COP / STAT_COP, anim swat | `data/peds.ide:868` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_CCPD3.dff` + `CC_CCPD3.txd` | no CC variation selector found |
| 48526 / `CC_CCPD4` | COP / STAT_COP, anim swat | `data/peds.ide:869` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_CCPD4.dff` + `CC_CCPD4.txd` | no CC variation selector found |
| 48527 / `CC_CCPD5` | COP / STAT_COP, anim swat | `data/peds.ide:870` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_CCPD5.dff` + `CC_CCPD5.txd` | no CC variation selector found |
| 48528 / `CC_CCPD6` | COP / STAT_COP, anim swat | `data/peds.ide:871` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_CCPD6.dff` + `CC_CCPD6.txd` | no CC variation selector found |
| 48578 / `CC_SWAT` | COP / STAT_COP, anim swat | `data/peds.ide:921` | `S&S\CDimages\default\COMPONENTPEDS.img:CC_SWAT.dff` + `CC_SWAT.txd` | no CC variation selector found |

`data/model_special_features.dat` documents `CustomModelName StandardModelName` aliases for vehicle behavior, with Carcer examples `cc_ccpdvan enforcer` (:59), `cc_copbike copbike` (:60), and `cc_copcarcc copcarvg` (:61). It does not select pedestrian IDs; it has no `CC_CCPD*`, `CC_SWAT`, or `CC_ARMY` entries. The Carcer peds are listed by `peds.ide` and their assets are mounted, but no direct wanted-level selector/call-site was found in the requested data files. A read-only text search of game data/configs also found no additional CC ped selector mapping; opaque compiled/script references remain outside this finding.

The broad variation targets have distinct TXD names; none shares TXD with another model in this target set. No duplicate DFF/TXD basename matches were found among their active archive matches. Across the full ped catalog, shared TXD groups are `generic` (ID 0 and 290–299) and `lcs_chauff` (IDs 49229 and 49236), unrelated to these law-enforcement variants.

## Recommendation and verification boundary

For the expected new-game origin Carcer City, no evidence-backed wanted-trigger target bundle can be recommended from the inspected selector configuration. `CC_CCPD1`–`CC_CCPD6` and `CC_SWAT` are role-tagged assets, but their selector/call-site use is unproven. Do not treat them as confirmed wanted-response targets. The `lapd1` + `swat` + `army` bundle is supported only for a controlled Los Santos variation test. CS/SF/LV require changing the standard COPPED model to `csher` (283), `sfpd1` (281), or `lvpd1` (282); their SWPED and ARPED mappings remain `swat`/`army`. To cover all six regions currently represented, Liberty City and Vice City each require bundling every listed variant, Carcer has no active selector mapping in this file.

`variation.dat` and `peds.ide` provide configuration-level role evidence. The saved catalog includes mounted IMG index matches, not proof of live streaming or spawn. `PECore.ini:33` enables model variation, but no runtime session or exact script call site was tested. `model_special_features.dat` is vehicle-specific. No save or live runtime was inspected; Carcer as expected new-game origin comes from local `Changelog.txt:84`.

Machine-readable source rows and every matching asset path are in `npc-law-enforcement-targets.json`.
