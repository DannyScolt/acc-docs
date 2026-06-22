## ADDED Requirements

### Requirement: Cụm tài sản và phân bổ của Phase 6 phải được chia thành các đơn vị review nhỏ hơn
Tài liệu Phase 6 SHALL tách rõ hơn các cụm ghi tăng, phân bổ, khấu hao, điều chỉnh, kiểm kê, theo dõi giá trị còn lại và báo cáo thay vì chỉ mô tả mỗi module bằng một bảng lớn.

#### Scenario: Review cấu trúc asset/allocation refine
- **WHEN** người dùng xem phần tài sản cố định hoặc công cụ dụng cụ / chi phí trả trước
- **THEN** tài liệu SHALL phản ánh được các bước vận hành riêng biệt và các điểm kiểm soát tương ứng để gần với cấu trúc của Phase 1

## IMPLEMENTATION STATUS: DONE

- **7.1**: 7.1.1 Ghi tăng & khai báo (kế toán TSCĐ tạo, kế toán trưởng duyệt) | 7.1.2 Khấu hao định kỳ (job tự động, kế toán trưởng phê duyệt) | 7.1.3 Điều chỉnh / điều chuyển / đánh giá lại | 7.1.4 Ghi giảm & kiểm kê
- **7.2**: 7.2.1 Ghi tăng & khai báo phân bổ | 7.2.2 Phân bổ định kỳ & theo dõi giá trị còn lại | 7.2.3 Điều chỉnh / ngừng phân bổ & kiểm kê

Ảnh hưởng kế toán: TK 211/214/811/153/242/627/641/642 được gắn rõ tại từng cụm con.
