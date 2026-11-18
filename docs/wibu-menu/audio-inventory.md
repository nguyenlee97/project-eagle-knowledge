# Wibu menu audio inventory

Selected from existing files under `D:\Music`; original source files were only read. Staged files are byte-for-byte copies (SHA-256 verified). No generated music or format conversion was used.

All staged assets are MP3; menu plugin implementation confirmed MP3 support through the existing BASS runtime. Duration/codec/channel/rate values were read with `C:\PATH_Program\ffprobe.exe`.

| Staged file | Track / credit | Use | Duration | Codec | Channels | Sample rate | Size | SHA-256 | Source |
|---|---|---|---:|---|---:|---:|---:|---|---|
| `menu_default_a_day_in_mondstadt.mp3` | A Day in Mondstadt — Yu-Peng Chen | Default calm menu loop | 59.82s | mp3 | 2 | 44100 Hz | 1327216 bytes | `f0268223c536f54891b646b258e03f2b97dd079132e12cc68f41fdc2be7e4667` | `D:\Music\Genshin Impact OST Relaxing (complete)\Yu-Peng Chen - A Day in Mondstadt.mp3` |
| `menu_another_day_in_mondstadt.mp3` | Another Day in Mondstadt — Yu-Peng Chen | Menu alternate | 52.741s | mp3 | 2 | 44100 Hz | 1207973 bytes | `46428d2482893006979f1cb12fbf4268d1981a322e0754b516d5d134f06c6c29` | `D:\Music\Genshin Impact OST Relaxing (complete)\Yu-Peng Chen - Another Day in Mondstadt.mp3` |
| `menu_a_gentle_wind_blows_softly.mp3` | A Gentle Wind Blows Softly — HOYO-MiX | Menu alternate | 127.92s | mp3 | 2 | 48000 Hz | 3070700 bytes | `7bc3d97e32c8958e088f05f35ada790b5cde202ff64b3898c09d0c507f64035b` | `D:\Music\Genshin New Music\HOYO-MiX - A Gentle Wind Blows Softly.mp3` |
| `menu_a_sweet_dream_in_fontaine.mp3` | A Sweet Dream in Fontaine — HOYO-MiX | Menu alternate | 71.76s | mp3 | 2 | 48000 Hz | 1722860 bytes | `a504f59291859571b4516781898e238b98e50ed051cd0506dddd76bef4ec12a8` | `D:\Music\Genshin New Music\HOYO-MiX - A Sweet Dream in Fontaine.mp3` |
| `menu_as_the_soft_wind_blows.mp3` | As the Soft Wind Blows — HOYO-MiX | Menu alternate | 74.64s | mp3 | 2 | 48000 Hz | 1791980 bytes | `b9f1ef5715ee3b029f9d75d978502e1b97f6be2ead27f3a80842c5c3dbb21d4f` | `D:\Music\Genshin New Music\HOYO-MiX - As the Soft Wind Blows.mp3` |

Default selection: `menu_default_a_day_in_mondstadt.mp3` (A Day in Mondstadt). This is a calm, recognizable town exploration theme and suits a static main/pause menu. Other four tracks are menu selections.

