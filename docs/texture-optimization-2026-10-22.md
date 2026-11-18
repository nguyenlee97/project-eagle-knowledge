# Tối ưu texture mở rộng — 22/10/2026

Đã xử lý 578 bản ghi / 322 TXD khác nhau; thêm 437 phiên bản tối ưu vào viewer (416 item khi lọc Tối ưu TXD; một item có thể chứa nhiều phiên bản).

Các cặp có bản tối ưu: 8.13 → 2.87 GiB (giảm 64.71%). Đây là dung lượng của các cặp skin thay thế khi dùng bản tối ưu; kho vẫn giữ bản gốc và có thêm bản mới. Không phải dung lượng đã dọn khỏi ổ C hay phép đo RAM/FPS.

## Kết quả

- Đã thêm bản tối ưu: **407**
- Đã nén sẵn, giữ nguyên: **126**
- Giữ gốc, chưa qua kiểm tra parser: **5**
- Giữ gốc, cần xem lại chất lượng: **8**
- Bản tối ưu của đợt này đã được đối chiếu lại: **30**
- Không giảm thêm, giữ nguyên: **2**

## Backup và phạm vi

Backup tăng thêm ở `D:\Skin Backup\Optimization-2026-10-22`. Đã đọc/đối chiếu hash 1138 đường dẫn nguồn; dùng lại 1065 đường dẫn từ bản backup cũ, chép mới 73 object (496.75 MiB). Bản tối ưu: 199 TXD (888.30 MiB), đã kiểm hash khi sao lưu. Snapshot metadata trước/sau và manifest liên kết nguồn đều nằm trong backup. Snapshot 18/10 được giữ nguyên.

Mọi DFF/TXD gốc, điểm chấm cũ, 10 mapping thử và IMG đang cài giữ nguyên. Không tối ưu mẫu Rất thích hoặc bị loại. Chỉ nén raster chưa nén: DXT1 cho alpha hoàn toàn opaque, DXT5 nếu có alpha; giữ độ phân giải, tên, thứ tự texture và số mip. Những mip phụ của raster chuyển đổi được texconv tạo lại. Texture đã DXT không nén lần nữa. Phần đệm zero hợp lệ được giữ nguyên.

Bản ghi dùng chung TXD chỉ nén một lần. Mỗi cặp DFF vẫn được parser đọc cùng bản TXD mới, đối chiếu hash DFF và danh sách texture đã kiểm tra trước/sau. Các bản có RGB PSNR dưới 32 dB hoặc alpha vượt ngưỡng kiểm tra được giữ lại trong staging, chưa thêm vào viewer. Chỉ số ảnh không thay thế đánh giá trực quan hoặc kiểm thử trong game.

## Sử dụng trong viewer

Xóa bộ lọc cũ, chọn Nhóm cũ → **Tối ưu TXD**; Mapping phiên bản → **Tất cả** để thấy các bản chưa gán. Dropdown Phiên bản có bản gốc và bản “Tối ưu DXT • giữ độ phân giải • 22/10”. Nhãn **Đã nén TXD** cho biết đã xử lý; cờ phân tích cũ có thể vẫn còn vì được kế thừa hoặc mẫu còn >10 MiB. Bạn tự chọn bản để đưa vào pool/gán NPC, rồi build khi muốn áp dụng. Mười skin đã thử trong game vẫn là 10 mapping trước đó.

## Danh sách

| Skin gốc | Kết quả | MiB trước → sau | ID bản tối ưu | Ghi chú |
|---|---|---:|---:|---|
| #12 Claret Flint | Đã thêm bản tối ưu | 25.24 → 6.56 | 3259 |  |
| #16 Cartethyia | Đã thêm bản tối ưu | 31.92 → 11.42 | 3260 |  |
| #19 Castorice | Đã thêm bản tối ưu | 34.81 → 8.97 | 3261 |  |
| #26 W | Đã nén sẵn, giữ nguyên | 21.16 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #33 Coralie BFDD 2 | Đã thêm bản tối ưu | 17.19 → 5.45 | 3262 |  |
| #35 Vodka | Đã thêm bản tối ưu | 12.68 → 4.08 | 3263 |  |
| #42 Fleurdelys | Đã thêm bản tối ưu | 25.36 → 6.69 | 3264 |  |
| #45 Len VS | Đã thêm bản tối ưu | 12.45 → 3.12 | 3265 |  |
| #53 Cyrene | Đã thêm bản tối ưu | 33.34 → 17.01 | 3266 |  |
| #64 Tokai Teio | Đã thêm bản tối ưu | 13.89 → 3.39 | 3267 |  |
| #65 BA Hiyori SS | Đã thêm bản tối ưu | 11.55 → 6.88 | 3268 |  |
| #74 Sparkle HI3 | Đã thêm bản tối ưu | 15.51 → 4.14 | 3269 |  |
| #75 Evanescia 2 | Đã thêm bản tối ưu | 23.79 → 6.29 | 3270 |  |
| #80 The Herta | Đã thêm bản tối ưu | 20.40 → 6.40 | 3271 |  |
| #83 Phoebe | Đã thêm bản tối ưu | 27.64 → 10.14 | 3272 |  |
| #91 Fischl | Đã nén sẵn, giữ nguyên | 12.04 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #95 Yuji Itadori | Đã nén sẵn, giữ nguyên | 22.96 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #114 M035PStyleIS | Đã thêm bản tối ưu | 17.87 → 15.36 | 3273 |  |
| #116 Haru Urara | Đã thêm bản tối ưu | 13.80 → 3.30 | 3274 |  |
| #117 Otogi | Đã nén sẵn, giữ nguyên | 10.75 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #122 Kuki Shinobu | Đã thêm bản tối ưu | 11.77 → 5.70 | 3275 |  |
| #130 Dehya | Đã nén sẵn, giữ nguyên | 10.28 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #131 Megumi Fushiguro | Đã nén sẵn, giữ nguyên | 22.45 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #134 Chixia | Đã nén sẵn, giữ nguyên | 20.44 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #164 Cheeta Racing | Đã thêm bản tối ưu | 24.09 → 6.89 | 3276 |  |
| #167 Gorushi | Đã thêm bản tối ưu | 13.53 → 3.03 | 3277 |  |
| #177 H Baelz | Đã thêm bản tối ưu | 25.87 → 8.37 | 3278 |  |
| #185 Lumi | Đã thêm bản tối ưu | 22.37 → 9.46 | 3279 |  |
| #192 Arle CS | Đã thêm bản tối ưu | 23.30 → 6.97 | 3280 |  |
| #199 Miku 25Ji | Đã thêm bản tối ưu | 13.19 → 3.27 | 3281 |  |
| #203 Lumi | Đã thêm bản tối ưu | 22.37 → 9.46 | 3282 |  |
| #206 Lingsha | Đã thêm bản tối ưu | 24.07 → 5.41 | 3283 |  |
| #215 Suzuya re | Đã thêm bản tối ưu | 13.19 → 2.69 | 3284 |  |
| #224 Yuji Itadori | Đã nén sẵn, giữ nguyên | 22.80 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #234 Tamamo | Đã thêm bản tối ưu | 13.19 → 4.58 | 3285 |  |
| #237 Escoffier | Đã thêm bản tối ưu | 27.55 → 5.88 | 3286 |  |
| #243 Coralie BFDD | Đã thêm bản tối ưu | 18.04 → 6.30 | 3287 |  |
| #244 Mavuika | Đã thêm bản tối ưu | 14.35 → 5.02 | 3288 |  |
| #250 Belle | Đã thêm bản tối ưu | 13.08 → 2.58 | 3289 |  |
| #259 Skirk 01 | Đã thêm bản tối ưu | 24.40 → 5.73 | 3290 |  |
| #270 Sasaki | Đã thêm bản tối ưu | 13.15 → 2.65 | 3291 |  |
| #272 Daiwa Scarlet | Đã thêm bản tối ưu | 12.89 → 4.62 | 3292 |  |
| #273 Jahoda | Đã thêm bản tối ưu | 19.78 → 8.12 | 3293 |  |
| #276 Ena 25ji | Đã thêm bản tối ưu | 13.10 → 3.19 | 3294 |  |
| #279 BA Kazusa | Đã thêm bản tối ưu | 14.67 → 5.33 | 3295 |  |
| #284 Skirk 01 | Đã thêm bản tối ưu | 24.04 → 5.38 | 3296 |  |
| #295 Cheeta Racing | Đã thêm bản tối ưu | 23.78 → 6.57 | 3297 |  |
| #303 Carlotta | Đã thêm bản tối ưu | 10.46 → 5.79 | 3298 |  |
| #312 Sparkle HI3 | Đã thêm bản tối ưu | 15.80 → 4.42 | 3299 |  |
| #326 M001Hatsune | Đã thêm bản tối ưu | 32.15 → 23.97 | 3300 |  |
| #328 Lumine | Đã thêm bản tối ưu | 27.26 → 13.19 | 3301 |  |
| #332 Esper Zero | Đã thêm bản tối ưu | 30.48 → 11.81 | 3302 |  |
| #335 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 19.82 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #336 Jetavie SS | Đã thêm bản tối ưu | 23.55 → 6.05 | 3303 |  |
| #337 Mita | Đã thêm bản tối ưu | 14.59 → 5.26 | 3304 |  |
| #352 Texas | Đã nén sẵn, giữ nguyên | 10.81 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #354 Nekomiya Mana | Đã nén sẵn, giữ nguyên | 27.44 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #358 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 19.80 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #363 Narita Top Road | Đã thêm bản tối ưu | 18.61 → 4.41 | 3305 |  |
| #370 Rappa HSR | Đã thêm bản tối ưu | 15.34 → 4.84 | 3306 |  |
| #374 Satono Diamond | Đã thêm bản tối ưu | 18.64 → 4.44 | 3307 |  |
| #378 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.88 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #379 Hysilens | Đã thêm bản tối ưu | 29.40 → 10.71 | 3308 |  |
| #381 Silver Wolf 999 | Đã thêm bản tối ưu | 30.64 → 13.06 | 3309 |  |
| #394 Bakushin | Đã thêm bản tối ưu | 13.75 → 3.25 | 3310 |  |
| #400 Li Sushang PS | Đã thêm bản tối ưu | 19.78 → 4.91 | 3311 |  |
| #405 Hyacine WCS | Đã thêm bản tối ưu | 28.36 → 9.68 | 3312 |  |
| #406 ManCafe | Đã thêm bản tối ưu | 12.54 → 3.94 | 3313 |  |
| #410 Mita Kind | Đã thêm bản tối ưu | 23.72 → 5.05 | 3314 |  |
| #411 Karenina E | Đã thêm bản tối ưu | 12.35 → 4.47 | 3315 |  |
| #420 Andoris | Đã thêm bản tối ưu | 13.53 → 5.36 | 3316 |  |
| #429 BA Asuna | Đã thêm bản tối ưu | 22.71 → 13.37 | 3317 |  |
| #432 Ineffa | Đã thêm bản tối ưu | 18.72 → 4.72 | 3318 |  |
| #437 Special Week | Đã thêm bản tối ưu | 13.13 → 4.52 | 3319 |  |
| #438 Gold Ship SS | Đã thêm bản tối ưu | 15.49 → 7.11 | 3320 |  |
| #439 Len VS | Đã thêm bản tối ưu | 12.57 → 3.23 | 3321 |  |
| #461 Hyacine WCS | Đã thêm bản tối ưu | 28.36 → 9.68 | 3322 |  |
| #467 Silver Wolf 999 | Đã thêm bản tối ưu | 30.64 → 13.06 | 3323 |  |
| #470 Admire Vega | Đã thêm bản tối ưu | 14.50 → 3.29 | 3324 |  |
| #479 Roxy Ifrita P | Đã thêm bản tối ưu | 18.68 → 4.66 | 3325 |  |
| #480 Noelle | Đã nén sẵn, giữ nguyên | 11.22 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #493 Evanescia LB | Đã thêm bản tối ưu | 28.24 → 9.56 | 3326 |  |
| #496 Cartethyia | Đã thêm bản tối ưu | 31.15 → 10.65 | 3327 |  |
| #497 Mita Cappie | Đã thêm bản tối ưu | 15.90 → 6.57 | 3328 |  |
| #509 Helia SP | Đã thêm bản tối ưu | 19.95 → 4.73 | 3329 |  |
| #512 Hyacine | Đã thêm bản tối ưu | 24.19 → 5.53 | 3330 |  |
| #529 Nefer | Đã thêm bản tối ưu | 15.16 → 4.66 | 3331 |  |
| #534 Evernight | Đã thêm bản tối ưu | 24.69 → 7.19 | 3332 |  |
| #542 Rice Shower | Đã thêm bản tối ưu | 14.20 → 3.26 | 3333 |  |
| #552 Mayano Top Gun | Giữ gốc, chưa qua kiểm tra parser | 19.02 → giữ gốc | — | Tên texture nội bộ bị lặp (tex_tail0001_00_1024_diff); parser nhập từ chối nên giữ gốc. Không kết luận skin gốc hỏng. |
| #559 Mita Kind | Đã thêm bản tối ưu | 23.48 → 4.82 | 3334 |  |
| #560 Yuji Itadori | Đã nén sẵn, giữ nguyên | 22.70 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #572 M001Hatsune | Đã thêm bản tối ưu | 32.12 → 23.94 | 3335 |  |
| #576 Grace Howard — GTA VC model | Đã nén sẵn, giữ nguyên | 11.15 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #578 Phoebe | Đã thêm bản tối ưu | 26.20 → 8.70 | 3336 |  |
| #579 Cerydra | Đã thêm bản tối ưu | 26.61 → 10.26 | 3337 |  |
| #587 Mafuyu 25Ji | Đã thêm bản tối ưu | 13.40 → 3.19 | 3338 |  |
| #592 Mayano | Đã thêm bản tối ưu | 11.46 → 2.85 | 3339 |  |
| #594 Mizuki 25Ji | Đã thêm bản tối ưu | 13.32 → 3.40 | 3340 |  |
| #599 Frieren | Giữ gốc, chưa qua kiểm tra parser | 11.56 → giữ gốc | — | Tên texture nội bộ bị lặp (fadxploit_base_outline); parser nhập từ chối nên giữ gốc. Không kết luận skin gốc hỏng. |
| #615 Rapi | Đã nén sẵn, giữ nguyên | 11.88 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #616 Satoru Gojo | Đã nén sẵn, giữ nguyên | 38.65 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #621 Special Week | Đã thêm bản tối ưu | 11.69 → 3.09 | 3341 |  |
| #627 Hyacine WCS | Đã thêm bản tối ưu | 27.57 → 8.89 | 3342 |  |
| #629 Aqua | Đã nén sẵn, giữ nguyên | 23.98 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #631 Grace Howard | Đã nén sẵn, giữ nguyên | 11.15 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #632 Tamamo | Đã thêm bản tối ưu | 11.67 → 3.06 | 3343 |  |
| #637 BA Hiyori SS | Đã thêm bản tối ưu | 12.19 → 7.52 | 3344 |  |
| #644 Mihono Bourbon | Đã thêm bản tối ưu | 12.89 → 4.29 | 3345 |  |
| #648 Sparkle HSR | Đã thêm bản tối ưu | 14.15 → 7.15 | 3346 |  |
| #650 Mudrock | Đã nén sẵn, giữ nguyên | 12.83 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #653 Suzuya re | Đã thêm bản tối ưu | 13.12 → 2.62 | 3347 |  |
| #654 Roxy Ifrita P | Đã thêm bản tối ưu | 18.68 → 4.66 | 3348 |  |
| #657 Kanata | Đã thêm bản tối ưu | 31.31 → 9.15 | 3349 |  |
| #661 W | Đã nén sẵn, giữ nguyên | 21.25 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #663 Robin S | Đã thêm bản tối ưu | 25.04 → 10.97 | 3350 |  |
| #670 Esper Zero | Đã thêm bản tối ưu | 28.36 → 9.70 | 3351 |  |
| #671 Karenina E | Đã thêm bản tối ưu | 12.29 → 4.41 | 3352 |  |
| #673 Gorushi | Đã thêm bản tối ưu | 13.66 → 3.16 | 3353 |  |
| #675 Shenhe FD | Đã thêm bản tối ưu | 14.10 → 3.60 | 3354 |  |
| #683 Astra Yao ZZZ | Đã thêm bản tối ưu | 18.81 → 4.81 | 3355 |  |
| #686 Takion | Đã thêm bản tối ưu | 14.05 → 3.11 | 3356 |  |
| #691 Trigger | Đã thêm bản tối ưu | 14.22 → 3.72 | 3357 |  |
| #693 Cissia | Đã thêm bản tối ưu | 24.90 → 7.35 | 3358 |  |
| #696 QingYi | Đã nén sẵn, giữ nguyên | 12.05 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #697 Sparkle HI3 | Đã thêm bản tối ưu | 15.51 → 4.14 | 3359 |  |
| #710 Miku BA | Đã thêm bản tối ưu | 23.62 → 18.69 | 3360 |  |
| #716 Seto Kaiba | Đã nén sẵn, giữ nguyên | 11.76 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #725 Zani 2 | Đã thêm bản tối ưu | 20.09 → 6.09 | 3361 |  |
| #727 Suzuka | Đã thêm bản tối ưu | 12.77 → 4.17 | 3362 |  |
| #731 Cheeta | Đã thêm bản tối ưu | 21.41 → 5.37 | 3363 |  |
| #740 Vesna | Đã thêm bản tối ưu | 32.47 → 18.45 | 3364 |  |
| #746 Tokai Teio | Đã thêm bản tối ưu | 14.05 → 3.55 | 3365 |  |
| #772 Usada Pekora | Đã nén sẵn, giữ nguyên | 47.29 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #784 Nicole Demara | Đã thêm bản tối ưu | 14.55 → 3.98 | 3366 |  |
| #793 Lauma | Đã thêm bản tối ưu | 17.15 → 5.48 | 3367 |  |
| #803 Cerydra | Đã thêm bản tối ưu | 26.61 → 10.26 | 3368 |  |
| #814 Chasca | Đã thêm bản tối ưu | 10.32 → 5.65 | 3369 |  |
| #818 Frieren | Giữ gốc, chưa qua kiểm tra parser | 11.43 → giữ gốc | — | Tên texture nội bộ bị lặp (fadxploit_base_outline); parser nhập từ chối nên giữ gốc. Không kết luận skin gốc hỏng. |
| #819 Nicole Demara | Đã thêm bản tối ưu | 14.55 → 3.98 | 3370 |  |
| #830 Hatsune Miku Black Top | Đã thêm bản tối ưu | 20.04 → 16.36 | 3371 |  |
| #834 BA Asuna | Đã thêm bản tối ưu | 23.29 → 13.95 | 3372 |  |
| #836 Takion | Đã thêm bản tối ưu | 14.20 → 3.26 | 3373 |  |
| #842 Kaoruko Hanayagi | Giữ gốc, cần xem lại chất lượng | 20.43 → giữ gốc | — | eyebrows: RGB PSNR 23.87 dB |
| #843 MEIKO | Giữ gốc, cần xem lại chất lượng | 13.27 → giữ gốc | — | 33920_n: RGB PSNR 31.52 dB |
| #847 Vesna | Đã thêm bản tối ưu | 32.46 → 18.44 | 3374 |  |
| #848 The Herta | Đã thêm bản tối ưu | 20.82 → 6.82 | 3375 |  |
| #851 Aether | Đã thêm bản tối ưu | 14.65 → 3.71 | 3376 |  |
| #853 Trigger | Đã thêm bản tối ưu | 14.48 → 3.98 | 3377 |  |
| #855 Suguru Geto | Đã nén sẵn, giữ nguyên | 25.10 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #860 Miku WxS | Đã thêm bản tối ưu | 14.41 → 3.33 | 3378 |  |
| #861 Special Week SS | Đã thêm bản tối ưu | 14.05 → 5.88 | 3379 |  |
| #863 Columbina | Đã thêm bản tối ưu | 22.89 → 7.72 | 3380 |  |
| #866 Vivian | Đã nén sẵn, giữ nguyên | 17.53 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #870 Klukai | Đã thêm bản tối ưu | 23.69 → 6.19 | 3381 |  |
| #871 Ch'en | Đã nén sẵn, giữ nguyên | 28.93 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #889 Escoffier | Đã thêm bản tối ưu | 27.93 → 6.27 | 3382 |  |
| #890 Female Traveler (Lumine) | Đã nén sẵn, giữ nguyên | 11.03 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #906 Mita Crazy | Đã thêm bản tối ưu | 18.96 → 4.96 | 3383 |  |
| #907 Tanjiro Kamado | Đã nén sẵn, giữ nguyên | 11.23 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #910 Li Sushang PS | Đã thêm bản tối ưu | 20.14 → 5.27 | 3384 |  |
| #911 Miku 25Ji | Đã thêm bản tối ưu | 13.19 → 3.27 | 3385 |  |
| #921 Mejiro McQueen | Đã thêm bản tối ưu | 10.50 → 2.29 | 3386 |  |
| #922 Lumine | Đã thêm bản tối ưu | 27.37 → 13.30 | 3387 |  |
| #923 Evanescia LB | Đã thêm bản tối ưu | 28.24 → 9.56 | 3388 |  |
| #926 HMarine 2 | Đã thêm bản tối ưu | 22.73 → 7.56 | 3389 |  |
| #931 Kasane Teto | Đã thêm bản tối ưu | 18.59 → 15.06 | 3390 |  |
| #932 Mizuki 25Ji | Đã thêm bản tối ưu | 13.32 → 3.41 | 3391 |  |
| #937 Miku 25Ji | Đã thêm bản tối ưu | 13.04 → 3.12 | 3392 |  |
| #939 Megumi Fushiguro | Đã nén sẵn, giữ nguyên | 22.97 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #940 Giyu Tomioka | Đã nén sẵn, giữ nguyên | 28.10 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #941 Yao Guang | Giữ gốc, cần xem lại chất lượng | 30.38 → giữ gốc | — | FadXploit_260421QX_05: RGB PSNR 31.51 dB |
| #944 Lumine | Đã thêm bản tối ưu | 27.29 → 13.22 | 3393 |  |
| #945 Enya ESS | Đã thêm bản tối ưu | 12.89 → 8.22 | 3394 |  |
| #946 Albedo | Đã nén sẵn, giữ nguyên | 10.11 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #949 Yoimiya | Giữ gốc, cần xem lại chất lượng | 10.00 → giữ gốc | — | A74_Yoimiya_Genshin_Impact: RGB PSNR 28.9 dB |
| #962 Nian | Đã nén sẵn, giữ nguyên | 18.29 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #966 Nico Robin | Đã nén sẵn, giữ nguyên | 11.33 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #967 Emu WxS | Đã thêm bản tối ưu | 13.00 → 3.08 | 3395 |  |
| #972 Miku SRC | Đã thêm bản tối ưu | 23.36 → 4.69 | 3396 |  |
| #978 Narita Brian | Đã thêm bản tối ưu | 13.31 → 4.71 | 3397 |  |
| #979 Daiwa Scarlet | Đã thêm bản tối ưu | 12.89 → 4.62 | 3398 |  |
| #980 Lumine | Đã thêm bản tối ưu | 27.37 → 13.30 | 3399 |  |
| #982 Silver Wolf 999 | Đã thêm bản tối ưu | 30.64 → 13.06 | 3400 |  |
| #985 A2 PGR | Đã thêm bản tối ưu | 11.91 → 3.74 | 3401 |  |
| #988 Lucy | Đã thêm bản tối ưu | 31.25 → 7.92 | 3402 |  |
| #990 McQueen | Đã thêm bản tối ưu | 12.86 → 4.25 | 3403 |  |
| #992 Mayano Top Gun | Đã thêm bản tối ưu | 10.26 → 2.06 | 3404 |  |
| #995 Hatsune Miku — school uniform variant | Đã thêm bản tối ưu | 27.56 → 23.74 | 3405 |  |
| #1000 Fleurdelys2 | Đã thêm bản tối ưu | 25.34 → 6.67 | 3406 |  |
| #1001 Boa Hancock | Đã nén sẵn, giữ nguyên | 14.83 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1009 BA Asuna | Đã thêm bản tối ưu | 23.08 → 13.75 | 3407 |  |
| #1021 Hatsune Miku — animated-face school uniform variant | Đã thêm bản tối ưu | 27.56 → 23.74 | 3408 |  |
| #1024 Rin VS | Đã thêm bản tối ưu | 12.42 → 3.09 | 3409 |  |
| #1025 Fleurdelys2 | Đã thêm bản tối ưu | 25.21 → 6.54 | 3410 |  |
| #1035 Miyabi | Đã nén sẵn, giữ nguyên | 15.20 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1039 M001Hatsune | Đã thêm bản tối ưu | 32.22 → 24.04 | 3411 |  |
| #1045 Keiko Hoshino | Đã thêm bản tối ưu | 10.12 → 2.23 | 3412 |  |
| #1049 Nicole Demara | Đã thêm bản tối ưu | 14.55 → 3.98 | 3413 |  |
| #1053 Mita | Đã thêm bản tối ưu | 14.32 → 4.99 | 3414 |  |
| #1054 BA Kazusa | Đã thêm bản tối ưu | 14.31 → 4.98 | 3415 |  |
| #1056 Yanagi | Đã nén sẵn, giữ nguyên | 17.35 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1063 Aino | Đã thêm bản tối ưu | 16.36 → 5.86 | 3416 |  |
| #1069 Nihilux | Đã thêm bản tối ưu | 24.53 → 5.85 | 3417 |  |
| #1073 Lumine | Đã thêm bản tối ưu | 27.37 → 13.29 | 3418 |  |
| #1079 Aijou Karen | Đã nén sẵn, giữ nguyên | 10.39 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1087 Soukaku | Đã nén sẵn, giữ nguyên | 11.77 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1088 Bennett | Đã nén sẵn, giữ nguyên | 14.80 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1109 Emu WxS | Đã thêm bản tối ưu | 13.14 → 3.22 | 3419 |  |
| #1119 Esper Zero | Đã thêm bản tối ưu | 29.82 → 11.15 | 3420 |  |
| #1123 Nene WxS | Đã thêm bản tối ưu | 14.48 → 3.39 | 3421 |  |
| #1124 Seiya | Đã nén sẵn, giữ nguyên | 11.18 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1136 Vivian ZZZ | Đã thêm bản tối ưu | 18.72 → 4.72 | 3422 |  |
| #1139 Noa | Đã thêm bản tối ưu | 49.38 → 7.38 | 3423 |  |
| #1142 Nicole Demara | Đã thêm bản tối ưu | 14.65 → 4.08 | 3424 |  |
| #1150 The Herta | Đã thêm bản tối ưu | 20.40 → 6.40 | 3425 |  |
| #1155 Mihono Bourbon | Đã thêm bản tối ưu | 11.72 → 3.11 | 3426 |  |
| #1158 Keqing | Đã nén sẵn, giữ nguyên | 12.59 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1167 Ganyu TB | Đã thêm bản tối ưu | 14.62 → 4.12 | 3427 |  |
| #1170 M034PStyleCW | Đã thêm bản tối ưu | 17.87 → 15.36 | 3428 |  |
| #1177 Varesa | Đã thêm bản tối ưu | 14.76 → 4.26 | 3429 |  |
| #1181 M001Hatsune | Đã thêm bản tối ưu | 32.06 → 23.88 | 3430 |  |
| #1190 Bianca PoZ | Đã thêm bản tối ưu | 14.67 → 7.67 | 3431 |  |
| #1202 Symboli Rudolf | Đã thêm bản tối ưu | 11.62 → 3.02 | 3432 |  |
| #1212 Ch'en | Đã nén sẵn, giữ nguyên | 21.15 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1217 M040PStyleCG | Đã thêm bản tối ưu | 17.87 → 15.36 | 3433 |  |
| #1226 Rice Shower | Đã thêm bản tối ưu | 14.33 → 3.39 | 3434 |  |
| #1227 Evanescia | Đã thêm bản tối ưu | 24.95 → 7.45 | 3435 |  |
| #1228 Vivian ZZZ | Đã thêm bản tối ưu | 18.43 → 4.43 | 3436 |  |
| #1233 Ganyu TB | Đã thêm bản tối ưu | 14.31 → 3.81 | 3437 |  |
| #1241 Fleurdelys2 | Đã thêm bản tối ưu | 25.08 → 6.41 | 3438 |  |
| #1258 Enya ESS | Đã thêm bản tối ưu | 12.41 → 7.74 | 3439 |  |
| #1272 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 22.81 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1284 Nicole Demara | Đã thêm bản tối ưu | 14.55 → 3.98 | 3440 |  |
| #1300 Oguri Cap | Đã thêm bản tối ưu | 14.38 → 3.44 | 3441 |  |
| #1315 Yuzuha1 | Đã nén sẵn, giữ nguyên | 22.87 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1318 Cheeta | Đã thêm bản tối ưu | 21.09 → 5.04 | 3442 |  |
| #1353 Yanagi ZZZ | Đã thêm bản tối ưu | 17.09 → 4.26 | 3443 |  |
| #1354 M039PStyleMG | Đã thêm bản tối ưu | 17.87 → 15.36 | 3444 |  |
| #1360 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.81 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1363 Tokai Teio | Đã thêm bản tối ưu | 10.50 → 2.30 | 3445 |  |
| #1371 Nanami P | Đã thêm bản tối ưu | 24.53 → 7.03 | 3446 |  |
| #1377 Nihilux | Đã thêm bản tối ưu | 24.53 → 5.85 | 3447 |  |
| #1381 BA Kazusa | Đã thêm bản tối ưu | 14.57 → 5.23 | 3448 |  |
| #1383 Mita Crazy | Đã thêm bản tối ưu | 18.73 → 4.73 | 3449 |  |
| #1384 Liv Eclipse | Đã thêm bản tối ưu | 17.07 → 5.40 | 3450 |  |
| #1388 Bakushin | Đã thêm bản tối ưu | 13.88 → 3.38 | 3451 |  |
| #1389 Hyacine WCS | Đã thêm bản tối ưu | 27.57 → 8.89 | 3452 |  |
| #1390 Agnes Tachyon C | Đã thêm bản tối ưu | 11.44 → 2.83 | 3453 |  |
| #1392 Phoebe | Đã thêm bản tối ưu | 28.20 → 10.70 | 3454 |  |
| #1396 Yuta Okkotsu | Đã nén sẵn, giữ nguyên | 22.55 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1405 Yao Guang | Giữ gốc, cần xem lại chất lượng | 30.01 → giữ gốc | — | FadXploit_260421QX_05: RGB PSNR 31.51 dB |
| #1418 BA Hiyori SS | Đã thêm bản tối ưu | 12.38 → 7.71 | 3455 |  |
| #1424 BA Karin | Đã thêm bản tối ưu | 26.09 → 12.09 | 3456 |  |
| #1430 Nene WxS | Đã thêm bản tối ưu | 14.34 → 3.26 | 3457 |  |
| #1432 Signora | Đã thêm bản tối ưu | 13.17 → 3.17 | 3458 |  |
| #1433 Tokai Teio | Đã thêm bản tối ưu | 10.50 → 2.30 | 3459 |  |
| #1436 Belle3 | Đã nén sẵn, giữ nguyên | 27.91 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1446 Cissia | Đã thêm bản tối ưu | 24.80 → 7.25 | 3460 |  |
| #1447 Rappa HSR | Đã thêm bản tối ưu | 15.68 → 5.18 | 3461 |  |
| #1452 Evelyn ZZZ | Đã thêm bản tối ưu | 18.54 → 4.54 | 3462 |  |
| #1454 Cissia | Đã thêm bản tối ưu | 24.51 → 6.96 | 3463 |  |
| #1461 Alice1 | Đã nén sẵn, giữ nguyên | 22.97 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1468 Megumi Fushiguro | Đã nén sẵn, giữ nguyên | 22.68 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1485 Kanade 25ji | Đã thêm bản tối ưu | 12.37 → 2.97 | 3464 |  |
| #1488 Zani | Đã thêm bản tối ưu | 20.33 → 6.33 | 3465 |  |
| #1490 Tohka | Đã thêm bản tối ưu | 11.07 → 3.99 | 3466 |  |
| #1492 McQueen ES | Đã thêm bản tối ưu | 13.37 → 4.76 | 3467 |  |
| #1497 Bocchi (Hitori Gotoh) | Đã nén sẵn, giữ nguyên | 18.19 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1503 Evernight | Đã thêm bản tối ưu | 24.89 → 7.39 | 3468 |  |
| #1507 Mayano | Đã thêm bản tối ưu | 12.58 → 3.98 | 3469 |  |
| #1515 Nefer 2 | Đã thêm bản tối ưu | 14.86 → 4.36 | 3470 |  |
| #1519 Velina Airgid | Đã nén sẵn, giữ nguyên | 10.43 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1520 Mita Short Hairs | Đã thêm bản tối ưu | 14.19 → 4.85 | 3471 |  |
| #1522 Kanade 25ji | Đã thêm bản tối ưu | 12.28 → 2.87 | 3472 |  |
| #1524 Mint | Đã thêm bản tối ưu | 17.35 → 6.85 | 3473 |  |
| #1531 Lucy | Đã thêm bản tối ưu | 31.87 → 8.53 | 3474 |  |
| #1536 McQueen ES | Đã thêm bản tối ưu | 11.82 → 3.21 | 3475 |  |
| #1541 Sasaki | Đã thêm bản tối ưu | 13.09 → 2.59 | 3476 |  |
| #1542 Robin S | Đã thêm bản tối ưu | 25.04 → 10.97 | 3477 |  |
| #1545 Piper Wheel | Đã nén sẵn, giữ nguyên | 12.33 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1556 Miku 25ji 3rd | Đã thêm bản tối ưu | 13.17 → 3.84 | 3478 |  |
| #1558 Frieren | Giữ gốc, chưa qua kiểm tra parser | 11.56 → giữ gốc | — | Tên texture nội bộ bị lặp (fadxploit_base_outline); parser nhập từ chối nên giữ gốc. Không kết luận skin gốc hỏng. |
| #1562 Astra Yao ZZZ | Đã thêm bản tối ưu | 19.17 → 5.17 | 3479 |  |
| #1571 Frieren | Giữ gốc, chưa qua kiểm tra parser | 11.43 → giữ gốc | — | Tên texture nội bộ bị lặp (fadxploit_base_outline); parser nhập từ chối nên giữ gốc. Không kết luận skin gốc hỏng. |
| #1572 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 19.96 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1578 Tachyon LL | Đã thêm bản tối ưu | 11.84 → 3.23 | 3480 |  |
| #1579 KAITO VS | Đã thêm bản tối ưu | 14.25 → 3.16 | 3481 |  |
| #1584 M033PStylePB | Đã thêm bản tối ưu | 19.72 → 17.12 | 3482 |  |
| #1594 Sparkle HI3 | Đã thêm bản tối ưu | 15.80 → 4.42 | 3483 |  |
| #1604 Ayane | Đã nén sẵn, giữ nguyên | 11.87 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1607 Hysilens | Đã thêm bản tối ưu | 28.25 → 9.56 | 3484 |  |
| #1610 Kanata | Đã thêm bản tối ưu | 30.93 → 8.76 | 3485 |  |
| #1612 Lucy | Đã thêm bản tối ưu | 31.71 → 8.38 | 3486 |  |
| #1615 Cipher | Đã thêm bản tối ưu | 23.92 → 5.25 | 3487 |  |
| #1620 Mita Sleepy | Đã thêm bản tối ưu | 13.77 → 4.44 | 3488 |  |
| #1621 201favorito | Đã thêm bản tối ưu | 25.14 → 4.25 | 3489 |  |
| #1627 McQueen | Đã thêm bản tối ưu | 11.59 → 2.99 | 3490 |  |
| #1635 Megumi Fushiguro | Đã nén sẵn, giữ nguyên | 22.45 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1639 Seele SN | Đã thêm bản tối ưu | 19.32 → 4.65 | 3491 |  |
| #1641 Hysilens | Đã thêm bản tối ưu | 29.40 → 10.71 | 3492 |  |
| #1644 Satoru Gojo | Đã nén sẵn, giữ nguyên | 23.00 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1645 Narita Brian | Đã thêm bản tối ưu | 11.80 → 3.20 | 3493 |  |
| #1654 Miku WxS | Đã thêm bản tối ưu | 14.29 → 3.21 | 3494 |  |
| #1661 Yanagi2 ZZZ | Đã thêm bản tối ưu | 16.86 → 4.03 | 3495 |  |
| #1664 Mita Mila | Đã thêm bản tối ưu | 15.69 → 6.36 | 3496 |  |
| #1665 asuna ba | Đã thêm bản tối ưu | 13.36 → 5.86 | 3497 |  |
| #1666 Silence Suzuka | Đã thêm bản tối ưu | 10.29 → 2.09 | 3498 |  |
| #1682 Miku BA | Đã thêm bản tối ưu | 23.62 → 18.69 | 3499 |  |
| #1689 Daiwa Scarlet | Đã thêm bản tối ưu | 10.56 → 2.86 | 3500 |  |
| #1694 Kagamine Rin | Đã thêm bản tối ưu | 33.11 → 22.58 | 3501 |  |
| #1702 Yameii | Đã thêm bản tối ưu | 26.58 → 5.58 | 3502 |  |
| #1706 Yuta Okkotsu | Đã nén sẵn, giữ nguyên | 22.43 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1707 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.63 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1711 Mirei Mikagura | Đã thêm bản tối ưu | 29.23 → 4.00 | 3503 |  |
| #1719 Firefly SM | Đã thêm bản tối ưu | 19.61 → 4.94 | 3504 |  |
| #1723 Yuji Itadori | Đã nén sẵn, giữ nguyên | 22.92 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1730 H Baelz | Đã thêm bản tối ưu | 26.21 → 8.71 | 3505 |  |
| #1731 Bianca PoZ | Đã thêm bản tối ưu | 14.49 → 7.49 | 3506 |  |
| #1732 Nicole Demara | Đã thêm bản tối ưu | 14.65 → 4.08 | 3507 |  |
| #1741 Enya ESS | Đã thêm bản tối ưu | 12.41 → 7.74 | 3508 |  |
| #1743 Andoris | Đã thêm bản tối ưu | 13.28 → 5.11 | 3509 |  |
| #1752 Aisaka Taiga | Đã thêm bản tối ưu | 11.44 → 2.11 | 3510 |  |
| #1759 Yuji Itadori | Đã nén sẵn, giữ nguyên | 20.09 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1764 BA Atsuko | Đã thêm bản tối ưu | 15.27 → 7.10 | 3511 |  |
| #1768 Yao Guang | Giữ gốc, cần xem lại chất lượng | 31.07 → giữ gốc | — | FadXploit_260421QX_05: RGB PSNR 31.51 dB |
| #1770 Suguru Geto | Đã nén sẵn, giữ nguyên | 22.95 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1773 Lumine | Đã thêm bản tối ưu | 14.72 → 3.78 | 3512 |  |
| #1795 Hugo | Đã nén sẵn, giữ nguyên | 17.31 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1796 Claret Flint | Đã thêm bản tối ưu | 25.24 → 6.55 | 3513 |  |
| #1802 M001Hatsune | Đã thêm bản tối ưu | 32.16 → 23.98 | 3514 |  |
| #1813 Silver Wolf 999 | Đã thêm bản tối ưu | 29.82 → 12.25 | 3515 |  |
| #1821 Tohka | Đã thêm bản tối ưu | 11.07 → 3.99 | 3516 |  |
| #1825 DUN SHIRT3 | Đã thêm bản tối ưu | 10.61 → 3.69 | 3517 |  |
| #1827 Evanescia LB | Đã thêm bản tối ưu | 27.42 → 8.73 | 3518 |  |
| #1836 Harin | Đã nén sẵn, giữ nguyên | 20.00 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1837 HMarine 2 | Đã thêm bản tối ưu | 22.34 → 7.17 | 3519 |  |
| #1839 Yelan | Đã nén sẵn, giữ nguyên | 12.33 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1855 Miku VS | Đã thêm bản tối ưu | 12.46 → 3.13 | 3520 |  |
| #1857 Klukai 2 | Đã thêm bản tối ưu | 23.19 → 5.69 | 3521 |  |
| #1860 Nanami P | Đã thêm bản tối ưu | 24.32 → 6.82 | 3522 |  |
| #1866 Mita Short Hairs | Đã thêm bản tối ưu | 13.98 → 4.64 | 3523 |  |
| #1869 Daiwa Scarlet | Đã thêm bản tối ưu | 10.56 → 2.86 | 3524 |  |
| #1878 Isolde | Đã nén sẵn, giữ nguyên | 14.08 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1880 Cartethyia | Đã thêm bản tối ưu | 31.80 → 11.30 | 3525 |  |
| #1889 Shenhe FD | Đã thêm bản tối ưu | 14.37 → 3.87 | 3526 |  |
| #1903 Cherno | Đã thêm bản tối ưu | 18.23 → 8.90 | 3527 |  |
| #1914 Hysilens | Đã thêm bản tối ưu | 28.25 → 9.56 | 3528 |  |
| #1918 M038PStyleFB | Đã thêm bản tối ưu | 19.12 → 15.52 | 3529 |  |
| #1921 Odette | Đã nén sẵn, giữ nguyên | 13.06 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1922 BA Ayane | Đã thêm bản tối ưu | 24.45 → 17.45 | 3530 |  |
| #1926 A2 PGR | Đã thêm bản tối ưu | 12.32 → 4.15 | 3531 |  |
| #1931 Wanderer | Đã nén sẵn, giữ nguyên | 10.19 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1942 Sucrose | Đã thêm bản tối ưu | 30.91 → 12.24 | 3532 |  |
| #1945 Yoimiya | Đã nén sẵn, giữ nguyên | 12.18 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1946 Zenitsu Agatsuma | Đã nén sẵn, giữ nguyên | 11.40 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1947 Tachyon LL | Đã thêm bản tối ưu | 13.53 → 4.92 | 3533 |  |
| #1953 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 19.76 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1955 Exusiai | Đã nén sẵn, giữ nguyên | 10.80 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1956 Sparkle HSR | Đã thêm bản tối ưu | 14.49 → 7.49 | 3534 |  |
| #1962 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.70 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1970 2B Rapi | Đã nén sẵn, giữ nguyên | 12.22 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1971 Kanao Tsuyuri | Đã nén sẵn, giữ nguyên | 15.27 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #1981 M036PStyleRP | Đã thêm bản tối ưu | 17.87 → 15.36 | 3535 |  |
| #1983 Mafuyu 25Ji | Đã thêm bản tối ưu | 13.60 → 3.39 | 3536 |  |
| #1988 Jahoda | Đã thêm bản tối ưu | 19.37 → 7.70 | 3537 |  |
| #1994 Evanescia LB | Đã thêm bản tối ưu | 27.42 → 8.73 | 3538 |  |
| #1997 Evanescia | Đã thêm bản tối ưu | 23.85 → 6.35 | 3539 |  |
| #2009 Robin S | Đã thêm bản tối ưu | 24.15 → 10.08 | 3540 |  |
| #2011 Nene WxS | Đã thêm bản tối ưu | 14.48 → 3.39 | 3541 |  |
| #2015 Yuzuki Yukari | Đã nén sẵn, giữ nguyên | 13.76 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2053 Firefly SM | Đã thêm bản tối ưu | 19.85 → 5.18 | 3542 |  |
| #2059 Yuzuha 2 | Đã thêm bản tối ưu | 18.62 → 4.62 | 3543 |  |
| #2067 Esper Zero | Đã thêm bản tối ưu | 28.81 → 10.14 | 3544 |  |
| #2069 Esper Zero | Đã thêm bản tối ưu | 28.82 → 10.15 | 3545 |  |
| #2079 Gold City | Đã thêm bản tối ưu | 11.68 → 3.08 | 3546 |  |
| #2082 Galbrena | Đã nén sẵn, giữ nguyên | 18.63 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2089 Mita Sleepy | Đã thêm bản tối ưu | 13.95 → 4.62 | 3547 |  |
| #2093 Symboli Rudolf | Đã thêm bản tối ưu | 12.81 → 4.21 | 3548 |  |
| #2098 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.77 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2099 Gold Ship SS | Đã thêm bản tối ưu | 14.10 → 5.71 | 3549 |  |
| #2100 Jetavie SS | Đã thêm bản tối ưu | 23.79 → 6.29 | 3550 |  |
| #2103 Brujas | Đã nén sẵn, giữ nguyên | 24.57 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2114 Lenna 2 | Đã thêm bản tối ưu | 30.61 → 6.98 | 3551 |  |
| #2125 Lumine | Đã thêm bản tối ưu | 27.26 → 13.19 | 3552 |  |
| #2128 Akaza | Đã nén sẵn, giữ nguyên | 11.56 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2133 Claret Flint | Đã thêm bản tối ưu | 25.24 → 6.56 | 3553 |  |
| #2136 Lumine | Đã thêm bản tối ưu | 27.09 → 13.01 | 3554 |  |
| #2140 Hyacine | Đã thêm bản tối ưu | 23.88 → 5.21 | 3555 |  |
| #2141 Amber | Đã thêm bản tối ưu | 14.06 → 10.41 | 3556 |  |
| #2147 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.70 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2159 Nihilux | Đã thêm bản tối ưu | 24.52 → 5.84 | 3557 |  |
| #2165 Meisho Doto | Đã thêm bản tối ưu | 14.56 → 3.36 | 3558 |  |
| #2168 ZhuYuan | Đã nén sẵn, giữ nguyên | 22.73 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2172 Nahida | Đã nén sẵn, giữ nguyên | 10.21 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2176 BA Karin | Đã thêm bản tối ưu | 26.29 → 12.29 | 3559 |  |
| #2182 Carlotta | Đã thêm bản tối ưu | 10.62 → 5.95 | 3560 |  |
| #2184 Liv Lux | Đã thêm bản tối ưu | 17.53 → 5.86 | 3561 |  |
| #2194 Mita Cappie | Đã thêm bản tối ưu | 16.09 → 6.76 | 3562 |  |
| #2195 Okabe Rintarou | Giữ gốc, cần xem lại chất lượng | 13.46 → giữ gốc | — | okarin02: cần xem lại alpha |
| #2206 Raiden Ei | Đã thêm bản tối ưu | 13.13 → 3.80 | 3563 |  |
| #2212 Karenina E | Đã thêm bản tối ưu | 12.18 → 4.31 | 3564 |  |
| #2214 Nihilux | Đã thêm bản tối ưu | 24.52 → 5.84 | 3565 |  |
| #2220 Lucy | Đã nén sẵn, giữ nguyên | 16.83 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2222 player4 | Đã thêm bản tối ưu | 50.03 → 10.03 | 3566 |  |
| #2227 Enya ESS | Đã thêm bản tối ưu | 12.89 → 8.22 | 3567 |  |
| #2228 Mostima | Đã nén sẵn, giữ nguyên | 11.60 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2230 Seele OFC | Đã thêm bản tối ưu | 20.76 → 6.76 | 3568 |  |
| #2236 Mita Mila | Đã thêm bản tối ưu | 15.46 → 6.13 | 3569 |  |
| #2248 Anis | Đã nén sẵn, giữ nguyên | 10.14 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2252 Aino | Đã thêm bản tối ưu | 16.73 → 6.23 | 3570 |  |
| #2260 Lauma | Đã thêm bản tối ưu | 17.46 → 5.79 | 3571 |  |
| #2262 Vodka | Đã thêm bản tối ưu | 11.49 → 2.89 | 3572 |  |
| #2274 Yuta Okkotsu | Đã nén sẵn, giữ nguyên | 22.43 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2276 2B Rapi | Đã nén sẵn, giữ nguyên | 12.77 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2278 Seele OFC 2 | Đã thêm bản tối ưu | 20.51 → 6.51 | 3573 |  |
| #2279 Bianca PoZ | Đã thêm bản tối ưu | 14.62 → 7.62 | 3574 |  |
| #2285 Griseo SSB | Đã thêm bản tối ưu | 22.67 → 5.17 | 3575 |  |
| #2289 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.50 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2294 Lingsha | Đã thêm bản tối ưu | 23.78 → 5.11 | 3576 |  |
| #2296 Miku 25ji 3rd | Đã thêm bản tối ưu | 13.04 → 3.71 | 3577 |  |
| #2297 Cipher | Đã thêm bản tối ưu | 24.24 → 5.57 | 3578 |  |
| #2298 Lumine | Đã thêm bản tối ưu | 27.09 → 13.01 | 3579 |  |
| #2300 Haru Urara | Đã thêm bản tối ưu | 13.68 → 3.18 | 3580 |  |
| #2307 Kyojuro Rengoku | Đã nén sẵn, giữ nguyên | 14.05 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2312 chevreuse | Đã thêm bản tối ưu | 17.72 → 4.39 | 3581 |  |
| #2316 Rin VS | Đã thêm bản tối ưu | 12.54 → 3.21 | 3582 |  |
| #2320 Evanescia 2 | Đã thêm bản tối ưu | 24.88 → 7.38 | 3583 |  |
| #2331 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 19.78 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2336 Silver Wolf 999 | Đã thêm bản tối ưu | 29.82 → 12.25 | 3584 |  |
| #2338 Esper Zero | Đã thêm bản tối ưu | 30.47 → 11.80 | 3585 |  |
| #2347 Helia SP | Đã thêm bản tối ưu | 19.69 → 4.47 | 3586 |  |
| #2359 Lumi | Đã thêm bản tối ưu | 22.37 → 9.46 | 3587 |  |
| #2362 Seele OFC 2 | Đã thêm bản tối ưu | 20.36 → 6.36 | 3588 |  |
| #2363 Harums | Đã nén sẵn, giữ nguyên | 17.38 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2372 T.M. Opera O | Đã thêm bản tối ưu | 14.70 → 3.50 | 3589 |  |
| #2373 Ineffa | Đã thêm bản tối ưu | 19.08 → 5.08 | 3590 |  |
| #2377 Miku WxS | Đã thêm bản tối ưu | 14.41 → 3.33 | 3591 |  |
| #2383 Phoebe | Đã thêm bản tối ưu | 26.56 → 9.06 | 3592 |  |
| #2402 Monkey D. Luffy | Đã thêm bản tối ưu | 16.30 → 4.05 | 3593 |  |
| #2405 Agnes Tachyon C | Đã thêm bản tối ưu | 12.65 → 4.05 | 3594 |  |
| #2412 Cyrene | Đã thêm bản tối ưu | 32.76 → 16.43 | 3595 |  |
| #2416 Nanami P | Đã thêm bản tối ưu | 24.48 → 6.98 | 3596 |  |
| #2418 Griseo SSB | Đã thêm bản tối ưu | 22.43 → 4.93 | 3597 |  |
| #2422 Yuzuha | Đã thêm bản tối ưu | 19.04 → 5.04 | 3598 |  |
| #2424 Haru Urara | Đã thêm bản tối ưu | 10.24 → 2.04 | 3599 |  |
| #2437 Ena 25ji | Đã thêm bản tối ưu | 13.25 → 3.33 | 3600 |  |
| #2443 Miku VS | Đã thêm bản tối ưu | 12.35 → 3.02 | 3601 |  |
| #2447 Kanade 25ji | Đã thêm bản tối ưu | 12.37 → 2.97 | 3602 |  |
| #2449 Len VS | Đã thêm bản tối ưu | 12.57 → 3.23 | 3603 |  |
| #2462 Gold City | Đã thêm bản tối ưu | 13.14 → 4.54 | 3604 |  |
| #2464 BA Karin | Đã thêm bản tối ưu | 25.76 → 11.76 | 3605 |  |
| #2471 Evelyn ZZZ | Đã thêm bản tối ưu | 18.23 → 4.23 | 3606 |  |
| #2472 Seth | Đã nén sẵn, giữ nguyên | 11.99 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2475 Roronoa Zoro | Đã nén sẵn, giữ nguyên | 17.00 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2476 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 20.00 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2482 Rappa HSR | Đã thêm bản tối ưu | 15.68 → 5.18 | 3607 |  |
| #2486 Satoru Gojo | Đã nén sẵn, giữ nguyên | 22.55 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2488 Sakura Bakushin O | Đã thêm bản tối ưu | 10.28 → 2.08 | 3608 |  |
| #2491 Yuji Itadori | Đã nén sẵn, giữ nguyên | 23.05 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2508 The Herta | Đã thêm bản tối ưu | 20.82 → 6.82 | 3609 |  |
| #2512 Claret Flint | Đã thêm bản tối ưu | 25.24 → 6.55 | 3610 |  |
| #2513 Special Week SS | Đã thêm bản tối ưu | 15.64 → 7.48 | 3611 |  |
| #2517 KAITO VS | Đã thêm bản tối ưu | 14.25 → 3.16 | 3612 |  |
| #2520 BA Ayane | Đã thêm bản tối ưu | 24.63 → 17.63 | 3613 |  |
| #2526 Lumine | Đã thêm bản tối ưu | 27.29 → 13.22 | 3614 |  |
| #2530 JaneDoe | Đã nén sẵn, giữ nguyên | 14.78 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2537 Ena 25ji | Đã thêm bản tối ưu | 13.25 → 3.34 | 3615 |  |
| #2541 Oguri Cap | Đã thêm bản tối ưu | 14.24 → 3.30 | 3616 |  |
| #2547 Emu WxS | Đã thêm bản tối ưu | 13.13 → 3.22 | 3617 |  |
| #2549 Fleurdelys | Đã thêm bản tối ưu | 25.21 → 6.54 | 3618 |  |
| #2550 Lucy | Đã nén sẵn, giữ nguyên | 16.50 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2553 Mafuyu 25Ji | Đã thêm bản tối ưu | 13.60 → 3.39 | 3619 |  |
| #2560 Kurumi | Đã nén sẵn, giữ nguyên | 10.25 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2563 Arle CS | Đã thêm bản tối ưu | 22.92 → 6.59 | 3620 |  |
| #2565 Saber | Đã thêm bản tối ưu | 24.06 → 5.40 | 3621 |  |
| #2571 M001Hatsune | Đã thêm bản tối ưu | 32.21 → 24.03 | 3622 |  |
| #2572 Evanescia 2 | Đã thêm bản tối ưu | 24.07 → 6.57 | 3623 |  |
| #2574 Saber | Đã thêm bản tối ưu | 23.77 → 5.10 | 3624 |  |
| #2582 BA Atsuko | Đã thêm bản tối ưu | 15.90 → 7.73 | 3625 |  |
| #2593 KAITO VS | Đã thêm bản tối ưu | 14.14 → 3.06 | 3626 |  |
| #2601 Yuta Okkotsu | Đã nén sẵn, giữ nguyên | 22.54 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2603 Raiden Ei | Đã thêm bản tối ưu | 13.31 → 3.98 | 3627 |  |
| #2606 Liv Lux | Đã thêm bản tối ưu | 17.32 → 5.65 | 3628 |  |
| #2608 Mint | Đã thêm bản tối ưu | 17.78 → 7.28 | 3629 |  |
| #2615 Seele SN | Đã thêm bản tối ưu | 19.54 → 4.88 | 3630 |  |
| #2616 Cerydra | Đã thêm bản tối ưu | 25.72 → 9.37 | 3631 |  |
| #2618 Columbina | Đã thêm bản tối ưu | 22.35 → 7.19 | 3632 |  |
| #2627 Shinobu Kocho | Đã nén sẵn, giữ nguyên | 24.61 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2644 Suzuka | Đã thêm bản tối ưu | 11.50 → 2.89 | 3633 |  |
| #2646 Lenna | Đã thêm bản tối ưu | 30.68 → 7.05 | 3634 |  |
| #2649 Seele OFC | Đã thêm bản tối ưu | 20.57 → 6.57 | 3635 |  |
| #2659 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 19.94 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2664 Robin S | Đã thêm bản tối ưu | 24.15 → 10.08 | 3636 |  |
| #2666 M037PStyleLB | Đã thêm bản tối ưu | 17.87 → 15.36 | 3637 |  |
| #2671 Mizuki 25Ji | Đã thêm bản tối ưu | 13.16 → 3.25 | 3638 |  |
| #2681 ManCafe | Đã thêm bản tối ưu | 11.43 → 2.82 | 3639 |  |
| #2684 Chevreuse | Đã thêm bản tối ưu | 17.73 → 4.40 | 3640 |  |
| #2685 Miku SRC | Đã thêm bản tối ưu | 23.43 → 4.76 | 3641 |  |
| #2690 Evernight | Đã thêm bản tối ưu | 26.23 → 8.73 | 3642 |  |
| #2695 Evanescia | Đã thêm bản tối ưu | 24.29 → 6.79 | 3643 |  |
| #2700 Rapi | Đã nén sẵn, giữ nguyên | 11.17 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2703 Mihono Bourbon | Đã thêm bản tối ưu | 11.58 → 2.97 | 3644 |  |
| #2705 Lumi | Đã thêm bản tối ưu | 22.37 → 9.46 | 3645 |  |
| #2708 BA Ayane | Đã thêm bản tối ưu | 23.91 → 16.91 | 3646 |  |
| #2714 SAnby | Đã nén sẵn, giữ nguyên | 14.81 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2717 Rappa HSR | Đã thêm bản tối ưu | 15.34 → 4.84 | 3647 |  |
| #2721 Silver Wolf 999 | Đã thêm bản tối ưu | 30.64 → 13.06 | 3648 |  |
| #2723 Cerydra | Đã thêm bản tối ưu | 25.72 → 9.37 | 3649 |  |
| #2730 Nobara Kugisaki | Đã nén sẵn, giữ nguyên | 17.02 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2739 Kurumi | Bản tối ưu của đợt này đã được đối chiếu lại | 11.73 → 4.66 | 3650 |  |
| #2741 Lenna | Bản tối ưu của đợt này đã được đối chiếu lại | 30.26 → 6.63 | 3651 |  |
| #2744 Luffy (Hat Off) | Bản tối ưu của đợt này đã được đối chiếu lại | 10.71 → 2.61 | 3652 |  |
| #2748 Leva | Bản tối ưu của đợt này đã được đối chiếu lại | 24.86 → 7.36 | 3653 |  |
| #2750 Zani 2 | Bản tối ưu của đợt này đã được đối chiếu lại | 19.92 → 5.92 | 3654 |  |
| #2753 Varesa | Bản tối ưu của đợt này đã được đối chiếu lại | 14.46 → 3.96 | 3655 |  |
| #2755 Klukai | Bản tối ưu của đợt này đã được đối chiếu lại | 23.32 → 5.82 | 3656 |  |
| #2761 Yanagi2 ZZZ | Bản tối ưu của đợt này đã được đối chiếu lại | 16.86 → 4.03 | 3657 |  |
| #2768 Kurumi | Bản tối ưu của đợt này đã được đối chiếu lại | 11.73 → 4.66 | 3658 |  |
| #2769 A74 Focalors | Bản tối ưu của đợt này đã được đối chiếu lại | 10.85 → 6.11 | 3659 |  |
| #2770 Promeia | Bản tối ưu của đợt này đã được đối chiếu lại | 14.40 → 3.90 | 3660 |  |
| #2772 Cherno TW | Bản tối ưu của đợt này đã được đối chiếu lại | 18.23 → 8.90 | 3661 |  |
| #2773 Lenna 2 | Bản tối ưu của đợt này đã được đối chiếu lại | 30.20 → 6.57 | 3662 |  |
| #2779 Zani | Bản tối ưu của đợt này đã được đối chiếu lại | 20.12 → 6.12 | 3663 |  |
| #2783 Yanagi ZZZ | Bản tối ưu của đợt này đã được đối chiếu lại | 16.84 → 4.00 | 3664 |  |
| #2785 Leva | Bản tối ưu của đợt này đã được đối chiếu lại | 25.32 → 7.82 | 3665 |  |
| #2786 Kurumi | Bản tối ưu của đợt này đã được đối chiếu lại | 11.73 → 4.66 | 3666 |  |
| #2788 A74 Focalors | Bản tối ưu của đợt này đã được đối chiếu lại | 10.55 → 5.81 | 3667 |  |
| #2797 Yanagi2 ZZZ | Bản tối ưu của đợt này đã được đối chiếu lại | 16.64 → 3.81 | 3668 |  |
| #2800 Kurumi | Bản tối ưu của đợt này đã được đối chiếu lại | 11.73 → 4.66 | 3669 |  |
| #2802 Chasca | Bản tối ưu của đợt này đã được đối chiếu lại | 10.32 → 5.65 | 3670 |  |
| #2806 Yanagi ZZZ | Bản tối ưu của đợt này đã được đối chiếu lại | 16.84 → 4.00 | 3671 |  |
| #2807 Yanagi2 ZZZ | Bản tối ưu của đợt này đã được đối chiếu lại | 16.64 → 3.81 | 3672 |  |
| #2809 Yuzuha 2 | Bản tối ưu của đợt này đã được đối chiếu lại | 18.37 → 4.37 | 3673 |  |
| #2811 Mavuika | Bản tối ưu của đợt này đã được đối chiếu lại | 14.00 → 4.67 | 3674 |  |
| #2814 Klukai 2 | Bản tối ưu của đợt này đã được đối chiếu lại | 22.86 → 5.36 | 3675 |  |
| #2816 Daiwa Scarlet | Bản tối ưu của đợt này đã được đối chiếu lại | 10.56 → 2.86 | 3676 |  |
| #2819 Yanagi ZZZ | Bản tối ưu của đợt này đã được đối chiếu lại | 17.09 → 4.26 | 3677 |  |
| #2820 Luffy | Bản tối ưu của đợt này đã được đối chiếu lại | 10.53 → 2.44 | 3678 |  |
| #2821 Yuzuha | Bản tối ưu của đợt này đã được đối chiếu lại | 18.73 → 4.73 | 3679 |  |
| #2827 MW FBI | Đã nén sẵn, giữ nguyên | 17.78 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2837 BW SCH BIOLOGY | Đã thêm bản tối ưu | 15.95 → 15.20 | 3680 |  |
| #2847 SA OGLOCBURGER | Đã nén sẵn, giữ nguyên | 12.57 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2863 CC WARDOG1 | Đã thêm bản tối ưu | 10.72 → 4.05 | 3681 |  |
| #2869 BW GR LUCKY | Không giảm thêm, giữ nguyên | 16.21 → giữ gốc | — | No reduction; do not create an optimized variant
 |
| #2875 BW PRP TAD | Đã nén sẵn, giữ nguyên | 10.48 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2879 AT WMYBS2 | Đã thêm bản tối ưu | 13.07 → 2.57 | 3682 |  |
| #2881 VC PHIL | Đã nén sẵn, giữ nguyên | 18.53 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2900 VCS RENI | Đã nén sẵn, giữ nguyên | 11.99 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2902 AT WMYMOUN3 | Đã thêm bản tối ưu | 13.21 → 2.71 | 3683 |  |
| #2905 AT WFYDJG | Đã thêm bản tối ưu | 12.24 → 4.15 | 3684 |  |
| #2922 MW BFOH | Đã nén sẵn, giữ nguyên | 10.26 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2927 BW FIREOWNER | Đã nén sẵn, giữ nguyên | 11.85 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2937 HECK1 | Đã nén sẵn, giữ nguyên | 12.12 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2950 BMYPOL2 | Đã nén sẵn, giữ nguyên | 10.67 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2952 BW CHL ASIAN | Đã nén sẵn, giữ nguyên | 16.79 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2958 VCS PHILC2 | Đã nén sẵn, giữ nguyên | 11.08 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2977 SBMOCD | Đã nén sẵn, giữ nguyên | 12.37 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2991 CC TRMP | Đã nén sẵn, giữ nguyên | 10.06 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #2994 BW XMAS ELFM | Đã nén sẵn, giữ nguyên | 10.13 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #3043 DWAYNE | Đã nén sẵn, giữ nguyên | 10.63 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #3049 BW HOBO | Không giảm thêm, giữ nguyên | 16.04 → giữ gốc | — | No reduction; do not create an optimized variant
 |
| #3089 AT BALLAS11 | Đã thêm bản tối ưu | 10.25 → 2.16 | 3685 |  |
| #3101 AT BALLAS9 | Đã thêm bản tối ưu | 10.15 → 7.30 | 3686 |  |
| #3109 LCS ARMY | Đã thêm bản tối ưu | 15.95 → 13.75 | 3687 |  |
| #3139 SBFYPRO | Đã nén sẵn, giữ nguyên | 12.21 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #3140 CC WARDOG4 | Đã thêm bản tối ưu | 14.40 → 3.83 | 3688 |  |
| #3198 CC WARDOG6 | Giữ gốc, cần xem lại chất lượng | 10.86 → giữ gốc | — | 2: cần xem lại alpha |
| #3200 BFYBE | Đã nén sẵn, giữ nguyên | 12.28 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #3226 2b nude | Đã nén sẵn, giữ nguyên | 16.71 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #3232 wfylg | Đã thêm bản tối ưu | 12.68 → 8.93 | 3689 |  |
| #3234 Mikasa_Nude | Đã nén sẵn, giữ nguyên | 14.64 → giữ gốc | — | All rasters already DXT; original resolution retained |
| #3238 Varesa | Đã thêm bản tối ưu | 15.77 → 4.10 | 3690 |  |
| #3240 Mavuika | Đã thêm bản tối ưu | 14.17 → 4.83 | 3691 |  |
| #3242 Daiwa Scarlet | Đã thêm bản tối ưu | 10.56 → 2.36 | 3692 |  |
| #3243 Mavuika | Đã thêm bản tối ưu | 14.52 → 5.18 | 3693 |  |
| #3245 Varesa | Đã thêm bản tối ưu | 16.07 → 4.40 | 3694 |  |
| #3246 Daiwa Scarlet | Đã thêm bản tối ưu | 10.56 → 2.36 | 3695 |  |
