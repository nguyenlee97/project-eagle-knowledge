# Eagle Dialogue / Paimon current state

**25/10/2026 — Paimon Agent installed:** web/native can read and operate validated EaglePhone actions through the actual Engine, with durable wallet/receipts, isolated Sample wallet, Chat only and fresh Live wallet modes. Input8192/full output16384; native220-character pages. The19-target guarded transaction is applied; cash9057/bank5500/savings2000/loan0 and three pending tickets preserved;12 protected hashes unchanged. GTA was closed during install and was not launched. Native gameplay acceptance remains pending. Agent functions use the existing Luna credential/model with reasoning none on Chat Completions; chat-only retains configured effort. Read [current handover and recovery](paimon-agent-2026-10-25.md) and [work item](../work-items/2026-10-25-codex-paimon-agent.md). Sections below describe earlier revisions; the old no-tools,100/160 and45-second limits are superseded by this slice. Current native turn timeout150 seconds.

**25/10/2026 — GPT-6 Luna:** Paimon web/native now use `gpt-6-luna` directly through OpenAI, matching the referenced NPC chat. Dedicated secret-free profile: `data/project-eagle/paimon/connection.json`; same existing external credential reference, low reasoning,1200 completion-token cap. One actual response passed in about2.77s;32 focused tests and2010 guard passed. Memories/UI unchanged. [Current AI handover and config recovery](paimon-luna-2026-10-25.md).

**24/10/2026 — Paimon Web Test installed and browser-verified:** http://127.0.0.1:8765/paimon, or EaglePhone app11 -> **Try Paimon on web**. The VN page uses the same AI/persona/2010 rules and36 prompts, supports typing/selection/cancel/history, and has chat-only, labeled sample and read-only live context modes. GTA is not required for sample/chat. Test memory is separate from game/Character Chat data. 128 automated checks pass; actual AI portfolio/memory/date/browser flow tested. Native gameplay QA below is still pending. [Web handover/startup/recovery](paimon-web-test-2026-10-24.md).

Current web transaction: `staging/project-eagle/paimon-web-test-20261024/manifest.json`, seven targets in Engine/Web/new web modules/source mirrors. It is independent of the native VN transaction; preserve both. Use `paimon_web_deploy.py` for web recovery with GTA and Phone closed. Shared lock released.

Native section updated23/10/2026, Asia/Saigon. **User reports the base Paimon feature works. Native visual novel HUD and randomized choices are installed; gameplay testing remains user-owned.** Services start through the existing launcher; no GTA launch by Codex.

## Use

Open the existing `Project Eagle/gta sa gameplay-lab/Start_Eagle_Lab_With_Sidecar.bat`. In game: **F7 -> 11.Paimon -> choose a row with I/K -> F9**. J/L on the home grid reaches app 11. The same app is available on the web Phone.

Rows: Call Paimon & talk; Check my portfolio; What should we do?; Today's EagleTimes. The Phone closes before spawning/opening native dialogue. The new visual novel panel shows Paimon's reply, three random choices from 36 English prompts and a separate typing field. UP/DOWN selects a suggestion, Enter sends; typing switches to free input, Backspace edits, TAB ends the conversation and removes only the owned Paimon instance. Enter advances a completed reply early; input also resumes after six seconds with the reply retained. Ctrl+Shift+Y and EAGLETALK no longer summon the actor. No separate game launcher. See [VN HUD implementation and recovery](vn-hud-2026-10-23.md).

Paimon is currently an on-demand conversation companion, with one ephemeral actor per call. Walking/following, vehicle companionship, voice and ambient-NPC takeover are not implemented by this slice.

## Character and context

Reuse live model **48295 / VC_DIAZ01**, directly verified to contain the smaller Paimon `d499aba3cfcc` library DFF/TXD pair. No skin mapping or archive modification. Stable memory identity is `paimon`; it is independent of the model and disposable ped handle. Native spawn queries nearby ground, applies a stand-still task and allows 600ms physics settling rather than freezing a new actor. Visual height/idle still needs user testing.

English personality prompt: lively, curious, food-loving, cheeky and loyal to Traveler. No voice clone or later release/game meta knowledge. Observed context includes coarse locations/nearby POIs, on-foot/vehicle state, vitals, current fictional game portfolio, current-date EagleTimes and nearby activity candidates. It starts recording after real RAM attachment and clock sync, not the engine's placeholder starting coordinates. It does not reconstruct unobserved history.

Loan overdue/due-soon and margin-versus-cash reminders are deterministic, based on actual game balances. They use the existing notification banner with throttling; model text does not execute trades, cheats or arbitrary game actions.

## Game date, news and memory

The calendar starts **2010-01-01**. Every model request receives the current game date, not the PC date. News uses only EagleTimes for that day. Political headlines use exact-date entries; yearly themes are excluded because they may reveal later events in the same year. Crypto stories are rebuilt from eligible current-date assets instead of exposing future coin seed prices. Future-year/dated text and known later topics/assets are filtered from context and checked in questions/replies. No external/live news or web tool is connected.

These are grounding and spoiler guards, not a mathematical erasure of a modern model's prior knowledge. Unknown implicit anachronisms remain a user-evaluation concern. Missing dated news is reported as unavailable rather than replaced with a generated headline. Availability floors for some assets are conservative and may omit an asset near its release.

Local SQLite `cleo/EagleDialogue/paimon.sqlite3` stores observed changes and accepted turns. It persists across calls and backend restarts, with bounded storage. A changed native bridge epoch (new game/load/restart) or rewound clock forks a new timeline. Old branches remain stored but are not silently merged into the active save. Save-slot identity/automatic cross-load memory reconciliation is future work; do not advertise uninterrupted memory across arbitrary saves. Cancelled/stale turns are not saved as completed conversations.

## AI connection

Runtime/source `eagle_dialogue/paimon_config.json` reference the secret-free `data/project-eagle/paimon/connection.json`, read afresh per request. It pins **OpenAI / gpt-6-luna**, low reasoning and1200 completion tokens, reusing Character Chat's named existing external credential. Character Chat and old relay profiles are untouched. Previous Groq/opencode selection is historical; see [Luna handover](paimon-luna-2026-10-25.md) for the current profile/transaction.

The game launcher starts/reuses the Paimon service. Its optional18082 relay startup runs only when that exact local provider is selected; the current direct OpenAI profile skips it. The caller reads only the named credential variable (including its per-user value for stale inherited environments); no key is in dialogue config or logs. It does not automatically fail over to another provider/model.

The caller uses text Chat Completions with bounded context/history, no executable tools, a maximum 35-second transport timeout inside the native 45-second turn deadline, and rejects failed/tool/incomplete responses. It has no mock fallback. Errors show in Phone status and `cleo/EagleDialogue/service.log`/`paimon_status.json`.

## Verification

Current revision: 107 offline tests passed, including native choice/key/snapshot tests and Lua5.1 parser/liveness/layout/scoped recovery coverage. Installed renderer/full HUD/source HUD compile under Lua5.1; five transaction hashes match and 28 protected files, including four save/settings files, are unchanged. Actual game font/input/appearance remains user QA. The offline layout PNG uses approximate fonts and is not a gameplay screenshot.

The custom ASI's Lua I/O exposure is not established by stock-interpreter QA; existing debugger source references `io.open`, but host initialization source was unavailable. Include successful live snapshot rendering in the user's acceptance test.

Earlier base verification had 87 checks, live Phone app11/backend heartbeat and API caller verification. That evidence is historical, not a claim that a game/service process is currently running.

The user subsequently said everything works before requesting these UI enhancements; record the base Paimon feature as user-reported working, without inferring exhaustive lifecycle testing. This VN HUD revision has not been accepted in game. Codex has not launched GTA for this task.

## Deployment, ownership and recovery

Current transaction: `staging/project-eagle/paimon-vn-hud-20261023/manifest.json` (applied), superseding the earlier Paimon transaction. Five targets: native bridge, new renderer, current runtime HUD, source HUD and prior manifest pointer. It preserves Antigravity's debugger wrapper and refreshes the stale source HUD from runtime; one preexisting radar helper's C-style delimiters are normalized to valid Lua without changing its calculation. The previous Paimon transaction installed the backend/app11 and retains its original before-images. The Lab launcher/bootstrap is unchanged.

With GTA closed, from workspace root:

```powershell
C:\Python310\python.exe -B tools\eagle-dialogue\vn_hud_deploy.py status
C:\Python310\python.exe -B tools\eagle-dialogue\vn_hud_deploy.py rollback
```

Rollback restores only these five targets and refuses later external changes. It preserves SQLite, context, logs, API setup, Engine/Web/debugger/map sources and launcher. Older Paimon/repair/pilot recovery layers refuse superseding ownership; earlier full Paimon rollback also encounters later debugger drift and must not be used over current features. Do not restore whole game/source directories or apply old map/localization source backups over the hooks.

Antigravity: preserve app11, Paimon hooks/import, VN draw hook/module and launcher bootstrap. Use the latest runtime HUD/source mirror and transaction, not old backups. The model appearance is reused, not owned as a global skin slot. Shared write lock is released. See [VN HUD work item](../work-items/2026-10-23-codex-paimon-vn-hud.md) and [original Paimon work item](../work-items/2026-10-23-codex-paimon-companion.md).
