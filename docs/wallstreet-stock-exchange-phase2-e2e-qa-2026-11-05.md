# Eagle Wall Street Stock Exchange — Báo Cáo Tích Hợp Phase 2 & Nghiệm Thu DirectX 9 (`2026-11-05`)

- **Agent / Phiên thực hiện**: Antigravity (`7cc5f56b-9a2d-46ce-902b-37b8220f72be`)
- **Phiếu công việc**: [2026-11-05-antigravity-wallstreet-exchange-phase2-ingame-integration.md](work-items/2026-11-05-antigravity-wallstreet-exchange-phase2-ingame-integration.md)
- **Target tích hợp**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Staging & Nguồn build**: `D:\GTA Archive\Staging\project-eagle\wallstreet-exchange-20261105\phase2_build`
- **Trạng thái kiểm thử**: **PASS 100%** (`Part A Offline` + `Part B Live DirectX 9 1920x1080` + `eagle_doctor 11/11 PASS`, `0` Lua errors, cả hai khóa `game-write` và `ingame-runtime` đã nhả sạch).

---

## 1. Tổng quan kiến trúc đã triển khai

1. **Nội thất 3D Không Cột Chắn (`Model ID = 15100`, `int_wallstreet`, `ws_interior.txd`, `wallstreet_exchange.col`)**:
   - Đặt tại tọa độ biệt lập `Area Code = 1` `(2200.0, -1650.0, 1650.0)` (`0` xung đột trong bán kính `300m`).
   - Thiết kế cảm hứng Sàn NYSE 18 Broad Street (`36m × 44m × 16.8m`): chỉ giữ 4 cột góc sảnh + 2 trụ đỡ gác lửng sát cầu thang (`0%` che khuất tầm nhìn của cả 5 bảng điện tử), tường đá cẩm thạch Travertine kín khít 4 hướng, mái vòm ô cờ lấy sáng trung tâm, tượng Bò Húc Phố Wall bằng đồng tại sảnh Nam, 4 Quầy Chuyên Biệt hình móng ngựa (`Post 01..04`) và Ban Công Chuông Khai Mạc phía Bắc có 2 cầu thang đá cẩm thạch đi bộ mượt không cần nhảy (`.COL3` ramp `nz = 0.894`).

2. **5 Bảng Điện Tử 3D Trực Tiếp Trên GPU (`EagleWallStreet.asi` + `eagle_wallstreet_floor.py`) — Đồng Bộ 1:1 Với `EagleCompanion`**:
   - Win32 Shared Memory `"Local\EagleWallStreetSHM"` (`9,445,376` bytes, magic `0x57535431` `'WST1'`) kết hợp bắt tay con trỏ tách đôi 16-bit `shm_ptr_hi` / `shm_ptr_lo` qua `cleo\EagleRide\ws_bridge.ini` (chống tràn số nguyên có dấu 32-bit dưới `LARGEADDRESSAWARE`).
   - `EagleWallStreet.asi` (`8,192` B, x86 PE) hook nối chuỗi `Idle -> CGame::Process` tại `0x0053E981`, tìm slot `ws_interior` trong `TxdStore` (`txd_slot = 7733` thực tế) và đẩy pixel `BGRA32` (`D3DFMT_A8R8G8B8`, 1 mip, không nén DXT) trực tiếp vào `RwRaster` qua `RwRasterLock` (`0x007FB2D0`) / `RwRasterUnlock` (`0x007FAEC0`):
     - `[0] ws_ticker_ring` (`2048×128`): Vòng băng giá LED 360° treo giữa sảnh + viền chạy tường Tây/Đông, cuộn mượt **60 FPS** trên GPU (`148 px/s`, số nguyên điểm tĩnh Q16.16).
     - `[1] ws_board_main` (`1024×512`): Đại bảng Jumbotron phía Bắc hiển thị chỉ số tổng hợp `EAGLE-51`, thang tâm lý thị trường, hiệu suất 6 nhóm ngành, bản đồ nhiệt Finviz 12 mã dẫn dắt, tin nóng `The Eagle Times` và số dư ví thật của Aether (`Cash`, `Bank`, `Spot`, `Active Futures`).
     - `[2] ws_board_chart_a` (`1024×512`): Tường biểu đồ phía Tây (`10.4m × 5.1m`) hiển thị 48 cây nến OHLCV + `MA7` / `MA20` + Volume + Sổ lệnh L2 (mặc định `NVDA`, bấm `[T]` ghim bất kỳ mã nào trong 51 mã).
     - `[3] ws_board_chart_b` (`1024×512`): Tường biểu đồ phía Đông (`10.4m × 5.1m`) hiển thị 48 cây nến OHLCV + `MA7` / `MA20` + Volume + Sổ lệnh L2 (mặc định `BTC`, bấm `[Y]` ghim bất kỳ mã nào trong 51 mã).
     - `[4] ws_post_screen` (`1024×512`): Cụm 3 màn hình máy trạm trên cả 4 Quầy Giao Dịch (`Top Movers Watchlist` + `Client Portfolio Desk` + `GPT-5-NANO Broker Wire` hiển thị trực tiếp nhận định AI vừa trả lời).

3. **Đội Hình Đúng 18 Nhân Vật Nữ Cố Định (`Custom Ped IDs 49448..49465`) & Hành Vi Ngẫu Nhiên Không Lặp Lại**:
   - Khi `inside_exchange == 1`, `EagleWallStreet.asi` khóa `CPopulation::PedDensityMultiplier` (`0x008D2530`) về `0.0f` để tuyệt đối không sinh ped nam/ngẫu nhiên ngoài đường trong sàn; khi bước ra thành phố tự động khôi phục giá trị gốc.
   - **8 Nữ Broker tương tác `[E]` (`49448..49455`)**:
     - `49448` `ws_yanagi` — Tsukishiro Yanagi (`Post 01`: AI, Bán Dẫn & Game Tech)
     - `49449` `ws_zani` — Zani (`Post 02`: Vàng, Dầu Thô & Hàng Hóa Vĩ Mô)
     - `49450` `ws_evelyn` — Evelyn Chevalier (`Post 04`: Quỹ Định Chế VIP & Blue-Chip)
     - `49451` `ws_kazusa` — Kyouyama Kazusa (Broker lưu động sảnh trung tâm)
     - `49452` `ws_yaowg` — Yao Quant (Broker lưu động khu bảng nến)
     - `49453` `ws_karenina` — Karenina: Ember (`Post 03`: Crypto & Phái Sinh `10x`)
     - `49454` `ws_himeko` — Himeko (Ban Công Chuông Khai Mạc phía Bắc)
     - `49455` `ws_topaz` — Topaz (Broker lưu động chiến lược M&A)
   - **10 Nữ Trader hoạt náo (`49456..49465`)**: `ws_hina`, `ws_griselle`, `ws_mcafe`, `ws_goldcity`, `ws_bourbon`, `ws_blackswan`, `ws_lynette`, `ws_chevreuse`, `ws_clorinde`, `ws_arlecchino`.
   - `FloorChoreographyDirector` rút thăm bố cục mới mỗi lần bước vào sàn và chuyển trạng thái ngẫu nhiên mỗi `14–32s` kèm bộ nhớ cấm lặp (`taboo`): đi bộ qua lại trên sàn, leo lên/xuống hai cầu thang đá cẩm thạch lên ban công lửng, đứng ngước nhìn bảng điện tử (`OTB::wtchrace_loop`, `COP_AMBIENT::Coplook_watch`), trầm ngâm suy nghĩ (`COP_AMBIENT::Coplook_think`), xem màn hình quầy (`COP_AMBIENT::Copbrowse_loop`) và tự động ghép đôi trò chuyện mặt đối mặt (`PED::IDLE_chat` + `COP_AMBIENT::Coplook_nod`).

4. **Tư Vấn Broker AI `gpt-5-nano` & Đặt Lệnh Trực Tiếp Vào Ví `EagleCompanion`**:
   - Bấm `[E]` cạnh bất kỳ Nữ Broker nào mở giao diện tư vấn chuyên nghiệp `EagleWallStreetHud.lua` dùng model **`gpt-5-nano`** (`BROKER_AI_MODEL = "gpt-5-nano"`, hoàn toàn tách biệt với `gpt-6-luna`), đọc trực tiếp giá, `MA7`/`MA20`, biên độ 20 phiên và danh mục hiện tại của người chơi.
   - Hỗ trợ đầy đủ phím nóng ngay tại quầy: `[1]` Hỏi `gpt-5-nano`, `[2]` Spot BUY, `[3]` Spot SELL, `[4]` LONG 10x, `[5]` SHORT 10x, `[6]` Đóng vị thế Futures, `[Q/R]` Đổi mã, `[Z/C]` Đổi quy mô lệnh (`\$500 .. \$100,000`), `[T/Y]` Ghim biểu đồ lên tường 3D Tây/Đông, `[F6]` Nhập câu hỏi tự do, `[Backspace]` Đóng.

5. **4 Cổng Thành Phố Khứ Hồi Thông Minh + 4 POI `GG Map` + Radar Blip (`$`, Icon `52`)**:
   - `[0]` **Los Santos — Pershing Square Financial Hall**: Cổng `(1481.0, -1770.5, 18.80)`, POI `wallstreet_poi_ls` `(1481.0, -1750.5, 13.55)`.
   - `[1]` **San Fierro — Financial District Tower**: Cổng `(-1725.5, 789.8, 23.90)`, POI `wallstreet_poi_sf` `(-1722.5, 789.8, 23.90)`.
   - `[2]` **Downtown Chicago — LaSalle Stock Exchange**: Cổng `(6256.2, 9257.5, 7.80)`, POI `wallstreet_poi_chi` `(6252.8, 9257.5, 7.80)`.
   - `[3]` **Liberty City — South Staunton Exchange**: Cổng `(14580.9, 7766.5, 21.52)`, POI `wallstreet_poi_lc` `(14580.9, 7762.5, 21.50)`.
   - Vào từ thành phố nào (`entry_city_idx = 0..3`), khi bước ra cửa sảnh Nam `(2200.0, -1670.6, 1650.05)` sẽ tự động đưa Aether về đúng vỉa hè thành phố đó.

---

## 2. Danh sách file triển khai & Mã băm SHA-256 (`manifest_before_after.json`)

### File thêm mới (7 file)
| File trong `gameplay-lab` | SHA-256 sau triển khai |
|---|---|
| `CUSTOM/wallstreet_exchange.img` | `8a577adc9d650e86979105a58f30bf58eca65f2d4e3eb05ed219ae611de414f1` |
| `CUSTOM/wallstreet_exchange.ide` | `4b7c46ac4fc0d8f10f1bae7886588d9768ef98b9911d5315eaa9d821a68c1cee` |
| `CUSTOM/wallstreet_exchange.ipl` | `1405dea4355c066f2b905ab0491ce7e7d0efde7d004d87eac60f52405798a08e` |
| `EagleWallStreet.asi` | `04c7fe53c4f411ce821c769232ba9f5a340b6282eb5e164344208e3594f92146` |
| `cleo/EagleWallStreetBridge.cs` | `794089f04f6e934cc02ddad781168b05be0e8035cc8d2171740856a75dcab37d` |
| `cleo/EagleWallStreetHud.lua` | `016b878285d451cc8a7132ee933d77077e7ea7482e5dc32c0f751f85696a6a68` |
| `eagle_wallstreet_floor.py` | `4af02fa96d9938d0a700a1504f2834f51b5a56fdd000f2850a9675cef819e1e0` |

### File dùng chung đã cập nhật có kiểm soát dưới `game-write.lock` (6 file)
| File trong `gameplay-lab` | SHA-256 trước (`before`) | SHA-256 sau (`after`) |
|---|---|---|
| `data/gta.dat` | `28f5defcdf5b2d37ac9d9821a8d3718b6ee595f68f90a3d8d687997e9c7c8580` | `c9b262038e3ae750d736f32ff1d19b3ce4d0a61badea30f24274a8707f77f80e` |
| `data/peds.ide` | `1c066f329392e6fb64c8aae207ec4b13d9c8b119d8c070a9fa6c1ae1383b71e0` | `71bb5f9410454f9f4812512437cd332615be7aae05e0ec99b865caf54ccac324` |
| `eagle_gg_map_pois.py` | `1a3b7de2a05fc15ae5bc17864ce2cd9d53d1c0dbf7244b92d3c7943a2b9295c9` | `b2ef4783d06e88e4defcf61df0c99ab292357f8cd60843943e8c33369f002198` |
| `EagleCompanion.py` | `d77c996330d462385e798f7c339e65103b7057d938ee0cc9e870f1d9c24d2d76` | `465401e291ee8e80a5deff8f1b647ff27805b813b0ec248f42825077d9a92c7c` |
| `hud.lua` | `d95879b12717219cbe6e7d2e5f58444094b9bd05f361c68c29d4d7aa66e71b94` | `40d8ecb8871bc7539c993e407b715cf9a5690306d0ee7fa2abc4e281ad8b313e` |
| `eagle_ride_engine.py` | `a68d6bf870544d5b57d0d21d2076f4e0ea476f491fc6a50f01813a9f10769001` | `d16e028dd92304263a16287e6c901fba85078a26c3dcad5049a547df1c661a62` |

---

## 3. Kết quả kiểm thử Part A (Offline) & Part B (Live DirectX 9 `1920×1080`)

- **Part A Offline (`test_part_a_offline.py` -> `part_a_offline_results.json`)**:
  - `py_compile` sạch 100%; `wallstreet_exchange.img` (`VER2`, `39` entries, `83.00 MiB`); render trọn bộ 5 bảng `BGRA32` chỉ mất **`59.35 ms`**; `5/5` lần rút thăm hành vi cho bố cục khác biệt + lộ trình leo cầu thang 3 nhịp; gọi thật API `gpt-5-nano` trả lời chuẩn xác 100% ASCII.
- **Part B Live In-Game DirectX 9 (`run_part_b_wallstreet_qa.py` -> `part_b_live_results.json`, `82.0s`, `EXIT=0`)**:
  - **Cổng Pershing Square LS (`01_pershing_square_entrance_live.png`)**: Nhận diện `near_portal_idx = 0`, hiển thị vòng sáng vàng + thanh nhắc `[E] Enter Eagle Wall Street Stock Exchange`.
  - **Nội thất & 5 Bảng Điện Tử 3D (`02`, `03`, `04`)**: `txd_slot_found = 7733`, `rasters_valid_mask = 31` (`0b11111`), `total_board_uploads = 96`, `ticker_gpu_frames = 1322`, `board_py_seq == board_gpu_ack == [24, 24, 24, 24, 24]`.
  - **Cô lập đúng 18 Nhân Vật Nữ & Hành Vi Động**: `spawned_mask = 0x3FFFF` (`18/18` nhân vật nữ có handle & `CPed*` hợp lệ), `ped_density_locked = 1` (`0.0f` trong RAM), `8` mã hoạt ảnh khác nhau hoạt động đồng thời trên `15` vị trí neo độc lập (kể cả đi bộ lên cầu thang cẩm thạch).
  - **Tư vấn `gpt-5-nano` + Đặt lệnh ví thật (`05_yanagi_gpt5nano_broker_terminal_live.png`)**: Nhấn `[E]` trước Yanagi (`Post 01`) mở bảng tư vấn, `gpt-5-nano` trả lời trực tiếp dựa trên nến `NVDA` hiện tại và đồng thời in lên màn hình 3D trên bàn Yanagi; nhấn `[2]` khớp lệnh Spot BUY `\$2,500` trừ tiền mặt thật `\$125,000 -> \$122,500`, tăng `NVDA spot_qty: 0.0000 -> 1.7351`.
  - **Ghim mã trực tiếp lên tường nến 3D (`06_west_wall_pinned_amd_live.png`)**: Chuyển tường Tây từ `NVDA` sang `AMD`, `board_gpu_ack[2]` tăng tức thì (`22 -> 23`), tường 3D đổi sang đồ thị nến `AMD` ngay trong khung hình DirectX 9.
  - **Thoát khứ hồi & Dọn dẹp**: Rời cửa sảnh Nam trả Aether đúng Pershing Square LS `(1481.0, -1768.0, 19.65, Area=0, sai số 0.00m)`, giải phóng `spawned_mask = 0`, trả `ped_density_locked = 0`, khôi phục nguyên vẹn trạng thái ví của người chơi trước test.
  - **Nghiệm thu đặt xe `EagleRide` tới đủ 4 thành phố (`run_eagleride_wallstreet_4cities_qa.py` -> `eagleride_4cities_live_results.json`, `119.4s`, `EXIT=0`)**: Đã mở khóa mặc định cả 4 POI `wallstreet_poi_{ls,sf,chi,lc}` trong `DEFAULT_UNLOCKED_POIS` và vá lỗi tồn đọng `fast_forward_trip` (`read_live_player()["pos"]` thay cho `read_player_coords()`). Đã test trực tiếp trong DirectX 9 với `Debug Mode = OFF` cho cả 4 hãng xe (`Uber Car` chạy thật trên làn đường LS + `[F10]` trả khách ở Pershing Square `er_01/er_02`, `Xanh SM Car` tới SF Financial District `er_03`, `GrabBike` tới Downtown Chicago LaSalle `er_04`, `BeBike` tới Liberty City South Staunton `er_05`), kèm vào `[E]` -> `Area 1` -> thoát cửa Nam trả về đúng từng thành phố (`sai số 0.33m` cả 4/4 cổng).
  - **Kiểm toán sức khỏe hệ thống (`eagle_doctor.py`)**: `11/11 PASS, 0 WARN, 0 FAIL`, `0` lỗi trong `cleo/EagleLuaErrors.log`.

---

## 4. Phục hồi (Guarded Rollback)

Nếu cần gỡ riêng tính năng Sàn Chứng Khoán Eagle Wall Street (kiểm tra khớp mã băm SHA-256 `after` trước khi khôi phục dưới khóa `game-write`):

```powershell
python "D:\GTA Archive\Staging\project-eagle\wallstreet-exchange-20261105\phase2_build\rollback_wallstreet_phase2.py"
```
