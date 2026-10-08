# Nội Thất — Website nội thất

Website thương mại điện tử nội thất xây dựng bằng **Astro + React + Tailwind CSS v4**.
Giao diện theo phong cách tối giản, sang trọng (tông walnut / sand / clay), tương thích
responsive trên điện thoại, tablet và desktop.

## Tech stack

| Thành phần | Công nghệ |
| :--- | :--- |
| Framework | Astro 7 (`@astrojs/react`) |
| UI | React 19, Astro components |
| Styling | Tailwind CSS 4 (`@tailwindcss/vite`) |
| Ngôn ngữ | TypeScript (strict) |
| Font | Be Vietnam Pro (sans), Lora (display) |

## Yêu cầu môi trường

- Node.js `>= 22.12.0`
- npm

## Cài đặt & chạy

```sh
npm install        # cài dependencies
npm run dev        # dev server: http://localhost:4321
npm run build      # build production vào ./dist
npm run preview    # xem thử bản build
```

Các lệnh Astro CLI khác:

```sh
npm run astro -- --help
```

## Cấu trúc thư mục

```text
storefront/
├── public/                     # ảnh, favicon, tài nguyên tĩnh
├── src/
│   ├── components/             # Header, Footer, ProductCard
│   ├── data/
│   │   ├── products.ts         # danh mục, không gian, khoảng giá, danh sách sản phẩm
│   │   └── product-details.ts  # mô tả, kích thước, bảo hành theo slug
│   ├── layouts/                # BaseLayout (site), AdminLayout (quản trị)
│   ├── pages/                  # route (xem bảng bên dưới)
│   ├── scripts/                # cart.ts, validate.ts, phong-thuy.ts
│   └── styles/global.css       # design tokens (@theme) + base styles
└── astro.config.mjs
```

## Các trang (routes)

| Route | Mô tả |
| :--- | :--- |
| `/` | Trang chủ: hero, danh mục theo không gian, sản phẩm nổi bật, dự án, showroom |
| `/san-pham` | Danh sách sản phẩm: lọc theo danh mục / không gian / khoảng giá, sắp xếp, phân trang |
| `/san-pham/[slug]` | Chi tiết sản phẩm: thông tin, kích thước, bảo hành, thêm vào giỏ |
| `/gio-hang` | Giỏ hàng |
| `/thanh-toan` | Thanh toán: địa chỉ giao hàng, phương thức, xác nhận |
| `/dang-nhap` | Đăng nhập |
| `/dang-ky` | Đăng ký tài khoản |
| `/phong-thuy` | Tư vấn phong thủy theo năm sinh, giới tính, loại phòng |
| `/admin` | Bảng quản trị: thống kê + danh sách sản phẩm (UI) |

## Tính năng chính

- **Giỏ hàng** (`src/scripts/cart.ts`): lưu bằng `localStorage`, phát sự kiện `cart:updated`
  để Header và các trang cập nhật số lượng, định dạng tiền `vi-VN`.
- **Lọc & phân trang sản phẩm**: 7 danh mục, 6 không gian, 4 khoảng giá, 8 sản phẩm/trang.
- **Biểu mẫu**: validate phía client (`src/scripts/validate.ts`) với các rule `required`,
  `email`, `phone`, `minLength`, `matches`, `accepted`.
- **Tư vấn phong thủy** (`src/scripts/phong-thuy.ts`): tra cung mệnh (Bát trạch) theo năm
  sinh, gợi ý hướng tốt, màu sắc và ý tưởng bài trí.
- **Responsive**: layout dùng grid/breadcrumb/menu trượt thích ứng mọi kích thước màn hình.

## Dữ liệu

Dữ liệu sản phẩm hiện là **mẫu tĩnh** trong `src/data/`:

- `products.ts` — 19 sản phẩm, interface `Product` (slug, name, category, space, price, material, isNew).
- `product-details.ts` — mô tả, kích thước, thời hạn bảo hành theo `slug`.

Khi nối backend, thay hai nguồn này bằng API mà không cần đổi component.

## Design tokens

Khai báo trong `src/styles/global.css` dưới `@theme`:

- Nền/chữ: `sand-50/100/200`, `walnut-800/900`
- Điểm nhấn: `clay-500/600`, `olive-700`, `danger-600`
- Font: `--font-sans` (Be Vietnam Pro), `--font-display` (Lora)

## Trạng thái dự án

- Đã xong: layout khung + responsive, danh sách & chi tiết sản phẩm, giỏ hàng, thanh toán,
  đăng nhập/đăng ký, phong thủy, giao diện admin.
- Còn lại: nối API backend (sản phẩm / giỏ hàng / tài khoản), thay dữ liệu mẫu bằng dữ liệu
  thật, tích hợp AI cho phần tư vấn phong thủy.

## Ghi chú phát triển

- Dev server chạy nền: `astro dev --background`, quản lý bằng `astro dev stop`,
  `astro dev status`, `astro dev logs`.
- Tài liệu Astro: https://docs.astro.build
