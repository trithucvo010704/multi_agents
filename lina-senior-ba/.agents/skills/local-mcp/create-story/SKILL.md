---
name: create-story
description: Đóng gói cuộc gọi tạo mới User Story qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tạo mới một User Story trên hệ thống và liên kết trực tiếp nó vào một Epic xác định.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án (VD: `PAI`, `EZAUTO`). |
| epicKey | String | Có | Mã hiệu Epic liên kết (VD: `EZAUTO-EPIC-19`). |
| title | String | Có | Tiêu đề của User Story cần tạo mới. |
| priority | String | Có | Độ ưu tiên của User Story (VD: `MUST`, `SHOULD`, `COULD`, `WONT`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "lina",
      "name": "create_story",
      "body": {
        "projectKey": "{{projectKey}}",
        "epicKey": "{{epicKey}}",
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
| data | Object | Chi tiết User Story vừa được tạo mới. Chứa các trường:<br>- `key` (String): Mã hiệu Story trên hệ thống (VD: `EZAUTO-STORY-12`).<br>- `projectKey` (String): Mã hiệu dự án.<br>- `epicKey` (String): Mã Epic liên kết.<br>- `title` (String): Tiêu đề Story.<br>- `priority` (String): Độ ưu tiên của Story.<br>- `status` (String): Trạng thái của Story (VD: `OPEN`). |
