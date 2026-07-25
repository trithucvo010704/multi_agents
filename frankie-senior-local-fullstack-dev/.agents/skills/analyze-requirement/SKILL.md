---
name: analyze-requirement
description: Phân tích yêu cầu đầu vào (Specs hoặc Prompt) và làm rõ để sẵn sàng thực hiện.
---

## Description
Kỹ năng tiếp nhận tài liệu Specs hoặc Prompt của người dùng, phân tích tính đầy đủ và tính khả thi của các yêu cầu phát triển ứng dụng local. Đảm bảo Agent không hành động khi thiếu thông tin.

## Triggers
- Được kích hoạt ở bước đầu tiên của quy trình phát triển ứng dụng local.
- Khi nhận được yêu cầu mới từ người dùng.

## Inputs
| Tên | Kiểu dữ liệu | Bắt buộc | Mô tả chi tiết |
|-----|--------------|----------|----------------|
| raw_input | String | Có | Yêu cầu thô từ người dùng (Specs hoặc Prompt) |

## Outputs
| Tên | Kiểu dữ liệu | Mô tả chi tiết |
|-----|--------------|----------------|
| is_specs | Boolean | Xác định đây là Specs (True) hay Prompt (False) |
| finalized_specs | Markdown | Bản đặc tả yêu cầu chi tiết đã được làm rõ và thống nhất |

## Steps
1. **Phân tích loại đầu vào:** Kiểm tra xem `raw_input` là Bản mô tả yêu cầu Specs chi tiết (đầy đủ cấu trúc API, giao diện, cấu hình) hay chỉ là Prompt chung chung.
2. **Xử lý dạng Specs:** Nếu là Specs, kiểm tra tính khả thi và đầy đủ thông tin (BE chính, cấu hình local, các chức năng chính). Nếu đạt, chuyển đổi thành `finalized_specs`.
3. **Xử lý dạng Prompt:** Nếu là Prompt chung chung, liệt kê các điểm chưa rõ (API cần viết, UI hoạt động ra sao, v.v.).
4. **Làm rõ (Q&A):** Gom các câu hỏi làm rõ (tối đa 5 câu) và gửi cho người dùng. Cập nhật `finalized_specs` sau khi nhận được phản hồi.

## Error Handling
| Tình huống Lỗi | Nguyên nhân | Cách xử lý (Self-healing) |
|----------------|-------------|---------------------------|
| Thiếu thông tin tích hợp API BE chính | Specs không đề cập cách thức kết nối với BE chính | Đặt câu hỏi phỏng vấn trực tiếp làm rõ API Endpoint và api_token |
| Yêu cầu mơ hồ, không khả thi | Prompt quá ngắn hoặc mâu thuẫn logic | Trả về thông báo lỗi, đề xuất giải pháp thay thế và chờ phản hồi của user |
