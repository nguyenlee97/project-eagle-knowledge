# Citlali Story Quest #1 (`"Where the Night-Wind Keeps Your Hue"`) — E2E Architecture, DAG Proof & Live DirectX 9 QA Report

- **Date:** `2026-11-06`
- **Agent / Conversation:** Antigravity (`9b8e4d82-749a-40d1-a34f-9454cc6c822b`)
- **Target Runtime:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Character / Ped ID:** Citlali — Granny Itztli of the Masters of the Night-Wind (`char_id = "citlali"`, `ped_id = 49430`, `theme_rgb = [192, 132, 252]`)
- **Campaign ID:** `"citlali_sq1_color_of_eternity"` (Multi-Story-Quest ready: exports both `STORY_QUEST_CAMPAIGN` and `STORY_QUEST_CAMPAIGNS = [STORY_QUEST_CAMPAIGN]`)
- **Final Verdict:** **`100% PASS` (Zero-Core-Edit Verified • `v2.0.0` Movie-Poster & `WaifuLink Card Hub v2.0` 3-Tab Certified • `44` Nodes • `569` Beats • `43/43` Unique CGs incl. `citlali_sq1_poster.jpg` • `17/17` Live D3D9 `1920x1080` Screenshots • `11/11` `eagle_doctor.py` PASS)**

---

## 1. Zero-Core-Edit Compliance & Deliverable Inventory

In strict compliance with multi-agent parallel isolation (`Furina`, `BGM`, `HUD Redesign`), **zero core runtime files were modified** (`eagle_story_quest.py`, `EagleCompanion.py`, `eagle_dating_sim.py`, and `cleo/hud.lua` remain untouched). `StoryQuestEngine.discover_campaigns()` automatically discovers `eagle_story_quest_citlali.py` on boot.

| Deliverable | Path | Metrics / Verification |
|---|---|---|
| **Campaign Pack (Zero-Core-Edit)** | `Project Eagle/gta sa gameplay-lab/eagle_story_quest_citlali.py` | `496,529` B, `44` nodes, `569` Literary English beats, `22` choice gates, `2` Combination Gates, `5` endings, `100%` `CFont` printable ASCII (`0x20..0x7E`), `max_inner_thought = 133 <= 138` |
| **42 Event CG Pack (`16:9`)** | `Project Eagle/gta sa gameplay-lab/ui_assets/story_quest_cgs/citlali/*.jpg` | `42/42` files, `1376x768` RGB JPEG, `42/42` distinct SHA-256 hashes, generated 100% via internal `image-generator` with official HoYoverse character refs & `Base -> Diff` continuity |
| **5-Chapter Narrative & Causal Bible (`v1.1`)** | `docs/project-eagle/story-quest-citlali-5ch-narrative-and-causal-bible-2026-11-06.md` | Adversarial AI Review `APPROVED WITH TARGETED REFINEMENTS`; all `33/33` `P0`/`P1`/`P2` refinements applied & verified |
| **Standalone Offline HTML Preview** | `docs/project-eagle/citlali-story-quest-5ch-full-preview.html` | `255,767` B (`file://` zero-server Interactive VN Player + 44-Node Causal Flowchart + 42-CG Gallery + 569-Beat Literary Script Reader) |
| **Corpus & DAG Proof Suite** | `staging/project-eagle/story-quest-citlali-impl-20261106/` | `37` canon/fanfic corpus files (`755,580` B), `verify_citlali_5ch_dag.py`, `citlali_5ch_dag_proof.json`, `part_a_qa_summary.json`, `live_d3d9_qa_results.json`, `manifest.json` |

---

## 2. Mathematical DAG Proof & Part A Offline Engine QA (`part_a.db`)

Verified identically across both `verify_citlali_5ch_dag.py` and `eagle_story_quest_citlali.py`:
- **Reachability & Termination:** `44/44` visited nodes, `0` dead-ends, `0` cycles, `36,669` distinct state signatures (`validate_campaign_pack(require_cgs_on_disk=True) -> ok: True, errors: []`).
- **Exact Trajectory Enumeration:**
  - **Rational Play (`priority_unlock` active on Combo Gates):** **`6,355` trajectories** — `END_TRUE = 1,242` (`19.54%`), `END_GOOD = 665` (`10.46%`), `END_NEUTRAL = 2,228` (`35.06%`), `END_BAD_1 = 1,024` (`16.11%`), `END_BAD_2 = 1,196` (`18.82%`).
  - **Full Open Enumeration (player may deliberately choose caution/fallback at unlocked gates):** **`8,372` trajectories** — `END_TRUE = 1,242` (`14.84%`), `END_GOOD = 1,729` (`20.65%`), `END_NEUTRAL = 2,228` (`26.61%`), `END_BAD_1 = 1,024` (`12.23%`), `END_BAD_2 = 2,149` (`25.67%`).
- **Pairwise Non-Dominance & Flag Ablation:** `13/13` Chapter 1–4 binary choices verified pairwise non-dominated (`0` dead traps); `11/11` Chekhov's Gun flags (`F01_SEAL_FROST_READ` .. `F11_CLAW_IKTOMI_FEATHER`) yield strictly negative `END_TRUE` deltas when ablated; `N17` second-chance handkerchief (`Bond >= 7` & `Insight >= 8`) and `N25` Ororon harmonic spindle recovery (`Insight >= 11` + `3` diagnostic clues) verified in `part_a.db`.
- **Part A Offline SQLite QA (`run_part_a_offline_qa.py`):**
  - Unlocked **`5/5` Endings**, **`42/42` CGs**, **`66` Checkpoints**, and triggered **`118` voice cues** across all **`8/8` Asami Tano JP `.wav` buckets** (`24` `.wav` files verified on disk).
  - Verified `on_touch(16, 1)` stage advance, `[H]` Hide UI restore-before-advance safety, `[B]` Backlog, `[J]` Flowchart Checkpoint Jump (`GATE:C22_FINAL`, `GATE:C11_A`, `GATE:C18_C_GATE2`), and `close_and_autosave()` resume cursor fidelity.

---

## 3. Live DirectX 9 (`1920x1080`) In-Game Verification & 11-Screenshot Audit

Executed inside `EagleCoordLock("ingame-runtime", chat="9b8e4d82-749a-40d1-a34f-9454cc6c822b")` via `run_citlali_live_d3d9_qa.py` (`exit code 0`):

1. **Launcher & Doorstep Integration (`Shots 01–02`):**
   - `01_app13_waifulink_citlali_launcher.png` (`1920x1080`, `mean_lum=37.7`): App 13 WaifuLink `DATE & VISIT` tab displays `Story Quest: Where the Night-Wind Keeps Your Hue / Endings 0/5 - Start Ch.1 - Pure VN`.
   - `02_verona_doorstep_f9_menu.png` (`1920x1080`, `mean_lum=60.3`): At Citlali's Verona Beach sanctuary (`[814.50, -1769.00, 13.40]`) beside 3D Citlali (`ped_id = 49430`), `[F9]` highlights `<< [6] Story Quest: Where the Night-Wind Keeps Your Hue (5 Ch - Pure VN - Endings 0/5) >>`.
2. **Pure VN Lockout, Mouse Patch & Touchscreen (`Shots 03–04`):**
   - `03_ch1_doorstep_opening_telepathy.png` (`1920x1080`, `mean_lum=110.6`): Launched via real key `[6]` (`0x36`); verified `CPad::UpdateMouse` (`0x0053F509`) NOP-patched `f3 a5 -> 90 90`, `wl_typing_active == "0"` (zero `[F6]` AI free-text bar), and live DirectInput LMB click registered `code = 16, arg = 1` in `0x00CAFE60`.
   - `04_n02_choice_gate_c01_preset.png` (`1920x1080`, `mean_lum=100.0`): Preset Choice Gate `C01` rendered cleanly over `ch1_02_key_frost_ward_diff.jpg`.
3. **`Base -> Diff` Continuity, Dual-Channel Telepathy & Asami Tano JP Voice (`Shots 05a–05b`):**
   - `05a_n03_sanctuary_wake_base.png` (`mean_lum=78.1`) -> `05b_n03_itzpapa_blush_diff.png` (`mean_lum=77.3`): Seamless `1920x1080` `Base -> Diff` transition in Citlali's study with Night-Wind rose-lavender (`#C084FC`) HUD accents and Citlali's blushing telepathic `inner_thought` leak.
   - Win32 MCI Telemetry (`GET /api/dating/voice_settings`): Verified **`39` live Asami Tano JP `.wav` clips played with `mci_ok == True`** across **all `8/8` voice buckets** (`greet_doorstep: 4`, `vn_sweet_happy: 10`, `vn_shy_blush: 12`, `vn_playful_tease: 5`, `vn_tender_love: 2`, `outing_cruise: 2`, `outing_bump_rescue: 3`, `outing_arrive_photo: 1`).
4. **VN Controls, Combination Gate #2 & Multi-Ending Time-Jump (`Shots 06–10`):**
   - `06_hide_ui_pure_cg.png` (`mean_lum=88.0`): Real `[H]` (`0x48`) hotkey hides HUD for pure `16:9` CG appreciation.
   - `07_backlog_overlay.png` (`mean_lum=50.6`): Real `[B]` (`0x42`) hotkey opens `DIALOGUE & DECISION BACKLOG`.
   - `08a_flowchart_modal_j.png` (`mean_lum=40.1`) & `08b_combo_gate2_ukumbuko_bridge.png` (`mean_lum=55.6`): Real `[J]` (`0x4A`) hotkey opens `CAUSAL FLOWCHART & CHECKPOINT TIME-JUMP` at `N29_C4_GATE2`, followed by `[COMBINATION GATE #2 -- UKUMBUKO RESONANCE BRIDGE]` unlocked over Xilonen, Mavuika, Citlali, and Aether.
   - `09_ending_true_eternal_sunrise_vow.png` (`mean_lum=122.0`): `TRUE ENDING - Where the Night-Wind Keeps Your Hue` (`Endings 1/5`, `Bond 20 Insight 10 Clues 7/11`).
   - `10_ending_bad1_stranger_shore.png` (`mean_lum=128.7`): Instant Flowchart Jump to `N17` -> Route A solo sacrifice -> `BAD ENDING I - White Canvas on Verona Shore` (`Endings 2/5`).
5. **Clean Exit, Pristine State Restoration & Doctor Audit:**
   - Real `[Backspace]` (`0x08`) exited Story Quest and restored `CPad::UpdateMouse` to `f3 a5`.
   - `cleo/EagleLuaErrors.log`: **`0` errors**.
   - `try ... finally` terminated `gta_pe.exe` & `EagleCompanion.py`, restored pristine `eagle_companion.db`, `waifulink.sqlite3`, `EaglePhoneState.lua`, and sanitized `EaglePhoneHUD.dat` (stripped all `-wal`/`-shm`), then released `ingame-runtime.lock`.
   - Post-cleanup `eagle_doctor.py`: **`11/11 PASS, 0 WARN, 0 FAIL`**.

---

## 4. `StoryQuestEngine v2.0` & `WaifuLink Card Hub v2.0` Theatrical Movie-Poster Upgrade (`v2.0.0`)

Following the integration of `WaifuLink Card Hub v2.0` and `StoryQuestEngine v2.0`, `eagle_story_quest_citlali.py` was upgraded to `version = "2.0.0"` with zero edits to `eagle_story_quest.py`, `hud.lua`, or `cleo/EagleWaifuCardHub.lua`:

1. **`16:9` Theatrical Movie Poster (`citlali_sq1_poster.jpg`):**
   - Generated exclusively via Antigravity's internal `image-generator` subagent using official Citlali & Traveler Aether references (`citlali-official-directory.png`, `waifu_citlali.png`, `citlali_wish_itzpapa.png`, `aether_official.png`), completely free of text, watermarks, or logos, and deployed at `Project Eagle/gta sa gameplay-lab/ui_assets/story_quest_cgs/citlali/citlali_sq1_poster.jpg` (`1376x768`, `448,707` B).
2. **`STORY_QUEST_CAMPAIGN` v2.0 Metadata (`100%` RenderWare `CFont` Clean ASCII `0x20..0x7E`):**
   - `"poster_cg"`: `"ui_assets/story_quest_cgs/citlali/citlali_sq1_poster.jpg"`
   - `"title"`: `"Where the Night-Wind Keeps Your Hue"`
   - `"subtitle"`: `"Opalstar Chronicle: Act I - The Color of Eternity"`
   - `"synopsis"`: `"Colorless frost creeps across Granny Itztli's Verona sanctuary as an ancient Night-Wind scroll bleaches the hue and sweetness from her memories. Gather eleven hidden clues beside Citlali before the White Surge silences your shared telepathy forever."` (`249` chars — spoiler-free, wraps cleanly into `4` balanced lines at `width=68` with zero clipped words).
3. **Part A Offline Suite (`test_citlali_sq_v2_offline.py` — `100% PASS`):**
   - Verified `validate_campaign_pack(require_cgs_on_disk=True)` (`43/43` `1376x768` JPEGs, `43/43` unique SHA-256 hashes), `49`-node / `33`-column 2D Causal Graph (`0` coordinate overlaps), `TIME-JUMP HERE` (`arg=87`) to `N02`, `Slot 0` Auto-Save + `Slot 1` Manual Save/Load exact `(node_id, beat_idx, cg, bond, insight, flags)` round-trip, and multi-campaign per-heroine isolation.
4. **Live DirectX 9 (`1920x1080`) 3-Tab `PAGE_STORY_QUEST` Verification (`run_citlali_card_hub_v2_live_qa.py` — `exit code 0`):**
   - `11_v2_citlali_hub_cards.png` (`mean_lum=37.9`): Citlali's 3-card `WaifuLink Card Hub v2.0` in Night-Wind Lavender (`#C084FC`) with live Natlan BGM (`Soothing of Soul and Sand`).
   - `12_v2_sq_tab1_overview_poster.png` (`mean_lum=50.3`): **`1. OVERVIEW & PLAY`** displaying `16:9` `citlali_sq1_poster.jpg`, gold title, rose subtitle, and complete `4`-line `synopsis` with zero text clipping or aspect distortion.
   - `13_v2_sq_tab2_causal_flowchart_2d.png` (`mean_lum=36.1`): **`2. CAUSAL FLOWCHART 2D`** (`Columns 1-4 / 33`, `0` overlapping nodes, gold orthogonal edges) + verified live **`TIME-JUMP HERE`** (`arg=87`) jumping directly into `N02` Choice Gate.
   - `14_v2_sq_tab3_saveload_slots.png` (`mean_lum=49.1`) & `15_v2_slot1_restored_beat_cg.png` (`mean_lum=96.6`): **`3. SAVE / LOAD SLOTS`** displaying `AUTO-SAVE` (`Slot 0`) + `SAVE SLOT 1` (`[CH1] Cabbages, Latches & Iktomi Down`, `16:9` `ch1_05_ororon_cabbage_chaos.jpg` preview); clicking **`LOAD SLOT`** (`arg=98`) restored exact `N04` beat `2` (`[3/3]`) + `ch1_05_ororon_cabbage_chaos.jpg` + blushing `inner_thought` in live DirectX 9.
   - Post-QA cleanup restored pristine DBs/HUD, verified `EagleLuaErrors.log == 0`, released all locks, and passed `eagle_doctor.py` **`11/11 PASS`**.

