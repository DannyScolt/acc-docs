## Context

Phase 1 đã có file riêng `ACC-dac-ta-nghiep-vu-phase-1.html` với format “bản đã duyệt”: trang bìa, letterhead, sơ đồ phạm vi, luồng trạng thái chứng từ, ma trận module, phần đặc tả chi tiết và phụ lục. Trong khi đó, nội dung Phase 2 hiện vẫn nằm trong `ACC-noi-dung-nghiep-vu-theo-phase.html` dưới dạng một section lớn, đủ ý nghiệp vụ nhưng còn lặp, nhiều bảng summary và chưa được đóng gói thành tài liệu độc lập để kế toán đọc như Phase 1.

Phase 2 bao phủ chu trình mua hàng, nhập kho, hóa đơn đầu vào, công nợ phải trả, thanh toán nhà cung cấp, trả lại/giảm giá, đối chiếu công nợ và quản lý kho. Đây là giai đoạn có nhiều giao điểm với các logic Phase 1 như quỹ, ngân hàng và sổ cái, nên việc chuẩn hóa phải vừa giữ phong cách trình bày giống Phase 1 vừa bảo toàn quan hệ nghiệp vụ chéo.

## Goals / Non-Goals

**Goals:**
- Tạo file tài liệu Phase 2 riêng theo đúng phong cách trình bày và chuẩn section của Phase 1.
- Chuyển Phase 2 từ nội dung nguồn phân mảnh sang tài liệu review-ready: sơ đồ HTML, ma trận phạm vi, luồng trạng thái baseline, đặc tả module theo bảng phù hợp và phụ lục tổng hợp.
- Giảm lặp trong các mục Phase 2 bằng cách chuẩn hóa: nghiệp vụ CRUD dùng bảng STT; nghiệp vụ chứng từ và vận hành dùng bảng Use Case 8 cột.
- Giữ nhất quán với Phase 1 về cách đánh số, letterhead, quy tắc trạng thái chứng từ, ảnh hưởng quỹ/ngân hàng/sổ cái và ngôn ngữ tài liệu cho bộ phận kế toán.

**Non-Goals:**
- Không thay đổi nội dung của `ACC-dac-ta-nghiep-vu-phase-1.html`.
- Không triển khai phần mềm, API hay data model kỹ thuật; chỉ chuẩn hóa tài liệu nghiệp vụ và artifact OpenSpec.
- Không viết lại Phase 3–6 trong change này.
- Không thay đổi nội dung gốc trong file tổng nhiều hơn mức cần thiết để tham chiếu nguồn; đầu ra chính là file Phase 2 riêng.

## Decisions

### Decision 1: Tạo file Phase 2 mới bằng cách kế thừa khung trình bày của Phase 1

**Decision:** Sử dụng `ACC-dac-ta-nghiep-vu-phase-1.html` làm template cấu trúc và style cho file mới `ACC-dac-ta-nghiep-vu-phase-2.html`.

**Why:** Phase 1 đã được duyệt và đã giải quyết các yêu cầu trình bày: self-contained, A4, letterhead, bảng và sơ đồ in đẹp. Kế thừa khung này giúp Phase 2 đồng bộ trực quan và giảm rủi ro lệch format.

**Alternative considered:** Dùng lại section trong file tổng `ACC-noi-dung-nghiep-vu-theo-phase.html` rồi sửa trực tiếp. Bị loại vì Phase 2 vẫn sẽ phụ thuộc file tổng và khó đạt cảm giác “bản đã duyệt” riêng như Phase 1.

### Decision 2: Dùng ba tầng cấu trúc giống Phase 1 cho tài liệu Phase 2

**Decision:** Tổ chức file Phase 2 thành ba mục lớn: (1) sơ đồ đặc tả nghiệp vụ + ma trận phạm vi, (2) luồng trạng thái chứng từ + bảng chú thích, (3) đặc tả chức năng chi tiết theo module, sau đó là phụ lục.

**Why:** Đây là mô hình người đọc đã quen ở Phase 1 và đủ để đọc từ tổng quan → kiểm soát trạng thái → chi tiết module.

**Alternative considered:** Giữ nguyên numbering hiện tại của Phase 2 trong file tổng. Bị loại vì không tạo được lớp tổng quan và kiểm soát chung trước khi đi vào chi tiết.

### Decision 3: Giữ baseline luồng trạng thái chứng từ của Phase 1, chỉ mở rộng phạm vi áp dụng

**Decision:** Sử dụng lại logic trạng thái `Nháp → Chờ duyệt → Đã duyệt → Đã ghi sổ → Đã khóa kỳ` cùng hai nhánh `Từ chối` và `Đã hủy` cho sơ đồ trạng thái Phase 2, nhưng cập nhật diễn giải để áp dụng cho chứng từ mua hàng, nhập kho, hóa đơn đầu vào, thanh toán và trả hàng/điều chỉnh.

**Why:** Quy tắc kiểm soát duyệt/ghi sổ là điểm chung toàn hệ thống, không nên tạo một state machine hoàn toàn khác nếu chưa có lý do nghiệp vụ bắt buộc.

**Alternative considered:** Tạo state machine riêng biệt cho từng module. Bị loại vì làm tài liệu nặng, trùng lặp và khó đồng bộ với Phase 1.

### Decision 4: Chuẩn hóa bảng theo loại nội dung, không bê nguyên mọi bảng nguồn

**Decision:** Biên tập lại nội dung nguồn Phase 2 theo hai form chính:
- Bảng STT cho phần quản lý/chức năng tổng hợp hoặc cấu hình.
- Bảng Use Case 8 cột cho phần nghiệp vụ chứng từ, vận hành và báo cáo cần actor, luồng chính, rule, kết quả đầu ra.

**Why:** Source hiện tại có nhiều đoạn “Danh sách chức năng” rồi lại nối tiếp bằng “Use Case chi tiết”, gây lặp và làm tài liệu dài. Chuẩn hóa theo logic Phase 1 giúp tài liệu gọn hơn nhưng vẫn đủ thông tin.

**Alternative considered:** Giữ nguyên mọi bảng hiện có rồi chỉ đổi style. Bị loại vì không xử lý được vấn đề lặp và chưa đạt chuẩn đọc nhanh của tài liệu duyệt.

### Decision 5: Tách capability theo loại tài liệu và nhóm nghiệp vụ

**Decision:** Chia thay đổi thành bốn capability: file tài liệu Phase 2 đã duyệt, procurement/AP, inventory và reporting/controls.

**Why:** Việc chuẩn hóa Phase 2 không chỉ là tạo file mới mà còn là biên tập sâu nhiều cụm nghiệp vụ khác nhau. Chia capability giúp specs và tasks bám sát phần việc thật sự.

**Alternative considered:** Dùng một capability chung cho toàn bộ Phase 2. Bị loại vì quá rộng, khó review và khó theo dõi phạm vi khi apply.

## Risks / Trade-offs

- **[Nguồn Phase 2 có lặp và độ chi tiết không đồng đều]** → Mitigation: Xem `ACC-noi-dung-nghiep-vu-theo-phase.html` là data source, không ràng buộc phải giữ nguyên từng bảng; ưu tiên chuẩn hóa theo format đích.
- **[Có điểm giao cắt với quỹ/ngân hàng/sổ cái Phase 1]** → Mitigation: Khi biên tập phần thanh toán, đối chiếu và ghi sổ, dùng ngôn ngữ tham chiếu chéo thống nhất với Phase 1 thay vì phát minh quy tắc mới.
- **[Tài liệu Phase 2 có thể quá dài nếu bê toàn bộ chi tiết thô]** → Mitigation: Gom nhóm use case, bỏ lặp, giữ mỗi chủ đề một bảng chuẩn thay vì “summary + detailed duplicate”.
- **[Rủi ro lệch numbering hoặc format với Phase 1]** → Mitigation: Sao chép khung section, CSS và cách đánh số từ file Phase 1 trước, sau đó mới thay nội dung.
- **[Một số rule kế toán vẫn cần người dùng xác nhận]** → Mitigation: Giữ chú thích rõ ở định khoản hoặc note cuối mục thay vì tự chốt thay người dùng.
