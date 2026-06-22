## ADDED Requirements

### Requirement: Cụm lương và giá thành của Phase 6 phải được chia thành các cụm thao tác rõ hơn
Tài liệu Phase 6 SHALL tách rõ hơn các cụm khai báo, nhập liệu, phân bổ, đối chiếu, tính toán, kết chuyển và cảnh báo trong phần lương và giá thành để tăng tính implementable.

#### Scenario: Review cấu trúc payroll/costing refine
- **WHEN** người dùng xem phần lương hoặc giá thành
- **THEN** tài liệu SHALL giúp phân biệt rõ các cụm nghiệp vụ nhỏ hơn cùng trạng thái, rule và điểm kiểm soát tương ứng thay vì chỉ là một bảng tổng hợp lớn

## IMPLEMENTATION STATUS: DONE

- **7.3**: 7.3.1 Khai báo & nhập liệu bảng lương (BR-PAY-05: quyền xem dữ liệu nhạy cảm) | 7.3.2 Phân bổ chi phí lương & hạch toán | 7.3.3 Trả lương & đối chiếu
- **7.4**: 7.4.1 Khai báo đối tượng & tập hợp chi phí | 7.4.2 Phân bổ chi phí chung & xác định dở dang | 7.4.3 Tính giá thành / kết chuyển & báo cáo

Cụm lương: phân quyền tách biệt giữa nhập liệu (kế toán tiền lương) và phê duyệt (kế toán trưởng); dữ liệu nhạy cảm chỉ hiển thị theo quyền.
Cụm giá thành: BR-COST-02 (không chốt khi chưa xác định dở dang) và BR-COST-05 (cảnh báo tính lại) được gắn rõ tại cụm 7.4.2 và 7.4.3.
