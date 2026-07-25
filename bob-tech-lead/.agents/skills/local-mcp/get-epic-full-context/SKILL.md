---
name: get-epic-full-context
description: Đóng gói cuộc gọi truy xuất toàn bộ ngữ cảnh của Epic bao gồm tất cả các Stories bên trong qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để lấy toàn bộ thông tin chi tiết của một Epic (bao gồm tiêu đề, trạng thái, tài liệu đính kèm) và danh sách chi tiết của tất cả các Stories thuộc Epic đó (kèm theo toàn bộ tài liệu đặc tả của từng Story). Điều này giúp Tech Lead (Bob) có cái nhìn toàn diện để phân rã task ở cấp độ Epic.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án (VD: `PAI`, `EZAUTO`). |
| epicKey | String | Có | Mã hiệu Epic trên hệ thống (VD: `EZAUTO-EPIC-19`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "get_epic_full_context",
      "body": {
        "projectKey": "{{projectKey}}",
        "epicKey": "{{epicKey}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Bối cảnh đầy đủ của Epic và danh sách Stories. Chứa các trường:<br>- `projectKey` (String): Mã hiệu dự án.<br>- `epicKey` (String): Mã hiệu Epic.<br>- `title` (String): Tiêu đề của Epic.<br>- `status` (String): Trạng thái của Epic.<br>- `documents` (Array): Mảng các tài liệu Epic (gồm `name`, `description`, `content` như `brief.md`).<br>- `stories` (Array): Mảng chi tiết toàn bộ các Stories thuộc Epic. Mỗi Story gồm:<br>&nbsp;&nbsp;* `key` (String): Mã hiệu Story.<br>&nbsp;&nbsp;* `title` (String): Tiêu đề Story.<br>&nbsp;&nbsp;* `status` (String): Trạng thái Story.<br>&nbsp;&nbsp;* `priority` (String): Độ ưu tiên.<br>&nbsp;&nbsp;* `documents` (Array): Các tài liệu đặc tả đính kèm Story (mỗi tài liệu gồm `name`, `description`, `content` như `01-story.md`, `04-api.md`...). |
