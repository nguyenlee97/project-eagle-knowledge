# Project Eagle title override route

**Scope:** Read-only check of the already-installed `WibuWorldLoading` TXD override and the earliest title/loading route. No game process was started, no game files were changed, and no broad binary scan was run.

**Resolution, 14/10/2026:** The user clarified that the old Eagle image referred to a startup seen before reopening the installed pack. They later opened the game and confirmed “oke nó work tốt rồi”. No title replacement failure was established, and no direct base-TXD fallback was applied. The install remains in the clean Eagle copy; gameplay-lab was not changed.

## Finding

The installed ModLoader override is on the correct standard splash route. The base PC-US executable calls `CTxdStore::LoadTxd` with `loadscs.txd` from `MODELS\\TXD\\` while loading the standard splash set. LINK/2012's official ModLoader SA 1.0 US address map explicitly marks the corresponding `0x5900D2` call as the `std.fx` hook for `loadscs.txd`. The project's installed ModLoader log independently records the WibuWorld file as found by `gta3.std.fx` and installed.

The ModLoader core starts its plugins and scans/installs mods before it calls the game's `WinMain` (upstream `loader.cpp`). That ordering is early enough in principle for the ordinary in-game title/loading screen. Project Eagle also has a separate PECore splash, documented in [loading-trace.md](loading-trace.md). Root visually compared the supplied image with both source assets: its wide canvas and lower legal/credit rows match `LOADSCS.txd::title_pc_US` / T0058. The separate 640×640 PECore PNG has no legal/credit band and does not match the supplied full image.

## Current file and log evidence

- `modloader/WibuWorldLoading/txd/loadscs.txd` is 37,181,768 bytes and hashes to `7A3E0899F94908EF89596B4939A59BA3C082193BBCED44CC5FB4F2CAAC96E80D`, matching the supplied installed-art hash.
- Base `models/txd/LOADSCS.txd` is also 37,181,768 bytes but has a different SHA-256: `88C7A84E7695BA1D7DA06DAECC29CE79B6135CB44EC4ECC07B6B4ADD99F43511`. The base archive remains unchanged relative to the described replacement operation.
- The current `modloader/modloader.log` says `Found file ... "txd\\loadscs.txd" with handler "gta3.std.fx"` and later `Installing file "modloader\\wibuworldloading\\txd\\loadscs.txd"`.
- `gta3.std.stream` is disabled in the log. That does not block this dictionary replacement: the observed handler is `gta3.std.fx`, whose upstream SA address map contains the `loadscs.txd` hook. `gta3.std.sprites` is loaded too, but the actual log does not attribute this file to it. The local `std.sprites.md` example documents a `txd/loadscs.txd` layout for sprite dictionaries; the actual installed handler is the stronger evidence for this target.
- The override file's last-write time is 18:38:53 on 14 October 2026; the ModLoader log's last-write time is 18:37:05 the same day. The available log therefore predates the override file by about 1m48s and cannot be treated as a fresh run after that file landed. No `gta_sa` or `gta_pe` process was running during this read-only check.

## Interpretation and uncertainty

There is no evidence here of a ModLoader “too early for the title” limitation on the standard `LOADSCS.TXD` path. Instead, static source and current log support that this override should be available before the normal GTA SA title/loading renderer opens the dictionary. The user's image matches the old `title_pc_US` asset, but a failed post-install replacement is not yet established because run timing and the launched game folder remain unconfirmed. Also, the log's `Installing file` line proves ModLoader setup, not which image a renderer finally displayed. The clean and gameplay-lab copies must be distinguished: only the clean copy received this artwork install.

The `std.sprites` local documentation describes handling TXDs under `txd/`; in this installation the scanner assigns this exact file to `std.fx`. The official upstream mapping confirms `std.fx` intercepts the game's `loadscs.txd` load call, but the inspected source does not establish which exact bytes were ultimately read on a post-install run. That final runtime fact remains unverified.

## Recommended next step and reversible fallback

First make one controlled launch of the intended Eagle folder after the override timestamp, then inspect the newly written ModLoader log and distinguish the brief PECore splash from the standard GTA title/loading images. No further install is needed for that check. Capture the visible image or note whether the old Eagle mark is on PECore's separate overlay or on the standard splash artwork.

If a fresh run still shows the original standard splash art, the simplest deterministic fallback is to stage the replacement at the executable's canonical `models/txd/LOADSCS.txd` path: preserve the original base file as a named backup, copy the replacement into that path, and restore the backup to revert. Do this only as a later, explicitly requested install step; this investigation did not write there. Keep the current ModLoader copy intact until the fallback is verified.

## References

- Existing Project Eagle trace and renderer separation: [loading-trace.md](loading-trace.md).
- LINK/2012 ModLoader official GTA SA 1.0 US address map: https://github.com/thelink2012/modloader/blob/master/src/translator/gta3/sa/10us.hpp (maps `0x5900D2` to the `CTxdStore::LoadTxd` call for `loadscs.txd`).
- LINK/2012 ModLoader official loader startup sequence: https://github.com/thelink2012/modloader/blob/master/src/core/loader.cpp (`Startup`, plugin loading and mod scan occur before the game's `WinMain` call).
- Installed local plugin notes: `modloader/.data/plugins/gta3/std.fx.md`, `modloader/.data/plugins/gta3/std.sprites.md`; runtime setup evidence: `modloader/modloader.log`.
