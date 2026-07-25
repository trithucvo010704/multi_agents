---
name: stitch-generator
description: Sinh và cập nhật giao diện trên StitchMCP, trích xuất Stitch ID, và lưu trữ kết quả lên server qua call_api.
---

## Description
Kỹ năng giúp Robin soạn thảo prompt thiết kế, lập danh sách các màn hình cần tạo, gọi StitchMCP để sinh và cập nhật giao diện dựa trên feedback của User. Khi User chốt duyệt hoàn toàn thiết kế, Robin gọi công cụ qua `local-mcp:call_api` (namespace: `robin`, name: `save_design_screen`) để lưu trữ kết quả từng màn hình lên server và tổng hợp bàn giao.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| storyKey | String | Có | Mã hiệu Story (VD: `PAI-STORY-23`). |
| stitchProjectId | String | Có | Project ID của Stitch. |
| stitchDesignSystemId | String | Có | Design System ID của Stitch. |
| chot_concept_note | Markdown | Có | Nội dung concept note đã được User chốt duyệt. |
| design_system_spec | Markdown | Có | Đặc tả Design System của repo. |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "robin",
      "name": "save_design_screen",
      "body": {
        "storyKey": "{{storyKey}}",
        "name": "{{name}}",
        "stitchProjectId": "{{stitchProjectId}}",
        "stitchScreenId": "{{stitchScreenId}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết màn hình thiết kế đã được lưu trữ thành công. Chứa các trường:<br>- `storyKey` (String): Mã User Story.<br>- `name` (String): Tên màn hình.<br>- `stitchProjectId` (String): Project ID trên Stitch.<br>- `stitchScreenId` (String): Screen ID trên Stitch. |
| screens_list | List | Danh sách các màn hình đã thiết kế và lưu server thành công, cấu trúc: `[{ "name": "tên màn hình", "stitchProjectId": "Stitch Project ID", "stitchScreenId": "Stitch Screen ID" }]`. |
