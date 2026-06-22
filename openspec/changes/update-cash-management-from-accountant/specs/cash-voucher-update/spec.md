## ADDED Requirements

### Requirement: Phiếu thu — Bảng chức năng mở rộng (2.3.1)
Hệ thống SHALL hiển thị 16 chức năng phiếu thu trong file quy trình HTML.

| STT | Chức năng | Mô tả |
|-----|-----------|-------|
| 1 | Lập phiếu thu | Ghi nhận nghiệp vụ thu tiền mặt |
| 2 | Thu tiền khách hàng | Thu công nợ KH và giảm công nợ phải thu |
| 3 | Thu hoàn ứng nhân viên | Thu hồi khoản tạm ứng còn thừa |
| 4 | Thu khác | Các khoản thu khác không liên quan công nợ |
| 5 | Chọn đối tượng thu | KH, NV, NCC hoặc đối tượng khác |
| 6 | Hạch toán tự động | Sinh bút toán theo loại nghiệp vụ |
| 7 | Đính kèm chứng từ | Upload hóa đơn, biên nhận, chứng từ liên quan |
| 8 | Lưu nháp | Lưu chứng từ chưa hoàn tất |
| 9 | Gửi duyệt | Chuyển chứng từ sang trạng thái chờ duyệt |
| 10 | Duyệt phiếu thu | Người có quyền xác nhận chứng từ |
| 11 | Từ chối duyệt | Trả lại chứng từ và nhập lý do |
| 12 | Ghi sổ | Sinh bút toán kế toán và cập nhật sổ quỹ |
| 13 | Hủy phiếu thu | Hủy chứng từ khi nhập sai |
| 14 | In phiếu thu | In theo mẫu doanh nghiệp |
| 15 | Xuất PDF | Xuất file PDF |
| 16 | Xem lịch sử thao tác | Theo dõi toàn bộ thay đổi chứng từ |

#### Scenario: Hiển thị bảng chức năng phiếu thu
- **WHEN** user xem section 2.3.1 trong file quy trình
- **THEN** hiển thị bảng 16 chức năng với STT, tên, mô tả

### Requirement: Phiếu thu — State machine (5+2 trạng thái)
File quy trình SHALL hiển thị state machine chứng từ phiếu thu với 5 trạng thái chính và 2 trạng thái phụ.

**Trạng thái chính:** Nháp → Chờ duyệt → Đã duyệt → Đã ghi sổ → Đã khóa kỳ

**Trạng thái phụ:** Từ chối (từ Chờ duyệt), Đã hủy (từ Nháp hoặc Chờ duyệt)

#### Scenario: Hiển thị state machine phiếu thu
- **WHEN** user xem section 2.3.1
- **THEN** hiển thị diagram state machine với 7 trạng thái và mũi tên chuyển tiếp

### Requirement: Phiếu thu — Field map (3 nhóm)
File quy trình SHALL hiển thị field map phiếu thu gồm 3 nhóm thông tin.

**Thông tin chung:** Số chứng từ, Ngày chứng từ, Ngày hạch toán, Quỹ tiền mặt, Đối tượng, Diễn giải

**Thông tin hạch toán:** Tài khoản Nợ, Tài khoản Có, Số tiền, Khoản mục chi phí, Phòng ban, Chi nhánh

**Thông tin công nợ:** Khách hàng, Hóa đơn, Số tiền thanh toán, Số tiền còn lại

#### Scenario: Hiển thị field map phiếu thu
- **WHEN** user xem section 2.3.1
- **THEN** hiển thị 3 nhóm field với tên field rõ ràng

### Requirement: Phiếu chi — Bảng chức năng mở rộng (2.3.2)
Hệ thống SHALL hiển thị 17 chức năng phiếu chi, bao gồm nghiệp vụ mới "Chi hoàn tiền khách hàng".

| STT | Chức năng | Mô tả |
|-----|-----------|-------|
| 1 | Lập phiếu chi | Ghi nhận nghiệp vụ chi tiền mặt |
| 2 | Thanh toán nhà cung cấp | Giảm công nợ phải trả |
| 3 | Chi tạm ứng | Tạm ứng tiền cho nhân viên |
| 4 | Chi hoàn tiền khách hàng | Hoàn tiền hoặc trả lại tiền |
| 5 | Chi khác | Chi phí hoạt động hoặc nghiệp vụ khác |
| 6 | Chọn đối tượng chi | NCC, NV, KH hoặc khác |
| 7 | Hạch toán tự động | Sinh bút toán theo nghiệp vụ |
| 8 | Đính kèm chứng từ | Hóa đơn, đề nghị thanh toán, hợp đồng |
| 9 | Lưu nháp | Lưu chứng từ chưa hoàn thiện |
| 10 | Gửi duyệt | Chuyển sang trạng thái chờ duyệt |
| 11 | Duyệt phiếu chi | Người có quyền duyệt |
| 12 | Từ chối duyệt | Trả lại chứng từ |
| 13 | Ghi sổ | Cập nhật sổ quỹ và sổ cái |
| 14 | Hủy phiếu chi | Hủy chứng từ sai |
| 15 | In phiếu chi | In theo mẫu |
| 16 | Xuất PDF | Xuất PDF chứng từ |
| 17 | Xem lịch sử thao tác | Truy vết toàn bộ thay đổi |

#### Scenario: Hiển thị bảng chức năng phiếu chi
- **WHEN** user xem section 2.3.2
- **THEN** hiển thị bảng 17 chức năng bao gồm "Chi hoàn tiền khách hàng"

### Requirement: Phiếu chi — Actors
File quy trình SHALL hiển thị bảng Actor cho phiếu chi.

| Actor | Vai trò |
|-------|---------|
| Kế toán quỹ | Tạo, nhập liệu |
| Thủ quỹ | Kiểm tra, xác nhận |
| Kế toán trưởng | Duyệt |
| Giám đốc | Phê duyệt đặc biệt |

#### Scenario: Hiển thị actors phiếu chi
- **WHEN** user xem section 2.3.2
- **THEN** hiển thị bảng 4 actors với vai trò

### Requirement: Phiếu chi — Use Case luồng chính
File quy trình SHALL hiển thị Use Case phiếu chi với luồng chính 11 bước.

| Bước | Mô tả |
|------|-------|
| 1 | Tạo phiếu chi |
| 2 | Chọn đối tượng nhận tiền |
| 3 | Nhập số tiền |
| 4 | Chọn tài khoản hạch toán |
| 5 | Đính kèm chứng từ |
| 6 | Lưu nháp |
| 7 | Gửi duyệt |
| 8 | Người có thẩm quyền duyệt |
| 9 | Ghi sổ |
| 10 | Cập nhật tồn quỹ |
| 11 | Sinh bút toán vào Sổ cái |

#### Scenario: Hiển thị UC phiếu chi
- **WHEN** user xem section 2.3.2
- **THEN** hiển thị luồng chính 11 bước

### Requirement: Phiếu chi — Business Rules BR-Q01~Q10
File quy trình SHALL hiển thị 10 Business Rules cho phiếu thu/chi.

| Mã | Quy tắc |
|----|---------|
| BR-Q01 | Chứng từ phải có số chứng từ duy nhất |
| BR-Q02 | Không cho ghi sổ khi chưa duyệt |
| BR-Q03 | Không cho sửa chứng từ đã ghi sổ |
| BR-Q04 | Hủy chứng từ phải nhập lý do |
| BR-Q05 | Không cho xóa chứng từ đã ghi sổ |
| BR-Q06 | Không cho ghi sổ vào kỳ đã khóa |
| BR-Q07 | Phiếu chi không được làm âm quỹ nếu DN không cho phép |
| BR-Q08 | Tổng Nợ phải bằng Tổng Có |
| BR-Q09 | Người tạo và người duyệt không được là cùng một người (nếu bật kiểm soát nội bộ) |
| BR-Q10 | Mọi thao tác thêm/sửa/xóa/duyệt/hủy phải ghi Audit Log |

#### Scenario: Hiển thị BR phiếu thu/chi
- **WHEN** user xem section 2.3.2
- **THEN** hiển thị bảng 10 Business Rules BR-Q01~Q10
