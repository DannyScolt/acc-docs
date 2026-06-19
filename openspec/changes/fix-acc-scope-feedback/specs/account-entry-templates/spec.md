## ADDED Requirements

### Requirement: Prominent feedback request for account entries
The Overview page SHALL display a prominent callout (using `.report-note` styling) replacing the current passive `.notice`, clearly stating that account entries (dinh khoan No/Co) are the core deliverable accountants MUST provide feedback on. The callout SHALL reference that sample entry tables exist at the end of each phase.

#### Scenario: Accountant opens Overview page
- **WHEN** an accountant reads the Overview page (section 1)
- **THEN** they see a visually prominent callout (orange background, bold text) that clearly communicates: (1) account entries are the core part needing their input, (2) sample tables are provided at each phase for them to review and modify

### Requirement: Sample account entry table per phase
Each phase (1-6) SHALL include a sample account entry table before the "Quy tac nghiep vu" section. The table SHALL have columns: STT, Nghiep vu (transaction), No (Debit TK), Co (Credit TK), Ghi chu (Notes). Each table SHALL contain 3-6 representative transactions for that phase with sample TK numbers per TT99.

#### Scenario: Phase 1 account entry table
- **WHEN** an accountant reads Phase 1
- **THEN** they see a table titled "Bang dinh khoan mau — Giai doan 1" with entries for: thu tien mat, chi tien mat, thu ngan hang, chi ngan hang — each with sample TK numbers (e.g., No 111 / Co 511 for thu tien mat ban hang)

#### Scenario: Phase 2 account entry table
- **WHEN** an accountant reads Phase 2
- **THEN** they see a table with entries for: mua hang nhap kho, thanh toan NCC, tra lai hang mua — with sample TK numbers

#### Scenario: Phase 3 account entry table
- **WHEN** an accountant reads Phase 3
- **THEN** they see a table with entries for: ban hang ghi nhan doanh thu, thu tien khach hang, xuat kho tinh gia von, tra lai hang ban

#### Scenario: Phase 4 account entry table
- **WHEN** an accountant reads Phase 4
- **THEN** they see a table with entries for: ket chuyen doanh thu, ket chuyen chi phi, xac dinh ket qua kinh doanh

#### Scenario: Phase 5 account entry table
- **WHEN** an accountant reads Phase 5
- **THEN** they see a table with entries for: thue GTGT dau vao, thue GTGT dau ra, khau tru thue GTGT

#### Scenario: Phase 6 account entry table
- **WHEN** an accountant reads Phase 6
- **THEN** they see a table with entries for: khau hao TSCD, phan bo CCDC, chi phi luong

### Requirement: Accountant guidance note below each table
Each account entry table SHALL be followed by an italicized guidance note stating: accountants should review, supplement, or adjust the TK numbers and transaction descriptions to match their company's actual accounting practice.

#### Scenario: Guidance note visibility
- **WHEN** an accountant views any phase's account entry table
- **THEN** they see an italicized note below the table guiding them to confirm or modify the entries
