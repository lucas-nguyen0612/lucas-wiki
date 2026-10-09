---
id: microservices
title: "Microservices (Kiến trúc vi dịch vụ)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [asynchronous-messaging, event-driven-architecture, api-design, distributed-transactions, load-balancing, circuit-breaker]
confidence: medium
tags: [architecture, system-design]
---

## Definition

Microservices là cách xây ứng dụng thành một tập các dịch vụ nhỏ, tự trị. Mỗi dịch vụ lo một khả năng kinh doanh trong một bối cảnh giới hạn (bounded context) và sở hữu dữ liệu của riêng nó. Đối lập với nó là monolith: toàn bộ ứng dụng là một khối, được triển khai cùng lúc.

## Variants

- **Monolith** — dễ phát triển, gỡ lỗi, hỗ trợ ACID; nhưng khó bảo trì khi lớn, khó mở rộng, mỗi bản cập nhật phải triển khai lại toàn bộ.
- **Monolith mô-đun** — vẫn một khối triển khai, nhưng chia thành các mô-đun độc lập.
- **Microservices** — dịch vụ nhỏ, triển khai và mở rộng độc lập.
- **Monolith phân tán (distributed monolith)** — trông như microservices nhưng liên kết chặt như monolith; gánh độ phức tạp mà không có lợi ích.
- **SOA** — tối đa hoá tái sử dụng qua giao diện chung; microservices thì tối đa hoá tự chủ và tách rời của nhóm.

## Đánh đổi

- Nên bắt đầu bằng monolith khi xây hệ thống mới. Microservices giải một vấn đề của tổ chức, không phải "viên đạn bạc".
- Cạm bẫy thường gặp: ranh giới dịch vụ không theo nghiệp vụ, đánh giá thấp độ khó của hệ phân tán, dùng chung cơ sở dữ liệu, cố làm mọi thứ ACID thay vì BASE.
- Hạ tầng đi kèm: API gateway (điểm truy cập duy nhất cho client), khám phá dịch vụ (service discovery), bộ ngắt mạch, mTLS giữa các dịch vụ.
- Tác giả đưa danh sách câu hỏi tự kiểm: nhóm có quá lớn cho một codebase? các nhóm có chặn nhau? có giá trị kinh doanh rõ ràng? tổ chức đủ trưởng thành? Nếu không, không cần tách.

## Trong các case study

- WhatsApp, Twitter, Netflix, Uber đều được thiết kế theo microservices: chia dữ liệu theo dịch vụ, mỗi dịch vụ sở hữu bảng của mình, dù mô hình dữ liệu trông như quan hệ.

## Key sources

- [[sources/system-design]] — monolith, microservices, SOA, cạm bẫy (pp. 59–63); API gateway, BFF (pp. 67–69); service discovery (pp. 81–83); case study (pp. 102–103, 110–111).
- Ghi chú đọc: [[readings/system-design/06-n-tang-nhan-tin-microservices]], [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]], [[readings/system-design/08-van-hanh-do-tin-cay-bao-mat]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]].

## Related concepts

- [[concepts/asynchronous-messaging]]
- [[concepts/event-driven-architecture]]
- [[concepts/api-design]]
- [[concepts/distributed-transactions]]
- [[concepts/load-balancing]]
- [[concepts/circuit-breaker]]

## Mentioned in

## Notes
