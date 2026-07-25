---
name: get-epic-context
description: Đóng gói cuộc gọi lấy bối cảnh Epic từ hệ thống qua local-mcp:call_api.
---

## Description
Kỹ năng này thực hiện cuộc gọi qua `local-mcp:call_api` để lấy thông tin chi tiết và các tài liệu đính kèm của một Epic cụ thể.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |
| epicKey | String | Có | Mã Epic |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lina",
      "name": "get_epic_context",
      "body": {
        "projectKey": "{{projectKey}}",
        "epicKey": "{{epicKey}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết bối cảnh Epic. Chứa các trường:<br>- `projectKey`: Mã dự án<br>- `epicKey`: Mã hiệu Epic<br>- `title`: Tiêu đề Epic<br>- `documents`: Mảng tài liệu đính kèm Epic (chứa `name`, `description`, `content`) |
