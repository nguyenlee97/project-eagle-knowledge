# Wibu menu plugin implementation

**Revision status:** behavior below describes the initial build. User testing found folded UVs and first-main-menu audio silence. The corrected build is now installed; current behavior, hashes, and checks are documented in `render-audio-fix.md`. It expands pregame artwork pages, corrects native UV order, and uses an independently initialized private menu BASS module with retry/logging. The user has not yet confirmed the corrected runtime behavior.

## Current deliverable

`staging/project-eagle/wibu-menu/plugin/build/WibuMenu.asi` is a compiled x86 ASI prepared for static review and parent packaging. Its matching source is `staging/project-eagle/wibu-menu/plugin/src/wibu_menu.cpp`; `staging/project-eagle/wibu-menu/plugin/build/build-x86.cmd` rebuilds it with the installed Visual Studio 2019 x86 toolchain. The build is deliberately separate from PECore and does not patch or replace core binaries.

The ASI accepts only the two currently installed Project Eagle PE32 variants (`gta_sa.exe` and `gta_pe.exe`) after checking PE timestamp, image base/size, variant checksum, hook/helper prologues, and the expected native main/pause page IDs. Both variants have matching relevant code and tables. The guard intentionally rejects other or modified executables. It does not rely on the executable filename, so a renamed copy with the same verified PE identity can pass.

## Behavior and boundaries

- Main page 34 draws the selected character's cover and the Wibu World logo before the native menu buttons. The 4:3 logo is drawn in an aspect-preserving rectangle bounded by 22.5% of screen width and 30% of screen height. It shifts the three main-page button X coordinates from the verified default to 140, preserving their center alignment and original Y values. It snapshots each X and restores only if it still equals the plugin's value. Other pages, including the map and settings, are not changed.
- F6 opens the main-menu-only selector panel. While it is open, the native menu input handler is bypassed so arrows/Enter cannot activate a button behind the panel. F7/F8 change character, F9 sets the favorite, F10 switches choose/random-per-launch mode (shown in the status line), F3/F4 change menu tracks, F11 mutes, and +/- changes the configured stream volume. The greeting is text and appears briefly when the custom menu opens.
- Pause page 41 draws a portrait from the selected cover's configured normalized `portrait_uv`; it does not edit the pause table. Pause navigation remains native. The page gate also skips map page 5 and settings page 33.
- Textures are loaded on demand for the selected character plus the logo. On leaving the main/pause menu, the BASS stream stops and menu TXDs are released. Music volume is applied only to this plugin's BASS stream. The plugin does not change radio state, audio-engine master/effects preferences, existing BASS global state, or radio files.
- MinHook and `bass.dll` are loaded by absolute game-root path and their loaded module paths are compared before use. They are separate dependencies and are not statically imported into the ASI. A MinHook global initialization/module reference is intentionally retained on hook setup failure because global uninitialization could remove another plugin's hooks. Every Wibu hook created before a failure is removed/disabled; rollback messages do not claim MinHook itself was unloaded.
- After the supported-executable guard and before hook installation, the ASI pins its own module with `GetModuleHandleExA(FROM_ADDRESS | PIN)`. If pinning fails, it installs no hooks. The plugin does not call engine or audio APIs from `DllMain` detach under loader lock; the pin keeps hook targets valid through process exit.

## Configuration contract

The example at `staging/project-eagle/wibu-menu/plugin/config/wibu-menu.ini.example` documents the INI format. The runtime path is `plugins\\wibu-menu\\wibu-menu.ini` under the game root. Every roster ID is compiled into the ASI in this fixed order:

`hutao, citlali, beidou, furina, yelan, kirara, raiden-shogun, mavuika, tsaritsa, clorinde, chiori, keqing, jean, mona, columbina, vesna, xiangling, lumine, barbara, ayaka, shenhe, ganyu, kokomi`.

Each `[character.<id>]` section supports `name`, `txd_path`, `texture_name`, `accent`, and `portrait_uv=x,y,w,h`. Cover TXDs use texture name `cover`, while the logo TXD uses `logo`. The audio section supports up to eight zero-based `trackN` paths and a volume between 0 and 1; the current install manifest places “A Day in Mondstadt” at index 0. Root packaging owns the completed 23-character INI and final TXD set.

## Build and static verification

Build from the workspace root with:

```powershell
& .\staging\project-eagle\wibu-menu\plugin\build\build-x86.cmd
```

The checked build completed successfully with the local VS2019 x86 compiler/linker. Validate it without launching the game:

```powershell
python .\staging\project-eagle\wibu-menu\plugin\qa\verify_build.py `
  --game-dir '.\Project Eagle\gta sa clean\gta sa clean'
```

The verifier checks both executable hashes and PE identities, native hook/helper prologues, main/pause table identifiers, source invariants, ASI architecture, static imports and the module-pin API, plus the game-root MinHook/BASS hashes, PE32 architectures, and required exports. Its machine-readable result is written to `staging/project-eagle/wibu-menu/plugin/qa/last-verification.json`.

Static verification has passed for both installed executable variants. It confirms compilation and binary/source structure only. The game was not launched, so module pinning in the loader, rendering, input suppression, music coexistence, pause behavior, device reset/lost handling, and actual TXD lifecycle remain unvalidated at runtime and must be checked by the user after parent-controlled staging/installation. The plugin makes no global render hook or device-lifecycle hook; it draws through the verified frontend call path and restores the frontend render states and CFont settings it changes.

## Evidence references

- `docs/project-eagle/wibu-menu/renderer-audit.md` records the local executable/table audit, hook ABI, and target draw ordering.
- `docs/project-eagle/main-menu-feasibility-2026-10-22.md` records initial feasibility and scope decisions.
- Official Plugin-SDK interfaces used to cross-check native structures/signatures: [CMenuManager](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CMenuManager.h), [CSprite2d](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CSprite2d.h), [CTxdStore](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CTxdStore.h), [CFont](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CFont.h), and [CAudioEngine](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CAudioEngine.h).
