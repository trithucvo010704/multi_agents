---
name: epic-task-decomposition
description: Phân rã toàn bộ các Stories thuộc một Epic thành các Task kỹ thuật chi tiết theo từng Repository, đồng bộ đặc tả API, và đăng ký lên hệ thống.
---

## Description
Kỹ năng này giúp Tech Lead (Bob) phân rã toàn bộ các Stories thuộc một Epic cụ thể thành các nhiệm vụ kỹ thuật (Tasks) chi tiết cho các Lập trình viên. Bằng cách load toàn bộ ngữ cảnh Epic và các Stories của Epic qua `get-epic-full-context`, Bob có cái nhìn toàn diện để thiết kế hệ thống và phân rã các tasks đồng bộ, nhất quán hơn.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án (VD: `PAI`, `EZAUTO`). |
| epicKey | String | Có | Mã hiệu Epic cần phân rã (VD: `EZAUTO-EPIC-19`). |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| systemTasks | Action | Gọi `create_task` tạo danh sách task trên hệ thống DB cho từng Story trong Epic. |
| apiSpecs | Action | Gọi `create_api_spec` để đẩy đặc tả API của các Backend tasks lên hệ thống. |
| taskSpecs | Action | Gọi `upload_task_spec` để đẩy chi tiết `task_spec.md` cho từng Task. |

## Steps
1. **Lấy bối cảnh Epic toàn diện:** Gọi skill đóng gói **`local-mcp/get-epic-full-context`** để tải bối cảnh Epic và toàn bộ thông tin chi tiết của tất cả các Stories thuộc Epic đó (kèm theo toàn bộ tài liệu đặc tả của từng Story).
2. **Lấy danh mục Repositories:** Gọi skill đóng gói **`local-mcp/get-project`** để lấy thông tin các repository hợp lệ và cấu hình của dự án.
3. **Phân tích thiết kế hệ thống:** Đọc toàn bộ các tài liệu đặc tả của các Stories trong Epic để có cái nhìn tổng quan:
   - Nhận diện các kết nối chéo giữa các Stories (Shared components, shared database tables, shared API endpoints).
   - Thiết kế giải pháp tổng thể cho cả Epic trước khi đi vào chi tiết từng Story.
4. **Phân rã Task theo từng Story:** Với mỗi Story trong danh sách:
   - Chia nhỏ Story thành các đầu việc độc lập (Backend, Frontend, Fullstack...).
   - Áp dụng ràng buộc: *1 Task = 1 Repo duy nhất* nằm trong danh sách repository hợp lệ của dự án.
5. **Tạo Task trên DB:** Gọi skill đóng gói **`local-mcp/create-task`** để đăng ký lấy `taskKey` từ hệ thống, truyền các tham số: `projectKey`, `storyKey`, `title`, `priority` và `repositoryName`.
6. **Đẩy đặc tả API lên hệ thống:** Đối với các Backend task liên quan đến API mới hoặc chỉnh sửa, gọi skill đóng gói **`local-mcp/create-api-spec`** để công bố thông số kỹ thuật chi tiết của API lên hệ thống.
7. **Soạn thảo và Upload Đặc tả Task:** Viết nội dung đặc tả nhiệm vụ kỹ thuật (`task_spec.md`) bao gồm:
   - Repository gán (`repositoryName`).
   - Hướng dẫn triển khai kỹ thuật và công nghệ yêu cầu.
   - Tham chiếu API Spec (Endpoint, HTTP Method).
   - Gọi skill đóng gói **`local-mcp/upload-task-spec`** để đẩy tài liệu lên hệ thống.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Epic không tồn tại hoặc trống | Sai `epicKey` hoặc Epic chưa có Story nào | Dừng thực thi, báo cáo lỗi và yêu cầu PM/BA kiểm tra lại. |
| Một task chạm nhiều Repo | Thiết kế task bị gộp chung | Hủy bỏ thiết kế cũ, thực hiện chia tách nhỏ hơn để đạt tính đơn nhiệm. |
| Không tìm thấy Repository phù hợp | Tên repo thiết kế không nằm trong danh sách repo hợp lệ của dự án | Báo cáo lỗi cấu hình dự án cho PM/User qua chat, yêu cầu cập nhật danh bạ repository của dự án. |
