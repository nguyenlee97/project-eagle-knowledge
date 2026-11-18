# Project Eagle animation rig audit — 2026-10-22

## Scope and method

This audit covers the built deployment snapshot recorded in `Skin Library\Project Eagle\numbered-skins\deployment\build.json` (`builtAt` 2026-10-21 21:30:49 UTC; mapping digest `334ba0fddb5a962ba6754527f0cd83ea230159e61278e1edda73690fb96997c3`). Its 1,638 NPC slots resolve to 1,205 distinct DFF payload paths and 1,183 distinct payload hashes. Payload paths and SHA-256 values from `changes.*.dff` were checked against disk; each slot joined its catalog, review, and NPC records. Each payload's model was compared with the same IMG member in `deployment\baseline\aba128f7409947c47684.img` (4,224 members; 1,638 target models parsed).

The read-only parser uses `tools\skin-viewer\shared_txd.py`'s DFF chunk walker and length handling for nonstandard `0x0100000C` Struct lengths. It inspects the HAnim node table, FrameList parents, and geometry Skin bone counts. Re-run with `python docs\project-eagle\evidence\audit_crash_animation_rigs_2026_10_22.py`. No game files, archives, mappings, or source assets were changed by this audit.

## Findings

- **1,201 payloads have 32 HAnim nodes and 32 Skin bones; four have 24 and 24.** All 1,638 corresponding models in the Eagle baseline have 32 HAnim nodes and 32 Skin bones. There are no payloads where HAnim count differs from Skin bone count.
- The four 24-node payloads are the only hierarchy-size departures from their target models' baseline rigs. They omit baseline node IDs `6, 7, 8, 26, 36, 44, 54, 201, 301, 302` and instead contain `2000, 2001`:

  | Slots / target models | Skin | Original catalog DFF | Exact deployed payload |
  | --- | --- | --- | --- |
  | 7 `male01`; 48897 `sa_ballas7` | Evelyn Chevalier | `raw\Evelyn Chevalier__e4f598730992.dff` | `D:\GTA Staging\Project Eagle Viewer Builds\build-df439c58e9564db5a29e32e8b418a473\sa-compatible\ac762e4b58aca2d9bd7653c052b55daac2555fb8b747e4f2d876a9fd47a4ccb6.dff` |
  | 165 `WMOMIB`; 48574 `CC_SMILEY7` | player4 | `raw\player4__4a2fdb929a74.dff` | `D:\GTA Staging\Project Eagle Viewer Builds\build-df439c58e9564db5a29e32e8b418a473\sa-compatible\08ca06f1d9dde07ab59afcf3ce315c4a9cfa2522e8a6a2f07fe7226b640502b0.dff` |
  | 48105 `VCS_JERRY`; 48570 `CC_SMILEY3` | Tsukishiro Yanagi | `raw\Tsukishiro Yanagi__57e06baf27da.dff` | `D:\GTA Staging\Project Eagle Viewer Builds\build-df439c58e9564db5a29e32e8b418a473\sa-compatible\3d2dd42db6af562f151d69ae2f3608feae0d5937f207ea7e7b594f83bfb782e5.dff` |
  | 49165 `UL_TEXAN1` | Grace Howard — GTA VC model | `raw\Grace Howard — GTA VC model__319ff3f42c4e.dff` | `D:\GTA Staging\Project Eagle Viewer Builds\build-df439c58e9564db5a29e32e8b418a473\sa-compatible\0def2141833116c9d8f718f5008c9fa46f74cd86e11065dc7813dea2fe7bbdb0.dff` |

  The exact source root for the shorter catalog paths above is `C:\Users\LENOVO\Desktop\GTA\Skin Library\Project Eagle\numbered-skins\`. Each of these payloads has 24 Skin bones, 24 unique HAnim IDs and indices, no out-of-range or missing HAnim indices, and valid frame parents with no cycles. Each also has one extra FrameList sentinel ID `0xFFFFFFFF` not present in HAnim; this is the only frame/HAnim table discrepancy observed in the four files.

- **Twelve other payloads are 32/32 but use alternate HAnim IDs at three indices relative to their own baseline model.** At indices 6, 7, and 8, the payload IDs are `8, 6, 7`; the baseline IDs are `5015, 5004, 5001`, respectively. The sets differ by those exact IDs (`5001, 5004, 5015` absent from payload; `6, 7, 8` added). These do not have a node-count mismatch or exceed the 64-bone bound in the local `RpAnimBlend.cpp` QA source. Treat them as animation-ID compatibility leads, not as evidence of a count overflow or of the crash cause.

  | Slot | Target model | Skin | Catalog DFF filename |
  | ---: | --- | --- | --- |
  | 48753 | `MW_BFYAPRO` | Tina Venus | `Tina Venus__4fc1885df815.dff` |
  | 48788 | `MW_HFYSPRO` | SWFYSTR | `SWFYSTR__b7edd5d431ca.dff` |
  | 48877 | `SA_FAM7` | Clorinde | `Clorinde__6d5344898c67.dff` |
  | 49356 | `SA_PRO1` | Marian RRS | `Marian RRS__8c5b3b2b37e7.dff` |
  | 49274 | `SA_TRIADELDER` | Lynette SS | `Lynette SS__9186e31dd455.dff` |
  | 49333 | `SA_BMYDJB` | Momiji Fantasy | `Momiji Fantasy__158ef31fab64.dff` |
  | 48879 | `SA_FAM9` | Jean Summer | `Jean Summer__647011f99870.dff` |
  | 49338 | `SA_DANCEA` | Sucrose | `Sucrose__ca0ffa6c91af.dff` |
  | 49339 | `SA_DANCEB` | ManCafe | `ManCafe__3105896f3afb.dff` |
  | 49342 | `SA_HELPER1` | Tanjiro Kamado | `Tanjiro Kamado__fd5564427e19.dff` |
  | 49343 | `SA_HELPER2` | Yukari Takeba | `Yukari Takeba__26d838d6837f.dff` |
  | 49344 | `SA_HO` | Katya DSL | `Katya DSL__de9930b34b0e.dff` |

  Filenames in this table are under `C:\Users\LENOVO\Desktop\GTA\Skin Library\Project Eagle\numbered-skins\raw\`.

- The recently loaded slots 284–287 (Focalors/`lapdm1`, Koleda/`swat`, Rei Ayanami/`fbi`, ZhuYuan/`army`) each have 32 HAnim nodes and 32 Skin bones, and match their baseline node IDs, indices, and flags.
- Across all 1,205 payloads, the parser found no duplicate HAnim IDs, duplicate frame IDs, duplicate node indices, out-of-range or missing HAnim indices, invalid frame parents, or parent cycles. No Skin count exceeded 64. All payload hashes matched the build record, all metadata joins succeeded, and no baseline model failed to parse.

## Crash relevance and limits

The strongest rig-size concern is the four 24/24 payloads replacing target models whose Eagle baseline is 32/32. That is an exact model-to-payload hierarchy mismatch and can affect animation-node mapping; it does not prove the triggering asset or explain this crash on its own. The 12 alternate-ID payloads are a separate matching concern; their hierarchy and Skin counts agree.

The supplied crash log records an access violation at `gta_sa.exe+0xD0752` in `CAnimBlendNode::Update` and `EBX=0x36`. The accompanying disassembly analysis identifies the faulting read as `mov al,[ebx+4]`, where EBX came from the animation-sequence pointer at `[edi+0x10]`. This points to an invalid sequence pointer (`0x36`), not evidence that bone ID 54 was accessed. It does not identify a DFF or prove the rig mismatch caused the bad pointer. The local QA `RpAnimBlend.cpp` declares `MAX_NUM_BONES=64`; that source snapshot is not proof of the shipped executable's array layout, but the observed 24/32 counts alone do not establish a 64-entry array overflow.

This is a structural audit of the recorded deployment payloads, not an in-game animation test. The snapshot is the build digest and timestamp above; later builds may contain different payloads.
