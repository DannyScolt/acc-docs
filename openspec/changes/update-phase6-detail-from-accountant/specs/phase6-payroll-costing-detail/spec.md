## ADDED Requirements

### Requirement: Chi tiết hóa cụm lương và giá thành của Phase 6
Tài liệu Phase 6 SHALL mô tả chi tiết các mục 7.3 và 7.4 ở mức tương đương Phase 1, bao gồm lương cơ bản phục vụ hạch toán, phân bổ chi phí lương, tập hợp chi phí, tính giá thành và kết chuyển giá thành.

#### Scenario: Bao phủ đầy đủ lương và giá thành
- **WHEN** người dùng đọc các mục 7.3 và 7.4 trong HTML
- **THEN** tài liệu SHALL mô tả rõ actor, điều kiện, use case có mã, workflow, business rules và ảnh hưởng kế toán cho từng nhóm nghiệp vụ lương và giá thành

### Requirement: Lương cơ bản phục vụ hạch toán phải có giới hạn phạm vi rõ ràng
Tài liệu SHALL mô tả rõ rằng Phase 6 chỉ bao phủ phạm vi lương kế toán cơ bản, đồng thời xác định các use case nhập bảng lương, phân bổ lương, hạch toán chi phí lương, trả lương và đối chiếu đã trả/chưa trả.

#### Scenario: Review phạm vi lương của Phase 6
- **WHEN** người dùng xem phần tiền lương cơ bản phục vụ hạch toán
- **THEN** tài liệu SHALL thể hiện rõ các nghiệp vụ được bao phủ và các nghiệp vụ HRM sâu hơn chưa thuộc phạm vi hiện tại

### Requirement: Giá thành sản xuất phải có workflow tập hợp và kết chuyển rõ ràng
Tài liệu SHALL mô tả các use case và business rules cho khai báo đối tượng tập hợp chi phí, tập hợp chi phí nguyên vật liệu/nhân công/sản xuất chung, phân bổ chi phí, xác định dở dang, tính giá thành và kết chuyển.

#### Scenario: Tính giá thành cho một đối tượng chi phí
- **WHEN** người dùng xem phần giá thành sản xuất
- **THEN** tài liệu SHALL mô tả được thứ tự xử lý tối thiểu từ tập hợp chi phí đến tính giá thành, xác định chi phí dở dang và kết chuyển kết quả vào kế toán liên quan

### Requirement: Lương và giá thành phải đối chiếu được với số liệu kế toán nguồn
Tài liệu SHALL mô tả cách liên kết bảng lương, phân bổ chi phí lương, chi phí tập hợp, giá thành tính ra và bút toán kết chuyển để phục vụ review và nghiệm thu.

#### Scenario: Đối chiếu chi phí lương và giá thành
- **WHEN** người dùng review phần ảnh hưởng kế toán hoặc tiêu chí nghiệm thu cho lương và giá thành
- **THEN** tài liệu SHALL chỉ rõ cách đối chiếu số liệu với sổ cái, đối tượng chi phí và báo cáo liên quan
