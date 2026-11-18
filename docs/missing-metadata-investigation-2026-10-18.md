# Project Eagle missing metadata investigation

Read-only investigation of active individual-skin catalog rows carrying `missing_legacy_rating`, `missing_txd`, and `missing_source`, using the catalog and review snapshot dated 2026-10-18.

## Filter and outcome

The three tags match **27** rows. Six are excluded by `reviews.excluded=true`, leaving **21 active rows**. No matching row is excluded by size policy: all six review exclusions have `autoSizePolicy.action=null`, and no active row has `policyHold=true` or a size-policy exclusion.

All 21 active rows currently have `series=[]`, `sources=[]`, `legacyRating=null`, and `txdPath=null`. The catalog already records the FadXploit archive name for 20 rows; the Promeia row has `archiveNames=[]` despite its inspection containing the exact archive path and member name.

Exact joins from inspector archive filename **and SHA-256** to the FadXploit source summary recover source records for **20** rows. **19** also have consistent archive member identity and franchise; **1** has archive provenance only because its internal name conflicts with the page subject. Seven rows have explicit source ratings (`like` → `like`; `somewhat` → `slight`). Thirteen exact archive records have `rating_pending`.

## Per-row evidence and proposed metadata

Every full key and current field is recorded in the machine-readable JSON. This table shows each active ID, current display name, internal DFF member filename, source URL or withheld candidate, series candidate, source-derived legacy rating, candidate TXD member names, and archive SHA evidence. Full candidate TXD paths and hashes are in the JSON.

| ID | Current display name | DFF member | Source URL | Series | Legacy rating | TXD candidate member(s) and archive evidence |
|---:|---|---|---|---|---|---|
| 2747 | A74 Charlotte | `A74_Charlotte.dff` | [archive origin only](https://fadxploit.my.id/gtasa/burnice-white-zenless-zone-zero/) | — | pending | `A74_Charlotte.txd`; `FadXploit_Burnice White.rar` SHA `b6e2e36786fe` → FAD-30/HSR-ZZZ-FAD-c8cc24595b474012; ambiguous_txd; member `A74_Charlotte.dff` conflicts with `Burnice White`, URL only |
| 2750 | Zani 2 | `Zani_2.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/zani-wuthering-waves/) | Wuthering Waves | slight | `Zani.txd`, `Zani_2.txd`; `FadXploit Zani Wuthering Waves 1.0.zip` SHA `82cfce139996` → FAD-18/f630e9556fe899a8; ambiguous_txd |
| 2752 | Akeha SA | `Akeha_SA.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/akeha-summer-assassin-nier-reincarnation/) | NieR Reincarnation | slight | `Akeha_SA.txd`, `Akeha_SA2.txd`; `FadXploit_Akeha_Summer_Assassin_2.0.7z` SHA `cb977a4b5ada` → FAD-07/491e995ab93e0f65; ambiguous_txd |
| 2757 | Tingyun HSR | `Tingyun_HSR.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tingyun-honkai-star-rail/) | Honkai: Star Rail | pending | `Tingyun_HSR.txd`, `Tingyun_HSR2.txd`; `FadXploit Tingyun HSR 1.0.7z` SHA `5d1551bee28d` → FAD-29/HSR-ZZZ-FAD-e5cb09e10aee2eda; ambiguous_txd |
| 2761 | Yanagi2 ZZZ | `Yanagi2_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yanagi2_ZZZ.txd`, `Yanagi_ZZZ.txd`; `FadXploit Tsukishiro Yanagi 1.0 + (Breast Physics DFF).zip` SHA `108eb2bb8158` → FAD-31/HSR-ZZZ-FAD-17ddbc858e448907; ambiguous_txd |
| 2763 | Nefer 2 | `Nefer_2.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/nefer-genshin-impact/) | Genshin Impact | like | `Nefer.txd`, `Nefer_2.txd`; `FadXploit_Nefer_1.0.zip` SHA `1ce39f62c56a` → FAD-23/GEN-FAD-84be8950c5eb5812; ambiguous_txd |
| 2770 | Promeia | `Promeia.dff` | [candidate only; withheld](https://fadxploit.my.id/gtasa/promeia-zenless-zone-zero/) | Zenless Zone Zero | pending | none; `FadXploit Promelija.7z` SHA `10e692b96ebe`; no source-manifest filename/SHA match; missing_txd |
| 2772 | Cherno TW | `Cherno_TW.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/cherno-enigma-tidal-whispers-snowbreak-containment-zone/) | Snowbreak: Containment Zone | slight | `Cherno_TW.txd`, `Cherno_TW.txd`; `FadXploit Cherno - Enigma Tidal Whispers 1.0 + (Breast Physics DFF).zip` SHA `d1003004485c` → FAD-10/baa54cb0cd0fb6ea; ambiguous_txd |
| 2774 | Nefer | `Nefer.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/nefer-genshin-impact/) | Genshin Impact | like | `Nefer.txd`, `Nefer_2.txd`; `FadXploit_Nefer_1.0.zip` SHA `1ce39f62c56a` → FAD-23/GEN-FAD-84be8950c5eb5812; ambiguous_txd |
| 2779 | Zani | `Zani.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/zani-wuthering-waves/) | Wuthering Waves | slight | `Zani.txd`, `Zani_2.txd`; `FadXploit Zani Wuthering Waves 1.0.zip` SHA `82cfce139996` → FAD-18/f630e9556fe899a8; ambiguous_txd |
| 2780 | Ellen ZZZ 2 | `Ellen_ZZZ_2.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/ellen-joe-zenless-zone-zero/) | Zenless Zone Zero | pending | `Ellen_ZZZ.txd`, `Ellen_ZZZ_2.txd`; `FadXploit_Ellen_ZZZ_1.0.zip` SHA `6a5afecfa1dc` → FAD-30/HSR-ZZZ-FAD-8b7aff890b7ee58f; ambiguous_txd |
| 2783 | Yanagi ZZZ | `Yanagi_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yanagi2_ZZZ.txd`, `Yanagi_ZZZ.txd`; `FadXploit Tsukishiro Yanagi 1.0 + (Breast Physics DFF).zip` SHA `108eb2bb8158` → FAD-31/HSR-ZZZ-FAD-17ddbc858e448907; ambiguous_txd |
| 2792 | Tingyun HSR2 | `Tingyun_HSR2.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tingyun-honkai-star-rail/) | Honkai: Star Rail | pending | `Tingyun_HSR.txd`, `Tingyun_HSR2.txd`; `FadXploit Tingyun HSR 1.0.7z` SHA `5d1551bee28d` → FAD-29/HSR-ZZZ-FAD-e5cb09e10aee2eda; ambiguous_txd |
| 2793 | Akeha SA2 | `Akeha_SA2.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/akeha-summer-assassin-nier-reincarnation/) | NieR Reincarnation | slight | `Akeha_SA.txd`, `Akeha_SA2.txd`; `FadXploit_Akeha_Summer_Assassin_2.0.7z` SHA `cb977a4b5ada` → FAD-07/491e995ab93e0f65; ambiguous_txd |
| 2797 | Yanagi2 ZZZ | `Yanagi2_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yanagi2_ZZZ.txd`, `Yanagi_ZZZ.txd`; `FadXploit Tsukishiro Yanagi 1.0 + (Breast Physics DFF).zip` SHA `108eb2bb8158` → FAD-31/HSR-ZZZ-FAD-17ddbc858e448907; ambiguous_txd |
| 2806 | Yanagi ZZZ | `Yanagi_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yanagi2_ZZZ.txd`, `Yanagi_ZZZ.txd`; `FadXploit Tsukishiro Yanagi 1.0 + (Breast Physics DFF).zip` SHA `108eb2bb8158` → FAD-31/HSR-ZZZ-FAD-17ddbc858e448907; ambiguous_txd |
| 2807 | Yanagi2 ZZZ | `Yanagi2_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yanagi2_ZZZ.txd`, `Yanagi_ZZZ.txd`; `FadXploit Tsukishiro Yanagi 1.0 + (Breast Physics DFF).zip` SHA `108eb2bb8158` → FAD-31/HSR-ZZZ-FAD-17ddbc858e448907; ambiguous_txd |
| 2809 | Yuzuha 2 | `Yuzuha_2.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/ukinami-yuzuha-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yuzuha.txd`, `Yuzuha_2.txd`, `Yuzuha.txd`, `Yuzuha_2.txd`; `FadXploit_Ukinami_Yuzuha_1.0.zip` SHA `e4029e2a2baf` → FAD-31/HSR-ZZZ-FAD-8c79d987f5131c07; ambiguous_txd |
| 2818 | Ellen ZZZ | `Ellen_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/ellen-joe-zenless-zone-zero/) | Zenless Zone Zero | pending | `Ellen_ZZZ.txd`, `Ellen_ZZZ_2.txd`; `FadXploit_Ellen_ZZZ_1.0.zip` SHA `6a5afecfa1dc` → FAD-30/HSR-ZZZ-FAD-8b7aff890b7ee58f; ambiguous_txd |
| 2819 | Yanagi ZZZ | `Yanagi_ZZZ.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yanagi2_ZZZ.txd`, `Yanagi_ZZZ.txd`; `FadXploit Tsukishiro Yanagi 1.0 + (Breast Physics DFF).zip` SHA `108eb2bb8158` → FAD-31/HSR-ZZZ-FAD-17ddbc858e448907; ambiguous_txd |
| 2821 | Yuzuha | `Yuzuha.dff` | [FadXploit source](https://fadxploit.my.id/gtasa/ukinami-yuzuha-zenless-zone-zero/) | Zenless Zone Zero | pending | `Yuzuha.txd`, `Yuzuha_2.txd`, `Yuzuha.txd`, `Yuzuha_2.txd`; `FadXploit_Ukinami_Yuzuha_1.0.zip` SHA `e4029e2a2baf` → FAD-31/HSR-ZZZ-FAD-8c79d987f5131c07; ambiguous_txd |

Explicit source ratings occur on **2750 Zani 2**, **2752 Akeha SA**, **2763 Nefer 2**, **2772 Cherno TW**, **2774 Nefer**, **2779 Zani**, and **2793 Akeha SA2**. Zani, Akeha, and Cherno have source rating `somewhat` (normalize to `slight`); Nefer has `like` (preserve as `like`).

The 13 archive-linked rows with `rating_pending` are IDs 2747, 2757, 2761, 2780, 2783, 2792, 2797, 2806, 2807, 2809, 2818, 2819, and 2821. The 12 identity-matched rows among them can receive source URL and series, with no rating. ID 2821 currently has `reviews.rating="like"`, but its source record says `rating_pending`, so its proposed legacy rating remains empty.

## Why the catalog omitted these fields

`enrich_catalog.py` creates `missing_source` when assembled `info.sources` is empty (line 223). It joins the download audit on exact DFF/TXD pair IDs; these keys are `unpaired-dff:<DFF SHA-256>`, so they cannot join paired-pair records. Additional inspection joins also use `pairId` (lines 296–306 and 453). The source-path fallback recognizes archive IDs under `archives\<16-hex-id>\...` and `jobs\GEN-FAD-*\...` (line 181), then derives source job IDs from original paths (lines 479–512). The target paths instead sit under `creators\results\HSR-ZZZ-FAD-*`, `creators\results\GEN-FAD-*`, `creators\manual-downloads\FAD-*`, and one `numbered-skins\inspections` folder, so the fallback does not link these source records. The enrichment inputs do not include the FadXploit summary. None of the four configured member-association files has an association row for these source jobs.

The staging path in inspection reports is a Windows junction to `Skin Library/Project Eagle/download-run-2026-10-15`, resolving to the same tree. For 20 rows, archive name and local SHA-256 match between inspection and source summary. The source summary has no published public archive hash, so this confirms the local source-manifest join only.

## Exceptions and limits

ID **2747 A74 Charlotte** is an exact archive-origin match to `FadXploit_Burnice White.rar` (local archive SHA matches in both records), so the Burnice page URL can be recorded with archive-only basis. The inspected internal member is `A74_Charlotte.dff`, while the source record identifies Burnice White / Zenless Zone Zero. Do not copy the Burnice character, series, or rating onto this row. The FAD-30 validation note calls this RAR a secondary candidate and records no paired model/texture resources.

ID **2770 Promeia** comes from a separate user-downloaded `FadXploit Promelija.7z` archive; inspection confirms exact member `Promeia.dff` and no TXD. A FadXploit Promeia page exists and its source row says Zenless Zone Zero / `rating_pending`, but it has no archive record; the FAD-30 validation record says `missing_after_bounded_filename_scan`. The archive label and internal member make that page a strong candidate, but there is no source-to-archive manifest link. The proposed exact patch adds only the archive name; URL, series, and legacy rating remain unassigned.

Source `rating_pending` supplies no legacy rating. Current `reviews.rating` is separate review data: Nefer is `love` while its source rating is `like`; Yuzuha is `like` while its source rating is `rating_pending`. Do not copy the review value into `legacyRating`.

All 20 archive-linked DFFs have inspector reason `ambiguous_txd` with one or more candidate textures. Promeia alone has reason `missing_txd` with zero candidates. The JSON preserves candidate TXD paths, logical names, hashes, and sizes per row. The metadata proposal does not repair pairing or choose a TXD; `missing_txd` and `ambiguous_pairing` remain.

## Excluded matches

These six rows carry the three tags but are outside the active set because `reviews.excluded=true`. Their review records have no size-policy exclusion (`autoSizePolicy.action=null`).

| ID | Name | Key |
|---:|---|---|
| 2745 | Kaneki S1 | `unpaired-dff:1b34b1465b7786c390243efb2eb611e153f8867afad1ecd0ed13e5d2f10c92d6` |
| 2756 | Kaneki S2 | `unpaired-dff:35dfce9f59372f3e86e80a18cc516ffda9af4d92bedf7e187ab47cd2a8668355` |
| 2776 | Cherno TW | `unpaired-dff:6d138822bc58d41241db64dff3a15503d71c1d9999f59c9bcc712beb5db13303` |
| 2804 | Kaneki S1 2 | `unpaired-dff:b1c73030b0f224669093956c876bcda6cc89b13768e8f4cc498f35aa021d69f0` |
| 2805 | Cherno TW | `unpaired-dff:ba85f1e4ce521085b355b7f066b0a6a10231a06239bbc082a211bbcfd8fa40cd` |
| 2813 | Kaneki S2 2 | `unpaired-dff:d1a9c75689dcac0b3e02076a54ce6236f92a1d773b5a4ca71200935bc3e01495` |

## Evidence files

- Catalog: `Skin Library/Project Eagle/numbered-skins/catalog.json` (updated 2026-10-18).
- Reviews: `Skin Library/Project Eagle/numbered-skins/reviews.json` (created 2026-10-18).
- Enrichment behavior: `tools/skin-viewer/enrich_catalog.py`.
- Source archive, series, and rating records: `Skin Library/Project Eagle/download-run-2026-10-15/fadxploit-summary-2026-10-18.json`.
- Burnice and Promeia validation details: `Skin Library/Project Eagle/download-run-2026-10-15/creators/manual-downloads/fad-30-download-validation-2026-10-17.md`.
- Full row fields and additive exact-key proposals: `docs/project-eagle/missing-metadata-investigation-2026-10-18.json`.

Only these two documentation artifacts were written. `catalog.json`, `reviews.json`, source code, archives, and extracted assets were not modified.
