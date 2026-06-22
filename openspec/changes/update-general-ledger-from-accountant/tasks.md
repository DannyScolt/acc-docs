## 1. Cập nhật HTML section 2.5

- [x] 1.1 Viết lại section 2.5.1 Ghi sổ kế toán theo format chi tiết `Nội dung / Chi tiết`
- [x] 1.2 Thêm đầy đủ Mục tiêu, Actor, Chức năng, Luồng chính 9 bước, Kết quả và BR-GL-01 ~ BR-GL-07 cho 2.5.1
- [x] 1.3 Viết lại section 2.5.2 Sổ cái theo format chi tiết `Nội dung / Chi tiết`
- [x] 1.4 Thêm đầy đủ Mục tiêu, Actor, Chức năng, Luồng chính 8 bước, Kết quả và BR-LEDGER-01 ~ BR-LEDGER-04 cho 2.5.2
- [x] 1.5 Viết lại section 2.5.3 Sổ nhật ký chung theo format chi tiết `Nội dung / Chi tiết`
- [x] 1.6 Thêm đầy đủ Mục tiêu, Actor, Chức năng, Luồng chính 6 bước, Kết quả và BR-JE-01 ~ BR-JE-04 cho 2.5.3
- [x] 1.7 Viết lại section 2.5.4 Bảng cân đối phát sinh theo format chi tiết `Nội dung / Chi tiết`
- [x] 1.8 Thêm đầy đủ Mục tiêu, Actor, Chức năng, Luồng chính 9 bước, Kết quả và BR-TB-01 ~ BR-TB-04 cho 2.5.4
- [x] 1.9 Thêm section Business Rules toàn phân hệ Sổ cái & hệ thống tài khoản với BR-GLOBAL-01 ~ BR-GLOBAL-20

## 2. Cập nhật OpenSpec spec

- [x] 2.1 Bổ sung capability mới `general-ledger-update` để phản ánh yêu cầu cập nhật section 2.5 HTML
- [x] 2.2 Mở rộng spec `general-ledger` với chi tiết nghiệp vụ ghi sổ kế toán và BR-GL-01 ~ BR-GL-07
- [x] 2.3 Mở rộng spec `general-ledger` với chi tiết nghiệp vụ sổ cái và BR-LEDGER-01 ~ BR-LEDGER-04
- [x] 2.4 Mở rộng spec `general-ledger` với chi tiết nghiệp vụ nhật ký chung và BR-JE-01 ~ BR-JE-04
- [x] 2.5 Mở rộng spec `general-ledger` với chi tiết nghiệp vụ bảng cân đối phát sinh và BR-TB-01 ~ BR-TB-04
- [x] 2.6 Bổ sung bộ business rules toàn phân hệ BR-GLOBAL-01 ~ BR-GLOBAL-20 vào delta spec `general-ledger`

## 3. Rà soát và kiểm tra

- [x] 3.1 Đối chiếu section 2.5 HTML với nội dung kế toán cung cấp để đảm bảo không thiếu mục nào
- [x] 3.2 Kiểm tra HTML valid, không phát sinh nested table hoặc vỡ ranh giới với Bảng định khoản mẫu
- [x] 3.3 Kiểm tra section 2.4 và phần sau 2.5 không bị ảnh hưởng khi cập nhật
- [x] 3.4 Xác nhận change ở trạng thái apply-ready sau khi hoàn tất artifacts
