---
name: research-api-spec
description: Tìm kiếm đặc tả API theo ngữ nghĩa gần đúng nhất qua call_api.
---

## Description
Sử dụng công cụ tìm kiếm ngữ nghĩa để tra cứu các tài liệu API Spec hoặc giao ước API cũ của một dự án cụ thể trên hệ thống, giúp đối chiếu chéo giao ước truyền nhận dữ liệu chính xác và khớp nhất.

## Inputs
| Tên | Kiểu | Bắt buộc | Mô tả |
|-----|------|----------|-------|
| projectKey | String | Có | Mã hiệu duy nhất của dự án trên hệ thống (VD: `PAI`). |
| query | String | Có | Câu truy vấn tìm kiếm API (VD: `API đăng nhập`, `Kafka sync user`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "mattin",
      "name": "research_api_spec",
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
| data | List<Object> | Danh sách các kết quả tìm kiếm API Spec khớp ngữ nghĩa. Mỗi phần tử chứa:<br>- `name` (String): Tên tệp tin đặc tả API.<br>- `description` (String/Null): Mô tả đặc tả.<br>- `content` (String): Nội dung chi tiết của đặc tả API.<br>- `createdBy` (String): Người tạo/đăng ký. |
