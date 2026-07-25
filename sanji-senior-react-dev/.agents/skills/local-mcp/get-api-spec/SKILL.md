---
name: get-api-spec
description: Đóng gói cuộc gọi lấy đặc tả chi tiết của một API cụ thể qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tải nội dung tài liệu đặc tả chi tiết của một API cụ thể từ hệ thống, giúp Frontend Developer đối chiếu giao ước kết nối (API Contract).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| apiSpecKey | String | Có | Mã hiệu đặc tả API cần truy xuất (VD: `PAI-API-12`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "kevin",
      "name": "get_api_spec",
      "body": {
        "apiSpecKey": "{{apiSpecKey}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết đặc tả API. Chứa các trường:<br>- `key` (String): Mã hiệu đặc tả API trên hệ thống.<br>- `name` (String): Tên chức năng API.<br>- `endpoint` (String): Đường dẫn endpoint (VD: `POST /login`).<br>- `content` (String): Nội dung Markdown chi tiết của đặc tả API.<br>- `createdBy` (String): Người tạo. |
