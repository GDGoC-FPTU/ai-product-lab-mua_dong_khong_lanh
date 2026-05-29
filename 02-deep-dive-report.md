# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
* **Bài Toán**: Xe buýt điện VinBus bảo trì chủ yếu theo lịch km/checklist; cần dự báo lỗi pin, phanh, HVAC, cửa, motor, BMS sớm để giảm downtime và chi phí sửa ngoài kế hoạch.

* **Mô Tả Bài Toán**: Bảo trì định kỳ & xử lý lỗi sau khi phát sinh: kỹ thuật viên đọc log, checklist, báo lỗi tài xế, lịch bảo dưỡng cố định theo km. Vấn đề cần xử lí là khả năng dự đoán được việc bảo trì sớm trước để giúp giảm chi phí bảo trì, downtime ngoài kế hoạch, giảm lỗi bất ngờ. AI dự báo lỗi pin, phanh, HVAC, cửa, motor, BMS; scoring rủi ro theo xe; tự động tạo work order; dự báo phụ tùng; phân biệt lỗi thật và lỗi cảm biến.

Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên bảo trì VinBus |
| **2. Current Workflow** | (4–5 bước, chủ yếu reactive) <br>**(1)** Hệ thống telematics/OBD thu log + cảnh báo; tài xế báo lỗi qua app/điện thoại (mô tả triệu chứng). <br>**(2)** Kỹ thuật viên mở log theo xe, đọc chuỗi sự kiện + checklist bảo dưỡng theo km/thời gian (Excel/checklist giấy + phần mềm nội bộ). <br>**(3)** Đối chiếu báo cáo tài xế với dữ liệu cảm biến (BMS, phanh, HVAC, cửa, motor…) để xác định “lỗi thật” hay “lỗi cảm biến/false alarm”. <br>**(4)** Quyết định xử lý: xếp lịch vào xưởng, tạo phiếu công việc (work order), đặt phụ tùng theo kinh nghiệm/quy định. <br>**(5)** Nếu lỗi phát sinh bất ngờ trên tuyến: xử lý sự cố, kéo xe/đổi xe, sau đó mới sửa chữa & cập nhật hồ sơ. |
| **3. Bottleneck** | **Bước 2–3** là tốn thời gian và dễ sai nhất: đọc log rời rạc + đối chiếu đa nguồn (log, checklist, báo cáo tài xế, dữ liệu cảm biến) để chẩn đoán nguyên nhân. Thường mất **~25–40 phút/xe/lần**; dễ bỏ sót “pattern” cảnh báo sớm hoặc nhầm false alarm thành lỗi thật (và ngược lại). |
| **4. Business Impact** | **Downtime ngoài kế hoạch** làm giảm số xe sẵn sàng chạy tuyến, gây trễ chuyến/hủy chuyến và ảnh hưởng trải nghiệm hành khách. <br>**Chi phí bảo trì** tăng do xử lý sửa ngoài kế hoạch, kéo xe, overtime và thay thế phụ tùng không tối ưu. <br>**Rò rỉ năng suất kỹ thuật**: mỗi lần chẩn đoán 25–40 phút/xe, cộng dồn thành nhiều giờ công/ngày cho đội bảo trì; backlog tăng vào giờ cao điểm/đợt thời tiết xấu. <br> Nếu lấy chi phí bảo trì/khắc phục lỗi thận trọng 2.000–4.000 VND/km, với 19,3 triệu km/năm là 39–77 tỷ VND/năm. Chỉ 10–15% do thay thế sớm, downtime, lỗi lặp, thiếu phụ tùng đúng lúc đã tương đương 4–12 tỷ VND/năm. |
| **5. Success Metric** | **Efficiency**: Giảm thời gian chẩn đoán sơ bộ từ **~35 phút/xe → dưới 10 phút/xe** (đầu vào đủ log). <br>**Reliability**: Giảm tỉ lệ **sự cố ngoài kế hoạch** từ **~12% → dưới 5%** trên đội xe/tháng. <br>**Quality**: ≥ **80%** cảnh báo “rủi ro cao” do hệ thống đề xuất được **xác nhận đúng** sau khi kỹ thuật viên kiểm tra (precision cho nhóm high-risk). |
| **6. Operational Boundary** | **AI được phép**: <br>- Đọc/parse log & sự kiện telematics, tóm tắt theo timeline; nhận mô tả lỗi từ tài xế. <br>- Chấm điểm rủi ro theo xe/hệ thống (pin, phanh, HVAC, cửa, motor, BMS), gợi ý nguyên nhân khả dĩ và **đề xuất hành động** (kiểm tra gì trước, ưu tiên xe nào). <br>- Tạo **work order dạng nháp** và gợi ý phụ tùng/lịch bảo trì ưu tiên (draft). <br><br>**TUYỆT ĐỐI KHÔNG được**: <br>- Tự động cho xe **ngừng vận hành** / tự thay đổi lịch chạy tuyến / tự đặt mua phụ tùng / tự đóng ticket mà không có duyệt. <br>- Khẳng định chắc chắn nguyên nhân khi thiếu dữ liệu; không được “bịa” sensor value/log. <br><br>**Điểm cần duyệt (HITL)**: Kỹ thuật viên/Trưởng ca bắt buộc phê duyệt trước khi (1) phát hành work order chính thức, (2) đổi kế hoạch bảo trì, (3) đặt phụ tùng, (4) đưa xe ra khỏi tuyến. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [X] Rule / State-Machine [ ] LLM Feature [X] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---