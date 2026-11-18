# Wibu menu TXD asset packaging

The menu plugin consumes one texture per dictionary: `cover` from each
`plugins/wibu-menu/assets/covers/<id>.txd`, and `logo` from
`plugins/wibu-menu/assets/branding/wibu-world.txd`. The packer writes to
staging by default; it never writes into or launches the game.

`staging/project-eagle/wibu-menu/scripts/pack_menu_txd.py` reuses the validated
Project Eagle DXT1 encoder and native fields from the original LOADSCS
dictionary. It rebuilds a standalone RenderWare root with one dictionary entry,
preserves the Eagle root/dictionary/native versions and root extension, names
the cover texture `cover`, and uses D3D9 platform 9, DXT1 (`D3DFMT_DXT1`, raster
`0x0200`) with one mip. Cover input must be opaque, at least 1600×900 and within
1% of 16:9. Output dimensions are the nearest multiples of four. When an input
dimension needs adjustment, the packer resamples the full image with Lanczos;
it does not crop it.

The approved transparent logo is stored as D3D9 A8R8G8B8 (`D3DFMT_A8R8G8B8`
21, raster `0x0500`), one mip, at the source PNG dimensions. The output payload
uses little-endian BGRA and the QA step compares each RGB and alpha byte against
the decoded PNG. The Eagle extractor also reparses and decodes the result.

The cover manifest records source and output dimensions plus an optional
normalized portrait UV rectangle (`u0`, `v0`, `u1`, `v1`). Actual cover builds
leave this field empty until the reviewed face crop metadata is supplied. The
fixture has a centered 3:4 crop for demonstrating the field only. It is marked
`fixture_only` and is not a Wibu character cover.

## Commands

Build available approved covers, the logo, and use metadata when provided:

```powershell
python staging/project-eagle/wibu-menu/scripts/pack_menu_txd.py batch-covers `
  --input-dir staging/project-eagle/wibu-menu/canonicalassets/covers `
  --output-root staging/project-eagle/wibu-menu/dist `
  --include-logo
```

The optional `--uv-json path.json` accepts an object keyed by character id;
each entry contains normalized `u0`, `v0`, `u1`, and `v1`. Batch mode records
missing sources and exits successfully so staged batches can be built
incrementally. Add `--require-all` once the final 23-source batch is expected.

Build only the approved logo:

```powershell
python staging/project-eagle/wibu-menu/scripts/pack_menu_txd.py logo
```

The focused DXT1 fixture uses an existing loading-screen PNG solely to prove
format and dictionary structure:

```powershell
python staging/project-eagle/wibu-menu/scripts/pack_menu_txd.py cover `
  --input staging/project-eagle/loading-screens/implementation/art-source/textures/LOADSC8.png `
  --output staging/project-eagle/wibu-menu/qa/txd/fixtures/cover-fixture.txd `
  --fixture
```

## Current QA

`staging/project-eagle/wibu-menu/qa/txd/manifest.json` stores source and TXD
SHA-256 hashes, native format fields, texture count, dimensions, round-trip
metrics, alpha checks, UV status, and missing source IDs. Decoded images are
under `staging/project-eagle/wibu-menu/qa/txd/`; `covers-contact-sheet.jpg`
shows current covers and labels the fixture separately.

The standalone file is checked by the existing Eagle parser and extractor and
by a separate bounds-checked RenderWare reader in the packer. The logo check
passed with exact RGB and alpha equality across 1,572,528 pixels; alpha values
range from 0 to 255 with both fully transparent and partial-alpha pixels.
The temporary LOADSC8 fixture parsed as one D3D9 DXT1 texture at 1672×940 from
the 1672×941 source, with a 0.10638% aspect-ratio change and no crop. The fixture
is test evidence only.

All 23 Wibu covers and the logo are now packaged under
`staging/project-eagle/wibu-menu/dist/plugins/wibu-menu/assets/`.
Every cover has reviewed face-crop UV metadata, and the final batch reports
24 artifacts with zero failures. The original fixture remains QA evidence
only and is absent from the installed package. The decoded cover and portrait
gallery is `staging/project-eagle/wibu-menu/qa/gallery.html`.
Current artifact hashes and full verification records are in the QA manifest.
