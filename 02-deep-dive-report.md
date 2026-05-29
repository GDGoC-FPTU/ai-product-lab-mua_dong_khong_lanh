# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = 12 phút/lượt**.

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
---

# 🏁 Phase 5 — EVALUATE (Nhóm): VinBus Predictive Maintenance

## AI Readiness Checklist

| # | Tiêu chí | Đánh giá | Bằng chứng / Ghi chú |
|---|----------|:--------:|----------------------|
| 1 | Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? | [x] Có một phần (đủ cho pilot hẹp) | VinBus có telematics/BMS (SOC, cell imbalance, nhiệt độ pack), DTC phanh/HVAC/cửa/motor, log tài xế qua app. **Thiếu:** bộ nhãn lỗi chuẩn (fault label) gắn với sự cố thực tế sau sửa và đồng bộ thời gian giữa cảm biến ↔ WO/CMMS. **Pilot đề xuất:** 30–50 xe, ưu tiên 2 subsystem (pin + phanh), tối thiểu 90 ngày log. |
| 2 | Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? | [x] Có | Scoring/rule **không** tự đưa xe vào bảo trì ngoài lịch; Agent chỉ tạo **draft** work order (WO) + gợi ý phụ tùng. KTV/Trưởng ca **bắt buộc duyệt** trước khi lên lịch. **Fallback:** confidence thấp / dữ liệu thiếu → “manual review”, giữ quy trình checklist theo km như hiện tại. Alert safety-critical (phanh/pin nhiệt bất thường) → **luôn** escalate ngay, không chờ batch. |
| 3 | Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? | [x] Có điều kiện | **Ủng hộ:** điều hành vận tải (giảm xe chết máy giữa tuyến), ban vận hành (SLA chuyến). **Cần change mgmt:** KTV quen đọc log thủ công → training 1–2 tuần + KPI pilot tập trung “giảm thời gian chẩn đoán”, tránh framing “thay thế KTV”. Tài xế: cần SLA xử lý báo lỗi app ≤24h để đối chiếu với cảm biến. |

**Tóm tắt checklist:** Đủ điều kiện **GO pilot hẹp**; chưa đủ để rollout toàn đội xe nếu chưa có baseline 3 tháng và nhãn lỗi tối thiểu cho các lỗi phổ biến.

---

## Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

- [x] **GO (Bắt đầu xây dựng Prototype):** bắt đầu với **scope hẹp**, không triển khai toàn mạng ngay.
- [ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** chọn nếu chưa truy cập được nguồn dữ liệu tối thiểu (telematics/BMS + lịch sử WO/CMMS).
- [ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** không chọn vì quy trình cần xếp hạng rủi ro đa nguồn và orchestration WO; rule-only không giải quyết tốt bước 2–4 ở quy mô đội xe.

---

## Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí)

### 1) Căn cứ nghiệp vụ (gắn metric có số)

- **Bottleneck rõ:** bước 2–3 tốn **25–40 phút/xe** (đọc log, đối chiếu báo lỗi tài xế vs cảm biến).
- **Mục tiêu đo lường (theo Card #1):**
  - Giảm sự cố ngoài kế hoạch: **~12% → <5%** đội xe/tháng
  - Giảm thời gian chẩn đoán: **35 phút → <10 phút/xe**
  - **≥80%** cảnh báo confidence cao được xác nhận đúng sau kiểm tra

→ Nếu pilot đạt giảm ≥30% sự cố khẩn trên nhóm xe pilot và rút ngắn chẩn đoán ≥40%, dự án có cơ sở mở rộng.

### 2) Căn cứ kỹ thuật (AI Fit đúng mức)

- **Rule/threshold (ưu tiên an toàn):** DTC critical, nhiệt độ pack bất thường, tín hiệu phanh nguy hiểm → luôn escalate theo ngưỡng OEM/quy định nội bộ.
- **ML scoring (nhẹ):** xếp hạng rủi ro 7/14/30 ngày theo xe (ví dụ: SOC drop nhanh, cell imbalance tăng, nhiệt độ lệch…).
- **Agent (hẹp):** tạo **draft** WO, đề xuất phụ tùng và slot bảo trì theo ưu tiên rủi ro; không tự động gửi WO nếu chưa duyệt.
- **LLM (tùy chọn):** chỉ dùng để tóm tắt log dài, giải thích “vì sao” cảnh báo; **không** dùng LLM để ra quyết định an toàn phanh/pin.

### 3) Operational Boundary (điều kiện để GO an toàn)

- **AI được phép:** scoring rủi ro; phân biệt lỗi thật vs nhiễu cảm biến; tạo draft WO; gợi ý phụ tùng; tóm tắt log.
- **AI tuyệt đối không được:** tự ý cho xe “dừng khai thác”; tự đặt phụ tùng vượt ngưỡng chi phí; override quyết định KTV/Trưởng ca; bỏ qua checklist an toàn.
- **HITL bắt buộc:** mọi WO ngoài lịch km; mọi cảnh báo **Critical**.
- **Fallback:** confidence < 0.7 hoặc thiếu ≥2 nguồn tín hiệu quan trọng → “Manual — full checklist”.

### 4) Scope pilot đề xuất (8–10 tuần)

1. **Tuần 1–2:** baseline (tần suất sự cố ngoài kế hoạch, thời gian chẩn đoán, tỉ lệ cảnh báo đúng nếu có).
2. **Tuần 3–5:** rule engine + risk dashboard (pin + phanh); tích hợp read-only telematics + CMMS/WO.
3. **Tuần 6–8:** agent draft WO + màn hình duyệt; chạy A/B 30 xe pilot vs 30 xe control (nếu đủ xe).
4. **Tuần 9–10:** review metric; quyết định mở rộng sang HVAC/cửa/motor hoặc chuyển NOT YET để tích lũy nhãn.

### 5) Rủi ro còn lại & cách giảm

- **False positive → bảo trì thừa:** đặt ngưỡng confidence; audit precision; bắt buộc HITL.
- **False negative → hỏng giữa tuyến:** rule cứng cho safety-critical; không tắt cảnh báo OEM.
- **Data silo / lệch timestamp:** chuẩn hóa time sync + audit trail + mapping sự kiện ↔ WO.
- **KTV thiếu niềm tin:** hiển thị “vì sao” (rule id/feature), không dùng black-box thuần.
