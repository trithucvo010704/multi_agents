---
name: get-stitch-config-spec
description: Gọi mcp tool `get_stitch_config` qua call_api để lấy cấu hình Stitch (`stitchProjectId`, `stitchDesignSystemId`) của repository.
---

## Description
Kỹ năng giúp Robin tải thông tin Project ID và Design System ID của Stitch tương ứng với repository UI của dự án thông qua `local-mcp:call_api` (namespace: `robin`, name: `get_stitch_config`). Chuỗi văn bản cấu hình trả về trong `data.content` sẽ được phân tích để trích xuất `stitchProjectId` và `stitchDesignSystemId`.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| projectKey | String | Có | Mã hiệu dự án (VD: `PAI`). |
| name | String | Có | Tên repository (VD: `pwa-client`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "robin",
      "name": "get_stitch_config",
      "body": {
        "projectKey": "{{projectKey}}",
        "name": "{{name}}"
      }
    }
  }
  ```

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết cấu hình Stitch. Chứa các trường:<br>- `name` (String): Tên tệp tin (thường là `STITCH.md`).<br>- `description` (String/Null): Mô tả.<br>- `content` (String): Nội dung cấu hình chứa thông tin Project ID và Design System ID dạng text.<br>- `createdBy` (String): Người tạo.<br><br>**Quy tắc phân tích `data.content`:**<br>- Tìm kiếm chuỗi `# PROJECT ID: [ID]` để lấy **`stitchProjectId`** (VD: `3753968417100338700`).<br>- Tìm kiếm chuỗi `# DESIGN SYSTEM ID: [ID]` để lấy **`stitchDesignSystemId`** (VD: `asset/5b08bb9a94a244b0a8d3ab8e67fa934d`). |
| stitchProjectId | String | Project ID của Stitch dành cho repo UI được chọn (đã được trích xuất). |
| stitchDesignSystemId | String | Design System ID của Stitch dành cho repo UI được chọn (đã được trích xuất). |
