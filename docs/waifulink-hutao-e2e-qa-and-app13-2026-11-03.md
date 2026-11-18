# WaifuLink v4.0 — EaglePhone Button #13 & Hu Tao End-to-End QA Report (2026-11-03)

- **Agent:** Antigravity (`35d5cf80-28f1-43e1-8e77-f60ee3d570c3`)
- **Work Item:** `docs/project-eagle/work-items/2026-11-03-antigravity-waifulink-hutao-e2e-test-and-app13-button.md`
- **Target Runtime:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Staging, Test Runners & Screenshots:** `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-hutao-qa-20261103\`
- **Presentation 03/11 Compliance:** Untouched (`WibuMenu.asi`, `models/fronten2.txd`, `models/fronten3.txd`, loading/menu/startup/audio packages intact). Furina & Citlali scenario/milestone packages preserved with zero regressions.

---

## 1. Summary of Completed Deliverables

1. **EaglePhone OS v5.0 — Upgraded App 13 (`WaifuLink`) to a Full First-Class Home Button:**
   - Generated custom `ep_ic_waifu` (glowing pink heart icon), `ep_ic_paimon`, and `ep_bn_waifu` assets in `build_eaglephone_txd.py` and rebuilt `models/hud.txd` (`29` `ep_*` textures), `CUSTOM/EAGLEPHONE_UI.TXD`, `models/txd/EAGLEUI.TXD`, and `ui_assets/*.png`.
   - Upgraded `hud.lua` (`activeApp == "0"`) from a `4×3` grid + thin bottom strip to a **5-Row (`5×3`) Home Screen Grid** (`ph = ScreenSize(386.0)`), rendering all **13 full rounded app tiles (`1..13`)** with `ep_ic_waifu` on Button #13 (`13.WaifuLink`) and a live WaifuLink Companion Status Card spanning columns 2–3 of Row 5.
   - Updated `eagle_phone_ui.py` Web UI `.app-dock` from `repeat(13, 1fr)` to `repeat(14, 1fr)` (`dock-0..dock-13`) and added the top `💖 WaifuLink (App 13)` shortcut button.
2. **Native DirectX 9 16:9 CG Streaming (`WLCG0.TXD` / `WLCG1.TXD`):**
   - Implemented ping-pong RenderWare D3D9 texture dictionary streaming (`_sync_dynamic_waifulink_cg_txd` in `EagleCompanion.py` + `RefreshWaifuLinkDynamicCg` / `DrawDynamicWlCg` in `hud.lua` via `Opcode 0x0390` / `0x038F` / `0x0391`) so all `135` Hu Tao `.jpg` CGs (`120` Scenario + `15` Milestone) render directly inside GTA SA's DirectX 9 framebuffer without stealing foreground focus or resetting Exclusive Fullscreen D3D9.
3. **Full End-to-End Verification of Hu Tao (`char_id = "hutao"`):**
   - **Part A (`run_hutao_engine_e2e.py`):** `46/46` assertions **PASS** (`T01..T07`, including live `gpt-6-luna` AI custom chat & AI-generated Turn-2 quick replies, 2-strike Off-Topic Re-Ask + Anti-Stuck Bridge, `45/stage` chat cap, `75/stage` free-roam cap, `199` Stage Gate clamp, `3/3` Stage Up counter reset, Non-Hardlocked Stage Carryover, and Dynamic AI Encore).
   - **Part B (`run_hutao_live_ingame_e2e.py`):** `10/10` live `gta_pe.exe` + `EagleCompanion.py` DirectX 9 screenshots & full-flow assertions **PASS** (`L01..L04`, `0` crashes, `0` Lua errors).

---

## 2. All 13 Bugs Discovered & Fixed During Audit + Live `gta_pe.exe` Testing

| # | Component | Root Cause | Fix Applied |
|---|---|---|---|
| 1 | `EagleCompanion.py` | Missing top-level `import os` caused `NameError: name 'os' is not defined` inside `is_game_active_and_unpaused(allow_self_overlay_fg=True)` (breaking `Backspace` & hotkeys whenever House Menu / VN Overlay opened) and inside `_sync_dynamic_waifulink_cg_txd`. | Added `import os` at top of `EagleCompanion.py`. |
| 2 | `hud.lua` & `eagle_dating_sim.py` | **Live `gta_pe.exe` Crash (`0x00727B45` in `CFont::ParseToken`):** Unmatched `~` tilde in Hu Tao's dialogue (`"Aiya~"`, `"Hehe~"`) crashed `Font.PrintString` with Access Violation `0xC0000005`. | Sanitized `~` -> `-` in `DrawPhoneText` (`hud.lua`) and `_hud_ascii` (`eagle_dating_sim.py`). |
| 3 | `EagleCompanion.py` | `is_game_active_and_unpaused` & `_check_gps_arrival_and_sync` read `0x00BA677B` (`m_bActivateMenuNextFrame`) instead of `0x00BA67A4` (`CMenuManager::m_bMenuActive = 0x00BA6748 + 0x5C`), and `poll_hotkey_edge` dropped fast `< 100ms` taps. | Switched both reads to `0x00BA67A4`, added LSB tap latch + modal transition `clear_hotkey_states()` drain, and enabled `Backspace` / `F8` close across House Menu, VN Overlay, and Proximity HUD. |
| 4 | `eagle_dating_sim.py` | Hu Tao's `home_coords` overlapped Woozie's EHI interior yellow warp cone (`sfh_woozie_apt_sf`), and `date_spots[0]` was only `9.9m` from her doorstep (`<= 25m` arrival radius -> instant auto-complete). | Moved `home_coords` to `wb_sakura_chinatown` (`[-2178.50, 662.00, 49.45]`, Chinatown SF) and `date_spots[0]` to `hutao_pier69` (`[-1736.50, 1369.50, 7.18]`, `834.2m` away) + `> 80m` distance guard. |
| 5 | `hud.lua` / `build_eaglephone_txd.py` / `eagle_phone_ui.py` | App 13 (`WaifuLink`) had no rounded tile on EaglePhone's Home Screen (only a thin bottom strip) and misaligned Web UI `.app-dock`. | Built `ep_ic_waifu` texture into `models/hud.txd`, upgraded Home Screen to a `5×3` grid with full rounded Button #13 + status card, and updated Web `.app-dock` to `repeat(14, 1fr)`. |
| 6 | `eagle_vn_ingame_overlay.py` | External Tkinter `deiconify()` stole focus from Exclusive Fullscreen D3D9 (`0x00C9C060 == 0`), minimizing `gta_pe.exe`. | Replaced default rendering with native DirectX 9 16:9 `WLCG0/1.TXD` streaming in `hud.lua` and gated Tkinter overlay behind `WAIFULINK_TK_OVERLAY == "1"` + windowed check (`0x00C9C060 != 0`). |
| 7 | `EagleCompanion.py` & `eagle_dating_sim.py` | `_sync_dynamic_waifulink_cg_txd` did not check `self.dating_sim.media_dir` (`data/project-eagle/dating-sim/media`), and `build_hud_kv` looked up `hm_card.get("milestones")` instead of `self._get_milestones_for_char(...)`. | Added `self.dating_sim.media_dir` fallback and `_get_milestones_for_char(...)` lookup so House Menu, 4-Scene VN, Cameo VN, and Time-Apart Photo Banners all stream real 16:9 `.jpg` CGs into DirectX 9 VRAM. |
| 8 | `hud.lua` | `DrawWaifuLinkRelationshipBar` centered text across full bar width instead of left region (colliding with the pink progress meter), and VN choice rows hardcoded `cIdx == 1` highlight instead of `vnSel`. | Centered relationship header/metrics within `leftRegionMidX` and wired dynamic `vnSel` (`wl_vn_sel`) highlight + `[F6]` live custom typing bar. |
| 9 | `eagle_dating_sim.py` | `build_projection()` omitted top-level `recommended_choices`, leaving App 13 quick-chat `[1/2/3]` empty in-game. | Added `"recommended_choices": selected_card.get("suggested_replies") or []` in `build_projection()`. |
| 10 | `eagle_dating_sim.py` | `send_message()` only checked static Stage starters & milestone reactions for `choice_id`, ignoring Turn 2+ AI-generated `ai_sug_1..3` replies stored in `suggested_replies_json`. | Resolved `suggested_replies_json` inside `send_message()`. |
| 11 | `eagle_dating_sim.py` | `tick_ram_guard()` never polled live GTA SA `CVehicle` (`+0x4C0` float HP) or wanted stars during Free-Roam Outings, so `crashes_detected` stayed `0`. | Added live `CVehicle` HP drop (`>= 12.0` HP, `1.5s` debounce) and wanted-level collision tracking in `tick_ram_guard()`. |
| 12 | `eagle_dating_sim.py` | Milestone CGs unlocked at `0ms` during in-person hangouts instead of waiting until Aether and Hu Tao are apart. | Added `pending_milestones` + `_tick_time_apart_photo_drops` in `tick_ram_guard()` so Milestone Photos + EaglePhone Event Banner + CG thumbnail fire autonomously after Aether leaves (`> 38m` apart & `>= 10s` elapsed). |
| 13 | `eagle_ingame_tester.py` | `_find_gta_hwnd` could select an internal `gta_pe.exe` helper window (`QuickTime`/`DirectShow`) instead of RenderWare's D3D9 window during map load. | Updated `_find_gta_hwnd` to read `RsGlobal.ps->window` (`0x00C17054`) first and prioritize class `"Grand theft auto San Andreas"`. |

---

## 3. Verified Live In-Game Screenshots (`1920×1080` DirectX 9)

Saved under `staging/project-eagle/waifulink-hutao-qa-20261103/live_screenshots/`:
- `live_01_phone_home_btn13.png` — EaglePhone OS v5.0 `5×3` Home Grid with cursor on full rounded Button #13 (`13.WaifuLink`) + Companion Status Card.
- `live_02_phone_app13_waifulink.png` — App 13 (`WAIFULINK v4.0: Hu Tao`) inside EaglePhone with 3 Quick-Chat choices & action rows.
- `live_03_chinatown_proximity_hud.png` — Ambient Chinatown SF doorstep proximity HUD (`wl_house_near = 1`) triggered automatically within `22m` without opening EaglePhone.
- `live_04_house_visit_event_selector.png` — 5-Option House Visit Event Selector (`[F9]`) with Hu Tao's `M01` 16:9 CG rendered in DirectX 9.
- `live_05_walkaway_hud_clean_hidden.png` — Clean GTA SA HUD with all WaifuLink overlays auto-hidden after walking `> 22m` away.
- `live_06_vn_scene1_opening_cg.png` — Core VN `Scene 1/4` (`The 77th Director's Grand Sales Pitch`) with native 16:9 Couple CG (`Aether + Hu Tao`), portrait card, Butterfly Spirit thought, 3 choices, and `[F6]` custom reply bar.
- `live_07_vn_scene4_ending_autoclose.png` — Core VN `Scene 4/4` Couple Ending (`SCENARIO PASSED! (+35 Affection)`, `Stage Gate: 1/3`, `Auto-closing overlay in 3.4s`).
- `live_08_vn_extra_cameo_genshin.png` — Extra Genshin Cameo VN (`Wanmin Kitchen Chaos with Xiangling, Xingqiu & Chongyun`).
- `live_09_freeroam_outing_hud_gps.png` — Free-Roam Chauffeur Outing to `Pier 69 Lantern Bayside (833m)` with native GTA SA GPS radar blip & `S-RANK (+25)` live tracker.
- `live_10_time_apart_photo_banner.png` — Autonomous Time-Apart Milestone Photo Drop (`M02: Wangsheng VIP Coupon Street Snap`) at Pier 69 after `10.8s` apart, complete with live `M02` 16:9 photo preview under the green `[ALERT]` banner.

---

## 4. Follow-Up Upgrade (2026-11-03 22:41) — Fullscreen 16:9 Visual Novel Stage & Translucent Footer Dialogue HUD

Per user feedback requesting a full-bleed scenario CG and a translucent bottom dialogue footer matching standard Japanese Visual Novels:

1. **Full-Bleed 16:9 Visual Novel Canvas + Translucent Frosted Dark-Glass Footer (`hud.lua`):**
   - Enlarged `DrawWaifuLinkDatingHud()` (`vnActive == true`) from a centered thumbnail card to a **full-bleed 16:9 viewport CG** (`cgW = min(sw, sh * 16/9)`, `cgH = cgW * 9/16`).
   - Anchored a **translucent dark-glass dialogue footer** (`fw = min(cgW - ScreenSize(24.0), ScreenSize(748.0))`, `fh = ScreenSize(124.0)`, `RGBA(8, 10, 22, 152)` ~60% frosted glass / 40% visible CG) directly along the bottom edge of the CG using `Sprite2d.DrawRect` (`CSprite2d::DrawRect` `0x00727B60`) for true DirectX 9 vertex alpha blending.
   - Added a classic crimson-gold speaker nameplate tab with avatar (`ep_ms_<char_id>`) on the top-left lip, scenario/cameo cast pill on the top-right lip, inner thought cue `(...)`, 1–3 balanced dialogue lines (`wl_vn_line1..3`, wrapped at `114` chars in `eagle_dating_sim.py`), 3 translucent interactive choice bars (`DrawVnChoiceRow`), `[F6]` live custom AI typing bar, and Scene `4/4` emerald translucent completion banner.
   - Added `wl_vn_active == "1"` early-return guards across `Hud.RenderWeaponIcon`, `Hud.RenderWeaponAmmo`, `Hud.RenderClock`, `Hud.RenderMoney`, `Hud.RenderArmorBar`, `Hud.RenderHealthBar`, `Hud.RenderBreathBar`, `Hud.RenderWantedLevel`, and `Hud.RenderRadar` so vanilla `$30000` / radar / HUD never draw over Visual Novel scenes.
   - Updated `DrawPhoneText()` to sanitize `|` -> `-` (`FONT_SUBTITLES` draws `|` as `°`) and strip `*` (`CFont` treats `*` as a control token and blanks strings).
2. **Crisp `1024×512` Ping-Pong D3D9 `.TXD` Streaming (`EagleCompanion.py`):**
   - Upgraded `_build_waifulink_cg_txd_bytes()` to `1024×512` (`2,097,320` bytes 32-bit BGRA RenderWare `0x1803FFFF` `.TXD`) and added `_ensure_waifulink_cg_txd_slots()` in `EagleCompanion.__init__` so `models/txd/WLCG0.TXD` and `models/txd/WLCG1.TXD` always exist before `gta_pe.exe` boots (ensuring `modloader.asi` indexes both slots in its VFS table and updates overwrite inactive slots in-place).
3. **Live DirectX 9 Verification (`verify_vn_fullscreen_footer.py` — `100% PASS`):**
   - Verified `RwTexture* = 0x6EC8D280` in VRAM (`0x00A94CE0`), `0` Lua errors (`cleo/EagleLuaErrors.log`), `0` crashes, and inspected all 5 live `1920×1080` D3D9 screenshots under `staging/project-eagle/waifulink-hutao-qa-20261103/live_screenshots/`:
     - `vn_v2_01_fullscreen_scene1.png` — Fullscreen 16:9 Scene `1/4` CG + translucent footer + Hu Tao nameplate + 3 choices.
     - `vn_v2_02_cursor_and_f6_typing.png` — Choice `[2]` gold/crimson highlight + `[F6]` live typing bar (`[TYPING] > hehe_`).
     - `vn_v2_03_fullscreen_scene2.png` — Ping-pong CG swap to Scene `2/4` with outfits clearly visible through translucent glass.
     - `vn_v2_04_fullscreen_scene4_ending.png` — Scene `4/4` Couple Ending + emerald translucent `SCENARIO PASSED! (+35 Affection)` banner & `4.3s` auto-close countdown.
     - `vn_v2_05_fullscreen_cameo_genshin.png` — Extra Genshin Cameo VN (`Xiangling, Xingqiu, Chongyun, Guoba`) in fullscreen 16:9.

### Final Runtime SHA-256 Manifest (`gta sa gameplay-lab`)
- `hud.lua`: `4B653BE5B3CEC9CACD107EEAC501E3B1E57EBBC82F4C096E92D2C76184553D61`
- `EagleCompanion.py`: `FD0E0A7EF3927903B69C67973E304EBCBECAD50699F61B180804D1F769891E03`
- `eagle_dating_sim.py`: `54911ED5E44146CBF925EAE9FE0FD830CD7402BE9F790AAFFF161B35D745B00F`
- `cleo/EagleWaifuBridge.cs`: `0B7B073D3FE6DDA25A54F5EE41DCC8209713177ED3293B1581AE1193ECE1D454`
- `models/txd/WLCG0.TXD`: `0C2930D0D0BCF506F3BC740B9E0F673F3B7C1E96B6713501232975CFD35E8368`
- `models/txd/WLCG1.TXD`: `5DA745EC7B750EAC396CFEBED400BC89AB4918BF4B6CAA68610FECA2FF9768A3`
- Coordination lock `data/project-eagle/coordination/game-write.lock`: **released**.

---

## 5. Follow-Up Upgrade (2026-11-04 02:12) — Uncut App 13 `[F6]` Live AI Chat, `575 Broadway` 3D Passenger Outing & Triple-Layer `2000 HP` Immortal Waifu (`EagleWaifuBridge.cs`)

1. **App 13 (`13.WaifuLink`) Uncut Multi-Line Live AI Chat & `[F6]` Custom Keyboard (`hud.lua`, `eagle_dating_sim.py`, `EagleCompanion.py`):**
   - Expanded App 13's dialogue box (`hud.lua` `lines 2684–2725`) to render up to `6` full lines (`wl_gf_l1..l6`, wrapped at `76` chars in `eagle_dating_sim.py:build_hud_kv`, `456`-char capacity vs `<= 290`-char AI replies) plus `84`-char player/action cue lines (`wl_user_line`, `wl_gf_cue`) and smart Quick-Chat option rendering (`p_txt` when `<= 84` chars, falling back to concise `label` only for long hardcoded Stage 1 starters).
   - Constrained `gpt-6-luna` system prompt (`eagle_dating_sim.py` `lines 2006–2009`) and parser (`lines 2061–2066`) to 1–2 capitalized mood words (`<= 16` chars, e.g., `Warm Playful`) so mood tags never clip mid-word in DirectX 9.
   - Wired `[F6]` custom keyboard typing directly inside App 13 (`EagleCompanion.py`) so typed messages submit live to `gpt-6-luna` and populate Turn-2 dynamic Quick-Chat options `[1]/[2]/[3]`.
   - *(Honest visual note: the initial hardcoded M01 starter `wl_gf_cue` in `cf_01` is ~88 chars so its very end wraps with `flashes a...`; once chatting with live `gpt-6-luna` in `cf_02`, `wl_gf_cue`, all AI dialogue lines, and all `[1]/[2]/[3]` options render 100% uncut with zero `...`).*
2. **3D Waifu Companion Spawning (`ped_id=192` Hu Tao *Cherries Snow-Laden*) & Always-Topless Headrest-Free `575 Broadway` Chauffeur Outing (`cleo/EagleWaifuBridge.cs`, `eagle_dating_sim.py`):**
   - Compiled and deployed `cleo/EagleWaifuBridge.cs` (`128`-byte shared memory block anchored at `0x00A94CE4`, magic `0x57414946` `"WAIF"`, 60 FPS heartbeat `+0x5C`), spawning 3D Hu Tao (`ped_id=192`) at her Chinatown doorstep when within `55m` and warping the player (driver) + 3D Hu Tao (front-right passenger seat `0`) into a freshly spawned convertible when starting a Free-Roam Outing.
   - Audited `S&S\Cdimages\default\vehicles.img` geometry and switched the Free-Roam date car from `536 Blade` (`0.802m` tall headrests) to **`575 Broadway`** (`extras=[]` guaranteed open-top, `ped_frontseat.z = +0.007m` `+22.3cm` higher seating, `0.589m` flat bench with zero headrests), making 3D Hu Tao clearly visible from both rear chase view and front windshield (`Q+E`) camera.
   - Added incapacitated/dead player guard in `eagle_dating_sim.py:start_freeroam_outing` (`lines 2579–2586`) refusing outing start if `player_hp <= 0.5` or `ped_state in (54, 55)`.
3. **Triple-Layer Immortal 3D Waifu Protection (`cleo/EagleWaifuBridge.cs`):**
   - **Layer 1 (All-Proofs + `2000 HP` Clamp):** `0x02AB` (`bullet/fire/explosion/collision/melee` proofs = `0xBC`), `0x0819` (`dont_fall_off_bike`), `0x0446` (`dismemberment off`), `0x07FE` (`drown_in_water off`), and every-frame `CPed +0x540 = 2000.0`, `+0x544 = 2000.0`, `+0x548 = 100.0`.
   - **Layer 2 (`< 250 HP` Burning-Car Pre-Emptive Evacuation):** Before a damaged car (`CVehicle +0x4C0 < 250.0` or upside-down/submerged) can explode, `0x0362` (`remove_actor_from_car_and_place_at`) warps Hu Tao `5.5m` clear onto groundZ (`0x02CE`), clears fire (`0x0326`), restores `2000.0 HP`, increments `rescue_count`, and triggers `[ALERT] HU TAO SAFE (2000 HP)` via `EagleCompanion.py`.
   - **Layer 3 (Player `Wasted` Survival & Resurrection):** Continues running its 60 FPS loop even while Aether/CJ is dead (`Wasted`, `player_hp = 0.0`, `ped_state = 55`), evacuating Hu Tao out of any burning wreck and keeping her standing unharmed (`ped_state = 1`, `2000.0/2000.0 HP`).
4. **Live DirectX 9 E2E Verification (`verify_chat_freeroam_immortal_waifu.py` — `100% PASS`):**
   - Report JSON: `staging/project-eagle/waifulink-hutao-qa-20261103/chat_freeroam_immortal_report.json` (`all_passed: true`, `0` Lua errors, `0` crashes, `eagle_doctor.py` `11/11 PASS`).
   - 7 Visually Inspected `1920×1080` DirectX 9 Screenshots (`staging/project-eagle/waifulink-hutao-qa-20261103/live_screenshots/`):
     - `cf_01_app13_f6_typing.png` — App 13 `[F6]` live custom input `[CHAT] > osmanthus tea tonight [Enter]`.
     - `cf_02_app13_live_ai_reply.png` — Live `gpt-6-luna` uncut multi-line reply (`80 -> 86 -> 92` affection) + 3 uncut dynamic Quick-Chat options.
     - `cf_03_freeroam_3d_passenger_hutao.png` — Sunny rear chase view on Esplanade North showing CJ + 3D Hu Tao (`ped_id=192`) in open-top crimson `575 Broadway` with `S-RANK (+25)` HUD & Pier 69 GPS route.
     - `cf_03b_freeroam_front_camera_hutao.png` — Front windshield (`Q+E`) close-up confirming 3D Hu Tao (*Cherries Snow-Laden* white hat, crimson bow, twin-tails) sitting beside CJ.
     - `cf_04_arank_arrival_and_photo_banner.png` — Collision drop (`S-RANK -> A-RANK`), Pier 69 arrival (`92 -> 112` affection), and autonomous Time-Apart `M02` Photo Banner + CG preview.
     - `cf_05_burning_car_hutao_rescued_2000hp.png` — Burning `Broadway` (`220 HP`) while 3D Hu Tao stands safely rescued `5.5m` away at `2000.0 HP` (`rescue_count = 1`) with `[ALERT] HU TAO SAFE (2000 HP)`.
     - `cf_06_aether_wasted_hutao_immortal_2000hp.png` — Car exploded (`0 HP`) + player genuinely `Wasted` (`player_hp = 0.0`, `ped_state = 55`), while 3D Hu Tao survives 100% unharmed (`waifu_alive = true`, `2000.0/2000.0 HP`, `ped_state = 1`, `rescue_count = 2`, `60FPS_hb = 2950 -> 2969`).
