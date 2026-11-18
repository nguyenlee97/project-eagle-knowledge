# Citlali Story Quest #1 (5-Chapter Pure Branching Visual Novel) — Narrative & Causal Design Bible (`v1.1 — APPROVED Post-Reviewer AI Audit`)

- **Campaign ID:** `"citlali_sq1_color_of_eternity"`
- **Title:** `"Where the Night-Wind Keeps Your Hue"`
- **Subtitle:** `"Opalstar Chronicle: Act I -- The Color of Eternity"`
- **Heroine:** **Citlali — Granny Itztli of the Masters of the Night-Wind** (`char_id = "citlali"`, `ped_id = 49430`, `theme_rgb = [192, 132, 252]`)
- **Protagonist:** **Traveler Aether** — Fourth Descender & Bearer of the Natlan Ancient Name **`Tumaini` ("Hope")**
- **Target Runtime & Architecture:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_story_quest_citlali.py` + `ui_assets\story_quest_cgs\citlali\*.jpg` (**100% Zero-Core-Edit Plug-and-Play** on `eagle_story_quest.py`; exports both `STORY_QUEST_CAMPAIGN` and `STORY_QUEST_CAMPAIGNS = [STORY_QUEST_CAMPAIGN]` for Multi-Campaign forward compatibility)
- **Scale & Mathematical Proof Summary (`verify_citlali_5ch_dag.py` `v1.1` = `0` Errors, `33/33` Reviewer AI Findings Patched):**
  - **5 Chapters** across a continuous **12-Day New-Moon Countdown** (`Day 1 Morning` -> `Dawn of Day 12`)
  - **`44` Scene Nodes (`N01..N42`)** — `44/44` reachable, `0` orphan nodes, `0` zombie nodes, `0` deadlocks across all `6,355` rational paths (`8,372` full-open paths)
  - **`~565` Literary English Beats** (`95` Ch.1 + `105` Ch.2 + `95` Route A + `100` Route B + `95` Route C + `75` Ch.5 `= 565` total; `~370` beats/run; `100%` strict `CFont` ASCII `0x20..0x7E`; every `inner_thought <= 138` chars)
  - **`22` Preset Choices (`C01..C22`)** + **`2` Pre-Choice Resonance Triggers (`N17` Second-Chance Handkerchief & `N25` Ororon Harmonic Spindle Recovery)** — **Pairwise Ceteris-Paribus Non-Dominance Proven (`opt0_unique_END_TRUE > 0` and `opt1_unique_END_TRUE > 0` across all `13` binary trade-off choices, `0` isomorphic pairs, `0` Route C priority downgrades, `0%` Route A `INSIGHT` bypass)**
  - **`2` Core Integer Stats (`BOND` max `21` pre-final / `24` post-final; `INSIGHT` max `21`)** + **`11` Primary Causal Flags (`F01..F11`)** — `11/11` verified with pairwise-distinct negative `END_TRUE` ablation deltas in both rational and full-open models
  - **`2` Multi-Chapter Combination Gates:** `C15_B_GATE1` (*The Seven-Color Prism Key*, `exclusive_rescue_gate`) and `C18_C_GATE2` (*Resonance Bridge of Ukumbuko & Tumaini*)
  - **`5` Distinct Endings:** `END_TRUE` (`18.59%`), `END_GOOD` (`21.65%`), `END_NEUTRAL` (`28.39%`), `END_BAD_1` (`11.91%`), `END_BAD_2` (`19.47%`) — Markov sum `= 100.0000%`
  - **`42` Unique `16:9` (`1376x768`) CGs** (`42/42` explicitly mapped to nodes/post-choice payoff beats) rendered via Antigravity's internal `image-generator` with official HoYoverse character sheets

---

## 1. Canonical Foundation, Top *Aetlali* Fanfic Synthesis & Four Ironclad World Laws

### 1.1 Core Thematic Conflict: *Two Centuries of Fading Wildflowers vs. The Immortal Golden Witness*

Beneath her tribe-wide reputation as the fearsome **"Granny Itztli"** whose name alone silences crying toddlers (`Character Story: Details`), Citlali's emotional world rests on a two-hundred-year wound documented across HoYoverse canon (`staging/project-eagle/story-quest-citlali-impl-20261106/corpus/`):

1. **Why She Started Counting "200 Years" (`Character Story 3 & 4` & `Character Story 5`):** For decades, Citlali ignored her ageless lifespan—until the autumn evening her sole equal and rival-turned-friend **Huitzilin** returned with wrinkles framing her eyes and pointed at a field of Natlan wildflowers that would bloom again next year. Citlali whispered back: **"But the flowers we see now... Not one of them will feel the warmth of the sunlight that shines down on next year's field."** Huitzilin passed away before their next twenty-year anniversary; from that night on, Citlali counted every passing year (`200`), barred her doors, and scrubbed—yet never banned—the taunting wall graffiti painted by Huitzilin's shamanic lineage solely to pretend those sparring days had never ended (`Character Story 1`). Even after uncovering Huitzilin's final seven-color message inside the Seven-Hued Ruins (*"The color of memories, that's what"*, *Opal Firebird Act III* & `Character Story 5`) and entrusting her handkerchief to the golden-haired Traveler, one deeper dread still haunts her present-day heart: *in the end, nothing gold can stay—and if she lets herself be remembered too deeply, what happens when even that bond bleeds away?*
2. **The Secret Sealed Book & Huitzilin's Bookmark Slip (`Character Story 2`):** Hidden behind multi-layered shamanic wards in Citlali's bookshelf is an obscure modern Inazuman light novel from Yae Publishing House, **`New Chronicles of the Six Kitsune`**, into which Citlali tucked a **200-year-old woven seven-color dye-bookmark slip** left by Huitzilin—because the novel's opening line cut straight to her soul:
   > *"Stories relating to memory always seem to have to do with those moments where you gain something and lose it straight away."*
3. **The Unclaimed Ancient Name `Ukumbuko` ("Memory") (`Character Story: Vision`):** Despite serving as Natlan's only living Great Shaman, Citlali never inherited an Ancient Name because she withdrew from mortal attachment at age seventy, claiming her multi-decade chronicle scrolls were *"just a way to pass the time."* Over a century ago, an ancestor called out from the mist-shrouded Night-Wind, bestowing her Cryo Vision alongside a deferred covenant embedded in the **First-Era Obsidian Name-Core**:
   > *"All that I depict shall be gifts, given to the world of the deceased. This was once my name, and it will be yours as well. **Ukumbuko, 'Memory.'** Sooner or later, you will indeed inherit it. You just do not yet know the reason why."*
4. **Why Only Aether Breaks Her Two-Century Armor (*Opal Firebird Act III: "The Color of Memory"* & `5.7 "Savior"`):**
   - Both Citlali and Aether perceive the **"Color of Memory."** When Citlali first took Aether's hand to share her senses (`Archon Quest V.3`), his **golden memory-mark** bonded directly into her mind (*Paimon, notably, never hears this private mental channel—making their silent arguments right in front of an oblivious Paimon a signature comedic dynamic*).
   - Per *The Color of Memory*, **the *only* way to sever their bidirectional telepathy is for one of them to forget the other.**
   - Trusting his Descender lifespan, Citlali gave Aether **her rose-lavender handkerchief (`Item 121130`)** and **her front-door house key**, while growing pointedly jealous whenever hand-holding with anyone else is mentioned (`5.7 "Savior"`: *"Why holding hands? Why that, specifically? Why not... literally anything else?"*).

### 1.2 Four Ironclad World & Soul-Link Laws (Zero Plot Holes / Zero Deus Ex Machina)

1. **Law 0 — Spatial & Temporal Continuity (Verona Coastal Sanctuary <-> Night-Wind Conduit, 12-Day Countdown):**
   - Citlali's secluded **Verona Point Cliffside Sanctuary** (`[814.50, -1769.00, 13.40]`) houses an inner **Obsidian Astral Loom Chamber** linked via a post-war **Wayob Ley-Conduit** directly to the Masters of the Night-Wind Archive, the **Seven-Hued Ruins Sub-Stratum**, and the **Night Kingdom Loom Threshold**. Every transition across **Day 1 Morning to Day 12 Sunrise** observes explicit travel, sleep/camp recovery, and coastal weather continuity.
2. **Law 1 — The `5.7` Loom of Fate Aftershock & The Embedded *Ukumbuko* Name-Core:**
   - Following the **Loom of Fate activation** inside Natlan's Night Kingdom memory-space (`5.7 "A Space and Time for You"`—ironically foreshadowed by Mualani's Direidyth gossip in `N07`!), a delayed chromatic shear fractures the **First-Era *Ukumbuko* Chronicle Scroll**, which houses the dormant **Obsidian Name-Core** of Citlali's *Vision* ancestor and anchors three centuries of Night-Wind dead (including Huitzilin's seven-color thread). Without re-anchoring before the **Twelfth New-Moon Tide (Night 11 Midnight)**, Chromatic Unraveling will bleach the scroll into blank white static.
3. **Law 2 — Living Memory-Pigment Cost & Telepathic Static Decay:**
   - Night-Wind scrolls require **living emotional memory-pigment** (`Character Story 5`). Holding a torn ancestral seam consumes **High-Density Living Hue**—and after 200 years of seclusion, Citlali's brightest living colors consist almost entirely of Huitzilin's wildflower memory and **Aether's golden-rose presence**.
   - Each midnight Citlali secretly bleeds her own pigment into the scroll, the drain numbs her fingertips with frost, dulls pale **Quenepa Berry wine** to tasteless water, weakens her sanctuary's inner wards, and begins consuming her **memory-bond with Aether**—causing her leaked `inner_thought` in Aether's mind (which Paimon cannot hear) to fracture into **`[...white static...]`** while Paimon notices only that Granny stopped snapping at her outwardly.
4. **Law 3 — Why Mavuika, Xilonen, and Yohualtecuhtin Cannot Trivially Solve It (Hardware Parity & Cost of `END_GOOD`):**
   - **Mavuika's Sacred Flame** carries blazing martial phlogiston that incinerates delicate individual Night-Wind hues into ash unless stepped down through a regulator.
   - **Yohualtecuhtin (Lord of the Night)**—though sustained in lifeforce since Il Capitano's fusion at the end of `AQ V.5`—governs the structural **Ley-vessel** of the Night Kingdom and by cosmic rule can never fabricate **living mortal emotional pigment** on a weaver's behalf.
   - **Why `Ukumbuko` Awakens Consistently Across Routes A, B, and C:** The dormant **Obsidian Name-Core** already rests *inside* the First-Era Scroll (`N17`). On **Routes A and B**, Aether and Citlali reach that Name-Core directly from *within* the Soul-Bridge or Seven-Hued Sub-Stratum. On **Route C**, because the team remains outside in the waking sanctuary, **Xilonen** must either seal the scroll behind an external **60-Day Phlogiston Stasis Clamp (`END_GOOD`)**—saving Citlali safely at the real cost of leaving `Ukumbuko` dormant behind humming obsidian glass requiring renewal every sixty days and muting her telepathy to shoulder-touch range—or engrave an external **Resonance Bridge (`C18_C_NAME_CONDUIT_UNLOCK`)** connecting the inner Name-Core to Night 11's threshold.
   - **Why Only `Ukumbuko` + Fourth Descender `Tumaini` Achieves `END_TRUE`:** Teyvat natives' memories reside inside the Ley Lines and drain when poured into the scroll. Aether's Fourth Descender memory stands **outside Irminsul and the Ley Lines** while bearing **`Tumaini` ("Hope")** and **Citlali's rose-lavender handkerchief (`Item 121130`)**, acting as an inexhaustible golden-rose mirror when Citlali ceases merely archiving the dead and claims **`Ukumbuko` ("Memory")** as a living vow.

---

## 2. State Variables (`BOND`, `INSIGHT`) & `11`-Flag Causal Matrix (`v1.1`)

### 2.1 Quantitative Axes & Game-Theoretic Non-Dominance

| Axis | Initial | Exact Max (`Pre-Final` / `Post-Final`) | Mechanical Role & `v1.1` Non-Vacuous Proof |
|---|---|---|---|
| **`BOND`** | `0` | **`21` / `24`** | Measures Citlali's emotional trust & willingness to let Aether bear her living hue. Tested at `N17` Second-Chance Handkerchief (`bond >= 7` with `insight >= 8`: **`56` Ch.1–2 prefixes / `500` rescued `END_TRUE` paths**), **Route C Gate #2 (`min_bond: 10`: `359` pass / `82` routed safely to `END_GOOD`, `0` downgraded to `END_NEUTRAL`!)**, and **Final Gate `C22_FINAL` (`min_bond: 14`: Route A `300` pass / `58` blocked; Route B `224` pass / `628` blocked)**. Ablating `BOND` shifts `END_TRUE` by **`+950` paths**. |
| **`INSIGHT`** | `0` | **`21` / `21`** | Measures shamanic comprehension of Seven-Color Weaving, Loom-of-Fate static, and Descender resonance. Tested at `N17` (`insight >= 8`), Route A `C11_A2` (`min_insight: 6`) & **`C12_A1` (`min_insight: 8`: `0%` Route A `END_TRUE` bypass!)**, Route B `N25` Harmonic Spindle Recovery (`insight >= 11`, `108` paths) & **Gate #1 `C15_B_GATE1` (`min_insight: 10`)**, and **Route C Gate #2 (`min_insight: 7`)**. Ablating `INSIGHT` shifts `END_TRUE` by **`+856` paths**. |

### 2.2 Master `11`-Flag Causal Matrix (`11/11` Pairwise-Distinct Negative Ablations)

| Flag ID | Planted At | Narrative Meaning | Tested At (Hard Gates + Literary `when` Callbacks) | `END_TRUE` Ablation (`Rational` / `Full-Open`) |
|---|---|---|---|---|
| **`F01_SEAL_FROST_READ`** | `C01_A` (`N02`) | Spots colorless frost bleeding through Citlali's doorway ward before unlocking. | **Route A** `C12_A1` (`requires_any`), **Route B** `N25` (`3-of-5` harmonic pool), **Gate #2** *Physical Bleed Proof*; `N17` inner-ward crackle payoff. | **`-72` / `-72`** |
| **`F02_NOVEL_SECRET_KEPT`** | `C02_A` (`N04`) | Shields Citlali's warded bookshelf latch when Ororon's cabbages nearly expose `Six Kitsune`. | **Gate #2** *Intimate Heart Truths* (`2-of-4` pool); `N05–N06` voluntary book-sharing variant & `N40` callback. | **`-186` / `-186`** |
| **`F03_SIX_KITSUNE_VERSE`** | `C03_A` (`N06`) | Reads `Six Kitsune`'s opening sentence + Huitzilin's 200-year-old woven seven-color bookmark slip. | **Route A** `C12_A1` (`requires_all`), **Route B** `N25` + **Gate #1** (`requires_any`), **Gate #2** *Intimate Heart Truths* (`2-of-4`); gates `N40` explicit `Six Kitsune` rebuttal! | **`-556` / `-556`** |
| **`F04_HAND_PROMISE_GIVEN`** | `C04_A` (`N08`) | Under the dusk snack table, offers open palm to soothe Citlali's `5.7` hand-holding jealousy. | **Route A** `C12_A1` (`requires_any`), **Gate #2** *Intimate Heart Truths* (`2-of-4`); `N20_A3`, `N36`, & `N41` callbacks. | **`-200` / `-200`** |
| **`F05_APHID_LOOM_TRACE`** | `C05_A` (`N10`) | Inspects Ororon's chalk-white phlogiston aphids behind the garden wall, isolating Night-Kingdom static. | **Route B** `N25` (`3-of-5`) + **Gate #1** (`requires_any`), **Gate #2** *Physical Bleed Proof*; `N22_B1` & `N28_C3` callbacks. | **`-60` / `-60`** |
| **`F06_GRAFFITI_TRUTH_HEARD`** | `C06_A` (`N12`) | Spares Huitzilin's faded 20-year corner mark while washing wall graffiti, earning Citlali's confession. | **Gate #2** *Intimate Heart Truths* (`2-of-4` pool); `N19_A2` & `N35` Huitzilin memory-echo callbacks. | **`-190` / `-190`** |
| **`F07_ROSE_HANDKERCHIEF`** | `C07_A` (`N14`) *or* `N17` (`bond>=7 & insight>=8`) | Citlali's rose-lavender handkerchief (`Item 121130`) knotted with Aether's golden thread. | **Gate #1** (`requires_all`), **Gate #2** (`requires_all`), **Final Gate `C22_FINAL`** (`requires_all`). | **`-1,242` / `-1,242`** |
| **`F08_QUENEPA_CONFESSION`** | `C08_A` (`N16`) | Catches Citlali's frost-numbed wrist over shattered stoneware Quenepa cup, tracing meridian frost. | **Route A** `C12_A1` (`requires_any`), **Route B** `N25` + **Gate #1** (`requires_any`), **Gate #2** *Physical Bleed Proof*. | **`-86` / `-86`** |
| **`F09_ETERNAL_HUE_VOW`** | `C11_A1` (`N20_A3`) | Binds Descender gold openly to her rose-lavender thread across the Soul-Bridge. | **Route A** `C12_A1` (`requires_all`); `N35` & `N40` callbacks. | **`-300` / `-300`** |
| **`F10_OPAL_SPINDLE_THREAD`** | `C13_B1` (`N23_B2`) *or* `N25` Harmonic Recovery | Huitzilin's unbleached First-Era Opal Spindle (or Ororon's `insight>=11` + `3`-clue harmonic lattice). | **Gate #1 `C15_B_GATE1`** (`requires_all: ["F07_ROSE_HANDKERCHIEF", "F10_OPAL_SPINDLE_THREAD"]`). | **`-224` / `-224`** |
| **`F11_CLAW_IKTOMI_FEATHER`** | `C02_B` (`N04`) | Collects Elder Tlapo's ("Claw") shed pale-iridescent memory-feather on the sanctuary terrace. | **Gate #2** *Physical Bleed Proof* (`requires_any`); `N18_A1` & `N27_C2` callbacks. | **`-10` / `-10`** |

**Secondary Expressive & Non-Dominance Markers (All Planted & Referenced in `flag_catalog`):**
- `SPECTRUM_GLITCH_SEEN` (`C04_B`: feeds Gate #1 `requires_any`), `PIGMENT_DRAIN_TIMED` (`C06_B`: feeds `N25` `3-of-5` harmonic pool), `CLOAK_STARLIGHT_WARMTH` (`C07_B`: `+3 BOND` rooftop embrace callback), `WILDFLOWER_STAR_ANCHOR` (`C10_A1`: feeds `C12_A1` `requires_any`), `PROJECTION_STEADIED` (`C13_B2`) + `ORORON_HARMONIC_TUNED` (`C14_B1`) -> `F10_HARMONIC_RECOVERED` (`N25`), `XILONEN_CHISEL_TUNED` (`C16_C1`: feeds Gate #2 *Physical Bleed Proof*), `COLD_FIREWALL_NO_VOW` (`C11_A2`) & `RAW_VIGIL_STRAIN` (`C12_A2`: both damp `N35–N37` link and forbid `END_TRUE` at `C22_FINAL`), `BAD1_KEY_RETURNED` / `BAD1_SILENT_THOUGHT` (`C19_BAD1`), `BAD2_KITSUNE_READ` / `BAD2_HANDS_JOINED` (`C20_BAD2`), `CH5_VOICE_LINK_CALL` / `CH5_TUMAINI_PULSE_ANCHOR` (`C21_CH5`).

---

## 3. Complete 5-Chapter, `44`-Node, `22`-Choice & `42`-CG Blueprint (`565` Beats)

### Chapter 1 — *"The Key, the Novel, and the Leaking Thought"* (`N01..N08`, Days 1–3, `95` Beats)

- **`N01` (Day 1, Morning — Verona Sanctuary Steps):** Aether climbs the coastal stone steps holding the **front-door house key** (`Item 121130`) Citlali entrusted to him. Loud challenger graffiti covers her outer wall, yet chill mist clings around the obsidian doorframe.
  - *CG:* `ch1_01_doorstep_graffiti_base.jpg`
- **`N02` (Day 1, Morning — The Threshold Ward, `C01`):** Citlali's drowsy mental grumbling leaks into Aether's mind before he even knocks.
  - *CG:* `ch1_02_key_frost_ward_diff.jpg` (Diff of `ch1_01`: close-up white rime along the obsidian ward as Aether raises her key)
  - **`C01`:** `C01_A_INSPECT_WARD` (`+0B, +2I`, `F01_SEAL_FROST_READ`) vs. `C01_B_USE_KEY_WARMLY` (`+2B, +0I`).
- **`N03` (Day 1, Late Morning — Nest of the Great Shaman):** Wrapped in her shawl clutching **Itzpapa** and **Citlalin** (`greet_doorstep`), Citlali scolds Aether aloud while her leaked `inner_thought` panics over tangled hair and her racing heartbeat.
  - *CG:* `ch1_03_sanctuary_wake_base.jpg` -> `ch1_04_sanctuary_blush_itzpapa_diff.jpg`
- **`N04` (Day 1, Noon — Ororon's Cabbage Ambush & Claw's Perch, `C02`):** **Ororon** enters with a sack of cabbages calling Aether *"Gramps"* and bumps an empty **Quenepa Berry wine** bottle toward Citlali's warded bookshelf latch, just as **Elder Tlapo ("Claw")** alights on the sea-terrace shedding a pale-iridescent feather (`vn_playful_tease`).
  - *CG:* `ch1_05_ororon_cabbage_chaos.jpg`
  - **`C02`:** `C02_A_SHIELD_BOOKSHELF` (`+2B, +0I`, `F02_NOVEL_SECRET_KEPT`) vs. `C02_B_CHECK_CLAW_FEATHER` (`+0B, +2I`, `F11_CLAW_IKTOMI_FEATHER`).
- **`N05` (Day 2, Afternoon — Spotless Shelves of Yae Publishing House):** Re-stacking shelves; Aether's gifted first editions sit spotless and uncracked (`vn_shy_blush`). Conditional transition (`when: F02` -> Citlali shyly unlocks her inner shelf compartment herself because Aether protected her dignity yesterday; `when: !F02` -> the unlatched compartment from Ororon's bump rests ajar beside the cushion).
  - *CG:* `ch1_06_bookshelf_novels_base.jpg`
- **`N06` (Day 2, Late Afternoon — Huitzilin's Bookmark in `Six Kitsune`, `C03`):** Inside modern **`New Chronicles of the Six Kitsune`** rests **Huitzilin's 200-year-old woven seven-color dye-bookmark slip**, marking the opening line about *"moments where you gain something and lose it straight away."*
  - *CG:* `ch1_07_six_kitsune_cipher_diff.jpg` (Diff of `ch1_06`: Citlali clutching `Six Kitsune` to her chest as sunlight catches the ancient woven bookmark slip)
  - **`C03`:** `C03_A_READ_KITSUNE_CIPHER` (`+0B, +2I`, `F03_SIX_KITSUNE_VERSE`) vs. `C03_B_TEASE_ITZPAPA_CUSHION` (`+2B, +0I`).
- **`N07` (Day 3, Dusk — Promenade Lanterns with Mualani, Kachina & Paimon):** Coastal grainfruit snacks (`outing_arrive_photo`, `outing_cruise`). **Mualani** chatters about northern Natlan rumors from the recent Loom-of-Fate incident (`5.7 Savior`)—how *"Tumaini had to hold some shy girl's hand all afternoon to see invisible monsters!"*
  - *CG:* `ch1_08_promenade_friends_base.jpg`
- **`N08` (Day 3, Dusk — "Why Holding Hands, Specifically?", `C04`):** Oblivious **Paimon** munches skewers while Citlali scoffs aloud about *"basic shamanic arts"* and blasts a jealous telepathic storm straight into Aether's head (*`"Holding hands?! Why holding hands specifically?! Couldn't they tie a spirit-cord to a sleeve--what kind of shameless excuse--"`*), edged by a sudden white-static flicker (`vn_playful_tease` -> `vn_shy_blush`).
  - *Pre-choice CG:* Keeps `ch1_08_promenade_friends_base.jpg` (no premature hand reach!).
  - **`C04`:**
    - `C04_A_OFFER_OPEN_PALM` (`+2B, +0I`, `F04_HAND_PROMISE_GIVEN`) -> **Post-choice `reaction_beats` CG:** `ch1_09_promenade_palm_diff.jpg` (Diff of `ch1_08`: Aether's open palm offered subtly under the lantern-lit table as Citlali blushes scarlet).
    - `C04_B_OBSERVE_SPECTRUM_GLITCH` (`+0B, +2I`, `SPECTRUM_GLITCH_SEEN`) -> Keeps `ch1_08_promenade_friends_base.jpg`.

---

### Chapter 2 — *"Two Centuries of Wildflowers and Static"* (`N09..N17`, Days 4–6, `105` Beats)

- **`N09` (Day 4, Misty Morning — Pale Aphids Outside the Garden Wall):** Citlali is still inside; **Ororon** and **Elder Tlapo** show Aether a jar of phlogiston aphids that turned chalk-white overnight near Granny's loom wall (*zero Citlali voice clips here*).
  - *CG:* `ch2_01_ororon_aphid_garden.jpg`
- **`N10` (Day 4, Morning — Silvered Phlogiston Residue, `C05`):**
  - *CG:* Inherits `ch2_01_ororon_aphid_garden.jpg`.
  - **`C05`:** `C05_A_TRACE_PALE_APHIDS` (`+0B, +2I`, `F05_APHID_LOOM_TRACE`) vs. `C05_B_HUMOR_GRAMPS_ORORON` (`+2B, +0I`).
- **`N11` (Day 4, Afternoon — Scrubbing Two Hundred Years of Graffiti):** Aether helps Citlali wash apprentice graffiti off her outer wall (`outing_cruise`), spotting Huitzilin's weathered twenty-year seven-petal corner mark.
  - *CG:* `ch2_02_graffiti_wall_base.jpg`
- **`N12` (Day 4, Sunset — Beyond Huitzilin's Answer, `C06`):** Citlali reflects softly (`vn_sweet_happy`): she already found Huitzilin's answer (*"the color of memories"*) in the Seven-Hued Ruins, yet watching mortal generations vanish still makes her terrified of what happens when *nothing gold can stay* and her own living hue burdens Aether.
  - *CG:* `ch2_03_graffiti_sunset_diff.jpg` (Diff of `ch2_02`: golden sunset; Citlali's fingertips pausing wistfully above Huitzilin's corner mark)
  - **`C06`:** `C06_A_SPARE_HUITZILIN_MARK` (`+2B, +0I`, `F06_GRAFFITI_TRUTH_HEARD`) vs. `C06_B_ANALYZE_PIGMENT_DRAIN` (`+0B, +2I`, `PIGMENT_DRAIN_TIMED`).
- **`N13` (Day 5, Starlit Night — Meteors Over Verona Roof):** Stargazing on the sanctuary roof with **Itzpapa** and **Citlalin** (`vn_sweet_happy`).
  - *CG:* `ch2_04_rooftop_stars_base.jpg`
- **`N14` (Day 5, Starlit Night — The Rose-Lavender Handkerchief, `C07`):** Citlali teases that outlanders lose keepsakes in a week while her leaked thought trembles over whether her rose-lavender handkerchief (`Item 121130`) still carries her color (`vn_shy_blush`).
  - *Pre-choice CG:* Keeps `ch2_04_rooftop_stars_base.jpg`.
  - **`C07`:**
    - `C07_A_KNOT_ROSE_HANDKERCHIEF` (`+1B, +1I`, `F07_ROSE_HANDKERCHIEF`) -> **Post-choice `reaction_beats` CG:** `ch2_05_rooftop_handkerchief_diff.jpg` (Diff of `ch2_04`: Aether holding out the rose-lavender handkerchief threaded with warm Descender gold).
    - `C07_B_WRAP_CLOAK_STARLIGHT` (`+3B, +0I`, `CLOAK_STARLIGHT_WARMTH`) -> Keeps `ch2_04_rooftop_stars_base.jpg`.
- **`N15` (Day 6, Late Night — Opaque Stoneware & Tasteless Quenepa):** Rain patters outside. Pouring from a dark stoneware flask into **opaque painted Night-Wind ceramic goblets**, Citlali doesn't realize she grabbed clear water instead of pale-golden **Quenepa Berry wine**, nor can her frost-numbed tongue taste it. **Paimon** eats the last honeyed grainfruit cake—and remarks in confusion that Granny didn't even glare or snap at her.
  - *CG:* `ch2_06_quenepa_lamp_base.jpg`
- **`N16` (Day 6, Midnight — Static in the Soul-Link, `C08`):** Citlali's opaque goblet slips from frost-rimmed fingers and shatters, exposing clear cold water across her hem while her telepathic stream in Aether's head tears into jagged white static: *`[...cold... don't let him touch my wrist... if the loom drinks his gold mark next, please don't let me forget the sound of his-- ...]`* (`outing_bump_rescue`).
  - *CG:* `ch2_07_quenepa_shatter_diff.jpg` (Diff of `ch2_06`: shattered painted stoneware on the mat, white frost on Citlali's knuckles as Aether reaches across)
  - **`C08`:** `C08_A_CATCH_FROSTED_WRIST` (`+0B, +2I`, `F08_QUENEPA_CONFESSION`) vs. `C08_B_HOLD_THROUGH_STATIC` (`+2B, +0I`).
- **`N17` (Day 6, Past Midnight — The Fractured Ward & Embedded *Ukumbuko* Name-Core, `C09`):** Citlali's pigment-drain causes her inner Astral Loom containment ward to crackle and fail (`when: F01` callback); pressing her house key's shamanic ownership-imprint together with `Tumaini`'s phlogiston unlatches the weakened inner seal. Inside hangs the **First-Era *Ukumbuko* Chronicle Scroll**, housing the dormant **Obsidian Name-Core** of her *Vision* ancestor while ribbons of Citlali's rose-lavender memory-pigment bleed into the Loom-of-Fate scar (`5` nights left until the New-Moon Tide).
  - *Pre-Event (`N17_SECOND_CHANCE_HANDKERCHIEF`):* If `!F07_ROSE_HANDKERCHIEF` and `bond >= 7` and `insight >= 8` (`56` prefixes / `500` `END_TRUE` paths), her handkerchief pulses hot against Aether's chest in resonance with the Name-Core (`adds F07_ROSE_HANDKERCHIEF, F07_SECOND_CHANCE_N17`).
  - *CG:* `ch2_08_astralloom_reveal.jpg`
  - **`C09`:** `C09_ROUTE_A_SOUL_BRIDGE` (`ROUTE_A`, `+1B`) / `C09_ROUTE_B_SEVEN_HUED_MAZE` (`ROUTE_B`, `+1I`) / `C09_ROUTE_C_TRIBAL_COUNCIL` (`ROUTE_C`, `+1B`).

---

### Chapters 3A & 4A — *Route A: "The Tandem Soul-Bridge"* (`N18_A1..N21_A4`, `N30_BAD1_1..N31_BAD1_2`, Days 7–10, `95` Beats)

*(Explicit daytime rest & broth recovery transitions open each night's dive across Days 7–10.)*
- **`N18_A1` (Night 7 — Entering Citlali's Palette):** Guarded by **Elder Tlapo** and **Itzpapa/Citlalin**, Aether clasps Citlali's hand during the midnight Ley-tide, stepping into her 200-year memory-space.
  - *CG:* `ch3a_01_soulbridge_handclasp.jpg`
- **`N19_A2` (Night 8 — Wildflower Meadow After Daytime Rest, `C10_A`):** After resting through Day 8's noon rain, Night 8's dive enters young Citlali's moonlit draw with **Huitzilin** (`when: F06` callback).
  - *CG:* `ch3a_02_huitzilin_wildflowers.jpg`
  - **`C10_A`:** `C10_A1_READ_WILDFLOWER_ECHO` (`+0B, +2I`, `WILDFLOWER_STAR_ANCHOR` — `32` unique `END_TRUE` wins) vs. `C10_A2_SHELTER_YOUNG_CITLALI` (`+2B, +0I` — `28` unique `END_TRUE` wins).
- **`N20_A3` (Night 9 — The White Surge Crossroads, `C11_A`):** White static surges toward the golden-rose knot of Aether's memories (`outing_bump_rescue` -> `vn_tender_love`).
  - *CG:* `ch4a_01_whitesurge_crossroads_base.jpg`
  - **`C11_A`:**
    - `C11_A1_ETERNAL_HUE_VOW` (`+2B, +1I`, `F09_ETERNAL_HUE_VOW` -> `N21_A4`).
    - `C11_A2_DESCENDER_FIREWALL` *(Requires `min_insight: 6`; explicitly badged `[Quarantine Protocol -- Severs Emotional Link]`)*: Clinical Descender Ley-firewall halts the bleed while shutting her out of your heart (`+0B, +2I`, `COLD_FIREWALL_NO_VOW` -> `N21_A4`; blocks `END_TRUE`).
    - `C11_A3_YIELD_TO_HER_PRIDE` (`-1B` -> `N30_BAD1_1`).
- **`N21_A4` (Night 10 — Counter-Weaving Before the New Moon, `C12_A`):**
  - *CG:* `ch4a_02_counterweave_diff.jpg` (Diff of `ch4a_01`: golden-rose threads stabilizing around their clasped palms)
  - **`C12_A` (`priority_unlock: True`):**
    - `C12_A1_UKUMBUKO_COUNTERWEAVE` *(Requires `F09 + F03` + `any(F01, F04, F08, WILDFLOWER_STAR_ANCHOR)` + `min_insight: 8`)*: Invert Huitzilin's woven bookmark cipher (`+3B, +1I`, `UKUMBUKO_WEAVE_PRIMED` -> `N34_CH5_CONVERGE`).
    - `C12_A2_RAW_GOLD_VIGIL` *(Fallback)*: Brute-forcing raw Ley-static all night drains their shared link (`-3B, +1I`, `RAW_VIGIL_STRAIN` -> `N34_CH5_CONVERGE`; prevents zero-investigation builds from coasting into `END_TRUE`).
- **Route A Tragic Branch (`N30_BAD1_1` -> `N31_BAD1_2` -> `C19_BAD1` -> `END_BAD_1`):**
  - **`N30_BAD1_1` (Night 10–11 — Seven Barriers on the Study Door):** Thrown back into Citlali's bookshelf room as seven violet-white shamanic barriers lock the loom door from within, Aether hears her last fading thought before silence falls.
    - *CG:* `end_bad1_01_sealed_door_diff.jpg` (Diff of `ch1_06_bookshelf_novels_base.jpg`: empty study bathed in pale moonlight with seven glowing shamanic seals barring the inner doorway)
  - **`N31_BAD1_2` (Day 12 Afternoon — Stranger on Verona Shore, `C19_BAD1`):** Buying pale Quenepa wine on Verona Beach, a healthy Citlali looks straight through Aether as a polite stranger while her telepathic channel is dead silent. Each option of `C19_BAD1` (`C19_A_RETURN_HOUSE_KEY` vs. `C19_B_SEND_SILENT_THOUGHT`) plays **`4` dedicated closing `reaction_beats`** before **`END_BAD_1`: *"White Canvas on Verona Shore"***.
    - *CG:* `end_bad1_02_stranger_shore.jpg`

---

### Chapters 3B & 4B — *Route B: "The Seven-Hued Abyss"* (`N22_B1..N25_B5_GATE1`, `N32_BAD2_1..N32B_BAD2_2`, Days 7–10, `100` Beats)

*(Includes glowing subterranean mushroom-ledge camp & ration transitions with Ororon and Chasca across Days 7–10.)*
- **`N22_B1` (Day 7 — Gorge Dive with Ororon & Chasca):** Riding **Chasca's** gun-frame into the Seven-Hued gorge while Citlali's furious, worried astral scolding crackles in Aether's ear (`vn_playful_tease` / `outing_bump_rescue`—no sightseeing audio).
  - *CG:* `ch3b_01_chasca_ororon_canyon.jpg`
- **`N23_B2` (Day 8 — Huitzilin's False Mural & Intangible Projection, `C13_B`):** Chasca guards the upper rift; Aether and **Ororon** spot the unbleached **First-Era Opal Spindle** beside Citlali's flickering astral projection (prose notes clearly her projection is intangible, though losing focus will yank her waking body toward the conduit).
  - *CG:* `ch3b_02_seven_hued_mural.jpg`
  - **`C13_B`:** `C13_B1_CLAIM_OPAL_SPINDLE` (`+0B, +2I`, `F10_OPAL_SPINDLE_THREAD` — `174` unique `END_TRUE` wins) vs. `C13_B2_STEADY_PROJECTION_LINK` (`+2B, +0I`, `PROJECTION_STEADIED` — `50` unique `END_TRUE` wins).
- **`N24A_B3` -> `N24B_B4` (Day 9 — Citlali Crosses the Wayob Conduit in the Flesh, `C14_B`):** Breaking past Paimon's delay via the sanctuary's **Law 0 Wayob Ley-Conduit** (with Paimon hurrying after Ororon's trail above), **Citlali physically stumbles into the monochrome lower vault** to drag Aether out, collapsing into his arms as her telepathy stutters.
  - *CG (`N24A_B3` & inherited by `N24B_B4`):* `ch4b_01_monochrome_vault_base.jpg`
  - **`C14_B`:** `C14_B1_TUNE_ORORON_HARMONIC` (`+0B, +2I`, `ORORON_HARMONIC_TUNED` — `86` unique `END_TRUE` wins) vs. `C14_B2_WHISPER_ACROSS_STATIC` (`+2B, +0I` — `138` unique `END_TRUE` wins).
- **`N25_B5_GATE1` (Day 10 Midnight — COMBINATION GATE #1: *"The Seven-Color Prism Key"*, `C15_B_GATE1`):**
  - *Pre-Event (`N25_ORORON_SECONDARY_SPINDLE`):* If `!F10_OPAL_SPINDLE_THREAD`, `PROJECTION_STEADIED + ORORON_HARMONIC_TUNED`, `3-of-5` of `{F01, F03, F05, F08, PIGMENT_DRAIN_TIMED}`, and `insight >= 11` (`108` paths), Ororon's tuning fork reconstructs the spindle's harmonic lattice (`adds F10_OPAL_SPINDLE_THREAD, F10_HARMONIC_RECOVERED`).
  - *Pre-choice CG:* Keeps `ch4b_01_monochrome_vault_base.jpg`.
  - **`C15_B_GATE1` (`exclusive_rescue_gate: True`):**
    - **`C15_B_PRISM_KEY_UNLOCK`:** Requires `F07 + F10` + `any(F03, F05, F08, SPECTRUM_GLITCH_SEEN)` + `min_insight: 10` (`+2B, +1I`, `COMBO1_CLEARED` -> `N34_CH5_CONVERGE`) -> **Post-choice `reaction_beats` CG:** `ch4b_02_prism_gate_diff.jpg` (Diff of `ch4b_01`: Opal Spindle wrapped in rose-lavender silk splitting Descender gold into seven tribal hues).
    - **`C15_B_BLIND_DIVE_WHITEOUT`:** Fallback (`-> N32_BAD2_1`).
- **Route B Tragic Branch (`N32_BAD2_1` -> `N32B_BAD2_2` -> `C20_BAD2` -> `END_BAD_2`):**
  - **`N32_BAD2_1`:** Both physical bodies are sealed side-by-side inside the vault's quarantine sphere (`inherits ch4b_01_monochrome_vault_base.jpg`), waking inside a timeless painted twilight diorama of Citlali's study.
  - **`N32B_BAD2_2` (`C20_BAD2`):** Outside in the vault, Ororon and Paimon lay fresh wildflowers beside two hand-clasped sleepers; inside, Citlali weeps (`outing_bump_rescue` on breakdown -> `vn_tender_love` only on quiet post-choice resignation). Each option of `C20_BAD2` (`C20_A_OPEN_SIX_KITSUNE_TOGETHER` vs. `C20_B_INTERLACE_PAINTED_HANDS`) plays **`4` bespoke closing `reaction_beats`** before **`END_BAD_2`: *"Prisoners of the Seventh Hue"***.
    - *CG:* `end_bad2_painted_twilight.jpg`

---

### Chapters 3C & 4C — *Route C: "The Council of Six Flames"* (`N26_C1..N29_C4_GATE2`, `N33_GOOD_1`, Days 7–10, `95` Beats)

- **`N26_C1` (Day 7 — Mavuika, Xilonen & Friends Raid the Hermitage):** **Mavuika, Xilonen, Mualani, Kachina, and Ororon** arrive (`vn_playful_tease`).
  - *CG:* `ch3c_01_mavuika_xilonen_council.jpg`
- **`N27_C2` (Day 8 — Xilonen's Obsidian Chisel & Blanket Granny, `C16_C`):** Xilonen explains that because the **Obsidian Name-Core** sits sealed inside the scroll, staying outside requires either clamping it shut (`60-day stasis`) or engraving an external **Resonance Bridge** (`vn_shy_blush`).
  - *CG:* `ch3c_02_xilonen_forge_terrace.jpg`
  - **`C16_C`:** `C16_C1_CALIBRATE_XILONEN_CHISEL` (`+0B, +2I`, `XILONEN_CHISEL_TUNED` — `58` unique `END_TRUE` wins) vs. `C16_C2_COMFORT_SHY_GRANNY` (`+2B, +0I` — `92` unique `END_TRUE` wins).
- **`N28_C3` (Day 9 — Stepping Down the Sacred Flame, `C17_C`):**
  - *CG:* `ch4c_01_sacred_flame_regulator_base.jpg`
  - **`C17_C`:** `C17_C1_MAP_SACRED_FLAME_RATIO` (`+1B, +2I` — `46` unique `END_TRUE` wins) vs. `C17_C2_PROMISE_NO_SOLITUDE` (`+2B, +0I` — `92` unique `END_TRUE` wins).
- **`N29_C4_GATE2` (Day 10 Evening — COMBINATION GATE #2: *"Resonance Bridge of Ukumbuko & Tumaini"*, `C18_C_GATE2`):**
  - *Pre-choice CG:* Keeps `ch4c_01_sacred_flame_regulator_base.jpg`.
  - **`C18_C_GATE2` (`priority_unlock: True`):**
    - **`C18_C_NAME_CONDUIT_UNLOCK`:**
      - `requires_all`: `["F07_ROSE_HANDKERCHIEF"]` *(1. Living color-token)*
      - `requires_any`: `["F01_SEAL_FROST_READ", "F05_APHID_LOOM_TRACE", "F08_QUENEPA_CONFESSION", "F11_CLAW_IKTOMI_FEATHER", "XILONEN_CHISEL_TUNED"]` *(2. Physical bleed/groove proof)*
      - `requires_at_least`: `2` of `["F02_NOVEL_SECRET_KEPT", "F03_SIX_KITSUNE_VERSE", "F04_HAND_PROMISE_GIVEN", "F06_GRAFFITI_TRUTH_HEARD"]` *(3. Intimate heart truths)*
      - `min_insight: 7`, **`min_bond: 10`** *(Guarantees `100%` of Conduit-unlocked rational paths reach `BOND >= 14` -> `0` paths downgraded from `END_GOOD` to `END_NEUTRAL`!)*
      - **Post-choice `reaction_beats` CG:** `ch4c_02_name_conduit_diff.jpg` (Diff of `ch4c_01`: Xilonen's Resonance Bridge glowing rose-lavender and gold beside Mavuika).
    - **`C18_C_SIXTY_DAY_STASIS_CLAMP`:** Always unlocked (`+2B` -> `N33_GOOD_1`).
- **`N33_GOOD_1` -> `END_GOOD` (*"Sixty-Day Candlelight"*):** Rooftop feast (`outing_arrive_photo`) with concrete 60-day obsidian stasis cost.
  - *CG:* `end_good_rooftop_candlelight.jpg`

---

### Chapter 5 — *"The Color That Outlasts the Stars"* (`N34_CH5_CONVERGE..N42`, Night 11 – Dawn of Day 12, `75` Beats)

- **`N34_CH5_CONVERGE` (Night 11, Midnight — The Iridescent Threshold):** Route-gated perimeter (`ROUTE_A` Elder Tlapo; `ROUTE_B` Ororon & Chasca; `ROUTE_C` Mavuika & Xilonen) before **Yohualtecuhtin's** structural Night-Kingdom mist.
  - *CG:* `ch5_01_nightkingdom_threshold.jpg`
- **`N35` (Night 11, Midnight — Living Inheritance of `Ukumbuko`, "Memory"):** Stepping beyond passive archival of the dead (`Character Story 5`), Citlali accepts living remembrance beside `Tumaini`, awakening the embedded **Obsidian Name-Core** of **`Ukumbuko` ("Memory")** (`when: COLD_FIREWALL_NO_VOW` / `RAW_VIGIL_STRAIN` / `bond < 14` plays a muted glass-pane variant foreshadowing `END_NEUTRAL`).
  - *CG:* `ch5_02_ukumbuko_awakening_base.jpg`
- **`N36_LOOM_CRESCENDO` (Night 11, Climax — Gold & Rose-Lavender Mirror, `C21_CH5`):** (`outing_bump_rescue`)
  - *CG:* `ch5_03_loom_crescendo_diff.jpg`
  - **`C21_CH5` (Symmetric `+2 BOND` Expressive Choice, `0` Dominance Loss):** `C21_A_CALL_HER_ACROSS_LINK` (`+2B`, `CH5_VOICE_LINK_CALL`) vs. `C21_B_ANCHOR_TUMAINI_PULSE` (`+2B`, `CH5_TUMAINI_PULSE_ANCHOR`).
- **`N37_SANCTUARY_MORNING` (Day 12, Pre-Dawn — Sweet Quenepa & Clear/Muted Link):** (`greet_doorstep` / `vn_sweet_happy`; muted glass-pane telepathy variant when `COLD_FIREWALL_NO_VOW`, `RAW_VIGIL_STRAIN`, or `bond < 14`).
  - *CG:* `ch5_04_morning_tea_sanctuary.jpg`
- **`N38` (Day 12, Sunrise — Route-Gated Cove Send-Off):** Strictly gated by route (`ROUTE_A`: Ororon, Paimon & Elder Tlapo only; `ROUTE_B`: Ororon, Chasca, Paimon & Elder Tlapo; `ROUTE_C`: full Council of Six Flames with Mavuika, Xilonen, Mualani & Kachina).
  - *CG:* `ch5_05_verona_cliff_sunrise_base.jpg`
- **`N39_VERONA_DAWN_CLIFF` (Day 12, Sunrise — Final Causal Gate Above the Western Surf, `C22_FINAL`):**
  - *CG:* `ch5_06_verona_cliff_turn_diff.jpg`
  - **`C22_FINAL` (`priority_unlock: True`):**
    - `C22_TRUE_ETERNAL_VOW` *(Requires `F07_ROSE_HANDKERCHIEF`, forbids `["COLD_FIREWALL_NO_VOW", "RAW_VIGIL_STRAIN"]`, `min_bond: 14`)* -> `N40` -> `N41` -> **`END_TRUE`**.
    - `C22_NEUTRAL_UNCRACKED_SPINE` -> `N42` -> **`END_NEUTRAL`**.
- **True Ending (`N40` -> `N41` -> `END_TRUE`: *"Where the Night-Wind Keeps Your Hue"*):**
  - **`N40`:** Rose-lavender silk binds their wrists (`when: F03_SIX_KITSUNE_VERSE` overturns the `Six Kitsune` opening sentence; `when: !F03` echoes Huitzilin's wildflower sun & her handkerchief color). *CG:* `end_true_01_wrist_ribbon_tears.jpg`.
  - **`N41` (`ending_id = "END_TRUE"`):** Speaks her **exact official Ascension 6 Eternal Vow** matching *CV: Asami Tano*'s `citlali/vn_tender_love_01.wav` (`3.32s`):
    > `"From this point on, I will always be by your side -- until the stars diminish, the flames die out, and the smoke dissipates into nothing."`
    *CG:* `end_true_02_eternal_sunrise_vow.jpg`.
- **Neutral Ending (`N42` -> `END_NEUTRAL`: *"The Uncracked Spine"*):** *CG:* `end_neutral_uncracked_spine.jpg`.

---

## 4. `v1.1` Verified Mathematical Audit (`verify_citlali_5ch_dag.py` -> Exit Code `0`)

| Ending ID | Rank & Title | Rational Paths (`6,355`) | Rational Markov `%` | Full-Open Paths (`8,372`) | Full-Open Markov `%` | `v1.1` Causal Guarantee |
|---|---|---:|---:|---:|---:|---|
| **`END_TRUE`** | `TRUE ENDING` — *"Where the Night-Wind Keeps Your Hue"* | `1,242` | **`18.5872%`** | `1,242` | `5.5583%` | `0%` Route A `INSIGHT` bypass; `0` dominated choices; all `3` routes contribute (`300` A / `224` B / `718` C). |
| **`END_GOOD`** | `GOOD ENDING` — *"Sixty-Day Candlelight"* | `665` | **`21.6471%`** | `1,024` | `27.4902%` | `0` paths ever downgraded to `END_NEUTRAL` by `C18_C_GATE2` (`82` low-`BOND` builds safely stay `END_GOOD`). |
| **`END_NEUTRAL`** | `NEUTRAL ENDING` — *"The Uncracked Spine"* | `2,228` | **`28.3854%`** | `3,886` | `35.5713%` | Reached only via Routes A/B (`BOND < 14`, missing `F07`, `COLD_FIREWALL_NO_VOW`, or `RAW_VIGIL_STRAIN`). |
| **`END_BAD_1`** | `BAD ENDING I` — *"White Canvas on Verona Shore"* | `1,024` | **`11.9141%`** | `1,024` | `11.9141%` | Route A `C11_A3` yield + `4` distinct closing beats per `C19_BAD1` option. |
| **`END_BAD_2`** | `BAD ENDING II` — *"Prisoners of the Seventh Hue"* | `1,196` | **`19.4661%`** | `1,196` | `19.4661%` | Route B incomplete Prism Key + physical Wayob conduit parity + `4` closing beats per `C20_BAD2` option. |
| **TOTAL** | **`44 / 44` Nodes Visited (`0` Orphans, `0` Deadlocks)** | **`6,355`** | **`100.0000%`** | **`8,372`** | **`100.0000%`** | **`13/13` Binary Trade-Offs Non-Dominated & Non-Isomorphic** |

---

## 5. Updated Benchmarks, Audio Alignment & Complete `42`-CG Roster

### 5.1 Patched Literary Benchmarks (`100%` ASCII `0x20..0x7E`, Exact `len()` Verified)

**Benchmark A — Chapter 1 (`N08`: Canonical `5.7` Hand-Holding Jealousy):**
```text
[Citlali]  (voice_emotion: "vn_playful_tease")
"Hmph. Sounds dreadfully contrived if you ask me. Any half-competent shaman could trace residual Ley-miasma with an obsidian mirror instead of clinging to someone's fingers like a lost toddler."
  -> inner_thought (132 chars): "Holding hands?! Why holding hands specifically?! Couldn't they tie a spirit-cord to a sleeve--what kind of shameless excuse is that!"

[Citlali]  (voice_emotion: "vn_shy_blush")
"Th-That was a strictly utilitarian sense-transfer incantation to find my errant grandson! Don't lump secret Night-Wind shamanic arts in with--stop grinning into your juice cup, Traveler!"
  -> inner_thought (125 chars): "Quiet, heart, quiet! He remembers the exact wording?! Ugh, if his palm brushes mine under this table I am going to combust..."
```

**Benchmark B — Chapter 2 (`N16`: Opaque Painted Goblet & White Static Decay):**
```text
[Narrator]
Painted Night-Wind stoneware strikes the reed mat and splits in two. Clear cold water--not pale-golden Quenepa wine--soaks the hem of Citlali's skirt while pale rime crusts every rigid knuckle.

[Citlali]  (voice_emotion: "outing_bump_rescue")
"Clumsy cup... Don't make that face at me, Traveler. Do you have any idea how ridiculous Natlan's hero looks hovering over spilled water? Take Paimon back to town. I still have scroll-work left."
  -> inner_thought (133 chars): "[...cold... don't let him touch my wrist... if the loom drinks his gold mark next, please don't let me forget the sound of his-- ...]"
```

### 5.2 Complete `42`-CG `Base -> Diff` Assignment Table (`42/42` Mapped)

- **Chapter 1 (`9` CGs):** `ch1_01_doorstep_graffiti_base` (`N01`), `ch1_02_key_frost_ward_diff` (`N02`), `ch1_03_sanctuary_wake_base` (`N03a`), `ch1_04_sanctuary_blush_itzpapa_diff` (`N03b`), `ch1_05_ororon_cabbage_chaos` (`N04`), `ch1_06_bookshelf_novels_base` (`N05`), `ch1_07_six_kitsune_cipher_diff` (`N06`), `ch1_08_promenade_friends_base` (`N07`, `N08` pre-choice), `ch1_09_promenade_palm_diff` (`C04_A` post-choice reaction).
- **Chapter 2 (`8` CGs):** `ch2_01_ororon_aphid_garden` (`N09`, `N10`), `ch2_02_graffiti_wall_base` (`N11`), `ch2_03_graffiti_sunset_diff` (`N12`), `ch2_04_rooftop_stars_base` (`N13`, `N14` pre-choice), `ch2_05_rooftop_handkerchief_diff` (`C07_A` post-choice reaction), `ch2_06_quenepa_lamp_base` (`N15`), `ch2_07_quenepa_shatter_diff` (`N16`), `ch2_08_astralloom_reveal` (`N17`).
- **Route A (`6` CGs):** `ch3a_01_soulbridge_handclasp` (`N18_A1`), `ch3a_02_huitzilin_wildflowers` (`N19_A2`), `ch4a_01_whitesurge_crossroads_base` (`N20_A3`), `ch4a_02_counterweave_diff` (`N21_A4`), `end_bad1_01_sealed_door_diff` (`N30_BAD1_1`, Diff of `ch1_06`), `end_bad1_02_stranger_shore` (`N31_BAD1_2`).
- **Route B (`5` CGs):** `ch3b_01_chasca_ororon_canyon` (`N22_B1`), `ch3b_02_seven_hued_mural` (`N23_B2`), `ch4b_01_monochrome_vault_base` (`N24A_B3`, `N24B_B4`, `N25` pre-choice, `N32_BAD2_1` opening), `ch4b_02_prism_gate_diff` (`C15_B_PRISM_KEY_UNLOCK` post-choice reaction), `end_bad2_painted_twilight` (`N32_BAD2_1` transition & `N32B_BAD2_2`).
- **Route C (`5` CGs):** `ch3c_01_mavuika_xilonen_council` (`N26_C1`), `ch3c_02_xilonen_forge_terrace` (`N27_C2`), `ch4c_01_sacred_flame_regulator_base` (`N28_C3`, `N29` pre-choice), `ch4c_02_name_conduit_diff` (`C18_C_NAME_CONDUIT_UNLOCK` post-choice reaction), `end_good_rooftop_candlelight` (`N33_GOOD_1`).
- **Chapter 5 & Endings (`9` CGs):** `ch5_01_nightkingdom_threshold` (`N34`), `ch5_02_ukumbuko_awakening_base` (`N35`), `ch5_03_loom_crescendo_diff` (`N36`), `ch5_04_morning_tea_sanctuary` (`N37`), `ch5_05_verona_cliff_sunrise_base` (`N38`), `ch5_06_verona_cliff_turn_diff` (`N39`), `end_true_01_wrist_ribbon_tears` (`N40`), `end_true_02_eternal_sunrise_vow` (`N41`), `end_neutral_uncracked_spine` (`N42`).
  - **Total Unique `.jpg` Assets:** `9 + 8 + 6 + 5 + 5 + 9 = 42` (`100%` node/reaction coverage, `0` unreferenced stems).

---

## 6. Post-Review Resolution Ledger (`33/33` Audit Items Closed in `v1.1`)

- **`[PLOT-01..11]` (`11/11` Closed):** `"Bitesberry"` purged globally -> canonical **`"Quenepa"`** (`F08_QUENEPA_CONFESSION`, `ch2_06/07`); Citlali physically crosses the Law 0 Wayob Conduit into the Seven-Hued vault in `N24A_B3`; `Character Story 5` / *The Color of Memory* answer preserved as prior canon while `N35` resolves living remembrance; *"nothing gold can stay"* reserved for present-day Aether; Paimon cannot hear telepathy (`N15` uses outward cake-eating tell); embedded First-Era **Obsidian Name-Core** unifies `Ukumbuko` across Routes A/B/C; Huitzilin's note fixed as a 200-year-old woven bookmark slip inside `Six Kitsune` with `F02`/`!F02` setup and `when: F03` gating in `N40`; Yohualtecuhtin post-`AQ V.5` Capitano fusion respected; `5.7` Loom of Fate seam aftershock added to Law 1; frost-cracked inner ward + ownership-imprint resonance in `N17`; `"Pacific"` -> `"western surf"` in `N39`.
- **`[DAG-01..10]` (`10/10` Closed):** `C21_CH5` equal `+2B/+2B`; `C10_A1` (`32` wins) vs `C10_A2` (`28` wins); `C12_A1` `min_insight: 8` + `C12_A2` `-3B + RAW_VIGIL_STRAIN` (`0%` Route A bypass); `C07_B` `+3B` + `N17` `bond>=7 & insight>=8` (`242` wins, `56` prefixes / `500` paths); `C13_B2` (`50` wins) + `N25` Ororon Harmonic Spindle recovery (`108` paths, `N24B_B4` `86/138` wins); `C18_C_GATE2` partitioned into Token + Physical Proof + `2-of-4` Heart Truths + `min_bond: 10` (`0` downgrades); `C01..C08` & `C16_C/C17_C` 100% non-isomorphic; `C11_A2` badged `[Quarantine Protocol -- Severs Emotional Link]`; exact max stats `21/24` & `21` verified.
- **`[PACE-01..05]`, `[PROSE-01..04]`, `[CG-01..02]`, `[AUDIO-01]` (`12/12` Closed):** `565`-beat budget rebalanced; `4` bespoke closing beats per option on `C19_BAD1` & `C20_BAD2`; `N38` send-off gated by `ROUTE_A/B/C`; `COLD_FIREWALL_NO_VOW` / `RAW_VIGIL_STRAIN` / `bond<14` damped variants in `N35–N37`; daytime sleep/camp transitions in Ch.3–4; `"incantation"` / `"shamanic arts"` / canonical `5.7` hand-holding quote / opaque stoneware goblets / verbatim `vn_tender_love_01.wav` Ascension 6 vow; `4` Diff CGs moved strictly onto post-choice `reaction_beats`; `42nd` CG assigned to `end_bad1_01_sealed_door_diff.jpg`; voice buckets cleaned on `N09`, `N22_B1`, and `N32B_BAD2_2`.
