---
name: create-api-spec
description: Tạo hoặc cập nhật Detailed API từ Story contract và code thực tế khi phân Task hoặc hoàn tất một Backend API Task.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `projectRoot` | Path | Yes | Project Workspace |
| `epicKey` | String | Yes | Epic key |
| `storyKey` | String | Yes | Story key |
| `surface` | String | Yes | Ví dụ `cms` |
| `endpoint` | String | Yes | `METHOD /path` |
| `storyApiSpec` | Markdown | Yes | Contract tại Story |
| `implementationEvidence` | Object | No | Controller/DTO/validation/error thực tế |

## Outputs

| Name | Type | Description |
|---|---|---|
| `detailedApiPath` | Path | File dưới `docs/api-detail` |
| `content` | Markdown | Detailed API theo guideline |

## Steps

1. Đọc chính xác `guideline://TASK_BE/detailed-api-spec.md`.
2. Nếu MCP không khả dụng, đọc chính xác `<GUIDELINES_ROOT>/TASK_BE/detailed-api-spec.md`.
3. Nếu cả hai không đọc được, trả `BLOCKED_GUIDELINE_UNAVAILABLE`; không dùng template tự suy đoán.
4. Xác định duy nhất `<projectRoot>/docs/api-detail/<surface>/<epicKey>/<storyKey>/<nn>-<method>-<slug>.md`; thiếu thành phần nào thì trả `BLOCKED_OUTPUT_PATH`.
5. Đối chiếu endpoint với `storyApiSpec`; endpoint ngoài Story hoặc owner conflict thì dừng.
6. Giữ đầy đủ sections, bảng field, flatten convention, examples và error format của guideline.
7. Planning ghi `Status: DRAFT` và `Implementation verification: PENDING`.
8. Chỉ sau khi kiểm chứng code mới ghi `Status: VERIFIED`, commit và evidence.
9. Đồng bộ qua MCP nếu khả dụng; local artifact vẫn bắt buộc.

## Error Handling

| Error | Handling |
|---|---|
| Story contract và code mâu thuẫn | Dừng, báo source cần Human chốt |
| Trùng endpoint owner | Không ghi đè; báo ownership conflict |
| MCP lỗi | Giữ local artifact và báo trạng thái chưa đồng bộ |
| Không xác định output path | Dừng và yêu cầu path components |
| Không đọc được guideline | Dừng và yêu cầu MCP Resource hoặc GUIDELINES_ROOT |
