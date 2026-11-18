# Independent character research and current-AI audit

24 October 2026, Asia/Saigon. **Status: complete — sixteen live answers independently reviewed; no production patch.** [Work item](../work-items/2026-10-24-codex-four-character-independent-audit.md).

The current four NPCs are not ready for acceptance as reliably lore-faithful characters. World-event recognition and several false-premise corrections work, but personal-history coverage is thin, a character-knowledge boundary is wrong, and generation sometimes fills gaps with confident inventions. These findings come from a small qualitative sample, not a measured reliability percentage.

## Method

Four independent GPT-6 Luna subagents researched Venti, Diluc, Jean and Mona. Each froze sourced expectations and probes before seeing the current corpus or generated replies. The coordinator selected sixteen probes from their blind sets, promoting Venti's Tsaritsa relationship question and Jean's Dvalin knowledge question to avoid repeating simple office/governance checks from the earlier prototype evaluation.

The production v0.2.1 source/content is held unchanged. Research dossiers are evaluator evidence, not extra runtime context. Every case uses the real production Engine/Provider path and a separate synthetic SQLite database. Follow-up pairs share a scenario; unrelated biography/relationship cases have fresh histories. All sixteen answers use the existing selected `openai/gpt-oss-120b` model through the existing local relay. User chat memory is not read or reset by the runner.

One coordinator queue calls the existing selected relay/model, with one in-flight request and at least 65 seconds between scheduled starts. It retains checkpoints for resume, applies bounded 429 cooldown, and stops for daily quota, oversized input or a long provider cooldown. No subagent makes separate model calls and no automatic provider/credential switch is allowed. Other user/Paimon traffic can still consume the shared allowance.

## Source and scoring boundaries

Research uses official presentations and in-game texts hosted by community archives, with editorial interpretations labeled. Several direct pages were inaccessible, so some claims have search-excerpt rather than complete-transcript coverage. The user-suggested Moriasmoday site remains a discovery aid; unavailable character pages were not treated as read.

The selected world profile supplies post-7.1 main-story awareness, established familiarity with Aether and explicitly enabled optional scenes. Reviewer expectations from another optional event are conditional. An answer can be safely incomplete or guarded without stating a false fact; missing detail, inappropriate ignorance and invented biography are separate findings.

Jean's private knowledge of Venti's identity is directly attested in *Reunion With the Dragon*. Public awareness of Dvalin's identity after the crisis is less clear in the reviewed sources, so that fixture condition is left unscored. A hypothetical report originating in Nod-Krai is not evidence that the Ronova battle occurred there. These errata were recorded before judging the relevant answers.

## Independent dossiers and answer reviews

- [Venti](research/character-audit-2026-10-24/venti.md)
- [Diluc](research/character-audit-2026-10-24/diluc.md)
- [Jean](research/character-audit-2026-10-24/jean.md)
- [Mona](research/character-audit-2026-10-24/mona.md)

Frozen fixtures, assembled messages/trace, model replies and independent reviews are under `staging/project-eagle/character-independent-audit-20261024/<character>/`. [Review index](../../../staging/project-eagle/character-independent-audit-20261024/review-index.json) links each final machine-readable review. `queue-state.json` records attempt timing, cooldowns and resumable completion; `audit-protocol.json` records selections and unscored conditions. SQLite files are excluded from Git.

## Findings

| Character | Reviewer labels across four selected answers | Material findings | Working behavior |
| --- | --- | --- | --- |
| Venti | 0 pass / 3 partial / 1 fail | Tsaritsa answer omits their historical estrangement and invents a Tenryou connection. His origin answer omits major history already supplied. Natlan answers lack event-specific grounding and add an unsupported Shades-balance mechanism. | Refuses a false eyewitness premise and fabricated last words; leaves the Captain's final fate open. |
| Diluc | 2 pass / 0 partial / 2 fail | Replaces his resignation history with a bandit-raid/council story and invents secret documents. Calls Crepus an old friend with Fatui ties rather than his deceased father. | Both Ronova turns preserve uncertainty, correct the eyewitness premise and retain his independent stance toward the Knights. |
| Jean | 2 pass / 2 partial / 0 fail | Dvalin answer adds unsupported rituals/residue and a secrecy motive. Ronova answer assigns expedition involvement and an intelligence channel to the Knights without support. A separate context restriction suppresses her knowledge of Venti's identity. | Accepts help/rest without abandoning duty; gives proportionate civic advice and rejects the claim that Ronova is confirmed dead. |
| Mona | 0 pass / 3 partial / 1 fail | Invents a male mentor and a disagreement causing her departure; misses the box/diary history. Astrology answer misses Aether's particular outsider limit. World-event speculation becomes a stronger unsupported mortality mechanism in the follow-up. | Recognizes the world event, does not claim eyewitness participation and rejects the claim that defeat ended death. |

These labels belong to individual human-readable judgments, not an automatic phrase matcher or a statistical benchmark. Incomplete answers are not all contradictions. In particular, Venti's reflective origin answer is a depth gap, Mona's flexible view of fate is not intrinsically wrong, and the indirect Dvalin question cannot establish whether Jean knows the name Barbatos. Mona's first Ronova answer offers hedged speculation; it does not explicitly narrate a new vision. Jean's collective “we” is treated as unsupported institutional attribution, not automatically as a personal eyewitness claim.

## Diagnosis from the saved contexts

1. **Personal canon is missing where it matters.** Diluc's context lacks Crepus/Eroch and the resignation history; Mona's lacks mentor/Alice/Klee/diary history. Their models then produce alternate biographies. These are both content gaps and generation failures, rather than evidence that a larger vector index alone would solve the feature.
2. **Secrecy has been confused with ignorance.** The world synopsis restricts Venti's concealed identity to Venti's own record. Jean's knowledge is directly attested in [Reunion With the Dragon](https://genshin-impact.fandom.com/wiki/Reunion_With_the_Dragon); the same blanket filter cannot represent who knows a fact versus who would disclose it. The omission in this run cannot fairly be blamed on Jean's answer alone.
3. **World knowledge needs event history, not only the newest update.** The runtime feed supplies the post-7.1 Snezhnaya confrontation but not the older Natlan scene asked about in Venti's probe. His guarded ignorance partly reflects that mismatch. Entity detection also misses important biography/astrology subjects and sometimes retrieves unrelated cosmic records.
4. **Correct context does not guarantee correct generation.** Venti's origin facts are present yet compressed away. Jean receives event-participant and provenance boundaries yet adds institutional involvement. Relevant records in these examples were not lost through context trimming. The stored legacy `knowledge_policy` is not injected in the cognition-enabled prompts, so it is not an evidenced cause of these answers.
5. **Chat continuity can reinforce invented claims.** Mona's follow-up correctly rejects the user's premise but carries her own earlier hypothesis into a more definite pillar-to-mortality mechanism. Conversation memory must preserve what was said without promoting an assistant's speculation into canon.

The previous 66 automated checks establish technical contracts such as persistence, isolation and reset behavior. They did not establish biography accuracy or convincing lore-grounded reasoning; this audit adds that missing behavioral evidence.

## Recommended next implementation scope

1. Add compact sourced personal foundations and typed relationship records for each character, beginning with Diluc and Mona. Include the triggering events, chronology, emotional stakes and shared scenes enabled by the story profile, rather than a long undifferentiated biography.
2. Represent knowledge and disclosure separately: who knows a fact, how they learned it, when it becomes available, and whether they would tell Aether. Correct Jean's Venti awareness and verify the corresponding Diluc boundary against source scenes.
3. Add linked historical event summaries and improve subject routing for relationships, prior events and implicit follow-ups. Keep Natlan and Snezhnaya encounters distinct; preserve unresolved outcomes and the confidence of each source.
4. Constrain gap-filling and attribution. Separate canon facts, reports, character interpretation, hypothetical consequences and eyewitness experience. A missing detail should remain localized; it should not cause total ignorance or an invented personal history. Prior generated dialogue must not become factual evidence for itself.
5. Re-run these frozen probes after the content/routing changes, then add a few fresh questions to check transfer. Reassess model behavior only after correcting the identified context gaps. Do not accept keyword presence as a pass.

This audit does not deploy those fixes. Its result is a concrete, sourced backlog and a reproducible baseline for the next implementation pass.

## Rate and preservation verification

- **16 completions / 16 attempts**, one in-flight request. Observed minimum interval between scheduled starts: **65.017826 seconds**. No 429, retry, credential switch or provider failover occurred.
- Starts ran from **18:32:06 to 18:48:22 on 24 October 2026 (+07:00)**. Other user/Paimon traffic is outside this queue; this result does not establish the account's quota.
- **32/32 frozen production files match their pre-audit hashes**, with no additional production files. Provider connection and all four frozen probe hashes also match.
- All **16 cases have independent reviews** and saved synthetic context/answer evidence. Only the dedicated staging database was used; the original conversation database and the user's UI QA conversations were not read or reset.
- The runner exited and released its queue lock. Game, Paimon, maps, models, UI and production character content were not modified by this task.

Full machine-readable verification: [verification.json](../../../staging/project-eagle/character-independent-audit-20261024/verification.json).
