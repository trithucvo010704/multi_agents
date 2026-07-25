---
name: upload-epic-doc
description: Đóng gói cuộc gọi tải lên tài liệu đính kèm của Epic qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tải lên hoặc cập nhật tài liệu Markdown gắn với một Epic cụ thể trên hệ thống (ví dụ: `brief.md`).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án (VD: `PAI`, `EZAUTO`). |
| epicKey | String | Có | Mã hiệu Epic trên hệ thống (VD: `EZAUTO-EPIC-19`). |
| name | String | Có | Tên tài liệu (VD: `brief.md`). |
| description | String | Có | Mô tả ngắn gọn về tài liệu tải lên. |
| content | String | Có | Nội dung chi tiết của tài liệu (chuỗi Markdown). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lina",
      "name": "upload_epic_doc",
      "body": {
        "projectKey": "{{projectKey}}",
        "epicKey": "{{epicKey}}",
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
| data | Object | Chi tiết thông tin tệp tài liệu Epic vừa được tải lên. Chứa các trường:<br>- `name` (String): Tên tệp tin (VD: `brief.md`).<br>- `description` (String): Mô tả của tệp tin.<br>- `content` (String/Null): Nội dung tài liệu.<br>- `createdBy` (String): Người thực hiện tải lên. |
