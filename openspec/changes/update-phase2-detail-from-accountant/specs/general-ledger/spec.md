## ADDED Requirements

### Requirement: Ghi sổ từ nghiệp vụ Phase 2 phải được mô tả chi tiết trong tài liệu liên kết
Tài liệu và đặc tả `general-ledger` SHALL phản ánh rõ ảnh hưởng ghi sổ từ các nghiệp vụ mua hàng, công nợ phải trả, thanh toán nhà cung cấp và kho của Phase 2 khi tài liệu Phase 2 được chi tiết hóa.

#### Scenario: Truy vết từ nghiệp vụ mua hàng sang journal entry
- **WHEN** người dùng review một nghiệp vụ mua hàng hoặc thanh toán nhà cung cấp trong Phase 2
- **THEN** tài liệu SHALL chỉ rõ thời điểm phát sinh ghi sổ, chứng từ nguồn liên quan và ảnh hưởng tới công nợ, kho, thuế hoặc sổ cái

#### Scenario: Đồng bộ rule ghi sổ giữa Phase 2 và general-ledger
- **WHEN** các business rules Phase 2 được bổ sung
- **THEN** đặc tả `general-ledger` SHALL giữ tính nhất quán với các quy tắc ghi sổ, không ghi vào kỳ đã khóa, truy vết chứng từ nguồn và kiểm soát cân đối bút toán
