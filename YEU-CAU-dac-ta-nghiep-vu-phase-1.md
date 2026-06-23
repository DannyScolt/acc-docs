# Yêu cầu — Đặc tả nghiệp vụ Phase 1 (ACC)

File tài liệu: `ACC-dac-ta-nghiep-vu-phase-1.html`
Mục tiêu: tài liệu đặc tả nghiệp vụ Phase 1 cho **bộ phận kế toán** đọc hiểu được *gồm có gì, chức năng gì, phạm vi như nào* — theo đúng **bản đã duyệt** của boss (Mạnh Tâm) và cấu trúc danh mục của Tâm (Nguyễn Phú Quý).

---

## 1. Bối cảnh

- Bản HTML ban đầu (`ACC-noi-dung-nghiep-vu-theo-phase.html`) sinh từ nội dung **link GitHub** → nghiệp vụ chưa đúng, trình bày chưa theo format duyệt.
- Tạo **file mới** `ACC-dac-ta-nghiep-vu-phase-1.html`, chỉ phạm vi **Phase 1**, theo đúng kiểu bản đã duyệt.

---

## 2. Yêu cầu về 3 mô hình đầu tài liệu (bản đã duyệt)

Tài liệu phải có đủ **3 mô hình** + bảng chú thích:

1. **Sơ đồ đặc tả nghiệp vụ chi tiết Phase 1** (Hình 1)
   - Luồng: Bắt đầu → 2.1 Quản trị → 2.2 Danh mục → rẽ nhánh 2.3 Quỹ / 2.4 Ngân hàng → 2.5 Sổ cái → Tuần 9 kiểm thử → Tuần 10 nghiệm thu.
   - Dựng bằng box HTML + mũi tên (in PDF được, không cần internet).
2. **Ma trận phạm vi theo module** (mục 1.1)
   - 5 cột: Mã · Module · Nội dung trọng tâm · Kết quả đầu ra · Mốc.
   - Mã module giữ **2.1–2.5** (đã duyệt — không đổi).
3. **Sơ đồ luồng trạng thái chứng từ dùng chung** (Hình 2)
   - Nháp → Chờ duyệt → Đã duyệt → Đã ghi sổ → Đã khóa kỳ; nhánh Từ chối, Đã hủy.
   - Dựng bằng SVG nhúng sẵn.
   - **Nháp và Chờ duyệt đều có thể Hủy** (khớp bảng chú thích).
4. **Bảng chú thích trạng thái** (mục 2.1) — boss dặn "thêm chú thích cho luồng trạng thái là xong"
   - 4 cột: Trạng thái · Ý nghĩa · Chuyển tiếp cho phép · Kiểm soát chính (7 trạng thái).

**Định dạng trình bày (khớp bản duyệt):**
- Tiêu đề ô trong Hình 1 viết **IN HOA**, không dùng dấu "·".
- Nhãn mũi tên rẽ nhánh ghi riêng từng nhánh (`dữ liệu nền hợp lệ` ×2; `chứng từ quỹ đã ghi sổ` / `chứng từ NH đã ghi sổ`).
- Letterhead mỗi trang: `ACC | ĐẶC TẢ NGHIỆP VỤ PHASE 1` — `BẢN ĐÃ DUYỆT`.

---

## 3. Yêu cầu về thứ tự danh mục (mục 3.2)

Danh mục phải sắp theo **chuỗi phụ thuộc** (để cuối cùng lập được phiếu thu/chi) — đây là thứ tự **chuẩn của Tâm**, đầy đủ **26 mục** (bỏ "Nhân viên" vì không có trong list):

| # | Danh mục | # | Danh mục |
|---|----------|---|----------|
| 1 | Loại tiền | 14 | Hàng hóa |
| 2 | Cơ cấu tổ chức | 15 | Ngân hàng |
| 3 | Chi nhánh – Phòng ban | 16 | Tài khoản ngân hàng |
| 4 | Hệ thống tài khoản | 17 | Điều khoản thanh toán |
| 5 | Tài khoản kết chuyển | 18 | Khoản mục chi phí |
| 6 | Tài khoản ngầm định | 19 | Đối tượng tập hợp chi phí |
| 7 | Nhóm khách hàng | 20 | Loại công trình |
| 8 | Khách hàng | 21 | Công trình |
| 9 | Nhóm nhà cung cấp | 22 | Loại công cụ dụng cụ |
| 10 | Nhà cung cấp | 23 | Loại tài sản cố định |
| 11 | Đơn vị tính | 24 | Mục thu chi |
| 12 | Nhóm vật tư hàng hóa | 25 | Mã thống kê |
| 13 | Kho | 26 | Loại chứng từ |

- Sau danh mục là **3.2.27 Số dư đầu kỳ** (nhập/import → đối chiếu → khóa).
- Nguyên tắc: Kho khai trước Hàng hóa; Loại chứng từ + đối tượng + khoản mục chi phí phải có trước khi lập phiếu thu/chi.
- 17 mục mới: tự soạn nội dung chức năng (STT / Chức năng / Mô tả) theo chuẩn kế toán — Tâm rà lại sau.

---

## 4. Yêu cầu đánh số & sắp xếp hợp lý

- **Mục 1**: Sơ đồ đặc tả (1.1 Ma trận).
- **Mục 2**: Sơ đồ luồng trạng thái (2.1 Chú thích trạng thái).
- **Mục 3**: Đặc tả chức năng chi tiết theo module — đánh số **3.1 → 3.5**, kèm chú **(Mã 2.x)** để liên kết với ma trận/sơ đồ (giữ mã 2.1–2.5 đã duyệt).
  - 3.1 Quản trị hệ thống & người dùng (Mã 2.1)
  - 3.2 Danh mục & dữ liệu đầu kỳ (Mã 2.2)
  - 3.3 Tiền mặt / Quỹ (Mã 2.3)
  - 3.4 Tiền gửi ngân hàng (Mã 2.4)
  - 3.5 Sổ cái & hệ thống tài khoản (Mã 2.5)
- Không để đụng số (đã bỏ "2.1" trùng); xóa bảng/định khoản bị lặp.

---

## 5. Yêu cầu định dạng bảng Use Case 8 cột

Tâm yêu cầu đưa **tất cả nghiệp vụ chứng từ** về **bảng Use Case 8 cột** cho gọn:

> Use Case ID · Chức năng · Actor · Luồng nghiệp vụ · Luồng chính · Business Rule · Liên kết với phân hệ khác · Kết quả đầu ra

- "Luồng chính" trình bày các bước đánh số (1, 2, 3…).
- "Kết quả đầu ra" nêu rõ trạng thái + bút toán Nợ/Có + tác động sổ.
- **Phạm vi áp dụng:** các mục nghiệp vụ chứng từ, **không** áp dụng cho danh mục CRUD (3.1.x, 3.2.1–3.2.26 giữ bảng STT).

**Các mục đã chuyển sang 8 cột (16 bảng):**
- Quỹ: 3.3.1 Phiếu thu · 3.3.2 Phiếu chi · 3.3.3 Sổ quỹ · 3.3.4 Kiểm kê quỹ · 3.3.5 Báo cáo quỹ
- Ngân hàng: 3.4.1 Thu · 3.4.2 Chi · 3.4.3 Chuyển nội bộ · 3.4.4 Sao kê · 3.4.5 Đối chiếu · 3.4.6 Báo cáo
- Sổ cái: 3.5.1 Ghi sổ · 3.5.2 Sổ cái · 3.5.3 Nhật ký chung · 3.5.4 Cân đối phát sinh
- Đầu kỳ: 3.2.27 Số dư đầu kỳ

---

## 6. Quy ước kỹ thuật

- 1 file HTML duy nhất, self-contained (SVG + CSS nhúng), in PDF khổ A4, mỗi mục lớn sang trang riêng.
- Sơ đồ vẽ bằng SVG/HTML thuần (không phụ thuộc internet/JS).
- Mọi chỉnh sửa giữ tag cân bằng (kiểm tra table/div/section/span/ol).

---

## 7. Điểm còn chờ xác nhận

- **"Nhân viên"**: đã bỏ khỏi danh mục theo list Tâm, nhưng nghiệp vụ phiếu thu/chi vẫn tham chiếu "tạm ứng / hoàn ứng nhân viên". Cần Tâm chốt: nhân viên thuộc *Cơ cấu tổ chức* hay cần thêm danh mục riêng.
- Nội dung 17 danh mục mới và các bảng Use Case là bản tự soạn theo chuẩn kế toán → **chờ kế toán rà soát** số tài khoản, rule và bút toán cho khớp thực tế doanh nghiệp.

---

## 8. Chuẩn bị triển khai các Phase tiếp theo

Phase 1 là **khuôn mẫu chuẩn**. Các phase sau làm theo đúng bộ quy ước này để đồng bộ toàn dự án.

### 8.1. Khuôn mẫu mỗi tài liệu phase (lặp lại y như Phase 1)

Mỗi phase tạo 1 file riêng `ACC-dac-ta-nghiep-vu-phase-N.html` gồm:

1. Trang bìa + letterhead `ACC | ĐẶC TẢ NGHIỆP VỤ PHASE N — BẢN ĐÃ DUYỆT`.
2. **Mục 1** — Sơ đồ đặc tả nghiệp vụ chi tiết (Hình 1, box HTML + mũi tên).
   - 1.1 Ma trận phạm vi theo module (5 cột, có cột Mã + Mốc tuần).
3. **Mục 2** — Sơ đồ luồng trạng thái chứng từ (Hình 2, SVG) + 2.1 Bảng chú thích trạng thái.
   - Phase nào có luồng chứng từ riêng (vd duyệt đơn mua, duyệt đơn bán) thì vẽ luồng riêng; nếu dùng chung thì tham chiếu luồng baseline Phase 1.
4. **Mục 3** — Đặc tả chức năng chi tiết theo module (3.1, 3.2…), kèm chú **(Mã x.y)** liên kết ma trận.
5. Phụ lục: Business Rules toàn phân hệ · Bảng định khoản mẫu · Kết quả bàn giao · Tiêu chí nghiệm thu.

### 8.2. Quy ước bắt buộc kế thừa

- **Định dạng**: tiêu đề ô sơ đồ IN HOA không dấu "·"; nhãn mũi tên ghi riêng từng nhánh; letterhead mỗi trang.
- **Danh mục**: nếu phase phát sinh danh mục mới, chèn vào đúng **chuỗi phụ thuộc** (khai báo cái được tham chiếu trước). Danh mục dùng chung đã khai ở Phase 1 thì **không khai lại**, chỉ tham chiếu.
- **Nghiệp vụ chứng từ**: trình bày bằng **bảng Use Case 8 cột** (Use Case ID · Chức năng · Actor · Luồng nghiệp vụ · Luồng chính · Business Rule · Liên kết với phân hệ khác · Kết quả đầu ra). Danh mục CRUD giữ bảng STT.
- **Use Case ID**: đặt tiền tố theo phân hệ (vd `UC-PO-xx` mua hàng, `UC-SO-xx` bán hàng) để không trùng giữa các phase.
- **Kết quả đầu ra** luôn nêu bút toán Nợ/Có + tác động sổ.
- **Kỹ thuật**: 1 file HTML self-contained, SVG/HTML thuần, in A4, giữ tag cân bằng.
- **Liên kết phân hệ khác**: ghi rõ tham chiếu chéo sang phase trước (vd Phase 2 nhập kho → giá vốn dùng ở Phase 3).

### 8.3. Phạm vi dự kiến từng phase (để chốt ma trận đầu mỗi phase)

| Phase | Trọng tâm | Phân hệ chính | Phụ thuộc phase trước |
|-------|-----------|---------------|------------------------|
| **2** | Mua hàng, nhập kho & công nợ phải trả | Đơn mua, hợp đồng mua, nhận hàng/nhập kho, hóa đơn mua vào, công nợ NCC (331), thanh toán NCC, trả lại hàng mua, quản lý kho | Danh mục NCC, hàng hóa, kho, TK (Phase 1); luồng duyệt chứng từ |
| **3** | Bán hàng, xuất kho, giá vốn & công nợ phải thu | Báo giá, đơn bán, xuất kho, hóa đơn bán ra, giá vốn, công nợ KH (131), thu tiền | Danh mục KH, hàng hóa, kho; tồn kho & giá vốn từ Phase 2 |
| **4** | Tổng hợp, kết chuyển, khóa kỳ & BCTC | Bút toán tổng hợp, phân bổ, kết chuyển cuối kỳ, khóa kỳ, báo cáo tài chính | Sổ cái Phase 1; phát sinh mua/bán Phase 2–3; TK kết chuyển |
| **5** | Thuế & hóa đơn điện tử | Kết nối HĐĐT, hóa đơn đầu vào/đầu ra, kiểm tra rủi ro, kê khai & báo cáo thuế | Hóa đơn mua (Phase 2), hóa đơn bán (Phase 3) |
| **6** | Mở rộng nâng cao | TSCĐ, CCDC, tiền lương, giá thành, vay, hợp đồng, dashboard quản trị | Danh mục Loại TSCĐ/CCDC/Công trình (đã khai Phase 1); sổ cái, chi phí |

### 8.4. Việc cần làm trước khi viết mỗi phase

1. Chốt **phạm vi & ma trận module** với kế toán (mã, nội dung trọng tâm, kết quả đầu ra, mốc tuần).
2. Liệt kê **danh mục mới** của phase và chèn vào đúng chuỗi phụ thuộc; rà các danh mục dùng chung từ Phase 1.
3. Vẽ/sửa **sơ đồ luồng nghiệp vụ** (Hình 1) và **luồng trạng thái chứng từ** (Hình 2) cho phase.
4. Viết các nghiệp vụ theo **bảng Use Case 8 cột**, đặt tiền tố Use Case ID riêng.
5. Soạn **bảng định khoản mẫu** + **Business Rules toàn phân hệ** + **tiêu chí nghiệm thu**.
6. **Kế toán rà soát** số tài khoản, rule, bút toán trước khi chốt "BẢN ĐÃ DUYỆT".
