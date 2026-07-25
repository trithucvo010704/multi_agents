---
name: write-backend-code
description: Viết code Backend Node.js + Express, kết nối API BE chính qua api_token trong .env và tuân thủ nguyên tắc chia nhỏ file.
---

## Description
Kỹ năng viết mã nguồn Backend phục vụ cho ứng dụng local. Tích hợp API chuyển tiếp hoặc tương tác trực tiếp với Backend chính. Yêu cầu mã nguồn phải được tách biệt rõ ràng thành routes, controllers, helpers để dễ dàng merge và hạn chế conflict.

## Triggers
- Sau khi hoàn thành thiết lập cấu hình cơ bản của Backend và có danh sách task Backend từ `tasks_list`.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| tasks_list | Markdown | Có | Danh sách task và DoD của Backend |
| api_specs | Markdown/JSON | Có | Đặc tả API endpoints cần xây dựng và cấu hình kết nối BE chính |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả chi tiết |
|-----|--------------|----------------|
| backend_code | Filesystem | Các file backend (routes, controllers, config, app.js) đã được sửa/thêm |

## Steps
1. **Kiểm tra cấu hình .env:** Đảm bảo file `.env` đã được thiết lập các thông tin kết nối cần thiết (ví dụ: `MAIN_BE_URL`, `API_TOKEN`).
2. **Thiết kế Router & Controller riêng biệt (File Splitting):**
   - Tạo file routes riêng (ví dụ: `src/routes/items.js`) quản lý endpoint.
   - Tạo file controllers riêng (ví dụ: `src/controllers/itemsController.js`) xử lý logic.
   - Đăng ký router mới vào file ứng dụng chính (ví dụ: `app.js` hoặc `server.js`).
3. **Thực thi gọi API tích hợp:** Trong controller, sử dụng HttpClient (như axios hoặc fetch) để gọi tới BE chính, đính kèm `api_token` từ `process.env.API_TOKEN` vào Authorization Header.
4. **Kiểm thử cục bộ Backend:** Chạy thử Backend ở local port, kiểm tra xem endpoints có trả về đúng định dạng JSON/mã lỗi hay không.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| API BE chính trả về lỗi Auth (401/403) | Thiếu hoặc sai api_token trong .env | Đọc log, báo lỗi thiếu/sai API Token và hướng dẫn người dùng khai báo lại trong file `.env` |
| Lỗi conflict cấu trúc router | Trùng lặp đường dẫn API hoặc require sai file | Phân tích stack trace, sửa lại đường dẫn mapping hoặc đường dẫn import, chạy lại server |
