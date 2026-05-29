# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinBus | Stakeholder Pain/Time-consuming | Bảo trì định kỳ & xử lý lỗi sau khi phát sinh: kỹ thuật viên đọc log, checklist, báo lỗi tài xế, lịch bảo dưỡng cố định theo km. Vấn đề cần xử lí là khả năng dự đoán được việc bảo trì sớm trước để giúp giảm chi phí bảo trì, downtime ngoài kế hoạch, giảm lỗi bất ngờ. AI dự báo lỗi pin, phanh, HVAC, cửa, motor, BMS; scoring rủi ro theo xe; tự động tạo work order; dự báo phụ tùng; phân biệt lỗi thật và lỗi cảm biến. |
| 2 | VinBus | Time-consuming | Xử lý phản ánh khách hàng thủ công: app/hotline/social nhận phản ánh về trễ chuyến, thái độ tài xế, bỏ bến, vệ sinh, mất đồ; nhân sự phải đọc, phân loại, tra camera/GPS rồi phản hồi. Bài toán vấn đề ở đây là cần làm một hệ thống AI tự động ghi nhận và xử lí các câu hỏi/phản ánh lặp lại, thường gặp; giúp cho việc giảm chi phí hỗ trợ, chăm sóc khách hàng. AI Complaint Triage + RAG Agent: tự phân loại phản ánh, map vào chuyến/xe/tài xế/điểm dừng, tóm tắt camera/GPS, gợi ý phản hồi, phát hiện cụm lỗi theo tuyến hoặc ca vận hành. |
| 3 | VinSpace | Time-consuming/Repetitive | Quản lý yêu cầu kỹ thuật, thay đổi thiết kế và traceability thủ công: requirement nằm rải rác trong Excel, Jira, Confluence, CAD note, email; kỹ sư phải tự đối chiếu impact giữa payload, power, thermal, ADCS, comms, mass budget |
| 4 | VinSpace | Time-consuming/Repetitive | Xử lý dữ liệu ảnh vệ tinh / payload data QC thủ công: kiểm tra ảnh cloud cover, blur, geolocation error, radiometric issue, duplicate scene; phân loại scene dùng được/không dùng được trước khi giao cho khách hàng hoặc team nội bộ |
| 5 | VinSpeed | Stakeholder Pain/Time-consuming | Lập kế hoạch bảo trì đường ray, điện kéo, tín hiệu, rolling stock theo lịch cố định: sau khi vận hành, nếu bảo trì chủ yếu theo checklist/time-based, sẽ có thay thế sớm, inspection thừa, hoặc lỗi phát sinh ngoài kế hoạch |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

**Top 3 đã chọn từ Phase 1:** **#1** (VinBus — dự báo bảo trì), **#2** (VinBus — phân loại phản ánh KH), **#4** (VinSpace — QC ảnh vệ tinh).

---

## Card #1 — VinBus: Dự báo bảo trì sớm (Predictive Maintenance)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Xe buýt điện VinBus bảo trì chủ yếu theo  │
│ lịch km/checklist; cần dự báo lỗi pin, phanh, HVAC, cửa,    │
│ motor, BMS sớm để giảm downtime và chi phí sửa ngoài kế    │
│ hoạch.                                                      │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: VinBus           │
│                                                             │
│ Ai đang đau (Actor)? Kỹ thuật viên bảo trì (đọc log thủ     │
│ công), điều hành vận tải (xe chết máy giữa tuyến), tài xế   │
│ (báo lỗi không được xử lý kịp), hành khách (trễ chuyến).   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Hệ thống/telematics ghi log + tài xế báo lỗi qua app   │
│   → 2. KTV đọc log, checklist, lịch bảo dưỡng cố định theo km│
│   → 3. Đối chiếu báo cáo tài xế vs dữ liệu cảm biến (thủ công)│
│   → 4. Lên lịch bảo trì / đặt phụ tùng theo quy trình cố định │
│   → 5. Sửa chữa khi xe đã hỏng hoặc đến hạn km (reactive)   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ 25–40 phút/xe) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4: scoring rủi ro│
│ theo xe, phân biệt lỗi thật vs cảm biến, tự tạo work order,  │
│ gợi ý phụ tùng và lịch bảo trì ưu tiên.                     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm sự cố ngoài kế hoạch từ ~12% ──> dưới 5% đội xe/tháng; │
│ giảm thời gian chẩn đoán từ 35 phút ──> dưới 10 phút/xe;    │
│ ≥80% cảnh báo có độ tin cậy cao được xác nhận đúng sau kiểm tra.│
│                                                             │
│ Quick Architecture: [x] Rule  [ ] LLM  [x] Agent             │
│ (ML/rule scoring + agent tạo WO; LLM chỉ tóm tắt log nếu cần)│
└─────────────────────────────────────────────────────────────┘
```

---

## Card #2 — VinBus: Phân loại & xử lý phản ánh khách hàng

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Phản ánh qua app/hotline/social (trễ      │
│ chuyến, thái độ tài xế, bỏ bến, vệ sinh, mất đồ) được xử lý │
│ thủ công — cần AI tự phân loại, map chuyến/xe và gợi ý phản hồi.│
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: VinBus           │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH (đọc/phân loại/tra GPS), │
│ trưởng ca vận hành (không thấy cụm lỗi theo tuyến), hành khách│
│ (chờ phản hồi 24–48h).                                      │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tiếp nhận phản ánh từ app, hotline, Facebook/Zalo       │
│   → 2. Nhân sự đọc, gắn nhãn loại (trễ/bỏ bến/thái độ/...)  │
│   → 3. Tra camera, GPS, lịch chuyến để xác minh thủ công    │
│   → 4. Soạn phản hồi và chuyển bộ phận xử lý (vận hành/HR)  │
│   → 5. Đóng ticket; tổng hợp báo cáo cụm lỗi cuối tuần      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–4 (⏱ 15–25 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4: Complaint   │
│ Triage + RAG — phân loại, map xe/tuyến/ca, tóm tắt GPS/camera,│
│ draft phản hồi, phát hiện cụm lỗi theo tuyến.               │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian xử lý phản ánh lặp từ 20 phút ──> dưới 5 phút;│
│ ≥85% phản ánh thường gặp được phân loại đúng trong 30 giây; │
│ giảm backlog ticket >24h từ 30% ──> dưới 10%.              │
│                                                             │
│ Quick Architecture: [ ] Rule  [x] LLM  [x] Agent             │
│ (Rule cho FAQ đơn giản; LLM+Agent cho phân loại, RAG, draft) │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #4 — VinSpace: QC dữ liệu ảnh vệ tinh / payload

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán (1 câu): Trước khi giao khách hoặc team nội bộ,    │
│ kỹ sư QC thủ công kiểm tra cloud cover, blur, geolocation,  │
│ radiometric, duplicate scene để phân loại scene dùng/không. │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: VinSpace           │
│                                                             │
│ Ai đang đau (Actor)? Kỹ sư xử lý ảnh / Data QC (lọc hàng    │
│ trăm scene/ngày), PM giao hàng (SLA trễ do QC tắc), khách   │
│ hàng B2B (nhận ảnh lỗi hoặc trễ).                           │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Payload downlink / ingest scene vào hệ thống nội bộ    │
│   → 2. Kỹ sư mở từng scene, kiểm tra metadata + xem trước ảnh│
│   → 3. Đánh nhãn Pass/Fail theo tiêu chí (mây, blur, geo...) │
│   → 4. Giao scene Pass cho khách/team analytics; Fail ghi log │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ 3–8 phút/scene) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: auto-score  │
│ chất lượng, gắn cờ duplicate/geolocation error, xếp hàng đợi │
│ ưu tiên review HITL cho case biên.                          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian QC trung bình từ 5 phút ──> dưới 1 phút/scene │
│ (auto-pass các scene rõ ràng); ≥92% scene auto-pass khớp    │
│ quyết định kỹ sư; giảm ảnh lỗi giao khách từ 2% ──> dưới 0,3%.│
│                                                             │
│ Quick Architecture: [x] Rule  [ ] LLM  [ ] Agent             │
│ (CV + rule threshold; LLM không cần thiết cho QC hình ảnh)   │
└─────────────────────────────────────────────────────────────┘
```

> **Ghi chú lựa chọn:** #3 (VinSpace traceability) và #5 (VinSpeed bảo trì đường ray) giữ lại cho deep-dive sau — #3 cần tích hợp nhiều nguồn tài liệu kỹ thuật; #5 tương tự #1 nhưng domain khác, ưu tiên VinBus vì có dữ liệu telematics + phản ánh KH sẵn hơn.

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
