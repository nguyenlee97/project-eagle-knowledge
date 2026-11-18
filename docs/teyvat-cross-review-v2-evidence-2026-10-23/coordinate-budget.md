# Coordinate and runtime-budget cross-check (2026-10-23)

## Scope and method

Read-only refresh against the gameplay-lab runtime and the revised master plan saved at 2026-10-23 23:16:28 +07:00. I did not scan IMG archives or run the game. The active config inventory from the earlier audit was reused because its recorded `gta.dat` and `default.dat` hashes match the current files. For the origin-overlap check, I parsed the text IPLs referenced by those active config directives using the existing section-aware parser and compared every parseable `inst` XYZ origin against the exact 196 rectangles in `placement-check.json` (closed interval edges). The helper and full machine-readable output are adjacent: [ipl-origin-overlap-audit.py](ipl-origin-overlap-audit.py) and [ipl-origin-overlap-audit.json](ipl-origin-overlap-audit.json).

## Findings

### IPL-origin check against the planned block set

- The active config references 272 unique IPLs. The parser found 84,386 text `inst` rows; 84,375 had numeric interior and XYZ fields.
- **Zero** valid origins fall inside the union of the 196 exact planned block rectangles (X `[-23,667, -2,163]`, Y `[-12,943, 4,465]`). Zero of the in-union origins have nonzero interior because there are no in-union origins.
- 1,550 valid origins fall inside the *bounding rectangle* but outside the disjoint block union. This is why a bbox-only count is not a placement overlap count.
- This is strictly a text-IPL **origin** check. It does not establish no overlap by model bounds: an IPL model can extend across a rectangle edge, and terrain/HLOD geometry may not be represented by these text IPL origins at all. Therefore it does not validate the plan’s broader “0% overlap with any GTA 3D island” statement.

### Revised plan anchor consistency

The master-plan formula at lines 25–29 is written for global OBJ vertex coordinates. The source manifest entries are separate anchor metadata, and the upstream city viewer transforms an entry’s X as `-position.x + 1024` before placing its mesh (upstream implementation is documented with links in the earlier [manifest review](../teyvat-geography-evidence-2026-10-23/coordinate-manifest-review.md#coordinate-implications-for-the-master-plan)). The current table at lines 35–44 mixes those frames:

| Table row | Source check | Result |
| --- | --- | --- |
| Mondstadt, line 37 | Manifest anchor is `(2275,263,-783)`; table uses raw OBJ horizontal pair `(-2275,-783)`. | Consistent with the stated raw-OBJ anchor convention for this row. |
| Liyue, line 39 | `Area_LYG_City_Constant_HLOD` manifest position is `(-610,240,290)`. Viewer X is `1634`; table says `world=(+1634,+290)`. | Table uses viewer-transformed X here. Its `dY_north=-3909` instead subtracts raw Mondstadt X `-2275` from `+1634`. This is a frame mix: the city-viewer X includes the loader’s +1024 shift, while the cited Mondstadt anchor is raw OBJ X. The manifest stores Liyue X=-610. Do not accept the derived relative value until every anchor is expressed in one named source frame; this does not challenge Liyue’s identity. |
| Inazuma, line 40 | `Area_DQC_Up_City_Constant_HLOD` manifest position is `(-3112,251,-4424)`. Viewer X is `4136`; table uses `+4136`. | Same mixed-frame pattern: the table’s north delta uses viewer X against raw Mondstadt X. The manifest stores Inazuma X=-3112. Do not compare that directly with either the viewer-transformed X or the raw Mondstadt anchor; normalize both anchors to the same declared frame first. |
| Sumeru, line 41 | The cited `Area_XKC02` entries share manifest position `(-367,364,2843)`; viewer X would be `1391`, not `3440`, and Z is `2843`, not `5530`. Five asset-group entries share that anchor; the central City group has Lod1/2 while Building, Leaf, Leaf ShadowMesh and Stone provide separate Lod0 records. | The table point `(3440,5530)` is not the `Area_XKC02` anchor under either the raw manifest or city-view transform. The earlier local manifest review found nearby `CWDJ*` entries around `(3374–3388, 5530–5570)` in viewer coordinates, but proximity alone does not establish which feature the plan intended. Treat the table point/label association as unsupported pending an explicit source entry or manual-anchor citation. |
| Fontaine, line 42 | `Area_FDC_Old01` manifest position is `(3335,467,4351)`; viewer X is `-2311`. | The displayed pair uses the viewer-transformed X. Its derived north delta also needs a declared, consistent reference frame; this table should not combine it with the raw Mondstadt X. |
| Natlan, line 43 | `Area_HGJTKD` manifest position is `(-2887,319,8559)`; viewer X is `3911`. | The row uses viewer X. The manifest review cautions that the exact place-name/feature is not established merely by a filename prefix; this is a coordinate-provenance issue, not a finding of wrong region identity. |
| Nod-Krai, line 44 | `Area_BGCWBM` manifest anchor is `(3263,328,9903)`; city-view X is `-2239`, while the table gives `(-8475,+9283)`. | The table point is not this manifest anchor under the city-view transform. An explicit alternate/manual source is needed; do not infer the label is false from this mismatch alone. |

The transform issue matters to proposed placements: the table’s `dY_north` values for Liyue and Inazuma equal `-(viewerX - rawMondstadtX)` (`-3909` and `-6411`), combining the city viewer’s +1024-transformed X with raw Mondstadt OBJ X. That is not a like-for-like subtraction. The plan’s formula is stated for raw OBJ vertices, and manifest anchors are not proven to equal each mesh’s raw vertex frame. Recompute every relative row from a single named frame and record any manual anchor’s source before using it to lay out sectors. This review does not choose a replacement coordinate convention; the parent’s image-fit review owns that decision.

### Current runtime snapshot and capacity context

Current hashes match the previously parsed active-inventory snapshot:

- `data/gta.dat`: `fbaae83cc08f5a74e25c2d10a069f695e25663f22d1e7cfa30d424f562ee2176`
- `data/default.dat`: `dbb63801e574f5004a4337203ef1d6696f6797e17d5d9daf056b59021cf37c32`

That snapshot sees 66 IMG, 189 IDE, 272 IPL and one COLFILE directive across the two configs, resolving to 187 unique IDEs and 272 unique IPLs. It counts 84,386 active text IPL `inst` rows and 63,322 unique active IDE model IDs excluding 2dfx. These mean “referenced by the current configs and present in the inventory,” not independently verified as loaded in a fresh game session. The FLA log in that inventory predates the current config timestamp, so it cannot certify a current-session load.

`gta.dat` currently references WIBU’s IMG, IDE and IPL directly (lines 11, 294 and 380); the three target files exist under `CUSTOM`. Thus WIBU-01 is installed/config-referenced, not stage-only. File presence and config reference do not establish a successful current game load.

The active IDE-ID snapshot has 63,322 IDs across `[0,199999]`, leaving 136,678 numerically unused. Of those, 17,927 are free in `[0,65535]` and 118,751 in `[65536,199999]`. The plan’s nominal need is 6,854 IDs (6,272 terrain near+LOD plus 582 architecture near+LOD), so the count fits even if limited to the low 16-bit range. That is only a capacity comparison, not proof the requested slots are allocatable: ownership and reservations apply. In particular, active IDs 6526–6862 are empty today, but planned/reserved ranges inside them are 6633–6704 (anime remap), 6710–6729 (Mondstadt slice) and 6730–6801 (Wilds M1). The 337-ID empty run therefore must not be represented as wholly available for Teyvat.

The number 147,231 quoted by the atlas is an atlas 3D-object count; 84,386 is a count of text IPL `inst` rows. They are different sources and units and should not be compared as a single occupancy total.

## Reproduction inputs and limits

- Runtime root: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
- Plan: [teyvat-continent-master-plan-and-lessons-2026-10-23.md](../teyvat-continent-master-plan-and-lessons-2026-10-23.md), table/formula lines 25–44.
- Exact planned block rectangles: [placement-check.json](placement-check.json), `blocks` array (196 records).
- Active inventories reused: `../teyvat-cross-review-evidence-2026-10-23/model-budget-active-inventory.json` and `model-budget-id-summary.json`; current config hashes above were independently refreshed.
- Local HoyoMap manifest/source limitations and transform distinctions: [coordinate-manifest-review.md](../teyvat-geography-evidence-2026-10-23/coordinate-manifest-review.md), especially lines 11–18 and 22–31.
- No IMG archive was hashed in this refresh; no game, staging, or runtime files were written; no game build or launch was performed.

