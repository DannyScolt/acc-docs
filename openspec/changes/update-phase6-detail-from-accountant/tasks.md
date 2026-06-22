## 1. Chi tiết hóa cụm tài sản và phân bổ

- [x] 1.1 Viết lại mục 7.1 Tài sản cố định theo format Phase 1: mục tiêu, actor, use case có mã, điều kiện, luồng chính, kết quả, workflow, business rules và ảnh hưởng kế toán
- [x] 1.2 Viết lại mục 7.2 Công cụ dụng cụ & chi phí trả trước với hai luồng nghiệp vụ rõ cho CCDC và chi phí trả trước, bao gồm kỳ phân bổ, trạng thái và rules đối chiếu giá trị còn lại
- [x] 1.3 Mở rộng phần báo cáo / đối chiếu của tài sản và phân bổ để liên kết được với sổ cái và chứng từ nguồn

## 2. Chi tiết hóa cụm lương và giá thành

- [x] 2.1 Viết lại mục 7.3 Tiền lương cơ bản phục vụ hạch toán với use case nhập bảng lương, phân bổ lương, hạch toán, trả lương, đối chiếu đã trả/chưa trả và giới hạn phạm vi HRM
- [x] 2.2 Viết lại mục 7.4 Giá thành sản xuất với use case tập hợp chi phí, phân bổ chi phí chung, xác định dở dang, tính giá thành, kết chuyển và rules cần tính lại khi dữ liệu nguồn thay đổi
- [x] 2.3 Bổ sung ảnh hưởng kế toán, workflow trạng thái và tiêu chí đối chiếu cho cụm lương / giá thành

## 3. Chi tiết hóa cụm vay, hợp đồng và ngân hàng điện tử

- [x] 3.1 Viết lại mục 7.5 Khế ước vay với use case khoản vay, lãi suất, giải ngân, trả nợ, chi phí lãi vay, cảnh báo đến hạn và báo cáo dư nợ
- [x] 3.2 Viết lại mục 7.6 Hợp đồng với use case mốc thanh toán, liên kết hóa đơn, liên kết thu chi, theo dõi thực hiện và cảnh báo đến hạn / quá hạn
- [x] 3.3 Viết lại mục 7.7 Ngân hàng điện tử với use case kết nối, tra cứu giao dịch, khởi tạo / duyệt giao dịch, tạo chứng từ, đối chiếu sổ phụ và xử lý giao dịch lệch
- [x] 3.4 Bổ sung business rules về phân quyền, trạng thái giao dịch, log xử lý và điều kiện tự động hạch toán cho e-banking

## 4. Chi tiết hóa quản trị nâng cao và tổng hợp Phase 6

- [x] 4.1 Viết lại mục 7.8 để tách rõ dashboard quản trị, phân tích tài chính, dự báo dòng tiền và ngân sách như các scope vận hành riêng bên trong cùng một heading
- [x] 4.2 Mở rộng Bảng định khoản mẫu — Giai đoạn 6 để bao phủ ghi tăng/ghi giảm tài sản, khấu hao, phân bổ, lương, giá thành, vay và e-banking
- [x] 4.3 Viết lại Quy tắc nghiệp vụ chung của Giai đoạn 6 với business rules có mã cho truy vết bút toán, khóa kỳ, phân quyền, phê duyệt và độ tin cậy dữ liệu quản trị
- [x] 4.4 Cập nhật Kết quả bàn giao để phản ánh rõ các phân hệ/use case chi tiết mới của Phase 6
- [x] 4.5 Viết lại Tiêu chí nghiệm thu theo từng cụm module Phase 6, bao gồm happy path, trạng thái, cảnh báo, đối chiếu và báo cáo đầu ra

## 5. Đồng bộ OpenSpec và rà soát cuối

- [x] 5.1 Hoàn thiện capability `phase6-asset-allocation-detail` theo nội dung HTML đã chi tiết hóa
- [x] 5.2 Hoàn thiện capability `phase6-payroll-costing-detail` theo nội dung HTML đã chi tiết hóa
- [x] 5.3 Hoàn thiện capability `phase6-loan-contract-ebanking-detail` theo nội dung HTML đã chi tiết hóa
- [x] 5.4 Hoàn thiện capability `phase6-management-reporting-detail` theo nội dung HTML đã chi tiết hóa
- [x] 5.5 Cập nhật delta spec `general-ledger` để đồng bộ các điểm ghi sổ và quy tắc khóa kỳ / truy vết từ Phase 6
- [x] 5.6 Đối chiếu toàn bộ Phase 6 với mục tiêu “chi tiết như Phase 1”, đảm bảo không còn section chỉ dừng ở bảng summary
- [x] 5.7 Kiểm tra HTML valid, không phát sinh nested table hoặc ảnh hưởng phần reconciliation / footer / các phase khác
- [x] 5.8 Xác nhận change ở trạng thái apply-ready sau khi hoàn tất artifacts
