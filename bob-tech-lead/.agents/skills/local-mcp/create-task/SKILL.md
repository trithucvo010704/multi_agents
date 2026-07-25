---
name: create-task
description: Đóng gói cuộc gọi tạo Task trên DB hệ thống qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tạo một Task kỹ thuật mới trên DB, đồng thời gán với một Story và một Repository tương ứng.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |
| storyKey | String | Có | Mã User Story |
| title | String | Có | Tiêu đề của Task |
| priority | String | Có | Mức độ ưu tiên (ví dụ: CRITICAL, HIGH, MEDIUM, LOW) |
| repositoryName | String | Có | Tên repository thực hiện task |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "create_task",
      "body": {
        "projectKey": "{{projectKey}}",
        "storyKey": "{{storyKey}}",
        "title": "{{title}}",
        "priority": "{{priority}}",
        "repositoryName": "{{repositoryName}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết thông tin Task vừa được tạo mới. Chứa các trường:<br>- `key` (String): Mã hiệu Task vừa tạo (VD: `EZAUTO-TASK-13`).<br>- `title` (String): Tiêu đề Task.<br>- `projectKey` (String/Null): Mã dự án.<br>- `storyKey` (String/Null): Mã User Story.<br>- `documents` (List<Object>/Null): Mảng tài liệu của Task.<br>- `story` (Object/Null): Thông tin Story của Task. |
