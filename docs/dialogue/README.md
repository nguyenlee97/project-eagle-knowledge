# Eagle Dialogue knowledge base

**04/11 — NPC Character Chat successor entry point:** [Complete handoff](character-system-full-handoff-2026-11-04.md) and [copyable next-chat prompt](character-system-successor-prompt-2026-11-04.md). Covers the standalone v0.3.3 engine, 10 Mondstadt profiles/Oz, lore/cognition/memory/evaluation, asset conversion, and the subsequently integrated Persona/Contacts runtime. User reports successful game operation. Read the bridge-capacity prerequisite before adding character 11. Older Paimon status below is a separate subsystem.

**25/10: [Paimon now uses GPT-6 Luna](paimon-luna-2026-10-25.md)** for web and native turns, through an independent secret-free profile using the same existing OpenAI credential reference as Character Chat. Model/low-reasoning/1200 cap verified with an actual reply; memories and game/UI files preserved.

**24/10: [Paimon Web Test](paimon-web-test-2026-10-24.md)** is running at http://127.0.0.1:8765/paimon through the existing EaglePhone host. Sample/chat modes work without GTA; live context is read-only and requires fresh tracking. Actual AI and web flow verified; test memory is isolated. [Latest work item](../work-items/2026-10-24-codex-paimon-web-test.md).

Target: gameplay-lab. Owner: Codex. Conversation and new UI use English.

Current feature: **Paimon through EaglePhone app11, now with a visual novel HUD and three random conversation choices from 36 English prompts**. Contextual AI, memory, portfolio and game-date EagleTimes remain in place. User reports the base feature works; new UI gameplay testing belongs to the user.

- [VN HUD and choices](vn-hud-2026-10-23.md) — current renderer, controls, tests and guarded recovery.
- [VN work item](../work-items/2026-10-23-codex-paimon-vn-hud.md) — latest source/transaction ownership.

- [Paimon work item](../work-items/2026-10-23-codex-paimon-companion.md) — current source and transaction ownership.
- [API provider handover](opencode2api-handover.md) — separate task owns connection/credentials; read the latest section.
- [Current state](current-state.md) — installed/build/runtime verification and shared-file ownership.
- [User validation](../work-items/2026-10-23-codex-dialogue-user-validation.md) — basic native/mock loop confirmed; fixture presentation and next slice.
- [Development diary](development-diary.md) — dated decisions and evidence.
- [Pilot protocol](pilot-protocol.md) — independent file IPC contract.
- [Integration design](../npc-dialogue-integration-plan-2026-10-22.md).
- [Current repair work item](../work-items/2026-10-22-codex-dialogue-launcher-fix.md).
- [Initial pilot work item](../work-items/2026-10-22-codex-dialogue-pilot.md).

Read shared-agent-workflow and current work items before editing. Paimon hooks are now in the latest localized/map-fixed Phone/Sidecar/HUD and mirrored source. Preserve app11, the hooks and launcher bootstrap. Do not restore older Engine/HUD source over them.
