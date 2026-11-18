# Copy into the next chat — Mondstadt Character Chat continuation

```text
Workspace: C:\Users\LENOVO\Desktop\GTA (Windows/PowerShell).
You are taking over expansion of the working Genshin NPC feature in Project Eagle.
The user reports the existing in-game integration is successful. Product UI/chat must remain English only. Do not start over or replace the engine with a generic persona prompt/RAG wrapper.

Read first:
1. AGENTS.md and docs/project-eagle/shared-agent-workflow.md (current dual-lock rules), latest project README/work items.
2. docs/project-eagle/dialogue/character-system-full-handoff-2026-11-04.md
3. tools/eagle-character-chat/README.md
4. docs/project-eagle/mondstadt-persona-chat-and-contacts-2026-11-04.md INCLUDING section6 follow-up, and eaglephone-ui-v6-and-touchscreen-2026-11-04.md.
5. The current source-snapshot.json at staging/project-eagle/character-system-handoff-20261104 as a dated baseline; verify current source/config before edits.

Current state: Character Chat v0.3.3; Venti, Jean, Diluc, Mona, Kaeya, Lisa, Klee, Barbara, Noelle, Fischl. 120 original adapted choices. Oz accompanies Fischl in dialogue and as object6702; one Fischl memory scope. Current engine/content is tools/eagle-character-chat; game adapter is Project Eagle/gta sa gameplay-lab/eagle_mondstadt_chat_bridge.py. The adapter imports shared Engine/content and workspace conversations.sqlite3 directly. Studio8952 is optional and is not the model endpoint. Current default safe provider config is OpenAI direct/gpt-6-luna, despite a relay URL in an older integration report; credentials stay in the existing named external environment reference. Never repeat keys or dump env/registry.

CRITICAL: The current CLEO MCHT protocol is sized for TEN NPCs. Handle array128+idx*4 and pointer array168+idx*4 overlap at idx10; headings212/216 also occupy later space. Do NOT simply append an11th actor. First plan a coordinated/versioned layout/capacity expansion and rebuild both sides using the generator at staging/project-eagle/mondstadt-persona-chat-20261104/build_world_assets_and_bridge.py. The .cs is compiled CLEO, not C#. Preserve existing indices/IDs/state and handle protocol mismatch safely.

The next scope is more Mondstadt characters. Sucrose was still outstanding from the user's original request. A physical ready DFF/TXD pair Sucrose__ca0ffa6c91af exists under D:\GTA Archive\Skin Library\Project Eagle\numbered-skins\raw; inspect current catalog/pair/rig/appearance and existing static alchemy-room placement before conversion or live placement. Do not assume a new ped ID is free. Get the concrete next batch from the user's accompanying instruction; this handoff alone does not choose a large roster.

Preserve: always-loaded world/character foundations, canonical biography vs shared story vs new chat memory, role-appropriate awareness/disclosure, optional progression gates, no retrieval-match => no detailed evidence (not identity amnesia), attributed old transcripts, strict locally checked evidence envelope, 20k context budget, character/branch memory isolation, idempotency/reset/cancel behavior. New profile needs characters/<id>.json + cognition/<id>.json + roster/entities/sources/tests; private records characters:[id]. One curated post7.1 world slice is not comprehensive lore ingestion.

Research game profiles/VO/teapot/quest text, official sources and community-hosted primary transcripts. Use Moriasmoday as discovery/secondary synthesis and trace important claims back to scenes. Record inaccessible pages as inaccessible. Source-review uncertain outcomes; do not turn defeat into confirmed death or reported knowledge into eyewitness history. Independent Luna subagents can research disjoint character/asset/audit packets; coordinator alone merges shared files. Run a single serial paid-call queue with synthetic DB, >=10s cooldown plus observed quota budgeting; no auto retry or separate paid verifier calls.

Asset work: prefer existing ready GTA ped pairs. The DAE/Oz converter produces static objects, not rigged peds. Preserve every original surface face, alpha/mips, meaningful normals/UV/material seams; no triangle-stride deletion or coarse welding. Read back DFF/TXD, visually compare and keep source/hash/count evidence. Current Oz is a static hover prop with scripted bob, not animated flight AI.

For game integration also update Python/CLEO rosters, protocol/capacity, peds.ide/archive assets, placement/area/GPS/dedup, six512px expressions + icons, fixed Contacts10/16 counts, current HUD/touch UI and tests. Preserve accepted UI/font/alpha fixes and other agents' runtime changes. New in-person and remote DM must use the correct same character/branch memory; the game currently picks bootstrap default branch. Note that current adapter auto-acks ready turns before presentation updates, so do not claim confirmed display ACK for all game paths.

Create a scoped work item and fresh staging/backup/manifest. Heavy build/research/offline synthetic tests outside locks. Use tools/eagle_coord_lock.py for shared source/runtime writes and exclusive game/sidecar/realDB/input operations; no ad-hoc locks or global process kills. Do not use the real conversation DB, unlock state or saved game as a test fixture. Rebase changes onto current source and recheck hashes immediately before authorized apply. Do not run old rollback/build/apply scripts unchanged or restore whole shared directories.

Start by inspecting current state, identifying any changed authority since handoff, and presenting the concrete next-batch/protocol approach. Then execute the scope authorized in the user's new request, with evidence-based offline/live-model/in-game verification and an updated handoff. Do not ask again for actions already authorized, but do not infer game deployment permission from a research-only request.
```

Full supporting context and evidence links are in the [handoff](character-system-full-handoff-2026-11-04.md). This prompt creates no chat, changes no memory and launches no process by itself.
