## ADDED Requirements

### Requirement: Workflow, controls và nghiệm thu của Phase 5 phải bám theo cấu trúc refine
Tài liệu Phase 5 SHALL cập nhật workflow tổng, controls chung, kết quả bàn giao và tiêu chí nghiệm thu để tương thích với cấu trúc đã chia nhỏ hơn ở các cụm hóa đơn và thuế.

#### Scenario: Review controls Phase 5 sau khi refine
- **WHEN** người dùng xem các phần workflow tổng, rule chung và nghiệm thu của Phase 5
- **THEN** tài liệu SHALL phản ánh được các điểm kiểm soát, quyền phê duyệt và acceptance theo từng cụm nghiệp vụ đã được tách nhỏ

## IMPLEMENTATION STATUS: DONE

- Workflow tổng Phase 5 cập nhật: liệt kê control point cho từng cụm 6.2.x–6.9.x
- Tiêu chí nghiệm thu cập nhật: mỗi dòng nghiệm thu tham chiếu rõ số cụm (6.2.x, 6.3.x…)
- Posting checkpoint được phân loại: cụm nào chỉ review dữ liệu vs. cụm nào tạo bút toán (liên kết chứng từ, hạch toán thuế)
- Rule chung Phase 5 bổ sung: override cảnh báo, khóa kỳ và phân quyền chốt bảng kê / tờ khai
