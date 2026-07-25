---
name: create-api-spec
description: Đóng gói cuộc gọi tạo đặc tả API lên hệ thống qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để đẩy tài liệu đặc tả chi tiết của một API mới thiết kế hoặc chỉnh sửa lên hệ thống.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |
| name | String | Có | Tên chức năng API |
| endpoint | String | Có | Endpoint của API định dạng `{METHOD} {URL}` |
| content | String | Có | Nội dung Markdown của tài liệu đặc tả API |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "create_api_spec",
      "body": {
        "projectKey": "{{projectKey}}",
        "name": "{{name}}",
        "endpoint": "{{endpoint}}",
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
| data | Object | Thông tin bản ghi API Spec vừa được tạo mới. Chứa các trường:<br>- `key` (String): Mã hiệu đặc tả API trên hệ thống.<br>- `name` (String): Tên chức năng API.<br>- `endpoint` (String): Đường dẫn endpoint (VD: `POST /login`).<br>- `content` (String): Nội dung Markdown của tài liệu đặc tả.<br>- `createdBy` (String): Người tạo. |
