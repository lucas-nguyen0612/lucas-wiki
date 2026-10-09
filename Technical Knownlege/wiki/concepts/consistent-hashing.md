---
id: consistent-hashing
title: "Băm nhất quán (Consistent hashing)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [data-partitioning, load-balancing, caching]
confidence: medium
tags: [distributed-systems, database]
---

## Definition

Băm nhất quán là cách chia khoá cho các nút mà không phụ thuộc trực tiếp vào số nút. Cả khoá và nút được đặt lên cùng một vòng băm, và mỗi khoá được giao cho nút gần nhất theo chiều kim đồng hồ. Khi thêm hoặc bớt một nút, chỉ khoảng K/N khoá phải di chuyển (K là số khoá, N là số nút).

## Variants

- **Băm modulo (`Hash(key) mod N`)** — cách đơn giản, nhưng hỏng khi N thay đổi: phần lớn khoá phải phân phối lại.
- **Vòng băm cơ bản** — mỗi nút vật lý chiếm một vị trí trên vòng.
- **Nút ảo (VNode)** — mỗi nút vật lý chiếm nhiều vị trí trên vòng, nhờ đó tải phân bố đều hơn.

## Đánh đổi

- Trên lý thuyết băm nhất quán chia tải đều, nhưng thực tế vẫn có điểm nóng. Nút ảo giảm được vấn đề này.
- Giải quyết bài toán "thêm/bớt nút", nhưng không tự giải quyết việc chọn khoá phân vùng tốt; khoá kém vẫn gây lệch tải.

## Trong các case study

- Apache Cassandra dùng băm nhất quán để phân vùng dữ liệu, Amazon DynamoDB dùng để phân phối tải.
- Cả năm case study (URL shortener, WhatsApp, Twitter, Netflix, Uber) đều dùng băm nhất quán để giảm phân bổ tải không đều sau khi sharding (pp. 98, 106, 115, 124, 133).

## Key sources

- [[sources/system-design]] — vòng băm, công thức K/N, nút ảo, ví dụ thực tế (pp. 48–51); case study (pp. 98, 106, 115, 124, 133).
- Ghi chú đọc: [[readings/system-design/05-nhat-quan-giao-dich-sharding]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/data-partitioning]]
- [[concepts/load-balancing]]
- [[concepts/caching]]

## Mentioned in

## Notes
