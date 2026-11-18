# Genshin NPC conversation: worldbuilding and character cognition first

**Date:** 24 October 2026, Asia/Saigon. **Status:** research/design handover; no engine upgrade deployed. English-only conversation remains the product language. [Work item](../work-items/2026-10-24-codex-character-chat-lore-expansion.md).

## User correction and scope

The intended feature is conversation with people who inhabit Genshin's world. It is not a lore search interface wearing character names. Venti is an ancient Anemo Archon who also lives as a bard. In the requested post-7.1 setting he must recognize the Four Shades/Rulers, the other Archons, the Heavenly Principles and the world-scale Ronova confrontation. It is reasonable for him to lack a stranger's private biography; that is fundamentally different from failing to recognize a major divine power or global event.

The user asked whether a separate lore-research chat was needed. It is not required. Research can be delegated within this conversation and synthesized into shared project artifacts. A separate chat's findings would not automatically train the runtime model or enter the app: they still need reviewed world/character state, source provenance and behavior requirements on disk. The current conversation retains responsibility for that synthesis.

The first implementation proved transport, persistent chat memory and a local UI. Its 17-record starter corpus and generic persona instructions did not establish the intended world model. The user is correct that appending facts about a single failed question would not, by itself, fix that conceptual gap.

## Direct diagnosis of the current Venti exchange

The read-only diagnosis inspected only the relevant recent Venti turns in the local database, without instantiating the mutating store. The player asked about recent Ronova events and then identified her as the Ruler of Death. The replies said Venti had not heard of her and had not encountered such a figure in his gathered tales.

Those requests carried about 5,000 context characters, well below the prompt limit. Ronova and Istaroth were absent from the corpus. Zero lexical matches triggered a fallback to unrelated bard/identity/teapot records. The prompt then translated missing supporting text into the character's ignorance. This is a content-coverage failure compounded by a retrieval contract and characterization failure, not a capacity or input-language problem.

There is a second conceptual defect: the current instruction against claiming an encounter absent from local conversation memory can suppress the character's sourced canonical biography and established shared history with the Traveler. Local chat memory must not be the sole test of whether a canonical event occurred.

## What must exist before another implementation pass

### 1. A compact, connected world reference

Prepare reviewed definitions and relationships for the concepts necessary to this slice: the Heavenly Principles and Celestia; the Four Shades and their domains; Archons, divine seats, Authorities and Gnoses; Sovereigns; the Abyss and the Abyss Order; Khaenri'ah; Ley Lines/Irminsul and Descenders. These concepts cannot be treated as interchangeable labels.

The reference must retain causal distinctions. Losing a Gnosis, losing an Authority, destroying a divine throne, being defeated and being confirmed dead are different state changes. An in-world book's account, a character's explanation and an editorial interpretation are different kinds of evidence. Open questions in cosmology should remain open; a plausible synthesis is not automatically a settled game fact.

The initial structure can be versioned JSON/text assertions and typed relations. A graph database, a complete world simulation or model training is not a prerequisite. What matters is that the provided baseline contains enough actual meaning to answer broad questions; a flag saying `knows_four_shades: true` without their definitions/relations is not a solution.

### 2. A character's role, relationships and worldview

For Venti, preserve both the public bard and the ancient Archon. His past losses, commitments to freedom, ties to Mondstadt, relationships with major powers and responsibility toward its people affect how he reasons. A conversation about divine death should not be answered with the same cheerful music-and-breeze template as a casual walk.

Separate four decisions:

- **Recognition and baseline knowledge:** who/what he already knows and at what level.
- **Experience:** his own past, a canonical encounter shared with the Traveler, or a world event known without participation.
- **Interpretation and importance:** how the event affects his values, relationships, concerns and view of the world.
- **Disclosure:** what he chooses to say to this Traveler. Deliberately keeping a secret is different from not knowing it.

The user-required Venti baseline is a product constraint for the selected setting. Source review establishes its factual contents and detail boundaries; a missing search result must not revoke it. The same system should give Jean, Diluc and Mona different perspectives rather than either stripping all three of world awareness or giving them every private memory of an Archon.

### 3. Current world state and consequential events

Define the starting setting explicitly: post-7.1 main-story state, Traveler already known to the relevant cast. Provide a small authored update for world-scale developments, including the Ronova confrontation and its established aftermath. Venti receives this as current setting knowledge. He does not need the player to teach him that Ronova exists, and the engine does not need to invent a courier or require proof that he watched the battle.

For each event, record participants, what changed, scope of impact, what remains in effect and unresolved outcomes. The exact mechanism or tactical dialogue can be retrieved later. Global awareness is distinct from eyewitness participation; the latter distinction should refine his answer, not become another reason to deny awareness.

Separate three time axes: when content was released, when an event occurs in the fiction, and when a change becomes effective in a character's current remembered world. A release-version filter alone cannot model a later Irminsul-related change to remembered history. A chat-memory edit must not rewrite canonical world state.

### 4. Canonical history, shared story and new conversations

Maintain three distinct histories:

1. **Character biography:** Venti's own sourced past exists before the local app starts.
2. **Shared canonical story:** selected main-story encounters with the Traveler, such as the Dvalin crisis, remain true even when the local chat has zero turns. Optional quests/events require explicit progression assumptions.
3. **New interaction memory:** preferences, promises and conversations created in this mod remain private to the correct character/playthrough/branch.

Assess a player statement against the story profile. Under post-7.1 progression, the Traveler's participation in a canonical battle may already be supported. That does not verify a newly supplied date, a fabricated side story, or a claim that the same event happened to Venti. Speaker and subject still matter.

### 5. Retrieval as a detail service

Always provide the compact world baseline, character baseline and current world update. Retrieval supplies exact passages, chronology and additional supporting detail. A no-match result means that supporting detail was not found, not that an Archon has never heard of the subject.

Entity/title aliases, follow-up resolution, relevance ranking, source confidence and coverage diagnostics are still necessary. They improve access to evidence; they do not replace the world state, baseline awareness or character perspective. Do not use arbitrary private/teapot fallback records for unrelated questions. Prior model mistakes must not outrank newly reviewed canonical facts.

## Moriasmoday's role

The supplied [Venti page](https://www.moriasmoday.com/characters/venti) is a useful index of character stories, appearances and links to related world/NPC topics. The site's [Istaroth article](https://www.moriasmoday.com/npc/istaroth) explicitly credits a fan contributor, cites in-game material and contains interpretive wording. Some Venti appearance recaps are still marked for later completion. It is a community educational resource, not a completeness guarantee or an official transcript service.

Use it to discover and organize the relevant relationships and story arcs. Retain the cited game source wherever possible, keep editorial interpretation labeled and review contested claims. The same entity/source framework should eventually support major NPCs, not just playable character profiles.

For the immediate Ronova case, the source's [7.1 Act IV recap](https://www.moriasmoday.com/main-quest/snezhnaya-4) distinguishes the confrontation/defeat from the uncertain final fate, and describes the Celestial Nail aftermath. The runtime must keep that distinction while still giving Venti appropriate world awareness. It should not replace the original ignorance error with an unsupported certainty that she is dead.

## Behavior requirements for the next slice

| Probe | Required behavior |
| --- | --- |
| Ask Venti who Ronova or the other Rulers are, with detailed retrieval disabled | Recognize their major roles from the reviewed baseline; never fall back to bard-only ignorance. |
| Ask about the Ronova confrontation after 7.1 | Understand the broad event and its significance from world state; retrieve exact detail if necessary. Do not require the user to supply the premise. |
| Ask whether defeating the Ruler of Death means death itself has ended | Reason from reviewed world rules, distinguish inference from established consequences and avoid asserting unsupported metaphysical effects. |
| Ask why this matters to Venti | Respond through his long history, relationships, values and concern for Mondstadt; change tone appropriately. |
| Ask about Istaroth or the Nameless Bard in a fresh local chat | Use canonical personal history; do not treat an empty interaction DB as amnesia. |
| Ask about the Dvalin journey in a fresh local chat | Use the selected shared story profile and relationship with the Traveler. |
| Ask about a random foreign NPC's private life | Admit the appropriate gap, ask questions or infer cautiously; major world knowledge is not a dossier on every person. |
| Ask a character to reveal a secret they know | Apply disclosure/relationship policy without erasing their knowledge. |
| Tell Venti something contradicting established world state | Attribute the player's claim, ask or respond in character; do not promote it to world canon or Venti's own experience. |
| Switch to Jean/Diluc/Mona on the same global topic | Preserve shared facts while changing detail depth, priorities, stance and voice. |

Evaluate factual consistency, awareness appropriate to role, causal reasoning, story continuity, character-specific reaction, disclosure and memory boundaries. Do not call this accepted merely because the answer mentions “Ronova” or because an API call succeeds. Test paraphrases and multi-turn follow-ups, including questions whose details are deliberately absent from retrieval.

## Research artifacts and confidence

- [Worldbuilding foundation](research/genshin-worldbuilding-foundation-2026-10-24.md): connected systems and sources; uncertain cosmology explicitly noted.
- [Character awareness baselines](research/genshin-character-awareness-baselines-2026-10-24.md): four-character comparison and canon/product-setting distinctions.
- [Character cognition architecture review](research/character-mind-architecture-review-2026-10-24.md): proposed contracts, context assembly and evaluation approach.
- [Moriasmoday/Ronova source audit](research/moriasmoday-ronova-source-audit-2026-10-24.md): source type, coverage limits and uncertain Ronova fate.

These are a bounded foundation for the intended slice, not evidence that the whole Genshin storyline has been comprehensively learned, ingested or validated. Important source-attribution ambiguities must be resolved before becoming runtime facts. The next implementation should follow this reviewed model rather than expanding a name/fact list in isolation.

## Current workspace state

The service remains **v0.1.0** with its existing starter corpus. No new character-cognition system is installed. The five initially edited source/character files were restored exactly to their before-image hashes; the two provisional lore packs and edited source copies were preserved in `staging/project-eagle/character-chat-lore-20261024/research-candidate/`. That candidate has not been reviewed/validated for deployment and contains provisional metadata/content that needs review.

No user conversation or note was rewritten, no service restart performed, and no GTA/Paimon/provider/map/skin source or shared deployment metadata changed. A consistent local DB backup exists in task staging and is excluded from version control. The research handover, rather than a deployed patch, is the deliverable of this phase.
