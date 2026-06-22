## Why

Phase 2 trong HTML hiện mới ở mức bảng chức năng tóm tắt, chưa đủ chi tiết để bộ phận kế toán review quy trình nghiệp vụ hoặc để đội triển khai dùng làm đặc tả thống nhất như Phase 1. Cần nâng toàn bộ Phase 2 lên cùng mức chi tiết với Phase 1 để loại bỏ việc phải tự suy diễn luồng, trạng thái, business rules và ảnh hưởng kế toán.

## What Changes

- Viết lại các section nghiệp vụ chính của Phase 2 theo format chi tiết giống Phase 1: danh sách use case, actor, điều kiện, dữ liệu đầu vào, luồng chính, kết quả, workflow và business rules.
- Chi tiết hóa cụm **mua hàng & công nợ phải trả** cho các mục 3.2 đến 3.10, bao gồm yêu cầu mua, đơn mua, hợp đồng mua, mua hàng hóa/dịch vụ, hóa đơn mua vào, công nợ phải trả, thanh toán nhà cung cấp, trả lại hàng mua và đối chiếu công nợ.
- Chi tiết hóa cụm **kho của Phase 2** cho các mục 3.5 và 3.11.1 đến 3.11.4, bao gồm nhận hàng/nhập kho, chuyển kho, kiểm kê, điều chỉnh tồn và thẻ kho/tồn kho.
- Chi tiết hóa cụm **báo cáo, định khoản và quy tắc chung Phase 2** cho mục 3.12, bảng định khoản mẫu, quy tắc nghiệp vụ chung, kết quả bàn giao và tiêu chí nghiệm thu.
- Bổ sung/cập nhật OpenSpec để phản ánh đầy đủ yêu cầu Phase 2 ở mức có thể dùng làm cơ sở triển khai và kiểm thử.

## Capabilities

### New Capabilities
- `phase2-procurement-detail`: Chi tiết hóa nghiệp vụ mua hàng, hợp đồng, hóa đơn đầu vào, công nợ phải trả và thanh toán nhà cung cấp trong Phase 2.
- `phase2-inventory-detail`: Chi tiết hóa nghiệp vụ nhận hàng, nhập kho, chuyển kho, kiểm kê và tồn kho trong Phase 2.
- `phase2-reporting-detail`: Chi tiết hóa báo cáo, định khoản mẫu, quy tắc chung và tiêu chí nghiệm thu của Phase 2.

### Modified Capabilities
- `general-ledger`: Mở rộng các yêu cầu liên quan ghi sổ từ nghiệp vụ mua hàng, công nợ phải trả và kho của Phase 2 khi mức chi tiết nghiệp vụ được bổ sung.

## Impact

- **HTML**: `ACC-noi-dung-nghiep-vu-theo-phase.html` phần Phase 2 sẽ được viết lại sâu hơn, đặc biệt các section 3.2 đến 3.12.
- **Spec**: Change mới sẽ bổ sung các capability riêng cho nghiệp vụ Phase 2 và có thể cần delta spec cho `general-ledger` để phản ánh logic ghi sổ liên quan.
- **Phụ thuộc nghiệp vụ**: Cần giữ đồng bộ với mức chi tiết đã có ở Phase 1 (quỹ, ngân hàng, sổ cái) để các luồng thanh toán, công nợ và ghi sổ không mâu thuẫn nhau.
