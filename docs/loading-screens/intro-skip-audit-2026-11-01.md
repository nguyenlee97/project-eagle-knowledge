# Startup intro clip skip audit — gameplay-lab

Date: 2026-11-01 (Asia/Saigon)  
Work item: [Loading/artwork refresh — mục đầu: bỏ video intro gốc](../work-items/2026-11-01-codex-wibu-startup-intros.md)  
Scope: read-only audit of `movies/Logo.mpg` and `movies/GTAtitles.mpg` in `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.

## Finding

**Do not move or rename the two files by themselves as a skip mechanism.** The exact lab executable returns from failed video playback but its startup state machine still enters a playing state. Automatic progression is driven by the DirectShow `EC_COMPLETE` event. If the movie is missing or cannot be rendered, that event is not established by the code path; the game can remain at the blank startup screen until input advances it.

No supported setting found in the installed lab configuration bypasses both movie states. `SilentPatchSA.ini` has `SkipIntroSplashes=1`; that skips the EAX/NVIDIA splash screens only. `cleo/starsandstripes/pe_database.ini` has `SKIPTOGAMEMODE = 1`, which selects the game mode after frontend startup and does not skip these movies. The current files/config do not expose the reverse-engineered FastLoader options `NoLogo` or `NoTitleOrIntro`.

## Evidence from the target executable

Target: `gta_pe.exe`, SHA-256 `ddf6456c9a1173b179db3ca67acef3f59e1a6fc8ddaa15737f5153ba545bd684`. This is offline PE32/x86 disassembly using installed `pefile` and `capstone`; no game or Sidecar was launched.

- At VA `0x748AFA`, startup passes the embedded `movies\\Logo.mpg` path to `VideoPlayer::Play` at `0x747660` (`CALL` at `0x748B00`). Immediately after return, VA `0x748B08` writes startup state `2` (the logo-playing state in the matching reverse-engineered state map).
- The title branch passes `movies\\GTAtitles.mpg` at `0x748BEC`, calls `VideoPlayer::Play` at `0x748BF9`, then VA `0x748BFE` writes state `4` (intro-playing state).
- In `VideoPlayer::Play`, failed HRESULT branches lead to the common function epilogue. The caller does not test a success result before setting state `2` or `4`.
- The target's `OnGraphNotify` at VA `0x745FB0` processes event code `1` and transitions state `2 -> 3` or `4 -> 5`, then disables the graph notification. The matching source identifies this event as DirectShow `EC_COMPLETE`. The source `WinMain.cpp` handles the playing-logo and playing-intro states by waiting for user input if the completion callback has not advanced them.

Primary source cross-checks from the GTA:SA reverse-engineering project (the binary addresses above were inspected in the lab executable itself): [VideoPlayer.cpp](https://github.com/gta-reversed/gta-reversed/blob/master/source/app/platform/win/VideoPlayer/VideoPlayer.cpp) and [WinMain.cpp](https://github.com/gta-reversed/gta-reversed/blob/master/source/app/platform/win/WinMain.cpp). The source reimplementation is corroboration; conclusions about the state writes and failure branches above come from the target PE.

## Current assets and configuration

| Lab file | Bytes | SHA-256 | Parsed stream info |
| --- | ---: | --- | --- |
| `movies/Logo.mpg` | 22,363,833 | `930EDB051BAAEEB208A6163FB6C9B0FAA17D9F25AA34BCB3634AF7EB2AA8DC6C` | MPEG program stream; MPEG-1 video 1920×1080, 25 fps average, MP2 stereo 48 kHz; 18.639 s |
| `movies/GTAtitles.mpg` | 65,921,024 | `4B865D251BB99AF7BDB9746EC12086F37301D9F1FA1062A7D232D58117400A07` | MPEG program stream; MPEG-1 video 1920×1080, 59.94 fps, MP2 stereo 44.1 kHz; 91.302 s |

Stream properties and durations were read with `ffprobe`; this confirms file structure, not successful playback in this session. `SkipIntroSplashes=1` is present in `SilentPatchSA.ini`. Both files remain unchanged in the lab.

## Lower-risk route if the goal is to show Project Wibu art

A short valid replacement at each existing path can preserve the native playback/completion path, avoiding an executable patch or new ASI hook. Matching the observed MPEG program stream with MPEG-1 video and MP2 audio is a reasonable candidate format, but this is an **inference**, not a proven codec/duration requirement: the engine only calls DirectShow `RenderFile` then `Run`; neither the target nor source specifies a minimum duration or a validated profile for newly encoded clips. An extremely short clip could still be rejected by DirectShow or appear as a flash. Build candidates in the registered task staging, preserve the originals with guarded hash-checked backups, and do not claim success until the user confirms the first startup in-game.

If the requirement is a true no-video jump directly into Project Wibu, the installed configuration does not provide that path. It would need a separately scoped and reviewed state-skip mechanism. This audit does not authorize or implement one.

## Verification boundary

- Read-only target inspection only: executable hash/disassembly, config search, movie SHA-256 and `ffprobe` metadata.
- No files in `movies/`, configs, executable, artwork, or deployment metadata were changed. No game/Sidecar launch or live playback test was performed.
- Static behavior establishes that move-only is not a safe automatic skip; whether a replacement clip decodes and reaches `EC_COMPLETE` in this environment remains unverified.

**Audit complete; handed back to the parent task for implementation planning.**
