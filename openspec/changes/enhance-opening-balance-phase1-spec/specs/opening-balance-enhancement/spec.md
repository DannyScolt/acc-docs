## ADDED Requirements

### Requirement: Module số dư đầu kỳ SHALL hỗ trợ đầy đủ vòng đời quản lý dữ liệu trước và sau khi khóa
Module Số dư đầu kỳ SHALL cho phép người dùng có quyền xem danh sách, lọc/tìm kiếm, nhập mới, sửa, xóa dữ liệu đầu kỳ khi dữ liệu chưa khóa; đồng thời SHALL hiển thị rõ trạng thái khóa, người khóa và thời điểm khóa.

#### Scenario: Xem và lọc dữ liệu đầu kỳ
- **WHEN** người dùng truy cập chức năng Số dư đầu kỳ và chọn năm tài chính hoặc loại dữ liệu
- **THEN** hệ thống hiển thị danh sách dữ liệu đầu kỳ tương ứng và cho phép lọc theo tài khoản, khách hàng, nhà cung cấp, kho, tài khoản ngân hàng hoặc loại dữ liệu

#### Scenario: Sửa dữ liệu chưa khóa
- **WHEN** người dùng có quyền cập nhật dữ liệu đầu kỳ và bản ghi chưa khóa
- **THEN** hệ thống SHALL cho phép chỉnh sửa dữ liệu và lưu lại phiên bản mới

#### Scenario: Chặn sửa dữ liệu đã khóa
- **WHEN** người dùng cố sửa hoặc xóa dữ liệu đầu kỳ đã khóa
- **THEN** hệ thống SHALL từ chối thao tác và hiển thị thông báo rằng dữ liệu đầu kỳ đã khóa

### Requirement: Module số dư đầu kỳ SHALL hỗ trợ import thực tế theo mẫu có kiểm tra lỗi
Hệ thống SHALL cho phép tải mẫu import, xem trước dữ liệu import, kiểm tra lỗi theo dòng/cột, và áp dụng import theo nguyên tắc all-or-nothing.

#### Scenario: Tải mẫu import
- **WHEN** người dùng chọn tải file mẫu import cho một loại hoặc toàn bộ dữ liệu đầu kỳ
- **THEN** hệ thống SHALL cung cấp file mẫu Excel đúng cấu trúc cột yêu cầu

#### Scenario: Preview và kiểm tra lỗi import
- **WHEN** người dùng tải lên file import số dư đầu kỳ
- **THEN** hệ thống SHALL phân tích dữ liệu, hiển thị preview trước khi lưu và chỉ rõ lỗi theo dòng/cột nếu có

#### Scenario: Import atomic
- **WHEN** file import chứa ít nhất một dòng lỗi
- **THEN** hệ thống SHALL không ghi nhận bất kỳ dòng dữ liệu nào từ file đó

### Requirement: Module số dư đầu kỳ SHALL đối chiếu chi tiết từng nhóm dữ liệu với số dư tài khoản tổng hợp tương ứng
Hệ thống SHALL tách riêng các chức năng kiểm tra cân đối cho tài khoản tổng hợp, công nợ khách hàng, công nợ nhà cung cấp, tồn kho, tiền mặt, tiền gửi ngân hàng, tài sản cố định, công cụ dụng cụ và chi phí trả trước.

#### Scenario: Cân đối tổng Nợ/Có
- **WHEN** người dùng yêu cầu kiểm tra cân đối số dư đầu kỳ
- **THEN** hệ thống SHALL kiểm tra tổng số dư Nợ bằng tổng số dư Có và hiển thị số chênh lệch nếu không khớp

#### Scenario: Đối chiếu công nợ khách hàng
- **WHEN** người dùng yêu cầu đối chiếu công nợ khách hàng đầu kỳ
- **THEN** hệ thống SHALL kiểm tra tổng chi tiết công nợ phải thu khớp với TK 131 và hiển thị khách hàng/chứng từ bị lệch nếu có

#### Scenario: Đối chiếu công nợ nhà cung cấp
- **WHEN** người dùng yêu cầu đối chiếu công nợ nhà cung cấp đầu kỳ
- **THEN** hệ thống SHALL kiểm tra tổng chi tiết công nợ phải trả khớp với TK 331 và hiển thị nhà cung cấp/chứng từ bị lệch nếu có

#### Scenario: Đối chiếu tồn kho
- **WHEN** người dùng yêu cầu đối chiếu tồn kho đầu kỳ
- **THEN** hệ thống SHALL kiểm tra tổng giá trị tồn kho chi tiết theo kho và mặt hàng khớp với các tài khoản hàng tồn kho liên quan

#### Scenario: Đối chiếu tiền mặt và ngân hàng
- **WHEN** người dùng yêu cầu đối chiếu tiền mặt hoặc tiền gửi ngân hàng đầu kỳ
- **THEN** hệ thống SHALL kiểm tra số dư chi tiết khớp lần lượt với TK 111 và TK 112

#### Scenario: Đối chiếu TSCĐ, CCDC và chi phí trả trước
- **WHEN** người dùng yêu cầu đối chiếu các khoản đầu kỳ mở rộng
- **THEN** hệ thống SHALL kiểm tra dữ liệu TSCĐ khớp TK 211/214, CCDC khớp tài khoản liên quan và chi phí trả trước khớp TK 242

### Requirement: Module số dư đầu kỳ SHALL hỗ trợ khóa và mở khóa có kiểm soát
Hệ thống SHALL chỉ cho phép khóa khi toàn bộ dữ liệu đã cân đối hợp lệ; mở khóa SHALL là thao tác quyền cao, bắt buộc nhập lý do và ghi audit log.

#### Scenario: Khóa số dư đầu kỳ thành công
- **WHEN** người dùng có quyền khóa và tất cả đối chiếu đều hợp lệ
- **THEN** hệ thống SHALL chuyển trạng thái số dư đầu kỳ sang Đã khóa, ghi nhận người khóa và thời điểm khóa

#### Scenario: Chặn khóa khi dữ liệu chưa cân đối
- **WHEN** tổng Nợ/Có hoặc bất kỳ đối chiếu chi tiết nào còn lệch
- **THEN** hệ thống SHALL không cho khóa số dư đầu kỳ

#### Scenario: Mở khóa số dư đầu kỳ
- **WHEN** người dùng có quyền `unlock_opening` yêu cầu mở khóa và nhập lý do mở khóa
- **THEN** hệ thống SHALL mở khóa dữ liệu đầu kỳ, ghi nhận người mở khóa, thời điểm mở khóa và lý do mở khóa

### Requirement: Module số dư đầu kỳ SHALL ghi nhận đầy đủ lịch sử thay đổi và lịch sử thao tác
Mọi thao tác nhập, sửa, xóa, import, khóa và mở khóa dữ liệu đầu kỳ SHALL được ghi nhận trong audit log và người dùng SHALL có thể tra cứu lịch sử liên quan.

#### Scenario: Ghi audit khi thay đổi dữ liệu đầu kỳ
- **WHEN** người dùng tạo mới, sửa hoặc xóa dữ liệu đầu kỳ
- **THEN** hệ thống SHALL ghi audit log với dữ liệu trước/sau thay đổi

#### Scenario: Xem lịch sử import và khóa/mở khóa
- **WHEN** người dùng có quyền tra cứu lịch sử truy cập màn hình lịch sử của module số dư đầu kỳ
- **THEN** hệ thống SHALL hiển thị lịch sử import, lịch sử khóa, lịch sử mở khóa và người thực hiện từng thao tác

### Requirement: Module số dư đầu kỳ SHALL hỗ trợ báo cáo và xuất dữ liệu phục vụ kiểm tra
Hệ thống SHALL cho phép in báo cáo số dư đầu kỳ, xuất Excel dữ liệu đầu kỳ và xuất kết quả đối chiếu để phục vụ kiểm tra/lưu trữ.

#### Scenario: In báo cáo số dư đầu kỳ
- **WHEN** người dùng chọn in báo cáo số dư đầu kỳ
- **THEN** hệ thống SHALL tạo báo cáo tổng hợp hoặc chi tiết theo loại dữ liệu đầu kỳ

#### Scenario: Xuất Excel số dư đầu kỳ
- **WHEN** người dùng chọn xuất Excel dữ liệu đầu kỳ hoặc kết quả đối chiếu
- **THEN** hệ thống SHALL xuất file chứa đúng dữ liệu tại thời điểm thực hiện xuất

### Requirement: Dữ liệu AR/AP, tồn kho, TSCĐ, CCDC và chi phí trả trước trong Phase 1 SHALL chỉ được đặc tả ở mức skeleton đầu kỳ
Change này SHALL chỉ làm rõ nhập liệu và đối chiếu đầu kỳ cho các nhóm dữ liệu skeleton; các hành vi vận hành đầy đủ thuộc các phase sau SHALL không được kéo vào phạm vi Phase 1.

#### Scenario: Giới hạn công nợ đầu kỳ ở Phase 1
- **WHEN** đặc tả công nợ khách hàng hoặc nhà cung cấp đầu kỳ được cập nhật
- **THEN** tài liệu SHALL chỉ bao gồm nhập đầu kỳ, hạn thanh toán, đối chiếu với sổ cái và khóa/mở khóa, không bao gồm tuổi nợ đầy đủ hoặc quản lý vòng đời công nợ hoàn chỉnh

#### Scenario: Giới hạn tài sản/CCDC/CPTT ở Phase 1
- **WHEN** đặc tả TSCĐ, CCDC hoặc chi phí trả trước đầu kỳ được cập nhật
- **THEN** tài liệu SHALL không thêm khấu hao, phân bổ định kỳ, điều chuyển, thanh lý hoặc kiểm kê đầy đủ của Phase 6 vào capability này
