# Project Eagle — điểm vào cho Antigravity/Gemini

- Presentation & Radio Shuffle 07/11 đã cài trên nền 178 ảnh PASS ngày 03/11 (`staging/project-eagle/presentation-radio-shuffle-20261107/plugin`); xem [trạng thái dùng chung/source/rollback](docs/project-eagle/presentation-current-state.md) trước khi sửa menu/loading/audio/radio/startup.

Đọc [AGENTS.md](AGENTS.md) để áp dụng quy định project và [quy ước phối hợp chung](docs/project-eagle/shared-agent-workflow.md) trước khi sửa file.

- Game chơi/build và đích tích hợp feature mới duy nhất: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
- Clean đã lưu trữ trên D; kho skin/staging/backup skin cũng ở D, các đường C cũ là junction. Không dùng clean làm đích cài mod.
- Knowledge hiện tại nằm trong `docs/project-eagle`, đặc biệt [bàn giao sau merge/chuyển ổ](docs/project-eagle/storage-migration-and-lab-handover-2026-10-22.md). Lịch sử chat hoặc báo cáo cũ không thay thế trạng thái hiện tại và kiểm tra file thực tế.
- Đăng ký phạm vi, dùng staging riêng, giữ khóa trước khi ghi vào game hoặc metadata deployment chung, rồi ghi báo cáo kết quả để bên Codex đọc lại. Không sửa đồng thời cùng file/archive.
- **LUẬT CỨNG TẠO ẢNH (KHÔNG NGOẠI LỆ):** Tuyệt đối **KHÔNG BAO GIỜ** gọi API tạo ảnh bên ngoài (OpenAI `gpt-image-*`, `dall-e-*`, v.v.) trừ khi người dùng chủ động ra lệnh rõ ràng. Chỉ dùng `image-generator` nội bộ của Antigravity (`100` hình / chu kỳ trượt `5 tiếng`). Hết quota nội bộ thì dừng phần vẽ ảnh, báo số hình còn thiếu + giờ hồi quota cho người dùng, tuyệt đối không fallback sang API ngoài.

Đây là điểm vào tới cùng bộ tài liệu dùng bởi Codex; không duy trì một bản knowledge riêng ở đây.
