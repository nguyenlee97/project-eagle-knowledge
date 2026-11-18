# Wibu Menu startup audio diagnosis

**Scope:** Read-only audit of staged Wibu Menu audio and local Project Eagle BASS evidence. No plugin, DLL, installed game file, or running game was changed or controlled.

## Finding

The leading explanation for “silent at initial main menu, audible on pause after gameplay” is initialization timing combined with one-shot failure handling:

- `staging/project-eagle/wibu-menu/plugin/src/wibu_menu.cpp` calls `StartBassStream()` once when `customMenu` first becomes true (`UpdateMenu`, around lines 643–655). It sets `gAudioAttemptedMenu = 1` before trying.
- `StartBassStream()` loads the game-root `bass.dll`, resolves stream/play/stop/free/volume exports, and immediately calls `BASS_StreamCreateFile`, then set-volume and play. It never resolves or calls `BASS_Init`.
- If the initial call fails, `gAudioAttemptedMenu` stays set while the main menu remains open. Leaving that custom-menu state resets the guard. Entering pause later is another custom-menu entry and allows one fresh attempt. This matches the reported timing, but remains a diagnosis until a runtime log captures the return/error code.
- The game’s `PECore.log` (2026-10-21 run) says `[OpcodeMgr] BASS audio functions loaded from bass.dll`; it does not establish when or whether PECore initializes BASS output. The game-root `bass.dll` is 32-bit BASS 2.4.17.41, SHA-256 `6C47E73A754FC0408E7E46A25743ED1A41017A8FA013447072E56380AEA0CE68`. Its export table includes `BASS_Init`, `BASS_Free`, `BASS_ErrorGetCode`, plus the five currently used functions. Its import table has only Windows/system libraries, no additional BASS companion DLLs.

## Recommendation for an initial-menu fix

Use a private, byte-identical BASS copy under the plugin’s own audio-runtime directory with a distinct module filename (for example `plugins/wibu-menu/audio-runtime/wibu-bass.dll`), load it by its verified full path, and keep every resolved function pointer tied to that `HMODULE`. Resolve `BASS_Init` and `BASS_Free` in addition to the stream APIs. Call `BASS_Init(-1, 44100, 0, gameWindow, 0)` (or another documented valid rate/window choice) on the private module before creating the first stream. Set an explicit, verified error path with `BASS_ErrorGetCode` when initialization or stream creation fails. Retry a failed start on later menu-process ticks with backoff, rather than consuming the only attempt for the entire menu visit.

Record an ownership flag only when this plugin’s own `BASS_Init` succeeds. At plugin cleanup, stop/free the menu stream first and call this private instance’s `BASS_Free` only when that ownership flag is set. Never call `BASS_Free` through the game-root module: PECore and other scripts load/use that instance, and freeing its output would have cross-plugin effects. Do not use `BASS_ERROR_ALREADY` as permission to free the shared instance.

A distinct basename/full-path load is a practical Windows isolation technique: it should map the private copy as a separately loaded module with separate BASS globals. BASS documentation describes initialized-device state and `BASS_Free` as instance API state, but does not explicitly guarantee that loading duplicate renamed copies is a supported isolation contract. Therefore, treat that isolation as an implementation hypothesis until verified in a controlled game run: confirm module paths/handles differ, the private `BASS_Init` succeeds, first-menu audio starts, PECore radio still works before/after gameplay, and unloading/cleanup does not stop PECore audio. The private device will still use the same OS audio endpoint, so this does not isolate device contention or OS-level audio routing.

Before shipping a copied BASS binary, confirm that the distribution/license terms permit bundling this proprietary runtime. If not, retain game-root BASS and implement a shared-instance ownership/initialization contract with PECore instead; do not independently initialize or free that shared module from Wibu Menu.

## API contract evidence

The official BASS API documentation states that `BASS_Init` must succeed before stream functions are used, that a device can already be initialized (`BASS_ERROR_ALREADY`), and that `BASS_Free` releases all resources for the selected initialized output device, including its streams. These points support both the missing-initialization diagnosis and the rule to avoid freeing PECore’s shared BASS instance: [BASS_Init](https://www.un4seen.com/doc/bass/BASS_Init.html), [BASS_Free](https://www.un4seen.com/doc/bass/BASS_Free.html).

**Evidence status:** Source and file/log evidence verified by inspection. The observed initial-menu/pause behavior was supplied by the user. The exact failing BASS call, PECore initialization timing, and the plugin-level proposed fix have not been runtime-tested. Duplicate-module isolation has since been confirmed in the local helper probe below.

## Local duplicate-module isolation probe (2026-10-21 UTC)

A narrow x86 helper probe now verifies the proposed loading arrangement on this machine without touching the game process or playing audio. Artifacts and exact result are under `staging/project-eagle/wibu-menu/qa/audio-isolation/`.

The probe loaded the game-root `bass.dll` and byte-identical staging copy `wibu-bass.dll` by full path. Windows returned different module handles and reported the expected distinct loaded paths. `BASS_Init(-1, 44100, 0, NULL, NULL)` on the private copy succeeded (error code 0), selected device 1, and `BASS_Free` on that private handle succeeded. On the game-root module, `BASS_GetDevice()` returned `0xFFFFFFFF` before and after; all six enumerated device entries had `BASS_DEVICE_INIT` clear in both snapshots. The game-root state therefore remained uninitialized and unchanged through private init/free. The DLL SHA-256 values match exactly: `6C47E73A754FC0408E7E46A25743ED1A41017A8FA013447072E56380AEA0CE68`. Probe exit code was 0.

This resolves the earlier local-isolation hypothesis positively for this exact DLL, OS, and load setup. It does not validate plugin startup timing, audio playback, other machines/Windows versions, or the runtime's distribution terms. The helper briefly initialized an output device in its own process only. See `qa/audio-isolation/README.md` and `result.json` for the invocation and machine-readable evidence.

