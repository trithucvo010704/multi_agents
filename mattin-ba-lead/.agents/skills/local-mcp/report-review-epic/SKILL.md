---
name: report-review-epic
description: Báo cáo kết quả review Epic lên hệ thống thông qua call_api.
---

## Description
Kỹ năng giúp Mattin đẩy kết quả thẩm định và báo cáo review chi tiết của Epic lên hệ thống qua `local-mcp:call_api` với namespace `mattin` và name `report_review_epic`.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| projectKey | String | Có | Mã hiệu dự án (ví dụ: `PAI`). |
| epicKey | String | Có | Mã hiệu Epic cần báo cáo (ví dụ: `PAI-EPIC-46`). |
| status | String | Có | Trạng thái thẩm định (`PASSED` hoặc `FAILED`). |
| title | String | Có | Tiêu đề của báo cáo (ví dụ: `BA Lead Review - PAI-EPIC-46`). |
| content | String | Có | Nội dung báo cáo review chi tiết chứa điểm số và các lỗi sai cần khắc phục. |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "mattin",
      "name": "report_review_epic",
      "body": {
        "projectKey": "{{projectKey}}",
        "epicKey": "{{epicKey}}",
        "status": "{{status}}",
        "title": "{{title}}",
        "content": "{{content}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Xác nhận báo cáo review Epic đã được lưu trữ trên hệ thống. Chứa các trường:<br>- `projectKey` (String): Mã dự án.<br>- `epicKey` (String): Mã Epic.<br>- `status` (String): Trạng thái review (`PASSED` hoặc `FAILED`).<br>- `title` (String): Tiêu đề báo cáo.<br>- `content` (String/Null): Nội dung báo cáo review. |
