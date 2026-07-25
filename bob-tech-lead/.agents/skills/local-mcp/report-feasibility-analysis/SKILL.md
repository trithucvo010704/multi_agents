---
name: report-feasibility-analysis
description: Đóng gói cuộc gọi gửi báo cáo phân tích khả thi qua local-mcp:call_api.
---

## Description
Kỹ năng này đóng gói cuộc gọi qua `local-mcp:call_api` để gửi báo cáo phân tích khả thi (Feasibility Analysis) của một Story lên hệ thống.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả |
|-----|--------------|----------|-------|
| projectKey | String | Có | Mã dự án |
| storyKey | String | Có | Mã User Story |
| status | String | Có | Trạng thái đánh giá khả thi (ví dụ: `FEASIBLE`, `NOT_FEASIBLE`) |
| title | String | Có | Tiêu đề báo cáo khả thi |
| content | String | Có | Nội dung báo cáo phân tích khả thi dưới dạng Markdown |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "bob",
      "name": "report_feasibility_analysis",
      "body": {
        "projectKey": "{{projectKey}}",
        "storyKey": "{{storyKey}}",
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
| data | Object | Xác nhận báo cáo đã được lưu trữ trên hệ thống. Chứa các trường:<br>- `projectKey` (String): Mã dự án.<br>- `storyKey` (String): Mã User Story.<br>- `status` (String): Trạng thái đánh giá khả thi.<br>- `title` (String): Tiêu đề báo cáo.<br>- `content` (String/Null): Nội dung báo cáo. |
