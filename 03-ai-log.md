## Nhật ký AI Log — Lab 02: AI Product Scoping

### 1. AI đã giúp gì cho tôi?

- **Brainstorm & cấu trúc bài toán VinBus Predictive Maintenance**  
  Tôi dùng AI để rà lại đề bài VinBus (bảo trì dự báo pin, phanh, HVAC, cửa, motor, BMS) và nhờ AI gợi ý cách diễn đạt lại thành **Problem Statement** có số liệu (tỉ lệ sự cố ngoài kế hoạch, thời gian chẩn đoán, độ chính xác cảnh báo). Nhờ đó, phần Phase 3 và Phase 5 của nhóm rõ ràng hơn, có metric cụ thể thay vì viết chung chung.
- **Ánh xạ bài toán vào rubric của lab**  
  AI giúp tôi đọc file `01-worksheet.md` và `02-deliverable-example.md`, sau đó đề xuất luôn cấu trúc tương tự cho Phase 5: AI Readiness Checklist → Quyết định GO/NOT YET/NO-GO → Justification theo logic “nghiệp vụ / kỹ thuật / ranh giới / chi phí”. Điều này giúp tôi tiết kiệm khá nhiều thời gian so với tự lần mò format.
- **Gợi ý nội dung chi tiết cho checklist & justification**  
  Khi tôi đưa Quick Problem Card #1 (VinBus) cho AI, AI gợi ý thêm các ý như: phạm vi pilot 30–50 xe, thời gian log tối thiểu 90 ngày, cách định nghĩa HITL & fallback, cũng như các rủi ro còn lại (false positive/false negative, data silo, niềm tin của KTV). Tôi tận dụng các gợi ý này để hoàn chỉnh phần Phase 5 cho nhóm.

### 2. AI sai hoặc chưa chuẩn ở đâu?

- **Giả định hơi “tự tin quá” về số liệu vận hành**  
  AI đưa ra một số con số giả định (ví dụ: 200 xe, 24 sự cố/tháng, chi phí 15–40 triệu/lần…) mà tôi không cung cấp từ trước. Các con số này hợp lý về logic nhưng lại không chắc trùng với thực tế của VinBus. Nếu tôi copy thẳng mà không ghi chú “giả định”, dễ bị hiểu nhầm là số liệu thật.
- **Đôi lúc over-engineering phần kiến trúc**  
  AI có xu hướng đề xuất kiến trúc khá đầy đủ (Rule + ML + Agent + LLM tóm tắt log). Với một bài lab thời lượng ngắn, nếu bám sát 100% đề xuất sẽ hơi “quá tải” so với yêu cầu tối thiểu của môn học (chỉ cần scoping bài toán và prototype prompt). Tôi phải tự cân nhắc cắt gọn những phần không cần thiết cho deliverable.

### 3. Tôi đã sửa/điều chỉnh như thế nào?

- **Rõ ràng hóa giả định**  
  Khi dùng các con số AI gợi ý, tôi coi đó là “placeholder” và chỉ giữ lại những gì hợp lý, đồng thời ghi rõ đây là giả định pilot (ví dụ: “Pilot đề xuất: 30–50 xe, 90 ngày log”). Nếu nhóm có số liệu thực, tôi sẽ thay thế lại để bài nộp sát thực tế hơn.
- **Rút gọn kiến trúc về đúng mức cần thiết**  
  Tôi không bê toàn bộ ý tưởng kiến trúc phức tạp vào bài nộp, mà chọn cách: giữ **Rule + ML scoring + Agent draft WO**, để phù hợp với Quick Card ban đầu (đã đánh dấu Rule + Agent, LLM chỉ optional để tóm tắt). Nhờ vậy, Phase 5 vẫn sâu sắc nhưng không “phô diễn công nghệ” quá mức.
- **Nhắc lại ranh giới vận hành của AI trong bài**  
  Dựa trên gợi ý của AI, tôi nhấn mạnh lại trong Justification và Checklist: AI chỉ được draft work order, luôn có HITL, có fallback khi thiếu dữ liệu, và không được quyết định an toàn (phanh/pin). Điều này biến các gợi ý rời rạc của AI thành bộ ranh giới vận hành rõ ràng, ăn khớp với yêu cầu “Operational Boundary” của môn học.

Tổng kết lại, AI đóng vai trò **thought-partner** khá hữu ích trong phần cấu trúc ý tưởng và diễn đạt, nhưng tôi phải luôn giữ vai trò “editor/engineer cuối” để kiểm tra sự hợp lý của số liệu, mức độ phức tạp kiến trúc, và tính phù hợp với rubric môn học.

