---
id: scalability
title: "Khả năng mở rộng (Scalability)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [availability, data-partitioning, caching, system-design-interview, asynchronous-messaging, load-balancing, real-time-communication]
confidence: medium
tags: [system-design, distributed-systems]
---

## Definition

Khả năng mở rộng là mức độ một hệ thống đáp ứng thay đổi về nhu cầu bằng cách thêm hoặc bớt tài nguyên. Có hai hướng: mở rộng theo chiều dọc (nâng cấp một máy) và mở rộng theo chiều ngang (thêm máy vào nhóm).

## Variants

- **Theo chiều dọc (scale up)** — đơn giản, dữ liệu nhất quán, nhưng khó nâng cấp mãi và có thể là điểm lỗi duy nhất.
- **Theo chiều ngang (scale out)** — tăng dư thừa và chịu lỗi, nhưng phức tạp hơn và dữ liệu có thể không nhất quán.

## Đánh đổi

- Mở rộng ngang cần thêm các khối xây dựng: bộ cân bằng tải để chia yêu cầu, bộ nhớ đệm để giảm tải CSDL, sharding và sao chép để chia dữ liệu, hàng đợi để tách rời các dịch vụ.
- SQL thường mở rộng theo chiều dọc; NoSQL mở rộng theo chiều ngang và nhiều hệ tự phân phối dữ liệu.
- Tách tầng vật lý (kiến trúc N tầng) tăng khả năng mở rộng nhưng thêm độ trễ mạng.

## Trong các case study

- Mọi case study đều đặt khả năng mở rộng là yêu cầu phi chức năng và bắt đầu bằng ước tính quy mô: URL shortener ~4.000 đọc/giây, WhatsApp ~24K RPS, Twitter và Uber ~12K RPS.
- Các hệ đọc nhiều (URL shortener 100:1, Netflix 200:1) được mở rộng bằng bản sao chỉ-đọc và bộ đệm.

## Key sources

- [[sources/system-design]] — định nghĩa và so sánh dọc/ngang (pp. 25–26); SQL vs NoSQL (pp. 32–33); N tầng (p. 53); ước tính trong case study (pp. 94–95, 101, 109, 118, 126–127).
- Ghi chú đọc: [[readings/system-design/03-cdn-proxy-kha-dung-mo-rong-luu-tru]], [[readings/system-design/02-can-bang-tai-phan-cum-bo-nho-dem]], [[readings/system-design/04-co-so-du-lieu-sql-nosql-sao-chep-chi-muc]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]].

## Related concepts

- [[concepts/availability]]
- [[concepts/data-partitioning]]
- [[concepts/caching]]
- [[concepts/load-balancing]]
- [[concepts/asynchronous-messaging]]
- [[concepts/real-time-communication]]
- [[concepts/system-design-interview]]

## Mentioned in

## Notes
