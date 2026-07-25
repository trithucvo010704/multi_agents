---
name: get-story-context
description: Gọi mcp tool `get_story_design_context` qua call_api để lấy ngữ cảnh của Story và trích xuất các thông tin nghiệp vụ/kỹ thuật.
---

## Description
Kỹ năng giúp Robin truy xuất ngữ cảnh UI/UX của một Story cụ thể thông qua `local-mcp:call_api` (namespace: `robin`, name: `get_story_design_context`). Kết quả JSON trả về được phân tích để trích xuất `projectKey`, nội dung `concept_note`, tên repository thực thi (`repository_select`), cùng các tài liệu đính kèm liên quan (`user-story.md`, `user-flow.md`).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| projectKey | String | Có | Mã hiệu của dự án (VD: `PAI`, `ECOM`). |
| storyKey | String | Có | Mã hiệu của Story cần thiết kế (VD: `PAI-STORY-23`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "robin",
      "name": "get_story_design_context",
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
| data | Object | Chi tiết bối cảnh Story. Chứa các trường:<br>- `projectKey`: Mã hiệu dự án trích xuất từ payload (VD: `PAI`).<br>- `documents`: Mảng tài liệu đính kèm Story (chứa `name`, `description`, `content`) |
| concept_note | Markdown | Nội dung tài liệu concept note do BA viết. |
| repository_select | String | Tên repository được chọn để thiết kế UI (VD: `pwa-client`). |
| user_story | Markdown | Nội dung đặc tả yêu cầu và Acceptance Criteria của Story. |
| user_flow | Markdown | Nội dung sơ đồ luồng điều hướng của người dùng. |
