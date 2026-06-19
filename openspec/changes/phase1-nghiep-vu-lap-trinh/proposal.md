## Why

Tài liệu Phase 1 hiện tại ([ACC-noi-dung-nghiep-vu-theo-phase.html](../../ACC-noi-dung-nghiep-vu-theo-phase.html)) liệt kê ~180 chức năng ở mức mô tả nghiệp vụ cho kế toán review, nhưng **thiếu hoàn toàn thông tin cần thiết để lập trình viên triển khai**: data model, validation rules, state machine, side effects, định khoản chi tiết, và entity skeleton cho số dư đầu kỳ.

Cần tạo tài liệu "Nghiệp vụ lập trình Phase 1" — chuyển đổi từ ngôn ngữ kế toán sang đặc tả kỹ thuật mà dev có thể viết code trực tiếp, đồng thời giải quyết vấn đề "forward reference" (Phase 1 yêu cầu nhập dữ liệu của entity thuộc Phase 2/3/6 nhưng chưa định nghĩa schema).

## What Changes

- **Tạo mới file HTML** `Phase1-nghiep-vu-lap-trinh.html` — tài liệu đặc tả kỹ thuật Phase 1 hoàn chỉnh, bao gồm:
  - Data model (~35 entity với bảng field chi tiết, kiểu dữ liệu, ràng buộc, khóa ngoại)
  - State machine cho chứng từ (Draft → Pending → Approved → Cancelled)
  - Functional spec chi tiết cho ~40-50 nghiệp vụ có side effect (phiếu thu/chi, thu/chi NH, chuyển nội bộ, kiểm kê quỹ, ghi sổ, nhập số dư đầu kỳ)
  - Compact spec cho ~50-60 CRUD danh mục có validation đặc biệt
  - Bảng định khoản đầy đủ (~25 nghiệp vụ thay vì 6 dòng hiện tại), đánh dấu chỗ cần kế toán xác nhận
  - Opening balance skeleton entity (AR/AP Invoice, Inventory, Fixed Asset, Tool, Prepaid) — schema tối thiểu Phase 1, ghi rõ sẽ mở rộng ở Phase nào
  - Báo cáo & truy vấn (~8-10 báo cáo với nguồn dữ liệu, bộ lọc, drill-down)
  - Quy tắc hệ thống xuyên suốt (audit log, phân quyền, đánh số chứng từ, khóa kỳ, multi-tenant)

## Capabilities

### New Capabilities

- `system-admin`: Quản trị hệ thống — entity Company, Branch, Department, FiscalYear, User, Role, Permission, AuditLog, DocumentType, NumberingRule. Bao gồm multi-tenant isolation, RBAC, audit logging.
- `master-data`: Danh mục dùng chung — entity Account (cây cha-con), Customer, Supplier, Employee, Product, ProductUnit, Warehouse, BankAccount, ExpenseCategory và các nhóm phân loại. Bao gồm CRUD + import/export Excel.
- `opening-balance`: Số dư đầu kỳ — entity OpeningBalance (tổng hợp) + skeleton entity cho công nợ phải thu/trả chi tiết theo hóa đơn, tồn kho theo kho×mặt hàng, TSCĐ, CCDC, chi phí trả trước. Bao gồm kiểm tra cân đối và khóa số dư.
- `cash-management`: Nghiệp vụ quỹ tiền mặt — entity CashReceipt, CashPayment (header + lines), CashBook, CashInventory. State machine chứng từ, sinh bút toán sổ cái, cập nhật công nợ, kiểm kê quỹ.
- `bank-management`: Nghiệp vụ tiền gửi ngân hàng — entity BankReceipt, BankPayment, BankTransfer, BankStatement, BankReconciliation. Thu/chi qua NH, chuyển nội bộ, nhập sao kê, đối chiếu ngân hàng.
- `general-ledger`: Sổ cái & hệ thống kế toán — entity JournalEntry (header + lines). Ghi sổ từ chứng từ, sổ cái, nhật ký chung, bảng cân đối phát sinh. Định khoản đầy đủ Phase 1.
- `reports-phase1`: Báo cáo Phase 1 — sổ quỹ, sổ tiền gửi NH, bảng kê phiếu thu/chi, sổ cái, nhật ký chung, cân đối phát sinh. Nguồn dữ liệu, bộ lọc, drill-down.

### Modified Capabilities

(Không có — đây là lần đầu tạo spec)

## Impact

- **Output**: Tạo mới 1 file HTML `Phase1-nghiep-vu-lap-trinh.html` trong thư mục gốc, cùng cấp với `ACC-noi-dung-nghiep-vu-theo-phase.html`
- **Tham chiếu**: Dựa trên nội dung Phase 1 trong file HTML hiện tại (section 2.1 → 2.5) làm input
- **Đối tượng sử dụng**: Lập trình viên backend/frontend, DBA, QA
- **Phụ thuộc**: Một số trường trong bảng định khoản đánh dấu `[CẦN KẾ TOÁN XÁC NHẬN]` — cần kế toán chốt trước khi dev triển khai
