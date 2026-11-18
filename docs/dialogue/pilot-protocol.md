# Eagle Dialogue pilot IPC v1

All files in `cleo/EagleDialogue/`, separate from Phone state and RAM mailbox. Single native bridge writer for request.ini, single mock-service writer for response.ini. ASCII English wire/display; backend Python keeps text as Unicode internally. One outstanding turn per session.

`request.ini` [request] keys: protocol=1, service_epoch (positive int32 copied from current response), bridge_epoch (persisted positive int32 incremented on every script instance, random fallback only on first creation), target (owned ped handle), seq (positive int32 turn/cancel sequence), kind (talk or cancel), text (ASCII <=100 bytes, printable, no ~ or line breaks), commit. Persist the new epoch before enabling the bridge; this avoids replaying the same game RNG after loading a save. Publish commit=0 first, then all payload keys, then commit=seq last. Service requires stable double-read bytes, commit==seq, current service_epoch, bounded strings and positive IDs. Duplicate request identity is ignored.

`response.ini` [service]: protocol=1, epoch (positive random int32), heartbeat (integer counter).

[response]: bridge_epoch, target, seq, status (ready, complete, cancelled, error), text (ASCII <=160 bytes, no user format codes), code. Service writes a temp file then atomic replace with bounded retries. Native validates service epoch plus bridge_epoch/target/seq before displaying. Read seq both before and after reading text and revalidate IDs; do not accept torn snapshots. Restart service gets a new epoch; pending turn fails/cancels rather than accepting stale response.

Native cancels on TAB, invalid/dead player/NPC, phone opening, or deadline. Restore only player control acquired by this pilot and delete only its own fixture. Cancel publishes a new seq with kind=cancel; text may be empty or the bounded printable placeholder `cancel` and is ignored (avoids native empty-string INI ambiguities). Service invalidates pending generation and must never deliver old text to another target. Service uses a bounded async worker for mock delay, can continue polling cancel while generation is pending. No model/audio dependencies in mock.

Game bridge startup/read loop must tolerate missing service. CTRL+SHIFT+Y arms the bridge; activation waits until all three keys are released, then retries task readiness for up to two seconds. Typed EAGLETALK is an alternative. Require player controllable/on foot and Phone closed. Guard rejections are visible and recorded; 03EE is not equivalent to ordinary controllability. Enter submits, TAB closes, Backspace edits. Do not intercept F6/F7/F11/F12. If Phone opens during dialogue, close and release the pilot. In-game testing belongs to the user at their request.


## Current Paimon Phone command channel

The Paimon bridge replaces the keyboard pilot at the existing single script path. `command.ini` [command] contains protocol=1, bridge_epoch, positive seq, action1..4, commit=seq. Phone closes its mailbox before atomic publication. Native double-reads identity/payload/commit, ignores duplicates/stale epoch, polls idle at10Hz and reports command_seq/tick_ms in bridge.ini. The four actions open empty input or submit the portfolio/activity/today-news preset through the same request/response v1. Ctrl+Shift+Y/EAGLETALK paragraphs above describe the historical pilot only. Paimon uses a45s native turn timeout and a<=35s HTTP timeout. Phone opening, TAB or actor/player invalidation cancels and restores only owned control. User tests the actual game.

## Visual novel display channel, 23/10/2026

Native writes `ui.dat` as14 LF-terminated plain-data lines: `EAGLE_DIALOGUE_UI_V1`, bridge_epoch, UI_revision, tick_ms, numeric_state, selected0..3, choice_id1, choice_id2, choice_id3, input<=100ASCII, accepted_reply<=160ASCII, repeated_revision, repeated_epoch, `END`. Trusted1-based IDs refer to the build's36-prompt pool; only states2/3/4 render. Publish at<=10Hz while active and on transitions/startup/cleanup. Lua rejects incomplete/mismatched/invalid data, requires an advancing writer before initial adoption and expires stale state after1.5s of HUD DeltaMS. User/model strings are never executed. Request/response/command IPC remains unchanged. [Full VN contract and recovery](vn-hud-2026-10-23.md).
