## Why

Phase 2 hiện chỉ tồn tại như phần nội dung bên trong file tổng `ACC-noi-dung-nghiep-vu-theo-phase.html`, đủ ý nghiệp vụ nhưng chưa ở định dạng “bản đã duyệt” giống Phase 1 để kế toán, BA và đội triển khai đọc thống nhất. Cần tạo tài liệu Phase 2 riêng theo đúng khung Phase 1 để chuẩn hóa sơ đồ, luồng trạng thái, đặc tả module, định khoản và tiêu chí nghiệm thu.

## What Changes

- Tạo mới file HTML độc lập `ACC-dac-ta-nghiep-vu-phase-2.html` theo cùng phong cách trình bày đã duyệt của Phase 1: trang bìa, letterhead, bố cục A4, sơ đồ, bảng và phụ lục.
- Chuẩn hóa nội dung Phase 2 từ file nguồn hiện tại thành tài liệu riêng có cấu trúc: Mục 1 sơ đồ đặc tả nghiệp vụ + ma trận phạm vi, Mục 2 luồng trạng thái chứng từ + chú thích, Mục 3 đặc tả chi tiết theo module, phụ lục rules/định khoản/kết quả bàn giao/nghiệm thu.
- Biên tập lại các phần nghiệp vụ Phase 2 để bỏ lặp, gom nhóm và chuyển về đúng format dùng ở Phase 1: CRUD hoặc quản lý cấu hình dùng bảng STT; nghiệp vụ chứng từ và vận hành dùng bảng Use Case 8 cột.
- Chuẩn hóa toàn bộ chu trình mua hàng, nhập kho, hóa đơn đầu vào, công nợ phải trả, thanh toán nhà cung cấp, trả lại/giảm giá, bù trừ đối chiếu công nợ, quản lý kho và báo cáo để kế thừa logic của Phase 1 mà không mâu thuẫn với quỹ, ngân hàng và sổ cái.
- Bổ sung OpenSpec cho bộ tài liệu Phase 2 ở mức đủ rõ để triển khai việc tách file và chuẩn hóa nội dung trong bước apply.

## Capabilities

### New Capabilities
- `phase2-approved-document`: Tạo tài liệu Phase 2 độc lập, self-contained, A4-printable và đồng bộ định dạng với file Phase 1 đã duyệt.
- `phase2-procurement-detail`: Chuẩn hóa chi tiết các module mua hàng, hợp đồng mua, mua hàng hóa/dịch vụ, hóa đơn mua vào, công nợ phải trả và thanh toán nhà cung cấp theo format Phase 1.
- `phase2-inventory-detail`: Chuẩn hóa chi tiết các module nhận hàng, nhập kho, chuyển kho, kiểm kê, điều chỉnh tồn kho, thẻ kho và tồn kho theo format Phase 1.
- `phase2-reporting-controls`: Chuẩn hóa báo cáo Phase 2, bảng định khoản mẫu, business rules chung, kết quả bàn giao và tiêu chí nghiệm thu để đồng bộ với cách trình bày của Phase 1.

### Modified Capabilities
- None.

## Impact

- **File đầu ra mới**: `ACC-dac-ta-nghiep-vu-phase-2.html` tại thư mục gốc dự án, song song với `ACC-dac-ta-nghiep-vu-phase-1.html`.
- **Nguồn nội dung**: Phase 2 trong `ACC-noi-dung-nghiep-vu-theo-phase.html` sẽ được dùng làm nguồn để biên tập lại, không phải viết mới từ đầu.
- **Chuẩn tài liệu**: Kế thừa CSS, cấu trúc section, kiểu sơ đồ, cách đánh số và format bảng từ `ACC-dac-ta-nghiep-vu-phase-1.html`.
- **Ảnh hưởng chéo**: Cần giữ nhất quán với logic quỹ, ngân hàng và sổ cái của Phase 1 để các phần thanh toán, đối chiếu và ghi sổ không mâu thuẫn.
