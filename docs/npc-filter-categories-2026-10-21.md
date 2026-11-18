# Eagle NPC category and filter evidence — 2026-10-21

## Catalog read

I read the local viewer's `GET /api/npcs` response on `127.0.0.1:8943` and compared its records with `tools/skin-viewer/import_npcs.py` and the selected Eagle game data. The response had 1,638 NPC records. Each record provides `id`, `model`, `title`, `regions`, `regionEvidence`, `groups`, `locations`, `pedtype`, `role`, and related asset/evidence fields. The importer derives role from the `peds.ide` default ped type and derives region candidates from population-group file membership and selected variation entries.

Current role counts are 1,105 ordinary civilians, 324 gang peds, 136 police/emergency, 42 prostitute ambient peds, and 31 criminal ambient peds. The region labels include 225 Vice City, 226 Carcer City, and 180 Los Santos records. These region sets overlap: 403 distinct NPCs match at least one of the three priority cities. Membership is configuration evidence; it does not prove that a ped spawned in a live session or estimate its spawn probability.

The API response contained 422 records with `locations`, but none had a non-null `specificLocation`. Those locations are region-level candidates, not known streets or interiors. The importer also states that no exact zone, street, or coordinate is linked to the model by the available evidence.

## Classification rules and current counts

`tools/skin-viewer/npc-filters.js` returns ordered, nonexclusive categories with Vietnamese UI labels. The live catalog currently classifies as street/outdoors candidate 698 records, possible indoors 38, prostitute 42, girlfriend 6, gangs 330, police/emergency 136, other 31, and unknown/unclassified 608. Counts overlap; 38 records match both street/outdoors candidate and possible indoors.

The street/outdoors label is “Ngoài đường (theo population)” and means only that the NPC has a population-group membership from a `data/pedgrp*.dat` file or a `POPCYCLE_GROUP` label, or has an exact location hint naming an outdoor context. This broad rule includes groups such as business, workers, aircrew, golfers, and entertainers; the group membership is a useful candidate for street population, not proof of a live or exterior spawn.

The possible-indoors label is “Có thể trong nhà”. It is limited to the named cohorts Shopkeepers, Office workers, Husbands, and Wives, plus exact location hints naming an interior context. I inspected Eagle `data/pedgrp.dat` lines 91–97 and `data/pedgrp_vc.dat` lines 87–93: those files list Dealers, Shopkeepers, Office workers, Husbands, and Wives together in the labeled tail groups, separate from the earlier `POPCYCLE_GROUP_*` lists. The comments give cohort names but do not identify a specific interior, so this remains a hint. Servants and clubbers alone do not mark an NPC as indoors. Region labels alone imply neither street nor indoors. `unknown` means the current role/group/location rules did not produce a recognized category; it does not mean the model is absent or invalid.

Gang, police/emergency, prostitute, and other categories also use the imported role and pedtype fields. The girlfriend category is deliberately restricted to six exact ID/model pairs that appear in Eagle `data/peds.ide` at lines 228–233 with `PED_TYPE_GFD` and named voice tokens:

| IDE ID | Model | Name from voice token |
| ---: | --- | --- |
| 190 | `COPGRL3` | Barbara |
| 191 | `GUNGRL3` | Helena |
| 192 | `MECGRL3` | Michelle |
| 193 | `NURGRL3` | Katie |
| 194 | `CROGRL3` | Millie |
| 195 | `GANGRL3` | Denise |

`matchesNpc` accepts an explicit `mapped` boolean for the current editable draft mapping. It ignores `viewerAppliedSkin`, which describes a prior deployment and may no longer match the draft. It searches IDs, names/models, roles, regions, groups, locations, and the validated girlfriend names.

## Limits

Population groups and `variation.dat` selectors are configuration evidence, not proof of runtime spawning. The filter does not assert an exact street, interior spawn point, or live population behavior. The girlfriend list reflects only the six marked Eagle `PED_TYPE_GFD` slots found in the current `peds.ide`; other story characters are not included just because they are women or have relationship-themed group membership.

Focused Node verification: `node --test tools/skin-viewer/npc-filters.test.mjs` passed all 6 tests.
