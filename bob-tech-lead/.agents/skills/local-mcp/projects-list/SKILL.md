---
name: projects-list
description: Đóng gói cuộc gọi lấy danh sách dự án hiện có trên hệ thống qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để lấy danh sách toàn bộ các dự án nhằm phục vụ việc xác thực và tra cứu.

## Inputs
Không có tham số đầu vào.

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lux",
      "name": "projects_list",
      "body": {}
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | List<Object> | Danh sách các dự án trên hệ thống. Mỗi phần tử chứa:<br>- `key` (String): Mã hiệu dự án (VD: `PAI`, `EZAUTO`).<br>- `name` (String): Tên dự án.<br>- `description` (String): Mô tả ngắn của dự án.<br>- `status` (String): Trạng thái dự án (VD: `ACTIVE`). |
