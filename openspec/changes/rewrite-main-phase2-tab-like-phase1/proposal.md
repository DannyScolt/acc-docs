## Why

Sau khi tab Phase 1 trong `ACC-noi-dung-nghiep-vu-theo-phase.html` đã được thay bằng bản Phase 1 chuẩn hóa, tab Phase 2 hiện lộ rõ là vẫn ở trạng thái nội dung raw: mở đầu bằng flow tóm tắt ngắn, đi thẳng vào danh sách chức năng và use case chi tiết dài, thiếu cặp sơ đồ tổng quan + ma trận phạm vi + luồng trạng thái chứng từ theo đúng nhịp tài liệu approved.

Cần viết lại trực tiếp tab Phase 2 trong file chính để nó đạt cùng đẳng cấp trình bày với tab Phase 1: cùng logic chương mục, cùng cách dẫn nhập, cùng tầng tổng quan/kiểm soát/chi tiết, nhưng vẫn giữ mô hình một file HTML duy nhất theo tab thay vì tạo file Phase 2 riêng.

## What Changes

- Cập nhật trực tiếp tab Phase 2 trong `ACC-noi-dung-nghiep-vu-theo-phase.html`, không tạo file `ACC-dac-ta-nghiep-vu-phase-2.html` mới trong phạm vi change này.
- Viết lại phần đầu tab Phase 2 theo cùng pattern với tab Phase 1 mới: phase header, intro card, lộ trình, sơ đồ đặc tả nghiệp vụ chi tiết, ma trận phạm vi module, luồng trạng thái chứng từ và bảng chú thích.
- Chuẩn hóa phần đặc tả module của Phase 2 để bỏ lặp giữa “danh sách chức năng”, “bộ trạng thái”, “use case chi tiết” và các đoạn tóm tắt raw hiện tại.
- Dùng đúng quy ước đã áp dụng cho Phase 1:
  - phần quản lý / cấu hình / CRUD tổng hợp dùng bảng STT,
  - phần nghiệp vụ chứng từ, vận hành và báo cáo dùng bảng Use Case 8 cột.
- Gom lại nội dung Phase 2 thành các cụm module đọc được như một tài liệu approved, đồng thời giữ nhất quán với logic quỹ, ngân hàng và sổ cái của Phase 1 cho các chỗ thanh toán, đối chiếu và ghi sổ.
- Giữ nguyên kiến trúc tabbed single-file document: tab navigation, anchor `#phase-2`, wrapper `tab-phase-2`, các tab khác và appendix không bị ảnh hưởng.

## Capabilities

### New Capabilities
- `main-phase2-approved-tab`: Tab Phase 2 trong file chính hiển thị nội dung đã được biên tập lại theo chuẩn approved giống tab Phase 1.
- `phase2-approved-structure`: Phase 2 có đầy đủ các lớp tổng quan, kiểm soát và chi tiết gồm sơ đồ nghiệp vụ, ma trận module, trạng thái chứng từ, đặc tả module và phụ lục.
- `phase2-single-file-consistency`: Chuẩn hóa Phase 2 ngay trong file tổng để cùng hệ trình bày với Phase 1 mà không lệch sang mô hình nhiều file.

### Modified Capabilities
- `tabbed-phase-document`: Nâng chuẩn tab Phase 2 để đồng bộ với tab Phase 1 mới bên trong cùng tài liệu theo tab.

## Impact

- **File chính bị chỉnh sửa**: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- **Nguồn tham chiếu cấu trúc**: tab Phase 1 đã approved trong chính file tổng, và `ACC-dac-ta-nghiep-vu-phase-1.html` như reference phụ cho format.
- **Không tạo file đầu ra mới trong scope change này**: thay đổi tập trung vào tab Phase 2 hiện có.
- **Ảnh hưởng trình bày**: tab Phase 2 sẽ thay đổi mạnh về bố cục, cách đánh số, cách gom module và loại bảng.
- **Ảnh hưởng chéo cần giữ nhất quán**: các phần công nợ, thanh toán, ghi sổ, kho và báo cáo phải không mâu thuẫn với logic Phase 1 đã được approved trong file chính.
