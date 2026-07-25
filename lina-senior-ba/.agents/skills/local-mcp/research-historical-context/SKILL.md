---
name: research-historical-context
description: Tìm kiếm bối cảnh và tài liệu Epic/Story cũ theo ngữ nghĩa gần đúng nhất qua call_api.
---

## Description
Sử dụng công cụ tìm kiếm ngữ nghĩa để tra cứu các tài liệu Epic Brief hoặc Story Specs cũ của một dự án cụ thể trên hệ thống, giúp tìm ra các tính năng tương đồng có độ khớp gần nhất.

## Inputs
| Tên | Kiểu | Bắt buộc | Mô tả |
|-----|------|----------|-------|
| projectKey | String | Có | Mã hiệu duy nhất của dự án trên hệ thống (VD: `PAI`). |
| query | String | Có | Câu truy vấn tìm kiếm ngữ nghĩa (VD: `Đăng nhập qua JWT`, `gán gói cước môi giới`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lina",
      "name": "research_document",
      "body": {
        "projectKey": "{{projectKey}}",
        "text": "{{query}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu | Mô tả |
|-----|------|-------|
| success | Boolean | `true` nếu tìm kiếm thành công |
| message | String | Thông báo từ hệ thống |
| data | List<Object> | Danh sách các tài liệu cũ tìm thấy khớp ngữ nghĩa. Mỗi phần tử chứa:<br>- `name` (String): Tên tài liệu cũ (VD: `01-overview.md`).<br>- `description` (String/Null): Mô tả tài liệu.<br>- `content` (String): Nội dung chi tiết tài liệu.<br>- `createdBy` (String): Người tạo/soạn thảo tài liệu. |
