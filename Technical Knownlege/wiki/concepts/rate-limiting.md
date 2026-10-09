---
id: rate-limiting
title: "Giới hạn tốc độ (Rate limiting)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [availability, api-design, circuit-breaker]
confidence: medium
tags: [reliability, security]
---

## Definition

Giới hạn tốc độ là chặn một thao tác khi nó được gọi quá một tần suất cho phép, ví dụ số yêu cầu mỗi giây từ một người dùng. Mục đích: chống tấn công từ chối dịch vụ (DoS), kiểm soát chi phí khi hệ thống tự mở rộng, và điều tiết luồng dữ liệu. API gateway thường đảm nhận việc này.

## Variants

- **Leaky bucket** — yêu cầu vào cuối một hàng đợi và được xử lý đều đặn theo kiểu FIFO; hàng đợi đầy thì yêu cầu mới bị loại bỏ.
- **Token bucket** — mỗi yêu cầu phải lấy một token từ "xô"; hết token thì bị từ chối và phải thử lại sau; xô được nạp lại sau một khoảng thời gian.
- **Fixed window** — đếm yêu cầu trong từng khung thời gian cố định.
- **Sliding log** — lưu dấu thời gian từng yêu cầu, bỏ các mục quá cũ, đếm số mục còn lại để quyết định; xử lý biên tốt hơn fixed window nhưng tốn công hơn.
- **Sliding window** — thoả hiệp: chi phí thấp như fixed window, xử lý biên tốt như sliding log, bằng cách cộng thêm phần có trọng số của cửa sổ trước.

## Đánh đổi

- Trong hệ phân tán có hai vấn đề: bộ đếm không nhất quán giữa các nút, và điều kiện tranh chấp (race condition) với kiểu "đọc rồi ghi" (get-then-set).
- Các cách giải đều có giá: phiên cố định làm mất khả năng chịu lỗi và mở rộng; kho tập trung như Redis tăng độ trễ và tranh chấp; khoá phân tán dễ thành nút cổ chai. Tác giả đề xuất "ghi rồi đọc" (set-then-get) bằng phép toán nguyên tử.

## Key sources

- [[sources/system-design]] — mục đích, thuật toán, vấn đề phân tán (pp. 80–81); API gateway (p. 67).
- Ghi chú đọc: [[readings/system-design/08-van-hanh-do-tin-cay-bao-mat]], [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]].

## Related concepts

- [[concepts/availability]]
- [[concepts/api-design]]
- [[concepts/circuit-breaker]]

## Mentioned in

## Notes
