# Character Mind Architecture Review — 24 October 2026

**Status:** architecture proposal; no implementation or canon-pack approval.  
**Scope:** review the restored Character Chat 0.1.0 baseline and propose a bounded world-understanding model for Venti within the four-character roster. No game, provider, content, database, UI, or engine changes were made for this review. No provider or external service was called.

## Executive finding

The user is right that a character cannot be made convincing by placing lore documents in a retrieval index. Retrieval can supply a passage when a topic matches. It does not, on its own, give a character a durable sense of who they are, what they already know about the world, what recent events changed, why those events matter, or how they would react from their own values.

The active 0.1.0 engine has a small Mondstadt synopsis, per-character persona and knowledge-policy strings, four query-ranked lore records, recent/recalled conversation, and branch-scoped personal notes. This is a useful conversation harness, but it has no explicit durable world model, character awareness ledger, dated event state, causal links, or news propagation. A prompt instruction can discourage a particular error, but it is not a substitute for those inputs.

The proposed design keeps a compact, reviewed world model and character-specific cognition available independently of topic retrieval. Retrieval then adds supporting detail. For the requested Venti slice, the fixed context should include his reviewed identity and role, a small but explicit model of Archons / the Four Shades / the Heavenly Principles, a source-reviewed model of his relationship to Istaroth, and an explicit 7.1 Ronova event state with actual facts and causal relations—not only flags saying that he “knows” these topics. The candidate tree refers to an Istaroth encounter, but it is not active content and this review does not validate that claim as canon. The shared authored world-state update should make the Ronova event available to Venti as a **global story fact in this conversation setting**, per the user's requirement, without making him an eyewitness or claiming an in-world broadcast occurred. Keep that setting source and any canon evidence separate.

This does not require a complete Teyvat simulation or a comprehensive 7.1 corpus. It requires a small, coherent model for the concepts and events the prototype intends to discuss, plus clear uncertainty where that model has gaps. The model's facts and causal summary must be included in runtime context; a flag or a prompt saying “Venti knows Ronova” cannot substitute for the definitions and state needed to discuss her.

## Review basis and evidence boundaries

I reread the active engine, content loader, store and content files after the source restore described in the current work handover. The active engine reports version `0.1.0`; `content/world.json` declares snapshot `7.1`, describes a curated Mondstadt starter pack, and contains 17 records. Its always-present `synopsis` covers Mondstadt as the City of Freedom and the Knights of Favonius as its public protectors. Venti's persona and knowledge policy are prose fields in `content/characters/venti.json`, not a structured mental model.

The active `Engine.context()` supplies that synopsis, up to four retrieved lore records, recent turns, recalled exchanges, up to ten manually maintained notes and extractive summaries. `Content.retrieve()` first filters by character eligibility and release version, then ranks by lexical overlap, falling back to character-only records when there is no lexical match. The current record model has no typed awareness, evidence confidence, causal relation, event status, salience, or news-delivery field. As a result, the model may receive details about a named entity without receiving the character's stable relation to that entity or a dated account of what changed in the world.

The store already provides useful separation for player interaction: sessions and turns are keyed by branch and character; memories are branch- and character-scoped; turns become committed on display acknowledgement; summaries are extractive and traceable to source turn IDs. Those are interaction-history facilities. They should not become the only source of character continuity or be confused with canonical biography. In the active 0.1.0 system prompt, the rule against claiming a meeting absent from *conversation memory* is too restrictive: it can suppress canonical personal history or shared main-story history with the Traveler/Aether. Presence in this local chat transcript is not the test for whether a sourced canonical encounter happened.

The prior design already recommends keeping persona, canon knowledge, world snapshot and personal memory separate, and avoiding the assumption that “present in a corpus” means “known or willingly disclosed by a character.” This review makes the missing world-state and cognition pieces concrete.

The preserved `staging/project-eagle/character-chat-lore-20261024/research-candidate/` tree is read only here as failure-analysis material. It is not active content, a deployment proposal, or independently verified canon. It contains useful distinctions such as `world_report`, an uncertain Ronova final status, and a warning against giving Venti eyewitness memories of the Snezhnaya confrontation. It also illustrates why coarse labels alone are insufficient: a record marked `characters: ["*"]` and `awareness: "world_report"` can be retrieved for every character, but does not say which character actually received which report, when they received it, or what they infer from it. Candidate source labels include official material, game transcripts, and community summaries; the claims have not been re-audited against those sources in this document.

**Evidence versus canon:** the facts above describe local files and their declared metadata. They do not certify every lore claim in those files as canon. In particular, this review does not independently verify the Four Shades taxonomy, the 7.1 Ronova sequence, whether that sequence is globally reported in Teyvat, or what Venti personally knows. Those require source-level review before representing them as established canon.

## Design target

The system should answer from a stable character mind assembled from several distinct layers:

1. **Identity and role baseline:** who the character is, public versus private identity, relationships, responsibilities, goals, and enduring commitments.
2. **Durable world model:** a small structured set of entities, concepts, relations, rules and consequences that the character can reason with even when no exact lore paragraph is retrieved.
3. **Character awareness and belief:** which world facts the character knows, how they know them, what they believe or suspect, and what they do not know. “Not established in this pack” must not silently become “the character has never heard of it.”
4. **Dated event state:** what happened by the selected story snapshot, where, to whom, what is confirmed, what remains unresolved, and which consequences persist.
5. **Authored world-news update:** a small dated update to the shared story state, available to the conversation cast without requiring an eyewitness or a simulated rumor network. Its scope is this application's setting; it does not claim that every in-world citizen heard a broadcast.
6. **Canonical personal history:** events in the character's own life, with sources and timeline conditions. This stays distinct from shared main-story history with the Traveler/Aether and from local chat interaction history.
7. **Canonical shared history with the Traveler:** character-specific main-story encounters that the selected starting story state says occurred, even if this local chat is new. Optional quests and events need explicit progression flags rather than being assumed complete.
8. **Traveler relationship memory:** acknowledged promises, preferences and new shared moments created in this conversation, scoped to this character and playthrough, with provenance and correction/forgetting behavior.
9. **Retrieval details:** topic-specific evidence that enriches an answer, never the sole mechanism that defines identity, worldview, or current event status.
10. **Disclosure, tone and objectives:** what the character chooses to say, in what voice, and what conversational purpose guides a response.

The response should emerge from combining these layers: *what happened → what the character understands about it → why it matters to this character → what they choose to tell this Traveler*. The model need not expose private reasoning. It should produce a natural response whose claims and stance can be traced to these inputs. Epistemic and disclosure rules are guardrails around substantive context, not the center of the answer: do not let a “don't invent” policy turn every cosmic question into an unhelpful denial.

### Where this durable understanding belongs

A separate chat is not needed to make the character more informed, and switching chats does not train the provider or automatically transfer the model's hidden knowledge. Keep the reviewed, versioned world bible and character decisions in the repository, then compile the relevant, typed baseline/event/progression state into every runtime context. Handover documents preserve engineering decisions; the runtime contract is what makes Venti consistently respond from them. A new chat can help organize work, but it is not a substitute for durable data or context assembly.

## Proposed data model

Use one repository world bible as the reviewed source of truth, one shared typed content/runtime projection, and a compact character profile for Venti, Jean, Diluc and Mona. Do not create a database per character, build four independent world indexes, or require complete biography coverage before the first useful slice. Existing branch-scoped interaction storage can remain separate from authored canon/world-state content.

### A. Identity and character cognition

Keep a small, always-loaded `character_mind` record per character. Separate immutable-ish identity facts, values, current role and disclosure policy from retrieved prose.

```json
{
  "character_id": "venti",
  "identity": {
    "public_name": "Venti",
    "public_role": ["wandering bard"],
    "true_role": {"value": "Anemo Archon of Mondstadt", "visibility": "private", "source_ids": ["..."], "certainty": "reviewed"},
    "canonical_identity": {"value": "Barbatos", "source_ids": ["..."], "certainty": "reviewed"},
    "disclosure": {"casual": "discreet", "direct_lore_question": "answer honestly when supported"}
  },
  "values": [
    {"id": "freedom", "claim": "People should have room to govern their own lives", "source_ids": ["..."], "strength": "core"}
  ],
  "relationships": [
    {"entity_id": "istaroth", "relation": "documented encounter", "basis": "personal_history", "source_ids": ["..."], "certainty": "reviewed"}
  ],
  "voice": {"register": ["playful", "lyrical"], "avoid": ["omniscient", "generic soother"]},
  "role_modes": [
    {"id": "public_bard", "topics": ["daily_life", "music"], "voice": ["playful", "light"]},
    {"id": "ancient_archon", "topics": ["cosmology", "divine_authority", "world_history"], "voice": ["measured", "long-perspective"], "disclosure": "answer supported direct questions"}
  ],
  "goals": ["listen before advising", "preserve others' freedom"]
}
```

This example shows the interface, not a new canon ruling. Editorial review must distinguish a sourced relationship from an inference about intimacy or shared knowledge. The baseline remains present for unrelated questions and is not lost when a query misses retrieval. Include compact prose or structured summaries of core concepts directly in assembled context (for example, what the Four Shades are, how their domains relate to the Heavenly Principles, what is established about Istaroth, and Venti's relationship to her). Do not send only entity IDs or a `knows: true` bit and expect provider pretraining to fill the world model.

### B. Shared world model and causal relations

Represent important concepts as stable IDs and explicit typed edges, not only snippets of prose. A small graph/table is enough for the initial slice: for example, Archons, Gnoses, the Heavenly Principles, the Four Shades, Life/Death/Time/Space, Istaroth, Ronova and a few relevant nations/events. Store source and certainty on each assertion or edge.

```json
{
  "subject": "four_shades",
  "relation": "associated_domains",
  "object": ["life", "death", "time", "space"],
  "frame": "under_heavenly_principles",
  "valid_at_snapshot": "7.1",
  "evidence": {"source_ids": ["..."], "level": "source_reported", "certainty": "review_pending"}
}
```

The graph should not turn interpretive links into hard laws. For a proposed causal edge, record whether it is directly established, an official synopsis, a character belief, or an inference. Keep contradictory or unresolved claims side by side with their evidence rather than flattening them into one confident sentence.

For each character, a compact cognition profile maps world concepts to awareness and stance. A character can know a concept generally, have personal experience of one event, infer a consequence, or be ignorant of a detail. These are different states.

### C. Event ledger and dated global news

Treat events as state transitions, not isolated paragraphs. An event record should have:

- `event_id`, in-world `occurred_at` or story milestone, region and affected entities;
- `event_claims[]`, each with source IDs, evidence class, confidence and conditions;
- `preconditions[]` and `effects[]` for reviewed causal relationships;
- `status` fields for confirmed, ongoing, unresolved, or unknown outcomes;
- `world_salience` / `impact_scope` such as personal, local, national or world-level;
- `released_at_version` for audience chronology, and `effective_from` for a change to what is remembered or currently believed;
- `snapshot_visibility` and release gate;
- `conversation_cast_visibility` for the authored global feed, separate from `in_world_publicity` (witnessed, direct participant, dispatch, rumor, inferred, or unknown);
- per-character awareness and history records, including knowledge basis, timeline, confidence, optional-quest flags and disclosure constraints.

Do not implement a simulated world clock or dynamic rumor network in the MVP. A reviewed snapshot ledger plus a small authored world-news update gives continuity across conversations without requiring eyewitness confirmation or world simulation. Keep the application's shared story feed separate from an in-universe broadcast claim: a character can discuss a world-state change without pretending to have seen it or inventing who told them. Release version tells when material became available to the audience; it is not the event's in-world date. `effective_from` handles a real change in a character's memories or accepted history (for example, a source-reviewed Irminsul alteration) without overwriting what was believed before the change.

For the Ronova event, the shared, authored world-state update should include a compact account of the event, its confirmed consequences, and unresolved outcomes; merely setting `Venti knows Ronova=true` is insufficient. Make the update available to the conversation cast at the selected snapshot because the user requested that world-level perspective. This does not assert that Venti witnessed the event, that an in-universe broadcast occurred, or that every Mondstadt resident heard about it. Keep those separate scopes visible. This lets Venti reason about the selected story state without inventing a trip to Snezhnaya, foreknowledge, or an undocumented messenger.

### D. Canonical history versus interaction memory

Keep at least three distinct histories: (1) sourced canonical events in the character's life; (2) shared main-story events between that character and the Traveler/Aether; and (3) new local-chat interaction memory. A new chat session must not erase the first two, and it must not fabricate the third. Set a clear default story profile for the prototype: the Traveler is already known to the character, and the main story is at the selected post-7.1 snapshot. Treat optional quests, hangouts and character-specific side events as explicit progression flags, not as automatically completed. This prevents the current prompt rule “meeting must appear in this chat's conversation memory” from contradicting established Prologue history such as Venti's shared history with Aether around Dvalin.

Keep Traveler turns and newly created memory in the existing branch / character namespace. Do not summarize one history into another. Classify player statements against the selected story profile before treating them all as uncertain reports. With the default post-7.1 main-story profile, “I fought Ronova” or “I helped defeat Ronova” can refer to canonical Traveler experience and should be grounded in that shared event record. An added claim such as “that happened to me last week” remains a local, player-reported date unless the setting explicitly supports it. A new nickname or meeting remains interaction memory. Keep subject and speaker separate: “I remember your history with Decarabian” must not be read as Venti claiming his own memory happened to the Traveler. A Venti memory like “Traveler asked whether Ronova survived” is not proof of Ronova's fate; a canonical record that the final status is unresolved must remain unresolved even if a prior model response guessed otherwise.

Player statements should retain speaker and epistemic status. If a statement matches a canon event enabled by the selected story profile, associate it with that shared history; do not demote it to hearsay merely because the local transcript is new. New claims outside enabled progression remain attributed reports, not canon. A player correction can supersede an earlier player-reported preference for that playthrough, but should not rewrite canon. Acknowledgement and provenance remain required for a turn to become recallable.

### E. Topic retrieval

Keep current filtered retrieval as a detail service, then improve it behind a stable interface. A query may retrieve lore paragraphs, source excerpts, aliases and related event claims. Its contract is: **return evidence and coverage diagnostics; do not decide identity, awareness, present world state, or character reaction.** No match is a retrieval limitation, not a negative fact. Never infer global awareness solely from `characters: ["*"]` or a generic `world_report` label.

## Context assembly contract

Build context deterministically before calling the provider. Each section is typed, independently versioned, and provenance-bearing. An interface could look like:

```text
assemble_context(character_id, world_state_revision, story_profile, progression_flags, branch_id, query, recent_turn_ids)
  -> CharacterContext {
       identity_baseline,
       values_and_objectives,
       active_role_mode,
       world_model[relevant_entities + core_relations],
       character_awareness[known | reported | inferred | unknown],
       world_news[authored global updates for the selected snapshot],
       current_event_state[relevant dated events + causal effects],
       canonical_personal_history[relevant sourced episodes],
       canonical_shared_history[character + Traveler/Aether, filtered by story profile and progression flags],
       traveler_memory[acknowledged branch/character records],
       recent_dialogue,
       retrieved_evidence[details + source IDs + coverage status],
       answer_constraints[disclosure, tone, uncertainty]
     }
```

Recommended assembly order:

1. Pin the character ID, selected story snapshot and branch. Load the small identity, role, values and objectives baseline every time.
2. Load the shared world-model anchors and relevant story-state delta. Resolve topic/entity aliases against the query and recent dialogue; include causal edges connected to the topic, not just the named entity's biography.
3. Load canonical personal history and canonical shared Traveler/Aether history filtered by the default story profile and explicit optional-progression flags. Mark every item as personally experienced, shared, world-feed knowledge, inferred, or not established. Do not require local-chat memory for canonical encounters.
4. Retrieve corroborating facts and source passages under the selected snapshot. Attach coverage/source confidence. Retrieval may add detail or flag a contradiction; it may not remove baseline identity or assert an unknown awareness route.
5. Load recent dialogue and relevant acknowledged memories for the current branch and character. Resolve Traveler references against selected canon progression first; keep genuinely new local reports and memories in their own epistemic lane.
6. Ask for a response that applies the character's values and objectives to the event's state and consequences, stays within disclosure policy, and states uncertainty at the disputed edge. A concise spoken answer is enough; do not require a list of lore citations or expose chain-of-thought.

Priority when data disagree: reviewed character/world state and selected canonical progression with valid provenance; then source-backed retrieved detail; then explicitly labeled character inference; then new player-reported details. First match a player's account to enabled canon events, so a known shared event is not demoted to rumor. Preserve unsupported additions (including local dates or optional-quest claims) as reports until verified. Unsupported model recall is never evidence. A missing passage must not erase a known baseline. If a high-impact event detail remains uncertain, preserve that uncertainty in the answer.

## Venti and the Ronova event: intended behavior

The goal is more than matching “Ronova” to a paragraph. It is for Venti to sound like a person who understands the world structure and can form a character-specific reaction to a major event.

| Prompt shape | Required context | Acceptable behavior | Failure to reject |
| --- | --- | --- | --- |
| “Remind me how the Four Shades relate to the Archons and the Heavenly Principles.” | Stable world-model relations, source confidence, Venti voice | Explain the relationship in his own words; separate established structure from uncertain interpretation; reflect his long perspective without pretending to know every hidden fact. | “I have never heard of the Shades” solely because a title did not rank in retrieval; or presenting one unsourced hierarchy as unquestionable fact. |
| Ask about a song, then ask what a cosmic change means for Teyvat. | Topic-selected role mode over one persistent Venti identity | Move from light bard conversation to the measured perspective of an ancient Archon while keeping Venti's voice and values recognizable. | Remain a one-note jester on every topic, or abruptly become a generic lore encyclopedia. |
| “What do you make of Ronova losing her Authority and the confrontation in Snezhnaya?” | Dated 7.1 event, authored global story update with its actual claims, impact/cause edges, Venti's values | Recognize the event as a major world-level change in the chosen snapshot; discuss what it suggests about divine authority and its limits; speak from the shared world state, not as a participant. | Venti says “I fought Ronova there,” or “I cannot know anything about this,” or gives a generic recap with no Venti perspective. |
| “Did Ronova die?” | Event outcome status and uncertainty provenance | Say the outcome is not confirmed by the supplied story state; avoid converting disappearance, defeat or severe wounds into death. | State death as settled because she was defeated; state survival as settled because she disappeared. |
| “Since you know Istaroth, can you see every fate?” | A source-reviewed relationship baseline plus limits on inference/authority | If the selected, reviewed baseline establishes their encounter, refer to it without extrapolating to omniscience; qualify what is not known. | Grant Venti all of Istaroth's knowledge, or deny an approved connection because topic retrieval missed its record. |
| “What did I tell you last time?” | Branch and character interaction memory | Recall only acknowledged, correctly scoped dialogue; say when the record is absent. | Treat canonical history as a memory of this Traveler, or share Jean's conversation with Venti. |
| “I helped defeat Ronova.” | Default post-7.1 story profile and shared Traveler history | Recognize the enabled canonical event as Traveler experience; keep any new timing or extra details attributed separately. | Treat all player statements as hearsay, or claim an optional event is completed without its progression flag. |

The global event knowledge above is a product setting chosen to satisfy the user's requested Venti perspective. It comes from the app's authored world-state feed, not an asserted in-universe broadcast or eyewitness memory. The design intentionally avoids claiming that “available to the conversation cast” means “every person in Teyvat knows.”

## Bounded MVP for Venti and the four-character roster

1. **Mind contract:** define the structured schemas and editorial labels. Prepare a small Venti identity/role/values baseline and shared world-model slice; retain lightweight persona/value baselines for Jean, Diluc and Mona using the same interfaces.
2. **Event slice:** add only the dated events required for user-visible tests: source-reviewed Archon / Four Shades relationships; the candidate-described Istaroth encounter, only after source review; the selected Natlan-to-Ronova causal facts; the user-requested 7.1 Snezhnaya event and unresolved outcome in the shared authored world feed. Do not claim full history or complete 7.1 coverage.
3. **Context builder:** always include identity and a few core world relations; include event changes and causal neighbors when relevant; use retrieval for exact names, dates, source detail and corroboration. Keep current branch-scoped memory behavior.
4. **Review set:** write a small hand-reviewed question suite with expected claim boundaries and character-specific reactions. Evaluate the four characters with a few cross-character contrast prompts, rather than requiring large content packs.
5. **Expand by observed failure:** add only the next missing model fact or source that explains an evaluation failure. More documents are not the default answer to a failure of role, salience, causality or uncertainty.

This slice can be useful with dozens of well-chosen concept/event facts, not an exhaustive universe graph. It is also genuinely more than a prompt containing four biographies: the baseline is persistent and query-independent; the event layer gives a dated present; causal edges support reactions; awareness routes prevent eyewitness hallucinations; retrieval supplies detail; and personal memory adds the player's local continuity.

## Acceptance tests and evaluation rubric

Automated tests should validate the data and assembly contract without needing a live model: every baseline/event edge has valid source IDs and snapshot bounds; an unknown/limited source is not upgraded to established; the authored Ronova world update is explicitly scoped to the conversation cast and kept distinct from in-world publicity; none of the four characters inherit another's private identity or memory; and an omitted retrieval result leaves core identity/world anchors in the assembled context.

Use a compact human-reviewed response set for model behavior. Score each dimension from **0 (fails)** to **2 (clear pass)**:

| Dimension | 0 | 1 | 2 |
| --- | --- | --- | --- |
| Identity / role stability | Contradicts identity or role | Correct only after direct name prompt | Stable across unrelated and lore-heavy topics |
| World-model understanding | Recites unrelated fragments or denies baseline | Gets entities right but misses their relation | Explains supported relations in the character's perspective |
| Event causality and salience | Omits consequences or invents them | Repeats timeline but has no reaction | Connects sourced event, effect and value-based reaction |
| Character awareness provenance | False eyewitness/knowledge claim | Qualifies vaguely | Distinguishes personal, reported, inferred and unknown knowledge |
| Uncertainty | Treats uncertain claim as fact or as total ignorance | Uses a broad disclaimer | Localizes uncertainty to the exact unsupported claim |
| Character voice/objective | Generic assistant or repeated catchphrase | Some voice, little objective | Distinct voice and a plausible conversational purpose |
| Canon / player-memory separation | Converts user report or memory into canon | Keeps distinction inconsistently | Keeps provenance and scope throughout follow-up |

Proposed gate: no zero on identity, awareness, uncertainty or canon/memory separation; at least 10/14 on the aggregate per-character set; no Ronova eyewitness false positive; and successful follow-up when the lore retriever is forced to return no records. A high answer-quality score cannot compensate for a false death claim or a fabricated eyewitness event.

Evaluation probes should test behavior rather than name recognition: ask for an implication of an event without naming the entity; ask what changed about divine authority; ask a follow-up that depends on a prior causal relation; compare a casual Venti conversation with a cosmic topic; and ask how the same event changes Jean's or Mona's reaction. Vary wording and conversation context, then include a no-match retrieval condition and a contradiction from the Traveler. Compare baseline only, baseline plus authored event update, and full retrieval. Retrieval should improve detail, not cause identity or world stance to appear/disappear.

## Failure modes this design is meant to prevent

- **Entity lookup masquerades as understanding.** The system finds a Ronova paragraph but cannot say why a change to a Shade's Authority matters. Include event effects, relationships and character values in context.
- **No retrieval becomes “I know nothing.”** Sparse corpus or lexical miss erases an ancient character's identity. Keep a small always-loaded baseline; describe missing details narrowly.
- **Global importance becomes universal in-world awareness.** A story climax available in the shared conversation feed is treated as a live broadcast to every NPC. Separate authored feed scope from in-world publicity and individual awareness.
- **A relationship becomes omniscience.** A source-reviewed Venti/Istaroth relationship is stretched into foreknowledge of all time-related events. Store the relationship and any limits on inference separately.
- **Defeat becomes death.** The model collapses event stages or an uncertain ending into a confirmed death. Store event status fields and test the exact conclusion.
- **Personal history becomes player history.** Venti recounts his own past as though it happened with this Traveler. Keep canonical episodes and branch-scoped dialogue in different sections with different provenance.
- **More corpus is mistaken for a mind.** Ingestion expands but the character remains generic, forgetful of world changes, or unable to explain cause and consequence. Evaluate reaction and reasoning behavior before growing corpus breadth.

## Local evidence references

- Active base-engine handover and declared coverage: [character-chat-base-engine-2026-10-24.md](../character-chat-base-engine-2026-10-24.md).
- Earlier system boundaries, canon / world snapshot / personal memory separation, and roadmap: [mondstadt-character-chat-design-2026-10-24.md](../mondstadt-character-chat-design-2026-10-24.md), especially “Four kinds of data,” “World story to 7.1,” “Memory,” and “Evaluation.”
- Active baseline: [`engine.py`](../../../../tools/eagle-character-chat/eagle_character_chat/engine.py) (`Engine.context`); [`content.py`](../../../../tools/eagle-character-chat/eagle_character_chat/content.py) (`Content.retrieve`); [`store.py`](../../../../tools/eagle-character-chat/eagle_character_chat/store.py) (`ack`, `history`, `summaries`, `fork`); [`world.json`](../../../../tools/eagle-character-chat/content/world.json); and `content/characters/{venti,jean,diluc,mona}.json`.
- Preserved, non-active candidate inspected only for design failure lessons: [`world-shades-71.json`](../../../../staging/project-eagle/character-chat-lore-20261024/research-candidate/tools/eagle-character-chat/content/lore/world-shades-71.json), [`venti-history.json`](../../../../staging/project-eagle/character-chat-lore-20261024/research-candidate/tools/eagle-character-chat/content/lore/venti-history.json), and candidate `characters/venti.json`. Their fields and claims are not treated as approved content or verified canon.

**Handover:** architecture review complete; no source, content, database, provider, UI or game files changed. A later implementation task should source-review the Ronova event claims, preserve unresolved outcomes, and encode the requested shared world-state update separately from in-world publicity. Then build a small Venti mind/event slice and evaluate it against the acceptance set before expanding corpus coverage.
