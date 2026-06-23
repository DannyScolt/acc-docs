## Context

Dự án hiện có hai biểu diễn Phase 1 song song:
- `ACC-dac-ta-nghiep-vu-phase-1.html`: bản Phase 1 đã được chuẩn hóa, có trang bìa, flow, ma trận phạm vi, luồng trạng thái chứng từ, đặc tả chi tiết và phụ lục.
- `ACC-noi-dung-nghiep-vu-theo-phase.html`: file tổng dùng cơ chế tab, trong đó tab Phase 1 vẫn còn mang nội dung cũ, dài và không đồng bộ với file chuẩn.

File tổng được thiết kế như nguồn đọc chính trên trình duyệt với tab navigation và quy ước “toàn bộ nội dung nằm trong một file HTML duy nhất”. Vì vậy, mục tiêu không phải tạo thêm file mà là đưa nội dung Phase 1 đã chuẩn vào đúng tab Phase 1 của file tổng.

## Goals / Non-Goals

**Goals:**
- Thay phần thân tab Phase 1 trong `ACC-noi-dung-nghiep-vu-theo-phase.html` bằng nội dung Phase 1 đã chuẩn hóa.
- Giữ nguyên tab navigation, ID `tab-phase-1`, anchor `#phase-1`, và cơ chế hiển thị theo tab hiện có.
- Chỉ mang phần nội dung Phase 1 cần hiển thị vào file tổng, tránh sao chép lại cấu trúc tài liệu độc lập không phù hợp.
- Tạo chuẩn trực tiếp trong file tổng để các phase sau bám theo cùng một phong cách.

**Non-Goals:**
- Không cập nhật Phase 2–6 trong thay đổi này.
- Không thay đổi CSS toàn cục ngoài mức cần thiết để Phase 1 mới hiển thị đúng trong file chính.
- Không thay đổi nội dung business của bản Phase 1 chuẩn; chỉ chuyển và thích nghi vào file tổng.
- Không bỏ hệ tab hoặc chuyển sang nhiều file độc lập.

## Decisions

### Decision 1: Giữ file tổng làm nguồn hiển thị chính, không tạo file Phase 1 mới

**Decision:** Chỉ cập nhật `ACC-noi-dung-nghiep-vu-theo-phase.html`; không tạo file HTML mới cho Phase 1.

**Why:** File tổng đã được thiết kế để đọc theo tab và mục lục của nó cũng khẳng định toàn bộ nội dung nằm trong một file duy nhất. Việc tiếp tục mở thêm file sẽ làm sai mục tiêu dùng file tổng như entry point.

**Alternative considered:** Dùng file riêng làm tài liệu chính và chỉ để file tổng như archive. Bị loại vì trái với cơ chế tab đang được dùng để đọc tài liệu trên trình duyệt.

### Decision 2: Thay toàn bộ nội dung section Phase 1 cũ thay vì merge từng mảnh

**Decision:** Xem section Phase 1 trong file chính như một khối cần thay thế gần như toàn bộ, thay vì vá từng bảng hoặc heading.

**Why:** Phase 1 cũ và mới khác nhau ở cấu trúc, nhịp trình bày và cách gom nội dung. Merge từng đoạn sẽ dễ sinh lệch numbering, lặp nội dung và lỗi tag HTML.

**Alternative considered:** Chỉnh incremental từng mục trong tab Phase 1 cũ. Bị loại vì tốn công, dễ sót và vẫn để lại nhiều mảnh cấu trúc cũ không mong muốn.

### Decision 3: Chỉ chuyển phần body content phù hợp, không copy nguyên file độc lập

**Decision:** Trích phần nội dung Phase 1 cần thiết từ file chuẩn và thích nghi nó vào wrapper `tab-panel` / `section` của file chính; không sao chép `doctype`, `html`, `head`, `style`, `body` hoặc cover-only structures không phù hợp với tab layout.

**Why:** File chuẩn là tài liệu độc lập hoàn chỉnh, còn file chính đã có HTML shell và CSS riêng. Copy nguyên file sẽ làm lồng tài liệu, gây trùng style, hỏng DOM và phá tab behavior.

**Alternative considered:** Nhúng nguyên block `.doc` của file chuẩn vào tab Phase 1. Bị loại vì tạo nested wrapper nặng, trùng semantics và tăng nguy cơ hiển thị sai trong web view.

### Decision 4: Giữ định danh tab và anchor của Phase 1 để không phá điều hướng

**Decision:** Giữ nguyên `div.tab-panel#tab-phase-1`, `section#phase-1`, và tab button tương ứng; thay đổi chỉ nằm ở nội dung bên trong.

**Why:** Các phần JS/CSS tab switching và mục lục đang trỏ vào những định danh này. Giữ nguyên giúp thay nội dung mà không tạo side effect ngoài dự kiến.

**Alternative considered:** Đổi tên lại toàn bộ ID/anchor theo cấu trúc file chuẩn. Bị loại vì không cần thiết và dễ làm hỏng các liên kết hiện tại.

### Decision 5: Xem tab Phase 1 mới trong file tổng là chuẩn hình thức cho các phase tiếp theo

**Decision:** Sau khi thay xong, tab Phase 1 trong file tổng sẽ là reference presentation trực tiếp để các phase sau noi theo.

**Why:** Điều này loại bỏ việc phải đối chiếu qua lại giữa file riêng và file tổng khi tiếp tục chuẩn hóa Phase 2–6.

**Alternative considered:** Tiếp tục dùng file riêng làm reference presentation lâu dài. Bị loại vì làm luồng chỉnh sửa file tổng kém trực quan hơn.

## Risks / Trade-offs

- **[Ranh giới section/tab trong file chính dễ lệch tag khi thay khối lớn]** → Mitigation: Xác định rõ điểm bắt đầu/kết thúc của `tab-phase-1` trước khi áp dụng; chỉ thay phần section body trong wrapper tương ứng.
- **[File Phase 1 chuẩn có cấu trúc độc lập khác file tổng]** → Mitigation: Adapt nội dung, không copy nguyên shell tài liệu; giữ wrapper tab hiện hữu.
- **[CSS của file tổng và file riêng có thể không hoàn toàn trùng]** → Mitigation: Ưu tiên tái sử dụng class đã có trong file chính; chỉ bổ sung hoặc điều chỉnh tối thiểu nếu phát sinh khác biệt hiển thị.
- **[Có thể vô tình làm hỏng tab switching hoặc in PDF]** → Mitigation: Giữ nguyên ID/tab structure và kiểm tra lại Phase 1 trong bối cảnh tabbed document sau khi thay.
- **[Bản Phase 1 trong file chính và file riêng có thể tiếp tục divergence về sau]** → Mitigation: Sau thay đổi này, xem file chính là nguồn hiển thị primary; file riêng chỉ còn vai trò reference hoặc archive nếu chưa được dọn dẹp.
