## 🏛️ Bối cảnh: Tôi là ai?

Tôi là **Nam**, AI Engineer tại **Vin Smart Future**. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của **Xanh SM (GSM)** để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo. 

Thông qua khảo sát thực địa tại Trung tâm Điều vận Xanh SM Hà Nội, tôi nhận thấy các điều phối viên (Dispatchers) đang gặp một áp lực cực kỳ lớn vào giờ cao điểm, dẫn đến việc rò rỉ hiệu suất điều xe và tăng tỉ lệ khách hàng hủy chuyến. Bài toán tôi mang vào buổi Lab hôm nay đến từ chính quan sát thực tế này.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |Vinfast|Time-comsuming|Tổng hợp phân tích các loại xe khác nhau cho khách hàng mua được dễ hơn (VF8, VF7) về độ hài lòng của khách hàng khi mua các loại xe|
| 2 |Vinhome|Privacy|Hiện tại có rất nhiều đối tượng tội phạm, người lạ đi vào trong vinhome|
| 3 |XanhSM|Stakeholder Pain / AI-upgrade|Phân tích phản ánh chuyến đi và hành vi lái xe nguy hiểm để xác định khu vực/tài xế/tình huống có rủi ro cao
| 4 |Vinpearls|Repetitive|Trợ lý gợi ý lịch trình vui chơi theo độ tuổi, thời gian, ngân sách, thời tiết và mức đông khách
| 5 |Vinmec|Time-consuming|Tóm tắt hồ sơ bệnh án/lịch sử khám trước buổi khám cho bác sĩ, nhưng chỉ hỗ trợ đọc nhanh, không chẩn đoán|

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#2 (Vinfast tổng hợp phân tích), #4 (Vinhomes phát hiện tội phạm), #6 (Phân tích phản ánh chuyến đi).**

## Thẻ bài toán tiêu biểu: Card #2 — AI hỗ trợ phát hiện đối tượng tội phạm

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #_2__                                     │
│                                                             │
│ Bài toán (1 câu):  AI hỗ trợ ở bước phát hiện người/đối tượng có dấu hiệu trùng khớp với danh sách cảnh báo nội bộ đã được pháp lý phê duyệt. AI chỉ tạo cảnh báo rủi ro ban đầu; bảo vệ và cơ quan chức năng phải xác minh thủ công trước mọi hành động.
________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Cư dân xung quanh, bảo vệ, người đi đường, ban quản lý______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Truy cập vào camera xem có ai giống hình ảnh tội phạm không___ ──> 2. Ghi lại những người khả nghi___ ──> 3. Xác minh nhân thân, nhân tính trực tiếp___ ──> 4. _Báo công an, bắt giữ__                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? _1__ (⏱ _60__ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? AI hỗ trợ ở bước object detection, bằng cách kết hợp với dữ liệu truy nã quốc gia_____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian phản hồi xuống dưới 10 min______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [] Rule  [] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘
```