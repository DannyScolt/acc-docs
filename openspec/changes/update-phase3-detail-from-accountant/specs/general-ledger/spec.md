## ADDED Requirements

### Requirement: Ghi sổ từ nghiệp vụ Phase 3 phải được mô tả chi tiết trong tài liệu liên kết
Tài liệu và đặc tả `general-ledger` SHALL phản ánh rõ ảnh hưởng ghi sổ từ các nghiệp vụ bán hàng, hóa đơn đầu ra, xuất kho, giá vốn, công nợ phải thu, thu tiền khách hàng và giảm trừ doanh thu khi tài liệu Phase 3 được chi tiết hóa.

#### Scenario: Truy vết từ nghiệp vụ bán hàng sang journal entry
- **WHEN** người dùng review một nghiệp vụ bán hàng, xuất kho, thu tiền hoặc trả lại hàng trong Phase 3
- **THEN** tài liệu SHALL chỉ rõ thời điểm phát sinh ghi sổ, chứng từ nguồn liên quan và ảnh hưởng tới doanh thu, thuế GTGT đầu ra, giá vốn, công nợ phải thu, tiền hoặc sổ cái

#### Scenario: Đồng bộ rule ghi sổ giữa Phase 3 và general-ledger
- **WHEN** các business rules Phase 3 được bổ sung từ tài liệu accountant
- **THEN** đặc tả `general-ledger` SHALL giữ tính nhất quán với các quy tắc ghi sổ, kiểm soát chứng từ đã duyệt/đã ghi sổ, truy vết chứng từ nguồn và cân đối bút toán cho doanh thu, giá vốn và công nợ phải thu