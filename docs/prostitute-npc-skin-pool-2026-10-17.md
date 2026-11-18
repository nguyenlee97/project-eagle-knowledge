# User-selected NPC role skin pool — 2026-10-17

This is a read-only inventory of assets in `C:\Users\LENOVO\Downloads\prosititute skin` (the exact `prosititute` directory does not exist). The user selected this folder as a source for future NPC role mapping. No files were moved or deleted, and no game files were changed.

## Results

- 14 completed archives in the folder; all 14 passed archive integrity checks. One archive exactly matches the existing Thick Miku catalog archive by SHA-256, so it is reused as provenance and not counted as a new source job.
- The remaining 13 archives are local extras: 14 exact-basename DFF/TXD pairs, including two Honoka appearance variants. They have no exact archive, pair, or individual member hash match in the existing inspection corpus.
- Across the folder selection there are 15 distinct DFF/TXD pair assets after exact-hash deduplication. There are no unpaired DFFs and no weapon/prop exclusions.
- Three archive records contain `missing_material_textures` warnings (Fiona, Kokoro, and Yuzuki Yukari). Keep them for review; the warning alone does not establish a broken skin. No archive was tested in game.
- Existing rating is preserved for the exact Thick Miku catalog match (`neutral`). The 14 new pair assets are `rating_pending`; role tags do not set or change ratings.
- The role tag is future planning metadata only. Adult-character candidates remain pending rating and exact-variant review. Ochako, Kasumi, and Hatsune Miku are retained in the neutral inventory but withheld from sexualized NPC-role assignment pending age eligibility; the Ada/Microbikini/Motorbike asset has unresolved character identity and is unassigned.

## Asset records

| Local archive | Character/member identity | Pair ID | Role review | Rating | Archive SHA-256 | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `1576123813_133293.rar` | Fiona (DOAXVV member path label) | `45b01084efeb` | adult_role_candidate_pending_rating | rating_pending | `32e5c32bd57df26649816e43ac17bf6d2dd33572830da8543e0884caf5076059` | missing_material_textures |
| `1581424556_135195.rar` | Kokoro (DOAXVV member path label) | `3b280ff8e2f8` | adult_role_candidate_pending_rating | rating_pending | `de75a47ef6f41145caf9c2e189a95b7c4260498ff3fdb1932323237c26132308` | missing_material_textures |
| `1605541151_ada-wong-nude.rar` | Ada Wong | `f3b4bc97f49a` | adult_role_candidate_pending_rating | rating_pending | `034f38fd820a597e359a7e179675ece3b179aa92a32eccf1befd51aff35b603b` | none |
| `1611120103_zero-two-nude.rar` | Zero Two | `6a28ab9b35b8` | adult_role_candidate_pending_rating | rating_pending | `93e7910e0424741b65eda39e3a4f00be1723a8cbd89809db7860aece40737e5e` | none |
| `1612075174_1512334837_2b-misaki-miyata.rar` | 2B (member DFF basename) | `450980a04b51` | adult_role_candidate_pending_rating | rating_pending | `132b18244f70be8b5eb4be01f1334f5d4d4016d28d8ac07eae564a0cbf029ef2` | none |
| `1613897560_1551733239_boa_hancock_nude_mod_v2.rar` | Boa Hancock | `5d6372d605bd` | adult_role_candidate_pending_rating | rating_pending | `7738f3d3a6fd4ca3ce9d673dbd944c55aa66db790b47cae866abbde858005b27` | none |
| `1636876040_ochako_uraraka_n.rar` | Ochako Uraraka | `531f3843996c` | withheld_age_eligibility_review | rating_pending | `798e2b44176888af83ce7c2ee9ef3cd07283dc14ce54539bf7587fedccee58c3` | none |
| `ada-vong-microbikini-jacket-moto_1673560246_979620.rar` | Ada_Microbikini_Motorbike (asset label only) | `9b0a0ee2f6af` | identity_pending | rating_pending | `e3d99ca2d119d09b5e3018368bd280f73092d9ef867a2429ae1df08d40f3a756` | none |
| `gan-jujj-iz-genshin-impact_1676646118_500043.rar` | Ganyu | `b8aaf0c5a976` | adult_role_candidate_pending_rating | rating_pending | `eca9ff71b10b15f752c74b8c3a930c2092ba2fd7c079b4c651465ca30b2c12b9` | none |
| `juzuki-jukari-v-kupalnike_1651180165_860991.rar` | Yuzuki Yukari | `bbeca36a9d75` | adult_role_candidate_pending_rating | rating_pending | `c469758d547a0ab0144250f2a2510faced646ed04ff347164fdc32c6216ae06e` | missing_material_textures |
| `kasumi-v-mikro-bikini_1674484111_917296.rar` | Kasumi | `cc4411e2090d` | withheld_age_eligibility_review | rating_pending | `b6844c3d9acd26fe435153ac3877c927cc51ad5e2412904f2467cd5f7255e83f` | none |
| `khonoka-v-nizhnem-bele-iz-dead-or-alive_1673649662_209167.rar` | Honoka (two appearance variants) | `32e5003069f9` | adult_role_candidate_pending_rating | rating_pending | `834666fb673746717b91aa247e08216a01b6d7076aa4ab9e0f3d2cb22030a2e0` | none |
| `khonoka-v-nizhnem-bele-iz-dead-or-alive_1673649662_209167.rar` | Honoka (two appearance variants) | `667bc8530095` | adult_role_candidate_pending_rating | rating_pending | `834666fb673746717b91aa247e08216a01b6d7076aa4ab9e0f3d2cb22030a2e0` | none |
| `thick-miku_1789976598_121481.zip` | Hatsune Miku | `be3788500049` | withheld_age_eligibility_review | neutral | `909896fffcd42cd0854d78746c099d28d7ec2b55cf295c36cb38d96c5b597cfc` | none |
| `tina-armstrong-thicc-nude-version_1745113961_692853.zip` | Tina Armstrong / Tina Venus | `1da4255b5842` | adult_role_candidate_pending_rating | rating_pending | `f886a7bec7eee36b06823c54b7fe2260c14478ddc8b2e11d7329332244584527` | none |

Honoka has two DFF variants paired by exact same-folder basename to the same TXD; both pair IDs and member hashes are preserved in the JSON evidence.

Adult-role-candidate is a planning label, not an age assertion from archive metadata. Before actual ped mapping, confirm the selected variant and review its rating. Under-18 or age-unclear variants remain unassigned; identity-unclear assets remain neutral until identified.

## LibertyCity LC-01 source handoff reconciliation

All 20 frozen canonical URLs and opened-tab records match. Fourteen files had exact public filename and SHA evidence. The user then explicitly confirmed the exact local filename for each of the six remaining source rows; those confirmations are recorded separately from public evidence. Public archive filenames and public SHA-256 values remain unavailable for those six, and no local SHA below is represented as a publisher hash.

Four permitted adult-model archives (Ganyu, Boa Hancock, Yuzuki Yukari, and Raynare) now have canonical LibertyCity copies with truthful local SHA-256 values and safe inspections. Three inspections are reused from the prior neutral role-pool inventory; Raynare was safely inspected once. Yuzuki’s `missing_material_textures` warning remains recorded. Ochako and Thick Miku are confirmed source associations, but sexualized-minor/age-eligibility policy holds keep them in neutral inventory only: no new LibertyCity copy, staging, extraction, or role review. Thick Miku’s prior exact GTAInside archive match remains historical provenance and does not establish its separate LC source; the user confirmation does.

Two previous pairing notes remain: Goku in (`missing_material_textures`) and Towa (`no_skin_plugin_found`). The 30.9 MB unknown partial remains untouched. LC-02 has 12 of 13 frozen source pages open for the user; Marin Kitagawa remains a policy hold and was not opened. No download controls, forms, or age checks were used. LC-03 remains unopened.

| Job | LibertyCity resource | User-confirmed filename | Local SHA-256 | Result |
| --- | --- | --- | --- | --- |
| Ganyu (`d5aff3a449febdb2`) | `libertycity:183954` | `gan-jujj-iz-genshin-impact_1676646118_500043.rar` | `eca9ff71b10b15f752c74b8c3a930c2092ba2fd7c079b4c651465ca30b2c12b9` | Canonical copy and prior safe inspection retained; role rating remains pending. |
| Ochako Uraraka (`b969eb026cc4f6e7`) | `libertycity:165974` | `1636876040_ochako_uraraka_n.rar` | `798e2b44176888af83ce7c2ee9ef3cd07283dc14ce54539bf7587fedccee58c3` | Metadata-only confirmation; sexualized-minor hold, no new stage/extraction/role review. |
| Boa Hancock (`21d6c29c6eedc6d1`) | `libertycity:154395` | `1613897560_1551733239_boa_hancock_nude_mod_v2.rar` | `7738f3d3a6fd4ca3ce9d673dbd944c55aa66db790b47cae866abbde858005b27` | Canonical copy and prior safe inspection retained. |
| Yuzuki Yukari (`6a20ce982741fbaa`) | `libertycity:173985` | `juzuki-jukari-v-kupalnike_1651180165_860991.rar` | `c469758d547a0ab0144250f2a2510faced646ed04ff347164fdc32c6216ae06e` | Canonical copy and prior inspection retained; `missing_material_textures` warning remains. |
| Hatsune Miku (`65ed1f188733f9af`) | `libertycity:243298` | `thick-miku_1789976598_121481.zip` | `909896fffcd42cd0854d78746c099d28d7ec2b55cf295c36cb38d96c5b597cfc` | Metadata-only confirmation; age-eligibility hold. Existing neutral inventory/catalog inspection retained; no new LC stage/extraction/role review. |
| Raynare (`b9378923a839dcce`) | `libertycity:236480` | `rajjnare-iz-high-school-dxd_1775487063_606559.rar` | `55afa41f67f959a06c09eaac6bc90a4a2b345b0821f749ca50cde7d1bc229524` | Exact user-confirmed filename found in Downloads root, copied without moving the original, and safely inspected (1 paired DFF/TXD, no warnings). |

## Evidence and links

- Detailed per-archive, DFF/TXD, identity, role status, and exact-hash provenance: [JSON evidence](evidence/prostitute-npc-skin-pool-2026-10-17.json).
- LC-01 validation: [validation report](../../staging/project-eagle/skin-downloads-2026-10-15/libertycity/manual-downloads/LC-01-validation-report.json).
- Frozen LC manual groups: [group index](../../staging/project-eagle/skin-downloads-2026-10-15/libertycity/manual-downloads/index.html).
- Archive inspections: `staging/project-eagle/prostitute-role-pool-2026-10-17/inspections/role-pool-validation.json` and the per-hash inspector reports referenced by the JSON evidence.

Validation was static and read-only. It did not install assets, write to the game, assign ped IDs, test animations, or estimate performance.
