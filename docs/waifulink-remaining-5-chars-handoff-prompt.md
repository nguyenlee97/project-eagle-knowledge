# 📋 WaifuLink v4.0 — Master Handoff Prompt for Building the Remaining 5 Girlfriends (`Furina`, `Citlali`, `Columbina`, `Kirara`, `Vesna`)

> [!TIP]
> **How to Use This Document in Another Conversation**
> Copy the entire block inside the **`=== BEGIN COPY-PASTE MASTER PROMPT ===`** section below and paste it into any new AI coding conversation. Specify which character(s) that conversation should build (e.g., *"Build Character #2: Furina first"*, or *"Build Citlali and Kirara"*). Every rule, file path, Python schema, lore timeline, Genshin cameo matrix, image-generation rule, and anti-stuck guardrail is self-contained below.

---

## === BEGIN COPY-PASTE MASTER PROMPT ===

```markdown
# TASK: Build Complete WaifuLink v4.0 Character Package(s) for Project Eagle (`gta sa gameplay-lab`)

You are building the complete **WaifuLink v4.0 AI-Powered Dating Sim & Visual Novel** expansion for one or more of the remaining 5 Girlfriends in **Project Eagle (`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`)**, matching the exact production standard already established and verified for **Character #1: Hu Tao**.

Before writing or modifying any files, read:
1. `c:\Users\LENOVO\Desktop\GTA\AGENTS.md` and `c:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md` (workspace & lock rules).
2. `c:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_pilot.py` (reference implementation of Hu Tao's 15 Milestone CGs, 20 Core Romance Scenarios, 10 Extra Genshin Cameo Scenarios, L1/L2/L3 Memory, and Off-Topic Re-Ask / Anti-Stuck Guardrail).
3. `c:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_dating_sim.py` (core engine, SQLite state, 5-option House Visit Event Selector, 4-Scene VN Overlay, and `gpt-6-luna` integration).
4. `c:\Users\LENOVO\Desktop\GTA\docs\project-eagle\dating-sim-v4-extra-cameos-and-antistuck-spec.md` (architectural spec).

---

## 1. CORE ARCHITECTURE & GAMEPLAY RULES (NON-NEGOTIABLE)

### 1.1 Roleplay Identity & Canonical Timeline Rule
- **Protagonist**: The player is **Traveler Aether** from *Genshin Impact* (iconic blonde braided hair, warm golden eyes, white/gold/dark-brown Traveler attire with floating scarf/cape), now living and cruising with the Teyvat cast in San Andreas (`gta sa gameplay-lab`).
- **Completed-Quest Timeline Rule**: All referenced Archon Quests, Story Quests (*Character Tales*), Tribal Chronicles, and Flagship Events MUST be treated as **already completed in the past** by Aether and the Girlfriend together. They reminisce about these shared memories naturally as things they already survived and accomplished side by side.
- **Language**: All dialogue, narration, inner thoughts, and UI prompts for WaifuLink are in **English** (for maximum nuance and consistency with Genshin Impact / visual novel transcripts).

### 1.2 5-Stage Relationship Progression (`0 – 1,000 Affection`, `200 pts / Stage`)
Progression is intentionally long-term and meaningful across 5 Stages:
- **Stage 1 (`0 – 199 Affection`)**: *Acquaintance & Playful Banter*
- **Stage 2 (`200 – 399 Affection`)**: *Close Companion & Shared Secrets*
- **Stage 3 (`400 – 599 Affection`)**: *Mutual Crush & Unspoken Tension*
- **Stage 4 (`600 – 799 Affection`)**: *Devoted Lover & Deep Intimacy*
- **Stage 5 (`800 – 1,000 Affection`)**: *Eternal Soulmate & Sacred Vow*

### 1.3 Three-Pillar Economy & Stage Gate Rules
Each 200-point Stage (`Stage A -> Stage B`) is governed by `STAGE_ECONOMY_RULES` in `eagle_waifulink_v4_pilot.py`:
1. **Pillar 1 — Visual Novel Scenarios (Primary Driver & Stage Gate)**:
   - **30 Total Scenarios per Character** = **20 Core Romance Scenarios** (`4 per Stage × 5 Stages`) + **10 Extra Genshin Cameo & Daily-Life Scenarios** (`2 per Stage × 5 Stages`).
   - **Stage Gate Requirement**: To cross a Stage boundary (`199->200`, `399->400`, `599->600`, `799->800`), the player must pass at least **3 out of 4** Core Scenarios in that Stage (`required_scenarios_per_stage = 3` out of `4` available, guaranteeing zero soft-locks).
   - **Pass Reward**: `+35 Affection` (`scenario_pass_points = 35`). Failed scenarios (`score < 20/45`) award `+10 Affection` consolation and can be replayed unlimited times until passed.
   - **Non-Hard-Locked Carryover Rule**: Scenarios are **NEVER locked** if the player advances to a higher Stage before playing them. Unplayed scenarios from earlier stages remain selectable under `[Carryover VN]` (`is_carryover = True`), awarding Affection and unlocking all 4 CGs, **without** counting toward the higher Stage's `3/4` Stage Gate.
2. **Pillar 2 — Free-Roam Chauffeur Outings (Secondary Driver)**:
   - Triggered from the Girlfriend's House Doorstep Menu (`Option [4]`).
   - Capped at **`75 Affection / Stage`** (`max 3–4 outings per Stage`):
     - `S-Rank` (`0 crashes`, smooth speed, arrives at destination): **`+25 Affection`**
     - `A-Rank` (`1 minor bump`): **`+20 Affection`**
     - `Failed` (`>= 2 crashes` or vehicle destroyed): **`0 Affection`**
3. **Pillar 3 — EaglePhone Casual Chat & Time-Apart Photo Drops (Tertiary Driver)**:
   - Capped at **`45 Affection / Stage`** (`~9–10 scored chats per Stage`):
     - `SWEET_ENGAGED`: **`+6 Affection`**
     - `NORMAL_PLEASANT`: **`+4 Affection`**
     - `LOW_EFFORT` / `RUDE`: **`0` or `-5 Affection`**
   - Always provide **3 Pre-Generated / Live-Recommended Dialogue Options (`[1]`, `[2]`, `[3]`)** alongside free-text input so the player never has to type manually unless they want to.

---

## 2. VISUAL NOVEL SCENARIO & CG SPECIFICATIONS (135 CGS / CHARACTER)

Every character requires **135 Unique Images** stored in `c:\Users\LENOVO\Desktop\GTA\data\project-eagle\dating-sim\media\`:
1. **15 Milestone CGs (`{char_id}_m01.jpg` .. `{char_id}_m15.jpg`)** — Proactive Time-Apart Smartphone Photos (`3 per Stage × 5 Stages`).
2. **80 Core Romance Scenario CGs (`{char_id}_s{1..5}_sc{1..4}_cg{1..4}.jpg`)** — `20 Core Scenarios × 4 CGs per Scenario`.
3. **40 Extra Genshin Cameo Scenario CGs (`{char_id}_s{1..5}_ex{1..2}_cg{1..4}.jpg`)** — `10 Extra Cameo Scenarios × 4 CGs per Scenario`.

### 2.1 Mandatory 4-Scene Visual Novel Flow (`4 CGs per Scenario`)
Every single Scenario (`sc1..sc4` and `ex1..ex2` across Stages `1..5`) MUST have **4 distinct 16:9 widescreen CGs** (`cg_sequence` of length 4):
- **Scene 1/4 (`node_idx = 0`, `{id}_cg1.jpg`)**: *Opening CG* — Establishes the setting, atmosphere, and initial interaction (with Choice `[1]`, `[2]`, `[3]` + Custom Free-Text Input).
- **Scene 2/4 (`node_idx = 1`, `{id}_cg2.jpg`)**: *Developing CG* — Deepens the chemistry, banter, or cameo hijinks (with Choice `[1]`, `[2]`, `[3]` + Custom Free-Text Input).
- **Scene 3/4 (`node_idx = 2`, `{id}_cg3.jpg`)**: *Climax Choice CG* — Emotional peak or pivotal romantic/comedic moment (with Choice `[1]`, `[2]`, `[3]` + Custom Free-Text Input).
- **Scene 4/4 (`finished = True`, `{id}_cg4.jpg`)**: *Ending Resolution CG* — Displays the final romantic/cameo payoff CG + score summary, and **automatically closes the VN overlay after `4.5 seconds`** (`auto_close_at = time.time() + 4.5`) to return to GTA SA!

### 2.2 Visual & Content Rules for CG Generation
- **Direct Character Reference Mandatory**: Never generate character art from text descriptions alone. Always pass the canonical reference image (`c:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\ui_assets\waifu_{char_id}.png` or `c:\Users\LENOVO\Desktop\GTA\data\project-eagle\dating-sim\media\{char_id}_cg1.jpg`) into the image generator (`refer style genshin`) so exact hair, eyes, accessories, and Genshin Impact cel-shaded anime style remain 100% consistent.
- **Couple Presence in Scenario CGs**: Scenario CGs (`_cg1` .. `_cg4`) must feature **both Traveler Aether AND the Girlfriend** interacting in the scene (not solo portraits). In Stages 4 and 5, Scenario CGs must be **genuinely romantic couple CGs** (holding hands, forehead-to-forehead, princess carry, slow dancing, resting on Aether's shoulder, sunset kiss silhouette).
- **Cameo Presence in Extra Scenarios (`_ex1`, `_ex2`)**: Extra Cameo Scenario CGs must visually include **Aether + the Girlfriend + the named Genshin Impact cameo character(s)** in the frame!
- **15 Milestone CG Spice Progression (`m01` .. `m15`)**:
  - `Stage 1 (m01–m03, Affection 60/125/185)`: Friendly, playful daily-life selfies.
  - `Stage 2 (m04–m06, Affection 250/320/385)`: Cute, candid after-hours & relaxing moments.
  - `Stage 3 (m07–m09, Affection 450/520/585)`: Romantic golden-hour date & moonlit closeness.
  - `Stage 4 (m10–m12, Affection 650/720/785)`: Alluring evening gown, silk loungewear, or private boudoir glance.
  - `Stage 5 (m13–m15, Affection 850/925/1000)`: Glamorous, spicy/intimate morning-after or bridal vow (**strictly SFW/PG-13 tasteful romance — complete nudity or explicit NSFW is strictly forbidden**).

---

## 3. AI OFF-TOPIC RE-ASK & ANTI-STUCK GUARDRAIL (`gpt-6-luna`)

All custom free-text inputs in VN Scenarios use the 2-Strike Off-Topic Re-Ask & Anti-Stuck Guardrail (`check_vn_input_relevance()` + `WAIFULINK_V4_VN_NODE_EVAL_FORMAT` in `eagle_waifulink_v4_pilot.py`):
- **Strike 1 (`node_retry_count == 0`, `off_topic_action = "REASK_CURRENT_NODE"`)**:
  - If the player types gibberish or an unrelated question during a VN scene, the AI **does not advance `node_idx`**.
  - Instead, the Girlfriend playfully teases Aether for daydreaming (or briefly answers his side question in 1 sentence) and **explicitly re-asks her current scene question** (`score = 0`, `node_retry_count = 1`).
- **Strike 2 (`node_retry_count >= 1`, `off_topic_action = "ANTI_STUCK_BRIDGE"`)**:
  - If the player is still off-topic on the second attempt, the Girlfriend takes the initiative in-character (e.g., grabs Aether's hand/sleeve and decides for both of them), awards **`GOOD (+10)`**, resets `node_retry_count = 0`, and **advances to `node_idx + 1`** so the scenario can **never get stuck**.

---

## 4. EXACT PYTHON DATA SCHEMAS (PLUG-AND-PLAY WITH `eagle_waifulink_v4_pilot.py`)

When creating data for a character `<CHAR>` (`furina`, `citlali`, `columbina`, `kirara`, `vesna`), export the following 4 structures (either in `eagle_waifulink_v4_<char_id>.py` imported into `eagle_waifulink_v4_pilot.py` and `eagle_dating_sim.py`):

### 4.1 `<CHAR>_15_MILESTONES` (`list[dict]`, 15 items `m01..m15`)
```python
{
    "id": "furina_m01",
    "milestone_num": 1,
    "stage": 1,
    "req_affection": 60,  # [60, 125, 185, 250, 320, 385, 450, 520, 585, 650, 720, 785, 850, 925, 1000]
    "spice_tier": "Stage 1 • Friendly",
    "title": "Milestone Title",
    "url": "/dating-media/furina_m01.jpg",
    "caption": "Short gallery caption.",
    "proactive_message": "In-character EaglePhone message sent after time apart when unlocked.",
    "proactive_inner_thought": "💧 Salon Solitaire's Whisper: Hidden inner thought about Aether.",
    "proactive_action_cue": "*physical action cue*",
    "reaction_choices": [
        {
            "id": "furina_m01_r1",
            "label": "🌟 Sweet/Witty Option Label (+6)",
            "player_text": "Full line Aether sends back.",
            "reply_thought": "Her inner thought upon reading Aether's reply.",
            "reply_action": "*her physical reaction*",
            "reply_text": "Her spoken/texted reply back to Aether.",
            "mood": "Delighted",
        },
        # + r2 and r3 (3 reaction choices per milestone)
    ],
}
```

### 4.2 `<CHAR>_20_SCENARIOS` (20 Core Romance Scenarios: `s1_sc1..s5_sc4`) & `<CHAR>_10_EXTRA_CAMEO_SCENARIOS` (10 Extra Cameo Scenarios: `s1_ex1..s5_ex2`)
```python
{
    "id": "furina_s1_ex1",  # or "furina_s1_sc1" for Core Romance
    "char_id": "furina",
    "stage": 1,             # 1..5
    "scenario_num": 5,      # 1..4 for Core, 5..6 for Extra Cameo
    "is_extra_cameo": True, # False for Core, True for Extra Cameo
    "cameo_cast": ["Neuvillette", "Charlotte"],  # [] for Core Romance
    "cameo_dynamic_tier": "Stage 1 Friendly Hangout: Neuvillette checks on Furina's lifestyle while Charlotte snaps a front-page photo for The Steambird.",
    "allow_custom_input": True,
    "title": "Scenario Title",
    "subtitle": "Stage 1 • Extra Cameo 1 • Location / Theme",
    "location": "In-Game / Lore Location Name",
    "cg_url": "/dating-media/furina_s1_ex1_cg1.jpg",
    "ending_cg_url": "/dating-media/furina_s1_ex1_cg4.jpg",
    "ending_scene_label": "Scene 4/4 • Finale Description",
    "cg_sequence": [
        {"scene_num": 1, "url": "/dating-media/furina_s1_ex1_cg1.jpg", "label": "Scene 1/4 • Opening: ..."},
        {"scene_num": 2, "url": "/dating-media/furina_s1_ex1_cg2.jpg", "label": "Scene 2/4 • Developing: ..."},
        {"scene_num": 3, "url": "/dating-media/furina_s1_ex1_cg3.jpg", "label": "Scene 3/4 • Climax: ..."},
        {"scene_num": 4, "url": "/dating-media/furina_s1_ex1_cg4.jpg", "label": "Scene 4/4 • Finale: ..."},
    ],
    "pass_threshold_score": 20,
    "summary_l2": "1-sentence episodic memory saved to SQLite L2 Memory when Aether passes this scenario.",
    "nodes": [
        # Exactly 3 interactive nodes (node_idx 0, 1, 2 -> Scenes 1/4, 2/4, 3/4; Scene 4/4 is the Ending Resolution screen)
        {
            "node_idx": 0,
            "cg_url": "/dating-media/furina_s1_ex1_cg1.jpg",
            "scene_label": "Scene 1/4 • Opening: ...",
            "scene_progress": "SCENE 1/4",
            "narration": "Rich visual novel narration describing the setting, cameo characters, and atmosphere.",
            "inner_thought": "💧 Salon Solitaire's Whisper: Furina's secret inner monologue.",
            "action_cue": "*expressive physical action cue*",
            "speaker_line": "Furina's spoken dialogue ending with a clear conversational hook or question for Aether.",
            "mood": "Playful",
            "choices": [
                {
                    "id": "c1",
                    "score": 15,
                    "grade": "BEST",
                    "label": "🌟 Best Option Summary",
                    "player_text": "Aether's full spoken response.",
                    "reaction_thought": "Her inner thought reaction.",
                    "reaction_action": "*her action cue*",
                    "reaction_reply": "Her spoken reply bridging to the next scene.",
                },
                # + c2 (score: 10, grade: "GOOD") and c3 (score: 0, grade: "AWKWARD")
            ],
        },
        # + node_idx 1 (Scene 2/4) and node_idx 2 (Scene 3/4)
    ],
}
```

---

## 5. CHARACTER LORE DOSSIERS & STAGE-RESPONSIVE GENSHIN CAMEO MATRICES FOR THE REMAINING 5 GIRLFRIENDS

### 💧 CHARACTER #2: FURINA DE FONTAINE (`char_id = "furina"`)
- **Home Coordinates in San Andreas**: Richman Mansion, Los Santos (`(321.5, -1180.2, 80.9)`)
- **Inner-Thought Channel**: `💧 Salon Solitaire's Whisper` (or `🎭 Focalors' Unmasked Heart`) — Contrasts her theatrical, haughty *"star of the stage"* outward bravado with her shy, deeply affectionate, praise-craving inner self who trusts Aether as the only person who knows the weight of her 500-year masquerade.
- **Completed Canon Quests (Past Reference)**:
  - *Fontaine Archon Quest Act V: Masquerade of the Guilty* (Aether witnessed her 500 years of lonely endurance in the opera house; she now lives freely as a human in her own apartment, cooking macaroni and directing theater).
  - *Story Quest: Animula Choragi Chapter, Act I ("The Little Oceanid")* (Stepping back onto the stage for *The Little Oceanid* musical after overcoming her stage trauma with Aether's support).
  - *Roses and Muskets* Fontinalia Film Festival (Winning the Furina Award as director alongside Aether, Chevreuse, Xavier, Ayaka, and Yoimiya).
- **Likes / Dislikes**:
  - *Likes*: Strawberry opera cake, La Lettre a Focalors pastry, Goldenshrimp balls, musical theater, Salon Solitaire (`usher Gentilhomme`, `Surintendante Chevalmarin`, `Mademoiselle Crabaletta`), Aether's genuine praise.
  - *Dislikes*: Being left alone in silence, bland overcooked pasta, paparazzi invading her private moments with Aether.
- **10 Extra Genshin Cameo Scenarios Matrix (`furina_s1_ex1` .. `furina_s5_ex2`)**:
  - `Stage 1 ex1` (**Neuvillette**): Running into Iudex Neuvillette at a Fontaine-style café while buying spring water and pastries; Neuvillette formally thanks Aether for bringing genuine laughter back to Lady Furina's daily life.
  - `Stage 1 ex2` (**Charlotte**): Dodging *The Steambird* reporter Charlotte's camera flash outside the theater with Aether while Mademoiselle Crabaletta accidentally photobombs the lens.
  - `Stage 2 ex1` (**Navia & Clorinde**): Afternoon tea and macarons with Spina di Rosula President Navia and Champion Duelist Clorinde; Navia playfully teases how Furina only saves the top strawberry macaron for Aether.
  - `Stage 2 ex2` (**Chiori**): Visiting *Chioriya Boutique* for custom stage wardrobe fittings; Chiori immediately notices Furina asking for gold-and-starlight accents that match Aether's scarf.
  - `Stage 3 ex1` (**Lyney, Lynette & Freminet**): Attending a magic show rehearsal at Opera Epiclese; Lyney performs a sleight-of-hand trick that produces a single Romaritime Flower right between Aether and a blushing Furina.
  - `Stage 3 ex2` (**Hu Tao Cross-Region Cameo**): Director Hu Tao visits from Liyue to collaborate on a spooky-comedic stage play; Hu Tao's teasing makes Furina cling to Aether's arm in flustered solidarity.
  - `Stage 4 ex1` (**Navia & Charlotte — Caught on a Date!**): Caught holding hands with Aether outside Patisserie *Pour la Justice* at twilight; Navia winks and blocks Charlotte's camera so the couple can escape to the harbor.
  - `Stage 4 ex2` (**Neuvillette — Rainy Evening Umbrella**): A sudden drizzle starts over the promenade as Neuvillette reflects on the court; Furina teases the Hydro Dragon to clear the skies because she's in the middle of a romantic anniversary walk with Aether.
  - `Stage 5 ex1` (**Fontaine Cast Encore — Navia, Clorinde, Lyney, Lynette**): Opening night gala where the entire Fontaine cast raises a toast to their star director Furina and her eternal leading man, Aether.
  - `Stage 5 ex2` (**Neuvillette's Official Blessing**): Beneath the Fountain of Lucine at starlight, Neuvillette offers his heartfelt blessing to Aether and Furina as eternal partners.

---

### 🔮 CHARACTER #3: CITLALI — GRANNY ITZTLI (`char_id = "citlali"`)
- **Home Coordinates in San Andreas**: Santa Maria Beach Villa, Los Santos (`(345.0, -1798.5, 4.8)`)
- **Inner-Thought Channel**: `🔮 Obsidian Mirror's Telepathy` — Since Citlali canonically shares a telepathic mental link with Aether, her inner thoughts constantly slip out (or she panics wondering if Aether just heard her heart racing through their mental bond!), while her plush pillows `Itzpapa` and `Citlalin` betray her tsundere blushes.
- **Completed Canon Quests (Past Reference)**:
  - *Natlan Archon Quest Act I–V: Incandescent Ode of Resurrection* (Divining Aether's fate in the smoke, establishing their exclusive telepathic link, weaving his Ancient Name *Tumaini* scroll, and celebrating Natlan's victory).
  - *Tribal Chronicles: Masters of the Night-Wind, Act III ("The Fading Star's Might")* (Understanding her 200-year fear of outliving short-lived friends—and realizing that immortal Traveler Aether is the one person who will never fade away from her across the centuries, which is why she entrusted him with the key to her home).
- **Likes / Dislikes**:
  - *Likes*: Inazuman romance light novels from Yae Publishing House, sparkling fruit wine / late-night drinks, staying cozy indoors, `Itzpapa` & `Citlalin` plushies, Aether visiting using his house key.
  - *Dislikes*: Being lectured like an old elder when she's flustered, Ororon accidentally spilling her secrets to Aether, waking up before noon.
- **10 Extra Genshin Cameo Scenarios Matrix (`citlali_s1_ex1` .. `citlali_s5_ex2`)**:
  - `Stage 1 ex1` (**Ororon**): Her well-meaning grandson-figure Ororon brings giant cabbages and aphids to her doorstep and innocently tells Aether, *"Granny cleaned her whole room three times because she knew you were coming!"*
  - `Stage 1 ex2` (**Kachina & Mualani**): Kachina and Mualani drop by for a Night-Wind blessing; Citlali puts on her intimidating *Granny Itztli* shaman voice, only to melt when Aether hands her a limited-edition light novel.
  - `Stage 2 ex1` (**Xilonen**): Visiting Xilonen's sunlit forge/workshop to tune phlogiston engravings; Xilonen teases Citlali for leaving her secluded sanctuary in broad daylight just to walk with Aether.
  - `Stage 2 ex2` (**Yae Miko & Kirara Cross-Region Delivery**): A special courier box from Inazuma's Yae Publishing House arrives with Chief Editor Yae Miko's personal note teasing Citlali's taste in *"Immortal Traveler × Shy Shaman"* romance novels.
  - `Stage 3 ex1` (**Mavuika**): Sharing a sunset drink with Pyro Archon Mavuika after a tournament; Mavuika grins knowingly at how relaxed Citlali looks whenever she sits beside Aether.
  - `Stage 3 ex2` (**Ororon & Chasca**): Ororon and Chasca ask Aether and Citlali to help mediate a Night-Wind / Flower-Feather patrol; Ororon whispers to Aether that Citlali's telepathic aura is glowing bright pink.
  - `Stage 4 ex1` (**Mualani & Kachina — Caught at the Hot Springs!**): Caught sharing a private twilight soak and fruit cider with Aether at the People of the Springs; Citlali hides behind `Itzpapa` as Mualani cheers for them.
  - `Stage 4 ex2` (**Mavuika & Xilonen — Late-Night Cruiser Ride**): Cruising the coastal highway with Mavuika and Xilonen; Mavuika teases that even Natlan's Sacred Flame isn't as warm as the way Citlali holds onto Aether.
  - `Stage 5 ex1` (**Ororon's Earnest Family Blessing**): Ororon formally thanks Aether for ensuring Granny Citlali will never have to face lonely centuries again, gifting them a hand-grown Night-Wind wreath.
  - `Stage 5 ex2` (**Natlan Champions' Starlit Bonfire — Mavuika, Xilonen, Mualani, Kachina**): Under a sky of woven Night-Wind stars, the heroes of Natlan celebrate Aether and Citlali's eternal bond across the centuries.

---

### 🕊️ CHARACTER #4: COLUMBINA — DAMSELETTE (`char_id = "columbina"`)
- **Home Coordinates in San Andreas**: Paradiso Sanctuary, San Fierro (`(-2458.0, 782.0, 35.2)`)
- **Inner-Thought Channel**: `🕊️ Frost Moon Lullaby` — Ethereal, serene, six-winged Seraphim/Seelie-descent sensibility. She speaks in soft, musical metaphors and sees straight through worldly illusions, yet feels a childlike wonder and profound devotion toward Aether's warm golden light.
- **Completed Canon Lore & Events (Past Reference)**:
  - *A Winter Night's Lazzo* (Her hauntingly pure hymn over Signora's resting place at Zapolyarny Palace).
  - *Harbinger #3 Lore & Frost Moon Sanctuary* (Leaving the cold political machinations of the Fatui behind to walk in the mortal sunlight with Aether, whom Childe and Wanderer warned was dangerous only because she sees the soul directly—and Aether's soul is the warmest star she has ever encountered).
- **Likes / Dislikes**:
  - *Likes*: Singing lullabies under the moon, white Glaze Lilies, warm honeyed milk tea, resting her head on Aether's shoulder with her eyes closed, songbirds landing on her fingertips.
  - *Dislikes*: Harsh industrial noise, Dottore's cold experiments, disingenuous flattery.
- **10 Extra Genshin Cameo Scenarios Matrix (`columbina_s1_ex1` .. `columbina_s5_ex2`)**:
  - `Stage 1 ex1` (**Childe / Tartaglia**): Running into Eleventh Harbinger Childe at a harbor restaurant; Childe isnervously polite around the #3 Damselette while shocked at how gently she smiles whenever Aether pours her tea.
  - `Stage 1 ex2` (**Wanderer**): Crossing paths with Wanderer on a quiet veranda; Wanderer warns Aether to stay sharp, only for Columbina to hum a harmless melody that makes a white dove land on Wanderer's hat.
  - `Stage 2 ex1` (**Arlecchino — The Knave**): Afternoon tea in a rose courtyard with Fourth Harbinger Arlecchino; mirroring *Commedia dell'arte* lore, Arlecchino is protective and respectful of Columbina, quietly assessing Aether's sincerity.
  - `Stage 2 ex2` (**Lyney, Lynette & Freminet**): Visiting the House of the Hearth siblings with Arlecchino's blessing; Columbina's gentle lullaby calms Freminet's clockwork penguin Pers as she and Aether share pastries.
  - `Stage 3 ex1` (**Sandrone — Marionette**): Inspecting an antique clockwork music box with Seventh Harbinger Sandrone; Columbina asks Sandrone to tune the melody to match the rhythm of Aether's footsteps.
  - `Stage 3 ex2` (**Venti & Zhongli Cross-Region Encounter**): Listening to windborne melodies by the cliffs where Venti's lyre and Zhongli's ancient memory recognize the Seelie-court cadence in Columbina's song—and how she now sings only for Aether.
  - `Stage 4 ex1` (**Childe — Caught Walking Hand-in-Hand in the Snow**): Childe spots Aether wrapping his golden scarf around Columbina's shoulders at twilight and grins, promising to keep their peaceful sanctuary a secret from Snezhnaya.
  - `Stage 4 ex2` (**Arlecchino's Quiet Approval**): Over crimson moonlit tea, Arlecchino tells Aether that she has never seen the Damselette open her eyes with such warmth for anyone else.
  - `Stage 5 ex1` (**Harbingers' Truce — Arlecchino, Childe, Lyney & Lynette**): A quiet candlelit dinner where Arlecchino and Childe toast to Columbina's newfound mortal happiness beside Aether.
  - `Stage 5 ex2` (**Seelie Court & Frost Moon Benediction**): Beneath an aurora sky, Columbina opens her eyes fully to gaze into Aether's golden eyes as ancient elemental spirits circle them in blessing.

---

### 📦 CHARACTER #5: KIRARA (`char_id = "kirara"`)
- **Home Coordinates in San Andreas**: Prickle Pine Villa, Las Venturas (`(1956.0, 2678.0, 10.8)`)
- **Inner-Thought Channel**: `🐾 Twin-Tail Radar` — Energetic, sunny Inazuman *nekomata* (youkai cat) courier for *Komaniya Express*. Whenever she tries to play cool, her twin tails swish, puff up, or curl into a heart shape around Aether's wrist!
- **Completed Canon Quests (Past Reference)**:
  - *Duel! The Summoners' Summit!* (Delivering international parcels across all nations with Aether and befriending Charlotte).
  - *Secret Summer Paradise / Veluriyam Mirage & Simulanka* (Exploring fairytale realms alongside Aether).
  - *Chiori's Story Quest: Cisoria Chapter, Act I* (Helping her longtime friend and outfit designer Chiori during Fontaine Fashion Week).
- **Likes / Dislikes**:
  - *Likes*: Fresh sashimi platters, sunbeams on the roof, cardboard parcels (`Urgent Neko Parcel` form), Aether gently brushing her twin tails or scratching behind her ears, 5-star delivery ratings.
  - *Dislikes*: Getting her tails soaked in heavy rain, dogs barking at her delivery boxes, late shipments.
- **10 Extra Genshin Cameo Scenarios Matrix (`kirara_s1_ex1` .. `kirara_s5_ex2`)**:
  - `Stage 1 ex1` (**Chiori**): Delivering fabric rolls to *Chioriya Boutique* with Aether; Chiori repairs a ribbon on Kirara's sleeve and teases her for purring while Aether carries the heavy boxes.
  - `Stage 1 ex2` (**Yoimiya**): Delivering sparkler materials to *Naganohara Fireworks*; Yoimiya invites Aether and Kirara to test handheld sparklers by the river.
  - `Stage 2 ex1` (**Yae Miko**): Picking up a confidential manuscript package at *Yae Publishing House*; Lady Guuji Yae Miko teases the little nekomata about why her twin tails form a heart whenever she stands near the Traveler.
  - `Stage 2 ex2` (**Charlotte**): Meeting *Steambird* journalist Charlotte at the harbor for an international courier handoff; Charlotte wants to interview Aether and Kirara as the fastest duo in Teyvat.
  - `Stage 3 ex1` (**Kamisato Ayaka & Thoma**): Delivering ceremonial tea sets to the Kamisato Estate; Thoma treats Aether and Kirara to homemade Tricolor Dango while Ayaka smiles warmly at their closeness.
  - `Stage 3 ex2` (**Keqing & Hu Tao Liyue Express Route**): An express delivery to Liyue Harbor where Keqing praises their punctuality and Hu Tao tries to recruit Kirara's cute twin tails for a parlor mascot photo.
  - `Stage 4 ex1` (**Chiori & Navia — Caught Napping on Aether's Lap!**): After a long fashion-week delivery run, Chiori and Navia walk into the back lounge to find Kirara curled up asleep with her head on Aether's lap and her tails wrapped around his waist.
  - `Stage 4 ex2` (**Yae Miko's Moonlit Shrine Tease**): Under the sakura blossoms of Grand Narukami Shrine, Yae Miko gifts Aether a sacred comb to brush Kirara's twin tails, making Kirara blush crimson.
  - `Stage 5 ex1` (**Inazuma & Fontaine Friends' 5-Star Celebration — Yoimiya, Chiori, Charlotte**): A surprise rooftop party with fireworks celebrating Kirara's 10,000th accident-free delivery alongside her partner Aether.
  - `Stage 5 ex2` (**Yae Miko & Chiori's Youkai Vow Blessing**): Chiori presents custom matching gold-and-emerald ribbons for Aether and Kirara as Yae Miko blesses the nekomata's lifelong devotion to her Traveler.

---

### ❄️ CHARACTER #6: VESNA STRIVOZHA (`char_id = "vesna"`)
- **Home Coordinates in San Andreas**: Mulholland Hillside Estate, Los Santos (`(1298.0, -798.0, 84.1)`)
- **Inner-Thought Channel**: `❄️ Snezhnayan Heartbeat` — Aristocratic yet playfully mischievous Snezhnayan noblewoman of *House Strivozha*. Outwardly poised, silver-haired, and teasingly bold with her fan and teacup, inwardly deeply protective of her older sister Danica and head-over-heels for Aether, the hero who sheltered their family when they broke away from Fatui political pressure.
- **Completed Canon / Fanon Lore Timeline (Past Reference)**:
  - *House Strivozha's Defection & Sanctuary* (Escaping Zapolyarny Palace's aristocratic schemes with her older sister Danica, establishing the *White Birch Salon* overlooking Mulholland with Aether's protection).
  - *Liyue–Fontaine Silk & Tea Trade Accord* (Working alongside Aether, Yelan, and Navia to secure independent trade routes free from Northland Bank coercion).
- **Likes / Dislikes**:
  - *Likes*: Black tea with sweet lemon preserve (`varenye`), classical waltzes, teasing her dutiful sister Danica, vintage sports cars on Mulholland Drive, Aether's warm hands against the Snezhnayan chill.
  - *Dislikes*: Fatui debt collectors, bitter black coffee, people who mistake her playful noble charm for superficiality.
- **10 Extra Genshin Cameo Scenarios Matrix (`vesna_s1_ex1` .. `vesna_s5_ex2`)**:
  - `Stage 1 ex1` (**Sister Danica Strivozha**): Afternoon tea at the Mulholland estate where dutiful older sister Danica scolds Vesna for slipping extra sweet lemon preserve into Aether's cup and winking at him across the table.
  - `Stage 1 ex2` (**Childe / Tartaglia**): Running into fellow Snezhnayan Childe at the docks; Childe recognizes House Strivozha's crest and laughs when Vesna boldly claims Aether is now her personal bodyguard and favorite companion.
  - `Stage 2 ex1` (**Yelan**): Meeting intelligence chief Yelan at *Yanshang Teahouse* to exchange trade-route ciphers; Yelan raises an amused eyebrow at how seamlessly Aether and Vesna play off each other's banter.
  - `Stage 2 ex2` (**Navia**): Hosting Spina di Rosula's Navia at the *White Birch Salon* for a pastry-and-tea exchange; Navia and Danica bond over managing their lively younger counterparts as Vesna links arms with Aether.
  - `Stage 3 ex1` (**Arlecchino**): A tense yet civilized encounter with The Knave at an opera balcony; Aether steps protectively beside Vesna, and Arlecchino respects their resolve, confirming House Strivozha is off-limits to Fatui interference.
  - `Stage 3 ex2` (**Ningguang & Keqing Trade Gala**): Attending a Liyue merchant gala where Ningguang commends Vesna's business acumen—while Vesna whispers to Aether that she only dressed up tonight to catch his eye.
  - `Stage 4 ex1` (**Sister Danica — Caught Slow-Dancing on the Balcony!**): Danica steps onto the moonlit Mulholland terrace to bring warm shawls, only to catch Aether and Vesna in an intimate waltz embrace—and quietly smiles, closing the glass doors to give them privacy.
  - `Stage 4 ex2` (**Childe & Yelan — Sunset Coastal Drive**): After outsmarting a rogue Northland Bank envoy with Childe and Yelan, Vesna pulls Aether into the passenger seat of her convertible for a romantic twilight drive along the cliffs.
  - `Stage 5 ex1` (**Sister Danica's Tearful Family Blessing**): Over House Strivozha's heirloom silver samovar, Danica entrusts Vesna's hand to Aether, thanking him for giving their family a true home and future.
  - `Stage 5 ex2` (**Mulholland Starlight Ball — Danica, Navia, Yelan, Childe**): An elegant starlit salon ball overlooking Los Santos where Aether and Vesna share the centerpiece waltz as eternal partners.

---

## 6. STEP-BY-STEP EXECUTION CHECKLIST FOR THE AGENT

When building a character `<CHAR>` in this conversation:
1. **Create Character Module**: Write `c:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_v4_<char_id>.py` containing:
   - `<CHAR>_15_MILESTONES` (`15` Time-Apart Milestone CG dicts, `m01..m15`)
   - `<CHAR>_20_SCENARIOS` (`20` Core Romance VN Scenarios, `s1_sc1..s5_sc4`, 4 scenes/CGs each)
   - `<CHAR>_10_EXTRA_CAMEO_SCENARIOS` (`10` Extra Genshin Cameo VN Scenarios, `s1_ex1..s5_ex2`, 4 scenes/CGs each)
   - `<CHAR>_STAGE_CHAT_STARTERS` (`Stage 1..5` pre-generated chat starters)
2. **Generate All 135 Unique Images (`15 Milestone CGs + 80 Core Scenario CGs + 40 Extra Cameo Scenario CGs`)**:
   - Always pass the canonical reference portrait (`c:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\ui_assets\waifu_<char_id>.png`) to the `image-generator` subagent so the character's design and Genshin anime style remain 100% authentic.
   - Save all 135 `.jpg` files into `c:\Users\LENOVO\Desktop\GTA\data\project-eagle\dating-sim\media\`.
3. **Wire into `eagle_dating_sim.py`**:
   - Register `<CHAR>_15_MILESTONES`, `<CHAR>_20_SCENARIOS`, `<CHAR>_10_EXTRA_CAMEO_SCENARIOS`, and `<CHAR>_STAGE_CHAT_STARTERS` in `EagleDatingSimManager._get_all_scenarios_for_char()` and `_get_cg_catalog()` so the character has full parity with Hu Tao!
4. **Run Verification**:
   - Verify all `30` scenarios (`120` unique scenario CG files) + `15` milestone CG files exist on disk, have unique SHA-256 hashes, and work in both the Web UI (`http://127.0.0.1:8765`), `hud.lua`, and `eagle_vn_ingame_overlay.py`.
```

## === END COPY-PASTE MASTER PROMPT ===
