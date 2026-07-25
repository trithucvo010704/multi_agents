---
name: plan-backend-story-tasks
description: Lập proposal và sinh Backend API/Foundation Task cho đúng một EZAUTO Story; dùng khi user yêu cầu phân rã một US thành Backend Tasks và phải chờ Human duyệt proposal trước khi ghi tài liệu.
---

# Plan Backend Story Tasks

## Inputs

- Một Epic ID và một Story ID duy nhất.
- Story context đã duyệt.
- API contract và database impact liên quan.
- `origin/dev` baseline report.
- TASK_BE guidelines và branch rules.
- Task/Detailed API output paths đã resolve duy nhất.

## Phase 1: Propose

1. Xác nhận yêu cầu chỉ bao phủ đúng một US.
2. Lập registry `Method + Endpoint → owner`.
3. Tạo một API Task proposal cho mỗi endpoint.
4. Tạo Foundation Task proposal chỉ khi phần dùng chung không thuộc riêng một endpoint.
5. Không tạo Task cho implementation đã tồn tại đầy đủ trên `origin/dev`; báo evidence.
6. Với mỗi Task, trình proposed key/title, Story owner, endpoint/foundation scope, objective, repository, parent/dependencies, sensitive impact, expected files và output paths.
7. Trả `STATUS: WAITING_FOR_TASK_PLAN_APPROVAL` và `CHANGES_MADE: NONE`.

Không ghi file trong Phase 1.

## Phase 2: Write Approved Proposal

Chỉ chạy khi user phê duyệt rõ proposal đang có trong hội thoại và proposal vẫn cùng Epic/US.

1. Không thêm, bớt, gộp hoặc đổi ownership so với proposal đã duyệt.
2. Ghi mỗi `task-spec.md` đúng TASK_BE guideline.
3. Task Spec phải tham chiếu Story/API/Detailed API, ghi parent ref, dependencies, allowed/forbidden scope, implementation direction, validation/auth/error/transaction, verification và approval state.
4. Dùng `create-api-spec` ghi Detailed API `DRAFT/PENDING` cho từng API Task.
5. Không tạo Detailed API cho Foundation Task không sở hữu endpoint.
6. Không code, tạo branch, push hoặc đổi trạng thái `DONE`.

## Stop Conditions

Trả `BLOCKED_*` và hỏi user nếu không xác định duy nhất Epic/US hoặc output path; thiếu guideline, contract, approval hay baseline; ownership chưa rõ; proposal được duyệt không có trong context/khác US; hoặc tài liệu mâu thuẫn baseline.
