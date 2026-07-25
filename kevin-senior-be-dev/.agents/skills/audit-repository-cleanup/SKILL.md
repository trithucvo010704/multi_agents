---
name: audit-repository-cleanup
description: Quét Backend repository để tìm code, dependency và cấu hình có thể dư thừa mà không thay đổi file; dùng khi user yêu cầu audit, cleanup proposal, tìm dead code hoặc cấu hình không còn sử dụng.
---

# Audit Repository Cleanup

## Required Inputs

- Backend repository root xác định duy nhất.
- Baseline ref đọc được; mặc định `origin/dev`.
- Audit scope.
- Report output: chat, hoặc đường dẫn duy nhất nếu user yêu cầu lưu file.

Thiếu repository, baseline, scope bắt buộc hoặc report path được yêu cầu thì dừng và hỏi user.

## Procedure

1. Xác nhận repository, branch, remote và dirty worktree.
2. Fetch và đọc baseline; bảo toàn local changes.
3. Đọc build files, conventions và guidelines.
4. Tìm unused import/private code, duplicate/unreachable code, unused Spring config/property, dependency không dùng, obsolete flag và misplaced artifact.
5. Kiểm tra dynamic usage qua Spring wiring, config binding, reflection, serialization, JPA, MapStruct, Lombok, profiles, scheduler, Kafka, Redis, security, tests, resources, scripts, docs và build plugins.
6. Không đủ bằng chứng thì đánh dấu `REVIEW_REQUIRED`; không đề xuất xóa an toàn.
7. Không sửa file trong audit phase.

## Proposal

Mỗi finding ghi `CLEANUP-ID`, classification, path/symbol, evidence, runtime risk, proposed change, behavior guarantee và validation commands.

Trả `WAITING_FOR_CLEANUP_APPROVAL` cùng `CHANGES_MADE: NONE`.

Nếu không có candidate, trả `NO_CLEANUP_CANDIDATES`, scope đã quét, evidence và `CHANGES_MADE: NONE`.

Thiếu path/ref/guideline/source hoặc có worktree conflict thì trả `BLOCKED_*`, `ATTEMPTED_SOURCES`, `USER_ACTION_REQUIRED`, `CHANGES_MADE: NONE`.
