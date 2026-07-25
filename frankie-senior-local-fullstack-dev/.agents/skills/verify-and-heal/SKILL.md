---
name: verify-and-heal
description: Chạy thử tích hợp ứng dụng local, kiểm thử chéo với DoD, phân tích log lỗi để tự động fix bug.
---

## Description
Kỹ năng kiểm tra chất lượng sản phẩm cuối cùng. Agent sẽ chạy song song Backend và Frontend ở chế độ local, thực hiện các kịch bản kiểm thử tự động/thủ công dựa trên DoD, ghi nhận log lỗi và tự động chỉnh sửa code (Self-healing / Fix bug) để đảm bảo ứng dụng hoạt động thông suốt.

## Triggers
- Sau khi hoàn thành việc phát triển cả Frontend và Backend.
- Khi nhận được thông báo lỗi trong quá trình build hoặc chạy thử.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| tasks_list | Markdown | Có | Danh sách task và DoD của dự án |
| build_command_be | String | Có | Lệnh build/run backend local (ví dụ: `npm run dev` hoặc `node server.js`) |
| build_command_fe | String | Có | Lệnh build/run frontend local (ví dụ: `npm run dev`) |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả chi tiết |
|-----|--------------|----------------|
| test_report | Markdown | Báo cáo kiểm thử tích hợp, trạng thái DoD, danh sách bug đã fix |
| app_status | String | Trạng thái ứng dụng (SUCCESS / FAILED) |

## Steps
1. **Khởi chạy ứng dụng local:**
   - Chạy Backend local trong background, ghi log ra file.
   - Chạy Frontend local trong background, ghi log ra file.
   - Kiểm tra các ports xem có khởi động thành công hay không.
2. **Kiểm tra tích hợp (Integration Testing):**
   - Thực hiện gửi request mẫu tới các endpoints của local Backend.
   - Kiểm tra xem Frontend có tải được dữ liệu từ Backend local lên hay không.
   - Đối chiếu kết quả với các tiêu chí trong `tasks_list` và DoD.
3. **Phát hiện lỗi & Tự sửa lỗi (Fix bug & Self-healing):**
   - Nếu phát hiện lỗi build (syntax, compiler error) hoặc lỗi runtime (API crash, UI render crash):
     - Phân tích log lỗi chi tiết từ file logs.
     - Xác định file gây ra lỗi.
     - Thực hiện sửa code trực tiếp trên file đó.
     - Restart server và chạy lại bước kiểm thử.
4. **Nghiệm thu & Đóng gói:** Khi tất cả DoD đã được tick xanh và không còn lỗi nghiêm trọng, tạo báo cáo nghiệm thu gửi người dùng.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Port bị xung đột (EADDRINUSE) | Port của BE hoặc FE đã bị tiến trình khác sử dụng | Tự động đọc file cấu hình (`.env` hoặc `vite.config.js`), đổi port trống khác, restart server |
| Vòng lặp sửa lỗi (Healing loop) quá 3 lần | Lỗi logic phức tạp hoặc phụ thuộc bên ngoài | Ghi nhận log chi tiết lỗi, đưa ra đề xuất hướng sửa đổi và dừng lại để hỏi ý kiến người dùng thông qua Q&A |
