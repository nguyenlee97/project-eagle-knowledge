# Paimon Web Test — 24/10/2026

Installed and running at **http://127.0.0.1:8765/paimon**. EaglePhone app11 has **Try Paimon on web**. Uses the existing Phone HTTP host, AI connection, Paimon persona/date rules and trusted36-message pool; no new BAT or separate permanent server.

## Use

- Choose **Sample game day** to test fictional Los Santos/portfolio context dated2010-01-01 without GTA. The sample has cash$30,000, bank$5,500, savings$2,000 and a$1,000 loan due in one day. It has no supplied EagleTimes article; Paimon must not invent one.
- **Chat only** supplies no travel/portfolio/news observations. It also starts at2010-01-01.
- **Live game context** reads the existing fresh game snapshot when GTA/Sidecar tracking is active. Stale/unavailable context is rejected instead of silently substituting a sample. Fresh live-context acceptance in an actual running game remains user QA.
- Click a suggestion to send, or use UP/DOWN then Enter. Typing returns to free text. Input follows native limits:100 printable English ASCII characters; reply160ASCII. Esc/Cancel cancels pending generation. Browser Tab keeps normal focus navigation.
- Three distinct prompts are sampled per accepted turn and remain stable while typing. Previous Paimon text stays visible. **Conversation** shows the test transcript; **New conversation** starts a separate session.

Today the existing Phone/API host is already running. If restarting the computer/host, use the existing modules from the lab directory without launching GTA:

```powershell
Set-Location 'C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab'
C:\Python310\python.exe -B -m eagle_dialogue.launcher --game-root .
C:\Python310\python.exe -X utf8 -B EagleCompanion.py
```

The first command starts/reuses the existing specific API relay/Paimon service; the second runs only EaglePhone. Open the web URL. A duplicate Sidecar exits through the existing singleton guard. The usual main game launcher remains unchanged.

## Memory, dates and scope

Test sessions use separate SQLite files in `data/project-eagle/paimon-web/sessions/`. They never write native request/command/context/UI files, the game Paimon DB or Character Chat's8952 data. Only a completed reply acknowledged as displayed is committed; cancelled/late results are discarded. Reloading the same browser tab resumes its current session while the Phone process is alive. Restarting the host expires session IDs and starts a new test conversation; old isolated SQLite files remain retained, not automatically resumed or deleted.

This tests the conversation, suggested messages and browser VN layout. It does not validate the CLEO spawn, actor/controls, exact game font or custom Lua I/O binding. Sample context is labeled and the system prompt distinguishes it from actual observations. The existing date/spoiler guards and ASCII conversion are reused; they do not erase a modern model's knowledge. Existing conversion may render unsupported smart punctuation as `?`.

## Source and transaction

- `tools/eagle-dialogue/runtime/eagle_dialogue/paimon_web.py`: loopback handler extension, bounded asynchronous model jobs, isolated sessions, context modes and acknowledgment/cancel semantics.
- `paimon_web.html`: responsive navy/gold VN page; text inserted through DOM text APIs.
- `paimon_choices.json`: generated from canonical `bridge/choices.py`;36 shared prompts.
- `build_paimon_web.py`: narrow host import/server wrapper and app11 link, based on current runtime files.
- `paimon_web_deploy.py`: fresh seven-target transaction with before-images and current-hash guards.

Applied manifest: `staging/project-eagle/paimon-web-test-20261024/manifest.json`. Targets: runtime Engine/Web UI, three new web assets/modules, Engine/Web source mirrors. This is independent of the VN-native transaction; no need to supersede or roll it back. No native bridge/HUD/skin/map/archive/provider config changes. Older full Paimon/debugger recovery must not overwrite these latest host sources.

The exact port8765 owner PID20776 was validated as EagleCompanion before stopping it; the new Phone host PID4040 was started hidden. The API relay and native Paimon service were kept running. Temporary browser QA used port18765 and a staging-only DB; that temporary host was stopped after verification. No GTA launch.

With GTA and the EaglePhone host closed, from workspace root:

```powershell
C:\Python310\python.exe -B tools\eagle-dialogue\paimon_web_deploy.py status
C:\Python310\python.exe -B tools\eagle-dialogue\paimon_web_deploy.py rollback
```

Rollback preflights all seven targets, refuses later drift, and leaves native VN files, API setup and isolated test history intact. Do not stop unrelated Python processes or the API relay as part of this recovery. Restart the existing Phone host afterward.

## Verification

128 automated checks passed, including17 web backend/HTTP tests and4 build/deployment checks alongside the107 existing tests. Candidate Python parses and browser JavaScript passes Node syntax checking. All seven installed hashes match;37 fresh protected hashes are unchanged, including native dialogue/memory/IPC, HUD, saves/settings, provider/backend and Character Chat source guards. See `qa/verification.json` and `qa/protected-before.json`.

Browser checks with the actual configured AI:

- Clicked a predefined portfolio question; reply correctly used labeled sample amounts and the loan due date.
- Typed a test picnic name **Sunflower**, then asked it back; reply remembered the name on the next turn.
- Selected a suggestion, then typed a future-year question; free typing took over and returned the2010-01-01 cutoff response.
- The installed8765 route returned a real AI greeting; completed turn was acknowledged and counted in test memory.
- Switched to Chat only; Live mode with GTA closed showed a clear unavailable/stale message, retaining the previous usable session.
- Clicked EaglePhone app11 -> Try Paimon on web, returning to the ready sample session. Screenshot: `qa/paimon-web-ready.png` (actual web page, not a gameplay screenshot).

The shared write lock is released. Work item handed back; other-agent acknowledgment is not assumed.
