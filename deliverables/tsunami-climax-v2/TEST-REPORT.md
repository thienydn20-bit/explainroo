# Tsunami Climax V2 — bản thử 20 giây

Bản mới: **1920×1080, 60 FPS, 20,00 giây**, H.264/AAC stereo 48 kHz. Dự án riêng `tsunami-climax-v2`, dựng bằng Explainroo 0.4.1 và Canvas/JavaScript. Bản tsunami cũ giữ nguyên, đã xác minh SHA-256 không đổi. Không dùng API trả phí.

## Thay đổi chính

- Thay sơ đồ mặt cắt bằng bờ biển 2.5D có đường phố, nhà mái dốc, địa hình, bóng đổ và lớp không khí xa. Camera tiến nhẹ, sau đó nâng và lùi; giữ một cảnh liên tục để tránh reset khi chuyển đoạn.
- Nước biến dạng theo vị trí và thời gian: khối sóng rộng cao dần trong vùng nước nông, vượt bờ rồi lan vào phố. Không dùng một hình sóng cứng trượt ngang hoặc sóng cuộn hình ống.
- Bọt, vệt dòng và năm mảnh gỗ có tốc độ riêng cùng hướng vào đất liền. Đã sửa thứ tự che khuất của vật trôi với nhà và làm mượt mực nước ở chân công trình.
- Mặt trước dòng nước dùng đường cong nối liên tục cả vị trí và vận tốc. Camera giảm tốc mềm, rung khoảng một pixel trong khoảnh khắc chạm bờ. Motion blur 6 mẫu trong cửa trập nửa frame chỉ dùng ở các đoạn nhanh 8,7–10,3 và 15–17,5 giây; đã kiểm tra renderer thực sự thực hiện lấy mẫu.
- Kokoro local đọc tiếng Anh. Lời đọc bám các mốc 4,00 / 9,02 / 15,01 giây. Tiếng sóng và va đập tổng hợp tại máy, giảm theo lời đọc; không nhạc nền. Trộn âm thanh giữ nguyên luồng video, không mã hóa lại hình.

## Đã kiểm thử

- Giải mã toàn bộ MP4: **1.200 frame, 1.200 mã frame khác nhau, không frame trùng liền nhau**. Engine tính hình ở từng thời điểm 1/60 giây, không nhân đôi frame 24/30 FPS.
- SRT: 4 đoạn, thời gian hợp lệ, không chồng lấn. Lời đọc kết thúc ở 17,64 giây, để lại khoảng quan sát cuối.
- Explainroo verify trên bản trộn cuối: **không vấn đề**, lời đọc được nhận dạng 100%, âm lượng −14,8 LUFS, true peak −1,1 dBFS, không đoạn khung đen ≥0,4 giây hoặc gần im lặng ≥2,5 giây.
- Kiểm tra chuyển động theo timeline: mặt trước dòng nước và vật trôi tiến cùng hướng; vị trí/vận tốc liên tục qua các mốc, không có giá trị hình học không hữu hạn. Mép nước trên đất bám cao độ địa hình.
- Kiểm tra bố cục: không error/warning; còn một hint “no new element for 20s” vì đây là một cảnh Canvas chuyển động liên tục, không phải chuỗi thẻ xuất hiện.
- Đã **xem ảnh trực tiếp**: 12 thời điểm chính và 3 chuỗi, mỗi chuỗi 8 frame liên tiếp ở 60 FPS, quanh 6,60 / 8,93 / 14,93 giây. Trong các mẫu đã xem không thấy bước nhảy rõ ở mép nước hay camera. [Contact sheet](contact-sheet.jpg) · [Chuỗi frame kiểm tra](motion-checks.jpg).

## Giới hạn

Đây là minh họa cơ chế có hình học giản lược, không phải mô phỏng thủy động lực học hay dự báo ngập. Dòng nước quanh công trình và vật trôi được dựng theo quy tắc, không có bộ giải va chạm/chất lỏng đầy đủ. Một số bề mặt vẫn mang nét hình học 2.5D. Đã xem chuỗi ảnh và dùng nhận dạng/đo âm thanh tự động; **chưa nghe trực tiếp toàn bộ audio hoặc xem playback thời gian thực**. Không suy rộng việc kiểm tra các mẫu thành bảo đảm mọi frame không có khuyết điểm.

Tệp bàn giao: `video.mp4`, `video.srt`, `contact-sheet.jpg`, `motion-checks.jpg`, báo cáo này và `validation.json`. Không upload model, cache, node_modules hoặc thông tin đăng nhập.
