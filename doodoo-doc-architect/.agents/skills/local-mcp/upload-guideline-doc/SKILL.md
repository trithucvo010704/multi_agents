---
name: upload-guideline-doc
description: Đẩy tài liệu guideline lên hệ thống thông qua call_api.
---

## Description
Kỹ năng giúp DooDoo gọi công cụ qua `local-mcp:call_api` (namespace: `doodoo`, name: `upload_guideline_doc`) để tải nội dung tài liệu guideline mới biên soạn hoặc cập nhật lên hệ thống.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| level | String | Có | Cấp độ của guideline (VD: `PROJECT`, `EPIC`, `STORY`). |
| name | String | Có | Tên guideline (VD: `01-overview.md`). |
| description | String | Có | Mô tả ngắn về tài liệu guideline (tối đa 256 ký tự). |
| content | String | Có | Nội dung chi tiết của guideline cần tải lên. |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "doodoo",
      "name": "upload_guideline_doc",
      "body": {
        "level": "{{level}}",
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
| data | Object | Chi tiết thông tin tệp tài liệu guideline vừa được tải lên. Chứa các trường:<br>- `level` (String): Cấp độ của guideline (VD: `PROJECT`).<br>- `name` (String): Tên tệp tin (VD: `01-overview.md`).<br>- `description` (String): Mô tả của tệp tin.<br>- `content` (String/Null): Nội dung tài liệu.<br>- `createdBy` (String): Người thực hiện tải lên. |
