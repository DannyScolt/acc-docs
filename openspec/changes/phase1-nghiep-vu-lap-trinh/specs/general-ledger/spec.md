## ADDED Requirements

### Requirement: Bút toán sổ cái (JournalEntry)
Hệ thống SHALL tự động sinh bút toán sổ cái khi chứng từ được duyệt, đảm bảo mỗi bút toán cân đối Nợ = Có.

**Entity: `journal_entry`** (header)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| entry_number | VARCHAR(30) | ✓ | Auto-gen |
| entry_date | DATE | ✓ | = ngày chứng từ gốc |
| source_type | ENUM | ✓ | cash_receipt \| cash_payment \| bank_receipt \| bank_payment \| bank_transfer \| adjustment |
| source_id | UUID | ✓ | ID chứng từ gốc |
| description | TEXT | | |
| total_debit | DECIMAL(18,2) | ✓ | = SUM(lines WHERE side=debit) |
| total_credit | DECIMAL(18,2) | ✓ | = SUM(lines WHERE side=credit) |
| is_reversal | BOOLEAN | ✓ | Default: false (true khi đảo chứng từ hủy) |
| reversed_entry_id | UUID(FK) | | → journal_entry (entry gốc bị đảo) |
| created_at | TIMESTAMP | ✓ | |

**Entity: `journal_entry_line`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| journal_entry_id | UUID(FK) | ✓ | → journal_entry |
| account_id | UUID(FK) | ✓ | → account |
| side | ENUM | ✓ | debit \| credit |
| amount | DECIMAL(18,2) | ✓ | > 0 |
| counterpart_account_id | UUID(FK) | | → account (TK đối ứng, cho tra cứu) |
| customer_id | UUID(FK) | | → customer (khi liên quan công nợ KH) |
| supplier_id | UUID(FK) | | → supplier (khi liên quan công nợ NCC) |
| employee_id | UUID(FK) | | → employee |
| bank_account_id | UUID(FK) | | → bank_account |
| expense_category_id | UUID(FK) | | → expense_category |
| description | TEXT | | |

**Ràng buộc:**
- total_debit MUST = total_credit cho mỗi journal_entry
- journal_entry không cho sửa/xóa trực tiếp — muốn sửa phải hủy chứng từ gốc → sinh entry đảo

#### Scenario: Ghi sổ từ phiếu thu
- **WHEN** phiếu thu được duyệt
- **THEN** hệ thống sinh journal_entry với source_type = cash_receipt, source_id = cash_receipt.id, tạo journal_entry_lines theo các line của phiếu thu (Nợ 111 / Có TK đối ứng)

#### Scenario: Ghi sổ từ phiếu chi
- **WHEN** phiếu chi được duyệt
- **THEN** sinh journal_entry source_type = cash_payment, lines (Nợ TK đối ứng / Có 111)

#### Scenario: Ghi sổ từ chứng từ ngân hàng
- **WHEN** chứng từ thu/chi NH được duyệt
- **THEN** sinh journal_entry source_type = bank_receipt/bank_payment, lines (Nợ/Có 112x)

#### Scenario: Ghi sổ từ chuyển nội bộ
- **WHEN** bank_transfer được duyệt
- **THEN** sinh journal_entry source_type = bank_transfer. Nếu cash_to_bank → Nợ 112 Có 111. Nếu bank_to_cash → Nợ 111 Có 112. Nếu bank_to_bank → Nợ 112b Có 112a. Nếu fee > 0 → dòng bổ sung Nợ 6427/635 Có 112

#### Scenario: Đảo bút toán khi hủy chứng từ
- **WHEN** chứng từ đã duyệt bị hủy
- **THEN** sinh journal_entry mới với is_reversal = true, reversed_entry_id = entry gốc, các line đảo ngược (Nợ ↔ Có)

#### Scenario: Kiểm tra cân đối Nợ/Có
- **WHEN** hệ thống tạo journal_entry
- **THEN** MUST verify total_debit = total_credit, nếu lệch → rollback và báo lỗi

#### Scenario: Truy vết về chứng từ gốc
- **WHEN** user bấm vào 1 dòng trên sổ cái
- **THEN** hệ thống mở chứng từ gốc tương ứng (source_type + source_id)

### Requirement: Bảng định khoản đầy đủ Phase 1
Hệ thống SHALL hỗ trợ tất cả các nghiệp vụ định khoản sau trong Phase 1:

| STT | Nghiệp vụ | Nợ (TK) | Có (TK) | Điều kiện | Ghi chú |
|-----|-----------|---------|---------|-----------|---------|
| 1 | Thu tiền mặt bán hàng thu ngay | 111 | 511 | receipt_type = sale | |
| 2 | Thu tiền mặt từ công nợ KH | 111 | 131 | receipt_type = customer_payment | Giảm AR |
| 3 | Thu hoàn ứng nhân viên | 111 | 141 | receipt_type = advance_return | |
| 4 | Thu tiền lãi tiền gửi (tiền mặt) | 111 | 515 | receipt_type = interest | |
| 5 | Thu khác bằng tiền mặt | 111 | 711 | receipt_type = other | |
| 6 | Chi mua hàng trả ngay (tiền mặt) | 156 | 111 | payment_type = purchase | |
| 7 | Chi thanh toán NCC (tiền mặt) | 331 | 111 | payment_type = supplier_payment | Giảm AP |
| 8 | Chi tạm ứng nhân viên | 141 | 111 | payment_type = advance | |
| 9 | Chi phí bán hàng (tiền mặt) | 641 | 111 | payment_type = expense, dept = sales | `[CẦN KẾ TOÁN XÁC NHẬN: phân biệt 641/642/627 theo dept hay theo expense_category?]` |
| 10 | Chi phí quản lý (tiền mặt) | 642 | 111 | payment_type = expense, dept = admin | |
| 11 | Chi phí sản xuất (tiền mặt) | 627 | 111 | payment_type = expense, dept = mfg | |
| 12 | Chi khác bằng tiền mặt | 811 | 111 | payment_type = other | `[CẦN XÁC NHẬN: 811 hay TK khác?]` |
| 13 | Thu tiền KH qua ngân hàng | 112 | 131 | bank receipt, customer_payment | Giảm AR |
| 14 | Thu lãi ngân hàng | 112 | 515 | bank receipt, interest | |
| 15 | Thu khác qua ngân hàng | 112 | 711 | bank receipt, other | |
| 16 | Chi thanh toán NCC qua NH | 331 | 112 | bank payment, supplier_payment | Giảm AP |
| 17 | Phí ngân hàng | ? | 112 | bank payment, bank_fee | `[CẦN KẾ TOÁN XÁC NHẬN: Nợ 6427 hay 635?]` |
| 18 | Chi phí qua ngân hàng | 641/642 | 112 | bank payment, expense | |
| 19 | Nộp tiền mặt vào NH | 112 | 111 | bank_transfer, cash_to_bank | |
| 20 | Rút tiền NH về quỹ | 111 | 112 | bank_transfer, bank_to_cash | |
| 21 | Chuyển giữa 2 TK NH | 112b | 112a | bank_transfer, bank_to_bank | a ≠ b |
| 22 | Phí chuyển khoản NH | ? | 112 | bank_transfer, fee_amount > 0 | `[CẦN XÁC NHẬN: 6427 hay 635?]` |
| 23 | Kiểm kê quỹ thừa | 111 | ? | cash_inventory, difference > 0 | `[CẦN XÁC NHẬN: Có 3381 hay 711?]` |
| 24 | Kiểm kê quỹ thiếu | ? | 111 | cash_inventory, difference < 0 | `[CẦN XÁC NHẬN: Nợ 1381 hay 1388?]` |
| 25 | Chênh lệch tỷ giá (lãi) | 112 | 515 | Ngoại tệ, lãi | `[CẦN XÁC NHẬN: Phase 1 có phát sinh ngoại tệ không?]` |
| 26 | Chênh lệch tỷ giá (lỗ) | 635 | 112 | Ngoại tệ, lỗ | `[CẦN XÁC NHẬN: như trên]` |
| 27 | Chi hoàn tiền khách hàng | `[CẦN KẾ TOÁN XÁC NHẬN: 131 hay 521 hay TK khác?]` | 111 | payment_type = refund_return | Nghiệp vụ mới từ docx kế toán |

#### Scenario: Ghi sổ khi duyệt phiếu chi hoàn tiền
- **WHEN** phiếu chi refund_return được duyệt
- **THEN** sinh journal_entry với debit_account = TK được kế toán xác nhận, credit = 111

#### Scenario: Kế toán xác nhận định khoản
- **WHEN** kế toán review bảng định khoản và chốt tài khoản cho các mục `[CẦN XÁC NHẬN]`
- **THEN** dev cập nhật logic sinh journal_entry_line theo TK đã chốt

### Requirement: Sổ cái (GeneralLedger view)
Hệ thống SHALL hiển thị sổ cái theo tài khoản với phát sinh Nợ/Có, số dư, và drill-down về chứng từ gốc.

#### Scenario: Xem sổ cái theo tài khoản
- **WHEN** user chọn tài khoản và kỳ
- **THEN** hiển thị: số dư đầu kỳ, danh sách bút toán (ngày, số CT, diễn giải, TK đối ứng, Nợ, Có), số dư cuối kỳ. Nguồn: journal_entry_line WHERE account_id = selected

#### Scenario: Lọc sổ cái theo đối tượng
- **WHEN** user lọc theo customer_id / supplier_id / employee_id / bank_account_id / expense_category_id
- **THEN** chỉ hiển thị journal_entry_line có đối tượng tương ứng

#### Scenario: Drill-down về chứng từ gốc
- **WHEN** user bấm vào 1 dòng sổ cái
- **THEN** mở chứng từ gốc thông qua journal_entry.source_type + source_id

### Requirement: Nhật ký chung
Hệ thống SHALL hiển thị toàn bộ bút toán theo trình tự thời gian.

#### Scenario: Xem nhật ký chung
- **WHEN** user chọn khoảng thời gian
- **THEN** hiển thị tất cả journal_entry + lines sắp xếp theo entry_date, có thể lọc theo loại chứng từ (source_type) hoặc tài khoản

### Requirement: Bảng cân đối phát sinh (TrialBalance)
Hệ thống SHALL lập bảng cân đối phát sinh tổng hợp.

#### Scenario: Lập bảng cân đối phát sinh
- **WHEN** user chọn kỳ
- **THEN** hiển thị theo từng tài khoản: số dư đầu kỳ (Nợ/Có), phát sinh trong kỳ (Nợ/Có), số dư cuối kỳ (Nợ/Có). Tổng Nợ đầu kỳ MUST = Tổng Có đầu kỳ, Tổng Nợ phát sinh MUST = Tổng Có phát sinh, Tổng Nợ cuối kỳ MUST = Tổng Có cuối kỳ

#### Scenario: Drill-down từ cân đối vào sổ cái
- **WHEN** user bấm vào 1 dòng tài khoản trên bảng cân đối
- **THEN** mở sổ cái của tài khoản đó trong kỳ tương ứng
