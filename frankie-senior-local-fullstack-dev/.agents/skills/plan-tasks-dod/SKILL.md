---
name: plan-tasks-dod
description: Phân rã specs thành các task nhỏ (API, Cấu hình, Giao diện, Fix bug) và định nghĩa DoD cho từng task.
---

## Description
Kỹ năng lập kế hoạch chi tiết cho các bước thực thi. Agent sẽ phân tích bản `finalized_specs`, chia nhỏ công việc thành các task cụ thể theo 4 nhóm chính, thiết lập Definition of Done (DoD) rõ ràng và xác định chiến lược tách file để đảm bảo code gọn gàng, modular, dễ merge.

## Triggers
- Sau khi có bản đặc tả yêu cầu chi tiết thống nhất `finalized_specs`.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| finalized_specs | Markdown | Có | Đặc tả yêu cầu đã được thống nhất |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả chi tiết |
|-----|--------------|----------------|
| tasks_list | Markdown | Danh sách các task phân rã, kèm DoD và chiến lược chia file của từng task |

## Steps
1. **Phân rã task (Task Decomposition):** Chia nhỏ các yêu cầu từ `finalized_specs` thành các task thuộc 4 nhóm:
   - **API (Backend):** Các endpoints, routes, middleware cần viết.
   - **Cấu hình (Environment, Router, Styling):** `.env`, routing FE/BE, config CSS/Tailwind.
   - **Giao diện (Frontend):** UI Layout, Components, States, Interactions.
   - **Sửa lỗi (Fix bug):** Dự báo các điểm dễ phát sinh lỗi tích hợp hoặc lỗi logic để chuẩn bị phương án kiểm thử và fix bug.
2. **Thiết lập chiến lược tách file (File Splitting Strategy):** Đối với các task code, xác định rõ:
   - File backend nào cần tạo mới/sửa (ví dụ: route riêng, controller riêng, helper).
   - Component React nào cần viết (ví dụ: Button, Form, Card, Layout riêng).
   - Tuyệt đối không gộp chung logic khác loại vào một file.
3. **Định nghĩa DoD (Definition of Done):** Với mỗi task, viết rõ tiêu chí thế nào là hoàn thành (ví dụ: API trả về 200, schema hợp lệ; Component UI hiển thị đúng, responsive; không có lỗi lint).
4. **Đóng gói kế hoạch:** Lưu kế hoạch thực thi vào file `task.md` local hoặc xuất dữ liệu để chuẩn bị thực hiện.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Thiếu phân rã cho phần Fix bug | Kế hoạch chỉ tập trung viết tính năng, bỏ qua bước kiểm thử và xử lý lỗi | Bổ sung bắt buộc một mục "Fix bug & Validation" trong DoD với các scenario kiểm thử cụ thể |
| Đề xuất cấu trúc file monolithic | Đề xuất gộp code backend hoặc frontend vào chung một file lớn | Chạy cơ chế kiểm duyệt cấu trúc, tự động chia nhỏ thành các file controller/component con trước khi trình bày kế hoạch |
