## ADDED Requirements

### Requirement: Báo cáo quỹ — Bảng chức năng mở rộng (2.3.5)
File quy trình SHALL hiển thị 9 báo cáo quỹ (thêm 4 báo cáo mới).

| STT | Chức năng | Mô tả |
|-----|-----------|-------|
| 1 | Sổ quỹ tiền mặt | Báo cáo chi tiết thu chi tồn quỹ |
| 2 | Bảng kê phiếu thu | Danh sách phiếu thu theo kỳ |
| 3 | Bảng kê phiếu chi | Danh sách phiếu chi theo kỳ |
| 4 | Báo cáo tồn quỹ | Theo dõi tồn quỹ theo thời gian |
| 5 | Báo cáo dòng tiền tiền mặt | Theo dõi luồng tiền vào ra |
| 6 | Báo cáo thu chi theo khoản mục | Phân tích mục đích thu chi |
| 7 | Báo cáo thu chi theo đối tượng | Phân tích KH, NCC, NV |
| 8 | Báo cáo chênh lệch kiểm kê | Theo dõi sai lệch quỹ |
| 9 | Dashboard quỹ | Tổng quan tình hình quỹ |

#### Scenario: Hiển thị bảng báo cáo quỹ
- **WHEN** user xem section 2.3.5
- **THEN** hiển thị bảng 9 báo cáo, 4 cái mới so với phiên bản trước

### Requirement: Báo cáo quỹ — Bảng Use Case
File quy trình SHALL hiển thị 6 Use Cases cho báo cáo quỹ.

| Mã UC | Tên Use Case | Actor |
|-------|-------------|-------|
| UC-BC01 | Xem sổ quỹ tiền mặt | Kế toán |
| UC-BC02 | Xem bảng kê phiếu thu | Kế toán |
| UC-BC03 | Xem bảng kê phiếu chi | Kế toán |
| UC-BC04 | Xem báo cáo tồn quỹ | Kế toán trưởng |
| UC-BC05 | Xem báo cáo dòng tiền | Kế toán trưởng |
| UC-BC06 | Xem dashboard quỹ | Ban giám đốc |

#### Scenario: Hiển thị bảng UC báo cáo
- **WHEN** user xem section 2.3.5
- **THEN** hiển thị bảng 6 UC

### Requirement: Báo cáo quỹ — UC-BC05 Báo cáo dòng tiền (luồng chính 6 bước)
File quy trình SHALL hiển thị luồng chính UC-BC05.

| Bước | Mô tả |
|------|-------|
| 1 | Chọn kỳ báo cáo |
| 2 | Hệ thống tổng hợp thu tiền |
| 3 | Hệ thống tổng hợp chi tiền |
| 4 | Nhóm theo khoản mục |
| 5 | Tính chênh lệch dòng tiền |
| 6 | Hiển thị báo cáo |

#### Scenario: Hiển thị UC-BC05
- **WHEN** user xem chi tiết UC-BC05
- **THEN** hiển thị bảng 6 bước

### Requirement: Báo cáo quỹ — Business Rules BR-BC01~BC07
File quy trình SHALL hiển thị 7 Business Rules báo cáo quỹ.

| Mã | Quy tắc |
|----|---------|
| BR-BC01 | Báo cáo chỉ lấy dữ liệu đã ghi sổ |
| BR-BC02 | Báo cáo phải phản ánh đúng dữ liệu tại thời điểm chạy |
| BR-BC03 | Cho phép lọc theo thời gian, đối tượng, khoản mục |
| BR-BC04 | Báo cáo xuất ra phải giống dữ liệu hiển thị |
| BR-BC05 | Dashboard cập nhật realtime |
| BR-BC06 | Báo cáo tồn quỹ lấy tồn cuối ngày |
| BR-BC07 | Báo cáo dòng tiền phân loại theo nhóm thu chi |

#### Scenario: Hiển thị BR báo cáo quỹ
- **WHEN** user xem section 2.3.5
- **THEN** hiển thị bảng 7 Business Rules
