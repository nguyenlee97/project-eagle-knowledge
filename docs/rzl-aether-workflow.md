# RZL-Trainer custom player skin workflow (Project Eagle)

Checked 13 October 2026. Read-only inspection of the selected Project Eagle directory; the game was not launched and no skin was installed. This note records the local trainer's built-in workflow as a candidate for a future Aether install. It does not establish that any particular Aether asset has a compatible rig or will work correctly in gameplay.

## Finding

The installed RZL-Trainer build has a dedicated ModLoader actor selector under the player-change menu. Its embedded help tells the user to put both a DFF and TXD in `modloader\RZL-Skin`, and its embedded validation strings enforce the local seven-character naming limit and reject a period in the name. This is direct evidence from the local build, independent of the newer v5.0.1 listing.

For a candidate playable Aether model, the intended menu path is **Player Options > Change Player > ModLoader Actors**. The section is explicitly under Change Player, rather than the separate nearby-ped modification feature. The trainer's own strings name the feature “ModLoader Actors”; “Modloader Skin” is wording used by some release listings.

## Use if/when an asset is approved for installation

1. Confirm the skin archive contains a GTA San Andreas player-compatible DFF and its matching TXD. The local trainer says to put both files in `modloader\RZL-Skin`; its scanner contains the `*.dff` pattern, which indicates it discovers candidates by DFF name. Pair each DFF with a TXD using the same basename. The shipped folder currently contains only `.File Name Rules.txt`, so there is no example asset to verify nested-folder behavior; keep the pair directly in the designated folder unless the trainer is later tested and shown to support subfolders.
2. Keep the basename to at most seven characters, do not put a dot in the basename, and do not use `~`. The shipped rules warn that tilde can crash the game when opening the list. The allowed-character list is in the rules file.
3. Open the trainer (INI default F2), then navigate to **Player Options > Change Player > ModLoader Actors** and choose the model. The local INI assigns Enter to accept, Backspace to go back, and arrow keys to navigate. The creator's later v5.0.1 release notes also list F2/Ctrl+R, Enter/Num5, Backspace/Num0, arrows, and page keys, but local key bindings are the source of truth for this build.

The cleanest practical basename for the candidate should be short, such as `AETHER` (6 characters), but do not install it until the asset has been reviewed and a recovery copy prepared.

## Reverting and persistence

The local menu data includes **Normal Actors > 000_DEFAULT** (`RZL-Trainer.cs`, embedded GXT strings near file offset `0x1EBEAF`–`0x1EBF0B`). This strongly indicates a built-in return-to-default player choice, expected to restore the normal CJ/player model. That behavior has not been exercised in game, so treat it as a static-code indication rather than a verified recovery operation. A backup/recovery route should still be prepared before any future install.

Static files do not establish whether a selected ModLoader actor persists after loading a game save, survives restarting the game, or is serialized into a save. `RZL-Trainer.ini` has no obvious selected-skin persistence setting; the local code has a separate `Save Game` menu, but its presence does not show that the chosen skin is saved. Resolve this only with a controlled in-game test after installation is authorized: select skin, save, reload save, exit/restart, and check whether it remains selected; also verify `000_DEFAULT` restores CJ.

## Evidence from the selected local installation

Installation root: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`.

- `cleo\RZL-Trainer.ini:6-27`: menu key defaults: `ShowMenu=113` (F2), `Accept=13` (Enter), `Back=8` (Backspace), and arrows for navigation.
- `cleo\RZL-Trainer.ini:288-289`: local version/config section is `[Version 5.CBT1.3]`, not a claim that this is release v5.0.0 or v5.0.1.
- `cleo\RZL-Trainer.cs`, offset `0x1BAD06` onward: embedded menu strings `Player_Options_>`, `Change_Player_>`, `Change_Player`, `Normal_Actors_>`.
- `cleo\RZL-Trainer.cs`, offset `0x1EBE1B` onward: embedded GXT keys and values include `rzpo1=Change_Player_>`, `rzchp0=Change_Player`, `rzchp1=Normal_Actors_>`, `rzna1=000_DEFAULT`.
- `cleo\RZL-Trainer.cs`, offsets `0x1C4B85`–`0x1C4CC2`: `+_ModLoader_Actors_>`, `ModLoader_Actors`, validation messages for dot and maximum length 7, “put DFF and TXD in folder `modloader\RZL-Skin`,” and “ModLoader not installed yet!!!”.
- `cleo\RZL-Trainer.cs`, offset `0x23BC42`: embedded path `modloader\RZL-Skin`; offset `0x23BC5C`: `*.dff` scan pattern.
- `modloader\RZL-Skin\.File Name Rules.txt:1-12`: allowed characters, maximum length 7, no dot in name, and tilde warning. The directory currently has no DFF/TXD assets.
- `modloader\modloader.asi` and `modloader\RZL-Skin` are present in this installation. The existing loader is ModLoader 0.3.7 per the installation inventory.
- `cleo\RZL-Trainer\Portable Clothes.ini` concerns individual clothing body parts; it is a distinct feature and not the full-player skin selector described here.

## Creator's release documentation

The author's [RZL-Trainer v5.0.1 listing on LibertyCity](https://libertycity.net/files/gta-san-andreas/222412-rzl-trainer-v5-0-1-cheat-menu.html) identifies `muhammad_herizal` as author and describes changing skins via ModLoader, Add-On, and Skin.img. Its controls section documents F2/Ctrl+R to open/close and keyboard navigation. This listing is for v5.0.1, while the local config says 5.CBT1.3; use it as creator-authored context, not proof that every release feature or control applies to this local build. The more relevant local proof is the embedded selector/help strings listed above.

## What remains unverified

No in-game confirmation exists for successful model loading, persistence through save/restart, restoration to CJ, player animation/weapon/vehicle compatibility, or compatibility with the eventual Aether model. A matching DFF/TXD pair and a selectable menu item would establish loading/selection only; they would not prove the player rig works across walking, running, combat, weapons, swimming, climbing, and vehicle use.
