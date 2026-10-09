---
id: database-replication
title: "Sao chép cơ sở dữ liệu (Database replication)"
type: concept
created: 2026-09-21
updated: 2026-10-07
key_sources: [system-design]
related_concepts: [availability, data-partitioning, cap-theorem, caching, database-indexing, supabase]
confidence: medium
tags: [database, distributed-systems]
---

## Definition

Sao chép cơ sở dữ liệu là việc giữ nhiều bản sao dữ liệu trên các máy khác nhau và đồng bộ giữa chúng, nhằm tăng độ tin cậy, khả năng chịu lỗi và khả năng đọc.

## Variants

- **Master–slave** — một nút nhận ghi, các nút phụ chỉ phục vụ đọc; master hỏng thì chạy chỉ-đọc tới khi nâng cấp một slave.
- **Master–master** — cả hai nút cùng đọc/ghi; chuyển đổi dự phòng nhanh nhưng phải giải quyết xung đột.
- **Đồng bộ / bất đồng bộ** — ghi đồng thời vào bản chính và bản sao, hoặc sao chép sau.

## Đánh đổi

- Master–slave: càng nhiều slave đọc thì càng phải sao chép nhiều, làm tăng độ trễ sao chép.
- Master–master: nhất quán lỏng hơn hoặc độ trễ ghi tăng, và cần cơ chế giải quyết xung đột.
- Sao chép bất đồng bộ nhanh hơn nhưng bản sao có thể trễ so với bản chính — gắn với lựa chọn nhất quán–khả dụng trong định lý CAP.

## Trong các case study

- Ở bước xử lý nút thắt, cả năm case study đều đề xuất dùng nhiều bản sao đọc cho CSDL (pp. 100, 108, 117, 125, 134). URL shortener (đọc/ghi 100:1) và Netflix (200:1) là các hệ đọc nhiều điển hình; URL shortener còn thêm bản sao dự phòng cho CSDL chính (p. 100).

## Key sources

- [[sources/system-design]] — master–slave, master–master, đồng bộ/bất đồng bộ (pp. 33–35); bản sao đọc trong case study (pp. 100, 108, 117, 125, 134).
- Ghi chú đọc: [[readings/system-design/04-co-so-du-lieu-sql-nosql-sao-chep-chi-muc]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/availability]]
- [[concepts/data-partitioning]]
- [[concepts/cap-theorem]]
- [[concepts/supabase]]
- [[concepts/caching]]
- [[concepts/database-indexing]]

## Mentioned in

## Notes
