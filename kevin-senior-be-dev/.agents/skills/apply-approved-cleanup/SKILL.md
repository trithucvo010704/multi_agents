---
name: apply-approved-cleanup
description: Áp dụng đúng các cleanup item đã được Human duyệt trong Backend repository và verify không đổi behavior; dùng sau audit khi user phê duyệt rõ CLEANUP-ID cụ thể.
---

# Apply Approved Cleanup

## Required Inputs

- Cleanup Proposal hoặc path xác định duy nhất.
- `CLEANUP-ID` được Human duyệt.
- Repository root, baseline/parent và validation commands.

Thiếu một input thì dừng; không suy đoán.

## Procedure

1. Xác nhận proposal/approval cùng repository và baseline.
2. Bảo toàn local changes.
3. Revalidate reference và dynamic usage từng item.
4. Chỉ áp dụng approved item; không tự thêm.
5. Không đổi business logic, API/DTO, transaction, validation, DB/migration, security, Spring wiring, serialization, scheduler, Kafka/Redis, integration, architecture, Story/Task docs hoặc workflow breakout/brainstorm.
6. Build/test theo policy, verify diff với parent và quét secret/local properties.
7. Không commit, push, merge hoặc đổi status.

Trả `CLEANUP_APPLIED`, `CLEANUP_PARTIAL` hoặc `BLOCKED_*` cùng approved/applied/skipped items, verification, diff và changes made.

Nếu build/test fail, không dùng `git reset`; chỉ hoàn tác phần workflow vừa tạo khi xác định an toàn và báo đầy đủ.
