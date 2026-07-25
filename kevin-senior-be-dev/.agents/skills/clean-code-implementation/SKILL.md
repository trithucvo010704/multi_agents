---
name: clean-code-implementation
description: Thực thi một Task Backend đã duyệt theo code baseline, conventions và test policy thực tế của repository.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `taskSpec` | Markdown | Yes | Task Backend đã duyệt |
| `storyContext` | Object | Yes | Story và API context |
| `baselineReport` | Markdown | Yes | Kết quả inspect repository |

## Outputs

| Name | Type | Description |
|---|---|---|
| `changes` | Files | Source changes đúng phạm vi |

## Steps

1. Lập danh sách file dự kiến và đối chiếu Task boundary.
2. Tái sử dụng controller/service/repository/DTO/mapper conventions hiện có.
3. Triển khai đúng một endpoint hoặc Foundation Task được duyệt.
4. Dừng trước entity, migration, config, security hoặc dependency chưa có approval.
5. Chạy test hiện có; chỉ tạo test source mới khi project policy cho phép.
6. Không sửa contract để hợp thức hóa implementation.

## Error Handling

| Error | Handling |
|---|---|
| Contract thiếu/mâu thuẫn | Dừng và báo finding |
| Cần file ngoài phạm vi | Xin Human duyệt mở rộng Task |
| Sensitive impact chưa duyệt | Trả `WAITING_FOR_HUMAN_REVIEW` |
