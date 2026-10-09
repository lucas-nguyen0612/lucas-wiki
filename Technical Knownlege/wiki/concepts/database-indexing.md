---
id: database-indexing
title: "Chỉ mục và chuẩn hoá cơ sở dữ liệu (Indexing & normalization)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [database-replication, data-partitioning, caching, geospatial-indexing]
confidence: medium
tags: [database, performance]
---

## Definition

Chỉ mục (index) là một cấu trúc dữ liệu phụ giúp tìm hàng nhanh hơn mà không phải quét cả bảng. Chuẩn hoá (normalization) là cách tổ chức bảng để loại dữ liệu dư thừa và tránh dị thường khi chèn, cập nhật, xoá. Cả hai đều là quyết định đánh đổi giữa tốc độ đọc, tốc độ ghi và dung lượng.

## Variants

- **Chỉ mục dày (dense)** — mỗi hàng có một mục chỉ mục; tìm nhanh bằng tìm kiếm nhị phân nhưng tốn bộ nhớ và làm chậm ghi.
- **Chỉ mục thưa (sparse)** — chỉ một số hàng có mục; ghi nhanh, ít bộ nhớ, nhưng đọc chậm hơn và chỉ dùng được với dữ liệu có thứ tự.
- **Dạng chuẩn 1NF, 2NF, 3NF, BCNF** — các bậc quy tắc chuẩn hoá; một quan hệ thường được gọi là "đã chuẩn hoá" khi đạt 3NF.
- **Phi chuẩn hoá (denormalization)** — cố ý thêm dữ liệu dư thừa để tránh phép nối tốn kém. Không có nghĩa là đảo ngược chuẩn hoá.
- **Materialized view** — kết quả truy vấn được tính trước và lưu lại.

## Đánh đổi

- Chỉ mục đổi chi phí lưu trữ và tốc độ ghi lấy tốc độ đọc.
- Phi chuẩn hoá tăng hiệu năng đọc nhưng giảm hiệu năng ghi và có rủi ro không nhất quán. Trong hệ phân tán, khi dữ liệu đã bị chia bằng federation và sharding, phi chuẩn hoá tránh được việc join qua mạng.

## Trong các case study

- URL shortener dùng chỉ mục để cải thiện hiệu năng truy vấn khi tra URL rút gọn.

## Key sources

- [[sources/system-design]] — chỉ mục dày/thưa (pp. 35–37); dị thường và dạng chuẩn (pp. 37–38); phi chuẩn hoá (p. 39); URL shortener (p. 95).
- Ghi chú đọc: [[readings/system-design/04-co-so-du-lieu-sql-nosql-sao-chep-chi-muc]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]].

## Related concepts

- [[concepts/database-replication]]
- [[concepts/data-partitioning]]
- [[concepts/caching]]
- [[concepts/geospatial-indexing]]

## Mentioned in

## Notes
