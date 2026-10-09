---
id: asynchronous-messaging
title: "Nhắn tin bất đồng bộ (Asynchronous messaging)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [scalability, availability, event-driven-architecture, microservices]
confidence: medium
tags: [system-design, messaging]
---

## Definition

Nhắn tin bất đồng bộ là cách các dịch vụ trao đổi qua một thành phần trung gian (hàng đợi, chủ đề, nhà môi giới tin nhắn) thay vì gọi trực tiếp và chờ nhau. Bên gửi không cần biết bên nhận ở đâu hay có đang chạy không, nhờ đó các dịch vụ được tách rời và mở rộng độc lập.

## Variants

- **Hàng đợi tin nhắn (điểm–điểm)** — mỗi tin được đúng một consumer xử lý; có DLQ, at-least-once, exactly-once, backpressure.
- **Pub/sub** — tin trên một chủ đề được đẩy tới mọi subscriber; fanout, lọc. Nhà xuất bản không cần biết ai nhận.
- **Event streaming** — chỉ hỗ trợ pub/sub, mở rộng tốt hơn broker nhưng không đảm bảo giao hàng và ít tính năng chịu lỗi hơn.
- **ESB (enterprise service bus)** — thành phần tích hợp tập trung; broker là lựa chọn "nhẹ" thay thế.
- **Kiến trúc hướng sự kiện**, event sourcing, CQRS — các mẫu kiến trúc dựa trên nhắn tin; xem trang riêng.

## Đánh đổi

- Lợi ích của hàng đợi: mở rộng, tách rời, hiệu năng (không chờ), độ tin cậy khi một phần hệ thống ngoại tuyến.
- ESB tập trung dễ thành nút cổ chai và điểm lỗi làm hỏng toàn bộ liên lạc.
- Khi hàng đợi phình quá bộ nhớ, hiệu năng giảm; backpressure giới hạn kích thước và trả HTTP 503 để client thử lại sau.

## Trong các case study

- WhatsApp gửi thông báo đẩy qua hàng đợi tin (không phải pub/sub thuần) vì mỗi nền tảng thiết bị xử lý thông báo khác nhau qua FCM/APNS.
- Netflix đặt xử lý video sau hàng đợi tin, tách khỏi chức năng tải lên; video vi phạm được đẩy vào DLQ cho kiểm duyệt viên.

## Key sources

- [[sources/system-design]] — broker, hàng đợi, pub/sub, ESB (pp. 54–59); EDA, event sourcing, CQRS (pp. 63–67); WhatsApp (p. 105); Netflix (p. 122).
- Ghi chú đọc: [[readings/system-design/06-n-tang-nhan-tin-microservices]], [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]].

## Related concepts

- [[concepts/scalability]]
- [[concepts/availability]]
- [[concepts/event-driven-architecture]]
- [[concepts/microservices]]

## Mentioned in

## Notes
