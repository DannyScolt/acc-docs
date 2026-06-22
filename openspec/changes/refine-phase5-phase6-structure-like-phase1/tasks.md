## 1. Tái cấu trúc Phase 5 theo nhịp đọc của Phase 1

- [x] 1.1 Viết lại mục 6.2 thành các cụm vận hành nhỏ hơn như cấu hình kết nối, xác thực, đồng bộ, lịch sử truyền nhận và đồng bộ lại lỗi
- [x] 1.2 Viết lại mục 6.3 thành các cụm nhỏ hơn cho tiếp nhận hóa đơn đầu vào, tra cứu/chi tiết, liên kết chứng từ, kiểm tra trùng/sai lệch, trạng thái xử lý và lưu hồ sơ
- [x] 1.3 Viết lại mục 6.4 thành các cụm nhỏ hơn cho tiếp nhận hóa đơn đầu ra, liên kết bán hàng/doanh thu/công nợ, cảnh báo bán chưa có hóa đơn và trạng thái xử lý
- [x] 1.4 Viết lại mục 6.5 và 6.6 theo các cụm kiểm tra / cảnh báo / override / xử lý sai sót nhỏ hơn thay vì mỗi mục chỉ là một block lớn
- [x] 1.5 Viết lại các mục 6.7 đến 6.9 để tách rõ cụm lập bảng kê, rà soát sai lệch, chốt bảng kê, lập tờ khai, chốt tờ khai, nộp thuế, điều chỉnh và báo cáo

## 2. Bổ sung lớp quyền và control cho Phase 5

- [x] 2.1 Bổ sung rõ quyền đồng bộ, kiểm tra, xác nhận cảnh báo, override, chốt bảng kê, chốt tờ khai và lập giấy nộp tiền theo từng cụm nghiệp vụ Phase 5
- [x] 2.2 Cập nhật workflow tổng, rule chung, kết quả bàn giao và tiêu chí nghiệm thu của Phase 5 để phản ánh cấu trúc mới đã chia nhỏ hơn

## 3. Tái cấu trúc Phase 6 theo nhịp đọc của Phase 1

- [x] 3.1 Bổ sung một lớp workflow tổng thể cho cả Phase 6 trước hoặc cùng với các module chi tiết
- [x] 3.2 Viết lại cụm 7.1 và 7.2 thành các đơn vị review nhỏ hơn như ghi tăng, phân bổ, khấu hao, điều chỉnh, kiểm kê và báo cáo
- [x] 3.3 Viết lại cụm 7.3 và 7.4 thành các cụm nhỏ hơn cho khai báo, nhập liệu, phân bổ, đối chiếu, tính toán, kết chuyển và cảnh báo
- [x] 3.4 Viết lại cụm 7.5 đến 7.7 thành các cụm nhỏ hơn cho khai báo, phê duyệt, thanh toán, đối chiếu, log và audit
- [x] 3.5 Tách mục 7.8 thành các scope review rõ hơn cho dashboard, phân tích tài chính, dự báo dòng tiền, ngân sách, theo dõi thực hiện và cảnh báo vượt ngân sách

## 4. Bổ sung lớp quyền và control cho Phase 6

- [x] 4.1 Bổ sung rõ quyền xem / sửa / duyệt / override cho các module nhạy cảm như lương, e-banking, vay nợ và ngân sách
- [x] 4.2 Cập nhật bảng định khoản, rule chung, kết quả bàn giao và tiêu chí nghiệm thu của Phase 6 để phản ánh cấu trúc refine và các checkpoint chi tiết hơn

## 5. Đồng bộ OpenSpec và rà soát cuối

- [x] 5.1 Hoàn thiện capability `phase5-phase1-style-structure` theo nội dung HTML đã refine
- [x] 5.2 Hoàn thiện capability `phase6-phase1-style-structure` theo nội dung HTML đã refine
- [x] 5.3 Đồng bộ các delta `phase5-einvoice-detail`, `phase5-tax-declaration-detail`, `phase5-reporting-controls-detail` theo cấu trúc mới của Phase 5
- [x] 5.4 Đồng bộ các delta `phase6-asset-allocation-detail`, `phase6-payroll-costing-detail`, `phase6-loan-contract-ebanking-detail`, `phase6-management-reporting-detail` theo cấu trúc mới của Phase 6
- [x] 5.5 Cập nhật delta `general-ledger` để phản ánh rõ hơn các checkpoint ghi sổ, phê duyệt và khóa kỳ sau khi refine cấu trúc
- [x] 5.6 Rà soát lại Phase 5 và Phase 6 với benchmark “đọc giống Phase 1”, đảm bảo không còn mục lớn nào chỉ là một block dày chữ khó review
- [x] 5.7 Kiểm tra HTML không phát sinh nested table, không làm hỏng tab structure và không ảnh hưởng phần reconciliation / footer / các phase khác
