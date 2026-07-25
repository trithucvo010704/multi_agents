---
name: task-decomposition
description: Phân rã Story thành các Task kỹ thuật chi tiết theo từng Repository, đồng bộ đặc tả API, và đăng ký lên hệ thống.
---

## Description
Bob chia nhỏ Story thành các đơn vị công việc chuyên biệt cho lập trình viên (DEV) dựa trên danh sách các Repository lấy động từ dự án, đảm bảo nguyên tắc cô lập trách nhiệm, đẩy đặc tả API lên hệ thống, và thiết lập tài liệu task-spec cho các Dev.

## Triggers
- Khi người dùng nhắn "[storyKey] đã được duyệt, bắt đầu phân rã task"

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã hiệu dự án |
| storyKey | String | Có | Mã hiệu story được duyệt phân rã |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| systemTasks | Action | Gọi `create_task` tạo danh sách task trên hệ thống DB kèm repositoryName. |
| apiSpecs | Action | Gọi `create_api_spec` để đẩy đặc tả API của các Backend tasks lên hệ thống. |
| taskSpecs | Action | Gọi `upload_task_spec` để đẩy chi tiết `task_spec.md` cho từng Task. |

## Steps
1. **Lấy danh mục Repositories:** Gọi skill đóng gói **`local-mcp/get-project`** với tham số đầu vào là `projectKey` để lấy thông tin chi tiết của dự án, bao gồm danh sách các repository hợp lệ và thông tin cấu trúc liên quan.
2. **Trích xuất Contract:** Sử dụng tài liệu API Spec (`apiSpec`) đã được tải từ context của Story trước đó để lấy API contract cần thiết.
3. **Thiết kế Task:** Chia nhỏ Story thành các đầu việc độc lập. Ràng buộc: *1 Task = 1 Repo duy nhất* và repo này phải nằm trong danh sách các repository hợp lệ thu được từ Bước 1.
4. **Tạo Task trên DB:** Với mỗi task được thiết kế, gọi skill đóng gói **`local-mcp/create-task`** để đăng ký lấy `taskKey` từ hệ thống, truyền các tham số: `projectKey`, `storyKey`, `title`, `priority` và **`repositoryName`** (tên repo xác định ở Bước 3).
5. **Đẩy đặc tả API lên hệ thống:** Đối với các Backend task liên quan đến API mới hoặc chỉnh sửa API, gọi skill đóng gói **`local-mcp/create-api-spec`** để công bố thông số kỹ thuật chi tiết của API lên hệ thống.
6. **Soạn thảo và Upload Đặc tả Task:** Viết nội dung đặc tả nhiệm vụ kỹ thuật (`task_spec.md`) bao gồm:
   - Repository gán (`repositoryName`).
   - Hướng dẫn triển khai kỹ thuật.
   - **Tham chiếu API Spec:** Ghi rõ thông tin Endpoint, HTTP Method và tên API đã đẩy ở Bước 5 để Dev Backend đối soát.
   - Thư viện cần cài đặt và Contract trích xuất.
   - **Công nghệ cần biết** (danh sách các thư viện, ngôn ngữ hoặc framework yêu cầu cho task).
   - Gọi skill đóng gói **`local-mcp/upload-task-spec`** để đẩy tài liệu lên hệ thống.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Story không ở trạng thái IN_PROGRESS | PM chưa duyệt Story | Dừng thực thi, báo cáo lỗi trạng thái và yêu cầu PM duyệt trước. |
| Một task chạm nhiều Repo | Thiết kế task bị gộp chung | Hủy bỏ thiết kế cũ, bắt buộc thực hiện chia tách nhỏ hơn để đạt tính đơn nhiệm. |
| Không tìm thấy Repository phù hợp | Tên repo thiết kế không nằm trong danh sách repo hợp lệ của dự án | Báo cáo lỗi cấu hình dự án cho PM/User qua chat, yêu cầu cập nhật danh bạ repository của dự án và dừng workflow. |
| Đẩy API spec thất bại | MCP server lỗi hoặc thông tin API bị trùng lặp | Ghi nhận lỗi và thử lại tối đa 2 lần. Nếu tiếp tục lỗi, liên kết thông tin API dạng plain-text trực tiếp trong tài liệu `task_spec.md` để Dev không bị thiếu ngữ cảnh. |
