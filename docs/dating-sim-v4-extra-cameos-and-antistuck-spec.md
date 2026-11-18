# WaifuLink v4.0 — Extra Genshin Impact Cameo Scenarios & Anti-Stuck Guardrail Standard

## 1. Mandatory 30-Scenario Standard per Waifu (20 Core + 10 Extra Genshin Cameo Scenarios)
Every character in the 6-Girlfriend Roster (`Hu Tao`, `Furina`, `Citlali`, `Columbina`, `Kirara`, `Vesna`) MUST include:
- **20 Core Romance Scenarios (`4 Core Scenarios × 5 Stages`)**: Focused on deep 1-on-1 emotional progression with Traveler Aether.
- **10 Extra Genshin Impact Daily-Life & Cameo Scenarios (`2 Extra Scenarios × 5 Stages`)**: Built **extra on top of the 20 Core Scenarios** (never reducing the 20 Core Scenarios), featuring canonical Genshin Impact friends, mentors, and cross-region encounters with **minimum 4 unique 16:9 CGs per scenario (`40 Extra Cameo CGs + 80 Core CGs = 120 Scenario CGs per Waifu`)**.
- **Stage-Responsive Cameo Reactions**:
  - **Stage 1 (0–199 AFF)**: Friendly group hangouts & workplace banter (e.g., eating at Wanmin Restaurant with Xiangling, Xingqiu & Chongyun; auditing Zhongli's receipts at Wangsheng Parlor).
  - **Stage 2 (200–399 AFF)**: Cultural outings & harbor encounters (e.g., watching Yun Jin sing opera at Heyu Tea House; bumping into Keqing & sleepy Ganyu at the night market while Aether carries her bags).
  - **Stage 3 (400–599 AFF)**: Friends spot the unspoken romantic sparks & tease them (e.g., Xingqiu & Chongyun noticing her leaning on Aether's shoulder; traveling to a festival and getting Couple Sparklers from Yoimiya & a teasing ballad from Venti).
  - **Stage 4 (600–799 AFF)**: Caught red-handed on a secret romantic date! (e.g., Xiangling & Guoba catching them feeding each other hand-in-hand; Keqing & Ganyu freezing in crimson-faced shock when witnessing a moonlit bridge kiss).
  - **Stage 5 (800–1000 AFF)**: Openly devoted couple vacation & Guardian's blessing (e.g., Fontaine honeymoon patisserie trip with Furina; returning to Wangsheng Parlor with matching rings for Zhongli's solemn Osmanthus tea blessing).

## 2. Pre-Generated Dialogue Options + Custom Free-Text Input with AI Anti-Stuck Guardrail
Every node in all 30 Scenarios provides:
1. **3 Pre-Generated Dialogue Options (`[1] BEST +15`, `[2] GOOD +10`, `[3] AWKWARD +0`)**.
2. **Custom Free-Text Input Box (`allow_custom_input = True`)** evaluated by `check_vn_input_relevance()` + `gpt-6-luna` (`WAIFULINK_V4_VN_NODE_EVAL_FORMAT`):
   - **1st Off-Topic / Unrelated Reply (`off_topic_action = "REASK_CURRENT_NODE"`, `node_retry_count = 0 -> 1`)**: The AI has full authority to either playfully call out Aether's distraction OR briefly answer his random tangent in 1 sentence and **explicitly re-ask the current scene question**, keeping the current node open so the player can answer properly.
   - **2nd Consecutive Off-Topic Reply (`off_topic_action = "ANTI_STUCK_BRIDGE"`, `node_retry_count >= 1`)**: To guarantee a scenario **NEVER gets stuck**, on a second consecutive off-topic reply the Waifu playfully takes the lead (`+10 GOOD` fallback score), resets `node_retry_count = 0`, and smoothly bridges to the next scene node (`node_idx + 1`).
