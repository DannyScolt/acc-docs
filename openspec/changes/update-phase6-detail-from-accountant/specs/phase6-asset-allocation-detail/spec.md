## ADDED Requirements

### Requirement: Chi tiết hóa cụm tài sản và phân bổ của Phase 6
Tài liệu Phase 6 SHALL mô tả chi tiết các mục 7.1 và 7.2 ở mức tương đương Phase 1, bao gồm tài sản cố định, công cụ dụng cụ, chi phí trả trước, phân bổ định kỳ, trạng thái xử lý và ảnh hưởng kế toán liên quan.

#### Scenario: Bao phủ đầy đủ tài sản và phân bổ
- **WHEN** người dùng đọc các mục 7.1 và 7.2 trong HTML
- **THEN** tài liệu SHALL mô tả rõ actor, điều kiện, dữ liệu đầu vào, use case có mã, luồng chính, kết quả, workflow và business rules cho từng nhóm nghiệp vụ tài sản và phân bổ

### Requirement: Tài sản cố định phải có workflow vòng đời đầy đủ
Tài liệu SHALL mô tả các use case và business rules cho vòng đời tài sản cố định từ khai báo, ghi tăng, tính khấu hao, điều chuyển, đánh giá lại, ghi giảm đến kiểm kê và báo cáo.

#### Scenario: Theo dõi vòng đời tài sản cố định
- **WHEN** người dùng xem phần tài sản cố định của Phase 6
- **THEN** tài liệu SHALL chỉ rõ các trạng thái hoặc bước xử lý tối thiểu từ ghi tăng, đưa vào sử dụng, trích khấu hao, điều chỉnh/điều chuyển, đến ghi giảm và đối chiếu sổ cái

### Requirement: Công cụ dụng cụ và chi phí trả trước phải quản lý phân bổ theo kỳ
Tài liệu SHALL mô tả rõ logic ghi tăng, khai báo kỳ phân bổ, phân bổ định kỳ, ngừng phân bổ, điều chỉnh và theo dõi giá trị còn lại cho công cụ dụng cụ và chi phí trả trước.

#### Scenario: Rà soát phân bổ công cụ dụng cụ hoặc chi phí trả trước
- **WHEN** người dùng xem phần công cụ dụng cụ và chi phí trả trước
- **THEN** tài liệu SHALL mô tả điều kiện bắt đầu phân bổ, cách theo dõi giá trị đã phân bổ/còn lại, các cảnh báo phân bổ trùng kỳ hoặc điều chỉnh, và kết quả ghi sổ tương ứng

### Requirement: Nghiệp vụ tài sản và phân bổ phải truy vết được tới bút toán nguồn
Tài liệu SHALL chỉ rõ ảnh hưởng kế toán của khấu hao, phân bổ, ghi tăng, ghi giảm và điều chỉnh để đối chiếu được với sổ cái.

#### Scenario: Đối chiếu tài sản và phân bổ với sổ cái
- **WHEN** người dùng review bảng định khoản hoặc phần ảnh hưởng kế toán cho tài sản và phân bổ
- **THEN** tài liệu SHALL giúp truy vết được mỗi bút toán tự động hoặc thủ công về tài sản, công cụ dụng cụ hoặc khoản chi phí trả trước nguồn
