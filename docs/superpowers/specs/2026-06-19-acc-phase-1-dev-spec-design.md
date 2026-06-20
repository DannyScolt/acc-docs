# ACC Phase 1 Developer-Facing Business Logic Document Design

## 1. Mục tiêu
Tạo một file HTML riêng tên `ACC-nghiep-vu-lap-trinh-phase-1.html` để mô tả nghiệp vụ lập trình cho Phase 1 của ACC. Tài liệu này dùng cho BA, dev, tester và reviewer nghiệp vụ đọc trước khi triển khai, không thay thế file scope nghiệp vụ hiện tại dành cho kế toán.

## 2. Nguồn tham chiếu
- File scope hiện tại: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- Chỉ lấy nội dung thuộc Phase 1
- Không kéo nội dung Phase 2, 3, 5, 6 vào tài liệu mới, trừ phần ghi chú ngoài phạm vi

## 3. Kết quả đầu ra
Tạo một file HTML tĩnh:
- `ACC-nghiep-vu-lap-trinh-phase-1.html`

File phải:
- đọc tốt trên browser
- có CSS inline, không cần build step
- đủ gọn để gửi review
- vẫn đủ cấu trúc để dev/tester bám triển khai
- hỗ trợ in hoặc export PDF tương đối ổn

## 4. Phạm vi nội dung
### 4.1 Có trong Phase 1
- Quản lý doanh nghiệp
- Người dùng, vai trò, phân quyền, audit log
- Hệ thống tài khoản và các danh mục nền dùng chung
- Nhập số dư đầu kỳ và khóa số dư đầu kỳ
- Phiếu thu, phiếu chi tiền mặt
- Thu ngân hàng, chi ngân hàng, chuyển tiền nội bộ
- Ghi sổ kế toán cơ bản
- Sổ quỹ, sổ tiền gửi, sổ cái, nhật ký chung, bảng cân đối phát sinh

### 4.2 Ngoài phạm vi
- Mua hàng chi tiết
- Bán hàng chi tiết
- Kho chi tiết và nghiệp vụ nhập xuất kho đầy đủ
- Thuế, hóa đơn điện tử, kê khai thuế
- TSCĐ, CCDC, chi phí trả trước ở mức quản lý đầy đủ
- Các quy trình chuyên sâu của các phase sau

## 5. Cách tổ chức tài liệu
Tài liệu HTML sẽ có 6 phần chính:
1. Cover page và metadata tài liệu
2. Mục tiêu, đối tượng đọc, phạm vi, ngoài phạm vi
3. Quy ước chung của Phase 1
4. Nhóm use case nền tảng
5. Nhóm use case giao dịch và sổ sách
6. Phần tổng hợp cuối file

## 6. Mức độ chi tiết
Để tránh file quá dài, tài liệu không tách thành quá nhiều tiểu use case nhỏ. Thay vào đó, nội dung được gom theo nhóm nghiệp vụ có thể build được.

Các nhóm use case chính:
1. Quản trị doanh nghiệp
2. Người dùng, vai trò, phân quyền, audit log
3. Hệ thống tài khoản và danh mục nền
4. Nhập số dư đầu kỳ và khóa số dư
5. Phiếu thu và phiếu chi tiền mặt
6. Thu ngân hàng, chi ngân hàng, chuyển tiền nội bộ
7. Ghi sổ kế toán và các sổ/báo cáo cơ bản

## 7. Template chuẩn cho mỗi use case
Mỗi use case chỉ giữ các block cần thiết sau:
- Mục tiêu
- Actor
- Màn hình cần có
- Dữ liệu đầu vào
- Luồng xử lý chính
- Quy tắc nghiệp vụ chính
- Trạng thái dữ liệu/chứng từ
- Kết quả sau xử lý / sổ báo cáo ảnh hưởng
- Quyền thao tác
- Lỗi / cảnh báo chính
- Điều kiện nghiệm thu

Template này được giữ ngắn, ưu tiên bảng bullet rõ hơn là mô tả dài.

## 8. Các phần tổng hợp cuối file
Cuối tài liệu sẽ có các phần sau ở mức gọn:
- Ma trận phân quyền theo vai trò chính
- Ma trận định khoản mặc định cho nghiệp vụ Phase 1
- Checklist đối chiếu cuối Phase 1
- Danh sách điểm cần reviewer/kế toán xác nhận

## 9. Nguyên tắc trình bày
- Reuse tinh thần trình bày từ file HTML hiện tại
- Dùng heading rõ ràng, bảng ngắn, callout cho các lưu ý quan trọng
- Không biến tài liệu thành thiết kế kỹ thuật DB/API
- Không biến tài liệu thành bản scope cấp cao quá chung chung
- Nội dung phải đủ để người đọc hiểu “cần build gì” và “hệ thống phải xử lý ra sao”

## 10. Quy ước nghiệp vụ chung cần thể hiện
Phần quy ước đầu file sẽ chốt các nguyên tắc dùng chung:
- Ngày chứng từ và ngày hạch toán
- Luồng trạng thái chuẩn: Nháp → Chờ duyệt → Đã duyệt/Ghi sổ → Đã hủy
- Chỉ chứng từ hợp lệ mới được ghi sổ
- Chứng từ đã duyệt không sửa trực tiếp; muốn chỉnh phải hủy hoặc tạo nghiệp vụ điều chỉnh theo rule được mô tả
- Mọi thao tác quan trọng phải có nhật ký truy vết
- Dữ liệu chỉ hiển thị và thao tác theo phạm vi phân quyền

## 11. Cách triển khai HTML
File HTML sẽ dùng:
- một trang cover ngắn
- khối mục lục nhanh ở đầu file
- section card cho từng nhóm use case
- bảng cho các block input/rule/permission/acceptance
- CSS inline để dễ gửi và không phụ thuộc môi trường build

## 12. Tiêu chí hoàn thành
Thiết kế được xem là hoàn thành khi file HTML sau này đáp ứng đủ các điểm:
- Có thể mở độc lập trên browser
- Giới hạn đúng Phase 1
- Có cấu trúc use-case-based
- Có quy ước chung rõ ràng
- Có các ma trận/checklist tổng hợp cuối file
- Ngắn hơn tài liệu full-spec nhưng đủ cho BA/dev/tester/reviewer dùng làm tài liệu review triển khai
