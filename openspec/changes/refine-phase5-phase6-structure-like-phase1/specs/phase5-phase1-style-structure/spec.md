## ADDED Requirements

### Requirement: Phase 5 phải được tái cấu trúc theo cách đọc giống Phase 1
Tài liệu Phase 5 SHALL giữ nguyên các phân hệ nghiệp vụ chính nhưng phải được trình bày lại với nhiều lớp cấu trúc hơn, bao gồm các tiểu mục hoặc cụm vận hành nhỏ hơn bên trong các heading lớn để người dùng có thể review từng phần giống cách đọc Phase 1.

#### Scenario: Review cấu trúc mới của Phase 5
- **WHEN** người dùng đọc lại Phase 5 trong HTML
- **THEN** họ SHALL thấy các cụm nghiệp vụ hóa đơn và thuế được chia thành các đơn vị review nhỏ hơn thay vì chỉ là một bảng lớn cho mỗi mục chính

### Requirement: Phase 5 phải thể hiện rõ phân quyền, phê duyệt và override theo cụm nghiệp vụ
Tài liệu Phase 5 SHALL mô tả rõ hơn ai được đồng bộ, kiểm tra, xác nhận cảnh báo, chốt bảng kê, chốt tờ khai, lập giấy nộp tiền hoặc override kiểm soát trong các cụm nghiệp vụ thuế và hóa đơn.

#### Scenario: Review quyền xử lý trong Phase 5
- **WHEN** người dùng xem các cụm xử lý hóa đơn, bảng kê, tờ khai và nộp thuế
- **THEN** tài liệu SHALL phân biệt rõ các vai trò và điểm phê duyệt thay vì chỉ nhắc quyền ở mức chung chung

## IMPLEMENTATION STATUS: DONE

Các thay đổi đã thực hiện trong `ACC-noi-dung-nghiep-vu-theo-phase.html`:

- **6.2** (Kết nối nền tảng HĐĐT): tách thành 6.2.1 Cấu hình kết nối & xác thực, 6.2.2 Đồng bộ & nhận dữ liệu, 6.2.3 Lịch sử truyền nhận & đồng bộ lại lỗi
- **6.3** (Xử lý hóa đơn đầu vào): tách thành 6.3.1 Tiếp nhận & tra cứu, 6.3.2 Kiểm tra hợp lệ & liên kết chứng từ, 6.3.3 Trạng thái xử lý & lưu hồ sơ
- **6.4** (Xử lý hóa đơn đầu ra): tách thành 6.4.1 Tạo & phát hành HĐĐT, 6.4.2 Liên kết bán hàng / doanh thu / công nợ, 6.4.3 Cảnh báo & trạng thái xử lý
- **6.5** (Kiểm tra & cảnh báo): tách thành 6.5.1 Kiểm tra tự động & phân loại cảnh báo, 6.5.2 Xử lý sai sót & override có kiểm soát
- **6.6** (Hóa đơn đặc thù): tách thành 6.6.1 Hóa đơn điều chỉnh & thay thế, 6.6.2 Hóa đơn hủy & xử lý sau hủy
- **6.7** (Bảng kê thuế): tách thành 6.7.1 Lập & rà soát bảng kê, 6.7.2 Chốt bảng kê & đối chiếu
- **6.8** (Tờ khai thuế): tách thành 6.8.1 Lập tờ khai, 6.8.2 Chốt tờ khai & nộp thuế, 6.8.3 Điều chỉnh tờ khai & bổ sung
- **6.9** (Báo cáo thuế): tách thành 6.9.1 Báo cáo kiểm soát nội bộ, 6.9.2 Báo cáo nộp cơ quan thuế

Mỗi cụm con đều có hàng **Actor & Quyền** rõ ràng thay vì chỉ liệt kê actor ở mức tổng.
