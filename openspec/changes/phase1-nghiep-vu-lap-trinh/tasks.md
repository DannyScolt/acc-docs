## 1. Chuẩn bị & cấu trúc file

- [x] 1.1 Tạo file `Phase1-nghiep-vu-lap-trinh.html` với CSS framework copy từ `ACC-noi-dung-nghiep-vu-theo-phase.html` (giữ đồng bộ style)
- [x] 1.2 Tạo cấu trúc HTML: cover page, mục lục, 7 chương chính (system-admin, master-data, opening-balance, cash, bank, general-ledger, reports)

## 2. Chương 1 — Quản trị hệ thống (system-admin)

- [x] 2.1 Viết data model cho entity: company, fiscal_year, branch, department (bảng field chi tiết, type, required, FK, ghi chú)
- [x] 2.2 Viết data model cho entity: user, role, permission, user_role, data_permission (RBAC)
- [x] 2.3 Viết data model cho entity: document_type, numbering_rule
- [x] 2.4 Viết data model cho entity: audit_log
- [x] 2.5 Viết functional spec chi tiết: khởi tạo doanh nghiệp, cấu hình năm tài chính, cấu hình chế độ kế toán
- [x] 2.6 Viết functional spec chi tiết: tạo/cập nhật/khóa/mở khóa user, đăng nhập/đăng xuất, quản lý phiên
- [x] 2.7 Viết functional spec chi tiết: khai báo vai trò, phân quyền theo chức năng/phân hệ/dữ liệu/duyệt, ma trận phân quyền
- [x] 2.8 Viết quy tắc hệ thống: audit log (ghi gì, cấu trúc, bảo vệ), cách ly multi-tenant, khóa kỳ

## 3. Chương 2 — Danh mục dùng chung (master-data)

- [x] 3.1 Viết data model cho entity: account (cây cha-con), customer, customer_group, supplier, supplier_group
- [x] 3.2 Viết data model cho entity: employee, product, product_group, product_unit, warehouse
- [x] 3.3 Viết data model cho entity: bank_account, expense_category
- [x] 3.4 Viết functional spec COMPACT: CRUD tài khoản kế toán (thêm/sửa/ngừng/import/export, validation code cha-con)
- [x] 3.5 Viết functional spec COMPACT: CRUD khách hàng (trùng MST, hạn mức công nợ, điều khoản thanh toán, import/export)
- [x] 3.6 Viết functional spec COMPACT: CRUD nhà cung cấp, nhân viên (liên kết user)
- [x] 3.7 Viết functional spec COMPACT: CRUD hàng hóa/vật tư/dịch vụ (đơn vị tính quy đổi, giá bán, định mức tồn, TK mặc định)
- [x] 3.8 Viết functional spec COMPACT: CRUD kho, TK ngân hàng, khoản mục chi phí

## 4. Chương 3 — Số dư đầu kỳ (opening-balance)

- [x] 4.1 Viết data model cho entity: opening_balance (TK tổng hợp)
- [x] 4.2 Viết data model skeleton entity: ar_invoice_opening, ap_invoice_opening (công nợ chi tiết theo HĐ) — ghi rõ field Phase 1 vs mở rộng Phase 2/3
- [x] 4.3 Viết data model skeleton entity: inventory_opening (tồn kho theo kho × mặt hàng) — ghi rõ mở rộng Phase 2
- [x] 4.4 Viết data model skeleton entity: fixed_asset_opening, tool_opening, prepaid_opening — ghi rõ mở rộng Phase 6
- [x] 4.5 Viết functional spec FULL: nhập số dư TK đầu kỳ, nhập công nợ KH/NCC chi tiết, nhập tồn kho, nhập TSCĐ/CCDC/CPTT
- [x] 4.6 Viết functional spec: import số dư từ Excel, kiểm tra cân đối (chi tiết khớp tổng hợp), khóa số dư đầu kỳ

## 5. Chương 4 — Quỹ tiền mặt (cash-management)

- [x] 5.1 Viết data model cho entity: cash_receipt + cash_receipt_line
- [x] 5.2 Viết data model cho entity: cash_payment + cash_payment_line
- [x] 5.3 Viết data model cho entity: cash_inventory
- [x] 5.4 Viết state machine diagram cho chứng từ quỹ (Draft → Pending → Approved → Cancelled) với điều kiện chuyển
- [x] 5.5 Viết functional spec FULL: lập phiếu thu (5 loại receipt_type), validation, side effects khi duyệt, hủy
- [x] 5.6 Viết functional spec FULL: lập phiếu chi (5 loại payment_type), validation, side effects khi duyệt, hủy
- [x] 5.7 Viết functional spec FULL: kiểm kê quỹ (so sánh, xử lý chênh lệch, đánh dấu [CẦN KẾ TOÁN XÁC NHẬN])
- [x] 5.8 Viết functional spec: sổ quỹ (công thức tồn, đối chiếu sổ cái), in phiếu thu/chi

## 6. Chương 5 — Tiền gửi ngân hàng (bank-management)

- [x] 6.1 Viết data model cho entity: bank_receipt + bank_receipt_line, bank_payment + bank_payment_line
- [x] 6.2 Viết data model cho entity: bank_transfer, bank_statement + bank_statement_line, bank_reconciliation
- [x] 6.3 Viết functional spec FULL: thu/chi ngân hàng (duyệt, side effects, định khoản)
- [x] 6.4 Viết functional spec FULL: chuyển tiền nội bộ (3 loại: bank↔bank, cash→bank, bank→cash, phí CK)
- [x] 6.5 Viết functional spec FULL: nhập sao kê, gợi ý đối chiếu tự động, đánh dấu khớp
- [x] 6.6 Viết functional spec FULL: đối chiếu ngân hàng (so sánh sổ vs sao kê, xử lý lệch, khóa kỳ đối chiếu)

## 7. Chương 6 — Sổ cái & định khoản (general-ledger)

- [x] 7.1 Viết data model cho entity: journal_entry + journal_entry_line
- [x] 7.2 Viết functional spec FULL: ghi sổ tự động từ phiếu thu/chi, từ chứng từ NH, từ chuyển nội bộ
- [x] 7.3 Viết functional spec: đảo bút toán khi hủy chứng từ, kiểm tra cân đối Nợ/Có, truy vết chứng từ gốc
- [x] 7.4 Viết bảng định khoản đầy đủ Phase 1 (~26 nghiệp vụ), đánh dấu [CẦN KẾ TOÁN XÁC NHẬN] cho các TK chưa chốt
- [x] 7.5 Viết functional spec: sổ cái (view theo TK, lọc đối tượng, drill-down), nhật ký chung, bảng cân đối phát sinh

## 8. Chương 7 — Báo cáo Phase 1 (reports)

- [x] 8.1 Viết spec báo cáo quỹ: sổ quỹ tiền mặt, bảng kê phiếu thu/chi, tồn quỹ, dòng tiền (nguồn dữ liệu, bộ lọc, công thức, drill-down)
- [x] 8.2 Viết spec báo cáo ngân hàng: sổ tiền gửi, bảng kê thu/chi NH, số dư NH, GD chưa đối chiếu
- [x] 8.3 Viết spec báo cáo kế toán: sổ cái, nhật ký chung, cân đối phát sinh (format xuất Excel/PDF)
- [x] 8.4 Viết spec in phiếu: mẫu phiếu thu, phiếu chi, chứng từ NH theo chuẩn kế toán

## 9. Review & hoàn thiện

- [x] 9.1 Review toàn bộ file HTML: kiểm tra tính đồng bộ giữa data model, functional spec, định khoản, và báo cáo
- [x] 9.2 Kiểm tra tất cả cross-reference: FK trỏ đúng entity, TK trong định khoản khớp account schema
- [x] 9.3 Đánh dấu tổng hợp danh sách [CẦN KẾ TOÁN XÁC NHẬN] vào 1 bảng tóm tắt ở cuối file
- [x] 9.4 Tạo Entity Relationship Diagram (ERD) tổng hợp Phase 1 (~35 entity) dạng ASCII/text trong file
