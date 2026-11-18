# Project Eagle: Aether protagonist candidates

Research date: 2026-10-13. Scope: GTA San Andreas PC/classic character models suitable for replacing CJ. The Project Eagle game was not modified. Downloaded archive contents were listed only; no archive files were extracted or run.

## Recommendation

**Best-supported candidate found: FadXploit, “Aether from Genshin Impact,” Update 3.0 (March 2023).** It has a direct GTAinside listing, creator attribution for conversion/rigging, and a creator-authored YouTube showcase. Its archive also ships a separate “Shadeless DFF & Smaller TXD (for non-ENB)” option that substantially cuts texture footprint. This is the strongest documented classic-SA option found in this search, but the available evidence does not establish complete CJ animation/function compatibility. In-game checks would still be needed for walking/running, combat and weapon poses, swimming, climbing, and vehicle entry/exit/driving.

## Candidate comparison

| Candidate | Evidence and appearance | Resource evidence | Rig/function confidence | Assessment |
|---|---|---|---|---|
| **FadXploit — Aether v3.0, GTA SA classic** ([GTAinside listing](https://www.gtainside.com/en/sanandreas/skins/156646-aether-from-genshin-impact/), [creator-authored showcase](https://www.youtube.com/watch?v=wq0WBo_lsl4)) | Listing credits HoYoverse for the source model and FadXploit for rig/convert/port. The creator's video description repeats those credits and points viewers to the GTAinside release. The listing says update 3.0, March 2023. Its screenshots show the detailed blond Traveler in GTA streets: front and back views, a weapon pose, and a GTA weapon pose. Screenshot frames have strong chromatic color fringing and stylized post-processing, so they are not clean evidence of default-game image quality. | Listing reports 2.094 MB. Downloaded archive is 2,195,669 bytes (7z). Standard Aether: DFF 1,265,954 B; TXD 4,981,288 B (6,247,242 B combined). Non-ENB/light option: DFF 1,080,110 B; TXD 1,311,272 B (2,391,382 B combined). The alternate pair is about 62% smaller combined; its TXD is about 74% smaller and DFF about 15% smaller. | Creator explicitly claims a rig/convert/port, but neither the listing nor the inspected archive manifest enumerates supported GTA animation groups. A GTAinside comment by FadXploit on the older listing says he had reduced a related model to 51K polygons and it still sometimes crashed; that comment predates the 2023 update and does not establish v3.0 polygon count or behavior. | **Lead option.** Strong provenance and a useful lightweight texture variant. Detailed appearance comes with a larger standard TXD; choose the smaller variant for a lighter starting point, then evaluate its shading/appearance in Eagle. No promise of complete protagonist animation support. |
| **Miyata Lee — “Aether - Genshin Impact,” third-party GTAall listing** ([listing](https://www.gtaall.com/gta-san-andreas/skins/237591-aether-genshin-impact.html), [French mirror](https://www.gtaall.eu/fr/gta-san-andreas/skins/237591-aether-genshin-impact.html)) | The page names Miyata Lee and claims a high-quality model/textures, movable skeleton and hands. It was added by “Underground47,” and the description is generic boilerplate. The page labels the skin gender “Female,” which conflicts with the named male Traveler. I found no creator-authored source establishing model provenance or a direct original release. | Listing gives no archive size or model/texture inventory. I followed the “download the zip-file without installer” route, but the endpoint returned an HTML page (12,656 bytes), not a ZIP; therefore there is no archive manifest or size comparison. | The page claims a movable skeleton and hands, but gives no animation coverage or test evidence. | **Do not prefer on current evidence.** It might be a usable option, but its provenance, male character identity, contents, and weight could not be checked. The one-click/manual route did not yield a usable archive. |

## FadXploit archive inspection

Downloaded from the GTAinside download route to:

`C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\aether\research\FadXploit_Aether_3.0.7z`

SHA-256: `CFC3D6129B8E493703579683E21DD2593B054B2A7F2F7E06A38EC2EE939F4F2B`

Archive manifest (uncompressed bytes as reported by 7z metadata):

| Entry | Size |
|---|---:|
| `Aether by FadXploit/Aether.dff` | 1,265,954 B |
| `Aether by FadXploit/Aether.txd` | 4,981,288 B |
| `Aether by FadXploit/Shadeless DFF & Smaller TXD (for non-ENB)/Aether_SL.dff` | 1,080,110 B |
| `Aether by FadXploit/Shadeless DFF & Smaller TXD (for non-ENB)/Aether_SL.txd` | 1,311,272 B |
| `Aether by FadXploit/FadXploit Aether GTA SA 00.jpg` | 881,349 B |
| `Aether by FadXploit/Readme (EN).txt` | 2,078 B |
| `Aether by FadXploit/Readme (ID).txt` | 2,257 B |

No archive content was extracted. File sizes are storage sizes only; mesh topology, texture dimensions, draw calls, memory use, model quality at gameplay distance, and runtime performance were not measured.

## Limits and next evaluation

The source and manifest support these claims: a creator-attributed GTA SA port exists; the archive contains standard and smaller non-ENB model/texture pairs; and the creator showcased it in GTA SA. They do not show that every CJ gameplay action works correctly, nor that it has been tested against the selected Eagle installation. Static screenshots do not test animation. The next meaningful evaluation is a staged install into a recoverable copy of Project Eagle, followed by explicit checks of walk/run, melee, common firearms, swimming, ladder/climb behavior, and vehicle use, including clipping, missing parts, and crashes. Do not infer compatibility from the third-party “movable skeleton” phrasing.

## Sources

- [GTAinside FadXploit listing and comments](https://www.gtainside.com/en/sanandreas/skins/156646-aether-from-genshin-impact/)
- [FadXploit-authored GTA SA showcase](https://www.youtube.com/watch?v=wq0WBo_lsl4)
- [GTAinside direct 7z archive](https://files.gtainside.com/202012/1677955155_FadXploit%20Aether%203.0.7z)
- [GTAall Miyata Lee listing](https://www.gtaall.com/gta-san-andreas/skins/237591-aether-genshin-impact.html)
- [GTAall manual-download route](https://www.gtaall.com/get-manual/15bd312caef2a37bea760508ed58dda48545efae/237591-aether-genshin-impact.html) (served HTML during this inspection)
