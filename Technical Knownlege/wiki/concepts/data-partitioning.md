---
id: data-partitioning
title: "Phân vùng dữ liệu (Data partitioning / Sharding)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [scalability, database-replication, cap-theorem, system-design-interview, consistent-hashing, database-indexing]
confidence: medium
tags: [database, distributed-systems]
---

## Definition

Phân vùng dữ liệu là chia một cơ sở dữ liệu hoặc bảng thành nhiều phần nhỏ đặt trên nhiều máy để cải thiện khả năng quản lý, hiệu năng và tính khả dụng. Sharding là phân vùng theo chiều ngang: tách các hàng của một bảng ra nhiều shard có cùng lược đồ.

## Variants

- **Ngang (sharding)** và **dọc** (theo cột).
- **Tiêu chí**: theo băm, theo danh sách, theo phạm vi, tổng hợp.
- **Băm nhất quán (consistent hashing)** — cách gán khoá cho shard mà chỉ K/N khoá phải di chuyển khi đổi số nút; xem trang riêng.
- **Liên kết CSDL (federation)** — chia theo chức năng; nhiều CSDL vật lý hiện ra như một CSDL logic.

## Đánh đổi

- Sharding có lợi khi mở rộng ngang bằng nhiều máy rẻ hơn mở rộng dọc.
- Nhưng join qua nhiều shard khó, và phải cân bằng lại khi dữ liệu lệch. Khi join qua mạng quá tốn kém, hệ thống thường phi chuẩn hoá dữ liệu.

## Trong các case study

- Cả năm case study đều đề xuất sharding ngang, rồi dùng băm nhất quán để khắc phục phân bổ tải không đều (pp. 98, 106, 115, 124, 133). Uber shard theo vùng (ví dụ mã zip).
- Mẫu chung: mô hình dữ liệu trông như quan hệ nhưng không đặt hết vào một CSDL — chia dữ liệu theo dịch vụ.

## Key sources

- [[sources/system-design]] — sharding, tiêu chí phân vùng, băm nhất quán, federation (pp. 46–52); case study (pp. 98, 102–103, 106, 110–111, 115, 124, 133).
- Ghi chú đọc: [[readings/system-design/05-nhat-quan-giao-dich-sharding]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/scalability]]
- [[concepts/database-replication]]
- [[concepts/cap-theorem]]
- [[concepts/consistent-hashing]]
- [[concepts/database-indexing]]
- [[concepts/system-design-interview]]

## Mentioned in

## Notes
