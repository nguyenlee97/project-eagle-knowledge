> Quy tắc phân bổ đã được người dùng cập nhật: Thích/Hơi thích dùng ở mọi vùng; Thích lặp nhiều hơn một chút; Bình thường chỉ dùng ở vùng không ưu tiên. Phân bổ và tỉ lệ sẽ xử lý sau. Các phép tính phủ slot trước đó là lịch sử theo giả định cũ, chưa phải kế hoạch phân bổ mới. [Policy hiện tại](evidence/skin-placement-policy.json).

# Skin selection pool

Built 2026-10-14 from the user's ratings export and the 2026-10-14 staged gallery manifest.

Ratings are joined to the gallery by index, then checked against group, legacy source name, target name, and DFF/TXD/pair byte sizes. Mapped rows are also checked against the referenced workbook's DFF and TXD mapping sheets. Each selected unique DFF+TXD pair was SHA-256 checked against the source files.

## Pool result

- Raw rated-selected rows before resource skip: 244.
- KEEP rating rows: 236 (like 25, somewhat 44, neutral 167).
- DROP rating rows: 1485 (explicit exclude 16; unrated and disallowed 1461; user resource-review skips 8).
- Unique selected byte pairs: 236; highest selected tier counts: {'like': 25, 'somewhat': 44, 'neutral': 167}.
- Unique selected-pair size: 453,767,939 bytes; selected-row copy size: 453,767,939 bytes.

`like` is preferred/common. `somewhat` and `neutral` are lower-priority/less-common. Any unrated row is DROP for this plan. An unrated duplicate does not expand the pool. Exact DFF+TXD hashes define a duplicate; source variants with different hashes stay separate.

Repeated rows for one exact pair retain all selected rating provenance, and the asset receives the highest selected tier. Explicit-exclude or unrated rows for a selected exact pair are recorded as contradictions on that asset; their ratings are not propagated. Historical names are provenance only and do not identify unique characters.

The JSON retains all 1,721 rating rows as KEEP/DROP records. DROP rows are logical tombstones only; no source file was deleted. Asset size, geometry, texture counts and warnings are inventory evidence, not runtime approval. This pool does not assign Eagle IDs from gallery names or workbook mappings.

Full row-level checks, assets, hashes, inventory, and provenance: [skin-selected-pool.json](evidence/skin-selected-pool.json).
