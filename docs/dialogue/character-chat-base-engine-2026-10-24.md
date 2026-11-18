# Character Chat base engine — standalone English prototype

Delivered **24 October 2026**, Asia/Saigon. [Work item](../work-items/2026-10-24-codex-character-chat-base-engine.md). User confirmed English only and authorized implementing the base engine without touching GTA.

## Result

The local Conversation Studio runs at **http://127.0.0.1:8952**. Start with [Start_Character_Chat.bat](../../../tools/eagle-character-chat/Start_Character_Chat.bat). [Tool README](../../../tools/eagle-character-chat/README.md) includes usage, API boundaries, test commands and stop/status instructions.

- Four stable characters: **Venti, Jean, Diluc, Mona**.
- **48 adapted English choices**, 12 per character, in validated branching graphs. Choices have sources and explicit `adapted` labels; these are original prototype dialogue, not imported verbatim game scripts.
- Free chat uses the existing selected Groq-hosted model through the configured loopback relay. No mock response path exists in the application; provider doubles occur only in automated tests. No provider selection or credential changes.
- Persistent SQLite memory scoped by profile/playthrough/branch/character. Recent turns, FTS5 topical recall beyond the recent window, extractive summaries with source IDs, and editable player-reported notes.
- A graph choice and its full reply enter the same transcript used by a free-form follow-up. Display acknowledgement commits the turn and advances the graph; cancelled, failed and undelivered replies are excluded from recall. Retry IDs prevent duplicate turns, including after a graph advance.
- Explicit playthrough creation and checkpoint forks. Branches inherit eligible committed exchanges and note versions at the chosen checkpoint. These are standalone journeys, not automatic GTA save detection.
- Curated lore retrieval with source references and release/character filtering before ranking. Content snapshot ceiling **7.1**, but only **17 selected Mondstadt records** are present; full 7.1 story ingestion has not been delivered.
- English UI supports character selection, adapted choices/free input, cancellation, note editing, exchange forgetting, source traces and journey controls. Compact windows expose Memory/Journey as drawers.

## Files and ownership

New isolated tool: `tools/eagle-character-chat/**`. The main controller, store, retrieval and provider adapter are Python modules under `eagle_character_chat/`; `static/` is dependency-free HTML/CSS/JavaScript. `content/` contains four character packs and the world/source manifest. All paths are separate from Paimon, map and game runtime sources.

Persistent local state: `data/project-eagle/character-chat/conversations.sqlite3`, its SQLite side files and the owned studio process/log files. No install/build in gameplay-lab, no archive/skin/HUD/launcher/game-save modification and no GTA launch. The studio launcher may start/reuse the **existing selected** provider relay as a dependency; stopping the studio leaves that shared provider running.

Connection is read from the existing secret-free `staging/project-eagle/opencode2api-20261023/connection.json`. Only the named environment credential is read, including the current user's Windows value when inherited environment state is stale. Keys are not copied into the tool, content, database, logs or QA output. Free chat sends selected character context/history to that provider; local storage does not mean offline inference.

Codex owns the new tool. Luna subagents prepared only `content/**` and `static/**` in separate scopes; both handed back those files before final parent edits. Antigravity's M1 Phase 2 ownership remains unchanged. No shared game-write lock was acquired. The original design document now records the user's English-only clarification.

## Validation and evidence

Evidence directory: `staging/project-eagle/character-chat-base-20261024/`.

- **33 automated tests passed**, using temporary databases and a test-only loopback HTTP provider. Coverage includes graph state/ack, restart persistence, scope isolation, checkpoint inheritance and note versioning, old-topic retrieval, cancellation/stale results, request deduplication, forgetting derived notes/traces, privacy filtering, full transcript length, HTTP host/origin/CSRF controls, rejected tool/incomplete API responses, redacted upstream errors and missing credentials.
- JavaScript syntax and PowerShell launcher parser checked. HTTP tests verify actual HTML/JS/CSS serving and exchange/fork routes.
- Real configured API: `live-v2/live-results.json` contains eight bounded checks: four persona responses, own nickname recall, cross-character isolation, scripted-to-free follow-up and Diluc's drink grounding. `live-v2/reviewed-results.json` re-evaluates saved output with English punctuation normalization; **8/8 transport/basic-behavior spot checks pass**. This is not an exhaustive characterization or lore evaluation.
- Live QA revealed a nickname subject reversal and Diluc improvising alcohol consumption in the first pass. Memory prompt now distinguishes Traveler/NPC subjects. Diluc persona, policy, lore and a graph branch now include sourced grape-juice/alcohol preferences. The later replies use Traveler's nickname correctly and ground Diluc's drink preference. The initial results remain in `live/` as evidence.
- A generated Jean reply still misspelled “Knights of Favonius”; this remains a model-quality limitation. Grounding/filtering and a source trace do not prove that every model sentence is canon-correct. Richer content and broader evals remain future work.
- Browser QA in the in-app browser at a compact viewport verified character selection, separate test journey creation, scripted reply -> acknowledgement -> graph advance, source drawer, note creation/edit, note absence on Jean, and a real UI free-chat response correctly recalling the edited mint-tea note. Reload and studio restart preserved the stored journey. The default user journey was left separate from synthetic QA.
- **10 protected source/runtime/provider/config files unchanged** by SHA-256; final content/source manifest recorded in `verification.json`. These are scoped checks, not a hash scan of all GTA files.

## Runtime behavior and limits

English only. Input limit is 2000 characters and memory-note limit 500; this prototype does not inherit GTA's 100/160-character transport limits. Full replies are stored, not cut to a HUD buffer.

Provider calls are text-only, nonstreaming, have <=35-second transport timeout and four bounded worker slots. Cancel cannot terminate an already-running remote inference request, but its late result is discarded and cannot enter acknowledged memory. There is no automatic paid failover. Adapted graph choices remain usable when the API is unavailable.

Memory notes are deliberately conservative: direct edits and `Remember: ...` create player-reported notes. Other conversations remain searchable without speculative extraction. Summaries are extractive topic aids rebuilt from acknowledged source turns. A corrected note takes priority over older statements, while older transcript remains inspectable.

Forgetting an exchange clears it and its derived note/search/trace copies in that branch. Later independently spoken messages or previously forked branches may retain mentions; removing a note alone does not erase its source conversation. This is recall management, not secure deletion from backups/SQLite disk pages. Restart preserves ready replies for later display acknowledgement and cancels interrupted pending requests.

No embeddings/vector service is required for this small starter corpus. Lexical recall has expected paraphrase/alias limitations. Canon release/character filters are deterministic, but faithful use of filtered facts and restraint about model-pretrained knowledge remain model-evaluation concerns.

## Handover / next phase

The engine slice is complete and usable for local conversation trials. Next work can expand the four content packs, import reviewed game dialogue trees and build a question-based character evaluation set. Full world synopsis/detail coverage through 7.1 requires a separately verified source snapshot and ingestion pass.

Game integration is later: an owned placement manager, proximity/focus interaction, shared UI arbitration with Paimon and a compatible paginated HUD transport. Named-NPC identity must remain independent of skins/handles. Read the latest M0/M1 and Paimon ownership/recovery handovers before registering those files. Existing skins were not converted or deployed in this task.

Stopping/removing standalone code does not require a GTA rollback. Preserve local SQLite state, and use a consistent SQLite backup before any future schema migration. No existing game/provider/Paimon rollback script should be run to remove this tool.
