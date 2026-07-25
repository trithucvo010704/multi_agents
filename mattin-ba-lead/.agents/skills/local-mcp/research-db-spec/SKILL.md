---
name: research-db-spec
description: Tìm kiếm thiết kế database hoặc đặc tả bảng dữ liệu theo ngữ nghĩa gần đúng nhất qua call_api.
---

## Description
Sử dụng công cụ tìm kiếm ngữ nghĩa để tra cứu các tài liệu DB Spec hoặc cấu trúc bảng dữ liệu cũ của một dự án cụ thể trên hệ thống, giúp đối chiếu chéo cấu trúc dữ liệu chính xác và khớp nhất.

## Inputs
| Tên | Kiểu | Bắt buộc | Mô tả |
|-----|------|----------|-------|
| projectKey | String | Có | Mã hiệu duy nhất của dự án trên hệ thống (VD: `PAI`). |
| query | String | Có | Câu truy vấn tìm kiếm cấu trúc DB (VD: `bảng user`, `gói cước môi giới`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "mattin",
      "name": "research_db_table_spec",
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
| data | List<Object> | Danh sách các kết quả tìm kiếm cấu trúc bảng DB khớp ngữ nghĩa. Mỗi phần tử chứa:<br>- `name` (String): Tên tệp đặc tả DB/bảng (VD: `db-design.md`).<br>- `description` (String/Null): Mô tả tệp.<br>- `content` (String): Nội dung đặc tả cấu trúc bảng/DB.<br>- `createdBy` (String): Người tạo. |
