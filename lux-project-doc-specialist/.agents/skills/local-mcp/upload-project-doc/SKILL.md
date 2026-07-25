---
name: upload-project-doc
description: Đẩy tài liệu dự án lên hệ thống thông qua call_api.
---

## Description
Kỹ năng giúp Lux gọi công cụ qua `local-mcp:call_api` (namespace: `lux`, name: `upload_project_doc`) để đẩy nội dung tài liệu cấp dự án đã được User chốt duyệt lên hệ thống.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| projectKey | String | Có | Mã hiệu dự án trên hệ thống (VD: `ECOM`). |
| name | String | Có | Tên file tài liệu (VD: `01-overview.md`). |
| description | String | Có | Mô tả ngắn gọn nội dung tài liệu (tối đa 256 ký tự). |
| content | String | Có | Chuỗi nội dung Markdown hoàn chỉnh của tài liệu. |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lux",
      "name": "upload_project_doc",
      "body": {
        "projectKey": "{{projectKey}}",
        "name": "{{name}}",
        "description": "{{description}}",
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
| data | Object | Chi tiết thông tin tệp tài liệu dự án vừa được tải lên. Chứa các trường:<br>- `name` (String): Tên tệp tin (VD: `01-overview.md`).<br>- `description` (String): Mô tả của tệp tin.<br>- `content` (String/Null): Nội dung tài liệu.<br>- `createdBy` (String): Người thực hiện tải lên. |
