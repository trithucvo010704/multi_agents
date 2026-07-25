---
name: cross-repository-task-audit
description: Audit Backend and Frontend Tasks for an Epic using approved documents and origin/dev code baselines without changing documents or code.
---

# Cross-Repository Task Audit

## Purpose

Xác định các Task Backend và Frontend của một Epic có:

- bao phủ đầy đủ Story đã duyệt;
- khớp API contract và UI handoff;
- đúng ownership và dependency order;
- phù hợp code đã tồn tại trên baseline của từng repo;
- có kích thước phù hợp với loại repo.

Skill này chỉ đọc.

## Required Inputs

Phải resolve đủ:

1. Epic Brief.
2. Toàn bộ Story đã duyệt trong phạm vi audit.
3. Backend và Frontend Task Specs hiện có.
4. API specification và Detailed API liên quan.
5. Concept Note, Stitch screen hoặc design handoff cho Story có UI.
6. `docs/project-level/story-task-branch-rules.md`.
7. Backend repository và baseline `origin/dev`.
8. Frontend repository và baseline `origin/dev`.
9. Guideline áp dụng từ MCP hoặc local guideline fallback đã cấu hình.

Thiếu hoặc không đọc được nguồn bắt buộc thì trả `BLOCKED`.
Không suy diễn contract bị thiếu và không tự tạo tài liệu thay thế.

## Baseline Inspection

Với từng repository:

1. Giữ nguyên worktree hiện tại, không ghi đè local changes.
2. Fetch remote references khi được phép.
3. Đọc `origin/dev` làm planning baseline.
4. Tìm implementation liên quan tới Story, endpoint, route, screen, component, model và shared infrastructure.
5. So sánh giả định trong Task với baseline.

Không có repository hoặc không đọc được `origin/dev` thì dừng, báo nguồn đã thử và hành động cụ thể user cần làm.

## Backend Audit Rules

Kiểm tra:

- một API Task sở hữu đúng một `Method + Endpoint`;
- không endpoint nào có nhiều Task owner;
- mọi endpoint Story yêu cầu đều có owner;
- entity, migration, security, configuration và foundation work dùng chung có một owner rõ ràng;
- foundation Task không bị lặp giữa các Story;
- dependency order khả thi;
- Detailed API đúng guideline và đủ để code;
- Task scope khớp cả tài liệu lẫn Backend baseline.

Không áp dụng cách gom Frontend delivery slice cho Backend API Task.

## Frontend Audit Rules

Một Frontend Task là một delivery slice gắn với một user outcome thống nhất.

Một Task hợp lệ có thể bao gồm:

- page hoặc route;
- modal, drawer hoặc dialog thuộc flow đó;
- local components và hooks hỗ trợ;
- loading, empty, validation, error và success states;
- nhiều endpoint liên quan;
- API integration và browser verification cho cùng user outcome.

Đánh dấu `TOO_SMALL` khi Task chỉ tách một component nhỏ, một API call hoặc một UI state và không thể demo, test hoặc bàn giao độc lập.

Đánh dấu `TOO_LARGE` khi Task gom nhiều user outcome không liên quan, route không liên quan, approval point riêng hoặc flow có thể release độc lập.

Kiểm tra thêm:

- mọi UI Story có Task coverage;
- behavior trace được tới acceptance criteria;
- UI trace được tới design handoff;
- integration trace được tới API contract;
- screen, component và flow dùng chung có một owner;
- giả định trong Task khớp Frontend baseline;
- dependency với Backend Task và Frontend foundation được nêu rõ.

Không áp dụng quy tắc một endpoint trên một Task của Backend cho Frontend.

## Required Report

Trả về:

1. Overall verdict: `READY`, `NEEDS_REVISION` hoặc `BLOCKED`.
2. Verdict cho từng Story.
3. Story coverage matrix.
4. Endpoint ownership matrix.
5. Frontend delivery-slice matrix.
6. Foundation/shared ownership findings.
7. Dependency-order findings.
8. Detailed API completeness findings.
9. Documentation-versus-code conflicts.
10. Required revisions theo severity.

Mỗi finding phải có severity, repository, Story/Task ID, evidence, rule bị vi phạm và correction ngắn gọn.

Không sửa bất kỳ file hay trạng thái nào.

## Blocked Response

```text
STATUS: BLOCKED
MISSING_OR_CONFLICT:
- ...
ATTEMPTED_SOURCES:
- ...
USER_ACTION_REQUIRED:
- ...
CHANGES_MADE: NONE
```
