---
name: get-design-system
description: Đóng gói cuộc gọi lấy đặc tả Design System qua local-mcp:call_api.
---

## Description
Kỹ năng này thực hiện cuộc gọi qua `local-mcp:call_api` để tải tài liệu Design System của repository cụ thể thuộc dự án.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |
| name | String | Có | Tên repository (ví dụ: `web-client`, `cms-client`) |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lina",
      "name": "get_design_system",
      "body": {
        "projectKey": "{{projectKey}}",
        "name": "{{name}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết cấu hình Design System của Repository. Chứa các trường:<br>- `name` (String): Tên tệp tin đặc tả (VD: `DESIGN.md`).<br>- `description` (String/Null): Mô tả của tệp tin.<br>- `content` (String): Nội dung Markdown chứa các tokens thiết kế (colors, typography, spacing...).<br>- `createdBy` (String): Người tạo thiết kế. |
