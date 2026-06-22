## ADDED Requirements

### Requirement: Ghi sổ, kết chuyển và báo cáo tổng hợp của Phase 4 phải được mô tả chi tiết trong tài liệu liên kết
Tài liệu và đặc tả `general-ledger` SHALL phản ánh rõ ảnh hưởng ghi sổ từ chứng từ nghiệp vụ khác, phân bổ chi phí, kết chuyển cuối kỳ, khóa kỳ, sổ kế toán tổng hợp và báo cáo tài chính khi Phase 4 được chi tiết hóa, bao gồm cả tracing từ báo cáo về sổ sách và chứng từ nguồn.

#### Scenario: Truy vết từ điều chỉnh cuối kỳ sang sổ cái và báo cáo
- **WHEN** người dùng review một nghiệp vụ tổng hợp, kết chuyển hoặc báo cáo tài chính trong Phase 4
- **THEN** tài liệu SHALL chỉ rõ chứng từ nguồn, điều kiện ghi sổ, ảnh hưởng tới sổ cái/sổ nhật ký/sổ chi tiết và mối liên hệ tới báo cáo tài chính

#### Scenario: Đồng bộ control cuối kỳ giữa Phase 4 và general-ledger
- **WHEN** các business rules Phase 4 được bổ sung từ tài liệu accountant
- **THEN** đặc tả `general-ledger` SHALL giữ tính nhất quán với các quy tắc cân đối bút toán, chỉ ghi sổ chứng từ hợp lệ, kiểm soát kết chuyển, khóa kỳ và truy vết từ báo cáo về dữ liệu nguồn
