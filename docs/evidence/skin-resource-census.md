# Static skin resource census

Read-only DFF geometry and TXD header census for the five legacy Underground custom IMG archives and the 403-model Eagle priority baseline. Eagle baseline data came from the pre-pilot backup `backups/project-eagle/npc-law-enforcement-20261013-211911/COMPONENTPEDS.img`; legacy source members came from `docs/evidence/ped-archive-audit.json`.

## Coverage

- Legacy: 3,442 members attempted (1,721 DFF and 1,721 TXD); 3,434 parsed and 8 remain unknown.
- Eagle pre-pilot baseline: 403 of 403 model pairs parsed.
- Members were read one at a time. The census did not allocate per-vertex arrays, decode texture pixels, create previews, or launch the game.

## Geometry comparison

| Set | DFFs parsed | Vertices (min / p50 / p90 / max) | Triangles (min / p50 / p90 / max) | DFF bytes (min / p50 / p90 / max) |
|---|---:|---:|---:|---:|
| Legacy source | 1,719 | 328 / 15,066 / 37,534 / 65,421 | 388 / 19,847 / 52,108 / 103,862 | 15,312 / 1,228,039 / 2,906,199 / 8,278,016 |
| Eagle priority baseline | 403 | 623 / 1,017 / 1,471 / 3,029 | 844 / 1,024 / 1,270 / 1,996 | 56,403 / 81,453 / 105,580 / 205,477 |

Every Eagle baseline DFF has one geometry and one atomic, with one skinned geometry, a 32-bone skin header, and normals present. Of 1,719 parseable legacy DFFs, 1,717 have one geometry and 2 have two; 1,713 contain a skin extension and 1,635 report normals. Material slots are read from each geometry's material-list chunk struct; concrete material definitions are counted separately. In both sets every model currently has equal slot and definition counts: legacy p50 8 and max 72; Eagle p50 1 and max 11. These structural counts do not establish that bone names, hierarchy, or animations match CJ.

## Texture headers

| Set | TXDs parsed | Texture count per TXD (min / p50 / p90 / max) | Texture entries / stored mip bytes | Hypothetical RGBA32 mip-chain bytes | Common formats |
|---|---:|---:|---:|---:|---|
| Legacy source | 1,715 | 1 / 4 / 11 / 37 | 9,455 / 5,306,024,036 | 30,048,864,536 | 6,457 DXT1; 1,056 DXT3; 839 DXT5; 1,100 uncompressed 32-bit; 3 unknown |
| Eagle priority baseline | 403 | 1 / 1 / 7 / 10 | 894 / 30,027,392 | 61,975,352 | 675 DXT1; 5 DXT3; 1 DXT5; 213 uncompressed 32-bit |

All successfully parsed TXD headers in both sets identify platform 9. RGBA32 values are hypothetical arithmetic equivalents derived from dimensions and mip counts; they do not represent measured VRAM or game allocations. The `alpha_flag` records a native texture properties bit and does not indicate actual transparent pixels.

DXT2 and DXT4 FOURCCs are recognized as well, though none occur in these two texture sets. The three remaining legacy unknown-format textures use raster format code `0x00000032` at depth 8; they are not DXT2/4.

The 403 Eagle target `txdName` values all match their model basenames, and all 403 pairs parsed from that member naming rule. DFF material texture names now use the first material texture string, with the second string recorded separately as a mask name. Cross-checks against the 11 previously audited NPC samples also matched: DFF triangle totals, per-texture dimensions, stored mip byte counts, and material definition counts all agree with `npc-reuse-audit.json`. The deep audit does not record declared material-list slot counts, so there is no prior slot value to compare. The Aether source audit's 18 material-color definitions match the corrected parser's 18 definitions and 18 declared slots.

## Unknowns and limits

Eight legacy members could not be safely parsed and remain `unknown` in the JSON: `LC_CAS_WOM.dff`, `ulpdh1.dff`, `BMOSEC.txd`, `UL_WMYCV.txd`, `MH2_WATCHDOGS1.txd`, `SOMYST.txd`, `MW_SOMYRG.txd`, and `VC_HMYST.txd`. Exact parse errors and archive provenance are recorded per asset. Unknown assets are not classified as lightweight.

Static triangle, vertex, and texture byte counts help compare payloads. They do not establish frame rate, streaming behavior, actual GPU memory use, visual quality, draw-call cost, or animation compatibility.
