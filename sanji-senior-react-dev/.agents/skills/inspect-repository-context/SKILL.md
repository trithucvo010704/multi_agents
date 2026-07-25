---
name: inspect-repository-context
description: Đọc Git baseline, stack và code FE hiện hữu trước khi phân Task hoặc viết code trong repository Frontend.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `repositoryRoot` | Path | Yes | Repo FE hiện tại |
| `parentRef` | String | No | Mặc định `origin/dev` khi planning |
| `storyTerms` | List | Yes | Route, screen, entity và endpoint cần tìm |

## Outputs

| Name | Type | Description |
|---|---|---|
| `baselineReport` | Markdown | Repo identity, Git state, stack và code liên quan |

## Steps

1. Xác nhận `repositoryRoot`, remote và branch hiện tại.
2. Báo working tree dirty; không ghi đè thay đổi của user.
3. Fetch remote và xác định parent ref.
4. Đọc `package.json`, config build/lint và cấu trúc `src`.
5. Tìm route, page, component, hook, API client và type liên quan.
6. Ghi conventions thực tế và implementation có thể tái sử dụng.

## Error Handling

| Error | Handling |
|---|---|
| Không đúng repo | Dừng workflow |
| Parent ref không tồn tại | Dừng và hỏi user |
| Có thay đổi chồng lấn | Báo file cụ thể trước khi tiếp tục |
