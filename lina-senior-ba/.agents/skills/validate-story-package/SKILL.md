---
name: validate-story-package
description: Audit Brief và các Story để phát hiện thiếu Story, trùng phạm vi, trùng API owner hoặc tài liệu không nhất quán trước khi phân Task.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `brief` | Markdown | Yes | Epic Brief |
| `stories` | List<Files> | Yes | Các Story Package |

## Outputs

| Name | Type | Description |
|---|---|---|
| `report` | Markdown | Findings và quyết định cần Human chốt |
| `valid` | Boolean | Có đủ điều kiện chuyển sang Task hay không |

## Steps

1. So sánh danh sách Story trong Brief với thư mục Story thực tế.
2. Kiểm tra actor, scope, acceptance criteria và out-of-scope.
3. Lập registry `Method + Endpoint → Story owner`.
4. Đánh dấu endpoint có nhiều Story cùng sở hữu.
5. Kiểm tra API field, data dictionary và DB design có cùng thuật ngữ.
6. Trả `valid = false` nếu còn mâu thuẫn ảnh hưởng Task ownership.

## Error Handling

| Error | Handling |
|---|---|
| Thiếu file bắt buộc | Ghi finding và dừng bàn giao Task |
| Hai source of truth mâu thuẫn | Yêu cầu Human chọn; không tự sửa |
