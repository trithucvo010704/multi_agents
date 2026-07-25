---
name: create-epic
description: Đóng gói cuộc gọi tạo mới Epic qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tạo mới một Epic (Epic Brief) trên hệ thống với các thông tin định danh và độ ưu tiên xác định.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án (VD: `PAI`, `EZAUTO`). |
| title | String | Có | Tiêu đề Epic cần tạo mới. |
| priority | String | Có | Độ ưu tiên của Epic (VD: `HIGH`, `MEDIUM`, `LOW`, `MUST`, `SHOULD`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lina",
      "name": "create_epic",
      "body": {
        "projectKey": "{{projectKey}}",
        "title": "{{title}}",
        "priority": "{{priority}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết Epic vừa được tạo mới. Chứa các trường:<br>- `key` (String): Mã hiệu Epic trên hệ thống (VD: `EZAUTO-EPIC-19`).<br>- `title` (String): Tiêu đề Epic.<br>- `projectKey` (String): Mã hiệu dự án.<br>- `priority` (String): Độ ưu tiên của Epic.<br>- `status` (String): Trạng thái của Epic (VD: `OPEN`). |
