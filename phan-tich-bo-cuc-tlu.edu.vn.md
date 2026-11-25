# Phân tích cấu trúc trang chủ Trường Đại học Thủy lợi (https://tlu.edu.vn/)

> Phân tích ngày 25/11/2026. Trang được xây bằng **Next.js + Tailwind CSS**, slider dùng thư viện **Swiper**. Thực tế site kết hợp Flexbox (điều phối 1 trục) và CSS Grid (bố cục 2 chiều).

---

## 1. Cấu trúc trang theo tư duy bố cục (chỉ dùng `div`, xác định thẻ lồng nhau)

```text
<div id="app">                                ← gốc trang (cột dọc: header → main → footer)
│
├── <div class="header">                       ← thanh đầu trang, sticky (dính khi cuộn)
│   ├── <div class="header-top">               ← dải trắng chứa brand
│   │   ├── <div class="header-logo">          ← logo + tên trường
│   │   └── <div class="header-tools">         ← nhóm công cụ bên phải
│   │       ├── <div class="header-search">    ← ô tìm kiếm (desktop)
│   │       ├── <div class="header-lang">      ← chuyển ngôn ngữ VN/EN
│   │       └── <div class="header-menu-btn">  ← nút hamburger
│   ├── <div class="header-nav">               ← dải xanh #0118d8 chứa menu chính
│   │   └── <div class="header-nav-inner">     ← giới hạn bề rộng 1400px
│   └── <div class="header-drawer">            ← menu phụ trợ (mobile): search + nav + footer phụ
│       ├── <div class="drawer-header">
│       ├── <div class="drawer-search">
│       ├── <div class="drawer-nav">
│       └── <div class="drawer-footer">
│
├── <div class="main">                         ← thân trang (chiếm phần dẻo còn lại)
│   ├── <div class="banner-slider">            ← ① slideshow toàn chiều rộng
│   │   ├── <div class="banner-track">         ← hàng ngang các slide (swiper-wrapper)
│   │   │   └── <div class="banner-slide"> ×7
│   │   └── <div class="banner-dots">          ← chấm chuyển slide
│   │
│   ├── <div class="news-block">               ← ② TIN TỨC + THÔNG BÁO
│   │   └── <div class="news-container">       ← lưới 3 cột (2 + 1)
│   │       ├── <div class="news-main">        ← cột trái (chiếm 2)
│   │       │   ├── <div class="section-heading">
│   │       │   └── <div class="news-grid">    ← tin nổi bật (2fr) + tin phụ (1fr)
│   │       └── <div class="news-notice">      ← cột phải: danh sách thông báo
│   │           ├── <div class="section-heading">
│   │           └── <div class="notice-list">
│   │
│   ├── <div class="events-block">             ← ③ SỰ KIỆN
│   │   ├── <div class="section-heading">
│   │   └── <div class="events-slider">
│   │       ├── <div class="events-card">      ← ngày (19/11) + nội dung sự kiện
│   │       ├── <div class="events-arrows">
│   │       └── <div class="events-dots">
│   │
│   ├── <div class="stats-block">              ← ④ NHỮNG CON SỐ ẤN TƯỢNG (5 ô)
│   │   ├── <div class="section-heading">
│   │   └── <div class="stats-row">            ← 5 cột: Người học / Đối tác / % có việc / Ngành / TS
│   │
│   ├── <div class="hero-image-block">         ← ⑤ ảnh giới thiệu phủ toàn bề rộng
│   │
│   ├── <div class="admission-block">          ← ⑥ TUYỂN SINH (2 cột: ảnh | chữ)
│   │   ├── <div class="admission-image">
│   │   └── <div class="admission-content">
│   │       ├── <div class="section-heading">
│   │       ├── <div class="admission-text">
│   │       ├── <div class="admission-links">  ← Đại học / Thạc sĩ / Tiến sĩ
│   │       └── <div class="admission-cta">    ← nút ĐĂNG KÝ NGAY
│   │
│   ├── <div class="training-block">           ← ⑦ 3 cột: ĐÀO TẠO | SINH VIÊN | CỰU SINH VIÊN
│   │   └── <div class="training-col"> ×3
│   │       ├── <div class="section-heading">
│   │       └── <div class="feature-card">     ← thẻ tin có bóng đổ
│   │
│   ├── <div class="units-block">              ← ⑧ CÁC ĐƠN VỊ ĐÀO TẠO, KHCN (2 vùng)
│   │   ├── <div class="units-list">           ← cột trái: tên các khoa, cuộn dọc
│   │   └── <div class="units-detail">         ← cột phải: mô tả + nút "Khám phá"
│   │
│   ├── <div class="international-block">      ← ⑨ HỢP TÁC QUỐC TẾ (3 card + 1 list)
│   ├── <div class="research-block">           ← ⑩ NGHIÊN CỨU (bố cục y như ⑨)
│   │   ├── <div class="section-heading">
│   │   ├── <div class="card-row">             ← 3 thẻ ảnh+chữ
│   │   └── <div class="side-list">            ← cột thứ 4: danh sách phân cách gạch ngang
│   │
│   ├── <div class="partners-block">           ← ⑪ MẠNG LƯỚI ĐỐI TÁC (nền xanh)
│   │   ├── <div class="section-heading">
│   │   ├── <div class="partners-intro">
│   │   └── <div class="partners-logo-slider">
│   │
│   ├── <div class="community-block">          ← ⑫ VÌ CỘNG ĐỒNG (bố cục như ⑨⑩)
│   └── <div class="gallery-block">            ← ⑬ KHOẢNH KHẮC TLU (lưới mosaic)
│       ├── <div class="section-heading">
│       └── <div class="gallery-grid">         ← 15 ô, có ô chiếm 3 cột × 2 hàng
│
├── <div class="quick-access">                 ← cụm 4 nút nổi bám mép phải màn hình
│
└── <div class="footer">                        ← chân trang nền xanh #1907dc
    ├── <div class="footer-container">
    │   ├── <div class="footer-contact-row">   ← logo + Địa chỉ | Email | Điện thoại
    │   ├── <div class="footer-links-row">     ← 4 cột: GIỚI THIỆU / TRUY CẬP NHANH /
    │   │                                       THEO DÕI TLU / BẢN ĐỒ TƯƠNG TÁC
    │   └── <div class="footer-copyright">     ← dòng © + link Trung tâm Công nghệ số
```

**Quy ước đặt tên:** tiền tố theo vùng (`header-`, `news-`, `events-`…) + hậu tố theo vai trò (`-block` = section, `-container` = giới hạn bề rộng, `-row`/`-col` = hàng/cột flex, `-card` = thẻ lặp, `-heading` = tiêu đề dùng chung 13 lần).

---

## 2. Phân tích tư duy thiết kế Flexbox từng thành phần

| Thành phần | Trục & quan hệ Flexbox | Điểm thiết kế |
|---|---|---|
| `#app` (body) | `flex-direction: column`, `min-height: 100vh` | **Sticky footer layout kinh điển**: `main` là `flex: 1` để footer luôn bị đẩy xuống cuối dù nội dung ngắn. |
| `header-top` | `row` + `align-items: center` + `justify-content: space-between` | Logo `flex: none` (không bị co), cụm tools `margin-left: auto` — **dùng `ml-auto` thay cho space-between** để nhóm phải luôn bám phải. |
| `header-nav` | `row` + `align-items: stretch`, `ul { display:flex }` | Menu ngang: các `li` kéo **cao đầy đủ dải màu** (items-stretch) để vùng hover liền mạch; menu tự cuộn ngang khi tràn. |
| `header-drawer` | `column` + `flex: 1` cho phần nav | **3 vùng header/body/footer trong drawer**: body `overflow-y: auto` + `flex: 1`, header/footer `flex: none` — pattern off-canvas chuẩn. |
| `banner-slider` | `row` (swiper-wrapper) | Không dùng flex thuần mà **tính translateX trên hàng ngang**; dots là `row` + `justify-content: center` + `gap`. |
| `news-container` | **Grid 3 cột** (`lg:grid-cols-3`), `news-main` chiếm `col-span: 2` | Bên trong card tin lại dùng `column` + `flex: 1` để **footer tin (ngày đọc) bị đẩy xuống đáy**, mọi card cao bằng nhau. |
| `notice-list` | `column`, các `li` `row` + `gap` | Icon + chữ căn `align-items: flex-start`; `divide-y` tạo vạch ngăn — flex lo khoảng cách, border lo phân cách. |
| `events-card` | `row`: khối ngày (`flex: none`) + nội dung (`flex: 1`) | Ngày 19/11 là **neo trái cố định**, phần phải dẻo. Overlay nhiều sự kiện: `position: absolute` + `column` + `flex: 1` cho từng article; arrows `justify-content: space-between`. |
| `stats-row` | **Grid 5 cột**, mỗi ô bên trong `column` + `align-items: center` | Số đếm to ở trên, nhãn dưới, căn giữa theo trục dọc — mỗi ô `min-width: 0` chống tràn chữ. |
| `admission-block` | **Grid 2 cột** desktop; **mobile chuyển về `column`** | Ảnh `aspect-ratio: 4/3` giữ tỷ lệ, chữ `flex: 1` chiếm hết khoảng còn lại; CTA `text-left` trên desktop. |
| `training-block` | **Grid 3 cột**, mỗi `feature-card` là `column` + `flex: 1` | 3 cột **độc lập nhưng cao bằng nhau** nhờ card trong kéo giãn (`flex-1`). |
| `units-block` | `row` (left \| right) | List tên khoa cuộn **dọc** (swiper vertical — đúng sở trường flex column + `overflow`); overlay gradient là div trần `position: absolute`, không tham gia flow. |
| `international/research/community` | `grid-cols: [1fr 1fr 1fr 230px]` | 3 card ảnh + 1 cột danh sách hẹp hơn — **lưới bất đối xứng**; mobile fallback về slider `column`. |
| `partners-block` | `column` + `align-items: center` | Toàn khối căn giữa trên nền xanh; logo slider `row` + `gap` chạy vô hạn. |
| `gallery-grid` | **Grid mosaic**: `grid-cols-4`, `auto-rows`, ô nổi bật `col-span-3 / row-span-2` | Flexbox không làm được — đây là Grid thuần. |
| `quick-access` | `column` + `gap` + `position: fixed` | 4 nút vuông vức `h-10 w-10`, icon `flex` căn giữa cả 2 trục; `display: none` dưới 768px. |
| `footer-contact-row` | **Grid `1.35fr 1fr 1fr 1fr`**, mỗi item liên hệ là `row` + `gap-2` | Icon `flex: none` + `align-items: flex-start` (icon không bị kéo giãn khi text nhiều dòng); `min-width: 0` chống text dài phá vỡ cột. |
| `footer-links-row` | `grid-cols-4`, mỗi cột `column` + tiêu đề + `ul` | Cột social: mỗi link `row` + `gap` để icon + nhãn thẳng hàng. |

**Tư duy chung rút ra:**

- Flexbox được dùng cho *thành phần cấp trong* (thẻ, hàng icon–chữ, drawer, căn giữa); Grid cho *xương cấp ngoài* (chia cột section).
- Kỹ thuật lặp lại nhiều nhất: `flex: 1` + `min-width: 0` để vùng dẻo co giãn an toàn.
- Phân tách 2 nhóm trái–phải: `margin-left: auto` hoặc `justify-content: space-between`.
- Card cao bằng nhau: container `column` + phần thân `flex: 1` đẩy footer xuống đáy.

---

## 3. Kiểu nội dung & phần tử HTML nên dùng cho từng thành phần

| Thành phần | Kiểu nội dung | Phần tử HTML nên dùng |
|---|---|---|
| `header-logo` | Ảnh logo + link về trang chủ | `<a href="/">` → `<img>` (alt) hoặc `<svg>` |
| `header-search` | Form tìm kiếm | `<form>` → `<input type="search">` + `<button type="submit">` |
| `header-lang` | Bật/tắt ngôn ngữ | `<label>` + `<input type="checkbox">` (iOS toggle) |
| `header-menu-btn` | Nút mở drawer | `<button aria-label="Menu">` → `<svg>` |
| `header-nav` | Menu 1 cấp + dropdown | `<nav>` → `<ul>` → `<li>` → `<a>`; dropdown: `<button aria-expanded>` lồng `<ul>` |
| `banner-slider` | Ảnh lớn có caption | `<section role="region">` → `<figure>` → `<img>` + `<figcaption>`; dots: `<button>` |
| `section-heading` | Tiêu đề mục + link "Xem thêm" | `<h2>` (viết hoa) + `<a>` |
| `news-main` | Tin nổi bật: ảnh, chuyên mục, tiêu đề, ngày | `<article>` → `<a><img></a>` + `<span>` (category badge) + `<h3>` + `<time datetime>` |
| `notice-list` | Danh sách thông báo tiêu đề + ngày | `<ul>` → `<li>` → `<a>` + `<time>` |
| `events-card` | Ngày + tên sự kiện + địa điểm + giờ | `<article>` → `<time>` (khối ngày tách `<strong>`/`<span>`) + `<h3>` + `<address>`/`<p>`; điều hướng: `<button>` |
| `stats-row` | Cặp số liệu ↔ nhãn | **`<dl>`** → `<div>` → `<dt>` (nhãn) + `<dd>` (số, `<strong>` hoặc `<span data-count>`) |
| `hero-image-block` | Ảnh tự sự (kỷ niệm 50 năm) | `<img>` trong `<section>` (ảnh trang trí, alt mô tả) |
| `admission-links` | Liệt kê bậc đào tạo | `<ul>` → `<li>` → `<a>` (có marker "›") |
| `admission-cta` | Nút kêu gọi hành động | `<a role="button">` hoặc `<button>` |
| `training-col` | 1 card tin chuyên mục | `<article>` → `<img>` + `<h3>` + `<p>` |
| `units-list` | Danh sách tên đơn vị cuộn dọc | `<ul>` → `<li>` → `<button>` (click đổi panel phải) |
| `units-detail` | Mô tả + nút khám phá | `<p>` + `<a>`; nền ảnh: `<div aria-hidden>` hoặc `<img>` |
| `card-row` (HTQT/NC/CĐ) | 3 card: ảnh + category + tiêu đề + ngày | `<article>` ×3, như mẫu `news-main` |
| `side-list` | Tin dạng chữ thuần | `<ul>` → `<li>` → `<a>` + `<time>` |
| `partners-logo-slider` | Dải logo đối tác | `<ul>` → `<li>` → `<img>` (mỗi logo 1 mục) |
| `gallery-grid` | Lưới ảnh mở lightbox | `<button>` (mở popup, không điều hướng) → `<img loading="lazy">`; lightbox: `<dialog>` |
| `quick-access` | 4 tiện ích (đăng ký học, liên hệ, bản đồ, top) | `<nav aria-label="Tiện ích">` → `<a>` ×4 → `<svg>` |
| `footer-contact-row` | Thông tin liên hệ | `<address>` → mỗi mục: `<svg>` + `<p>`; email/SĐT: `<a href="mailto:">`, `<a href="tel:">` |
| `footer-links-row` | 4 cụm sitemap + social | `<nav>`/`<section>` → `<h3>` + `<ul>` → `<li>` → `<a>`; social: `<a rel="me">` + `<svg>` |
| `footer-copyright` | Bản quyền | `<p>` → `© 2026…` + `<a>` |

---

## Phụ lục: Dàn trang thực tế của site (ghi nhận từ DOM)

- Container chung: `max-width: 1400px`, padding `px-4 / sm:px-6 / lg:px-8`.
- Menu desktop ẩn dưới 1025px, thay bằng drawer `width: 340px / max 90vw`.
- Section tin dạng lưới: `grid-cols-[repeat(3,minmax(0,1fr))_minmax(230px,1fr)]` (desktop) → slider (mobile).
- Gallery: `grid-cols-3/4`, `auto-rows-[100px~160px]`, ô lớn `col-span-3 row-span-2`.
- Footer: `grid-cols-[1.35fr_1fr_1fr_1fr]` cho hàng liên hệ, `grid-cols-4` cho hàng links.
