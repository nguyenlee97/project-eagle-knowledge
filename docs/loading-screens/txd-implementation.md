# Wibu World TXD packaging and install route

Implementation for the 14 October 2026 artwork rollout. The final pack is installed at `modloader/WibuWorldLoading/txd/loadscs.txd` in `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`. The pilot was launched briefly, without a poster/title visual capture; the user subsequently tested the full pack and confirmed it works well. [Current install report and rollback](wibu-world-implementation.md) supersede the earlier staging status below.

## Staged work

- `staging/project-eagle/loading-screens/implementation/scripts/prepare_png_exports.py` reads approved masters from `art-source`, checks each image against the dimensions/aspect of its `LOADSCS.txd` texture, refuses aspect mismatch above 1%, then exports to exact native size with RGB/Lanczos and no crop. It preserves the source artwork files.
- `staging/project-eagle/loading-screens/implementation/scripts/package_loadscs.py` encodes 13 opaque poster/title PNGs as DXT1 and encodes `LOADSC6` as native X8R8G8B8. It replaces native chunks in a copy of the original dictionary and independently reparses input/output with the existing `scripts/extract_loading_txd.py`. Pilot, final, title-only, and LOADSC6-only QA modes are available.
- The DXT1 encoder was tested against source previews. An encoder defect with uniform color blocks was found and fixed before the approved pilot was packaged. Current pilot round-trip is 34.19 dB PSNR, 2.92 mean absolute RGB error, and 117 maximum channel-level error.
- Pilot artifact: `staging/project-eagle/loading-screens/implementation/ready/LOADSCS-pilot.txd`, SHA-256 `bd01cbc67275a1372a3efb01a3304dd23f3b68f43200475c1eba3e09cc8f9ff3`. Exactly `LOADSC8` changed. All other native chunks, both vendor chunks, X8R8G8B8 `LOADSC6`, names/order/cardinality (17), and dictionary trailer were verified unchanged. Its DXT1 payload is 1,036,800 bytes for 1920×1080.
- Pilot visual comparison: `staging/project-eagle/loading-screens/implementation/qa/LOADSCS-pilot/LOADSC8-comparison.jpg`; machine report: `staging/project-eagle/loading-screens/implementation/qa/LOADSCS-pilot/LOADSCS-pilot-qa.json`. Each package run writes into a folder named for its output artifact so synthetic fixtures cannot overwrite actual artwork QA.
- The title export composites the approved black-and-white Hu Tao mark at native size centered at `(1273, 0)` on a black 3800×2048 canvas. It preserves original decoded legal/credit rows 1456–2047 pixel-for-pixel. Because row 1456 is aligned to a BC1 block boundary, packaging also copies the original DXT1 blocks for that entire lower band; title-only QA confirmed byte identity for the encoded band.
- Title preview and test archive: `staging/project-eagle/loading-screens/implementation/qa/title_pc_US-composite.png`, `staging/project-eagle/loading-screens/implementation/qa/LOADSCS-title-fixture/title_pc_US-roundtrip.png`, and `staging/project-eagle/loading-screens/implementation/qa/LOADSCS-title-fixture/LOADSCS-title-fixture-qa.json`.

## Source backup and loader evidence

The live `models/txd/LOADSCS.txd` was copied byte-for-byte to `staging/project-eagle/loading-screens/implementation/backup/LOADSCS.original.txd`. Both hashes are `88c7a84e7695ba1d7da06daecc29ce79b6135cb44ec4ecc07b6b4add99f43511` (37,181,768 bytes). The backup inventory also records SHA-256 and source timestamp for `modloader.ini`, `modloader.log`, and `modloader/.data/plugins/gta3/std.sprites.{md,dll}`; the corresponding read-only copies are under `implementation/backup/modloader/`.

The current profile is `Default`. Its config documents a default mod priority of 50. The `std.sprites.md` shipped with this game gives the route `modloader/<name>/txd/loadscs.txd`; the saved modloader log records `gta3.std.sprites` loaded. No existing `modloader/**/loadscs.txd` collision was found, and the proposed `Genshin Loading Pilot` and `WibuWorldLoading` folders were absent at capture time. These prove the selected plugin/config and lack of a named collision in the captured state, not that an overlay was applied or rendered in game.

## Build and verify

From `C:\Users\LENOVO\Desktop\GTA` after the relevant approved images are present:

```powershell
C:\Python310\python.exe staging\project-eagle\loading-screens\implementation\scripts\prepare_png_exports.py --names LOADSC8
C:\Python310\python.exe staging\project-eagle\loading-screens\implementation\scripts\package_loadscs.py pilot
C:\Python310\python.exe staging\project-eagle\loading-screens\implementation\scripts\package_loadscs.py verify --input staging\project-eagle\loading-screens\implementation\ready\LOADSCS-pilot.txd --mode pilot
```

When all 14 poster masters are approved and exported, run the exporter with no `--names`, then `package_loadscs.py final`. Final expected changed set: `LOADSC1`–`LOADSC14` and `title_pc_US` (15 texture members). All posters except `LOADSC6`, plus the title, use DXT1. `LOADSC6` is re-encoded losslessly as X8R8G8B8 with its original platform, filter, raster format, depth, mip count, raster type, and flags; build QA compares every decoded RGB pixel against the exported PNG. The builder refuses incomplete inputs or dimension mismatches. Only NVIDIA and EAX native chunks remain unchanged in the completed archive.

## Install route and rollback

The actual pilot and full-pack installs used the same `modloader\WibuWorldLoading\txd\loadscs.txd` path; the full pack replaced the pilot. The initial separate Genshin Loading Pilot folder proposal was not used. Loader config and `models\txd\LOADSCS.txd` remain unchanged. The pilot log records the file accepted/installed by `gta3.std.fx`; the sprites documentation supplied the folder layout. Root installed the reviewed final pack and PECore startup/caption candidate with hash guards and an original-core backup. The guarded `implementation/scripts/rollback_wibu.ps1` restores original PECore and removes only the recorded overlay file, then removes its empty folders without recursive deletion.

The user performed the final in-game test and confirmed “oke nó work tốt rồi” on 14 October 2026. Root did not launch the full pack after the user chose self-testing. Individual crop/fade timings and performance were not separately measured; the confirmation is recorded in implementation/qa/user-runtime-confirmation.json.
