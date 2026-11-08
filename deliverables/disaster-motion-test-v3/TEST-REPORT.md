# Disaster Motion Test V3

**120,00 giây · 1280×720 gốc · 60 FPS · 3D thật.** Video tiếng Anh, 243 từ, Kokoro local. Dự án riêng `disaster-motion-test-v3`; hai bản cũ đã được kiểm tra SHA-256 và giữ nguyên. Không dùng API trả phí, footage hay video AI bên ngoài.

## Kỹ thuật và diễn tiến

Dựng bằng **Explainroo 0.4.1 + Three.js r180 (MIT)**, WebGL2 trong Chromium/SwiftShader. Các cảnh có mesh 3D, camera phối cảnh, ánh sáng, chiều sâu và phép kiểm tra che khuất. Texture là nhiễu bề mặt tạo tại máy. Kiến trúc thay đổi mái, độ cao, màu, ban công/cửa chớp; cây có dạng tán rộng và dạng nón; xe được cách điệu.

- 0–10s: montage rung đường, nước, đá; trở về phố trước thảm họa. Không title card mở đầu.
- 10–35s: đèn/dây điện/công trình rung khác pha; mặt cắt đứt gãy và sóng địa chấn; bụi, mảnh rơi và mảng tường tách ra.
- 35–65s: đáy biển nâng, khối nước biến dạng; góc rộng, hạ camera gần bờ, nước tràn và xe/vật trôi dịch chuyển, rồi camera nâng ra vùng ngập.
- 65–90s: mưa, vết nứt, khối trượt; đá tăng tốc/nảy/xoay và cây bị cuốn; bụi có độ trễ và vệt trượt còn lại đến đường.
- 90–112s: cột tro/khí và vật liệu bay theo quỹ đạo; dung nham có vỏ tối/khe sáng và ánh sáng nóng. Camera từ thấp sang toàn cảnh.
- 112–120s: montage bốn cơ chế và khoảng nghỉ cuối. Đây là các tình huống độc lập.

Animation tính theo thời gian tuyệt đối và hash có seed, không tích lũy theo frame. Đá được tính trước ở bước 1/240 giây, nội suy vị trí theo timeline. Nước dùng shader bề mặt 3D biến dạng, bọt/tia nước dùng hạt trong không gian 3D. Dùng bóng cảnh tĩnh và bóng tiếp xúc gần đúng cho đá; không blur toàn khung để che chuyển động.

Âm thanh rung trầm, nước, đá và gió/tro được tổng hợp local bằng DSP, có giảm âm trước cao trào và duck dưới lời đọc. MP4 dùng H.264/AAC stereo 48 kHz. SRT rời để giữ hình thoáng.

## Đã kiểm thử và sửa

- Đã render bản nháp gồm sáu đoạn chuyển động, mỗi đoạn 1,5s, ở 60 FPS trước bản cuối. Benchmark 1080p 3D phần mềm chậm; chọn 720p/60 theo phương án bạn cho phép. Bản đầy đủ đầu tiên mất khoảng 35,7 phút render offline; FPS xuất không đồng nghĩa tốc độ xử lý realtime.
- Giải mã MP4 cuối: **7,200 frame**, FPS `60/1`, 7,200 mã frame khác nhau; 0 cặp frame liền nhau giống hệt sau giải mã. Engine dựng từng thời điểm `frame/60`; không nhân đôi hay nội suy từ nguồn 24/30 FPS. 
- SRT: **32 đoạn**, không lỗi thời gian/chồng lấn; kết thúc lời ở 118.28s.
- Nhận dạng lời đọc trên bản trộn cuối: **100%**, không cảnh báo verify. Âm lượng -14 LUFS; true peak -1.5 dBFS. Không đoạn khung đen ≥0,4s hay gần im lặng ≥2,5s.
- Tái lập A → B → A ở sáu thời điểm: ảnh A giống hệt, thử ở độ phân giải QC. Kiểm tra 1,35 triệu mẫu đỉnh đá: không giá trị lỗi; sai số tiếp xúc nền trong ngưỡng 0,15 đơn vị của mô hình; cả 45 khối đến khu vực đường. Dòng nước không đảo hướng tiến tổng thể.
- Đã sửa tư thế đá ban đầu và lỗi camera xuyên địa hình đầu đoạn núi lửa. Đoạn 90–112s được render lại và ghép thay đúng 1.320 frame; AAC giữ nguyên bitstream. Camera mới được kiểm tra ở 1.321 thời điểm, khoảng hở nhỏ nhất hơn 10 đơn vị địa hình.
- Đã **xem ảnh trực tiếp** từ MP4: 20 thời điểm chính và 12 chuỗi, mỗi chuỗi 8 frame liên tiếp quanh cao trào/đổi camera. Sau sửa đã trích lại ảnh từ MP4 bàn giao. [Contact sheet](contact-sheet.jpg) · [Chuỗi frame](motion-checks.jpg). Không xem playback realtime hoặc nghe trực tiếp toàn bộ audio; kiểm tra tiếng nói/âm lượng là tự động.
- Layout không error/warning; các hint “no new element” xuất hiện vì đồ họa 3D được đưa vào Canvas như một khối chuyển động liên tục.

## Giới hạn còn lại

Phong cách là **3D low-poly có texture**. Nước và chuyển động xe/vật trôi là mô hình minh họa, không có bộ giải thủy động lực học/buoyancy đầy đủ. Bụi/tro là hạt billboard 3D, không phải thể tích khí mô phỏng CFD. Va chạm đá–đá, công trình và hàng rào chưa giải đầy đủ; tiếp xúc địa hình/bóng động còn gần đúng. Bóng cứng và răng cưa nhỏ có thể thấy ở 720p. Việc xem các mẫu không bảo đảm mọi frame đều hoàn hảo.

Các tệp bàn giao gồm MP4, SRT, hai ảnh kiểm tra, báo cáo này và `validation.json`. Không upload model AI, cache, node_modules hoặc thông tin đăng nhập.
