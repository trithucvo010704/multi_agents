---
name: update-task-status
description: Đóng gói cuộc gọi cập nhật trạng thái Task qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để cập nhật trạng thái của Task (ví dụ: IN_PROGRESS, DONE) trên hệ thống.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| taskKey | String | Có | Mã hiệu Task |
| status | String | Có | Trạng thái cần cập nhật |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "kevin",
      "name": "update_task_status",
      "body": {
        "taskKey": "{{taskKey}}",
        "status": "{{status}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết thông tin Task sau khi cập nhật trạng thái. Chứa các trường:<br>- `key` (String): Mã hiệu Task (VD: `EZAUTO-TASK-13`).<br>- `status` (String): Trạng thái mới của Task (VD: `IN_PROGRESS`, `DONE`). |
