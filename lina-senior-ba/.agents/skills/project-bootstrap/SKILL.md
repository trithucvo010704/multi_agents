---
name: project-bootstrap
description: Tạo cấu trúc Project Workspace tối thiểu sau khi Project Charter đã được Human duyệt.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `workspaceRoot` | Path | Yes | Thư mục project mới |
| `projectKey` | String | Yes | Mã project đã duyệt |
| `projectName` | String | Yes | Tên project |

## Outputs

| Name | Type | Description |
|---|---|---|
| `workspace` | Directory | Workspace tối thiểu |

## Steps

1. Xác nhận target không ghi đè project hiện hữu.
2. Tạo `docs/project-level`, `docs/epic` và `stitch-screens`.
3. Tạo `overview.md` từ guideline PROJECT; không bịa nội dung chưa chốt.
4. Báo các repository dự kiến nhưng không tự tạo source repository.

## Error Handling

| Error | Handling |
|---|---|
| Target đã có dữ liệu | Dừng và xin hướng xử lý |
| Thiếu Project Charter | Quay lại Q&A |
