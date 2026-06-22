## ADDED Requirements

### Requirement: Định khoản chi hoàn tiền khách hàng
Bảng định khoản SHALL bao gồm nghiệp vụ "Chi hoàn tiền khách hàng" cho payment_type = refund_return.

| STT | Nghiệp vụ | Nợ (TK) | Có (TK) | Điều kiện | Ghi chú |
|-----|-----------|---------|---------|-----------|---------|
| 27 | Chi hoàn tiền khách hàng | `[CẦN KẾ TOÁN XÁC NHẬN: 131 hay 521 hay TK khác?]` | 111 | payment_type = refund_return | Nghiệp vụ mới từ docx kế toán |

#### Scenario: Ghi sổ khi duyệt phiếu chi hoàn tiền
- **WHEN** phiếu chi refund_return được duyệt
- **THEN** sinh journal_entry với debit_account = TK được kế toán xác nhận, credit = 111
