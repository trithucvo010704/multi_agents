---
name: design-audit
description: Rà soát chéo concept_note với Design System, giải quyết xung đột với User và cập nhật lên server qua call_api.
---

## Description
Kỹ năng giúp Robin đối chiếu ý tưởng thiết kế trong `concept_note` với đặc tả Design System (`design_system_spec`). Nếu phát hiện xung đột hoặc thiếu dữ kiện, Robin sẽ phỏng vấn trực tiếp User (tối giản dưới 5 câu). Khi User đã chốt phương án và nội dung, Robin hiệu chỉnh lại tài liệu `concept_note.md` cục bộ và gọi công cụ qua `local-mcp:call_api` (namespace: `robin`, name: `edit_concept_note`) để đồng bộ lên server.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| storyKey | String | Có | Mã hiệu Story (VD: `PAI-STORY-23`). |
| concept_note | Markdown | Có | Nội dung concept note thô nhận được từ BA. |
| design_system_spec | Markdown | Có | Đặc tả Design System quy chuẩn của repo. |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "robin",
      "name": "edit_concept_note",
      "body": {
        "storyKey": "{{storyKey}}",
        "conceptNote": "{{concept_note}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Xác nhận cập nhật concept note thành công. Chứa các trường:<br>- `storyKey` (String): Mã User Story.<br>- `conceptNote` (String/Null): Nội dung concept note đã lưu trên server. |
| chot_concept_note | Markdown | Nội dung concept note hoàn chỉnh đã được User chốt duyệt và lưu local/server. |
