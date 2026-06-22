## 1. Chi tiết hóa workflow tổng và cụm hóa đơn điện tử

- [x] 1.1 Viết lại mục 6.1 Quy trình hóa đơn điện tử & thuế thành workflow tổng thể có trạng thái, điểm kiểm soát và liên kết giữa 6.2–6.9
- [x] 1.2 Viết lại mục 6.2 Kết nối nền tảng hóa đơn điện tử theo format Phase 1: mục tiêu, actor, use case, điều kiện, luồng chính, kết quả, workflow và business rules
- [x] 1.3 Viết lại mục 6.3 Quản lý hóa đơn đầu vào với use case có mã, actor, điều kiện, luồng xử lý, trạng thái, rule kiểm tra trùng/liên kết chứng từ và ảnh hưởng kế toán/thuế
- [x] 1.4 Viết lại mục 6.4 Quản lý hóa đơn đầu ra với use case có mã, liên kết chứng từ bán hàng/doanh thu/công nợ, workflow trạng thái và business rules
- [x] 1.5 Viết lại mục 6.5 Kiểm tra hợp lệ hóa đơn & cảnh báo rủi ro theo hướng control framework: tiêu chí kiểm tra, mức cảnh báo, kết quả xử lý và rule override
- [x] 1.6 Viết lại mục 6.6 Xử lý hóa đơn sai sót với luồng điều chỉnh/thay thế/hủy, liên kết hóa đơn gốc, hồ sơ xử lý, trạng thái và business rules

## 2. Chi tiết hóa cụm bảng kê, kê khai và nghĩa vụ thuế

- [x] 2.1 Viết lại mục 6.7 Bảng kê hóa đơn mua vào / bán ra với use case lập bảng kê, đối chiếu, xử lý thiếu/thừa, lọc, xuất và business rules chốt bảng kê
- [x] 2.2 Viết lại mục 6.8 Kê khai thuế & tờ khai thuế với use case đăng ký/lập/kiểm tra/chốt/xuất/tra cứu/điều chỉnh tờ khai, workflow versioning và business rules
- [x] 2.3 Viết lại mục 6.9 Giấy nộp tiền & báo cáo thuế với use case lập giấy nộp tiền, theo dõi trạng thái, đối chiếu nghĩa vụ thuế, liên kết thanh toán và báo cáo
- [x] 2.4 Bổ sung workflow và quy tắc truy vết từ hóa đơn → bảng kê → tờ khai → nghĩa vụ thuế → giấy nộp tiền → báo cáo/lưu hồ sơ

## 3. Định khoản, rules chung và nghiệm thu Phase 5

- [x] 3.1 Mở rộng Bảng định khoản mẫu — Giai đoạn 5 để bao phủ VAT đầu vào, VAT đầu ra, khấu trừ, nộp thuế, điều chỉnh VAT, hóa đơn điều chỉnh/thay thế/hủy và ghi chú kiểm soát
- [x] 3.2 Viết lại Quy tắc nghiệp vụ chung của Giai đoạn 5 với business rules có mã và phạm vi rõ ràng cho hóa đơn, kê khai, khóa kỳ, truy vết, phân quyền và cảnh báo
- [x] 3.3 Rà soát và cập nhật Kết quả bàn giao để phản ánh các phân hệ/use case chi tiết mới của Phase 5
- [x] 3.4 Viết lại Tiêu chí nghiệm thu theo từng phân hệ Phase 5, bao gồm happy path, cảnh báo sai lệch, trạng thái, đối chiếu và xuất dữ liệu/báo cáo

## 4. Cập nhật OpenSpec và rà soát cuối

- [x] 4.1 Hoàn thiện capability `phase5-einvoice-detail` theo nội dung HTML đã chi tiết hóa
- [x] 4.2 Hoàn thiện capability `phase5-tax-declaration-detail` theo nội dung HTML đã chi tiết hóa
- [x] 4.3 Hoàn thiện capability `phase5-reporting-controls-detail` theo nội dung HTML đã chi tiết hóa
- [x] 4.4 Cập nhật delta spec `general-ledger` để đồng bộ các điểm ghi sổ từ nghiệp vụ hóa đơn điện tử và thuế của Phase 5
- [x] 4.5 Đối chiếu toàn bộ Phase 5 với mục tiêu “chi tiết như Phase 1”, đảm bảo không còn section chỉ dừng ở bảng summary
- [x] 4.6 Kiểm tra HTML valid, không phát sinh nested table hoặc ảnh hưởng Phase 1–4 / Phase 6
- [x] 4.7 Xác nhận change ở trạng thái apply-ready sau khi hoàn tất artifacts
