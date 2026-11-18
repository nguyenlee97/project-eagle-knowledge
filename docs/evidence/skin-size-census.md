# NPC skin size census

Date: 2026-10-14. This is a disk-footprint comparison for legacy basenames matched to the existing Eagle target-slot candidate list, not a prediction of frame rate, VRAM use, visual quality, or animation support. No Eagle archive or skin was changed.

## Findings

The source audit contains **1,721 complete DFF/TXD pairs** across five IMG archives. Directly rereading each IMG directory header found the expected entry count and an exact match with the cached audit for every member name and sector tuple. The source pair files total **7,785,021,422 bytes (7,424 MiB / 7.25 GiB)** by uncompressed RAR entry lengths. Their IMG allocations total **7,788,517,376 bytes (7,427 MiB)**; the roughly 3.3 MB difference is sector padding.

Across all 1,721 pairs, the median is **2.90 MiB**, the 90th percentile is **10.11 MiB**, and the largest pair is **26.58 MiB**. In the fixed disk-only bands, **1,104 pairs (64%) are at most 4 MiB** and **617 (36%) exceed 4 MiB**. That makes a useful first-pass sort for NPC candidates; it does not make a size threshold for whether a model is safe to run.

| Pair size (MiB) | All 1,721 | Legacy basename matches for 403 target slots | Legacy basename matches for 64 favorite slots |
|---|---:|---:|---:|
| ≤0.5 | 111 | 24 | 1 |
| 0.5–1 | 104 | 27 | 4 |
| 1–2 | 298 | 71 | 12 |
| 2–4 | 591 | 128 | 23 |
| 4–8 | 313 | 79 | 15 |
| >8 | 304 | 74 | 9 |

The 403 legacy basenames matching the existing Eagle target slots total **1,854,926,464 bytes (1,769 MiB / 1.73 GiB)**, with a 2.80 MiB median and 26.58 MiB maximum. The 64 favorite-slot legacy basename lookups total **292,572,536 bytes (279 MiB)**, with a 3.26 MiB median. These are source DFF+TXD totals for filename matches. A basename match does not establish character identity, selection, approval, or approved reuse: Eagle slot IDs and TXD names remain separate review fields. The existing 403/64 candidate sets remain unchanged with no character assigned.

Across all pairs, DFF files contribute **2,446,494,150 bytes (31.4%)** and TXD files contribute **5,338,527,272 bytes (68.6%)** of the source byte total.

| Statistic | All pairs | 403 target-slot basename matches | 64 favorite-slot basename matches |
|---|---:|---:|---:|
| Mean | 4.31 MiB | 4.39 MiB | 4.36 MiB |
| P10 | 0.89 MiB | 0.85 MiB | 1.20 MiB |
| P25 | 1.81 MiB | 1.78 MiB | 1.97 MiB |
| Median | 2.90 MiB | 2.80 MiB | 3.26 MiB |
| P75 | 5.87 MiB | 6.14 MiB | 5.30 MiB |
| P90 | 10.11 MiB | 9.96 MiB | 8.97 MiB |
| P95 | 12.21 MiB | 12.18 MiB | 12.27 MiB |
| P99 | 16.21 MiB | 16.84 MiB | 13.17 MiB |

The lightest pairs include SANEWS and WFYSEX at 112 KiB each. The largest are BW_MAILMAN and WFYBU at 26.58 MiB each, followed by MW_HMYBE2 and VC_GDA at 21.90 MiB. The full sorted top and bottom ten are in the JSON, along with any cached workbook historical names and cells. Those labels come from `workbook-audit.json` only and remain historical, unverified associations.

## Current Eagle baseline and disk scenarios

For the same 403 Eagle target slots, current mounted IMG directories provide each slot's DFF and its separately named TXD for **403/403**. Across 806 distinct requested archive members, sector allocations total **65,394,688 bytes (62.37 MiB)**. Reading only each member's first RenderWare chunk header gives a summed payload lower bound of **64,405,875 bytes (61.42 MiB)**; this is explicitly a lower bound if a member contains trailing data. This is the current archive baseline and includes the changed pilot members, so it is not a pristine pre-pilot comparison.

| Assumed pair size per target slot | 0.5 MiB each | 1 MiB each | 2 MiB each | 4 MiB each | 8 MiB each |
|---|---:|---:|---:|---:|---:|
| 64 favorite target slots | 32 MiB | 64 MiB | 128 MiB | 256 MiB | 512 MiB |
| 403 target slots | 201.5 MiB | 403 MiB | 806 MiB | 1,612 MiB | 3,224 MiB |

These are hypothetical arithmetic disk-budget scenarios only, for the existing slot counts at fixed assumed MiB per model. The 403/64 rows are legacy basename lookups against those slots, not approved model assignments. Compressed RAR size is not expanded IMG size. The current Eagle baseline is a different archive/game build from the custom RAR source set, so its smaller disk allocation does not imply equivalent assets or performance behavior.

## Group and coverage caveats

Canonical region membership comes from the existing master selection, not filename prefixes. Its lists overlap: Vice City has 225 candidates (29 favorites), Carcer City 226 (35), and Los Santos 180 (21). Every listed regional candidate has a matching source DFF/TXD basename pair in this census; this measures lookup coverage only, not identity, approved reuse, current Eagle installation, or runtime loading.

The workbook census does not open the XLSX files. Every retained historical name and cell comes from the cached JSON audit and should be treated as a lookup lead. Source member bytes are the audit's RAR metadata lengths; IMG allocated bytes are current source-audit sector allocations. The script does not hash the multi-gigabyte source archives.

## Files

- `skin-size-census.json` contains all 1,721 pair records, exact source and IMG allocation sizes, RAR paths, historical workbook names/cells, existing master-record IDs and memberships, distributions, extrema, source IMG header checks, and the current Eagle 403-model baseline.
- `build_skin_size_census.py` rebuilds the JSON from the existing audit/catalog/master JSON files and reads the current Eagle IMG headers and selected member chunk headers without extracting or changing archive data.
