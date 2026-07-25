---
name: fetch-guideline
description: Đọc guideline bắt buộc từ MCP Resource hoặc GUIDELINES_ROOT khi Lina chuẩn bị viết Project, Epic hay Story document.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `level` | String | Yes | `PROJECT`, `EPIC` hoặc `STORY` |
| `name` | String | Yes | Tên file guideline |
| `guidelinesRoot` | Path | No | Fallback local, thường lấy từ `GUIDELINES_ROOT` |

## Outputs

| Name | Type | Description |
|---|---|---|
| `content` | Markdown | Guideline chính thức |
| `source` | String | MCP URI hoặc local path đã dùng |

## Steps

1. Đọc `guideline://<LEVEL>/<name>` bằng `read_resource` nếu MCP khả dụng.
2. Nếu MCP không khả dụng, đọc `<GUIDELINES_ROOT>/<LEVEL>/<name>`.
3. Ghi nhận nguồn đã dùng trong báo cáo.
4. Dừng và hỏi user nếu cả hai nguồn đều không tồn tại.

## Error Handling

| Error | Handling |
|---|---|
| MCP timeout | Retry tối đa 2 lần rồi dùng local fallback |
| Local fallback thiếu | Dừng; không tự tạo template thay thế |
