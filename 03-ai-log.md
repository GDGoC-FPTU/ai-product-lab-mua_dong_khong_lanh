### Name: Le Dam Quan - 2A202600930
# 📝 Phase 6 — Reflection (AI Log)

## Em đã dùng AI như “thought-partner” như thế nào?
- **Brainstorm & chọn bài toán (Phase 1–2)**: AI giúp tôi “đẩy nhanh” việc biến ý tưởng thô thành **Quick Problem Card** có workflow, actor, metric và kiến trúc (Rule/LLM/Agent). Nhờ vậy tôi không bị kẹt ở mô tả chung chung.
- **Chuẩn hóa Problem Statement (Phase 3.2)**: AI giúp viết lại nội dung theo đúng rubric 6-field (workflow, bottleneck, business impact, success metric, operational boundary) và “đóng khung” theo ngôn ngữ vận hành.
- **Prototype & kiểm chứng ranh giới (Phase 4)**: AI hỗ trợ debug lỗi môi trường Python/SDK và chỉnh script để chạy được trên autograder, đồng thời bổ sung thêm các ca tấn công (adversarial).
- AI giỏi ở tăng tốc viết nháp và “bắt form” theo rubric, nhưng dễ hallucinate chi tiết vận hành nếu mình không cung cấp số liệu/nguồn. Vì vậy cần khóa lại bằng: metric có số, workflow cụ thể, boundary + HITL.
- Khi làm prototype, rủi ro thường nằm ở môi trường chạy & integration (SDK, encoding, exit code) hơn là prompt. “Pass autograder” đòi hỏi kiểm tra rất thực dụng.