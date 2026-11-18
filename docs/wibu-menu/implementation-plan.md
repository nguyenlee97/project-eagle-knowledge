# Wibu menu — implementation scope

Authorized by user on 22/10/2026 after the menu concept discussion. Main game: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`. Gameplay-lab belongs to another stream and is outside this installation.

- First version: 23 single-character full menu covers, favorite/random-per-launch selection, a portrait in appropriate pause pages, short text greeting, and a configurable existing Genshin menu soundtrack from D:.
- Visual direction: approved flat 2D anime lineart/cel shadow, urban outfits and the existing white/black Wibu World wordmark. Cover artwork has no baked UI or lettering.
- A dedicated ASI will draw before native frontend options, retaining the native play/load/settings actions. Avoid map and control-binding pages; custom input is active only in its own menu panel.
- Hook compatibility follows the current executable identity and measured draw route from `renderer-audit.md`. Stage and validate before a scoped installation; preserve current core, loading artwork, skins, radio and gameplay mods.
- Audio is copied from existing D: MP3s. Default: A Day in Mondstadt; four alternatives are staged. No generated music or voice. Greeting is text in this version.
- Subtle native UI fades are in scope if safe; hand-animated character blinking/hair and per-page cast assignments remain later visual enhancements.
- Source art/prompts, native TXDs, source/build outputs, QA, backups, install manifest and a guarded rollback remain under `staging/project-eagle/wibu-menu`. User performs runtime testing; do not launch or control the game automatically.
