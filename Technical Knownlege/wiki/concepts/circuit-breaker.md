---
id: circuit-breaker
title: "Bộ ngắt mạch (Circuit breaker)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [availability, microservices, rate-limiting]
confidence: medium
tags: [reliability, microservices]
---

## Definition

Bộ ngắt mạch là một lớp bọc quanh lời gọi tới dịch vụ khác, đếm số lần lỗi. Khi lỗi vượt ngưỡng, nó "ngắt": các lời gọi tiếp theo bị trả lỗi ngay mà không gọi tới dịch vụ đang hỏng nữa. Mục đích là để hệ thống "thất bại nhanh" thay vì treo chờ.

## Variants

- **Đóng (closed)** — lời gọi đi qua bình thường, lỗi được đếm.
- **Mở (open)** — vượt ngưỡng lỗi; mọi lời gọi bị từ chối ngay.
- **Nửa mở (half-open)** — sau một thời gian, cho thử vài lời gọi; thành công thì đóng lại, lỗi thì mở tiếp.

## Đánh đổi

- Lý do cần: lời gọi từ xa có thể thất bại hoặc treo tới hết thời gian chờ; nhiều caller cùng chờ một dịch vụ không phản hồi có thể cạn tài nguyên và gây lỗi dây chuyền.
- Trong microservices, nguồn khuyên "thất bại nhanh bằng bộ ngắt mạch để đạt khả năng chịu lỗi".

## Key sources

- [[sources/system-design]] — cơ chế và ba trạng thái (pp. 79–80); nguyên tắc microservices (p. 62).
- Ghi chú đọc: [[readings/system-design/08-van-hanh-do-tin-cay-bao-mat]], [[readings/system-design/06-n-tang-nhan-tin-microservices]].

## Related concepts

- [[concepts/availability]]
- [[concepts/microservices]]
- [[concepts/rate-limiting]]

## Mentioned in

## Notes
