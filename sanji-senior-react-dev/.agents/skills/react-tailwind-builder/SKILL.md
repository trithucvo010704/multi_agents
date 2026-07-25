---
name: react-tailwind-builder
description: Dựng giao diện UI React Component chuẩn Responsive Mobile-first cao cấp (Studio-quality), TailwindCSS, Framer Motion 60fps, loại bỏ hoàn toàn AI Slop.
---

## Description
Dựng các file UI React Component chuẩn Responsive Mobile-first có độ hoàn thiện mỹ thuật cao (Studio-quality), ứng dụng cơ chế "Three Design Dials" (Variance, Motion, Density) để triệt tiêu các thiết kế AI rập khuôn (Slop), tối ưu hóa Framer Motion 60fps và đạt Lighthouse Performance >= 90.

## Triggers
- Kích hoạt khi xây dựng hoặc cập nhật bất kỳ trang, layout, component React nào trong dự án.

## Inputs
| Tên | Kiểu | Bắt buộc | Mô tả |
|-----|------|----------|-------|
| componentName | String | Có | Tên component cần tạo. |
| uiDescription | String | Có | Mô tả nghiệp vụ giao diện và tương tác. |
| designVariance | Float | Không | Núm xoay độ phá cách bố cục (0.0: An toàn/Gọn gàng -> 1.0: Phá cách/Bất đối xứng). Mặc định: 0.2. |
| motionIntensity | Float | Không | Mức độ chuyển động (0.0: Tĩnh/Micro -> 1.0: Scenic Motion mượt mà). Mặc định: 0.4. |
| visualDensity | Float | Không | Mật độ thông tin (0.0: Thoáng đạt nhiều khoảng thở -> 1.0: Nén dữ liệu dashboard). Mặc định: 0.5. |

## Core Implementation Rules (Tinh hoa Taste Skill)

### 1. Phân Tích Bối Cảnh Nghệ Thuật (Design Read)
Trước khi viết mã nguồn, Sanji bắt buộc phải phân tích nghiệp vụ để chọn một trong ba định hướng thẩm mỹ chính:
- **Minimalist (Tối giản cao cấp):** Tông màu đơn sắc/HSL chọn lọc, khoảng giãn rộng, kiểu chữ sắc nét (Outlined/Inter), nhấn mạnh vào sản phẩm.
- **Editorial (Tạp chí thời thượng):** Bố cục bất đối xứng nhẹ, sử dụng font serif kết hợp sans-serif, các mảng khối đè nhẹ lên nhau tạo chiều sâu không gian.
- **Industrial/Brutalist (Công nghiệp/Thô mộc kỹ thuật):** Viền border dày (`border-2 border-black`), đổ bóng phẳng cứng (`shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]`), lưới grid chặt chẽ, mật độ thông tin cao.

### 2. Triệt Tiêu Thiết Kế AI Rập Khuôn (Anti-Slop Protocols)
- **Không lạm dụng Card vô tội vạ:** Sử dụng các đường phân cách thanh mảnh (`border-b border-neutral-100/50`) hoặc phân chia phân khu bằng khoảng trắng (whitespaces) thay vì đóng khung tất cả nội dung vào các hộp bo góc bóng mờ màu trắng.
- **Không dùng dải Gradient tím/xanh đại trà:** Sử dụng màu sắc HSL có chủ đích, ưu tiên nền tối huyền ảo hoặc nền sáng ấm nhẹ (Warm soft background như `#FAF9F6`), sử dụng màu nhấn (Accent color) độc bản.
- **Chống lười biếng:** Tuyệt đối không viết comment dạng `// TODO: Implement later` hoặc sử dụng các thư viện Icon cồng kềnh ngoài quy chuẩn.

### 3. Responsive Mobile-First & Framer Motion 60fps
- **Mobile-First Layout:** Cấu trúc mặc định không có tiền tố là dành cho màn hình di động, bổ sung `md:` và `lg:` cho PC. Chiều cao vùng chạm của nút tối thiểu đạt 44px.
- **Tối ưu GPU Animation:** Chỉ animate các thuộc tính `transform` (x, y, scale, rotate) và `opacity` qua Framer Motion để đạt hiệu năng 60fps tuyệt đối trên di động, tránh kích hoạt lại luồng Repaint/Reflow của trình duyệt.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Giao diện bị rối mắt | Design Variance đặt quá cao trên trang thông tin | Hạ Variance xuống mức an toàn (0.1 - 0.2), sử dụng bố cục cột/lưới truyền thống. |
| Suy giảm Lighthouse Performance | DOM quá sâu do lạm dụng bọc Framer Motion | Giảm thiểu thẻ bọc, gộp các motion hiệu ứng vào một container duy nhất và tối ưu dynamic import. |