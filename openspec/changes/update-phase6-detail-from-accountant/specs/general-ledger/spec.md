## ADDED Requirements

### Requirement: Ghi sổ từ nghiệp vụ mở rộng của Phase 6 phải được mô tả chi tiết trong tài liệu liên kết
Tài liệu và đặc tả `general-ledger` SHALL phản ánh rõ ảnh hưởng ghi sổ từ khấu hao tài sản, phân bổ công cụ dụng cụ/chi phí trả trước, chi phí lương, giá thành, lãi vay, trả nợ và các giao dịch e-banking khi tài liệu Phase 6 được chi tiết hóa.

#### Scenario: Truy vết từ nghiệp vụ Phase 6 sang journal entry
- **WHEN** người dùng review một nghiệp vụ tài sản, phân bổ, lương, giá thành, vay hoặc e-banking trong Phase 6
- **THEN** tài liệu SHALL chỉ rõ thời điểm phát sinh ghi sổ, chứng từ nguồn liên quan và ảnh hưởng tới sổ cái, công nợ, tiền hoặc chi phí tương ứng

### Requirement: Đồng bộ rule ghi sổ giữa Phase 6 và general-ledger
Tài liệu SHALL giữ tính nhất quán giữa business rules của Phase 6 và các nguyên tắc ghi sổ của sổ cái, bao gồm truy vết chứng từ nguồn, không sửa trực tiếp bút toán đã ghi sổ, không ghi vào kỳ đã khóa và đối chiếu được với số liệu nguồn.

#### Scenario: Review tính nhất quán giữa Phase 6 và sổ cái
- **WHEN** business rules của Phase 6 được bổ sung cho khấu hao, phân bổ, lương, giá thành, vay hoặc e-banking
- **THEN** đặc tả `general-ledger` SHALL phản ánh các giới hạn ghi sổ tương ứng để tránh mâu thuẫn với Phase 1 và các capability hiện có
