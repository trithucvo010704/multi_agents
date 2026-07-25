---
name: inspect-repository-context
description: Đọc Git baseline, build stack và code Backend hiện hữu trước khi phân Task hoặc viết code.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `repositoryRoot` | Path | Yes | Repo Backend hiện tại |
| `parentRef` | String | No | Mặc định `origin/dev` khi planning |
| `storyTerms` | List | Yes | Endpoint, entity và nghiệp vụ cần tìm |

## Outputs

| Name | Type | Description |
|---|---|---|
| `baselineReport` | Markdown | Repo identity, Git state, stack và code liên quan |

## Steps

1. Xác nhận repo, remote, branch và working tree; bảo toàn thay đổi của user.
2. Fetch remote và xác định parent ref.
3. Đọc build file, application structure và repository conventions.
4. Tìm controller, service, repository, DTO, mapper, entity, migration và config liên quan.
5. Xác định implementation đã có, phần thiếu và sensitive impact.

## Error Handling

| Error | Handling |
|---|---|
| Không đúng repo/parent | Dừng workflow |
| Thay đổi local chồng lấn | Báo file cụ thể trước khi tiếp tục |
