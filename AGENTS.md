# Phạm vi project GTA

## Mục tiêu hiện tại

- **07/11/2026 — Presentation & Radio Shuffle đã cài (trên nền 178 ảnh PASS ngày 03/11):** nâng cấp Fisher–Yates Shuffle Bag + cooldown xuyên lần mở game (`wibu-shuffle.dat`) cho 89 loading (`2s`), 89 menu (`4s`), nhạc menu (tự đổi bài khi hết và khi rời menu vào gameplay) + random mốc thời gian `RadioEx` khi vào New Game ngay trong `WibuMenu.asi` (`sha256=c8106951...`, giữ nguyên `PECore.asi` và `radio.dat` trên đĩa). Đọc [trạng thái hiện tại](docs/project-eagle/presentation-current-state.md) và `data/project-eagle/coordination/presentation-state.json` trước khi sửa loading/menu/audio/radio/startup. Nguồn plugin mới nhất ở `staging/project-eagle/presentation-radio-shuffle-20261107/plugin`; ba transaction presentation có rollback riêng theo thứ tự mới trước, không dùng rollback merge để gỡ chúng. Giữ source/artwork/packages/before-images; compiler intermediates và executable QA đã được dọn, build script tạo lại được.
- Từ ngày 13/10/2026, game mục tiêu là **Project Eagle**. GTA Underground chỉ còn là tài liệu tham khảo cho quy trình cũ.
- Từ 22/10/2026, bản chơi hợp nhất là `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`, đã nhận loading, main menu và NPC từ bản `gta sa clean\gta sa clean`; Aether và radio đã có sẵn. Đọc `docs\project-eagle\merge-clean-to-gameplay-lab-2026-10-22.md` trước khi cài hoặc phục hồi.
- Bản clean đã chuyển sang `D:\GTA Archive\Project Eagle\gta sa clean\gta sa clean` để lưu trữ. Đường dẫn C cũ là junction tới D; không dùng bản lưu trữ làm đích chơi/build/cài mod. Bộ Eagle ban đầu được đưa vào dưới dạng clean, hiện đã có mod; không coi tên `clean` là bằng chứng GTA SA vanilla.
- Kho skin vật lý ở `D:\GTA Archive\Skin Library`; đường `C:\Users\LENOVO\Desktop\GTA\Skin Library` và các staging/backup skin cũ được giữ bằng junction. Giữ ổ D sẵn khi xem kho/build. Asset runtime của gameplay-lab vẫn ở C.
- Skin Viewer, Radio Studio và các workflow loading/menu hiện nhắm gameplay-lab; giữ kiểm tra hash/ownership, không tái dùng lịch sử clean hoặc bản build cũ để apply vào lab. Lần build skin tiếp theo phải tạo plan/build mới. Menu/loading thuộc transaction merge dùng rollback merge riêng; không chạy lại script thử nghiệm Aether/autoload/NPC pilot cũ chỉ vì chúng còn được lưu.
- Đọc `docs\project-eagle\storage-migration-and-lab-handover-2026-10-22.md` để biết các đường D, bằng chứng chuyển dữ liệu, ownership mới và trạng thái kiểm tra.
- Trải nghiệm mong muốn: nhân vật chính Aether từ Genshin Impact; NPC/ped từ game/anime theo danh sách được chọn sau; radio custom để lái xe dạo phố, nghe nhạc và ngắm NPC.
- Với Aether thay CJ: ưu tiên chất lượng ngoại hình đẹp và rig hỗ trợ đầy đủ các animation/chức năng của nhân vật chính. Cần đánh giá việc đi bộ/chạy, chiến đấu, dùng vũ khí, bơi, leo trèo và điều khiển phương tiện; không coi một skin ped nhìn đúng là đủ.
- Với NPC/ped về sau: ưu tiên đúng hình dạng và tài nguyên nhẹ để hạn chế ảnh hưởng performance; không yêu cầu mức hoàn thiện hoặc phạm vi kiểm thử animation tương đương nhân vật chính.
- Không tiếp tục thay đổi bản Underground trừ khi người dùng yêu cầu quay lại.

## Điều phối và nghiên cứu

- Mọi feature mới được phát triển để tích hợp vào **gameplay-lab**. Codex và Antigravity dùng chung [quy ước phối hợp và knowledge](docs/project-eagle/shared-agent-workflow.md); mỗi agent phải đọc tài liệu này cùng báo cáo bàn giao mới nhất trước khi nhận việc, đăng ký phạm vi và cập nhật kết quả sau khi làm.
- Code/file nguồn không được sửa đồng thời bởi hai agent. Các thao tác ghi vào game, metadata deployment dùng chung hoặc rollback phải giữ khóa ghi chung theo tài liệu phối hợp; build trong staging riêng và kiểm lại hash ngay trước apply. Có phạm vi chồng nhau thì tiếp tục phần độc lập, chờ bàn giao phần đang bị chiếm.
- Hội thoại chính dùng để xác định tác vụ, điều phối và tổng hợp kiến thức.
- Với tìm kiếm rộng hoặc công việc khảo sát nặng, giao cho subagent dùng GPT Luna. Model nhỏ hiện có là `gpt-6-luna`; khi chọn model khác với agent chính, dùng `fork_turns="none"` và cung cấp đủ ngữ cảnh/phạm vi cho agent.
- Agent chính có thể kiểm tra nhanh, đọc kết quả và xác minh các điểm quyết định. Tránh thực hiện lại toàn bộ tìm kiếm đã giao.
- Chia phạm vi độc lập khi hữu ích; không để nhiều agent sửa cùng một file.
- Chỉ tạo chat mới trong sidebar khi người dùng yêu cầu. Các phần việc của cùng yêu cầu có thể dùng subagent.
- **QUY TẮC CỨNG VỀ TẠO ẢNH (BẮT BUỘC 100%):** **CẤM TUYỆT ĐỐI** dùng bất kỳ API tạo ảnh bên ngoài nào (OpenAI `gpt-image-*`, `dall-e-*`, hay dịch vụ tạo ảnh bên thứ ba khác) để vẽ, sửa hoặc bù ảnh trong mọi tác vụ, **TRỪ KHI người dùng yêu cầu rõ ràng bằng lời trong hội thoại đó**. Chỉ được dùng công cụ/subagent `image-generator` nội bộ của Antigravity (`gemini-3.1-flash-image` / Nano Banana, hạn mức thực tế `100` hình / cửa sổ trượt `5 tiếng` dùng chung toàn tài khoản Ultra). Khi `image-generator` nội bộ chạm trần quota `429 RESOURCE_EXHAUSTED`, bắt buộc **dừng phần tạo ảnh ngay lập tức**, giữ nguyên các ảnh đã tạo đạt chuẩn, báo rõ số lượng ảnh còn thiếu và thời điểm hồi quota cho người dùng để chờ hồi quota vẽ tiếp; tuyệt đối không tự ý chuyển sang API ngoài hay tạo ảnh giả/placeholder ghi đè vào thư mục đích.

## Cách làm việc với mod

- Với yêu cầu tìm hiểu/khảo sát, chỉ đọc game và tài nguyên. Ghi báo cáo dưới `docs\project-eagle`; không cài skin, thay archive hoặc audio khi chưa có yêu cầu triển khai.
- Dựa vào bản Eagle thực tế, cấu hình loader, log và tài liệu Eagle. Không mặc định các giới hạn hoặc cách cài của Underground áp dụng cho Eagle.
- Tách rõ: có file/config, tài liệu mô tả hỗ trợ, và tính năng đã được thử trong game.
- Khi có yêu cầu cài mod, chuẩn bị bản phục hồi và kiểm tra thay đổi trong staging phù hợp với phạm vi được giao.
- Discord/browser được dùng để đọc hướng dẫn liên quan. Không gửi tin nhắn, tham gia server hoặc thực hiện hành động với người khác nếu chưa được người dùng yêu cầu.
