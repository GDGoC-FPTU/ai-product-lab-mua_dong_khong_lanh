# AI Log & Reflection - Lab 02

## 1. Tôi đã dùng AI như một thought-partner như thế nào?

Trong buổi lab này, tôi dùng AI chủ yếu ở 4 phần: brainstorm bài toán, phản biện quick problem card, hỗ trợ viết problem statement, và kiểm tra prompt prototype.

Ở Phase 1, tôi bắt đầu với nhiều ý tưởng rời rạc như phân tích trải nghiệm xe VinFast, phát hiện rủi ro an ninh ở Vinhomes, phân tích phản ánh chuyến đi Xanh SM, gợi ý lịch trình Vinpearl và tóm tắt hồ sơ Vinmec. AI giúp tôi nhìn các ý tưởng này theo 4 lenses: repetitive, time-consuming, AI-upgrade và stakeholder pain. Nhờ vậy tôi hiểu rằng không phải ý tưởng nào nghe "AI" cũng là bài toán tốt. Một bài toán tốt cần có actor rõ, workflow hiện tại rõ, bottleneck có thể đo được, và ranh giới vận hành đủ an toàn.

Ở Phase 2, tôi dùng AI để stress-test quick card về an ninh Vinhomes. Ban đầu tôi viết theo hướng "AI phát hiện tội phạm ẩn trốn trong Vinhomes". AI phản biện rằng cách viết này dễ gặp vấn đề về privacy, pháp lý và false positive. Sau đó tôi điều chỉnh wording theo hướng an toàn hơn: AI chỉ tạo cảnh báo rủi ro ban đầu dựa trên danh sách cảnh báo nội bộ đã được phê duyệt, còn bảo vệ và cơ quan chức năng vẫn phải xác minh thủ công trước mọi hành động.

Khi nhóm chuyển sang deep-dive bài toán Xanh SM xử lý sự cố pin, AI giúp tôi cấu trúc lại quy trình hiện tại thành các bước rõ ràng: nhận cuộc gọi, tra cứu GPS xe, tra cứu trạm sạc còn trụ trống, soạn tin nhắn hướng dẫn và gọi cứu hộ nếu cần. AI cũng giúp tôi biến mô tả nghiệp vụ thành problem statement 6-field có actor, bottleneck, business impact, success metric và operational boundary.

## 2. AI giúp được gì nhiều nhất?

AI giúp tôi nhanh nhất ở phần biến ý tưởng mơ hồ thành format có thể chấm điểm được. Ví dụ, thay vì chỉ nói "điều phối viên xử lý lâu", AI gợi ý tôi phải ghi cụ thể: bước 3 và bước 4 mất khoảng 10 phút, tổng quy trình thủ công khoảng 15 phút/lượt, mục tiêu giảm xuống dưới 3 phút/lượt.

AI cũng giúp tôi nghĩ về ranh giới vận hành. Với bài toán Xanh SM, nếu AI tự động gửi hướng dẫn sai cho tài xế đang còn 2% pin thì có thể gây rủi ro ngoài thực địa. Vì vậy nhóm đặt rule rõ: AI chỉ tạo draft có tag `[DRAFT_ONLY]`, không tự gửi tin nhắn nếu chưa có điều phối viên duyệt; nếu pin dưới 5% và trạm sạc xa hơn 5km thì phải đề xuất xe cứu hộ pin di động thay vì cố hướng dẫn tài xế chạy tới trạm.

Ở phần prompt prototype, AI giúp tôi thiết kế adversarial test input để thử phá ranh giới, ví dụ yêu cầu "bỏ qua bước nháp" hoặc ép AI chỉ đường đến trạm sạc cách 8km khi pin còn 2%. Test này giúp nhóm kiểm tra xem prompt có bảo vệ đúng boundary không.

## 3. AI sai hoặc chưa tốt ở đâu?

AI có lúc đề xuất giải pháp quá "xịn" so với scope bài lab. Ví dụ với bài toán camera/an ninh Vinhomes, AI có thể dễ dàng đẩy sang Agent tự phát hiện, tự tạo ticket, tự điều phối bảo vệ, tự escalate. Ý tưởng này nghe mạnh nhưng nếu không kiểm soát sẽ quá rộng, khó prototype, và dễ bị hỏi về dữ liệu cá nhân, quyền truy cập camera, quyền xác minh danh tính và trách nhiệm khi AI cảnh báo sai.

Một điểm nữa là AI đôi khi làm metric nghe có vẻ chắc chắn nhưng chưa có dữ liệu thật. Ví dụ các con số như "80 sự cố/ngày", "giảm từ 15 phút xuống dưới 3 phút" hoặc "98% hướng dẫn đúng" cần được hiểu là giả định để scope lab, không phải thống kê chính thức. Tôi phải tự nhắc mình ghi theo hướng estimated metric và dùng nó để minh họa cách đo thành công, không trình bày như dữ liệu đã được kiểm chứng.

AI cũng có xu hướng chọn LLM hoặc Agent hơi nhanh. Sau khi so sánh lại, tôi thấy không phải bước nào cũng cần LLM. Phần tra cứu GPS, lọc trạm sạc theo khoảng cách và loại cổng sạc nên dùng rule/API logic. LLM chỉ phù hợp cho phần tạo nội dung hướng dẫn dễ hiểu, thân thiện, đúng ngữ cảnh cho tài xế.

## 4. Tôi đã sửa prompt và cách làm như thế nào?

Tôi sửa bằng cách thêm ranh giới rõ hơn vào prompt và report. Thay vì để AI "tự xử lý sự cố", tôi giới hạn nhiệm vụ của AI thành: đọc thông tin sự cố, kiểm tra các điều kiện an toàn, chọn action phù hợp, và tạo draft cho điều phối viên duyệt.

Các boundary quan trọng tôi thêm vào gồm:

- Luôn bắt đầu tin nhắn bằng `[DRAFT_ONLY]`.
- Không được tự động gửi hướng dẫn cho tài xế khi chưa có human approval.
- Nếu pin dưới 5% và trạm sạc xa hơn 5km, không được đề xuất chạy tới trạm; phải đề xuất xe cứu hộ pin di động.
- Nếu dữ liệu GPS, loại xe hoặc trạng thái trạm sạc thiếu/không chắc chắn, AI phải yêu cầu điều phối viên xác minh thay vì tự đoán.

Tôi cũng sửa cách đánh giá AI Fit. Ban đầu tôi nghĩ dùng Agent sẽ hấp dẫn hơn, nhưng sau khi phân tích rủi ro, tôi thấy MVP nên là LLM Feature kết hợp rule/API. Quy trình có cấu trúc khá rõ, cần tốc độ và độ chính xác, nên Agent tự trị chưa cần thiết ở giai đoạn đầu.

## 5. Bài học cá nhân

Bài học lớn nhất của tôi là AI rất hữu ích để mở rộng góc nhìn, nhưng người làm product vẫn phải chịu trách nhiệm chốt scope. AI có thể giúp nghĩ nhanh, viết nhanh và phản biện nhanh, nhưng nếu tôi không kiểm tra lại bằng actor, workflow, metric và boundary thì bài toán dễ bị quá rộng hoặc thiếu an toàn.

Sau lab này, tôi hiểu hơn sự khác nhau giữa "ý tưởng AI hay" và "bài toán AI làm được". Một bài toán làm được phải có quy trình hiện tại rõ, bottleneck đo được, AI chỉ tham gia vào đúng bước có giá trị, và luôn có fallback khi AI sai. Với bài toán Xanh SM, tôi thấy hướng phù hợp nhất là GO cho MVP nhỏ: dùng rule/API để kiểm tra điều kiện an toàn, dùng LLM để soạn draft hướng dẫn, và giữ điều phối viên trong vòng phê duyệt cuối cùng.
