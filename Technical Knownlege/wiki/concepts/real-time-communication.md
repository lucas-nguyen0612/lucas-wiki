---
id: real-time-communication
title: "Giao tiếp thời gian thực: Long polling, WebSocket, SSE"
type: concept
created: 2026-09-21
updated: 2026-10-07
key_sources: [system-design]
related_concepts: [api-design, scalability, geospatial-indexing, supabase]
confidence: medium
tags: [networking, real-time]
---

## Definition

Web ban đầu theo mô hình client khởi tạo mọi giao dịch, nên máy chủ không có cách tự gửi dữ liệu mới cho client. Giao tiếp thời gian thực là các kỹ thuật cho phép máy chủ "đẩy" dữ liệu ngay khi có, thay vì để client liên tục hỏi lại.

## Variants

- **Kéo (pull / polling)** — client định kỳ gửi yêu cầu hỏi có dữ liệu mới không.
- **Long polling** — client gửi yêu cầu, máy chủ giữ yêu cầu mở tới khi có dữ liệu mới rồi mới trả lời.
- **WebSocket** — kênh song công toàn phần (hai chiều) qua một kết nối TCP lâu dài.
- **Server-Sent Events (SSE)** — kênh một chiều, máy chủ đẩy sự kiện xuống client qua kết nối lâu dài.

## Đánh đổi

- Kéo không mở rộng được: tạo nhiều yêu cầu thừa và phần lớn phản hồi là rỗng.
- Long polling dễ làm nhưng thường không mở rộng được.
- WebSocket song công, nhưng kết nối bị đứt không tự phục hồi.
- SSE đơn giản, nhưng chỉ một chiều và không hỗ trợ dữ liệu nhị phân.

## Trong các case study

- WhatsApp và Uber đều chọn mô hình đẩy (WebSocket hoặc SSE) thay vì kéo; WhatsApp nghiêng về WebSocket vì cần song công (pp. 104–105, 131).
- Uber cần công việc nền để ping GPS khi ứng dụng ở chế độ nền (p. 131).

## Key sources

- [[sources/system-design]] — long polling, WebSocket, SSE (pp. 74–76); WhatsApp (pp. 104–105); Uber (p. 131).
- Ghi chú đọc: [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/api-design]]
- [[concepts/scalability]]
- [[concepts/geospatial-indexing]]
- [[concepts/supabase]]

## Mentioned in

## Notes
