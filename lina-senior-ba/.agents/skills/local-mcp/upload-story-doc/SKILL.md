---
name: upload-story-doc
description: Đóng gói cuộc gọi tải lên tài liệu đính kèm của Story qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tải lên hoặc cập nhật các tài liệu đặc tả Markdown đính kèm của một User Story cụ thể (ví dụ: `01-story.md`, `02-flow.md`, `03-ui-ux.md`, `04-api.md`, `05-db.md`).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án (VD: `PAI`, `EZAUTO`). |
| storyKey | String | Có | Mã hiệu User Story trên hệ thống (VD: `EZAUTO-STORY-12`). |
| name | String | Có | Tên tài liệu (VD: `01-story.md`, `04-api.md`). |
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
      "name": "upload_story_doc",
      "body": {
        "projectKey": "{{projectKey}}",
        "storyKey": "{{storyKey}}",
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
| data | Object | Chi tiết thông tin tệp tài liệu Story vừa được tải lên. Chứa các trường:<br>- `name` (String): Tên tệp tin (VD: `01-story.md`).<br>- `description` (String): Mô tả của tệp tin.<br>- `content` (String/Null): Nội dung tài liệu.<br>- `createdBy` (String): Người thực hiện tải lên. |
