---
name: verify-project
description: Xác thực sự tồn tại của dự án trên hệ thống thông qua call_api.
---

## Description
Kỹ năng giúp Lux kiểm tra xem mã hiệu dự án (`projectKey`) do User cung cấp có tồn tại trong danh sách dự án của hệ thống hay không trước khi bắt đầu bất kỳ quy trình xử lý tài liệu nào.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| projectKey | String | Có | Mã hiệu duy nhất của dự án cần xác thực (VD: `ECOM`, `PAI`). |

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
| data | List<Object> | Danh sách các dự án trên hệ thống. Mỗi phần tử chứa:<br>- `key` (String): Mã hiệu dự án (VD: `PAI`, `EZAUTO`).<br>- `name` (String): Tên dự án.<br>- `description` (String): Mô tả dự án.<br>- `status` (String): Trạng thái hoạt động (VD: `ACTIVE`). |
| is_valid | Boolean | Trả về `true` nếu dự án có tồn tại trong danh sách, ngược lại trả về `false`. |
