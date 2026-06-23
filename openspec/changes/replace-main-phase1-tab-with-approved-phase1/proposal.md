## Why

Tab Phase 1 trong file chính `ACC-noi-dung-nghiep-vu-theo-phase.html` hiện vẫn là bản nội dung cũ, chưa đồng bộ với bản Phase 1 đã được viết lại và duyệt trong `ACC-dac-ta-nghiep-vu-phase-1.html`. Điều này tạo ra hai nguồn nội dung Phase 1 khác nhau: một bản riêng đã chuẩn hóa và một bản trong tab Phase 1 của file chính vẫn còn dài, thô và không cùng nhịp trình bày.

Cần thay nội dung tab Phase 1 trong file chính bằng phiên bản Phase 1 đã chuẩn hóa để file tổng quay lại vai trò là tài liệu đọc chính theo tab, đồng thời tạo chuẩn hình thức trực tiếp trong file tổng trước khi tiếp tục chỉnh các phase khác.

## What Changes

- Cập nhật trực tiếp `ACC-noi-dung-nghiep-vu-theo-phase.html` để thay toàn bộ nội dung tab Phase 1 hiện tại bằng nội dung Phase 1 đã chuẩn hóa từ `ACC-dac-ta-nghiep-vu-phase-1.html`.
- Giữ nguyên kiến trúc tài liệu một file HTML duy nhất, gồm navigation tab, overview, Phase 1–6 và appendix; không tạo file Phase 1 mới và không thay đổi cấu trúc tab chung.
- Giữ nguyên hành vi của tab Phase 1 trong file chính (`tab-panel`, anchor `#phase-1`, tab button) nhưng thay phần thân section để nội dung hiển thị theo đúng format đã duyệt: mở chương rõ ràng, sơ đồ, ma trận, luồng trạng thái, đặc tả module, phụ lục.
- Thích nghi nội dung Phase 1 chuẩn từ file riêng vào file chính theo cách an toàn: chỉ mang phần nội dung section cần thiết, không sao chép lại `doctype`, `html`, `head`, `body` hay CSS toàn cục đã có sẵn trong file chính.
- Tạo nền tảng để về sau chỉnh tiếp các tab khác (đặc biệt là Phase 2) theo ngay chuẩn đã sống bên trong file chính, thay vì phải đối chiếu qua lại giữa file tổng và file riêng.

## Capabilities

### New Capabilities
- `main-phase1-approved-tab`: Tab Phase 1 trong file chính hiển thị nội dung Phase 1 đã chuẩn hóa, đồng bộ với bản duyệt riêng và phù hợp với mô hình tài liệu theo tab.
- `single-file-phase-consistency`: File tổng duy trì một nguồn hiển thị chính cho Phase 1 trong cùng cấu trúc tabbed document, tránh lệch giữa file riêng và file chính.

### Modified Capabilities
- `tabbed-phase-document`: Điều chỉnh capability tài liệu theo tab để Phase 1 trong file chính không còn dùng bản cũ mà dùng nội dung đã chuẩn hóa.

## Impact

- **File chính bị chỉnh sửa**: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- **File tham chiếu nguồn**: `ACC-dac-ta-nghiep-vu-phase-1.html`
- **Không tạo đầu ra HTML mới**: thay đổi này cập nhật file tổng hiện có, không mở thêm file tài liệu mới.
- **Ảnh hưởng UI tài liệu**: tab Phase 1 sẽ thay đổi đáng kể về nội dung và bố cục hiển thị, nhưng các tab khác và navigation phải tiếp tục hoạt động như cũ.
- **Ảnh hưởng triển khai tiếp theo**: sau thay đổi này, file tổng sẽ có một chuẩn Phase 1 trực tiếp để dùng làm mẫu cho việc chỉnh các tab Phase 2–6.
