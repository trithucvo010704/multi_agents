---
description: Read-only audit of Backend and Frontend Tasks for one Epic against approved documents and origin/dev code baselines.
---

# Audit Epic Tasks

Use `.agents/skills/cross-repository-task-audit/SKILL.md`.

## Trigger

Khi user yêu cầu Bob audit Backend và Frontend Tasks của một Epic.

## Flow

1. Xác nhận Epic ID và Project Workspace.
2. Nạp Epic Brief, các Story đã duyệt, Task Specs, API, Detailed API, UI handoff, branch rules và guidelines.
3. Resolve Backend và Frontend repositories.
4. Giữ nguyên worktree hiện tại của cả hai repo.
5. Fetch và đọc `origin/dev` của từng repo.
6. Tìm implementation liên quan trong từng baseline.
7. Audit Backend theo `Method + Endpoint` ownership.
8. Audit Frontend theo cohesive UI delivery slice; cho phép nhiều endpoint liên quan và chống micro-task.
9. Audit Story coverage, shared foundation ownership, cross-repo dependencies, Detailed API completeness và document-versus-code consistency.
10. Trả matrices, findings và verdict.

## Stop Conditions

Trả `BLOCKED` và không thay đổi gì nếu:

- không resolve được Story hoặc contract đã duyệt;
- không resolve được guideline áp dụng;
- không đọc được repository hoặc `origin/dev`;
- chưa biết Task phải nằm ở đâu;
- có UI Task nhưng thiếu design handoff bắt buộc;
- tài liệu mâu thuẫn khiến audit không thể kết luận chắc chắn.

## Restrictions

- Không sửa tài liệu hoặc code.
- Không tạo, đổi tên hoặc xóa Task.
- Không tạo branch.
- Không push, merge hoặc đổi status.
- Không áp dụng Backend Task granularity cho Frontend Task.
