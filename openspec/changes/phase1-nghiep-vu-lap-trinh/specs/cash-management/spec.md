## ADDED Requirements

### Requirement: Phiếu thu tiền mặt (CashReceipt)
Hệ thống SHALL cho phép lập, duyệt, hủy phiếu thu tiền mặt với state machine thống nhất và tự động sinh bút toán sổ cái.

**Entity: `cash_receipt`** (header)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| branch_id | UUID(FK) | | → branch |
| receipt_number | VARCHAR(30) | ✓ | Auto-gen theo numbering_rule |
| receipt_date | DATE | ✓ | ≥ fiscal_year.start_date, ≤ today, kỳ chưa khóa |
| receipt_type | ENUM | ✓ | customer_payment \| advance_return \| interest \| sale \| other |
| customer_id | UUID(FK) | | → customer (khi receipt_type = customer_payment) |
| employee_id | UUID(FK) | | → employee (khi receipt_type = advance_return) |
| total_amount | DECIMAL(18,2) | ✓ | = SUM(lines.amount), readonly |
| description | TEXT | | |
| status | ENUM | ✓ | draft \| pending_approval \| approved \| posted \| period_locked \| rejected \| cancelled |
| approved_by | UUID(FK) | | → user |
| approved_at | TIMESTAMP | | |
| posted_at | TIMESTAMP | | Thời điểm ghi sổ |
| cancelled_reason | TEXT | | Bắt buộc khi status = cancelled |
| rejected_reason | TEXT | | Bắt buộc khi status = rejected |
| created_by | UUID(FK) | ✓ | → user |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

**Entity: `cash_receipt_line`** (chi tiết)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| cash_receipt_id | UUID(FK) | ✓ | → cash_receipt |
| debit_account_id | UUID(FK) | ✓ | → account (111) |
| credit_account_id | UUID(FK) | ✓ | → account (131/141/511/515/711...) |
| amount | DECIMAL(18,2) | ✓ | > 0 |
| description | TEXT | | |
| ar_invoice_opening_id | UUID(FK) | | → ar_invoice_opening (khi thu công nợ) |
| expense_category_id | UUID(FK) | | → expense_category |

**State machine (5+2 trạng thái):**
```
Draft → submit() → Pending Approval → approve() → Approved → post() → Posted → lock_period() → Period Locked
                                     → reject() → Rejected → edit() → Draft
Draft → cancel() → Cancelled
Pending Approval → cancel() → Cancelled
```

#### Scenario: Lập phiếu thu từ công nợ khách hàng
- **WHEN** user tạo phiếu thu với receipt_type = customer_payment, chọn customer_id, thêm lines với ar_invoice_opening_id
- **THEN** mỗi line.amount MUST ≤ ar_invoice_opening.remaining_amount, tổng tiền thu > 0

#### Scenario: Submit phiếu thu
- **WHEN** user submit phiếu thu draft
- **THEN** hệ thống validate: ≥ 1 line, total_amount > 0, receipt_date hợp lệ (kỳ chưa khóa), chuyển status → pending_approval

#### Scenario: Duyệt phiếu thu — side effects
- **WHEN** người có quyền approve duyệt phiếu thu
- **THEN** hệ thống thực hiện tất cả side effects sau:
  1. status → approved, ghi approved_by, approved_at
  2. Sinh journal_entry + journal_entry_lines (Nợ 111 / Có theo credit_account_id mỗi line)
  3. Tăng tồn quỹ tiền mặt (cash_book)
  4. Nếu receipt_type = customer_payment → giảm ar_invoice_opening.remaining_amount cho mỗi line có ar_invoice_opening_id, tăng paid_amount
  5. Ghi audit_log

#### Scenario: Hủy phiếu thu đã duyệt
- **WHEN** user hủy phiếu thu đã approved (kỳ chưa khóa, nhập cancelled_reason)
- **THEN** hệ thống đảo ngược tất cả side effects:
  1. status → cancelled
  2. Sinh journal_entry đảo (Nợ credit_account / Có 111)
  3. Giảm tồn quỹ
  4. Hoàn lại ar_invoice_opening.remaining_amount nếu có
  5. Ghi audit_log

#### Scenario: Chặn khi kỳ đã khóa
- **WHEN** user cố tạo/sửa/duyệt/hủy phiếu thu có receipt_date thuộc kỳ đã khóa
- **THEN** hệ thống SHALL từ chối với lỗi "Kỳ kế toán đã khóa"

### Requirement: Phiếu chi tiền mặt (CashPayment)
Hệ thống SHALL cho phép lập, duyệt, hủy phiếu chi tiền mặt.

**Entity: `cash_payment`** (header)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| branch_id | UUID(FK) | | → branch |
| payment_number | VARCHAR(30) | ✓ | Auto-gen |
| payment_date | DATE | ✓ | Kỳ chưa khóa |
| payment_type | ENUM | ✓ | supplier_payment \| advance \| purchase \| expense \| refund_return \| other |
| supplier_id | UUID(FK) | | → supplier (khi payment_type = supplier_payment) |
| employee_id | UUID(FK) | | → employee (khi payment_type = advance) |
| customer_id | UUID(FK) | | → customer (khi payment_type = refund_return) |
| total_amount | DECIMAL(18,2) | ✓ | = SUM(lines.amount) |
| description | TEXT | | |
| status | ENUM | ✓ | draft \| pending_approval \| approved \| posted \| period_locked \| rejected \| cancelled |
| approved_by | UUID(FK) | | → user |
| approved_at | TIMESTAMP | | |
| posted_at | TIMESTAMP | | Thời điểm ghi sổ |
| cancelled_reason | TEXT | | |
| rejected_reason | TEXT | | Bắt buộc khi status = rejected |
| created_by | UUID(FK) | ✓ | → user |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

**Entity: `cash_payment_line`** (chi tiết)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| cash_payment_id | UUID(FK) | ✓ | → cash_payment |
| debit_account_id | UUID(FK) | ✓ | → account (331/141/156/641/642/627...) |
| credit_account_id | UUID(FK) | ✓ | → account (111) |
| amount | DECIMAL(18,2) | ✓ | > 0 |
| description | TEXT | | |
| ap_invoice_opening_id | UUID(FK) | | → ap_invoice_opening (khi thanh toán NCC) |
| expense_category_id | UUID(FK) | | → expense_category |

#### Scenario: Duyệt phiếu chi — side effects
- **WHEN** người có quyền duyệt phiếu chi
- **THEN** side effects:
  1. status → approved
  2. Sinh journal_entry (Nợ debit_account / Có 111 theo mỗi line)
  3. Giảm tồn quỹ tiền mặt
  4. Nếu payment_type = supplier_payment → giảm ap_invoice_opening.remaining_amount
  5. Ghi audit_log

#### Scenario: Chi tạm ứng nhân viên
- **WHEN** user lập phiếu chi với payment_type = advance, chọn employee_id
- **THEN** line.debit_account_id MUST = 141 (tạm ứng), hệ thống ghi nhận khoản tạm ứng cho employee

#### Scenario: Chi hoàn tiền khách hàng
- **WHEN** user lập phiếu chi với payment_type = refund_return, chọn customer_id
- **THEN** bắt buộc chọn customer_id, hệ thống gợi ý TK đối ứng `[CẦN KẾ TOÁN XÁC NHẬN: 131 hay 521 hay TK khác?]`, sinh journal_entry Nợ TK xác nhận / Có 111

### Requirement: Kiểm kê quỹ (CashInventory)
Hệ thống SHALL cho phép lập biên bản kiểm kê quỹ, so sánh tồn thực tế với tồn sổ, xử lý chênh lệch.

**Entity: `cash_inventory`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| inventory_date | DATE | ✓ | |
| book_balance | DECIMAL(18,2) | ✓ | Tồn sổ (auto-calc từ cash_book) |
| actual_balance | DECIMAL(18,2) | ✓ | Tồn thực tế kiểm kê |
| difference | DECIMAL(18,2) | ✓ | = actual - book |
| status | ENUM | ✓ | draft \| pending_approval \| approved \| adjusted \| cancelled |
| adjustment_receipt_id | UUID(FK) | | → cash_receipt (khi thừa) |
| adjustment_payment_id | UUID(FK) | | → cash_payment (khi thiếu) |
| confirmed_by | UUID(FK) | | → user |
| notes | TEXT | | |

#### Scenario: Kiểm kê phát hiện thừa
- **WHEN** actual_balance > book_balance
- **THEN** difference > 0, hệ thống gợi ý tạo phiếu thu điều chỉnh với định khoản Nợ 111 / Có 3381 `[CẦN KẾ TOÁN XÁC NHẬN: 3381 hay 711?]`

#### Scenario: Kiểm kê phát hiện thiếu
- **WHEN** actual_balance < book_balance
- **THEN** difference < 0, hệ thống gợi ý tạo phiếu chi điều chỉnh với định khoản Nợ 1381 / Có 111 `[CẦN KẾ TOÁN XÁC NHẬN: 1381 hay 1388?]`

**Entity: `cash_inventory_denomination`** (kiểm kê chi tiết theo mệnh giá)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| cash_inventory_id | UUID(FK) | ✓ | → cash_inventory |
| denomination | DECIMAL(18,2) | ✓ | Mệnh giá (500000, 200000, 100000...) |
| quantity | INTEGER | ✓ | Số lượng tờ/đồng |
| amount | DECIMAL(18,2) | ✓ | = denomination × quantity |

#### Scenario: Nhập kiểm kê theo mệnh giá
- **WHEN** thủ quỹ kiểm kê quỹ
- **THEN** nhập số lượng cho từng mệnh giá, hệ thống tính amount = denomination × quantity, actual_balance = SUM(denomination lines.amount)

### Requirement: Sổ quỹ tiền mặt (CashBook)
Hệ thống SHALL duy trì sổ quỹ ghi nhận tồn đầu kỳ, phát sinh thu, phát sinh chi, tồn cuối kỳ.

#### Scenario: Xem sổ quỹ theo kỳ
- **WHEN** user chọn khoảng thời gian
- **THEN** hệ thống hiển thị: tồn đầu kỳ (opening_balance TK 111 + phát sinh trước kỳ), thu trong kỳ (SUM cash_receipt approved), chi trong kỳ (SUM cash_payment approved), tồn cuối kỳ

#### Scenario: Xem tồn quỹ tức thời
- **WHEN** user xem tồn quỹ hiện tại
- **THEN** hệ thống tính: opening_balance TK 111 + SUM(approved receipts) - SUM(approved payments) đến thời điểm hiện tại

#### Scenario: Đối chiếu sổ quỹ với sổ cái
- **WHEN** user yêu cầu đối chiếu
- **THEN** hệ thống so sánh tồn quỹ với số dư TK 111 trên sổ cái, hiển thị chênh lệch nếu có
