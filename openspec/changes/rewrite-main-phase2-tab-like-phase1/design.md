## Context

File tổng `ACC-noi-dung-nghiep-vu-theo-phase.html` là nguồn đọc chính theo mô hình tab, trong đó tab Phase 1 vừa được thay thành bản approved. Điều này tạo ra một chuẩn trình bày sống ngay trong file chính: có sơ đồ đặc tả nghiệp vụ, ma trận module, luồng trạng thái chứng từ dùng chung, phần đặc tả module theo bảng phù hợp và phụ lục định khoản/rule/nghiệm thu.

Tab Phase 2 hiện vẫn mang cấu trúc cũ: bắt đầu bằng intro card và lộ trình nhưng sau đó đi ngay vào mini-flow, danh sách chức năng, bộ trạng thái riêng lẻ, use case chi tiết dài và nhiều đoạn raw. Vì vậy khi đặt cạnh tab Phase 1 mới, Phase 2 bị lệch hệ cả về nhịp đọc lẫn mức độ biên tập.

## Goals / Non-Goals

**Goals:**
- Viết lại trực tiếp tab Phase 2 trong file tổng theo cùng pattern approved đang dùng cho tab Phase 1.
- Giữ nguyên wrapper `tab-phase-2`, anchor `#phase-2`, tab button và cơ chế tab switching hiện có.
- Tạo đủ ba tầng nội dung cho Phase 2: tổng quan nghiệp vụ, kiểm soát trạng thái, đặc tả chi tiết theo module.
- Gom và nén lại nội dung raw hiện tại để người đọc kế toán/BA có thể duyệt theo nhịp giống Phase 1.
- Bảo toàn nội dung nghiệp vụ cốt lõi của Phase 2: mua hàng, nhập kho, hóa đơn đầu vào, AP, thanh toán NCC, trả lại/giảm giá, bù trừ, kho và báo cáo.

**Non-Goals:**
- Không tạo file `ACC-dac-ta-nghiep-vu-phase-2.html` trong change này.
- Không chỉnh tab Phase 3–6 hoặc Overview/Appendix.
- Không thay đổi nghiệp vụ của Phase 1; chỉ dùng nó làm chuẩn trình bày.
- Không thiết kế phần mềm hay data model kỹ thuật; đây là thay đổi tài liệu nghiệp vụ trong HTML chính.

## Decisions

### Decision 1: Sửa trực tiếp tab Phase 2 trong file chính, không tiếp tục hướng file riêng

**Decision:** Scope của change là rewrite tab Phase 2 bên trong `ACC-noi-dung-nghiep-vu-theo-phase.html`.

**Why:** Định hướng mới của tài liệu là một file HTML duy nhất theo tab. Sau khi tab Phase 1 đã được approved ngay trong file chính, việc tạo thêm file Phase 2 riêng sẽ làm lệch kiến trúc và tiếp tục sinh hai nguồn hiển thị khác nhau.

**Alternative considered:** Tiếp tục change cũ tạo `ACC-dac-ta-nghiep-vu-phase-2.html`. Bị loại vì không còn khớp với hướng single-file tabbed document mà user đã chốt.

### Decision 2: Phase 2 phải có cùng ba lớp như Phase 1 mới

**Decision:** Tổ chức Phase 2 theo ba lớp:
1. Sơ đồ đặc tả nghiệp vụ + ma trận phạm vi module
2. Luồng trạng thái chứng từ dùng chung + chú thích trạng thái
3. Đặc tả chức năng chi tiết theo module + phụ lục

**Why:** Đây là điểm khác biệt lớn nhất giữa tab Phase 1 mới và tab Phase 2 cũ. Khi áp dụng cùng cấu trúc, người đọc sẽ cảm nhận hai phase thuộc cùng một bộ approved.

**Alternative considered:** Chỉ giữ intro card/lộ trình rồi chỉnh từng module. Bị loại vì không xử lý được sự thiếu vắng lớp tổng quan và lớp kiểm soát chung.

### Decision 3: Dùng Phase 1 trong file chính làm template trực tiếp, không tham chiếu qua nhiều lớp

**Decision:** Xem tab Phase 1 mới trong `ACC-noi-dung-nghiep-vu-theo-phase.html` là template trực tiếp về nhịp nội dung, loại section và loại bảng cho Phase 2.

**Why:** Sau khi Phase 1 đã sống trong file chính, đây là chuẩn gần nhất với bối cảnh thật của tài liệu. Dùng nó làm template giúp Phase 2 sau sửa đồng bộ ngay trong cùng một DOM/CSS environment.

**Alternative considered:** Chỉ dùng `ACC-dac-ta-nghiep-vu-phase-1.html` làm template. Bị loại vì dễ lệch với cách nhúng thật trong file tổng.

### Decision 4: Gom module Phase 2 về cấu trúc approved thay vì giữ nguyên các mảnh raw

**Decision:** Không giữ nguyên cấu trúc raw hiện tại của Phase 2. Nội dung được biên tập lại theo các cụm module approved, ví dụ:
- Yêu cầu mua & Đơn mua
- Hợp đồng mua
- Mua hàng hóa / dịch vụ
- Nhận hàng & nhập kho mua hàng
- Hóa đơn mua vào
- Công nợ phải trả nhà cung cấp
- Thanh toán nhà cung cấp
- Trả lại hàng mua & giảm giá hàng mua
- Bù trừ & đối chiếu công nợ
- Quản lý kho
- Báo cáo mua hàng, công nợ phải trả & kho

**Why:** Source hiện tại bị phân mảnh thành danh sách chức năng, trạng thái riêng, use case chi tiết và rule dài. Nếu giữ nguyên, tài liệu sẽ vẫn giống notes BA nội bộ hơn là bản approved gửi duyệt.

**Alternative considered:** Chỉ đổi style nhưng giữ nguyên trình tự section hiện có. Bị loại vì không giải quyết được sự rời rạc và lặp.

### Decision 5: Giữ baseline trạng thái chứng từ của Phase 1, còn trạng thái nghiệp vụ đặc thù để ở từng module

**Decision:** Luồng trạng thái dùng chung của Phase 2 tiếp tục dùng baseline kiểu Phase 1 (`Nháp → Chờ duyệt → Đã duyệt → Đã ghi sổ → Đã khóa kỳ`, cùng `Từ chối` và `Đã hủy`). Các trạng thái đặc thù như “Nhận một phần”, “Nhận đủ”, “Thanh toán một phần”, “Hoàn thành” sẽ được mô tả ở module tương ứng.

**Why:** Điều này giữ tính nhất quán xuyên phase và tránh biến phần trạng thái chung thành sơ đồ quá nặng, quá nhiều nhánh riêng cho từng loại chứng từ.

**Alternative considered:** Thiết kế state machine riêng đầy đủ cho từng chứng từ ngay trong phần chung. Bị loại vì khó đọc và lệch tinh thần Phase 1.

### Decision 6: Phân loại bảng giống Phase 1

**Decision:**
- CRUD / quản lý cấu hình / danh sách tổng hợp: dùng `stt-table`
- Nghiệp vụ chứng từ / vận hành / báo cáo: dùng `uc-table` 8 cột
- Rule, tiêu chí, định khoản: tiếp tục dùng `rule-table`, `rule3-table`, `entry-table`

**Why:** Đây là quy luật trình bày đã tạo cảm giác approved cho Phase 1 mới.

**Alternative considered:** Tiếp tục pha trộn `stt-table`, `rule-table` và prose dài cho cùng một khối nội dung. Bị loại vì tạo cảm giác thiếu nhất quán.

## Risks / Trade-offs

- **[Phase 2 hiện có rất nhiều chi tiết raw]** → Mitigation: ưu tiên biên tập lại theo đích approved, không cố giữ nguyên mọi đoạn văn hoặc mọi bảng hiện có.
- **[Có proposal cũ đi theo hướng file riêng]** → Mitigation: tách change mới với scope rõ ràng cho tab Phase 2 trong file chính, tránh tiếp tục nhầm lẫn.
- **[Các trạng thái nghiệp vụ phụ của PO/Nhập kho/Hóa đơn có thể chồng với trạng thái chứng từ chung]** → Mitigation: giữ baseline chung ở phần trạng thái dùng chung, dời trạng thái phụ về từng module cụ thể.
- **[Rủi ro Phase 2 sau sửa vẫn dài]** → Mitigation: gom module, bỏ lặp summary/detail và ưu tiên mỗi chủ đề một bảng chuẩn chính.
- **[Nguy cơ làm lệch numbering hoặc ảnh hưởng tab Phase 3 trở đi]** → Mitigation: chỉ thay đúng phạm vi `tab-phase-2` và kiểm tra ranh giới trước/sau khi apply.
