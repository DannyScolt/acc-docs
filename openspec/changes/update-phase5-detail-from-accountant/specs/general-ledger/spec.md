## ADDED Requirements

### Requirement: Ghi sổ từ nghiệp vụ hóa đơn điện tử và thuế của Phase 5 phải được mô tả chi tiết trong tài liệu liên kết
Tài liệu và đặc tả `general-ledger` SHALL phản ánh rõ ảnh hưởng ghi sổ từ các nghiệp vụ hóa đơn đầu vào, hóa đơn đầu ra, khấu trừ thuế GTGT, nghĩa vụ thuế và nộp thuế khi tài liệu Phase 5 được chi tiết hóa.

#### Scenario: Truy vết từ hóa đơn hoặc nghĩa vụ thuế sang journal entry
- **WHEN** người dùng review một nghiệp vụ hóa đơn điện tử, kê khai thuế hoặc giấy nộp tiền trong Phase 5
- **THEN** tài liệu SHALL chỉ rõ thời điểm phát sinh ghi sổ, chứng từ nguồn liên quan và ảnh hưởng tới thuế đầu vào/đầu ra, công nợ, tiền hoặc sổ cái

### Requirement: Đồng bộ rule ghi sổ giữa Phase 5 và general-ledger
Tài liệu SHALL giữ tính nhất quán giữa các business rules Phase 5 và các nguyên tắc ghi sổ của sổ cái, bao gồm truy vết chứng từ nguồn, không sửa trực tiếp bút toán đã ghi sổ và không ghi vào kỳ đã khóa.

#### Scenario: Review tính nhất quán giữa Phase 5 và sổ cái
- **WHEN** business rules của Phase 5 được bổ sung cho hóa đơn, tờ khai hoặc nộp thuế
- **THEN** đặc tả `general-ledger` SHALL phản ánh các giới hạn ghi sổ tương ứng để tránh mâu thuẫn với Phase 1 và các capability hiện có
