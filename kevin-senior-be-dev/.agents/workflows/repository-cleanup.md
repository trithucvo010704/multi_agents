# Workflow: Audit and Apply Safe Repository Cleanup

## Trigger

- Audit code/config/dependency dư thừa.
- Áp dụng Cleanup Proposal đã được Human duyệt.

Không dùng workflow này để breakout Story/Task, brainstorm hoặc refactor logic.

## Required Skills

1. `inspect-repository-context`
2. `audit-repository-cleanup`
3. `apply-approved-cleanup` — chỉ sau approval

## Flow

1. Resolve repository root, scope, baseline và report output.
2. Nếu cần lưu report nhưng không biết path, trả `BLOCKED_OUTPUT_PATH`.
3. Đọc CODE_REVIEW, CODING, ARCHITECTURE, QA và SAFETY guidelines qua MCP/local fallback.
4. Fetch/read baseline; bảo toàn dirty worktree.
5. Audit only và trình proposal có `CLEANUP-ID`; không sửa file.
6. Không có candidate thì báo `NO_CLEANUP_CANDIDATES`.
7. Chờ Human duyệt exact item IDs.
8. Revalidate rồi chỉ áp dụng approved items.
9. Build/test/verify diff và báo cáo; không commit/push/merge.

## Boundary

Không đổi business logic, API/DTO behavior, transaction, validation, DB/migration, security, Spring wiring, serialization, scheduler, Kafka/Redis, integration, architecture hoặc Task/Story docs. Rủi ro không loại trừ được thì `BLOCKED_LOGIC_RISK`.

## Blocked Response

```text
STATUS: BLOCKED_<REASON>
WORKFLOW: REPOSITORY_CLEANUP
MISSING_OR_CONFLICT:
ATTEMPTED_SOURCES:
USER_ACTION_REQUIRED:
CHANGES_MADE: NONE
```
