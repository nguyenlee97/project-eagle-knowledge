# RZL-Trainer player-model branch: static byte findings

Checked 13 October 2026 against the selected Project Eagle installation. This is read-only static analysis of `cleo\RZL-Trainer.cs` (2,723,721 bytes), `data\peds.ide`, and existing loader/CLEO logs. The game was not launched. The source decompiler did not produce a usable listing, so opcode interpretations below are limited to clear byte signatures and local opcode definitions.

## Special slot used by the ModLoader Actors branch

The RZL script contains this opcode sequence in the block that embeds the ModLoader scan path:

- `cleo\RZL-Trainer.cs +0x23BBDF`: opcode word `023C` (`load_special_character` / `load_special_actor`).
- `+0x23BC4C` and `+0x23BC5C`: embedded literals `modloader\RZL-Skin` and `*.dff`.
- `+0x23BDA8`: `023D 04 01`, the `has_special_character_loaded` check with literal slot `1`.
- `+0x23BE2C`: `0296 04 01`, the `unload_special_character` call with literal slot `1`.
- `+0x23C3E4`, `+0x23C7BA`, `+0x23CA97`, and `+0x23CE6D`: `09C7` (`set_player_model`) opcodes in this same code region. Each encodes model ID 290 as a 16-bit immediate (`05 22 01`, where `0x0122` is decimal 290); the player argument is a variable reference.

The local IDE maps special-character slot 1 to model ID 290 (`special01`) at `data\peds.ide:336`; slots 1–10 map to IDs 290–299. The loaded-status check, unload call, and four player-model changes all use slot1/model290 in this flow. This is strong evidence that RZL's ModLoader Actors flow occupies slot 1 / model 290. A separate autoload script intended to coexist with the trainer should use another slot, such as slot 10 / model 299. The scan does not decode the selected DFF basename or prove every execution path.

## Player-model rebuild and save behavior

The exact little-endian constant for `0x005A81E0` (the CLEO 5 example's `CClothes::ConstructPedModel()` patch target) does not occur in `RZL-Trainer.cs`. No `070D BUILD_PLAYER_MODEL` opcode occurs in the `+0x23B000`–`+0x23D000` actor branch. This supports only the narrow finding that the branch has no visible literal patch of that address and no explicit rebuild opcode; it does not rule out another patch target or computed pointer.

`0A8C`/`0A8D` memory-write/read opcodes occur in this general byte region, with variable pointer operands. Some nearby writes use small values `0x1B`–`0x1E` through that variable pointer; the target structure is unresolved without a working disassembly, so do not interpret these as player-rebuild protection or as proof there is none. `0A95` (`save_this_custom_script`) is present elsewhere in the trainer but absent from the inspected actor branch. That opcode concerns CLEO script thread state; the static scan does not establish whether the selected player model is written into a GTA save.

The embedded menu label `Normal Actors > 000_DEFAULT` is present in the trainer. Its intended reset effect remains unverified; do not treat it as proof that it restores CJ or preserves other player state.

## Log context and limits

The existing `cleo.log` records RZL-Trainer.cs registration on 13 October 2026 at 16:21 local time. The existing `modloader\modloader.log`, last written at 16:24 local time, reports no handler for `RZL-Skin\AETHER.dff` and `.txd`. These are startup-log observations, not proof of the later F2 selection result supplied by the user; RZL may load the assets through its own path. The user reports F2 selection is currently tested and working.

Still unresolved from static evidence: the exact asset-mount mechanism, the decoded model-name value, how RZL handles player rebuilds or clothing stats after `09C7`, whether it preserves the selected model across save/restart, and what `000_DEFAULT` does at runtime. Do not infer those from the opcode presence alone.
