# Renderer and menu hook audit (Project Eagle)

**Captured:** 2026-10-22  
**Scope:** Read-only inspection of the selected clean-folder install, existing local evidence, and Plugin-SDK references. No game process was launched and no game/core/config/art/audio file was changed. The existing Project Wibu PNG+caption was left intact.

## Target identity and method

The selected executable is the original GTA SA 1.0 US HOODLUM build by exact hash: `gta_sa.exe`, 14,383,616 bytes, SHA-256 `7C5A7661B2E01D64B2A9201C369F26888B8F9B38CE82C9928EF81775079240CF`. This matches the supplied baseline. `gta_pe.exe` has the same size and SHA-256 `F115B49C5AC3A8FCEDB00EE216730B2A6F573AFE4908B2AC328A9CC2B9D0DCB3`. `PECore.asi` is 3,151,360 bytes, SHA-256 `4C3B891061D773B095C52B4CD87A1C1FC1A5FBFD40533AF707046D929B861560`.

I found no PECore, `menupatch`, or CustomStartScreen source in the searched workspace / ProjectEagleModPack trees. REA tools were not registered in this session, so binary work here is ordinary bounded static analysis with the already-installed `pefile` and Capstone Python packages, not an REA result. The address/call evidence below is from the hash-verified executable and the installed plugin bytes; there is no new runtime observation.

## Main, pause, map, and loading render paths

Plugin-SDK maps `FrontEndMenuManager` to `CMenuManager* 0x00BA6748`. Its useful fields are:

| Field | Address expression | Use |
| --- | --- | --- |
| menu active | `FrontEndMenuManager + 0x5C` | Menu visibility state |
| drawing radar/map | `+0x59` | Map/radar display flag |
| game not loaded | `+0xE9` | Main-front-end versus in-game pause gate |
| current menu page | `+0x15D` | Page-specific gating |
| background sprite index | `+0x1B50` | Current background sprite |

The current-page value `5` takes the map path: the local `CMenuManager::DrawBackground` assembly calls `PrintMap` at `0x00575130` when page is 5. For reliable main/pause separation, check `m_bGameNotLoaded` and `m_nCurrentMenuPage`, then explicitly skip map pages.

The local call chain is:

- `CMenuManager::DrawFrontEnd` at `0x0057C290`, called from `0x0053E82D` and `0x0053EB8C`.
- `DrawFrontEnd` tail-jumps to `CMenuManager::DrawBackground` at `0x0057B750`.
- `DrawBackground` draws its background, calls `PrintMap` at `0x00575130` for page 5, then calls `CMenuManager::DrawStandardMenu(bool)` at `0x005794A0` from `0x0057BA58` from the normal page path (special pages `0x26` and `0x2B` use other draw functions).

**Best layering candidate for a full-screen main-menu image:** a pre-original hook on `DrawStandardMenu` (`0x005794A0`), guarded by `m_bGameNotLoaded`, so the custom background is drawn after the engine background and before normal menu foreground. This call order is directly visible in the local executable. Do not draw after `DrawBackground`: its normal menu drawing is already complete by return, so a full-screen overlay can cover the buttons. This is still a static hook recommendation; its appearance and hook coexistence must be checked by the user in-game.

Plugin-SDK also maps `CMenuManager::LoadAllTextures` to `0x00572EC0`. The local function loads the frontend dictionaries through the path/slot strings at `0x008651B4..0x00865240`, including `MODELS\\FRONTEN1.TXD` -> `frontend1`, `MODELS/FRONTEN_pc.TXD` -> `frontend_pc`, and the `frontend2` / `frontend3` slots. The separate base-game loading artwork is `CLoadingScreen::LoadSplashes` at `0x005900B0` using `models\\txd\\LOADSCS.TXD`; that is not the frontend-menu texture path. Existing local evidence identifies `fronten2.txd` as the likely menu-background dictionary, but states that the exact texture's contribution to Eagle's 3D title scene has not been runtime-verified. Replacing a loading TXD will not replace a menu background.

Source references: [Plugin-SDK CMenuManager.cpp](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CMenuManager.cpp) and [Plugin-SDK CMenuManager.h](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CMenuManager.h). These supply the class-global and method mappings; direct-call ordering above was disassembled from this install's hash-matched executable.

## Existing menu components and activation evidence

- **PECore TransparentMenu:** `PECore.ini` has `TransparentMenu = true`; the saved `PECore.log` lists `TransparentMenu` under enabled features. The current `PECore.asi` contains a logger string stating that it installs `CHudDraw` and `RsMouseSetPos` hooks and writes frontend-background/scaling patches. The current log does not print those hook target addresses or an individual success line, so exact patch sites and live visual effect remain unverified. Treat CHudDraw/mouse handling and frontend sizing as occupied/shared surfaces; prefer the menu-specific hook above over a second HUD or D3D EndScene overlay.
- **RadioEx menu integration:** current PECore binary strings and log identify the menu hooks at `0x005746F0` (`PrintRadioStationList`) and `0x00507000` (`GetRadioStationName`); the log says “Menu hooks installed successfully.” This is radio-name/station-list integration, not evidence of a separate main-menu BGM hook. The Eagle v1.3 changelog describes radio names/sprites in the pause menu as visual-only.
- **`plugins\\menupatch.asi`:** present, 2,048 bytes, SHA-256 `6ED7573D23504C27463DF12CAC938470871C2CE93C197FD37ED35B59D822C247`. Its entire executable section disassembles to a small startup patch: it copies a 0x48-byte table to game memory `0x008D0444..0x008D048C`, clears `0x90` bytes at `0x008D048C..0x008D051C`, and sets bytes at `0x008CE47B=1`, `0x008CFD33=2`, `0x008CFEF7=3`. The copied records visibly contain `FEP_RES`, `FEH_MAP`, `FEP_OPT`, and `FEP_QUI`; they appear to be the four pause-menu entries, though that meaning is inferred from the string IDs. Preserve this table and flags; do not replace the surrounding page/screen data.
- **Activation status for the two nested plugins is unknown:** `plugins\\CustomStartScreenByDarkP1xel.asi` and `menupatch.asi` are present, and the CustomStartScreen INI contains its camera/point coordinates. The most recent saved `cleo.log` plugin summary (2026-10-22 04:06) lists 16 root-level ASIs but lists neither nested plugin. That does not prove no other loader can load them, but there is no plugin-specific success log or other affirmative activation evidence in the inspected files. The CustomStartScreen binary is packed/opaque under ordinary string scanning (56,832 bytes; imports only LoadLibraryA/GetProcAddress/VirtualProtect), so this pass could not resolve its hook target or determine which scene it selects.
- **BASS/audio availability:** root `bass.dll`, `ogg.dll`, `vorbis.dll`, `vorbisFile.dll`, and `vorbisHooked.dll` are present. PECore logs its RadioEx startup and menu hooks, but also warns that `audio\\pe\\radio\\static.mp3` failed to load. File presence does not establish that BASS playback works. The radio list/sprite in the pause menu is visual-only according to the Eagle changelog; no evidence in this audit establishes a custom main-menu music path.

## Implementation constraints

1. Keep the new full-screen artwork draw on the pre-original `0x005794A0` path, gated to the not-loaded main menu; leave pause, map (page 5), and normal in-game UI alone.
2. Use RenderWare/menu rendering in the existing frontend path, with viewport/scaling behavior checked on the target aspect ratio. PECore and WidescreenFix both affect frontend sizing; D3D EndScene is already a shared PECore surface.
3. Do not overwrite `0x008D0444..0x008D051C` or the three menu flags without understanding the existing `menupatch` behavior.
4. Keep the frontend TXD route (`fronten1/fronten2/fronten3/fronten_pc`) distinct from `LOADSCS.TXD` loading art. Do not disturb the installed Project Wibu PNG+caption while preparing the separate menu artwork.
5. The user's own in-game check is required to settle whether either nested plugin is loaded, whether the custom start scene is visible, and whether the chosen hook behaves correctly under TransparentMenu and the active aspect-ratio settings.

## Follow-up: audio, input gate, and shipped menu-table geometry (2026-10-22)

### Native frontend/loading audio

The local executable hash above is still the target. Official Plugin-SDK and gta-reversed `CAudioEngine` surfaces expose `IsLoadingTuneActive()` at `0x00506D90`, `StartLoadingTune()` at `0x00507410`, and `ServiceLoadingTune(float)` at `0x005078A0`; neither declares a `StopLoadingTune` method. The local `IsLoadingTuneActive` entry is a thunk that adds `0xB4` to `this` and jumps to the frontend audio entity routine at `0x004DD470`. The reconstructed implementation returns `m_FrontendAE.IsLoadingTuneActive()`. `StartLoadingTune` posts `AE_FRONTEND_LOADING_TUNE_START` then services the sound manager. The reconstructed frontend-idle state machine starts it only at `GAME_STATE_LOADING_STARTED`, after the menu has closed and game loading begins; that is not evidence of a native main-menu theme.

`ServiceLoadingTune(0.0f)` is not a targeted stop: reconstructed code sets the audio hardware **effects fader** to the requested factor and services the sound manager; it only rate-limits increases by `0.005` per service call. `SetMusicMasterVolume(int8)` at `0x00506DE0` changes the global music master scaling (`volume / 64`), so it would mute/change other music too. Keep custom menu music on its own BASS stream and stop that stream on the native-menu close edge. Do not call the effects fader or global music volume as a substitute for a targeted stop. The boolean query at `0x00506D90` is a possible passive predicate, not a stop API.

### Native menu input and close observation

Plugin-SDK maps `CMenuManager::ProcessUserInput(char down, char up, char enter, char exit, char input)` to `0x0057B480`. Its local 1.0 US entry is a thiscall method (`ECX = self`), has five one-byte stack arguments and returns `void`; both the short bypass and normal epilogue use `ret 0x14`. The one direct call site found is `0x0058061B`. A custom overlay that owns input can skip the original method only while its panel is open (return without forwarding); outside that state it should call the original with all five arguments unchanged. This blocks arrows/Enter from navigating the native menu while the overlay is active.

`CMenuManager::Process` at `0x0057B440` is declared `int` by Plugin-SDK and is called from `0x0053BF44` in the game processing path and `0x0053E7A5` in frontend idle. Preserve its original call/result, then inspect `FrontEndMenuManager.m_bMenuActive` at `0x00BA6748 + 0x5C` for the menu-close edge and stop the plugin's own BASS channel there. `SwitchMenuOnAndOff` at `0x00576B70` is named `CheckForMenuClosing` in gta-reversed; the local bounded direct-call scan found no direct `E8` xref, making it a weaker close callback than the confirmed recurring `Process` entry. The `Process` call cadence and close-edge timing are statically established only; runtime timing is untested.

### Actual native page and text placement

The local executable table is `aScreens` at `0x008CE008`, with `CMenuScreen` size `0xE2` and 12 entries of 18 bytes (matching Plugin-SDK's packed structure). Main-menu root is page 34 (`FEM_MM`, record at `0x008CFE0C`): its entries are Start Game / Options / Quit Game. First item position is `(320, 170)` with align value `3` (center); following entries store zero X/Y and center alignment, so the native root menu stacks centered around the screen midpoint rather than sitting in the left quiet area. Pause menu is page 41 (`FET_PAU`, record at `0x008D043A`); its base first entry is `(320, 140)`, align `3`.

`menupatch.asi` copies `0x48` bytes to `0x008D0444`, exactly page 41's first four 18-byte entries, then clears the following `0x90` bytes (eight more entries). The copied runtime coordinates are `FEP_RES` `(320,170)`, `FEH_MAP` `(320,200)`, `FEP_OPT` `(320,230)`, and `FEP_QUI` `(320,260)`, all align `3` (center). Thus the current pause list comes from that plugin patch, not the original seven-entry page; preserve `0x008D0444..0x008D051C`. A main-menu-only layout can be adjusted through page 34's entry X/Y/alignment fields or at draw time; snapshot the original values and restore them on plugin detach, and gate the change strictly on page 34. Do not modify page 41, map page 5, or settings page 33. The exact visual placement under PECore TransparentMenu / widescreen remains subject to the user's own in-game check.

Sources: [Plugin-SDK CMenuManager.h](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CMenuManager.h), [gta-reversed MenuManager.cpp](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/MenuManager.cpp), [gta-reversed AudioEngine.h](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Audio/AudioEngine.h), [gta-reversed AudioEngine.cpp](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Audio/AudioEngine.cpp), and [gta-reversed WinMain.cpp](https://github.com/gta-reversed/gta-reversed/blob/master/source/app/platform/win/WinMain.cpp). Page geometry, xrefs, and entry argument/return ABI above were checked against the installed hash-verified executable; official source supplies names/layout declarations and the audio implementation semantics. No game was launched and no game files were edited.
