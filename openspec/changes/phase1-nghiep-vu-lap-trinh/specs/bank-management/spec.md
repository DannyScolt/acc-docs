## ADDED Requirements

### Requirement: Chứng từ thu ngân hàng (BankReceipt)
Hệ thống SHALL cho phép lập, duyệt, hủy chứng từ thu tiền qua ngân hàng.

**Entity: `bank_receipt`** (header)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| branch_id | UUID(FK) | | → branch |
| receipt_number | VARCHAR(30) | ✓ | Auto-gen |
| receipt_date | DATE | ✓ | Kỳ chưa khóa |
| receipt_type | ENUM | ✓ | customer_payment \| interest \| other |
| bank_account_id | UUID(FK) | ✓ | → bank_account |
| customer_id | UUID(FK) | | → customer |
| total_amount | DECIMAL(18,2) | ✓ | = SUM(lines.amount) |
| description | TEXT | | |
| status | ENUM | ✓ | draft \| pending_approval \| approved \| cancelled |
| approved_by | UUID(FK) | | |
| approved_at | TIMESTAMP | | |
| cancelled_reason | TEXT | | |
| created_by | UUID(FK) | ✓ | |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

**Entity: `bank_receipt_line`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| bank_receipt_id | UUID(FK) | ✓ | |
| debit_account_id | UUID(FK) | ✓ | → account (112x từ bank_account.accounting_account_id) |
| credit_account_id | UUID(FK) | ✓ | → account (131/515/711...) |
| amount | DECIMAL(18,2) | ✓ | > 0 |
| description | TEXT | | |
| ar_invoice_opening_id | UUID(FK) | | → ar_invoice_opening |

#### Scenario: Duyệt thu ngân hàng — side effects
- **WHEN** người có quyền duyệt chứng từ thu NH
- **THEN** side effects:
  1. status → approved
  2. Sinh journal_entry (Nợ 112x / Có credit_account theo mỗi line)
  3. Tăng số dư tài khoản NH (bank_book)
  4. Nếu customer_payment → giảm ar_invoice_opening.remaining_amount
  5. Ghi audit_log

#### Scenario: Thu tiền lãi ngân hàng
- **WHEN** user lập chứng từ thu NH với receipt_type = interest
- **THEN** line.credit_account_id = 515 (doanh thu tài chính)

### Requirement: Chứng từ chi ngân hàng (BankPayment)
Hệ thống SHALL cho phép lập, duyệt, hủy chứng từ chi tiền qua ngân hàng.

**Entity: `bank_payment`** (header)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| branch_id | UUID(FK) | | → branch |
| payment_number | VARCHAR(30) | ✓ | Auto-gen |
| payment_date | DATE | ✓ | Kỳ chưa khóa |
| payment_type | ENUM | ✓ | supplier_payment \| bank_fee \| expense \| other |
| bank_account_id | UUID(FK) | ✓ | → bank_account |
| supplier_id | UUID(FK) | | → supplier |
| total_amount | DECIMAL(18,2) | ✓ | = SUM(lines.amount) |
| description | TEXT | | |
| status | ENUM | ✓ | draft \| pending_approval \| approved \| cancelled |
| approved_by | UUID(FK) | | |
| approved_at | TIMESTAMP | | |
| cancelled_reason | TEXT | | |
| created_by | UUID(FK) | ✓ | |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

**Entity: `bank_payment_line`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| bank_payment_id | UUID(FK) | ✓ | |
| debit_account_id | UUID(FK) | ✓ | → account (331/641/642/6427...) |
| credit_account_id | UUID(FK) | ✓ | → account (112x) |
| amount | DECIMAL(18,2) | ✓ | > 0 |
| description | TEXT | | |
| ap_invoice_opening_id | UUID(FK) | | → ap_invoice_opening |
| expense_category_id | UUID(FK) | | → expense_category |

#### Scenario: Duyệt chi ngân hàng — side effects
- **WHEN** người có quyền duyệt chứng từ chi NH
- **THEN** side effects:
  1. status → approved
  2. Sinh journal_entry (Nợ debit_account / Có 112x)
  3. Giảm số dư tài khoản NH
  4. Nếu supplier_payment → giảm ap_invoice_opening.remaining_amount
  5. Ghi audit_log

#### Scenario: Phí ngân hàng
- **WHEN** user lập chi NH với payment_type = bank_fee
- **THEN** line.debit_account_id = `[CẦN KẾ TOÁN XÁC NHẬN: 6427 (chi phí quản lý - phí ngân hàng) hay 635 (chi phí tài chính)?]`

### Requirement: Chuyển tiền nội bộ (BankTransfer)
Hệ thống SHALL cho phép chuyển tiền giữa các tài khoản NH, nộp tiền mặt vào NH, rút tiền NH về quỹ.

**Entity: `bank_transfer`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| transfer_number | VARCHAR(30) | ✓ | Auto-gen |
| transfer_date | DATE | ✓ | Kỳ chưa khóa |
| transfer_type | ENUM | ✓ | bank_to_bank \| cash_to_bank \| bank_to_cash |
| from_bank_account_id | UUID(FK) | | → bank_account (khi from = bank) |
| to_bank_account_id | UUID(FK) | | → bank_account (khi to = bank) |
| amount | DECIMAL(18,2) | ✓ | > 0 |
| fee_amount | DECIMAL(18,2) | | Phí chuyển tiền (default: 0) |
| description | TEXT | | |
| status | ENUM | ✓ | draft \| pending_approval \| approved \| cancelled |
| approved_by | UUID(FK) | | |
| approved_at | TIMESTAMP | | |
| cancelled_reason | TEXT | | |
| created_by | UUID(FK) | ✓ | |

#### Scenario: Chuyển giữa 2 tài khoản ngân hàng
- **WHEN** transfer_type = bank_to_bank, chọn from_bank_account và to_bank_account (khác nhau)
- **THEN** khi duyệt → sinh journal_entry Nợ 112b / Có 112a, giảm sổ bank A, tăng sổ bank B. Nếu fee_amount > 0 → sinh thêm bút toán Nợ `[CẦN XÁC NHẬN: 6427/635]` / Có 112a

#### Scenario: Nộp tiền mặt vào ngân hàng
- **WHEN** transfer_type = cash_to_bank, chọn to_bank_account
- **THEN** khi duyệt → sinh journal_entry Nợ 112 / Có 111, giảm tồn quỹ, tăng sổ bank

#### Scenario: Rút tiền ngân hàng về quỹ
- **WHEN** transfer_type = bank_to_cash, chọn from_bank_account
- **THEN** khi duyệt → sinh journal_entry Nợ 111 / Có 112, tăng tồn quỹ, giảm sổ bank

### Requirement: Sao kê ngân hàng (BankStatement)
Hệ thống SHALL cho phép nhập sao kê ngân hàng và gợi ý đối chiếu tự động.

**Entity: `bank_statement`** (header)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| bank_account_id | UUID(FK) | ✓ | → bank_account |
| statement_date | DATE | ✓ | |
| opening_balance | DECIMAL(18,2) | ✓ | |
| closing_balance | DECIMAL(18,2) | ✓ | |
| imported_at | TIMESTAMP | ✓ | |
| imported_by | UUID(FK) | ✓ | → user |

**Entity: `bank_statement_line`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| bank_statement_id | UUID(FK) | ✓ | |
| transaction_date | DATE | ✓ | |
| description | TEXT | | Nội dung giao dịch |
| debit_amount | DECIMAL(18,2) | | Tiền ra |
| credit_amount | DECIMAL(18,2) | | Tiền vào |
| running_balance | DECIMAL(18,2) | | Số dư |
| reference_number | VARCHAR(50) | | Số tham chiếu |
| is_matched | BOOLEAN | ✓ | Default: false |
| matched_entity_type | VARCHAR(50) | | bank_receipt \| bank_payment \| bank_transfer |
| matched_entity_id | UUID | | ID chứng từ đã khớp |

#### Scenario: Nhập sao kê từ Excel/CSV
- **WHEN** kế toán upload file sao kê ngân hàng
- **THEN** hệ thống parse file, tạo bank_statement + bank_statement_lines, tự động gợi ý match theo số tiền + ngày + nội dung

#### Scenario: Gợi ý đối chiếu tự động
- **WHEN** hệ thống xử lý statement_line mới
- **THEN** tìm chứng từ (bank_receipt/bank_payment/bank_transfer) khớp theo: amount ± tolerance, date ± 3 ngày, description contains reference. Hiển thị kết quả gợi ý cho user xác nhận

#### Scenario: Đánh dấu đã khớp
- **WHEN** user xác nhận match giữa statement_line và chứng từ
- **THEN** set is_matched = true, matched_entity_type + matched_entity_id

### Requirement: Đối chiếu ngân hàng (BankReconciliation)
Hệ thống SHALL cho phép đối chiếu sổ tiền gửi với sao kê ngân hàng.

**Entity: `bank_reconciliation`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| bank_account_id | UUID(FK) | ✓ | → bank_account |
| reconciliation_date | DATE | ✓ | |
| book_balance | DECIMAL(18,2) | ✓ | Số dư sổ kế toán |
| statement_balance | DECIMAL(18,2) | ✓ | Số dư sao kê |
| difference | DECIMAL(18,2) | ✓ | = statement - book |
| unmatched_book_count | INTEGER | ✓ | Số chứng từ chưa khớp trên sổ |
| unmatched_statement_count | INTEGER | ✓ | Số GD sao kê chưa khớp |
| status | ENUM | ✓ | draft \| confirmed \| locked |
| confirmed_by | UUID(FK) | | → user |
| confirmed_at | TIMESTAMP | | |

#### Scenario: Đối chiếu sổ với sao kê
- **WHEN** kế toán chọn bank_account và kỳ đối chiếu
- **THEN** hệ thống tính book_balance (từ journal_entry TK 112x), statement_balance (từ bank_statement.closing_balance), liệt kê giao dịch chưa khớp cả 2 phía

#### Scenario: Xử lý chênh lệch
- **WHEN** difference ≠ 0 sau khi match hết có thể
- **THEN** hệ thống hiển thị danh sách giao dịch gây chênh lệch, kế toán quyết định tạo chứng từ bổ sung hoặc ghi nhận chờ kỳ sau

#### Scenario: Khóa kỳ đối chiếu
- **WHEN** kế toán xác nhận đối chiếu hoàn tất
- **THEN** status → locked, không cho thay đổi match/unmatch trong kỳ đã khóa
