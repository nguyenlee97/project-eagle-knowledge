# OpenCode2API backend handover — 23 October 2026

## Current handover: Groq verified and selected

**This section supersedes the quota-blocked candidate below.** User authorized Groq first, OpenAI if Groq cannot be used, and supplied a Groq key. Groq live `/models` returned `openai/gpt-oss-120b`; three bounded text checks passed (exact text, history/game-date, no-future-answer spot check), followed by a successful call through the existing Paimon `chat_completion` function without editing its source. No OpenAI key was supplied or used, and no OpenAI request was sent.

Active [connection.json](../../../staging/project-eagle/opencode2api-20261023/connection.json) now points to **`http://127.0.0.1:18082/v1`**, model **`openai/gpt-oss-120b`**, `api_key_env=EAGLE_OPENCODE_API_KEY`, timeout 35 seconds, `readiness.chat_verified=true`. The name `openai/gpt-oss-120b` is the Groq-hosted model identifier, not a call to the OpenAI paid API. Direct upstream connection details and required headers/options are also recorded under `upstream` without credentials.

This is a small independent **text-only loopback relay** in `tools/opencode2api/provider_setup.py`, separate from the Go gateway on 18080. Groq initially returned a non-JSON403 to default urllib requests; adding the identifying `User-Agent: EaglePaimon/1.0` produced 200 with the same key and endpoint. The current Paimon caller does not consume arbitrary extra headers or `reasoning_format`; this relay applies those required provider options without changing the other chat's source ownership. It forces text/nonstreaming, the selected model, bounded completion tokens, low reasoning effort and hidden reasoning, and rejects caller tool declarations. It has no tool executor, no conversation storage, no automatic paid failover, and no web search. The unchanged caller reads the explicitly named per-user environment variable when its process environment is stale.

Latest evidence:

- [provider-status.json](../../../staging/project-eagle/opencode2api-20261023/provider-status.json): `/models`200 and three chat200 results, about 0.4–0.7 seconds each in the final run. The date-cutoff refusal is a spot check, not proof of a hard knowledge boundary or polished Paimon characterization. A curly apostrophe in `can’t` exposed an overly strict local checker; normalization was corrected and the final live checks passed.
- [provider-caller-verification.json](../../../staging/project-eagle/opencode2api-20261023/provider-caller-verification.json): unchanged `tools/eagle-dialogue/runtime/eagle_dialogue/paimon_service.py::chat_completion` returned `EAGLE_CALLER_OK` through the relay in 0.75 seconds; includes that source's SHA-256. This imported function test did not instantiate the game service, launch GTA, modify runtime or touch game saves.
- Missing local API auth gives401 on model/chat routes; health reports ready; CSRF/Origin guards protect key-entry POSTs. Six offline checks cover discovery, tool/incomplete/spoiler rejection, punctuation normalization, fallback, compare-before-write activation, backups and secret redaction. No real key is included in evidence.
- User-entered Groq key is stored only in the private state directory and the named per-user `EAGLE_GROQ_API_KEY`. Do not copy private state or key values into game config, docs or chat. Local authentication remains the fresh random gateway key provisioned earlier; it is not the Groq credential.
- The previous connection was backed up immediately before activation; its path and before/after SHA-256 are recorded in provider-status. [provider-setup-manifest.json](../../../staging/project-eagle/opencode2api-20261023/provider-setup-manifest.json) records the new setup file hashes.

Current process can be reused/started without duplicate workers:

```powershell
.\tools\opencode2api\provider_service.ps1 -Action status
.\tools\opencode2api\provider_service.ps1 -Action start
```

The setup/key page is [http://127.0.0.1:18082](http://127.0.0.1:18082). The UI and API share one hidden Python process bound to loopback only. Restarting this process reloads the saved secret-free status and connection, without automatically sending API tests. `provider_service.ps1 -Action stop` targets only the recorded Python process after identity checks. Start it again after Windows reboot. No startup task or extra game BAT was created; the Paimon owner can integrate service startup into their existing bootstrap within their scope. Game launcher/runtime/Phone/HUD/shared deployment files remain untouched here. The old Go process on18080 is retained as the user requested earlier; it is no longer the selected backend.

OpenAI is an authorized alternative if Groq later cannot be used. Since no OpenAI key was needed, it is not configured as an automatic runtime fallback. The local setup page can accept the user's OpenAI key then; selection tests Groq first and only proceeds to OpenAI after Groq fails. OpenAI candidates are small text models discovered with that supplied key (`gpt-4.1-mini`, then `gpt-4o-mini` if listed), with at most three short verification requests, no tools and bounded output. Selection uses official [OpenAI model documentation](https://developers.openai.com/api/docs/models/gpt-4.1-mini) and [Groq API parameters](https://console.groq.com/docs/api-reference).

**Ready for the Paimon integration owner through filesystem handover. In-game acceptance still belongs to the user.** No other-chat message sent, no shared game-write lock acquired. The older sections below describe the initial OpenCode setup and failure history only.

## Historical OpenCode anonymous setup

**Local gateway installed and running; upstream chat is NOT verified working.** A synthetic text request received HTTP 429: `Free usage limit reached. Subscribe to OpenCode Go to keep going`. The user chose to retain anonymous/free configuration and wait rather than supply a paid upstream key, then requested other free API options. Do not label this connection as an operational Paimon AI backend.

## Ownership and integration contract

This chat owns only `tools/opencode2api/**`, `staging/project-eagle/opencode2api-20261023/**`, this document and its own work item. It has not changed `tools/eagle-dialogue`, Phone/Sidecar/HUD, the game launcher, runtime game files, archives or shared deployment state. No game was launched. No game-write lock was needed or acquired. No messages were sent into another chat.

The secret-free candidate is [connection.json](../../../staging/project-eagle/opencode2api-20261023/connection.json):

```json
{
  "base_url": "http://127.0.0.1:18080/v1",
  "model": "deepseek-v4.1-flash-free",
  "api_key_env": "EAGLE_OPENCODE_API_KEY",
  "timeout_seconds": 100,
  "extra_body": {"tool_choice": "none"}
}
```

The actual file additionally records `readiness.status=upstream_quota_blocked` and `chat_verified=false`. The model ID was selected from the live gateway's authenticated `/v1/models`, not guessed. It is a candidate, not a successful model test or a quality recommendation. The caller sends `POST <base_url>/chat/completions`, `model`, `messages`, `stream:false`; merge `extra_body` into that JSON object. Only consume nonempty `choices[0].message.content`; reject tool calls, missing text, incomplete responses and non-2xx HTTP statuses. Do not present an error response or reasoning as Paimon's spoken reply.

`tool_choice:none` is recommended for this text-only caller but has not been verified against a successful upstream completion. The baseline smoke request contained only model/messages/stream and failed with 429. The gateway internally adds OpenCode tool schemas and streams on the anonymous lane, then collapses to JSON for nonstreaming callers (pinned source `internal/gateway/upstream.go`, `prepareAnonymousBody`). Source inspection found no production `os/exec`, `exec.Command`, `os.Getenv` or `UserHomeDir` calls in its Go sources. This is an HTTP gateway, not a local tool execution loop. Do not add any tool executor to Paimon.

The game begins **2010-01-01**. Every request must receive the current game date, dated observations and only EagleTimes news available on/before that game date from the companion caller. A modern model contains later knowledge; a prompt cutoff reduces disclosure but is not a hard knowledge boundary. No web search tool is needed. The provided `paimon` and `cutoff` smoke cases remain unexecuted because the first chat request hit quota.

## Installed upstream and boundaries

- Repository: [jasonxu114514/opencode2api](https://github.com/jasonxu114514/opencode2api).
- Pinned release: [v1.4.3](https://github.com/jasonxu114514/opencode2api/releases/tag/v1.4.3), commit `f0f064f31d634b327e1c9ec9b3d49d1a83f724bb`.
- Windows amd64 release archive SHA-256 was compared with its release checksum before extraction; see [download-verification.json](../../../staging/project-eagle/opencode2api-20261023/download-verification.json). The GitHub API returned real release assets even though the browser-cached Releases page showed none.
- EXE SHA-256: `6df44c40b2c60f704a7c6663d96ba2a1651f41498d7992b88a9fadc8aaa2d36c`. Binary/source locations are recorded in [install.json](../../../tools/opencode2api/install.json).
- The distinct [TiaraBasori/OpenCode2API](https://github.com/TiaraBasori/OpenCode2API) wraps OpenCode CLI/server and defaults to reusing its local home/login state; it was not installed. The direct Go gateway avoids that credential dependency.
- API binds **127.0.0.1:18080** only. WebUI disabled, no listener on 18081, direct upstream networking, no public endpoint, no proxy pool, no firewall changes.
- Upstream `zen_keys` and `go_keys` are empty, `anonymous:true`, `models.free_only:true`. No Codex, ChatGPT, OpenAI or other existing login/API credential was read or reused.
- A fresh random local authentication key was generated. It is in the dedicated private `tools/opencode2api/state/config.json` and the Windows per-user environment variable `EAGLE_OPENCODE_API_KEY`. It authenticates the loopback gateway only and is not a paid upstream credential. Private state directory inheritance was disabled and access restricted to the current user and SYSTEM. `config.redacted.json` in staging contains no key.
- Existing Codex/terminal/game processes may have stale environment blocks. Restart the caller after provisioning, or have the integrating agent read only this named per-user environment variable in a fresh shell. Never copy the secret into connection.json, documentation or chat.

## Checks and observed results

[verification.json](../../../staging/project-eagle/opencode2api-20261023/verification.json) records the live checks. `/healthz` returned 200/ready with live catalog, authenticated `/v1/models` returned 200 and 8 free IDs; missing authentication returned 401. Health/catalog readiness does not prove inference availability: the gateway treats quota/auth/timeouts as inconclusive and can remain healthy during these upstream failures.

[The synthetic chat evidence](../../../staging/project-eagle/opencode2api-20261023/check-deepseek-v4.1-flash-free-basic.json) records `stream:false`, HTTP 429 and the complete upstream error without credentials. The gateway's automatic first-minute availability probes also received `http_429` for all 8 exposed models; see [initial-gateway.log](../../../staging/project-eagle/opencode2api-20261023/initial-gateway.log). Those probes and one smoke request were the first traffic from this setup. The server internally tried its documented anonymous lanes; no custom proxy/IP/account rotation was added. We cannot infer the exact quota scope or reset time from that error. No successful reply, personality, memory or date-cutoff acceptance is claimed.

`service.ps1 start` was run repeatedly and reused the same owned PID 19048. Process identity guards compare executable, exact configuration argument and process start time before reuse/stop. The initial timestamp comparison was repaired for PowerShell's automatic JSON date parsing, then status/start reuse passed. The stop/restart lifecycle test was rejected by automatic approval review (`blocked by policy`); it did not execute. Stop code is available but actual stop/restart is unverified.

No in-game validation was attempted; that remains with the user. No automatic paid fallback was configured. No recurring quota monitor or scheduled task was created. The upstream gateway itself refreshes metadata and periodically probes free availability while running.

## Service commands and recovery

From `C:\Users\LENOVO\Desktop\GTA`, in PowerShell:

```powershell
.\tools\opencode2api\service.ps1 -Action status
.\tools\opencode2api\service.ps1 -Action start
.\tools\opencode2api\service.ps1 -Action stop
```

The start command verifies the pinned executable hash, loopback-only API, disabled WebUI, free-only anonymous route, official upstream origins and no external proxies or upstream keys. It refuses a port occupied by another process. The background process is hidden. No Windows startup task/service or extra game BAT was created: use `start` again after Windows reboot. Logs/cache/private config live under `tools/opencode2api/state`.

To recheck later, first review `/v1/models` and make one bounded synthetic call:

```powershell
python -B .\tools\opencode2api\check_api.py --model deepseek-v4.1-flash-free --case basic --tool-choice-none
```

This script checks that the model still appears in the live local catalog before sending a synthetic prompt; it does not read any external credential store or use environment HTTP proxies for loopback. It writes secret-free evidence to staging. Only after basic success run `--case paimon --tool-choice-none` and `--case cutoff --tool-choice-none`, assess the response manually, then update connection readiness and hand over to the Paimon agent. A model listing alone must not clear the blocked status. Avoid repeated requests while quota is exhausted.

Recovery scope is isolated: stop only this owned gateway with its controller, then retain/archive its service and staging folders. No game rollback is involved. If removing the per-user `EAGLE_OPENCODE_API_KEY`, compare it with this dedicated config key first and remove only on a match, so a later owner is not affected. The controller's `publish-key` action can republish the same local key if missing and refuses a mismatching existing user value.

## Other free APIs requested by the user

Checked official documentation on 23 October 2026; no provider accounts created and no alternative API requests sent. Each needs the user's own provider key. The user's existing OpenAI API key is reserved as a last resort, with no automatic chargeable fallback.

| Option | Direct compatible base URL | Verified free-tier facts |
| --- | --- | --- |
| Groq | `https://api.groq.com/openai/v1` | Published Free limits for `openai/gpt-oss-120b`: 30 RPM, 1,000 requests/day, 8,000 tokens/minute, 200,000 tokens/day. Actual organization limits appear in console. Stay on Free; paid Developer upgrade is a separate action. |
| Gemini | `https://generativelanguage.googleapis.com/v1beta/openai` | Limited models have free input/output. Quotas depend on project and model; check AI Studio. Free-tier content may be used to improve products. |
| OpenRouter | `https://openrouter.ai/api/v1` | Free plan: 50 requests/day without buying credits. Choose a current `:free` model; availability is provider-dependent. Useful as a fallback for occasional chat. |

Suggested first trial for this project: **Groq Free**, because its published allowance and direct compatibility make a bounded Paimon text trial straightforward. This is an implementation recommendation, not a measured character-quality comparison. Keep context/history bounded; request-count allowance can be undercut by token limits. Gemini is another direct option if its active project quota fits. Any model should be discovered with the user's actual key and evaluated before activation.

Primary sources: [Groq compatibility](https://console.groq.com/docs/openai), [Groq Free limits](https://console.groq.com/docs/rate-limits), [Groq billing](https://console.groq.com/docs/billing-faqs), [Groq Free billing FAQ](https://community.groq.com/t/do-i-get-charged-for-anything-on-the-groq-free-plan/832), [Gemini compatibility](https://ai.google.dev/gemini-api/docs/openai), [Gemini pricing/data use](https://ai.google.dev/gemini-api/docs/pricing), [Gemini quotas](https://ai.google.dev/gemini-api/docs/rate-limits), [OpenRouter pricing](https://openrouter.ai/pricing/), [OpenRouter limits](https://openrouter.ai/docs/api/reference/limits).

Status: **handoff — local setup complete, anonymous inference quota blocked; alternative provider choice/key pending.** The parent Paimon chat should read this document and connection readiness before integration. Shared README/Dialogue current-state are owned by that active chat and were not concurrently edited here.
