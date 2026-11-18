# Paimon Agent — EaglePhone actions and long conversations

Target: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`. This continues the interrupted chat `01a163eb-fc33-79b0-8f8e-16fe17601003` under the existing user authorization. The19-target transaction is applied. Cash$9,057, bank$5,500, savings$2,000, loan$0 and three pending tickets match the final old-host capture;12 protected hashes are unchanged. The shared write lock is released. Native gameplay acceptance remains pending.

## Behavior

Paimon can read the Phone's portfolio, markets, bank, loans, sports, lottery, life, map, settings, diagnostics and dated news. Three function tools expose factual state, discover exact action schemas and execute validated Phone actions. The Engine's existing dispatcher performs the operation; the AI does not calculate or overwrite balances. Missing amounts, symbols, picks, destinations and numbers cause a rejection/request for details. Random ticket numbers require an explicit request. All money and betting are fictional game mechanics.

The web page retains three modes:

- **Sample wallet:** isolated real Engine math, no RAM/process bridge or game files. Initial cash $30,000, bank $5,500, savings $2,000 and loan $1,000. Default Engine tickets are also present; they are included in sample net worth. Each new conversation creates a separate sample wallet.
- **Chat only:** conversation without wallet tools.
- **Live wallet:** the actual running Phone Engine, requiring fresh attached-game context. Mutations affect fictional game money through the same dispatcher as Phone buttons. Diagnostics/teleport/test actions only run when requested; a dispatcher receipt does not certify that a background gameplay test finished.

Native Paimon uses the same live Phone tool adapter through a loopback endpoint. There is no second native wallet. The existing launcher and app11 entry remain the entry points. No game is launched by this task.

## Transport, model and execution boundaries

Input is now bounded at **8,192 printable English ASCII characters** and full output at **16,384 characters**. Web input uses a multiline field, flattened to the printable transport on send. Enter sends; Shift+Enter inserts a line break; editing a nonempty draft keeps arrow keys for text navigation. Native protocol2 sends full input and returns up to75 pages of220 characters. LEFT/RIGHT reviews reply pages. Legacy protocol1 retains its100/160 limits.

The character keeps the2010 game-date rules and existing credential/model profile. Agent requests use `gpt-6-luna` through Chat Completions with `reasoning_effort=none`, because Luna functions on that endpoint require it; chat-only retains the configured effort. The provider rejected the earlier low-reasoning function request with an explicit400 capability error. This was verified against [the official Luna documentation](https://developers.openai.com/api/docs/models/gpt-6-luna). Tool messages follow [the official function calling guide](https://developers.openai.com/api/docs/guides/function-calling).

Agent generation has a4096 completion-token floor, a100-second total deadline, six model rounds and twelve tool calls at most; native turn timeout is150 seconds. Existing API keys are resolved by their named environment reference, never copied into configuration or logs. There are no web, shell, arbitrary-file or provider-management tools.

Writes are journaled before dispatch and finished with actual before/after amounts, deltas, Engine message and applied/rejected/started/unknown status. A repeated call identity returns its prior result and rejects changed arguments. Distinct identities can represent explicitly requested repeated purchases. A crash in the uncertain dispatch window is recorded as unknown and never automatically replayed. The model is instructed to execute only requested operations and not repeat successes; this instruction is not a formal natural-language authorization proof.

Web receipts remain visible after cancellation; cancellation does not undo committed game actions. Recent journal entries can be read through portfolio/overview tools. Provider failure after an action returns the recorded result rather than silently reissuing the transaction. The full raw receipts are retained locally.

## Wallet and existing data

The Phone previously kept its economy in process memory. A final public `/api/state` capture is imported before restarting the old host. The original capture is retained in staging, and migration is immutable deployment input. New state persists separately in `cleo/EagleDialogue/phone-wallet.json`; live receipts use `agent-receipts.sqlite3`. Normal Engine HUD writes checkpoint the current economy, including actions made by ordinary Phone controls. Snapshot loading restores integer market-anchor keys and rebuilds today's newspaper.

This is Phone economy persistence, not a GTA save-slot system. Existing Paimon and Character Chat conversation databases are preserved. The old public projection cannot recover hidden in-memory flags that it never exposed; migration preserves the captured balances, market holdings, fixtures, tickets and available statistics. Do not claim recovery of a state from after the last successful capture.

## Validation

- **189/189 offline tests passed** in the final complete run (`qa/final-unittest.log`). Coverage includes scoped rollback preserving wallet/other-agent files, rejection of later source drift, native authorized day advance, and cancellation after a real sandbox bank debit.
- Four actual Luna web turns passed: $100 bank deposit, $50 BTC spot buy, one XSKT123456 ticket, and a detailed receipt-grounded read-only summary. Observed turn times were20.83s,14.12s,6.19s and6.36s. Final sample cash was$29,840, bank$5,600; exactly three action receipts, with no extra summary transaction. These observations do not imply identical future latency.
- Browser UI tested on temporary port18765 with a135-character request and an actual$25 sample deposit; the response and receipt were visibly rendered. [Screenshot](../../../staging/project-eagle/paimon-agent-20261025/qa/browser-receipt.png).
- Lua5.1 parsed the renderer and current complete HUD. JavaScript passed `node --check`. Native bytecode and protocol2 paging are covered offline; native font/input, controls and live money actions still need user gameplay acceptance.

## Installation and guarded recovery

Source/build helper: `tools/eagle-dialogue/paimon_agent_deploy.py`. Transaction: `staging/project-eagle/paimon-agent-20261025/manifest.json`. Nineteen targets include the narrow latest-Engine patch, its source mirror, native bridge, renderer, dialogue modules, immutable migration input and two superseded Paimon ownership pointers. The Engine uses an RLock to avoid nested dispatcher deadlock. Map/skin/archive/audio assets and the complete HUD are outside the transaction.

Before first apply: close GTA, keep the old Phone host available long enough to run `refresh-wallet`, then stop the verified Phone and native Paimon service. The installer requires all three to be idle, obtains `game-write.lock`, checks executable/current/candidate hashes and writes only the allowlist. It releases the lock before waiting for user gameplay.

From the workspace, with `PYTHONPATH` including `tools/eagle-dialogue` and `tools/eagle-dialogue/runtime`:

```powershell
C:\Python310\python.exe -B tools\eagle-dialogue\paimon_agent_deploy.py status
C:\Python310\python.exe -B tools\eagle-dialogue\paimon_agent_deploy.py rollback
```

Recovery requires GTA, Phone and native Paimon service closed. It refuses later drift and preserves wallet, receipt journals, conversation databases and other-agent features. Old web/VN installers are superseded by this transaction. Do not restore whole directories or force old repair scripts over the new ownership.
