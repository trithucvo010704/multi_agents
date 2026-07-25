---
name: write-frontend-code
description: Viết code Frontend React + Vite + Tailwind CSS, kết nối API local và chia nhỏ các UI components.
---

## Description
Kỹ năng phát triển giao diện người dùng cho ứng dụng local. Sử dụng React, Vite và Tailwind CSS để xây dựng giao diện responsive, hiện đại. Kỹ năng này bắt buộc phải chia nhỏ giao diện thành các components nguyên tử riêng biệt để tối ưu hóa việc quản lý mã nguồn và merge code.

## Triggers
- Sau khi hoàn thành thiết lập Backend sơ bộ và có danh sách task Frontend từ `tasks_list`.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| tasks_list | Markdown | Có | Danh sách task và DoD của Frontend |
| ui_specs | Markdown | Có | Đặc tả giao diện người dùng, các components và luồng tương tác |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả chi tiết |
|-----|--------------|----------------|
| frontend_code | Filesystem | Các components, hooks, assets và file config của Frontend đã được thêm/sửa |

## Steps
1. **Phân rã Component (File Splitting):**
   - Không viết dồn toàn bộ giao diện vào một file (như `App.jsx`).
   - Tạo thư mục `src/components/` chứa các component nhỏ hơn (ví dụ: `Header.jsx`, `Sidebar.jsx`, `DataCard.jsx`, `ConfigForm.jsx`).
   - Đặt styles và assets riêng biệt. Sử dụng tailwind classes trực tiếp trên từng component.
2. **Xây dựng Giao diện & Trạng thái (UI & States):**
   - Viết các UI component theo thiết kế responsive và các trạng thái loading, error, empty.
   - Quản lý state bằng hooks (`useState`, `useEffect`, hoặc custom hooks).
3. **Kết nối API local:**
   - Cài đặt proxy trong `vite.config.js` hoặc cấu hình biến môi trường `.env` của Frontend để trỏ tới Backend local.
   - Gọi API local để fetch và hiển thị dữ liệu hoặc cập nhật cấu hình.
4. **Kiểm tra styling và responsive:** Đảm bảo responsive trên các kích cỡ màn hình khác nhau và các class Tailwind CSS hoạt động chính xác.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Giao diện bị vỡ layout hoặc Tailwind không nhận style | Cấu hình file `tailwind.config.js` thiếu đường dẫn quét component hoặc sai phiên bản | Kiểm tra lại file cấu hình tailwind, thêm đường dẫn quét thư mục `src/**/*.{js,ts,jsx,tsx}`, build lại FE |
| API call từ FE đến BE bị lỗi CORS hoặc 404 | Chưa thiết lập proxy hoặc gọi sai địa chỉ cổng local BE | Kiểm tra config port của BE và proxy config của Vite, khởi động lại Vite dev server |
