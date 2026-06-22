## ADDED Requirements

### Requirement: Các phân hệ bảng kê, kê khai và nộp thuế của Phase 5 phải được chia thành cụm thao tác rõ hơn
Tài liệu Phase 5 SHALL tách rõ các cụm thao tác lập bảng kê, rà soát sai lệch, chốt bảng kê, lập tờ khai, chốt tờ khai, điều chỉnh và theo dõi nộp thuế để gần với cách phân rã của Phase 1.

#### Scenario: Review cấu trúc tax declaration refine
- **WHEN** người dùng xem các mục 6.7 đến 6.9
- **THEN** tài liệu SHALL cho phép nhận ra các cụm thao tác nhỏ hơn cùng quyền xử lý và trạng thái kiểm soát tương ứng thay vì chỉ thấy một bảng mô tả chung cho từng mục lớn

## IMPLEMENTATION STATUS: DONE

- **6.7**: 6.7.1 Lập & rà soát bảng kê (quyền: kế toán thuế lập, kế toán trưởng rà soát) | 6.7.2 Chốt bảng kê & đối chiếu (quyền: kế toán trưởng chốt)
- **6.8**: 6.8.1 Lập tờ khai thuế | 6.8.2 Chốt tờ khai & nộp thuế (quyền: kế toán trưởng chốt, lập giấy nộp tiền) | 6.8.3 Điều chỉnh tờ khai & bổ sung
- **6.9**: 6.9.1 Báo cáo kiểm soát nội bộ | 6.9.2 Báo cáo nộp cơ quan thuế

Trạng thái kiểm soát đầy đủ cho từng cụm: Bảng kê → Chốt bảng kê → Tờ khai → Chốt tờ khai → Đã nộp → Đã điều chỉnh.
