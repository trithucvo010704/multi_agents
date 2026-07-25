# TOOL ACCESS FAILURE STANDARD

## Purpose

Áp dụng cho mọi Agent khi workflow cần tool, MCP server, resource, connector hoặc filesystem capability nhưng capability đó không gọi được.

## Rules

1. Xác nhận tên tool/resource và server/capability dự kiến.
2. Nếu timeout hoặc lỗi kết nối tạm thời, retry tối đa 2 lần.
3. Không retry khi lỗi permission, validation, tool không tồn tại hoặc resource không tồn tại.
4. Không bịa tool, tham số, response hoặc kết quả đồng bộ.
5. Chỉ dùng local fallback khi workflow/skill cho phép rõ và nguồn local được xác định duy nhất.
6. Local fallback cho thao tác đọc không đồng nghĩa MCP đã hoạt động.
7. Ghi local khi MCP write/upload lỗi không được báo là đã đồng bộ.
8. Nếu capability bắt buộc vẫn thiếu, dừng workflow trước mọi thay đổi phụ thuộc capability đó.

## Status

- `BLOCKED_TOOL_NOT_AVAILABLE`: Tool không xuất hiện trong session.
- `BLOCKED_TOOL_NOT_CONNECTED`: Server/connector chưa kết nối.
- `BLOCKED_TOOL_PERMISSION`: Tool/resource trả permission denied, `401` hoặc `403`.
- `BLOCKED_TOOL_TIMEOUT`: Retry 2 lần vẫn timeout.
- `BLOCKED_RESOURCE_NOT_FOUND`: Resource/URI không tồn tại.
- `BLOCKED_LOCAL_ACCESS`: Không đọc/ghi được local path cần thiết.
- `BLOCKED_TOOL_NOT_IMPLEMENTED`: Có yêu cầu nghiệp vụ nhưng không có tool thực hỗ trợ.
- `BLOCKED_TOOL_INPUT`: Thiếu tham số bắt buộc hoặc input mơ hồ.

## Required Report

```text
STATUS: BLOCKED_<REASON>
AGENT: <agent>
WORKFLOW: <workflow>
REQUIRED_TOOL_OR_RESOURCE: <exact name/URI/capability>
EXPECTED_SERVER_OR_PROVIDER: <server/provider or UNKNOWN>
ATTEMPTED_ACTIONS:
- <attempt>
FAILURE_EVIDENCE:
- <error without secrets>
LOCAL_FALLBACK: AVAILABLE | NOT_AVAILABLE | NOT_ALLOWED
USER_ACTION_REQUIRED:
- <connect/grant/provide/clarify/implement action>
CHANGES_MADE: NONE | <exact safe local changes made before block>
SYNC_STATUS: NOT_ATTEMPTED | FAILED | LOCAL_ONLY
```

Không đưa token, secret, connection string hoặc credential vào báo cáo.
