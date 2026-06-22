## ADDED Requirements

### Requirement: Kiểm kê quỹ — Bảng chức năng mở rộng (2.3.4)
File quy trình SHALL hiển thị 8 chức năng kiểm kê quỹ.

| STT | Chức năng | Mô tả |
|-----|-----------|-------|
| 1 | Lập biên bản kiểm kê quỹ | Ghi nhận số tiền thực tế kiểm kê |
| 2 | Nhập số lượng theo mệnh giá | Kiểm kê chi tiết từng loại tiền |
| 3 | So sánh tồn thực tế với tồn sổ | Tự động tính chênh lệch |
| 4 | Duyệt biên bản kiểm kê | Xác nhận kết quả kiểm kê |
| 5 | Xử lý chênh lệch quỹ | Sinh chứng từ điều chỉnh |
| 6 | In biên bản kiểm kê | In theo mẫu |
| 7 | Lưu lịch sử kiểm kê | Theo dõi các lần kiểm kê |
| 8 | Tra cứu kiểm kê | Tìm kiếm các đợt kiểm kê trước |

#### Scenario: Hiển thị bảng chức năng kiểm kê
- **WHEN** user xem section 2.3.4
- **THEN** hiển thị bảng 8 chức năng bao gồm "Nhập số lượng theo mệnh giá"

### Requirement: Kiểm kê quỹ — Bảng Use Case
File quy trình SHALL hiển thị 6 Use Cases cho kiểm kê quỹ.

| Mã UC | Tên Use Case | Actor |
|-------|-------------|-------|
| UC-KQ01 | Lập biên bản kiểm kê | Thủ quỹ |
| UC-KQ02 | Gửi duyệt kiểm kê | Thủ quỹ |
| UC-KQ03 | Duyệt kiểm kê | Kế toán trưởng |
| UC-KQ04 | Điều chỉnh chênh lệch | Kế toán |
| UC-KQ05 | In biên bản kiểm kê | Kế toán |
| UC-KQ06 | Xem lịch sử kiểm kê | Kế toán |

#### Scenario: Hiển thị bảng UC kiểm kê
- **WHEN** user xem section 2.3.4
- **THEN** hiển thị bảng 6 UC

### Requirement: Kiểm kê quỹ — UC-KQ01 Lập biên bản (luồng chính 7 bước)
File quy trình SHALL hiển thị luồng chính UC-KQ01.

| Bước | Mô tả |
|------|-------|
| 1 | Tạo biên bản kiểm kê |
| 2 | Nhập thông tin kiểm kê |
| 3 | Nhập số lượng từng mệnh giá |
| 4 | Hệ thống tính tổng tiền thực tế |
| 5 | Hệ thống lấy tồn sổ |
| 6 | Tính chênh lệch |
| 7 | Lưu biên bản |

#### Scenario: Hiển thị UC-KQ01
- **WHEN** user xem chi tiết UC-KQ01
- **THEN** hiển thị bảng 7 bước

### Requirement: Kiểm kê quỹ — UC-KQ04 Điều chỉnh chênh lệch (luồng chính 6 bước)
File quy trình SHALL hiển thị luồng chính UC-KQ04.

| Bước | Mô tả |
|------|-------|
| 1 | Chọn biên bản đã duyệt |
| 2 | Chọn điều chỉnh |
| 3 | Hệ thống xác định thừa hoặc thiếu |
| 4 | Sinh phiếu thu hoặc phiếu chi điều chỉnh |
| 5 | Cập nhật tồn quỹ |
| 6 | Hoàn thành điều chỉnh |

#### Scenario: Hiển thị UC-KQ04
- **WHEN** user xem chi tiết UC-KQ04
- **THEN** hiển thị bảng 6 bước

### Requirement: Kiểm kê quỹ — Workflow (5 trạng thái)
File quy trình SHALL hiển thị workflow kiểm kê quỹ.

| Trạng thái | Mô tả |
|------------|-------|
| Nháp | Đang nhập liệu |
| Chờ duyệt | Đã gửi duyệt |
| Đã duyệt | Đã được phê duyệt |
| Đã điều chỉnh | Đã xử lý chênh lệch |
| Hủy | Không sử dụng |

#### Scenario: Hiển thị workflow kiểm kê
- **WHEN** user xem section 2.3.4
- **THEN** hiển thị bảng 5 trạng thái với mô tả

### Requirement: Kiểm kê quỹ — Business Rules BR-KQ01~KQ10
File quy trình SHALL hiển thị 10 Business Rules kiểm kê quỹ.

| Mã | Quy tắc |
|----|---------|
| BR-KQ01 | Số biên bản kiểm kê tự động tăng |
| BR-KQ02 | Một quỹ chỉ có một biên bản nháp tại một thời điểm |
| BR-KQ03 | Chỉ biên bản đã duyệt mới được điều chỉnh |
| BR-KQ04 | Không được điều chỉnh nhiều lần cho cùng một biên bản |
| BR-KQ05 | Chênh lệch = Tồn thực tế − Tồn sổ |
| BR-KQ06 | Chênh lệch dương sinh phiếu thu điều chỉnh |
| BR-KQ07 | Chênh lệch âm sinh phiếu chi điều chỉnh |
| BR-KQ08 | Sau điều chỉnh, tồn sổ phải bằng tồn thực tế |
| BR-KQ09 | Không cho sửa biên bản đã duyệt |
| BR-KQ10 | Không được xóa lịch sử kiểm kê |

#### Scenario: Hiển thị BR kiểm kê
- **WHEN** user xem section 2.3.4
- **THEN** hiển thị bảng 10 Business Rules
