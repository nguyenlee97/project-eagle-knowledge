# Teyvat cross-review v2: orientation and collision evidence

Read-only evidence for the revised master plan (last write `2026-10-23 23:16:28`). The active master plan now defines the compass mapping correctly, but the current Mondstadt builder and staged binaries still use the earlier axis frame. No game or builder was run. The audit read the staged source, generated COL/IDE/IPL files and current gameplay-lab INI/SkyGfx configuration.

## Current source and binary snapshot

| Artifact | Last write | SHA-256 |
|---|---:|---|
| `D:\GTA Archive\Staging\mondstadt-vertical-slice-2026-10-23\build_mondstadt_vertical_slice.py` (91,539 bytes) | `2026-10-23 09:41:14` | `B482B55BED0458AC5DBE1F638DFB53344F4A0D8F4A3F003D2E1D0CD4189B6C43` |
| `D:\GTA Archive\Staging\mondstadt-vertical-slice-2026-10-23\models\col\mondstadt_city.col` (184,152 bytes) | `2026-10-23 23:03:38` | `810AF70C9CB3B1EA4789A114D8CE1864BF087B0E0CC313F322E36CD6F1C7FF92` |

The builder still parses OBJ positions at lines 90–108 as `(ux, uz, uy)`, and normals as `(nx, nz, ny)` (lines 111–116); source face order is swapped and then conditionally corrected against normals (lines 117–141). The revised master plan's desired mapping is `(−uz, −ux, uy)`, so the current staged mesh/COL is not yet in the revised compass frame.

An independent COL3 archive parse of the current bytes found:

| COL ID | Header name | Entry bytes | Faces / vertices / face groups | Header bounds (x,y,z), metres | Sphere radius | Quantized raw axis bounds (x,y,z), metres | Clamped scalar components |
|---|---|---|---|---|---:|---|---:|
| 6715 | `md_island_bridge` | 16,896 | 1,257 / 993 / 27 | x `[-204.0522, 204.0530]`; y `[-299.6782, 299.6772]`; z `[-39.0168, 39.0163]` | 342.0211 | x `[-204.0547, 204.0547]`; y `[-255.9922, 255.9922]`; z `[-39.0156, 39.0156]` | 105 on y |
| 6713 | `md_city_barbatos_plaz` | 16,324 | 1,268 / 883 / 27 | x `[-63.3358, 63.3350]`; y `[-58.3478, 58.3480]`; z `[-35.5112, 35.5122]` | 80.4319 | x `[-63.3359, 63.3359]`; y `[-58.3516, 58.3516]`; z `[-35.5078, 35.5156]` | 0 |

The int16 values encode metres at 1/128 resolution. On 6715, raw axis y reaches `±32767 / 128 = ±255.9921875m`; the COL header still claims about `±299.678m`. That is a confirmed truncation/deformation in this snapshot, with up to `43.686m` lost on the ends. Here “y” means the second stored component produced by the current builder's `(ux, uz, uy)` mapping. It is a horizontal OBJ-Z axis in this file, not world-up. Script lines 1018–1028 clamp each component independently to `[-32767,+32767]`; they do not reject or recenter out-of-range vertices. The script's COL writer at lines 1081–1112 uses per-entry packed bytes, not a face-count limit.

COL ID 6713 also has a likely binding defect: its IDE model name is the full `md_city_barbatos_plaza` (22 characters), but the writer at line 1086 truncates every COL model name to 21 characters before null-padding. GTA reversed's loader accepts an ID match only when the COL name key matches that model ID, then falls back to a model-name lookup in the COL slot; the truncated name matches neither the full ID key nor the full model name. Treat 6713 collision attachment as unproven and likely missing until the serialized name is corrected and the game confirms it. The current DFF/IDE names and COL bytes were inspected; the game was not run.

## Orientation migration: preserve a coherent frame

The revised mapping in the master plan is internally consistent with its anchor equations:

```text
X_gta = -Z_obj - 7283
Y_gta = -X_obj - 5775
Z_gta =  Y_obj - 203.5
```

The city-relative old parser frame is `p_old=(X_obj+2275, Z_obj+783, Y_obj−263)`. The new city-relative frame is therefore:

```text
p_new = (-p_old.y, -p_old.x, p_old.z)
```

This horizontal transform has determinant `−1`: it is a reflection across the negative diagonal, not just a label swap or a pure rotation. It reverses triangle orientation. Applying the parser edit alone is unsafe: current district classification uses local x/y at lines 145–177 and `slice_city_mesh` uses those coordinates (lines 179 onward); bridge terrain windows and shoreline cuts use explicit x/y ranges at lines 370–422; the procedural bridge endpoints are hard-coded in the old frame at lines 426–543; and the combined raycast/prop placement operates in that same local frame at lines 1279–1409 and 1433–1497. Existing per-model pivoting and local-to-IPL output at lines 1233–1402 and generated `mondstadt_city.ipl` are also tied to this frame. A parser-only change would move the OBJ geometry while leaving its masks/classifiers, bridge, props and world placement behind. It can also reverse face orientation relative to the current normal correction path.

The current staged IPLs are test placements: `mondstadt_city.ipl` places the city at the Sandar Bay test anchor `(6200,−3200,59.5)`, while `mondstadt_city_ls_bay.ipl` uses `(550,−3650,59.5)`. Neither is the revised plan's final Mondstadt anchor `(−6500,−3500,59.5)`. The eventual IPL export must apply the selected site/anchor only after the mesh-frame transform is settled.

**Safer Sector M1 approach:** retain the existing frame as an internal authoring frame while building/validating a candidate, then apply one explicit `p_new=(-y,-x,z)` transform at the export boundary to every spatial product. The export step must cover DFF positions, normals and triangle winding; COL vertices, faces and bounds; generated bridge and other procedural geometry; district/seam/ownership masks and grid selection; local pivots and IPL placements; raycast/prop placement coordinates; any world-space UV/projection data; and any route, walkability, A* or ped-node coordinates. The current builder does not emit A*/ped-node data, so those future consumers need an explicit coordinate contract rather than an assumption that they share the model's frame.

For a reflected point transform `B`, normals transform by `B` (renormalize), while retaining the same face order makes the geometric cross-product normal `−B*n`; reverse each triangle once to keep the face normal aligned with the transformed normal. A cleaner alternate migration is to update parser and all dependent algorithms together, then remove the old-frame winding compensation only after testing fixtures for a known upward triangle, known east/north landmarks, city classifier ownership, bridge endpoints and all four neighboring tile seams. Do not mix the parser's new basis with old hard-coded masks or coordinates.

## Correct interpretation of the limits in the plan

The gameplay-lab INI has `Collision size = 92768` and `LOD distance = 300.0` at lines 577 and 583. Upstream Fastman92 development INI describes Collision size as the maximum size of a *single collision from a COL archive*, separately from LOD distance. It is a byte budget per collision model, not “about 3,200 faces”: serialized model size depends on unique quantized vertices, faces, face groups, and fixed header data. In this snapshot, ID 6715's 16,896-byte entry and 1,257 faces are direct measurements; extrapolating a universal face cap from them is invalid.

`int16 / 128` constrains each vertex coordinate relative to its local model origin to about `±255.992m`; it does not impose a 255.99m spherical radius. A 256m horizontal tile centered on its pivot has `±128m` on each horizontal component and a 181.02m corner distance, so its horizontal components fit, but that alone says nothing about vertical extent, off-center pivots, or COL face count. Choose/recenter the vertical pivot to fit component bounds and check all three axes after quantization. The 6715 raw bound proves the current writer can silently clip one axis even though the nominal model is under the byte budget.

`LOD distance = 300` is not a general physics or collision-store unload radius. `DrawDistance` is per model and renderer/streamer decisions depend on the entity/camera distance, camera LOD multiplier, LOD relationship and model bound; COL data is loaded through the separate collision streaming path. The IDE's current near entries use 295 and LOD entries 1500, but those values do not prove that a nearby collision is guaranteed loaded everywhere or that a 256m tile remains continuously collidable at all camera/player positions. Test the actual near/LOD association and collision streaming in game before treating a distance as a safety guarantee.

The current SkyGfx config at `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\skygfx1.ini` has `ps2Modulate=0`, `dualPass=1`, `buildingPipe=PS2`, `detailMaps=1`, `doRadiosity=1`, and `disableGamma=1`; the `ps2ModulateBuilding=1` override is commented out. This supports no claim that the proposed prelight × tiled-texture output is already visually validated in the active build. RenderWare prelight and the GTA day/night extra-color path are separate concerns: standard PRELIT color data can be multiplied with a texture by a compatible pipeline, while day/night vertex data requires the expected plugin/pipeline. The local settings do not verify which DFF atomic pipeline is active in the shipped game. Test neutral diffuse textures first, then day/night interpolation, then colored albedo; inspect near/LOD handoff under the actual SkyGfx preset. In particular, a sampled BaseMap baked only into near prelight with grayscale LOD colors can cause a near/LOD tone pop, and a single planar projection stretches detail texture on steep cliffs.

## Primary source references and verification limits

- [Fastman92 limit-adjuster development INI](https://github.com/fastman92/fastman92_limit_adjuster/blob/master/fastman92%20limit%20adjuster/Dev%20INI%20files/fastman92limitAdjuster_GTASA_dev.ini): separate comments for single-COL byte size and LOD distance.
- [GTA reversed `FileLoader.cpp`](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/FileLoader.cpp#L2982-L3047): COL3 archive lookup by matching ID/name key, then fallback name lookup; [COL3 parsing](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/FileLoader.cpp#L3412-L3518) reads stored bounds and component arrays.
- [GTA reversed `Streaming.cpp`](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Streaming.cpp#L3110-L3128) shows COL loading as its own streaming model type; renderer/LOD-distance behavior is separate in [the model-distance logic](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Streaming.cpp#L3352-L3372).
- [GTA reversed custom-building renderer](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/Pipelines/CustomBuilding/CustomBuildingRenderer.cpp#L421-L447) initializes and attaches the day/night custom-building pipeline. This is source evidence of a GTA pipeline, not proof that the installed runtime preset selects it for these DFFs.

The game executable's actual treatment of the present 6715 clamped vertices, 6713 truncated COL name, streaming behavior, and SkyGfx rendering is **not proven**. No binary decompiler was available and none was installed; no game/build execution was performed.
