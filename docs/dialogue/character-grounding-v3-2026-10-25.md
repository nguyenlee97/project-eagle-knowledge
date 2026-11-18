# Character Chat v0.3.0 — character grounding and dialogue provenance

25 October 2026, Asia/Saigon. **Status: complete — v0.3.0 running at [Conversation Studio](http://127.0.0.1:8952/) with GPT-6 Luna.** [Work item](../work-items/2026-10-24-codex-character-grounding-v3.md). This follows the [four-character independent audit](character-independent-audit-2026-10-24.md).

The final build completed twenty real-provider cases in twenty attempts, with eighteen pass and two partial qualitative judgments. All 88 automated checks pass. The original conversation data is preserved. Remaining partials concern omitted relationship/quest detail; this small sample does not establish comprehensive lore reliability.

## What changed

The engine now supplies sourced personal history and typed relationships, separately from general world knowledge. Diluc receives the Crepus/Eroch/Delusion chronology and his different relationships with Kaeya, Jean and the Knights. Mona receives her mentor/box/diary history, actual hydromancy capability, the Traveler-specific prediction limit and her livelihood. Venti receives his Tsaritsa history; Jean receives her family and colleague relationships and a precise account of Dvalin's rescue.

Character awareness is distinct from disclosure. An awareness record specifies when the NPC knows something and whether discussion is public, guarded or private with the acquainted Traveler. Jean and Diluc can know Venti is Barbatos without receiving all of Venti's personal memories or permission to announce his identity publicly. Mona receives no unsupported identity knowledge. The old blanket world-synopsis restriction has been removed.

Historical Natlan records distinguish Mavuika's bargain and Capitano's sacrifice/merger from the later Snezhnaya confrontation. Events have explicit participants; the context marks each NPC's access as participation or reported knowledge. Awareness therefore does not create a visit, messenger, expedition or intelligence channel.

Question-focused anchors repeat the most relevant reviewed facts near the answer task. Personal facts are searchable, topic cues help implicit questions, and character-specific relational aliases distinguish “your father” from the Traveler's “my father.” Broad Aether/Mondstadt mentions have lower ranking weight so stage directions do not dominate a biographical question.

Always-present reviewed briefs preserve major world and personal awareness; selected records retain their full text and authored chronology. A shorter dialogue-writing task explicitly separates historical causes from a character's values or present preferences. The context budget is 20,000 characters. Across the eight captured pre-compaction questions, median assembled size fell from 25,698 to 17,171 characters (**33.2%**); these are payload character counts, not token-billing estimates. Full source records remain intact.

Recent dialogue is supplied as attributed quotations inside the context rather than replayed as fresh assistant demonstrations. It remains available for conversational recall, but prior generated statements have no canonical authority. The prompt explicitly separates reviewed facts, reports, opinions and unsupported mechanisms, and instructs the character to correct earlier mistakes. Stored conversations, notes, branches and reset behavior are retained; no database migration or memory reset is part of this update.

One completion now returns a compact evidence-selection envelope plus the natural reply. The engine accepts only record IDs actually supplied to that request, then attaches the original curated text locally. The model cannot replace that evidence with an invented quotation. Only the natural dialogue is exposed, with selected support retained in the trace. Invalid envelopes fail explicitly without committing a substitute answer; no second verifier call or automatic retry is added. This validates source provenance, not semantic truth: a real record can still be used incorrectly, so the live answers are reviewed separately.

## Source review

Independent Luna content scopes supplied staged source/entity packets for Venti/Jean, Diluc/Mona and Natlan. Existing IDs were retained, new references merged and validated. The coordinator checked the decisive Natlan transcript and Dvalin rescue mechanism, and corrected an initial draft's inaccurate Holy Lyre wording before freezing the candidate. Sources remain labeled as official material, community-hosted game text or secondary coverage; unavailable pages were not treated as read.

The final source pass also narrowed Eroch's order to Diluc, rather than the whole order, against [Diluc's profile transcript](https://genshin-impact.fandom.com/wiki/Diluc/Profile). [A Bewildering Fate](https://www.hoyodex.com/wiki/genshin-impact/a-bewildering-fate) establishes that Mona read a book dropped from Klee's backpack before learning it was the diary, and had spent her Mora coming to Mondstadt. These facts are kept distinct from her later research expenses.

- [Natlan finale dialogue](https://genshin-impact.fandom.com/wiki/When_All_Becomes_a_Monument) supports Capitano's substitution, the immortality rule and his concluded journey; precise post-merger consciousness/return remains open.
- [A Long Shot dialogue](https://genshin-impact.fandom.com/wiki/A_Long_Shot) supplies the tainted-blood-clot mechanism for Dvalin's rescue.
- [Reunion With the Dragon](https://genshin-impact.fandom.com/wiki/Reunion_With_the_Dragon) establishes Jean's private recognition of Venti.
- Character-specific source notes and before/after manifests are retained under `staging/project-eagle/character-grounding-v3-20261024/{diluc-mona,venti-jean,natlan}/`.

## Validation protocol and results

The existing suite plus new boundary regressions passes **88/88**. Tests cover private awareness versus disclosure, relationship validation, relational aliases, event participants, progression/release eligibility, question focus, quoted old mistakes, source tracing, compact context budgeting, evidence-envelope rejection, API parameter compatibility and existing memory/reset isolation. JavaScript syntax checking also passes. Tests verify supplied information and storage behavior, not every generated factual claim.

The final candidate is frozen in `evaluation-luna/candidate-manifest.json`. A single coordinator queue repeated the sixteen unchanged audit questions plus four fresh stress cases: Jean's private identity knowledge, Diluc correcting an old wrong biography, Mona correcting an old causal theory, and Venti distinguishing the two Ronova events. The two repair cases seed synthetic old replies; no real player conversation is used.

Historical Groq runs used at least 65 seconds between starts. `pilot-1/` retains one reply and an HTTP 502; `pilot-2/` retains six replies before unsupported Jean details prompted a revision; `pilot-3/` retains two replies and two rejected paraphrased evidence envelopes. A later Groq run accepted eight cases before its daily token quota stopped the queue. A four-record relationship answer also exposed an unnecessarily strict three-record limit; the validator now accepts up to eight eligible records. Source-precision revisions and exact-request retention checks are recorded separately. These development artifacts are not counted as final Luna results.

The user then explicitly authorized GPT Luna. After verifying the official model ID and account access, the dedicated profile selected **[gpt-6-luna](https://developers.openai.com/api/docs/models/gpt-6-luna)** through OpenAI Chat Completions, low reasoning, a 1,200-token completion ceiling and native structured output. The final queue used one in-flight request, a six-second minimum cooldown plus an interval calculated from observed rate headers. Actual minimum start spacing was **8.593 seconds**. All twenty cases completed in twenty attempts, with **zero 429 or format errors**. Evaluation usage was 78,812 input + 5,243 completion tokens, 84,055 total; a separate tiny readiness request used 54 tokens. No automatic provider failover occurred.

| Character | Five final cases | Corrections demonstrated | Residual review note |
| --- | --- | --- | --- |
| Venti | 5 pass | Wind-spirit/bard history; Tsaritsa estrangement without Tenryou invention; separate Natlan/Snezhnaya events; no false eyewitness memory. | Reflective answers can remain concise. |
| Jean | 5 pass | Correct blood-clot rescue, private recognition of Barbatos, proportionate civic advice without invented expedition involvement. | Public Dvalin awareness remains unscored; present discretion is not asserted as historical policy. |
| Diluc | 4 pass / 1 partial | Crepus is his father; Eroch/Delusion/resignation chronology; corrects an old false biography. | Relationship answer leaves adoption/cooperation detail implicit. |
| Mona | 4 pass / 1 partial | Accidental book-before-identification sequence; outsider reading limit; no invented mortality mechanism; corrects old speculation. | Diary answer omits Alice's relation and the box's original role. |

Both source reviewers independently examined all twenty final answers. Their [Venti/Jean review](../../../staging/project-eagle/character-grounding-v3-20261024/reviews/venti-jean/luna-review.md) and [Diluc/Mona review](../../../staging/project-eagle/character-grounding-v3-20261024/reviews/diluc-mona/luna-review.md) retain per-case judgments. Full [machine verification](../../../staging/project-eagle/character-grounding-v3-20261024/evaluation-luna/verification.json) records hashes, timing, token usage and review provenance. These comparisons include content, prompt and model changes together; they are not a model-only A/B experiment or statistical reliability estimate.

## Runtime and recovery

The standalone tool remains outside GTA. The owned Conversation Studio at port 8952 has restarted and its bootstrap confirms v0.3.0, `gpt-6-luna` and the evaluated content hash. All six protected user-data tables have identical before/after row digests, including conversations and memory. Game, Paimon, maps and character models were outside this task's write scope.

The dedicated profile is `data/project-eagle/character-chat/connection.json`; it contains only an external credential variable name. The credential is stored in the current user's Windows environment, not in the repository, evidence or logs. The shared Paimon/relay connection hash is unchanged. All 35 final tool files match the evaluated manifest; 19 files differ from the pre-change snapshot, including three additions. A scoped source scan found no API-key literals.

The pre-change source snapshot and SHA256 manifest are in `staging/project-eagle/character-grounding-v3-20261024/before/` and `before-manifest.json`. Recovery must restore only the changed tool files after checking the installed hashes and stopping the owned studio; preserve the current conversation database. Source rollback to v0.2.1 does not require replacing the database because this update leaves the store schema unchanged.

The staging `rollback_source.py --check` command checks current candidate and backup hashes. To intentionally roll back, stop the owned studio with `tools/eagle-character-chat/studio.ps1 -Action stop`, run that helper with `--apply`, then start the studio again. It restores only changed source files, removes only its hash-matched added files, refuses a later conflicting edit or occupied port 8952, and never opens/restores the database. A separate consistent pre-restart SQLite backup is retained for preservation; it is not part of source rollback.

The helper does not remove external credentials or the dedicated profile. The old v0.2.1 source uses its historical shared connection; provider recovery is separate from memory recovery. The historical Groq runner is marked retired to prevent accidental quota retries. Repeating the final evaluation requires a fresh staging run based on `evaluation-luna/run_regression.py`, preserving its synthetic-only scope and bounded rate control.

## Limits

This is a bounded, sourced character/world slice, not an automatic complete-wiki import. Focused evidence and explicit provenance reduce known failure modes but do not prove that the model cannot improvise an unsupported fact. A character can reasonably be concise or guarded without reciting every dossier detail. The current build is ready for user trials; broader lore coverage, repeated behavioral evaluation and later game integration remain future work.
