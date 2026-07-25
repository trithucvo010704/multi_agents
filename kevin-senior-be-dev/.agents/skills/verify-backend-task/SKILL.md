---
name: verify-backend-task
description: Build, test, kiểm tra API contract, secrets và Git diff của một Task Backend trước khi bàn giao.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `taskSpec` | Markdown | Yes | Task và acceptance criteria |
| `parentRef` | String | Yes | Nhánh cha trực tiếp |
| `commands` | Object | Yes | Build/test commands của repo |

## Outputs

| Name | Type | Description |
|---|---|---|
| `report` | Markdown | Evidence, failures và residual risks |

## Steps

1. Chạy build và test hiện có theo project policy.
2. Kiểm tra validation, auth, success và error behavior của endpoint.
3. So sánh implementation với Story API contract và Detailed API.
4. Kiểm tra diff với parent, file ngoài phạm vi, secret và local properties.
5. Kiểm tra số commit riêng của Task khi branch đã tồn tại.
6. Ghi rõ phần pass, chưa test và residual risk.

## Error Handling

| Error | Handling |
|---|---|
| Build/test fail | Quay lại implementation |
| Contract mismatch | Dừng bàn giao và cập nhật đúng source of truth |
| Diff ngoài scope/secret | Dừng bàn giao |
