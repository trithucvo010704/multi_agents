---
name: verify-frontend-task
description: Build, lint, kiểm tra browser/visual và verify Git diff của một Task Frontend trước khi bàn giao.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `taskSpec` | Markdown | Yes | Task và acceptance criteria |
| `parentRef` | String | Yes | Nhánh cha trực tiếp |
| `commands` | Object | Yes | Build/lint commands của repo |

## Outputs

| Name | Type | Description |
|---|---|---|
| `report` | Markdown | Evidence, failures và residual risks |

## Steps

1. Chạy build và lint được khai báo bởi repository.
2. Chạy browser test thủ công/automation cho UI flow của Task.
3. So sánh với screenshot/handoff nếu Task có design.
4. Kiểm tra diff với `parentRef`, file ngoài phạm vi và dữ liệu nhạy cảm.
5. Ghi rõ phần pass, chưa test và residual risk; không khai báo pass thiếu bằng chứng.

## Error Handling

| Error | Handling |
|---|---|
| Build/lint fail | Quay lại implementation |
| Không chạy được browser | Ghi blocked evidence và residual risk |
| Diff ngoài scope | Dừng bàn giao |
