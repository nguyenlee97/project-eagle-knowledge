# Paimon — GPT-6 Luna, 25/10/2026

User requested the same GPT Luna selection as the referenced chat **Thiết kế chat NPC Genshin** (`01a16c0f-373a-7860-9845-930226ecaa22`). Read its completed migration and current secret-free profile; Paimon now selects **gpt-6-luna directly through OpenAI** for both web and native dialogue.

The new Paimon-owned profile is `data/project-eagle/paimon/connection.json`. It copies only the verified API base/model and named external credential reference from Character Chat, with low reasoning, a1200-completion-token ceiling and a35-second transport timeout. Existing Paimon client accepts these options at top level. Character Chat's structured lore-output schema is not copied into Paimon's plain-text contract. Existing160ASCII reply and100ASCII input bounds remain.

Credential values were not copied into source, profiles, evidence or logs. The same existing named Windows user-environment credential is read through the existing caller. Character Chat's profile and the historical Groq/opencode relay profile are unchanged; Paimon has an independently pinned selection. No automatic fallback to another provider/model.

The runtime/source `paimon_config.json` both reference the new profile. They reload on every turn; no module, gameplay, UI or memory changes and no process restart needed. At inspection the Phone was closed, so only the existing EaglePhone host was started hidden as PID13184. GTA was not launched. The running `/api/paimon-web/session` confirms `model=gpt-6-luna` and `configured=true`.

## Validation and recovery

- Production request-body check confirms model, low reasoning and1200 completion cap, with no tools, conflicting `max_tokens` or NPC response schema.
- One actual OpenAI request with synthetic chat-only context completed in about2.77 seconds. A second future-year question was rejected locally using the2010-01-01 cutoff without another API call.
-15 core and17 web focused tests pass. QA memory is isolated under the task's staging directory; no real user conversation reset or game DB change.
- Three applied configuration hashes match;17 protected hashes including Engine/Web/HUD/native bridge, game IPC/memory and Character Chat/Groq profiles remain unchanged. Shared lock released. Evidence: `staging/project-eagle/paimon-luna-20261025/qa/live-luna.json` and `qa/verification.json`.

Applied manifest: `staging/project-eagle/paimon-luna-20261025/manifest.json`, before-images in `before/`. Targets are only the new Paimon profile plus runtime/source Paimon configs. The profile is installed before references are changed; rollback restores references before removing the profile. Future drift is refused before writing.

```powershell
C:\Python310\python.exe -B tools\eagle-dialogue\luna_config.py status
C:\Python310\python.exe -B tools\eagle-dialogue\luna_config.py rollback
```

Recovery is configuration-only and hot-loaded; it preserves all conversation stores and does not stop processes. It returns the prior Groq selection explicitly; normal operation never silently fails over. Do not restore unrelated Engine/HUD/whole-game backups.

Model compatibility checked against [official GPT-6 Luna documentation](https://developers.openai.com/api/docs/models/gpt-6-luna). This task changes the model connection, not the character/lore capabilities or the still-pending native gameplay QA. Source ownership handed back; no other-agent acknowledgment assumed.
