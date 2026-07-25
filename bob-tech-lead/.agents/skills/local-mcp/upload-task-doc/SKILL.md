---
name: upload-task-doc
description: Đóng gói cuộc gọi tải lên tài liệu liên quan đến Task qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để đẩy các tài liệu bổ trợ hoặc báo cáo kỹ thuật liên quan đến Task (ví dụ: technical_debt_note.md, code_review_report.md) lên hệ thống.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| taskKey | String | Có | Mã hiệu Task |
| name | String | Có | Tên file tài liệu |
| content | String | Có | Nội dung Markdown của tài liệu |
| description | String | Không | Mô tả ngắn về tài liệu tải lên (mặc định: "Tải lên tài liệu Task") |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "kevin",
      "name": "upload_task_doc",
      "body": {
        "taskKey": "{{taskKey}}",
        "name": "{{name}}",
        "description": "{{description || 'Tải lên tài liệu Task'}}",
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
| data | Object | Chi tiết thông tin tệp tài liệu Task vừa được tải lên. Chứa các trường:<br>- `name` (String): Tên tệp tin (VD: `code_review_report.md`).<br>- `description` (String): Mô tả của tệp tin.<br>- `content` (String/Null): Nội dung tài liệu.<br>- `createdBy` (String): Người thực hiện tải lên. |
