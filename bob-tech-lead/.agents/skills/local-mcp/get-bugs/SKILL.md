---
name: get-bugs
description: Đóng gói cuộc gọi API lấy danh sách bug từ QC của Story qua local-mcp:call_api.
---

## Description
Kỹ năng này thực hiện cuộc gọi qua `local-mcp:call_api` để tải danh sách các báo cáo lỗi đã ghi nhận cho một Story cụ thể.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |
| storyKey | String | Có | Mã User Story |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "get_bugs",
      "body": {
        "projectKey": "{{projectKey}}",
        "storyKey": "{{storyKey}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | List<Object> | Danh sách các lỗi đã log từ QC. Mỗi phần tử chứa:<br>- `key` (String): Mã hiệu bug (VD: `BUG-01`).<br>- `title` (String): Tiêu đề lỗi.<br>- `description` (String): Mô tả chi tiết lỗi.<br>- `status` (String): Trạng thái lỗi (VD: `OPEN`, `RESOLVED`).<br>- `createdBy` (String): Người tạo/báo cáo lỗi. |
