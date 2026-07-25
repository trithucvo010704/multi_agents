---
name: plan-frontend-delivery-slice
description: Gom Story FE thành Task theo user outcome hoàn chỉnh, tránh tách quá nhỏ theo component, API call hoặc UI state.
---

## Inputs

| Name | Type | Required | Description |
|---|---|---|---|
| `storyContext` | Object | Yes | Story, user flow, API và design handoff |
| `baselineReport` | Markdown | Yes | Code FE hiện có |

## Outputs

| Name | Type | Description |
|---|---|---|
| `deliverySlices` | List | Task FE bàn giao/kiểm thử độc lập |

## Phase 1: Propose

1. Xác định user outcome chính.
2. Gom page, modal/drawer, components, UI states và API calls cùng phục vụ outcome vào một Task.
3. Cho phép nhiều endpoint trong một Task nếu thuộc cùng UI flow.
4. Không tách riêng loading/error state, component nhỏ, hook hoặc API call.
5. Chỉ tách khi flow/route độc lập, dependency riêng, ownership khác hoặc diff quá lớn để review.
6. Loại phần đã có đầy đủ trên `origin/dev`.
7. Ghi outcome, scope, APIs, states, dependencies, exclusions và DoD.
8. Trình output path dự kiến cho từng Task.
9. Trả `STATUS: WAITING_FOR_TASK_PLAN_APPROVAL` và `CHANGES_MADE: NONE`.

Không ghi file trong Phase 1.

## Phase 2: Write Approved Proposal

Chỉ chạy khi user duyệt rõ proposal đang có trong hội thoại và proposal vẫn cùng Epic/US.

1. Không thêm, bớt, gộp hoặc đổi ownership so với proposal đã duyệt.
2. Ghi `task-spec.md` đúng TASK_FE guideline dưới đúng Story.
3. Ghi Story/design/API references, parent/dependencies, included/excluded scope, expected files, UI states, verification và approval state.
4. Không tạo Detailed API phía FE.
5. Không code, tạo branch, push hoặc đổi `DONE`.

## Quality Heuristics

- Task phải demo hoặc nghiệm thu độc lập.
- Page và modal hỗ trợ trực tiếp thường nằm cùng Task.
- Shared component chỉ là Task riêng khi dùng xuyên nhiều Story và đủ lớn.
- Không áp quy tắc một endpoint/một Task của Backend cho Frontend.

## Error Handling

| Error | Handling |
|---|---|
| User outcome chưa rõ | `BLOCKED_CONTEXT_CONFLICT` |
| Thiếu design/API bắt buộc | `BLOCKED_MISSING_INPUT`; không suy đoán |
| Không biết nơi ghi hoặc proposal khác US | `BLOCKED_OUTPUT_PATH` hoặc `BLOCKED_SCOPE`; hỏi user |
| Chưa duyệt proposal | Không ghi file; trả `WAITING_FOR_TASK_PLAN_APPROVAL` |
