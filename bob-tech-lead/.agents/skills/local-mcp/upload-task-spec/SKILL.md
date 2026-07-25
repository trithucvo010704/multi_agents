---
name: upload-task-spec
description: Đóng gói cuộc gọi tải lên tài liệu đặc tả của Task qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tải lên hoặc cập nhật tài liệu đặc tả `task_spec.md` cho một Task cụ thể.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| taskKey | String | Có | Mã hiệu Task |
| name | String | Có | Tên tài liệu đặc tả (ví dụ: `task_spec.md`) |
| content | String | Có | Nội dung Markdown của tài liệu đặc tả |
| description | String | Không | Mô tả ngắn gọn về đặc tả (mặc định: "Tải lên đặc tả nhiệm vụ") |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "upload_task_spec",
      "body": {
        "taskKey": "{{taskKey}}",
        "name": "{{name}}",
        "description": "{{description || 'Tải lên đặc tả nhiệm vụ'}}",
        "content": "{{content}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết thông tin tệp đặc tả vừa được tải lên. Chứa các trường:<br>- `name` (String): Tên tệp tin (VD: `task_spec.md`).<br>- `description` (String): Mô tả của tệp tin.<br>- `content` (String/Null): Nội dung tài liệu.<br>- `createdBy` (String): Người thực hiện tải lên. |
