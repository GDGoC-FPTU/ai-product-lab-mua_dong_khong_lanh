Tên nhóm: mua_dong_khong_lanh
Họ tên: Nguyễn Tiến Đạt
Email: 26ai.datnt5@vinuni.edu.vn
# 01 - Problem Scan: Vin Smart Future

File này hoàn thiện Phase 1 (SCAN) và Phase 2 (QUICK-ASSESS) cho Lab 02 - AI Product Scoping.

---

# Phase 1 - SCAN: Tìm kiếm cơ hội

## List bài toán của tôi

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Vinhomes | Tốn thời gian | Ban quản lý phải đọc ảnh chụp đồng hồ điện/nước do kỹ thuật viên gửi, nhập số thủ công vào file đối soát và kiểm tra bất thường theo từng căn hộ. |
| 2 | VinFast | AI-upgrade | Nhân viên kho phụ tùng phải tìm linh kiện thay thế tương thích khi mã phụ tùng cũ hết hàng, bằng cách tra nhiều file catalog và hỏi kỹ thuật viên. |
| 3 | Vinmec | Stakeholder Pain | Tổng đài đặt lịch phải nghe mô tả nhu cầu khám của khách, hỏi lại nhiều câu và chọn gói khám phù hợp; khách lớn tuổi thường phải chờ lâu hoặc đặt nhầm chuyên khoa. |
| 4 | Xanh SM | Lặp lại | Đội vận hành phải kiểm tra ảnh xe trước/sau ca của tài xế để phát hiện trầy xước, thiếu phụ kiện hoặc nội thất bẩn trước khi bàn giao ca mới. |
| 5 | Vinpearl | Tốn thời gian | Bộ phận F&B phải tổng hợp yêu cầu ăn kiêng/dị ứng thực phẩm của khách đoàn từ email, form đặt tiệc và ghi chú lễ tân để chuyển cho bếp. |
| 6 | Vinhomes | Stakeholder Pain | Nhân viên an ninh phải xác minh thủ công danh sách khách/shipper đăng ký vào tòa, đối chiếu biển số, căn hộ, thời gian vào và ghi nhận ngoại lệ. |
| 7 | VinFast | Lặp lại | Đội bảo hành phải rà soát hồ sơ claim gồm ảnh, biên bản, số km, ngày mua và lịch sử sửa chữa để phát hiện hồ sơ thiếu giấy tờ trước khi gửi duyệt. |
| 8 | Vinpearl | AI-upgrade | Lễ tân phải gợi ý lịch trình trong khu nghỉ dưỡng cho từng nhóm khách dựa trên tuổi, thời tiết, thời gian check-in/check-out và tình trạng đông ở từng điểm dịch vụ. |

---

# Phase 2 - QUICK-ASSESS: 3 Quick Problem Cards

Từ danh sách scan, tôi chọn 3 bài toán tiềm năng nhất để đánh giá nhanh:

| Card | Bài toán | Lý do chọn |
|---|---|---|
| #1 | Xanh SM kiểm tra ảnh xe trước/sau ca | Tần suất cao, dữ liệu ảnh rõ ràng; vision model có thể phát hiện vết trầy/móp/bẩn mà con người dễ bỏ sót khi giao ca đông. |
| #2 | VinFast rà soát hồ sơ claim bảo hành | Có giá trị vận hành nhưng thiên về rule/checklist; phù hợp làm baseline rule hơn là ứng viên deep-dive AI tốt nhất. |
| #3 | Vinpearl tổng hợp yêu cầu ăn kiêng/dị ứng cho bếp | Tác động trực tiếp đến trải nghiệm khách đoàn và an toàn dịch vụ, phù hợp LLM trích xuất thông tin từ text. |

---

## Quick Problem Card #1 - Xanh SM kiểm tra ảnh xe trước/sau ca

| Trường | Nội dung |
|---|---|
| Bài toán | Tự động hỗ trợ kiểm tra ảnh xe Xanh SM trước/sau ca để phát hiện trầy xước, móp nhẹ, nội thất bẩn hoặc thiếu phụ kiện. |
| Công ty thành viên | Xanh SM |
| Ai đang đau? | Điều phối viên bãi xe, tổ trưởng tài xế và tài xế nhận ca sau. |
| Workflow thủ công hiện tại | 1. Tài xế kết thúc ca chụp ảnh 4 góc xe và nội thất -> 2. Điều phối viên mở từng ảnh để so với checklist -> 3. Nếu nghi ngờ có lỗi, điều phối viên nhắn lại tài xế xác minh -> 4. Điều phối viên ghi biên bản bàn giao hoặc cho phép xe vào ca mới -> 5. Tổ trưởng xử lý tranh chấp nếu tài xế sau phát hiện lỗi. |
| Bước tốn thời gian/lỗi nhất | Bước 2-3: xem ảnh thủ công và phát hiện lỗi nhỏ; khoảng 7-10 phút/xe, dễ bỏ sót vết trầy nhỏ khi giờ giao ca có nhiều xe. |
| AI hỗ trợ ở bước nào? | Bước 2-3: vision model đánh dấu vùng ảnh nghi ngờ bất thường, gợi ý loại lỗi và tạo checklist nháp để điều phối viên xác nhận. |
| Metric thành công | Giảm thời gian kiểm tra ảnh từ 8 phút xuống dưới 2 phút/xe; phát hiện ít nhất 90% lỗi ngoại thất rõ trên ảnh; giảm 40% tranh chấp bàn giao ca liên quan tình trạng xe. |
| Quick Architecture | LLM/Vision Feature + Rule. Vision model phát hiện điểm bất thường; rule kiểm tra đủ số ảnh, góc chụp, biển số, thời điểm chụp; điều phối viên duyệt kết luận cuối. |

**Ghi chú ranh giới:** AI không được tự kết luận tài xế chịu trách nhiệm bồi thường, không được khóa xe khỏi vận hành nếu chưa có điều phối viên xác nhận. Ảnh thiếu sáng/mờ phải yêu cầu chụp lại thay vì đoán.

---

## Quick Problem Card #2 - VinFast rà soát hồ sơ claim bảo hành

| Trường | Nội dung |
|---|---|
| Bài toán | Hỗ trợ đội bảo hành VinFast kiểm tra hồ sơ claim trước khi gửi duyệt để phát hiện thiếu giấy tờ, thiếu ảnh hoặc thông tin mâu thuẫn. |
| Công ty thành viên | VinFast |
| Ai đang đau? | Nhân viên bảo hành, cố vấn dịch vụ tại xưởng và bộ phận phê duyệt claim. |
| Workflow thủ công hiện tại | 1. Cố vấn dịch vụ gom ảnh, biên bản kiểm tra, số VIN, số km, ngày mua, lịch sử sửa chữa -> 2. Nhân viên bảo hành đối chiếu checklist claim -> 3. Nếu thiếu thông tin, hồ sơ bị trả về xưởng bổ sung -> 4. Nhân viên sửa lại hồ sơ và gửi duyệt lần nữa -> 5. Bộ phận phê duyệt ra quyết định. |
| Bước tốn thời gian/lỗi nhất | Bước 2-4: kiểm tra checklist và phát hiện thiếu/mâu thuẫn dữ liệu; khoảng 15-25 phút/hồ sơ, hồ sơ bị trả về làm chậm tiến độ bảo hành. |
| AI hỗ trợ ở bước nào? | Bước 2-3: ưu tiên rule engine kiểm tra checklist bắt buộc theo loại claim; LLM chỉ là tùy chọn nếu hồ sơ có ghi chú tự do cần tóm tắt hoặc chuẩn hóa. |
| Metric thành công | Giảm thời gian rà soát hồ sơ từ 20 phút xuống dưới 6 phút; giảm 50% tỷ lệ hồ sơ bị trả về do thiếu giấy tờ; 95% hồ sơ gửi duyệt có đủ trường bắt buộc. |
| Quick Architecture | Rule-first. Rule kiểm tra checklist cố định theo loại claim, định dạng file, trường bắt buộc và điều kiện mâu thuẫn đơn giản; LLM chỉ hỗ trợ phần ghi chú tự do nếu thật sự cần. Người phụ trách bảo hành xác nhận trước khi gửi duyệt. |

**Ghi chú ranh giới:** AI không được tự phê duyệt hoặc từ chối bảo hành, không được sửa số liệu gốc, không được suy đoán lỗi kỹ thuật nếu hồ sơ thiếu bằng chứng. AI chỉ được đánh dấu rủi ro và tạo checklist nháp.

---

## Quick Problem Card #3 - Vinpearl tổng hợp yêu cầu ăn kiêng/dị ứng cho bếp

| Trường | Nội dung |
|---|---|
| Bài toán | Tự động tổng hợp yêu cầu ăn kiêng, dị ứng thực phẩm và ghi chú đặc biệt của khách đoàn để chuyển cho bếp Vinpearl trước giờ phục vụ. |
| Công ty thành viên | Vinpearl |
| Ai đang đau? | Nhân viên F&B, bếp trưởng, lễ tân đoàn và khách có yêu cầu ăn uống đặc biệt. |
| Workflow thủ công hiện tại | 1. Sale/booking nhận email hoặc form đặt tiệc từ đoàn -> 2. Lễ tân bổ sung ghi chú khi khách check-in -> 3. Nhân viên F&B đọc nhiều nguồn và nhập lại vào bảng tổng hợp -> 4. Bếp trưởng lọc các case dị ứng/người ăn chay/trẻ em -> 5. F&B xác nhận lại với trưởng đoàn trước giờ ăn. |
| Bước tốn thời gian/lỗi nhất | Bước 3-4: tổng hợp ghi chú phân tán và phân biệt dị ứng thật với sở thích ăn uống; khoảng 20-30 phút/đoàn, rủi ro bỏ sót dị ứng nghiêm trọng. |
| AI hỗ trợ ở bước nào? | Bước 3-4: LLM trích xuất tên khách/phòng, loại yêu cầu, mức độ rủi ro, bữa ăn áp dụng và tạo bảng tổng hợp rõ cho bếp; các dị ứng nghiêm trọng được gắn cờ cần xác nhận lại. |
| Metric thành công | Giảm thời gian tổng hợp yêu cầu từ 25 phút xuống dưới 5 phút/đoàn; 100% yêu cầu dị ứng được gắn cờ để người phụ trách xác nhận; giảm 80% lỗi nhập lại thông tin giữa booking và bếp. |
| Quick Architecture | LLM Feature + Rule. LLM trích xuất từ email/form/ghi chú; rule gắn cờ các từ khóa dị ứng nghiêm trọng như hải sản, đậu phộng, gluten; F&B xác nhận trước khi chuyển bếp. |

**Ghi chú ranh giới:** AI không được tự xác nhận thực đơn an toàn thay cho bếp trưởng, không được bỏ qua yêu cầu dị ứng mơ hồ. Các trường hợp không chắc chắn phải được gắn nhãn "cần xác minh với khách/trưởng đoàn".

---

## Đánh giá nhanh sau Phase 2

| Tiêu chí | Card #1 Xanh SM | Card #2 VinFast | Card #3 Vinpearl |
|---|---:|---:|---:|
| Tần suất sử dụng | Cao | Trung bình-cao | Cao |
| Rủi ro khi AI sai | Trung bình | Cao | Cao |
| Dữ liệu đầu vào sẵn có | Ảnh xe, timestamp, biển số, checklist ca | Hồ sơ claim, ảnh, biên bản, metadata xe | Email/form đặt tiệc, ghi chú lễ tân, danh sách khách |
| Cần Human-in-the-loop | Có | Bắt buộc | Bắt buộc |
| Phù hợp prototype nhanh | Cao | Trung bình | Cao |

**Ứng viên nên chọn để deep-dive:** Card #1 - Xanh SM kiểm tra ảnh xe trước/sau ca.

Lý do: bài toán có dữ liệu ảnh rõ ràng và vision model giải quyết đúng phần con người dễ bỏ sót: phát hiện vết trầy, móp nhẹ, nội thất bẩn hoặc thiếu phụ kiện từ ảnh bàn giao. Rule chỉ phù hợp để kiểm tra đủ số ảnh, góc chụp, biển số và thời điểm chụp; phần nhận diện bất thường trên ảnh là nơi AI tạo khác biệt rõ. Quy trình vẫn có điều phối viên duyệt kết luận cuối nên rủi ro vận hành được kiểm soát bằng human-in-the-loop.
