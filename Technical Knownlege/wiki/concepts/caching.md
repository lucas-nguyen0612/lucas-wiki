---
id: caching
title: "Bộ nhớ đệm (Caching)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [scalability, database-replication, system-design-interview, consistent-hashing, database-indexing, geospatial-indexing]
confidence: medium
tags: [system-design, performance]
---

## Definition

Bộ nhớ đệm lưu tạm một phần dữ liệu ở nơi truy cập nhanh để giảm số lần phải đọc từ tầng lưu trữ chậm hơn. Nó đánh đổi dung lượng lấy tốc độ, dựa trên giả định rằng dữ liệu vừa được dùng sẽ sớm được dùng lại.

## Variants

- **Chiến lược ghi** — ghi xuyên (write-through), ghi vòng (write-around), ghi sau (write-back).
- **Chính sách loại bỏ** — FIFO, LIFO, LRU, MRU, LFU, ngẫu nhiên.
- **Bộ đệm phân tán / toàn cục** — gộp RAM nhiều máy thành một kho, hoặc một bộ đệm chung cho mọi nút ứng dụng.
- **CDN** — mạng máy chủ biên phân bố theo địa lý, đệm file tĩnh gần người dùng; kiểu push (đẩy khi có thay đổi) hoặc pull (kéo khi có yêu cầu).
- **Bộ đệm DNS** — bản ghi được giữ trong khoảng TTL.

## Đánh đổi

- Ghi xuyên giữ bộ đệm và CSDL nhất quán nhưng ghi chậm hơn; ghi vòng giảm trễ ghi nhưng tăng cache miss khi đọc lại ngay; ghi sau cho độ trễ thấp, thông lượng cao nhưng có nguy cơ mất dữ liệu nếu lớp đệm gặp sự cố.
- Không nên dùng bộ đệm khi truy cập đệm chậm ngang kho chính, khi yêu cầu ít lặp lại, hoặc khi dữ liệu thay đổi liên tục. Không bao giờ coi bộ đệm là nơi lưu trữ vĩnh viễn.
- Push CDN hợp với trang ít truy cập hoặc ít cập nhật; pull CDN hợp với trang lưu lượng lớn.

## Trong các case study

- URL shortener đệm ~20% yêu cầu theo quy tắc 80/20 (~35 GB/ngày) với LRU; WhatsApp chỉ đệm tin cũ vì người dùng muốn tin mới nhất; Netflix phân phối video qua Open Connect (CDN riêng); Uber đệm vị trí tài xế mới nhất bằng Redis.

## Key sources

- [[sources/system-design]] — chiến lược ghi, chính sách loại bỏ, khi nào không nên dùng (pp. 16–19); CDN (pp. 20–22); TTL (p. 9); case study (pp. 94–95, 99, 106, 123, 132).
- Ghi chú đọc: [[readings/system-design/02-can-bang-tai-phan-cum-bo-nho-dem]], [[readings/system-design/03-cdn-proxy-kha-dung-mo-rong-luu-tru]], [[readings/system-design/01-mo-dau-va-mang-co-ban]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]].

## Related concepts

- [[concepts/scalability]]
- [[concepts/database-replication]]
- [[concepts/consistent-hashing]]
- [[concepts/database-indexing]]
- [[concepts/geospatial-indexing]]
- [[concepts/system-design-interview]]

## Mentioned in

## Notes
