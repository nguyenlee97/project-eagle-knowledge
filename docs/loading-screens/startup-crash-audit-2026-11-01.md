# Startup crash audit — gameplay-lab

Date: 2026-11-01 (Asia/Saigon)  
Scope: read-only audit of crash logs, current Mod Loader binary/config, and startup intro files for `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`. No runtime interaction.

## Finding

The intro replacement did **not originate this crash signature**: a scan of 121 crash-log headers found the same `modloader.asi+0x9ABD` fault, with `modloader/.data/config.ini` as the last file loaded, in multiple pre-install logs. Examples include 2026-10-31 20:27–20:29 and 2026-11-01 00:43–00:44, all before the clips were installed at 14:21 local. The available evidence therefore excludes the two clips as the origin of this recurring failure mode. The primary fault is in `modloader.asi` while initialization is still in its basic-config / command-line phase. The current Mod Loader log has only `Loading basic config file modloader/.data/config.ini` and `Parsing command line`; crash metadata names that config as the last file loaded and `MinHook.x86.dll` as the last library loaded. Mod Loader fails before the game reaches its normal startup movie playback path. This is a phase/order inference from the log plus game startup architecture, not live execution tracing.

The exact fault RVA `modloader.asi+0x9ABD` decodes to `cmp dword ptr [esi], 0`. Immediately preceding instructions set `esi = eax + 0x6c`, where `eax` is returned by a helper; the access violation therefore occurs while reading an object field during Mod Loader initialization. The native crash dump does not include the faulting memory address or page state, so it does not establish whether the object was invalid due to corruption, lifetime, or another cause. Static disassembly is included in `../../../staging/project-eagle/startup-crash-investigation-20261101/agent-evidence/modloader-rva-9abd.txt`.

The 14:32:37 exception should be treated as secondary. The pre-intro 14:03:05 log already has the same `std.data.dll+0x16F6DD` access-violation signature during `ExitProcess`/`RtlExitUserProcess` teardown after the primary exception. It is not new evidence implicating the intro clips.

## Evidence and limitations

- 14:32:26: `modloader.asi` base `0x5EAC0000`, EIP `0x5EAC9ABD` (`+0x9ABD`), access-violation read; log says last file `modloader/.data/config.ini`, last library `MinHook.x86.dll`; Mod Loader log stops at command-line parsing.
- Backtrace addresses resolve to Mod Loader return addresses (`+0xBE71`, `+0xC1B8`, `+0xD06BC`, `+0xDB9A5`, among others). The first fault is within loader initialization; the call chain alone does not identify a source-level function.
- The 121-header index also contains multiple pre-install instances of the exact primary `modloader.asi+0x9ABD` signature (including 2026-11-01 00:43:25, 00:43:37, 00:44:02, and 00:44:26), all with `modloader/.data/config.ini` last loaded. The 14:03:05 pre-install exception at `std.data.dll+0x16F6DD` and 14:32:37 exception share the same secondary teardown signature; both stacks pass through `LdrShutdownProcess`, `RtlExitUserProcess`, `ExitProcess`, and `PECore`'s exception-reporting path. The module bases differ because the two logs are from separate processes.
- Current `modloader/.data/config.ini` is 156 bytes and retains its 2026-10-13 mtime, consistent with the supplied unchanged-config observation. Hashes for current loader, config, clips, executable, WibuMenu, and MinHook are in `../../../staging/project-eagle/startup-crash-investigation-20261101/agent-evidence/input-hashes.json`.
- Current `.asi` hashes identify observed files only; without before/after hashes for Mod Loader, MinHook, plugin set, and full startup inputs, this audit cannot determine why the loader fault began today or whether another mod/configuration state contributed. Correlation does not establish causation.
- No game process was launched, attached, or controlled. No runtime files were changed or restored. No claim is made that either replacement movie successfully played or completed.

## Conclusion

Subsequent user feedback on 01/11/2026: the user attributed the crash to opening multiple game windows and confirmed the intro test passed. This is the user's runtime finding; the agent did not reproduce or independently isolate the multi-instance condition. No crash fix was applied.

The recurring primary crash is demonstrably pre-existing: the same Mod Loader RVA and last-file signature occurred repeatedly before the intro change. The 14:32:26 instance also happens in Mod Loader initialization, before the startup movie stage, so the two replacement clips are not supported as its cause. The repeated `std.data.dll` exception is likewise a pre-existing teardown signature. The underlying Mod Loader fault remains unidentified; no A/B test or game execution was performed, so this does not settle whether the clips could affect some distinct later-stage issue. No changes or restoration are authorized by this report.
