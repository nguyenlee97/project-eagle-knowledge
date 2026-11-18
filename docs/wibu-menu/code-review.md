# Wibu menu plugin: static code review

**Follow-up:** user runtime evidence exposed a UV argument-order error that this initial static review missed, plus missing first-menu BASS initialization. The corrected binary mapping and offline regression are in `uv-page-fix-audit.md`; audio isolation evidence and the staged revision are in `audio-start-fix-audit.md` and `render-audio-fix.md`. The build described below remains the initial installed revision, not the staged fix.

**Reviewed:** 2026-10-22  
**Scope:** Read-only review of the staged C++ plugin and built ASI. The game was not launched; no live process or installed game files were modified.

## Reviewed snapshot

| Artifact | SHA-256 | Evidence |
| --- | --- | --- |
| `plugin/src/wibu_menu.cpp` | `D915675424EC469A944426307B9EE847410FA0FE500D0F5378F10690AB1677D8` | Recomputed during self-pin revision review; matches `qa/last-verification.json` |
| `plugin/build/WibuMenu.asi` | `6351BE8B59F64153565D6D81336DCA141C262DBDC552142F73D69EA3DE503D51` | Recomputed during self-pin revision review; matches `qa/last-verification.json` |
| Target `gta_sa.exe` | `7C5A7661B2E01D64B2A9201C369F26888B8F9B38CE82C9928EF81775079240CF` | Matches original Eagle baseline |
| Target `gta_pe.exe` | `F115B49C5AC3A8FCEDB00EE216730B2A6F573AFE4908B2AC328A9CC2B9D0DCB3` | Matches verifier's second supported PE variant |

The ASI is x86 PE32 (machine `0x14C`, optional-header magic `0x10B`), has ASLR/NX flags, and imports only `kernel32.dll` and `user32.dll`; MinHook and BASS are loaded dynamically from the game root. The revision delta from the previous reviewed snapshot is the `GetModuleHandleExA` declaration/import and a self-pin guard in `PluginInitThread`, placed after executable validation and before any hooks install. It calls `GetModuleHandleExA(0x5, address-of-PluginInitThread, &pinnedModule)`: `0x5` combines `GET_MODULE_HANDLE_EX_FLAG_PIN` (`0x1`) with `GET_MODULE_HANDLE_EX_FLAG_FROM_ADDRESS` (`0x4`). A failed pin exits without installing hooks. `qa/last-verification.json` reports static checks only and `runtime_validated: false`.

## Findings

- **Hook ABI matches the inspected executable.** `CMenuManager::Process` at `0x0057B440` is `int __thiscall(self)` and the hook forwards and returns the original result. `ProcessUserInput` at `0x0057B480` is `void __thiscall(self, char down, char up, char enter, char exit, char input)` with callee cleanup `ret 0x14`; the fastcall thunk preserves those arguments, returns early only when the custom main-menu panel owns input, and otherwise forwards them unchanged. Static call-site evidence and executable prologues are recorded in `renderer-audit.md`.
- **Page gating is scoped to the intended screens.** Main artwork and the optional overlay require `m_bGameNotLoaded` and page 34; the pause portrait requires in-game page 41. Map page 5 and settings page 33 are not selected by those gates. Only page 34's three root-menu X fields are shifted to 140, with guarded restoration when leaving that page. The `menupatch.asi` page-41 table at `0x008D0444..0x008D051C` is not written.
- **The native menu remains in front of the main artwork.** The background draw is before the original `DrawStandardMenu` at `0x005794A0`; transient panel/portrait drawing is after it. Sprite/rectangle calls use the local executable's verified entries and CRect layout. The code restores the captured CFont scalar state after overlay text and calls `SetFrontEndRenderStates(this)` (`0x00573A60`) after custom RenderWare draws. This restores the expected frontend baseline, not a snapshot of every possible D3D/RenderWare state; composition with PECore TransparentMenu and the actual aspect ratio still needs the user's in-game check.
- **TXD ownership appears balanced in the reviewed paths.** Successful custom TXD loads are AddRef'd once; release deletes the sprite, removes that reference, then removes the slot. Failed loads remove the allocated slot without a reference release. Cover swaps release the previous sprite/slot before loading another. This is a static ownership trace, not a runtime resource-lifetime test.
- **Menu audio is isolated from native global audio controls.** The plugin starts/stops/frees its own BASS stream and does not call `ServiceLoadingTune(0)` or `SetMusicMasterVolume`. Native `IsLoadingTuneActive` at `0x00506D90` is a query, not a stop method; `ServiceLoadingTune` affects the effects fader. The post-original `Process` hook observes menu close and stops the BASS stream even when draw callbacks cease. BASS playback and transition timing were not runtime-tested.
- **Executable and helper identity checks are narrow and useful.** The loader checks PE32 identity/checksum plus prologues for all three hook targets and the used renderer helpers, then validates the expected page-34 table strings and geometry. This is a compatibility signature guard, not a full file-hash check; a binary that differs in a way outside those checked bytes can still pass. Conversely, this intentionally rejects other editions/modified executables.
- **Hook-install rollback removes this plugin's hooks.** The reviewed failure branches remove created hooks and disable already-enabled hooks. MinHook is deliberately retained after failure; this avoids globally uninitializing a shared MinHook instance and disturbing hooks owned by other plugins. Log messages now make that retained state explicit.

## Remaining constraints

Final integration follow-up (root, static): the installed revision changes only
the logo rectangle to preserve the actual 1448x1086 PNG's 4:3 aspect ratio and
appends random/favorite mode feedback to the existing selector status. The
verifier was rerun successfully. Installed source SHA-256:
`1abff6de2c5a0dbf6eaf1284db0888f0041895d2f04b1e39fd1fb4db9b3188ac`;
ASI SHA-256: `7fa4b33ddd6204df35c576ef43521b627c231cadaa1eb61a66087a196256f834`.
The snapshot table above refers to the independently reviewed self-pin revision;
the final UI-only delta was inspected during integration. Runtime remains untested.

`DllMain(DLL_PROCESS_DETACH)` still does not unhook, stop BASS, release TXD resources, or restore page-34 coordinates. Once the init thread successfully pins the module, an ASI loader cannot unload it before process termination; that addresses the dangling-detour risk during gameplay and makes runtime unload unsupported by design. The pin occurs asynchronously after `DllMain` returns, so there is a short startup window before it succeeds; the ASI loader must retain the just-loaded module through that window. No explicit detach teardown is needed for the normal process-exit path. Pin behavior is established from the Windows API contract rather than a game runtime test.

The current executable includes PECore and other frontend modifications. The inspected evidence did not identify a conflicting hook on `DrawStandardMenu`, but CustomStartScreen activation and runtime hook coexistence remain unverified. No automated static test can establish visible placement, input feel, audio audibility/ducking, or stability under PECore; those are reserved for the user's own test.
