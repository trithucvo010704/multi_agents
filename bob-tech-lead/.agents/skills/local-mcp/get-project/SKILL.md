---
name: get-project
description: Đóng gói cuộc gọi lấy thông tin dự án qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để lấy thông tin chi tiết cấu hình của dự án (bao gồm danh sách repository).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "get_project",
      "body": {
        "projectKey": "{{projectKey}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết thông tin cấu hình dự án. Chứa các trường:<br>- `key` (String): Mã hiệu dự án (VD: `PAI`).<br>- `name` (String): Tên dự án.<br>- `description` (String): Mô tả dự án.<br>- `status` (String): Trạng thái (VD: `ACTIVE`).<br>- `documents` (List<Object>): Mảng tài liệu dự án, mỗi phần tử gồm: `name`, `description`, `content`, `createdBy`.<br>- `repositoryList` (List<Object>): Mảng repositories của dự án, mỗi phần tử gồm: `name`, `description`, `language`, `framework`, `hasUi`, `designSystem`. |
