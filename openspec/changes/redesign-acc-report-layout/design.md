# Design: Redesign ACC Report Layout

This document outlines the implementation strategy for converting `ACC-noi-dung-nghiep-vu-theo-phase.html` into a formal PDF report format.

## Constraints & Context

The requirement is to keep the content in a single HTML file but format it so that when printed or viewed as a PDF, it reads like a multi-page formal business report.

## Structural Changes

### Document Sections

The document will be reorganized into clear, distinct sections that act as pages in the PDF:

1. **Cover Page**: Redesigned to look like a consulting/business report cover.
2. **Executive Summary Page**: A new section summarizing the 6 phases and the document's purpose.
3. **Table of Contents**: A quick link section to jump to different phases.
4. **Phase Chapters**: Each of the 6 phases will be wrapped in a container that forces a page break. The phase will start with an introductory summary block before displaying the detailed tables.

### CSS Changes

The CSS in the `<head>` will be updated to enforce the report layout:

- **`page-break-before: always;`**: Added to phase title sections or chapter wrappers so each phase always prints on a new page.
- **Cover Page Styles**: Adjusted layout for the cover to remove emojis and center professional text (Title, subtitle, metadata block).
- **Executive Summary & TOC Styles**: Styling for the new introductory pages.
- **Phase Intro Styles**: A distinct visual block (e.g., a card or bordered section) at the top of each phase summarizing its goals and modules.

## Component Design

### 1. The Cover Page

```html
<section class="cover page">
  <h1>ACC</h1>
  <h2>PHẠM VI NGHIỆP VỤ KẾ TOÁN<br/>THEO GIAI ĐOẠN TRIỂN KHAI</h2>
  <div class="subtitle">
    Tài liệu mô tả phạm vi chức năng, quy trình nghiệp vụ, chứng từ, sổ sách và báo cáo của hệ thống kế toán ACC.
  </div>
  <div class="meta-box">
    ... metadata ...
  </div>
</section>
```

### 2. The Executive Summary

```html
<section class="page page-break">
  <h2>Executive Summary</h2>
  <p>Tóm tắt mục tiêu tài liệu...</p>
  ... summary tables or lists ...
</section>
```

### 3. The Phase Chapter Structure

Each phase will be enclosed or separated with a class that forces a page break:

```html
<section class="phase-chapter page-break" id="phase-1">
  <div class="phase-header">
    <h2>PHASE 1</h2>
    <h3>Nền tảng hệ thống, danh mục, tiền mặt & tiền gửi</h3>
  </div>
  <div class="phase-intro-card">
    <h4>Mục tiêu:</h4>
    <p>...</p>
    <h4>Module chính:</h4>
    <ul>...</ul>
  </div>

  ... existing phase content (tables, rules, etc.) ...
</section>
```

## Migration Plan

1. **CSS Update**: Add classes for `.page`, `.page-break`, `.phase-header`, `.phase-intro-card`, `.exec-summary`.
2. **Cover Replacement**: Replace the current cover section with the new formal design.
3. **Add Exec Summary & TOC**: Insert the new sections immediately after the cover.
4. **Restructure Phases**: Wrap existing phases in the new chapter structure, ensuring `page-break` properties apply.
5. **Validation**: Check HTML structure, ensure no missing closing tags, and verify print view behavior using browser print preview.
