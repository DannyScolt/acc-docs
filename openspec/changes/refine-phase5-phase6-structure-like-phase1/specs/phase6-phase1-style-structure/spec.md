## ADDED Requirements

### Requirement: Phase 6 phải được tái cấu trúc theo cách đọc giống Phase 1
Tài liệu Phase 6 SHALL giữ nguyên các module nâng cao chính nhưng phải được chia nhỏ thành các cụm vận hành hoặc tiểu mục rõ hơn để người đọc có thể review từng phần như cách Phase 1 trình bày các phân hệ con.

#### Scenario: Review cấu trúc mới của Phase 6
- **WHEN** người dùng đọc lại Phase 6 trong HTML
- **THEN** họ SHALL thấy các module lớn như tài sản, phân bổ, giá thành, e-banking và quản trị nâng cao được tách thành các đơn vị review nhỏ hơn thay vì chỉ là một bảng lớn cho mỗi mục

### Requirement: Phase 6 phải có workflow tổng thể ở cấp chapter
Tài liệu Phase 6 SHALL bổ sung một lớp workflow tổng thể giúp người đọc hiểu mối liên hệ giữa các module nâng cao trước khi đi vào từng module chi tiết.

#### Scenario: Review flow tổng thể của Phase 6
- **WHEN** người dùng đọc phần đầu của Phase 6
- **THEN** tài liệu SHALL mô tả được cách các cụm tài sản, phân bổ, lương, giá thành, vay, hợp đồng, e-banking và quản trị nâng cao liên hệ với nhau trong vận hành tổng thể

### Requirement: Phase 6 phải làm rõ quyền và trạng thái cho các module nhạy cảm
Tài liệu Phase 6 SHALL mô tả rõ hơn các điểm quyền xem / sửa / duyệt / override đối với lương, e-banking, vay nợ và ngân sách.

#### Scenario: Review quyền xử lý trong Phase 6
- **WHEN** người dùng xem các mục lương, e-banking, khế ước vay hoặc ngân sách
- **THEN** tài liệu SHALL thể hiện được các điểm quyền và trạng thái xử lý ở mức cụm nghiệp vụ thay vì chỉ ở rule chung toàn phase

## IMPLEMENTATION STATUS: DONE

Các thay đổi đã thực hiện trong `ACC-noi-dung-nghiep-vu-theo-phase.html`:

- **7.0** (Workflow tổng thể Giai đoạn 6): section mới mô tả luồng liên hệ giữa tất cả các module Phase 6
- **7.1** (Tài sản cố định): tách thành 7.1.1 Ghi tăng & khai báo, 7.1.2 Khấu hao định kỳ, 7.1.3 Điều chỉnh / điều chuyển / đánh giá lại, 7.1.4 Ghi giảm & kiểm kê
- **7.2** (CCDC & CPTT): tách thành 7.2.1 Ghi tăng & khai báo phân bổ, 7.2.2 Phân bổ định kỳ & theo dõi giá trị còn lại, 7.2.3 Điều chỉnh / ngừng phân bổ & kiểm kê
- **7.3** (Tiền lương cơ bản): tách thành 7.3.1 Khai báo & nhập liệu bảng lương, 7.3.2 Phân bổ chi phí lương & hạch toán, 7.3.3 Trả lương & đối chiếu đã trả / chưa trả
- **7.4** (Giá thành sản xuất): tách thành 7.4.1 Khai báo đối tượng & tập hợp chi phí, 7.4.2 Phân bổ chi phí chung & xác định dở dang, 7.4.3 Tính giá thành / kết chuyển & báo cáo
- **7.5** (Khế ước vay): tách thành 7.5.1 Khai báo khoản vay & lịch trả nợ, 7.5.2 Giải ngân & theo dõi dư nợ, 7.5.3 Thanh toán gốc / lãi / cảnh báo & báo cáo
- **7.6** (Hợp đồng): tách thành 7.6.1 Khai báo & mốc thanh toán, 7.6.2 Liên kết chứng từ & theo dõi thực hiện, 7.6.3 Cảnh báo đến hạn & báo cáo
- **7.7** (Ngân hàng điện tử): tách thành 7.7.1 Kết nối & cấu hình, 7.7.2 Nhận giao dịch / tạo chứng từ / đối chiếu, 7.7.3 Khởi tạo & phê duyệt chuyển tiền
- **7.8** (Dashboard / phân tích / dự báo / ngân sách): tách thành 7.8.1 Dashboard & phân tích tài chính, 7.8.2 Dự báo dòng tiền, 7.8.3 Ngân sách / theo dõi thực hiện / cảnh báo vượt ngân sách

Mỗi cụm con đều có hàng **Actor & Quyền** rõ ràng; các module nhạy cảm (lương, e-banking, vay nợ, ngân sách) nêu rõ quyền xem / sửa / duyệt riêng biệt tại từng cụm.
