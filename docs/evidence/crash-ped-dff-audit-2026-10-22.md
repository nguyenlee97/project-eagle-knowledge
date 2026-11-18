# Project Eagle mapped ped DFF audit — 2026-10-22

## Scope and method

Audited the original DFF/TXD source files for the 1,638 mappings recorded as applied in `Skin Library\Project Eagle\numbered-skins\deployment\state.json`, joined to the 1,638 build slots and `catalog.json`. This resolves to 1,205 unique DFFs and 1,156 unique TXDs. No game, archive, mapping, or source asset was changed. The crash context is `Project Eagle\gta sa clean\gta sa clean\ProjectEagle_crashes\2026-10-22_04-06-47.log`; its stack reaches `RpClumpForAllAtomics` / `GetFirstAtomic` with a null clump.

Decoded RenderWare version fields with the same formula used in `tools\skin-viewer\vendor\dff-loader\Reader.js`. For length compatibility, applied the exact guarded rule in `tools\skin-viewer\shared_txd.py:dff_length` and `Reader.js`: only Struct/Clump lengths whose high byte is `0x01` and whose raw size exceeds remaining file bytes are masked to 24 bits. The supported `0x34000..0x36003` Clump Struct range below is from the main investigation's separate disassembly of Eagle's shipped `gta_sa.exe`.

## Findings

- **Four unique source DFFs use RW 3.3.0.2 (`0x33002`) in both the root Clump and its Struct, affecting seven slots.** These are the only mapped files below `0x34000`. Their root and Clump Struct versions agree.

  | Source DFF | Applied NPC slots |
  | --- | --- |
  | `Evelyn Chevalier__e4f598730992.dff` | 7 `male01`; 48897 `sa_ballas7` |
  | `player4__4a2fdb929a74.dff` | 165 `WMOMIB`; 48574 `CC_SMILEY7` |
  | `Tsukishiro Yanagi__57e06baf27da.dff` | 48105 `VCS_JERRY`; 48570 `CC_SMILEY3` |
  | `Grace Howard ...__319ff3f42c4e.dff` | 49165 `UL_TEXAN1` |

- The other 1,201 unique DFFs are in range: 1,199 have root/Clump Struct `0x36003`, and two have `0x36000`. Across all 1,205 files, every parsed core Struct uses its file's same version; no file has mixed core Struct versions. This makes the four `0x33002` files the clear version-compatibility candidates in the applied DFF set. It does not by itself prove which asset triggered the crash.
- The first bounded Clump root in each file has one actual Atomic, matching that Clump Struct's declared Atomic count. The bounded first-Clump walk found no child chunk extending past its parent. All 1,205 files expose Skin and HAnim plugin chunks in their parsed extension lists.
- In 544 files, a Struct header stores raw length `0x0100000C`; the viewer/builder compatibility rule reduces it to `0x0000000C`. After that documented adjustment, these Struct chunks fit their parent. This is a noncanonical length pattern, not an observed chunk overrun.
- 615 files have bytes after the end of their first Clump root: 67 have 1–4,095 bytes and 548 have at least 4,096 bytes. The total is 19,163,588 bytes; the maximum is 35,111 bytes. `Reader.js` returns the first Clump, so this data is outside the parsed root and was not treated as an invalid child chunk. The audit does not classify the trailing bytes' contents.

## TXD platform and D3D8 metadata

Reading the first native platform field in each of the 1,156 unique mapped TXDs found 1,153 platform-9 (D3D9) dictionaries and three platform-8 (D3D8) dictionaries. Across slots, that is 1,633 D3D9 and five D3D8 assignments. The TXD probe read native headers only; it did not decode texture pixels. For D3D8, `hasAlpha` below is the native alpha flag read by the viewer, and compression names decode the stored D3D8 compression byte.

- `Evelyn Chevalier__e4f598730992.txd` — slots 7 and 48897; three textures, all depth 16, one mip, platform 8:
  - `face`: 1024×1024, raster `0x0100` (1555), DXT1, alpha flag true.
  - `body`: 1024×1024, raster `0x0300` (4444), DXT5, alpha flag true.
  - `body2`: 1024×1024, raster `0x0300` (4444), DXT5, alpha flag true.
- `Tsukishiro Yanagi__57e06baf27da.txd` — slots 48105 and 48570; three textures, all depth 16, one mip, platform 8:
  - `Face`: 2048×2048, raster `0x0100` (1555), DXT1, alpha flag true.
  - `Body1`: 2048×2048, raster `0x0200` (565), DXT1, alpha flag false.
  - `Body2`: 2048×2048, raster `0x0100` (1555), DXT1, alpha flag true.
- `Grace Howard � GTA VC model__319ff3f42c4e.txd` — slot 49165; five textures, all depth 16, one mip, platform 8:
  - `face`: 2048×2048, raster `0x0200` (565), DXT1, alpha flag false.
  - `gunbody`: 1024×1024, raster `0x0200` (565), DXT1, alpha flag false.
  - `hairin`: 2048×2048, raster `0x0200` (565), DXT1, alpha flag false.
  - `hairshine`: 2048×2048, raster `0x0100` (1555), DXT1, alpha flag true.
  - `clothes`: 2048×2048, raster `0x0200` (565), DXT1, alpha flag false.

The four old-version DFFs overlap three of the D3D8 TXDs (Evelyn, Tsukishiro, Grace); `player4` uses D3D9. All three D3D8 dictionaries parsed their declared texture counts without a header error.

