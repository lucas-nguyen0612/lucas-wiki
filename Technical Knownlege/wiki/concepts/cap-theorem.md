---
id: cap-theorem
title: "Định lý CAP (CAP theorem)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [availability, database-replication, data-partitioning, distributed-transactions]
confidence: medium
tags: [distributed-systems, consistency]
---

## Definition

Định lý CAP phát biểu rằng một hệ phân tán chỉ có thể đảm bảo hai trong ba đặc tính: nhất quán (C), khả dụng (A) và chịu phân vùng mạng (P). Vì phân vùng mạng luôn có thể xảy ra, trên thực tế phải chọn giữa C và A khi có phân vùng.

## Variants

- **CA** — nguồn liệt kê PostgreSQL, MariaDB; nhưng CA chỉ có nghĩa với hệ không phân tán (xem Notes).
- **CP** — tắt nút không nhất quán khi phân vùng (ví dụ MongoDB, HBase).
- **AP** — mọi nút vẫn trả lời nhưng có thể trả dữ liệu cũ (ví dụ Cassandra, CouchDB).
- **PACELC** — mở rộng của Daniel J. Abadi: khi có phân vùng (P) chọn A hay C; còn khi chạy bình thường (E) vẫn phải chọn giữa độ trễ (L) và nhất quán (C).
- **ACID vs BASE** — hai mô hình nhất quán: ACID (nguyên tử, nhất quán, cô lập, bền vững) cho độ tin cậy giao dịch; BASE (khả dụng cơ bản, trạng thái mềm, nhất quán cuối cùng) cho khả dụng và mở rộng.

## Đánh đổi

- Không có câu trả lời đúng chung cho ACID hay BASE; BASE buộc lập trình viên tự lo tính nhất quán, ACID phù hợp khi độ tin cậy dữ liệu là bắt buộc.
- PACELC ra đời vì CAP không nói gì về độ trễ: theo CAP, một CSDL trả lời sau 30 ngày vẫn là "khả dụng".
- Hầu hết NoSQL hy sinh ACID để lấy hiệu năng và khả năng mở rộng; SQL vẫn tốt hơn khi cần giao dịch tin cậy.

## Key sources

- [[sources/system-design]] — ACID/BASE (pp. 39–40); CAP (pp. 40–42); PACELC (p. 42); SQL vs NoSQL (p. 33).
- Ghi chú đọc: [[readings/system-design/05-nhat-quan-giao-dich-sharding]], [[readings/system-design/04-co-so-du-lieu-sql-nosql-sao-chep-chi-muc]].

## Related concepts

- [[concepts/availability]]
- [[concepts/database-replication]]
- [[concepts/data-partitioning]]
- [[concepts/distributed-transactions]]

## Mentioned in

## Notes

- Nguồn xếp PostgreSQL/MariaDB vào loại "CA" (p. 41) trong khi vừa lập luận rằng hệ phân tán buộc phải chọn P. Điểm này dễ gây tranh cãi và nên đối chiếu với nguồn khác.
