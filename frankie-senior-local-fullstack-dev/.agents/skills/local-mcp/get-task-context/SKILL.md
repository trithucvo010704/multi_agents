---
name: get-task-context
description: Gọi mcp tool get_context_task qua call_api của local-mcp để lấy thông tin chi tiết và tài liệu đặc tả của Task dựa trên taskKey.
---

## Description
Kỹ năng này giúp Dev lấy toàn bộ dữ liệu nghiệp vụ, ranh giới kỹ thuật và file đặc tả nhiệm vụ (`task-spec.md`) do Tech Lead Bob gán cho task thông qua mã hiệu `taskKey`.

## Triggers
- Kích hoạt khi bắt đầu chu kỳ thực thi của một task cụ thể.
- Yêu cầu tiên quyết: Được cung cấp mã định danh Task (`taskKey`).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| `taskKey` | String | Có | Mã hiệu duy nhất của Task cần thực hiện (ví dụ: `ECOM-TS-01`). |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết bối cảnh Task và tài liệu đính kèm. Chứa các trường:<br>- `projectKey` (String): Mã hiệu dự án.<br>- `storyKey` (String): Mã User Story.<br>- `key` (String): Mã hiệu Task.<br>- `title` (String): Tiêu đề Task.<br>- `documents` (List<Object>): Mảng tài liệu đính kèm Task, mỗi tệp gồm: `name`, `description`, `content`, `createdBy`.<br>- `story` (Object): Thông tin chi tiết Story chứa Task đó. |

## Steps
1. **Bước 1:** Thực hiện gọi MCP tool **`local-mcp:call_api`** để gọi gián tiếp API `get_context_task` (namespace: `kevin`) với body `{"taskKey": taskKey}`.
2. **Bước 2:** Nhận phản hồi từ MCP server, kiểm tra tính hợp lệ của dữ liệu.
   - Nếu tìm thấy task, trích xuất dữ liệu `data` (bao gồm `storyKey`, `title`, `priority` và nội dung file `task-spec.md`).
   - Nếu không tìm thấy hoặc lỗi kết nối, chuyển sang phần xử lý lỗi.
3. **Bước 3:** Đóng gói thông tin `taskContext` dưới dạng JSON Object chuẩn để bàn giao cho các bước lập kế hoạch và code.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Không tìm thấy Task | Sai `taskKey` hoặc hệ thống chưa đăng ký task | Ghi nhận lỗi và báo cáo trực tiếp cho Tech Lead hoặc User qua giao diện chat để làm rõ, sau đó dừng thực hiện. |
| MCP Tool Timeout | Sự cố mạng hoặc MCP server không phản hồi | Thực hiện thử lại (Retry) tối đa 2 lần, mỗi lần cách nhau 5 giây. |
