---
name: write-story-specs
description: Viết Story Package theo impact thực tế sau khi Epic Brief được Human duyệt.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `epicBrief` | Markdown | Yes | Epic Brief đã duyệt |
| `storyScope` | Object | Yes | Mục tiêu, actor, flow và acceptance criteria |
| `impacts` | Object | Yes | Cờ `ui`, `api`, `data`, `database` |
| `guidelines` | Map | Yes | Guideline cho từng file cần sinh |

## Outputs

| Name | Type | Description |
|---|---|---|
| `storyPackage` | Files | Bộ tài liệu Story theo impact |

## Steps

1. Luôn viết `user-story.md` và `user-flow.md`.
2. Viết `concept_note.md` chỉ khi `impacts.ui = true`.
3. Viết `api-spec.md` chỉ khi `impacts.api = true`.
4. Viết `data-dictionary.md` chỉ khi `impacts.data = true`.
5. Viết `db_design.md` chỉ khi `impacts.database = true`.
6. Ghi repository impact nhưng không phân Task kỹ thuật.
7. Đối chiếu tên trường, rule và acceptance criteria giữa mọi file.

## Error Handling

| Error | Handling |
|---|---|
| Brief chưa duyệt | Dừng workflow |
| Impact chưa rõ | Hỏi tối đa 5 câu trong một lượt |
| Tài liệu mâu thuẫn | Báo delta; không tự chọn source of truth |
