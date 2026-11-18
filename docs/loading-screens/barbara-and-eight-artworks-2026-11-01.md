# Barbara anatomy fix + eight new loading artworks

Date: 01/11/2026. Target: gameplay-lab. Status: **user visually approved all nine artworks; not installed**. User asked to proceed to the [full-roster batch plan](female-roster-batch-plan-2026-11-01.md).

User accepted the short Project Wibu intros and reported that the crash came from opening multiple game windows. This stage only creates the requested artwork; it does not change runtime archives, plugins, music, or the existing fourteen posters.

## Deliverables

All nine assets were created/edited using built-in ImageGen. Original generated masters are retained in the workspace; standard PNG exports are RGB, 1920×1080.

| File in exports/ | Content |
| --- | --- |
| barbara-fixed.png | Corrected LOADSC14 composition: remove extra ear-touching hand/sleeve; one arm lowered and one holding the player |
| citlali-solo.png | City overlook, violet twilight, coupe and plush |
| hutao-solo.png | Cinema and burgundy car, lanterns after rain |
| furina-solo.png | Waterfront opera-house cafe and cake |
| kirara-solo.png | Hillside delivery street, mint van and parcel |
| chiori-solo.png | Boutique, designer streetwear, ivory/black coupe |
| lumine-solo.png | Coastal roadtrip viewpoint, map and white coupe |
| columbina-tsaritsa-vesna-trio.png | Shared hotel-arrival scene and limousine, ice/lavender/teal palette |
| barbara-jean-duo.png | Sisters on seaside roadtrip, blue convertible |

Approved direction retained: flat 2D anime lineart/cel shading, GTA poster framing, urban adaptations with recognizable Genshin identities, black/white Wibu World wordmark. Tsaritsa and Vesna use the visual designs embedded in the user's reference atlas. Attribution was preserved as supplied, not independently reverified in this art-production stage.

## Review and evidence

- [Offline gallery, with Barbara before/after comparison](../../../staging/project-eagle/loading-art-refresh-20261101/gallery.html).
- [Asset manifest and hashes](../../../staging/project-eagle/loading-art-refresh-20261101/manifest.json).
- [Exact prompt set, source outputs and input images](../../../staging/project-eagle/loading-art-refresh-20261101/generation-records.json).
- [Export/original preservation verification](../../../staging/project-eagle/loading-art-refresh-20261101/qa/verification.json).
- Masters: `staging/project-eagle/loading-art-refresh-20261101/masters/`; exports: sibling `exports/`; individual prompts: sibling `prompts/`.

Agent inspected each generated output for requested cast/identity, visible arm/hand connections, framing and logo. The two group scenes have distinct poses and the expected character counts. All nine exported PNGs decode at the intended size; all local gallery image/manifest links resolve. Existing fourteen artwork exports still match their recorded hashes. Browser interaction and GTA playback were not tested by the agent; the user subsequently approved all nine artworks on 01/11/2026.

## Integration boundary

No shared game-write lock was acquired because no runtime or deployment metadata was written. There is no runtime rollback for this stage; existing assets are retained unchanged. Barbara is a replacement candidate for LOADSC14; the other eight are additional library candidates, not assigned to new native slots.

The native loading path previously traced chooses among fourteen poster indices. Merely appending LOADSC15+ textures does not extend that selection. Preserve current roster coverage when preparing the later integration; design the library/selection extension separately rather than replacing eight unrelated existing screens or claiming these PNGs are already active.

User passed this set on 01/11/2026. Full female-roster loading/menu expansion remains plan-first, with small approved batches. No full-roster or additional nonplayable artwork was generated here.
