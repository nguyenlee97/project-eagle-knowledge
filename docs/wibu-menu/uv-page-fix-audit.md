# Wibu menu UV and page whitelist audit

**Date:** 2026-10-22  
**Scope:** Read-only static audit of the selected Project Eagle executable and staged Wibu Menu source. No plugin, live install, configuration, or game-process changes were made; the game process was left running.

## Target and evidence

The target `Project Eagle\gta sa clean\gta sa clean\gta_sa.exe` is 14,383,616 bytes and SHA-256 `7C5A7661B2E01D64B2A9201C369F26888B8F9B38CE82C9928EF81775079240CF`. This matches the requested executable.

The executable was parsed as PE32 and disassembled offline with Capstone. `CSprite2d::Draw(CRect const&, CRGBA const&, u1,v1,...,u4,v4)` is at VA `0x728420`; its `SetVertices` helper is `0x727A00`. The ABI is interleaved UV pairs, not eight position coordinates: at `0x728420` the final stack arguments are `u1` at `[esp+0x0C]`, `v1` at `[esp+0x10]`, `u2` at `[esp+0x14]`, `v2` at `[esp+0x18]`, `u3` at `[esp+0x1C]`, `v3` at `[esp+0x20]`, `u4` at `[esp+0x24]`, and `v4` at `[esp+0x28]`. The executable's wrapper forwards them to `SetVertices`; this matches the official declarations and the gta-reversed implementation.

The helper writes the four screen positions and UVs as follows:

| UV pair | Screen vertex position |
| --- | --- |
| `u1,v1` | `(rect.left, rect.top)` |
| `u2,v2` | `(rect.right, rect.top)` |
| `u4,v4` | `(rect.right, rect.bottom)` |
| `u3,v3` | `(rect.left, rect.bottom)` |

The source's `MakeRect(left, top, right, bottom)` stores `{left,bottom,right,top}` in the actual `CRect` layout, so the vertex positions above are upper-left, upper-right, lower-right, lower-left. The important quirk is that the final two UV argument pairs are attached in the opposite order: `u4,v4` goes to lower-right, then `u3,v3` goes to lower-left. The staged source currently supplies pairs as upper-left, upper-right, lower-right, lower-left, so it swaps the two bottom corners and folds the image diagonally. Keep interleaved argument semantics and change the values to upper-left, upper-right, lower-left, lower-right. For a full non-flipped texture pass `(0,0), (1,0), (0,1), (1,1)`; for a portrait crop `x,y,w,h` pass `(x,y), (x+w,y), (x,y+h), (x+w,y+h)`.

For an uncropped logo, the safer native path is `CSprite2d::Draw(rect,color)` at `0x728350`. Its local disassembly calls the default `SetVertices` helper at `0x727420`; the reconstructed implementation supplies the canonical four-corner UVs. This avoids handwritten UV pairs for the logo.

This is confirmed by local executable disassembly and cross-checked against the [Plugin-SDK CRect declaration](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CRect.h), [Plugin-SDK CSprite2d declaration](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CSprite2d.h), [Plugin-SDK implementation](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CSprite2d.cpp), and [gta-reversed Sprite2d implementation](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Sprite2d.cpp). In gta-reversed's `SetVertices`, vertices 0/1 use `u1/v1` and `u2/v2`, vertex 2 (lower-right) uses `u4/v4`, and vertex 3 (lower-left) uses `u3/v3`.

The offline probe [uv-native-probe.py](../../../staging/project-eagle/wibu-menu/qa/uv-native-probe.py) disassembles the hash-pinned executable's `0x727A00` helper and extracts the actual stack-argument-to-vertex UV stores. It feeds those extracted assignments the distinct UV corners TL `(0.12,0.23)`, TR `(0.67,0.23)`, BL `(0.12,0.89)`, BR `(0.67,0.89)`. Correct TL,TR,BL,BR arguments reconstruct all four expected corners; the prior TL,TR,BR,BL call swaps the lower vertices. Run with `python staging/project-eagle/wibu-menu/qa/uv-native-probe.py`. This is deterministic static execution of extracted native assignments, not a game/runtime test.

## Page table and recommended explicit allowlist

The installed binary's `aScreens` begins at `0x008CE008`; screen records have stride `0xE2`. There are normal screen records for IDs 0–41. Record 34 is `FEM_MM` with `FEP_STG`, `FEP_OPT`, and `FEP_QUI`. Record 1 is `FEH_LOA` with `FES_NGA`, `FES_LOA`, and `FES_DEL`. The named record contents below come directly from the local executable; semantic labels in parentheses are inferred from their GXT keys and entries.

Recommended explicit whitelist for the requested pregame Start Game, save/load/delete, and settings surfaces:

- Main / Start Game: **34**, **1**
- New-game / load / delete / save flows: **6, 7, 8, 9, 10, 11, 12, 15, 16, 17, 19, 20, 21, 22**
- Settings and ordinary settings confirmations: **2, 3, 4, 23, 24, 25, 26, 27, 28, 33, 36, 37, 39**

Relevant records include 6–7 `FES_NGA` (new-game screens), 9 `FET_LG` (load slots), 10 `FES_DEL` (delete slots), 11–12 (load/delete confirmations), 16–17 `FET_SG` (save slots/overwrite confirmation), 19–22 (save/load confirmation or completion dialogs), 33 `FET_OPT` (options root), 3 `FEH_AUD` (audio), 4/27 `FEH_DIS` (display/advanced display), 28 `FEH_LAN` (language), 36–37 `FET_CTL` (controls), and 39 `FEC_MOU` (mouse).

Keep **page 5** out of the whitelist: it enters the map renderer. Keep **38** and **43** out: the hash-matched executable routes those control-binding/special screens through non-`DrawStandardMenu` drawing paths. Page 38 is a `FET_CTL` record without normal entries; page 43 has no ordinary record in the 0–41 table but is still a special draw case in the frontend dispatch. Page 0 is statistics, page 35 is quit confirmation, and pages 13–14 and 18 are empty/status records; they are not needed for the requested allowlist. Do not replace this explicit set with a broad range check.

The existing [renderer audit](../wibu-menu/renderer-audit.md) contains the local call-path finding that map page 5 and special pages 38/43 do not share the ordinary page draw route. Page-table labels establish what the executable contains; this audit does not claim runtime navigation or final visual behavior was tested.

## Implementation consequence

For explicit UV draws (full cover and pause portrait), keep top-left and top-right in pairs 1 and 2, then pass bottom-left in pair 3 and bottom-right in pair 4. For the uncropped logo, prefer `0x728350` with the rectangle and color. If the cover hook is expanded beyond the main page, gate it by the explicit whitelist above in addition to the frontend/game-not-loaded state, while preserving the existing map and special-page exclusions.


