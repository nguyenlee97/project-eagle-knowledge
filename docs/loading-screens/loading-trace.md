# Loading screens: source and render trace

**Follow-up 14/10/2026:** [Project Wibu branding research](project-wibu-branding-research.md) resolved the earlier embedded PNG activation gap: PECore code explicitly loads resource 10/200/1033 and renders it through GDI+ / UpdateLayeredWindow. This is static evidence, not a runtime capture. The later research supersedes the resource-use uncertainty in the original bounded scan below. Current art direction and roster are in [wibu-world-art-direction.md](wibu-world-art-direction.md).

## Decisive path

The installed PC-US `gta_sa.exe` has a focused static path at `CLoadingScreen::LoadSplashes` (`VA 0x005900B0`, file offset `0x0018F4B0`). It opens the `MODELS\\TXD\\` directory, creates TXD slot `loadscs`, and loads `loadscs.txd` into that slot. It then builds seven splash entries: the first is `title_pc_US`; the other six are selected by shuffling the IDs 1–14 and formatting them as `loadsc%d`. The PC-US loader therefore displays a title texture and six randomized members from `LOADSCS.TXD`; it does not show all fourteen sequentially. The texture lookup and call sites are recorded in [the bounded disassembly evidence](evidence/gta-sa-disassembly.txt).

This settles which art source matters for the standard splash sequence: the parent dictionary `models/txd/LOADSCS.txd`. It is distinct from loose files such as `models/txd/loadsc1.txd`. The separate loose `loadsc1.txd` is a 512×512 SA portrait; the parent `LOADSCS.TXD` member `LOADSC1` is the 3840×2160 Stars & Stripes urban composition seen in the prepared preview. Root-reviewed previews also show `LOADSC4` and `LOADSC7` as 1920×1080 Stars & Stripes purple-gradient/GTA3 compositions. Those previews describe the parent dictionary’s members; do not treat the loose file as the active PC-US source. Member-level visual review came from the existing staged extraction, not a new extraction in this trace.

The startup routine at `0x005902B0` calls `LoadSplashes` (`0x005902C6`), and the state-dispatch path at `0x00748AAA` calls `LoadSplashes`, initializes the loading screen, runs title fade-in and fade-out, and cleans up. A second sequence repeats these calls. This statically connects the same splash dictionary to startup/title sequencing. Static analysis does not establish the exact first visible member or demonstrate the experience at runtime.

## Menu and 3D startup scene

`CMenuManager::LoadAllTextures` at `0x00572EC0` separately loads the frontend TXD slots. The local executable contains `frontend1`, `frontend2`, `frontend3`, and `frontend_pc` plus references to `MODELS\\FRONTEN1.TXD` and `MODELS/FRONTEN_pc.TXD`; the bundled community reconstruction names all four files `fronten1/2/3/fronten_pc`. This is the menu texture route and differs from the `LOADSCS.TXD` splash route. Community reconstructed source identifies frontend2 among the menu background resources, but I did not prove which frontend member is drawn at each menu/title state from this bounded binary trace.

`CustomStartScreenByDarkP1xel.asi` and its root INI exist. The INI has both a Position XYZ and Point XYZ vector, a pattern consistent with placing a camera in a 3D scene, but that interpretation is not verified from source. More importantly, the target’s `cleo.log` loaded-plugin summary at lines 262–286 lists the ASIs observed in that startup and does not list `CustomStartScreenByDarkP1xel.asi`; the available crash-module logs likewise do not establish that plugin as loaded. Treat it as present but inactive/unconfirmed in the captured target startup, not as the proven title/menu renderer. Do not build the art plan around it until there is a later load log or runtime confirmation.

PECore adds a separate five-second startup splash: its changelog says so, `PECore.log` records `[Splash] Starting`/`Done`, and its binary contains the caption `Project Eagle is loading`, class `PECoreSplashClass`, and embedded PNG resource id 200 at 640×640. Its imports include window and GDI+ drawing APIs. This supports a separate startup overlay window; it does not identify the PNG’s visual content or prove that the standard `LOADSCS.TXD` route is replaced. The focused PECore/Modloader_Patch scan found no direct references to the base `LoadSplashes`, `RenderSplash`, or `RenderLoadingBar` addresses, but indirect signature-based hooks remain unresolved. Details are in [the PECore trace](evidence/pecore-splash-trace.txt).

## New game, load-save, and loading overlay

The standard loading renderer is `RenderSplash` at `0x0058FF60`. It selects the current texture handle and draws it in a viewport-sized rectangle with a 5-pixel overscan margin. Fade/alpha and crossfade branches are present. `RenderLoadingBar` begins separately at `0x00590370`; the bar/text are layered drawing, not baked into the splash route by this function. The bar’s precise safe-area placement could not be established from this bounded extract, so preserve margins for UI overlays. PECore.log also confirms a loading-bar accuracy patch that changes expected files from the default 100 to 402; that affects progress accounting, while its effect on exact visible geometry is not established.

The same global `CLoadingScreen` initialization/rendering functions are called from the game’s state dispatcher. This supports reuse of the splash artwork during loading transitions, including likely new-game and save-load transitions, but I did not map every dispatcher state to a user-visible event or run the game. Treat new-game/save-load presentation details as static inference, not runtime verification.

## Active configuration and replacement implications

The target’s ModLoader config selects `Default` and sets `IgnoreAllMods=false`, `ExcludeAllMods=false` ([`modloader.ini`](../../../Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/modloader/modloader.ini), lines 4–9). Its priority list has no active overrides (lines 11–16); `_ignore` is the only ignore-mod entry (lines 17–22). `plugins.ini` explicitly sets `gta3.std.stream=0`, and the ModLoader log says `std.stream.dll` is skipped because its priority is zero (log lines 33–35). This means streamed-resource replacement must not be assumed to work here.

The log confirms `gta3.std.sprites` is loaded (lines 30–32). Its bundled documentation says it handles texture dictionaries under a `txd/` folder and gives `modloader/<mod>/txd/loadscs.txd` as an example. Thus a future replacement of the splash dictionary has a documented non-stream route, but no such artwork override appears in the current ModLoader tree/log. The `New Official Loading Themes` folder contains only eight `GENRL\\Bank_076\\sound_001..008.wav` files, and the log finds/installs only those WAVs (lines 49–57, 63–73); it changes loading music, not image artwork.

The local WidescreenFix INI sets `ResX=0`, `ResY=0`, `ForceAspectRatio=auto`, and `FrontendAspectRatio=16:9` (lines 3–8). Its comment explicitly says that frontend ratio scales frontend textures such as menu backgrounds or loading screens. The target’s CLEO module summary records `GTASA.WidescreenFix.asi` at lines 262–286, so it was loaded in that captured startup. PECore.ini enables `TransparentMenu`; PECore.log line 105 says it writes frontend-background and scaling patches, so frontend/menu rendering is modified by another active component too. The base-game splash renderer itself uses a full-viewport rectangle; WidescreenFix is intended to scale frontend/loading artwork, but neither the INI nor the bounded binary trace settles whether a particular texture is cropped, stretched, or letterboxed at the actual display resolution. Runtime geometry remains unverified.

## Candidates not established as active

- `LOADSUK.TXD`, `load0uk.txd`, `splash1.txd`, `splash2.txd`, and `splash3.txd` exist, but the traced US PC `LoadSplashes` call explicitly loads `loadscs.txd` and uses `title_pc_US`/`loadsc%d`. I did not find a proven path from those candidate filenames into this sequence; do not select them as the primary art replacement based on names alone.
- `loadsc0` is not in the randomized 1–14 set. It may belong to another locale/path; this trace does not assign it a visible startup role.
- The current ModLoader scan has no `txd/loadscs.txd` replacement. The standard `LOADSCS.TXD` in `models/txd` is the confirmed source for the traced PC-US sequence.

## Evidence status and limits

Verified from current files: Default profile and active/inactive flags; `std.stream` disabled; `std.sprites` loaded and documented; WAV-only loading-theme override; presence and config of CustomStartScreen; root WidescreenFix settings; PECore startup Splash log, embedded PNG metadata, and loading-bar patch log; existence and distinct sizes of candidate TXDs; and exact PE call/string references for `LoadSplashes`, `RenderSplash`, `RenderLoadingBar`, and frontend loading.

Static-source inference: selected six-of-fourteen random sequence and title member; parent dictionary as the splash source; frontend texture route distinct from splash; shared loading renderer likely used in new-game/load-save flows; screen-fill base rect; coordinates suggesting a 3D plugin camera.

Not verified: an in-game start/title/menu/new-game/load-save capture; CustomStartScreen plugin activation or exact implementation; actual display resolution; final WidescreenFix crop/stretch/letterbox result; exact loading bar safe area; exact ordering and timing of user-visible splash transitions.

The source references consulted are listed in [evidence/sources.txt](evidence/sources.txt). Community reverse-engineered source is supporting context, not authoritative Rockstar source. Binary snippets, offsets, and after-inspection hashes are in the evidence directory. The target was not launched, and no game data or save was changed.
