## Why

Mục `2.2.10. Số dư đầu kỳ` trong tài liệu nghiệp vụ hiện tại mới dừng ở nhóm thao tác nhập/import/kiểm tra/khóa, trong khi quá trình rà soát cho thấy còn thiếu các chức năng vận hành cần thiết như xem-sửa-xóa khi chưa khóa, mở khóa có kiểm soát, lịch sử thay đổi, export/báo cáo và đối chiếu chi tiết từng loại số dư.

Cần bổ sung đặc tả để tài liệu Phase 1 đủ rõ cho BA/dev/QA triển khai module Số dư đầu kỳ theo đúng nghiệp vụ kế toán, đồng thời không kéo quá sâu các nghiệp vụ thuộc Phase 2/3/6.

## What Changes

- Mở rộng đặc tả chức năng Số dư đầu kỳ trong `ACC-noi-dung-nghiep-vu-theo-phase.html` và `Phase1-nghiep-vu-lap-trinh.html`:
  - Bổ sung xem danh sách, lọc/tìm kiếm, sửa/xóa dữ liệu đầu kỳ khi chưa khóa.
  - Bổ sung download mẫu import, preview import, kiểm tra lỗi theo dòng/cột, file lỗi import.
  - Tách rõ các chức năng đối chiếu: TK tổng hợp, AR/AP, tồn kho, tiền mặt, ngân hàng, TSCĐ, CCDC, chi phí trả trước.
  - Bổ sung mở khóa số dư đầu kỳ có phân quyền, lý do, audit log và cảnh báo rủi ro.
  - Bổ sung lịch sử thay đổi, lịch sử import, lịch sử khóa/mở khóa.
  - Bổ sung in báo cáo và xuất Excel số dư đầu kỳ / kết quả đối chiếu.
- Bổ sung Use Case chi tiết cho “Nhập số dư đầu kỳ”:
  - Actor, điều kiện tiên quyết, luồng chính, luồng ngoại lệ.
  - Làm rõ trạng thái `chưa khóa` / `đã khóa` và điều kiện không được sửa/import.
- Bổ sung Business Rules cho module Số dư đầu kỳ:
  - Quyền thao tác, khóa/mở khóa, audit log.
  - Cân đối tổng Nợ/Có.
  - Đối chiếu chi tiết với TK 111/112/131/331/152/156/211/214/242.
  - Import all-or-nothing.
  - Không nhập/sửa khi đã phát sinh chứng từ kế toán liên quan.
- Làm rõ giới hạn Phase 1:
  - Công nợ AR/AP, tồn kho, TSCĐ, CCDC, CPTT chỉ nhập skeleton đầu kỳ và đối chiếu với sổ cái.
  - Không triển khai tuổi nợ đầy đủ, mua/bán/kho đầy đủ, khấu hao, phân bổ định kỳ, điều chuyển, thanh lý trong Phase 1.

## Capabilities

### New Capabilities
- `opening-balance-enhancement`: Bổ sung yêu cầu chi tiết cho quản lý, import, đối chiếu, khóa/mở khóa, lịch sử và báo cáo của module Số dư đầu kỳ Phase 1.

### Modified Capabilities
- (Không có — dự án chưa có capability gốc trong `openspec/specs/`, nên thay đổi này được ghi nhận như capability mới để làm rõ và mở rộng đặc tả Phase 1.)

## Impact

- Tài liệu nghiệp vụ chính: `ACC-noi-dung-nghiep-vu-theo-phase.html`, mục `2.2.10. Số dư đầu kỳ`.
- Tài liệu kỹ thuật lập trình: `Phase1-nghiep-vu-lap-trinh.html`, chương `Số dư đầu kỳ`.
- OpenSpec artifacts liên quan đến Phase 1 opening balance.
- Không thay đổi code ứng dụng trong proposal này; đây là thay đổi tài liệu/spec để chuẩn bị cho apply phase.
