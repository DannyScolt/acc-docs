## ADDED Requirements

### Requirement: Sổ quỹ — Bảng chức năng mở rộng (2.3.3)
File quy trình SHALL hiển thị 12 chức năng sổ quỹ.

| STT | Chức năng | Mô tả |
|-----|-----------|-------|
| 1 | Xem sổ quỹ tiền mặt | Theo dõi toàn bộ phát sinh thu, chi và tồn quỹ theo thời gian |
| 2 | Xem tồn quỹ tức thời | Hiển thị số dư quỹ hiện tại theo thời gian thực |
| 3 | Lọc sổ quỹ theo thời gian | Tra cứu theo ngày, tuần, tháng, quý, năm hoặc tùy chọn |
| 4 | Lọc sổ quỹ theo đối tượng | Tra cứu theo KH, NCC, NV, cổ đông |
| 5 | Lọc sổ quỹ theo khoản mục | Tra cứu theo nhóm thu chi, mục đích sử dụng tiền |
| 6 | Xem chi tiết chứng từ | Từ dòng sổ quỹ mở trực tiếp PT/PC liên quan |
| 7 | Truy vết nguồn phát sinh | Xác định phát sinh từ nghiệp vụ nào |
| 8 | Đối chiếu sổ quỹ với sổ cái | So sánh số dư quỹ và TK tiền mặt trên sổ cái |
| 9 | Xuất sổ quỹ | Xuất Excel hoặc PDF |
| 10 | In sổ quỹ | In trực tiếp theo mẫu quy định |
| 11 | Khóa sổ quỹ | Khóa dữ liệu theo kỳ kế toán |
| 12 | Xem lịch sử chỉnh sửa | Theo dõi thay đổi dữ liệu quỹ |

#### Scenario: Hiển thị bảng chức năng sổ quỹ
- **WHEN** user xem section 2.3.3
- **THEN** hiển thị bảng 12 chức năng

### Requirement: Sổ quỹ — Bảng Use Case tổng hợp
File quy trình SHALL hiển thị bảng 7 Use Cases cho sổ quỹ.

| Mã UC | Tên Use Case | Actor |
|-------|-------------|-------|
| UC-Q01 | Xem sổ quỹ tiền mặt | Thủ quỹ, Kế toán quỹ, Kế toán trưởng |
| UC-Q02 | Xem tồn quỹ tức thời | Thủ quỹ, Kế toán |
| UC-Q03 | Tra cứu sổ quỹ | Thủ quỹ, Kế toán |
| UC-Q04 | Xem chi tiết chứng từ | Thủ quỹ, Kế toán |
| UC-Q05 | Đối chiếu sổ quỹ | Kế toán trưởng |
| UC-Q06 | Xuất/In sổ quỹ | Kế toán |
| UC-Q07 | Khóa sổ quỹ | Kế toán trưởng, Admin |

#### Scenario: Hiển thị bảng UC sổ quỹ
- **WHEN** user xem section 2.3.3
- **THEN** hiển thị bảng 7 UC với mã, tên, actor

### Requirement: Sổ quỹ — UC-Q01 Xem sổ quỹ (luồng ngắn)
File quy trình SHALL hiển thị luồng chính UC-Q01 gồm 7 bước.

Bước: (1) Mở màn hình Sổ quỹ → (2) Chọn khoảng thời gian → (3) HT lấy dữ liệu phát sinh → (4) Tính tồn đầu kỳ → (5) Tính thu, chi từng dòng → (6) Tính tồn cuối từng dòng → (7) Hiển thị dữ liệu

#### Scenario: Hiển thị UC-Q01
- **WHEN** user xem chi tiết UC-Q01
- **THEN** hiển thị bảng 7 bước (Bước + Mô tả)

### Requirement: Sổ quỹ — UC-Q02 Tồn quỹ tức thời (chi tiết đầy đủ)
File quy trình SHALL hiển thị UC-Q02 với format đầy đủ: mục đích, actor, điều kiện tiên quyết, dữ liệu đầu vào, luồng chính 8 bước (3 cột), công thức, luồng ngoại lệ, business rules riêng.

**Mục đích:** Cho phép người dùng xem nhanh số dư quỹ tiền mặt hiện tại tại thời điểm truy cập.

**Actor:** Thủ quỹ, Kế toán quỹ, Kế toán trưởng, Giám đốc

**Điều kiện tiên quyết:** Đã đăng nhập, có quyền xem quỹ tiền mặt.

**Dữ liệu đầu vào (tùy chọn):** Quỹ tiền mặt, Chi nhánh, Đơn vị hạch toán

**Luồng chính:**

| Bước | Người thực hiện | Mô tả |
|------|----------------|-------|
| 1 | Người dùng | Mở màn hình Dashboard Quỹ hoặc Tồn quỹ |
| 2 | Hệ thống | Xác định quỹ được phép truy cập |
| 3 | Hệ thống | Lấy tồn đầu kỳ gần nhất |
| 4 | Hệ thống | Tổng hợp toàn bộ phiếu thu đã ghi sổ |
| 5 | Hệ thống | Tổng hợp toàn bộ phiếu chi đã ghi sổ |
| 6 | Hệ thống | Tổng hợp các chứng từ điều chỉnh quỹ |
| 7 | Hệ thống | Tính tồn quỹ hiện tại |
| 8 | Hệ thống | Hiển thị số dư quỹ hiện tại |

**Công thức:** `Tồn hiện tại = Tồn đầu kỳ + Tổng thu - Tổng chi + Điều chỉnh tăng - Điều chỉnh giảm`

**Luồng ngoại lệ:**
- EX-01: Không tìm thấy dữ liệu quỹ → Thông báo "Không tìm thấy dữ liệu quỹ", người dùng chọn quỹ khác
- EX-02: Không có quyền → Thông báo "Bạn không có quyền xem quỹ này"

**Business Rules:**

| Mã | Quy tắc |
|----|---------|
| BR-Q02-01 | Chỉ tính các chứng từ đã ghi sổ |
| BR-Q02-02 | Không tính chứng từ nháp |
| BR-Q02-03 | Không tính chứng từ hủy |
| BR-Q02-04 | Tồn quỹ hiển thị theo thời gian thực |
| BR-Q02-05 | Không cho phép chỉnh sửa trực tiếp tồn quỹ |

#### Scenario: Hiển thị UC-Q02 đầy đủ
- **WHEN** user xem chi tiết UC-Q02
- **THEN** hiển thị tất cả: mục đích, 4 actors, ĐKTT, dữ liệu đầu vào, bảng 8 bước (3 cột), công thức, 2 EX, 5 BR

### Requirement: Sổ quỹ — UC-Q03 Tra cứu / Lọc sổ quỹ (chi tiết đầy đủ)
File quy trình SHALL hiển thị UC-Q03 với format đầy đủ.

**Mục đích:** Cho phép tìm kiếm và lọc dữ liệu sổ quỹ theo nhiều tiêu chí khác nhau.

**Actor:** Thủ quỹ, Kế toán quỹ, Kế toán trưởng

**Bộ lọc hỗ trợ:**
- Thời gian: Hôm nay, Tuần này, Tháng này, Quý này, Năm nay, Tùy chọn
- Theo chứng từ: Số chứng từ, Loại chứng từ
- Theo đối tượng: Khách hàng, Nhà cung cấp, Nhân viên
- Theo khoản mục: Thu bán hàng, Thu khác, Mua hàng, Chi phí, Thuế
- Theo số tiền: Từ tiền, Đến tiền

**Luồng chính:**

| Bước | Người thực hiện | Mô tả |
|------|----------------|-------|
| 1 | Người dùng | Mở màn hình Sổ quỹ |
| 2 | Người dùng | Nhập điều kiện lọc |
| 3 | Người dùng | Chọn Tìm kiếm |
| 4 | Hệ thống | Kiểm tra điều kiện lọc |
| 5 | Hệ thống | Truy vấn dữ liệu |
| 6 | Hệ thống | Tính toán số dư |
| 7 | Hệ thống | Hiển thị kết quả |

**Luồng ngoại lệ:**
- EX-01: Không có dữ liệu → Hiển thị danh sách rỗng, thông báo "Không có dữ liệu phù hợp"
- EX-02: Ngày bắt đầu > ngày kết thúc → Thông báo "Ngày bắt đầu phải nhỏ hơn ngày kết thúc"

**Business Rules:**

| Mã | Quy tắc |
|----|---------|
| BR-Q03-01 | Có thể kết hợp nhiều điều kiện lọc |
| BR-Q03-02 | Mặc định hiển thị tháng hiện tại |
| BR-Q03-03 | Kết quả được sắp xếp theo ngày tăng dần |
| BR-Q03-04 | Nếu cùng ngày thì sắp xếp theo thời gian tạo |
| BR-Q03-05 | Chỉ hiển thị dữ liệu thuộc phạm vi phân quyền |

#### Scenario: Hiển thị UC-Q03 đầy đủ
- **WHEN** user xem chi tiết UC-Q03
- **THEN** hiển thị: mục đích, 3 actors, bộ lọc 5 nhóm, bảng 7 bước, 2 EX, 5 BR

### Requirement: Sổ quỹ — UC-Q04 Xem chi tiết chứng từ (chi tiết đầy đủ)
File quy trình SHALL hiển thị UC-Q04 với format đầy đủ.

**Mục đích:** Cho phép truy xuất ngược từ dòng sổ quỹ đến chứng từ gốc.

**Actor:** Thủ quỹ, Kế toán quỹ, Kế toán trưởng, Kiểm toán nội bộ

**Nguồn chứng từ:** Phiếu thu, Phiếu chi, Thu công nợ, Chi công nợ, Điều chỉnh quỹ, Điều chỉnh kiểm kê

**Luồng chính:**

| Bước | Người thực hiện | Mô tả |
|------|----------------|-------|
| 1 | Người dùng | Mở Sổ quỹ |
| 2 | Người dùng | Chọn một dòng phát sinh |
| 3 | Người dùng | Click số chứng từ |
| 4 | Hệ thống | Kiểm tra quyền xem |
| 5 | Hệ thống | Tìm chứng từ gốc |
| 6 | Hệ thống | Mở màn hình chi tiết chứng từ |
| 7 | Hệ thống | Hiển thị toàn bộ thông tin chứng từ |

#### Scenario: Hiển thị UC-Q04 đầy đủ
- **WHEN** user xem chi tiết UC-Q04
- **THEN** hiển thị: mục đích, 4 actors (bao gồm Kiểm toán nội bộ), 6 nguồn CT, bảng 7 bước

### Requirement: Sổ quỹ — UC-Q05 Đối chiếu sổ quỹ (luồng ngắn)
File quy trình SHALL hiển thị luồng chính UC-Q05 gồm 5 bước.

Bước: (1) Người dùng chọn kỳ đối chiếu → (2) HT lấy số dư quỹ → (3) HT lấy số dư TK111 → (4) So sánh số liệu → (5) Hiển thị kết quả đối chiếu

#### Scenario: Hiển thị UC-Q05
- **WHEN** user xem chi tiết UC-Q05
- **THEN** hiển thị bảng 5 bước

### Requirement: Sổ quỹ — Business Rules BR-Q01~Q09
File quy trình SHALL hiển thị 9 Business Rules tổng section sổ quỹ.

| Mã | Quy tắc |
|----|---------|
| BR-Q01 | Sổ quỹ chỉ phát sinh từ phiếu thu, phiếu chi và chứng từ điều chỉnh |
| BR-Q02 | Không được nhập trực tiếp vào sổ quỹ |
| BR-Q03 | Tồn cuối = Tồn đầu + Thu − Chi |
| BR-Q04 | Không cho sửa số dư quỹ trực tiếp |
| BR-Q05 | Chứng từ đã khóa kỳ không được sửa hoặc xóa |
| BR-Q06 | Dữ liệu hiển thị theo ngày hạch toán |
| BR-Q07 | Một dòng sổ quỹ phải liên kết được chứng từ nguồn |
| BR-Q08 | Có thể cấu hình không cho phép âm quỹ |
| BR-Q09 | Mọi thay đổi phải ghi Audit Log |

#### Scenario: Hiển thị BR sổ quỹ
- **WHEN** user xem section 2.3.3
- **THEN** hiển thị bảng 9 Business Rules BR-Q01~Q09
