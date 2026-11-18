# Aether autoload compiler notes

## Portable compiler

The official Sanny Builder 4.2.0 Windows release ZIP is staged at `staging\project-eagle\aether-autoload\tools\SannyBuilder-v4.2.0`. It contains `sanny.exe` and compiler data directories; no installer was run. The downloaded archive SHA-256 is `4ACEB1C1E430E57BC57216FBE95A3EAC1829F2BD982BA19D99BB147CAA4B33E6`.

Compile a GTA San Andreas source file with:

```powershell
& 'C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\aether-autoload\tools\SannyBuilder-v4.2.0\sanny.exe' --no-splash --game sa --compile 'C:\path\script.txt' 'C:\path\script.cs'
```

Sanny Builder's CLI documentation defines `--compile <input> [output]`; `--game sa` selects San Andreas. A source beginning with `{$CLEO}` emits CLEO format and enables the CLEO extension. The staged `data\sa` has `SASCM.CLEO.ini`, `SASCM.CLEO+.ini`, and `opcodes.txt`. The extension files include `save_this_custom_script` (0A95), `does_file_exist` (0AAB), and other CLEO definitions. Opcode presence in compiler data is not evidence that a particular opcode is enabled by the installed game runtime or plugins.

## Local compile check

The exact command above successfully compiled a minimal source containing `{$CLEO}` and `0000:` into `probe.cs` (47 bytes; SHA-256 `63F4D54148BD3DD36B346B5585479E4150EE02AD491A73F95983F6C5D2B4CE1C`). This confirms the portable binary, CLI invocation, and CLEO output directive. It does not validate runtime behavior or the script's eventual opcodes in game.

## CLEO script startup and save behavior

CLEO 5's engine source scans the CLEO directory for `.cs`, `.cs3`, and `.cs4`, loads each custom script when game scripts begin, and registers it. Before discovery it loads per-save CLEO state; it applies saved thread state only when an entry with a matching code checksum exists. `save_this_custom_script` opts a thread into save-state persistence (locals and execution position); omitting it means the script is freshly loaded from its beginning on a new game or save load. This is appropriate for an autoload trigger that should run each session, but has not been tested in this game.

The existing local `.cleo.log` is historical, dated 2025-04-23/24. It identifies SA 1.0 US and includes an earlier custom-script listing and registration. The game was not running during this compiler work and was not launched.

## Primary references

- [Sanny Builder CLI](https://docs.sannybuilder.com/editor/cli)
- [Official Sanny Builder 4.2.0 release](https://github.com/sannybuilder/dev/releases/tag/v4.2.0)
- [Sanny Builder `$CLEO` directive](https://docs.sannybuilder.com/language/directives#cleo)
- [Official San Andreas opcode data](https://github.com/sannybuilder/data/tree/master/sa)
- [CLEO 5 README](https://github.com/cleolibrary/CLEO5/blob/master/README.md)
- [CLEO 5 script engine](https://github.com/cleolibrary/CLEO5/blob/master/source/CScriptEngine.cpp)
- [CLEO 5 Skin Selector example](https://github.com/cleolibrary/CLEO5/blob/master/examples/Skin_Selector.txt) — reference only; it uses save-state behavior and memory patches that should not be carried over without separate review.
