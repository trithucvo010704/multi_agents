---
name: get-design-system-spec
description: Gọi mcp tool `get_design_system` qua call_api để lấy đặc tả Design System tương ứng của repository UI.
---

## Description
Kỹ năng giúp Robin tải tài liệu đặc tả Design System (colors, typography, components, rules) tương ứng với repository UI được chọn của dự án thông qua `local-mcp:call_api` (namespace: `robin`, name: `get_design_system`).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| projectKey | String | Có | Mã hiệu của dự án (VD: `PAI`). |
| name | String | Có | Tên repository (chính là `repository_select`, VD: `pwa-client`). |

## Tool Invocation Details
- **Server Name:** `local-mcp`
- **Tool Name:** `call_api`
- **Payload Structure:**
  ```json
  {
    "param": {
      "namespace": "robin",
      "name": "get_design_system",
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
| data | Object | Chi tiết cấu hình Design System của Repository. Chứa trường `content` (nội dung Markdown của Design System). |
| design_system_spec | Markdown | Đặc tả Design System chi tiết của repository (trích xuất từ `data.content`). |
