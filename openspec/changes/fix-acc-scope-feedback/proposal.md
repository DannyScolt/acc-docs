## Why

Tài liệu phạm vi nghiệp vụ ACC (`ACC-noi-dung-nghiep-vu-theo-phase.html`) nhận feedback từ reviewer kế toán (Mạnh Tâm Acc). Tài liệu này dùng để gửi cho kế toán đọc và phản hồi, nhưng hiện tại có 2 vấn đề chính: (1) phần định khoản Nợ/Có — cốt lõi mà kế toán cần xác nhận — chỉ được ghi bằng một dòng notice thụ động, không có bảng mẫu để kế toán biết cần điền gì; (2) mục nhập số dư đầu kỳ liệt kê nhập chi tiết công nợ, tồn kho, TSCĐ nhưng không ghi rõ đây chỉ là opening balance, module quản lý đầy đủ nằm ở phase sau — gây nhầm lẫn cho kế toán đọc.

## What Changes

- Biến notice thụ động ở trang Overview (dòng 543-545) thành khung yêu cầu phản hồi nổi bật (dùng class `.report-note` thay `.notice`), nhấn mạnh định khoản Nợ/Có là phần cốt lõi cần kế toán xác nhận.
- Thêm bảng định khoản mẫu (Nghiệp vụ / TK Nợ / TK Có / Ghi chú) vào cuối mỗi phase (6 bảng), với các nghiệp vụ chính và số tài khoản mẫu theo TT99 để kế toán kiểm tra, bổ sung, điều chỉnh.
- Bổ sung ghi chú tại mục 2.2.10 (Số dư đầu kỳ) cho các item công nợ (2-3), tồn kho (4), TSCĐ/CCDC/CPTT (7-8-9) — chỉ rõ Phase 1 nhập opening balance, module quản lý đầy đủ ở Phase nào.

## Capabilities

### New Capabilities
- `account-entry-templates`: Bảng định khoản mẫu (Nợ/Có) cho mỗi phase, kèm yêu cầu phản hồi từ kế toán.
- `opening-balance-clarification`: Ghi chú rõ ràng tại mục số dư đầu kỳ về scope opening balance vs module đầy đủ ở phase sau.

### Modified Capabilities

## Impact

- File duy nhất: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- Không ảnh hưởng code, API hay dependency — chỉ sửa nội dung HTML/text trong tài liệu scope.
- Không cần thêm CSS mới (dùng lại class `.report-note` và cấu trúc `<table>` đã có).
