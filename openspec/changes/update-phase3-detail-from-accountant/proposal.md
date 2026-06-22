## Why

Phase 3 trong HTML hiện mới ở mức bảng chức năng tóm tắt, chưa đủ chi tiết để kế toán review chu trình bán hàng hoặc để đội triển khai dùng như đặc tả nghiệp vụ thống nhất giống Phase 1. File nguồn từ bộ phận kế toán đã cung cấp đầy đủ use case, business rule, trạng thái, bút toán và liên kết phân hệ cho Phase 3, nên cần cập nhật lại toàn bộ phần này theo đúng độ sâu của tài liệu nguồn.

## What Changes

- Viết lại toàn bộ Phase 3 trong HTML theo format chi tiết giống Phase 1, thay cho cấu trúc summary `STT / Chức năng / Mô tả` hiện tại.
- Chi tiết hóa các phân hệ bán hàng từ **4.2 đến 4.12** theo DOCX nguồn, bao gồm: báo giá, đơn đặt hàng bán, hợp đồng bán, chính sách giá, bán hàng hóa/dịch vụ, hóa đơn bán ra, xuất kho bán hàng, hàng bán bị trả lại & giảm giá hàng bán, công nợ phải thu, thu tiền khách hàng và báo cáo bán hàng/doanh thu/công nợ phải thu.
- Cập nhật lại cấu trúc và numbering của Phase 3 để bám sát tài liệu nguồn, bao gồm việc bỏ cấu trúc tách riêng `4.9 Tính giá vốn hàng bán`, `4.11 Bù trừ công nợ & đối trừ chứng từ`, `4.13 Báo cáo...` trong HTML hiện tại nếu chúng không còn khớp với source-of-truth từ kế toán.
- Bổ sung cho từng module: business rules có mã, danh sách use case chi tiết, actor, luồng chính, kết quả đầu ra, luồng trạng thái, liên kết dữ liệu với phân hệ khác và bút toán kế toán phát sinh khi nguồn có cung cấp.
- Cập nhật OpenSpec để phản ánh đầy đủ yêu cầu Phase 3 ở mức có thể dùng làm cơ sở triển khai, kiểm thử và review nghiệp vụ.

## Capabilities

### New Capabilities
- `phase3-sales-detail`: Chi tiết hóa nghiệp vụ báo giá, đơn đặt hàng bán, hợp đồng bán, bán hàng hóa/dịch vụ và các luồng chứng từ bán của Phase 3.
- `phase3-pricing-and-invoicing-detail`: Chi tiết hóa chính sách giá, bảng giá, chiết khấu, hóa đơn bán ra và các quy tắc điều chỉnh/đối chiếu hóa đơn của Phase 3.
- `phase3-fulfillment-and-receivables-detail`: Chi tiết hóa xuất kho bán hàng, hàng bán bị trả lại & giảm giá hàng bán, công nợ phải thu, thu tiền khách hàng và báo cáo Phase 3.

### Modified Capabilities
- `general-ledger`: Mở rộng các yêu cầu liên quan ghi sổ từ nghiệp vụ doanh thu, thuế GTGT đầu ra, giá vốn, công nợ phải thu, thu tiền và giảm trừ doanh thu khi Phase 3 được chi tiết hóa theo tài liệu kế toán.

## Impact

- **HTML**: `ACC-noi-dung-nghiep-vu-theo-phase.html` phần Phase 3 sẽ được viết lại sâu hơn, đặc biệt các section [4.2](ACC-noi-dung-nghiep-vu-theo-phase.html:2279) đến [4.13](ACC-noi-dung-nghiep-vu-theo-phase.html:2440) hiện tại.
- **OpenSpec**: Cần thêm các capability spec mới cho nghiệp vụ Phase 3 và cập nhật delta spec `general-ledger` để đồng bộ logic ghi sổ liên quan.
- **Cấu trúc tài liệu**: Numbering và grouping của các chương bán hàng có thể thay đổi để khớp tài liệu DOCX accountant, tránh lệch giữa HTML và source-of-truth.
- **Phụ thuộc nghiệp vụ**: Cần giữ đồng bộ với Phase 1 (quỹ, ngân hàng, sổ cái) và Phase 2 (kho / mua hàng) để các luồng công nợ, xuất kho, thu tiền và ghi sổ không mâu thuẫn.