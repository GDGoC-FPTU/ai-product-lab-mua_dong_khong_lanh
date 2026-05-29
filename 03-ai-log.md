# 03 - AI Log & Reflection

## Bối cảnh sử dụng AI

Trong bài lab này, tôi dùng AI như một thought-partner để hỗ trợ quá trình scoping sản phẩm AI cho Vin Smart Future. Mục tiêu không phải là để AI làm thay toàn bộ bài, mà là dùng AI để brainstorm, phản biện và chỉnh lại hướng chọn bài toán sao cho phù hợp hơn với tiêu chí "problem first, AI second".

---

## 1. AI đã giúp gì?

AI giúp tôi ở ba phần chính:

**Brainstorm bài toán vận hành.** Ban đầu tôi cần tìm nhiều bottleneck khác nhau trong các công ty thành viên Vingroup. AI giúp mở rộng danh sách ý tưởng sang nhiều mảng như Xanh SM, VinFast, Vinpearl, Vinhomes và Vinmec. Nhờ đó tôi có đủ lựa chọn cho Phase 1 thay vì chỉ bám vào một mảng quen thuộc.

**Cấu trúc hóa Quick Problem Cards.** AI giúp biến các ý tưởng thô thành card có đủ actor, workflow thủ công, bottleneck, bước AI có thể tham gia, metric thành công và quick architecture. Việc này giúp tôi nhìn rõ hơn bài toán nào chỉ là tự động hóa đơn giản, bài toán nào thật sự cần AI.

**Phản biện lựa chọn deep-dive.** Khi so sánh Card #1 "Xanh SM kiểm tra ảnh xe trước/sau ca" với Card #2 "VinFast rà soát hồ sơ claim bảo hành", AI giúp tôi diễn đạt lại lý do tại sao Card #1 hợp AI hơn: vision model xử lý ảnh xe và phát hiện bất thường là phần con người dễ bỏ sót, còn Card #2 chủ yếu là checklist có thể làm bằng rule engine.

---

## 2. AI đã sai hoặc chưa tốt ở đâu?

Điểm sai rõ nhất là lần đầu AI đề xuất một số bài toán khá giống ví dụ mẫu của đề bài, như phân loại phản ánh cư dân, mô tả lỗi xe hoặc tóm tắt xuất viện. Những ý tưởng này không sai về mặt nghiệp vụ, nhưng làm bài bị thiếu tính độc lập vì lặp lại pattern có sẵn trong worksheet/inspiration kit.

Điểm chưa tốt thứ hai là AI ban đầu đánh giá Card #2 VinFast claim bảo hành như một bài toán LLM tốt. Sau khi xem kỹ, tôi thấy phần lớn logic của bài này là kiểm tra checklist: có ảnh chưa, có số VIN chưa, có số km chưa, ngày mua có hợp lệ không, hồ sơ có thiếu giấy tờ không. Các bước này nên dùng rule-based system trước, không cần LLM làm trung tâm.

Điểm chưa tốt thứ ba là AI có xu hướng gắn nhãn "LLM Feature + Rule" cho nhiều bài toán. Nếu không phản biện lại, bài làm dễ rơi vào lỗi "AI-first", tức là cố dùng AI dù rule hoặc quy trình nghiệp vụ đơn giản đã đủ.

---

## 3. Tôi đã sửa đổi prompt/cách làm như thế nào?

Tôi điều chỉnh yêu cầu theo hướng cụ thể hơn:

- Yêu cầu AI tạo các bài toán khác với ví dụ mẫu, tránh lặp lại các use case đã có trong file đề.
- Yêu cầu so sánh rõ giữa Rule, LLM và Vision model thay vì mặc định chọn LLM.
- Yêu cầu đánh giá AI-fit dựa trên phần việc mà rule khó làm tốt, ví dụ nhận diện vết trầy, móp nhẹ, nội thất bẩn hoặc thiếu phụ kiện từ ảnh xe.
- Yêu cầu hạ Card #2 về hướng Rule-first vì đây là bài toán checklist rõ ràng.
- Yêu cầu đổi ứng viên deep-dive sang Card #1 vì vision model có vai trò rõ hơn và tạo giá trị khác biệt hơn.

Sau khi sửa, hướng chọn cuối cùng hợp lý hơn: Card #1 dùng AI để xử lý dữ liệu ảnh, còn rule chỉ kiểm tra các điều kiện cố định như đủ số ảnh, đúng góc chụp, đúng biển số và timestamp. Kết luận cuối vẫn do điều phối viên xác nhận, nên có human-in-the-loop để giảm rủi ro vận hành.

---

## 4. Bài học rút ra

Bài học lớn nhất là không nên chọn bài toán chỉ vì "có thể dùng AI". Một bài toán tốt cho AI cần có phần mà rule-based khó xử lý tốt, ví dụ dữ liệu ảnh, ngôn ngữ tự do, hoặc ngữ cảnh mơ hồ. Nếu bài toán chủ yếu là checklist rõ ràng, rule engine thường đơn giản hơn, rẻ hơn và dễ kiểm soát hơn.

Tôi cũng thấy AI hữu ích nhất khi được dùng để phản biện và tái cấu trúc suy nghĩ, không phải khi chấp nhận câu trả lời đầu tiên. Việc hỏi lại "bài này có thật sự cần AI không?" giúp tôi chọn được use case tốt hơn cho deep-dive và làm rõ ranh giới vận hành ngay từ đầu.
