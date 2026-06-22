## ADDED Requirements

### Requirement: Cụm dashboard, phân tích, forecast và ngân sách của Phase 6 phải không còn bị nén trong một block lớn
Tài liệu Phase 6 SHALL trình bày rõ ràng hơn các scope dashboard quản trị, phân tích tài chính, dự báo dòng tiền, lập ngân sách, theo dõi thực hiện và cảnh báo vượt ngân sách như các đơn vị review tách biệt bên trong cùng chương.

#### Scenario: Review cấu trúc management/reporting refine
- **WHEN** người dùng xem phần quản trị nâng cao của Phase 6
- **THEN** tài liệu SHALL cho phép nhận ra rõ các scope và workflow riêng của dashboard, analysis, forecast, budget và budget control thay vì chỉ là một bảng dày chữ

## IMPLEMENTATION STATUS: DONE

- **7.8.1** Dashboard tổng quan & phân tích tài chính: phân quyền theo vai trò (ban giám đốc chỉ xem; kế toán trưởng cấu hình)
- **7.8.2** Dự báo dòng tiền: kế toán trưởng phê duyệt kịch bản trước khi phát hành; BR-MGMT-03 ghi rõ giả định
- **7.8.3** Ngân sách / theo dõi / cảnh báo: khai báo → phê duyệt → theo dõi thực hiện → cảnh báo vượt ngân sách → điều chỉnh / tái phê duyệt

Không có cụm nào trong 7.8 tạo bút toán trực tiếp; mọi chỉ tiêu phải truy vết được về dữ liệu kế toán nguồn (BR-MGMT-01, BR-MGMT-02).
