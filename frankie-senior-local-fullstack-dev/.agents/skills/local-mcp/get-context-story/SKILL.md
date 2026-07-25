---
name: get-context-story
description: Gọi mcp tool get_context_story qua call_api của local-mcp để lấy thông tin chi tiết của Story dựa trên storyKey.
---

## Description
Kỹ năng này chịu trách nhiệm truy xuất toàn bộ dữ liệu nghiệp vụ và ngữ cảnh của một User Story từ kho lưu trữ thông tin dự án, làm cơ sở để phân rã nhiệm vụ và thiết kế giải pháp kỹ thuật local fullstack.

## Triggers
- Kích hoạt khi nhận được yêu cầu thực thi hoặc phân rã một Story cụ thể.
- Yêu cầu tiên quyết: Được cung cấp mã định danh Story (`storyKey`).

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| `storyKey` | String | Có | Mã hiệu duy nhất của User Story (ví dụ: `ECOM-US-01`, `ECOM-US-02`). |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả |
|-----|--------------|-------|
| success | Boolean | `true` nếu thành công |
| message | String | Thông báo từ hệ thống |
| data | Object | Chi tiết bối cảnh Story và tài liệu đính kèm. Chứa các trường:<br>- `projectKey` (String): Mã hiệu dự án.<br>- `epicKey` (String): Mã hiệu Epic.<br>- `key` (String): Mã hiệu Story.<br>- `title` (String): Tiêu đề Story.<br>- `description` (String/Null): Mô tả.<br>- `deadline` (String/Null): Hạn hoàn thành.<br>- `priority` (String): Độ ưu tiên (VD: `MUST`).<br>- `status` (String): Trạng thái (VD: `OPEN`).<br>- `createdBy` (String): Người tạo.<br>- `documents` (List<Object>): Mảng tài liệu đính kèm, mỗi tệp gồm: `name`, `description`, `content`, `createdBy`.<br>- `project` (Object): Thông tin dự án.<br>- `epic` (Object): Thông tin Epic.<br>- `screens` (List<Object>/Null): Mảng màn hình thiết kế. |

## Steps
1. **Bước 1:** Thực hiện gọi MCP tool **`local-mcp:call_api`** để gọi gián tiếp API `get_context_story` (namespace: `bob`) với body `{"storyKey": storyKey}`.
2. **Bước 2:** Nhận phản hồi từ MCP server, kiểm tra trường `status`.
   - Nếu `status = 1`, chuyển tiếp dữ liệu `data` sang bước tiếp theo của workflow.
   - Nếu `status = 0` hoặc dữ liệu rỗng, chuyển dịch sang phần xử lý lỗi.
3. **Bước 3:** Đóng gói thông tin `storyContext` dưới định dạng JSON có cấu trúc để sẵn sàng cho bước phân rã.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Không tìm thấy Story (`status = 0`) | Truyền sai `storyKey` hoặc Story chưa được khởi tạo trên hệ thống | Ghi nhận lỗi vào tệp `error.log` trong thư mục task và thông báo trực tiếp cho PM hoặc User qua giao diện chat để làm rõ, sau đó dừng workflow. |
| MCP Tool Timeout / Mất kết nối | Sự cố mạng hoặc MCP server không phản hồi | Thực hiện thử lại (Retry) tối đa 2 lần, mỗi lần cách nhau 5 giây. Nếu tiếp tục lỗi, báo cáo cho User để kiểm tra trạng thái MCP server. |
