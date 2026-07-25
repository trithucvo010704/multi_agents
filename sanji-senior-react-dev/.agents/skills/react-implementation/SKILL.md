---
name: react-implementation
description: Thực thi một Task React/TypeScript đã duyệt theo stack và conventions thực tế của repository.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `taskSpec` | Markdown | Yes | Task FE đã duyệt |
| `storyContext` | Object | Yes | Story, API và design context |
| `baselineReport` | Markdown | Yes | Kết quả inspect repository |

## Outputs

| Name | Type | Description |
|---|---|---|
| `changes` | Files | Source changes đúng phạm vi |

## Steps

1. Lập danh sách file dự kiến và đối chiếu Task boundary.
2. Tái sử dụng router, component, hook, API client và styles hiện có.
3. Triển khai loading, empty, error, forbidden và success states theo Task.
4. Dùng dependency hiện hữu; xin duyệt trước khi thêm dependency.
5. Không thay đổi API contract hoặc design handoff để hợp thức hóa code.

## Error Handling

| Error | Handling |
|---|---|
| Contract thiếu/mâu thuẫn | Dừng và báo finding |
| Cần file ngoài phạm vi | Xin Human duyệt mở rộng Task |
