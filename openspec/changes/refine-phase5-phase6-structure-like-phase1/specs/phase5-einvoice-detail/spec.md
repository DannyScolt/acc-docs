## ADDED Requirements

### Requirement: Các phân hệ hóa đơn điện tử của Phase 5 phải được chia thành cụm vận hành nhỏ hơn
Tài liệu Phase 5 SHALL trình bày các mục kết nối, hóa đơn đầu vào, hóa đơn đầu ra, kiểm tra rủi ro và xử lý sai sót bằng nhiều cụm nghiệp vụ nhỏ hơn bên trong mỗi phân hệ lớn để tăng khả năng review và kiểm thử.

#### Scenario: Review cấu trúc e-invoice refine
- **WHEN** người dùng xem các mục 6.2 đến 6.6
- **THEN** tài liệu SHALL cho phép tách biệt rõ các cụm như tiếp nhận, tra cứu, liên kết chứng từ, kiểm tra, xử lý sai sót, lịch sử và quyền xử lý thay vì gom tất cả trong một block lớn

## IMPLEMENTATION STATUS: DONE

- **6.2**: 6.2.1 Cấu hình kết nối & xác thực | 6.2.2 Đồng bộ & nhận dữ liệu | 6.2.3 Lịch sử truyền nhận & đồng bộ lại lỗi
- **6.3**: 6.3.1 Tiếp nhận & tra cứu hóa đơn đầu vào | 6.3.2 Kiểm tra hợp lệ & liên kết chứng từ | 6.3.3 Trạng thái xử lý & lưu hồ sơ
- **6.4**: 6.4.1 Tạo & phát hành HĐĐT đầu ra | 6.4.2 Liên kết bán hàng / doanh thu / công nợ | 6.4.3 Cảnh báo & trạng thái xử lý
- **6.5**: 6.5.1 Kiểm tra tự động & phân loại cảnh báo (3 mức: Thông tin / Kiểm soát / Chặn) | 6.5.2 Xử lý sai sót & override có kiểm soát
- **6.6**: 6.6.1 Hóa đơn điều chỉnh & thay thế | 6.6.2 Hóa đơn hủy & xử lý sau hủy

Mỗi cụm có hàng Actor & Quyền phân biệt vai trò thực thi / phê duyệt / override.
