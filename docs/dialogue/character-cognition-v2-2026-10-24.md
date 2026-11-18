# Character Chat v0.2 — world continuity, character perspective and memory

24 October 2026, Asia/Saigon. Implementation and evaluation record for [the authorized work item](../work-items/2026-10-24-codex-character-cognition-v2.md). This follows the [worldbuilding research](genshin-worldbuilding-and-character-cognition-2026-10-24.md).

## Result and boundaries

The standalone engine now separates a character's existing world/personal/shared history from new conversation memory. Detail retrieval no longer decides whether Venti recognizes the world's major divine powers. The main implementation is Venti's foundation; Jean, Diluc and Mona use the same contracts with separate roles, values and knowledge limits. This is a bounded world/history slice, not comprehensive ingestion of every quest through 7.1.

There is no GTA, map, skin, Paimon or shared provider-configuration integration in this task. Conversation remains English-only. The existing selected relay/model is reused; synthetic evaluation has its own SQLite database.

## Runtime knowledge

`content/cognition/world.json` selects a post-7.1 setting, Aether as Traveler, completed main story and explicit optional story flags. The current default enables `venti_story_quest`, `summer_58` and `mona_story_quest`. This is an authored prototype setting, not live GTA quest detection. Optional shared-history records are filtered by `requires_story`; a character's ancient personal experience does not begin when the player views a later revealing scene.

Every prompt receives filtered world concepts/relationships, current events, its own character identity/values/voice/disclosure/limits, personal biography and enabled shared Traveler history. The world slice distinguishes the Shades, Heavenly Principles, Archons, Authorities, Gnoses, Sovereigns, Abyss/Order/Khaenri'ah, and Irminsul/Descender accounts. Event records preserve confirmed changes and unresolved consequences. Global event awareness does not invent eyewitness participation or a messenger.

Venti's personal foundation includes his wind-spirit origin, the Nameless Bard, the distinct later Vennessa revolt, Four Winds, Dvalin, Gnosis loss, Istaroth connection, selected Carmen Dei history and a private Archon-peer identity link. Private personal records are character-scoped before assembly. Canonical shared Dvalin history survives a fresh local chat.

The content pack carries source IDs, release versions, entity references, evidence classes and optional-story conditions. Startup validates references and rejects malformed/unknown sources. Sources include official material, community-hosted in-game text, community summaries and explicitly authored setting assumptions. An uncertain identity/ending is not promoted to certainty. Source review is recorded in task staging, including rejected provisional claims.

## Conversation assembly

`Content.foundation()` is independent of search. Entity/title aliases and a recent topical follow-up can route additional detail; a location mentioned in a follow-up need not erase its preceding subject. Generic words such as "time" are not aliases that reroute personal-memory questions to Istaroth. Lexical retrieval ranks eligible records and returns no result when no terms match; it no longer supplies unrelated bard/teapot records as a fallback.

Serious topics request measured plain language; everyday conversation can use the character's warmer voice. This is one persistent identity responding to the subject, not interchangeable personalities. The response contract separates known events from inferred possibilities and keeps knowledge distinct from disclosure. Earlier AI replies remain inspectable but are fallible transcripts and cannot override reviewed current facts.

Prompt records omit repeated source/filter bookkeeping after local validation; full evidence remains in traces. Context trimming sheds whole summaries, recalled exchanges, older recent exchanges, detail records and excess notes before removing any reviewed foundation. Traces record the content hash, story profile, foundation IDs, routed subjects, optional detail, actual retained memory/history and trimming counts. These traces show supplied evidence, not proof of sentence-level grounding.

## Memory and migration

Schema v2 adds attribution/subject/origin/slot metadata without replacing existing text, IDs, source links or checkpoint intervals. Startup migrates v1 additively; it does not backfill old user conversations or rewrite failed Venti replies. A consistent before-upgrade SQLite backup is in staging.

Automatic extraction runs only after display acknowledgement, from the Traveler's exact supported first-person sentence. It recognizes names/nicknames, likes/dislikes, explicit preferences, plans/promises and selected personal facts. It does not call a second model, parse arbitrary prose or learn from the NPC's reply. Other dialogue remains available through recent history, FTS recall and extractive summaries.

Corrections are versioned by semantic slot. Compatible likes coexist; opposite statements about the same item can replace each other. Explicit reminders outrank automatic notes; direct notes/edits outrank both. All stay player-reported and character/branch scoped. Edits retain their original source link. Forks remap note/turn references so forgetting an inherited exchange also clears its derived trace copies in that branch, while retaining the parent branch.

The Memory panel labels automatic, explicit and edited notes, with an exchange number when available. A visible setting notice states that the player is Aether after 7.1. The source drawer distinguishes always-present foundations from additional search passages.

## Validation

Offline contract suite: **59 tests passed on the final code/content**; live review is recorded in the work item and staging verification manifest. Tests include an empty-detail ablation, canonical history without local chat, privacy/release/progression filters, pronoun follow-up routing, bounded context trimming, source validation, v1 migration, acknowledged-only extraction, corrections/manual priority, checkpoint inheritance and forgetting within a fork. Existing HTTP/provider/cancellation/idempotency tests remain included.

`evaluations/cognition-v2.json` contains behavior expectations and hard failures. `verify_cognition.py` uses a fresh synthetic database, a maximum of 20 planned provider completions, optional pacing and saved outputs requiring explicit review. It does not equate a phrase match or transport success with character understanding.

Initial exploratory runs exposed an absent relay, a rate-limit response, an evaluation timeout that incorrectly included pacing, and overextended musical analogies that invented world mechanisms. The relay was started through its existing helper, the evaluation timer corrected, and serious-topic instructions made explicit. Earlier outputs remain as failed/interrupted evidence rather than accepted results.

Final reviewed set: **20 real-provider completions plus one authored adapted exchange**, selected from saved runs with focused rechecks replacing earlier failed cases. See `staging/project-eagle/character-cognition-v2-20261024/reviewed-behavior-results.json`. Empty-detail awareness, event recognition, refusal of false eyewitness/death conclusions, nickname correction and isolation, and canonical-history continuity were checked. A later governance recheck corrected the model's earlier claim that Barbatos directly administers Mondstadt. World divine roles and civil institutions now have an explicit distinction.

This is bounded prototype acceptance, not a certificate of perfect canon or voice. Saved replies still show minor chronology compression, speculative causal language, similar phrasing across some characters, ambiguous nickname ownership when no history exists, and an invented song presented as familiar repertoire. These are recorded per response; no automatic phrase score is reported as full lore accuracy. Broader personal histories and whole-story ingestion remain future content work.

UI verification used a separate copy of synthetic evaluation history: setting notice, Ronova follow-ups, foundation/source trace and the corrected automatic nickname note were visible. Screenshot: `staging/project-eagle/character-cognition-v2-20261024/cognition-v2-preview.png`. The main user database was not used for synthetic QA. Runtime and migration evidence show all original profile/playthrough/branch/session rows, 10 turns and 2 notes preserved; ten protected provider/Paimon/runtime source files remained unchanged. The live app is v0.2.0 at port 8952; port 8953 was a temporary QA preview.

## Recovery and handover

Code/content before-images and hashes: `staging/project-eagle/character-cognition-v2-20261024/before/` and `before-files.json`. Original user database: `conversations-before.sqlite3` in the same excluded staging directory. Final verification compares original user rows and protected provider/Paimon/runtime source hashes.

Normal content changes preserve the live database. Reverting to v0.1 code also requires a compatible database because that version rejects schema v2: first preserve any newer database, then intentionally restore the matching pre-upgrade snapshot if a full standalone rollback is needed. Do not run a GTA/Paimon rollback for this tool.
