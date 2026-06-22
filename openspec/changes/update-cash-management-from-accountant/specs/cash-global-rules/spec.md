## ADDED Requirements

### Requirement: Business Rules toàn phân hệ quỹ BR-G01~G08
File quy trình SHALL hiển thị section mới "Business Rules Toàn Phân Hệ Quỹ" với 8 quy tắc.

| Mã | Quy tắc |
|----|---------|
| BR-G01 | Không cho phép chi vượt tồn quỹ nếu bật cấu hình "Không cho âm quỹ" |
| BR-G02 | Mọi chứng từ quỹ phải sinh bút toán sổ cái tương ứng |
| BR-G03 | Chứng từ đã khóa kỳ không được sửa, xóa hoặc duyệt lại |
| BR-G04 | Tồn đầu kỳ sau = Tồn cuối kỳ trước |
| BR-G05 | Số chứng từ không được trùng trong cùng năm tài chính |
| BR-G06 | Mọi thao tác thêm, sửa, xóa, duyệt phải ghi Audit Log |
| BR-G07 | Người dùng chỉ được xem dữ liệu thuộc phạm vi được phân quyền |
| BR-G08 | Hệ thống phải lưu lịch sử thay đổi dữ liệu tối thiểu theo người thao tác, thời gian và nội dung thay đổi |

#### Scenario: Hiển thị BR toàn phân hệ
- **WHEN** user xem section 2.3
- **THEN** hiển thị bảng 8 Business Rules BR-G01~G08 ở cuối section quỹ tiền mặt

### Requirement: Bảng định khoản mở rộng (6→26 nghiệp vụ)
File quy trình SHALL cập nhật bảng định khoản từ 6 dòng lên 26 nghiệp vụ, bao gồm nghiệp vụ mới "Chi hoàn tiền KH".

Bảng 26 nghiệp vụ lấy từ file spec lập trình (general-ledger/spec.md), thêm dòng mới:
- Chi hoàn tiền KH: Nợ `[CẦN KẾ TOÁN XÁC NHẬN]` / Có 111, payment_type = refund_return

Các mục `[CẦN KẾ TOÁN XÁC NHẬN]` từ bảng hiện có MUST được giữ nguyên marker.

#### Scenario: Hiển thị bảng định khoản đầy đủ
- **WHEN** user xem bảng định khoản Phase 1
- **THEN** hiển thị 26+ nghiệp vụ với các cột: STT, Nghiệp vụ, Nợ (TK), Có (TK), Điều kiện, Ghi chú
