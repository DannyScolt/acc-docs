## ADDED Requirements

### Requirement: Cụm vay, hợp đồng và e-banking của Phase 6 phải làm rõ trạng thái và phê duyệt theo từng cụm thao tác
Tài liệu Phase 6 SHALL tách rõ hơn các cụm khai báo, phê duyệt, theo dõi, thanh toán, đối chiếu và audit cho khoản vay, hợp đồng và ngân hàng điện tử.

#### Scenario: Review cấu trúc loan/contract/e-banking refine
- **WHEN** người dùng xem phần khế ước vay, hợp đồng hoặc ngân hàng điện tử
- **THEN** tài liệu SHALL thể hiện được các điểm trạng thái, phê duyệt, quyền thao tác và truy vết ở mức chi tiết hơn thay vì chỉ ở một khối mô tả tổng quát

## IMPLEMENTATION STATUS: DONE

- **7.5** (Khế ước vay): 7.5.1 Khai báo & lịch trả nợ (kế toán trưởng phê duyệt trước giải ngân) | 7.5.2 Giải ngân & theo dõi dư nợ | 7.5.3 Thanh toán / cảnh báo / báo cáo
- **7.6** (Hợp đồng): 7.6.1 Khai báo & mốc thanh toán | 7.6.2 Liên kết chứng từ & theo dõi thực hiện | 7.6.3 Cảnh báo & báo cáo
- **7.7** (Ngân hàng điện tử): 7.7.1 Kết nối & cấu hình (quản trị thiết lập, kế toán trưởng duyệt) | 7.7.2 Nhận giao dịch / tạo chứng từ / đối chiếu | 7.7.3 Khởi tạo & phê duyệt chuyển tiền (4-eyes: người khởi tạo ≠ người duyệt)

Quyền e-banking: tách biệt cấu hình (quản trị), khởi tạo lệnh (kế toán thanh toán) và phê duyệt lệnh (kế toán trưởng / người duyệt). Log audit bắt buộc tại mọi cụm.
