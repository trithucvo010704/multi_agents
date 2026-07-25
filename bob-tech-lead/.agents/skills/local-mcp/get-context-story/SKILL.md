---
name: get-context-story
description: Đóng gói cuộc gọi lấy chi tiết bối cảnh Story qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để tải đầy đủ thông tin bối cảnh (User Story, Acceptance Criteria, UI/UX Specs) của một Story.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| storyKey | String | Có | Mã User Story |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "get_context_story",
      "body": {
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
| data | Object | Chi tiết bối cảnh Story và tài liệu đính kèm. Chứa các trường:<br>- `projectKey` (String): Mã hiệu dự án.<br>- `epicKey` (String): Mã hiệu Epic.<br>- `key` (String): Mã hiệu Story.<br>- `title` (String): Tiêu đề Story.<br>- `description` (String/Null): Mô tả.<br>- `deadline` (String/Null): Hạn hoàn thành.<br>- `priority` (String): Độ ưu tiên (VD: `MUST`).<br>- `status` (String): Trạng thái (VD: `OPEN`).<br>- `createdBy` (String): Người tạo.<br>- `documents` (List<Object>): Mảng tài liệu đính kèm, mỗi tệp gồm: `name`, `description`, `content`, `createdBy`.<br>- `project` (Object): Thông tin dự án.<br>- `epic` (Object): Thông tin Epic.<br>- `screens` (List<Object>/Null): Mảng màn hình thiết kế. |
