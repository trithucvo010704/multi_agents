# Workflow: Chỉnh sửa tài liệu sau Review

## Description
Quy trình này hướng dẫn Lina tự động hoặc chủ động xử lý phản hồi từ Mattin, David, hoặc Leader sau khi họ đã review các tài liệu EPIC/STORY.

## Triggers
Workflow này được kích hoạt bởi các trường hợp sau:
- **Manual Command (Thủ công):** Người dùng chat trực tiếp với câu lệnh (hoặc câu lệnh có ý nghĩa tương đương):
   > *"Lina, có tài liệu đã trả review rồi đấy, hãy bắt tay vào xem đi"*

## Mermaid Diagram

```mermaid
flowchart TD
  Start([Nhận feedback review từ User]) --> Analyze[Đọc tài liệu gốc & Phân tích Feedback]
  Analyze --> EditDoc[Chỉnh sửa nội dung tài liệu]
  EditDoc --> CheckType{Loại tài liệu?}
  CheckType -->|EPIC| SaveEpic[Skill: save-epic-local]
  CheckType -->|STORY| SaveStory[Skill: save-story-local]
  SaveEpic --> UploadEpic[Skill: upload-epic-doc]
  SaveStory --> UploadStory[Skill: upload-story-doc]
  UploadEpic --> ReportDone[Báo cáo hoàn tất]
  UploadStory --> ReportDone
  ReportDone --> End([Kết thúc quy trình])
```

## Steps

| # | Bước | Actor | Tool/Action | Output |
| --- | --- | --- | --- | --- |
| 1 | Tiếp nhận feedback review | Lina | Đọc feedback từ User qua chat/message | Nắm rõ nội dung comment/feedback chi tiết của Reviewer. |
| 2 | Phân tích và chỉnh sửa tài liệu | Lina | Đọc tài liệu gốc + Cập nhật nội dung theo feedback | File tài liệu gốc (EPIC/STORY) đã được sửa đổi, tối ưu logic. |
| 3 | Lưu và đồng bộ tài liệu EPIC mới (nếu có) | Lina | `[../skills/save-epic-local/SKILL.md](../skills/save-epic-local/SKILL.md)` & `[../skills/local-mcp/upload-epic-doc/SKILL.md](../skills/local-mcp/upload-epic-doc/SKILL.md)` | Tài liệu EPIC được lưu cục bộ và cập nhật thành công lên server. |
| 4 | Lưu và đồng bộ tài liệu STORY mới (nếu có) | Lina | `[../skills/save-story-local/SKILL.md](../skills/save-story-local/SKILL.md)` & `[../skills/local-mcp/upload-story-doc/SKILL.md](../skills/local-mcp/upload-story-doc/SKILL.md)` | Bộ tài liệu STORY được lưu cục bộ và cập nhật thành công lên server. |
| 5 | Thông báo kết quả | Lina | Gửi log/message xác nhận | Báo cáo hoàn tất gửi tới Reviewer/User. |

## Definition of Done

* [ ] Đã đọc và phân tích kỹ lưỡng toàn bộ dữ liệu feedback nhận được từ User.
* [ ] Mọi comment, điểm lưu ý từ Mattin, David, hoặc Leader đều được chỉnh sửa triệt để trong tài liệu mới.
* [ ] Tài liệu được lưu trữ đúng vị trí cục bộ trong workspace qua kỹ năng `save-epic-local` hoặc `save-story-local`.
* [ ] Tài liệu cập nhật đã được đồng bộ lên hệ thống qua kỹ năng `upload-epic-doc` hoặc `upload-story-doc`.
* [ ] Trạng thái workflow được cập nhật thành công sang "Hoàn tất chỉnh sửa".

