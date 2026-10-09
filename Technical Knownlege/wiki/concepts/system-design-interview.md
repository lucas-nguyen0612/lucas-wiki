---
id: system-design-interview
title: "Phỏng vấn thiết kế hệ thống (System design interview)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [scalability, availability, caching, data-partitioning]
confidence: medium
tags: [system-design, interview]
---

## Definition

Phỏng vấn thiết kế hệ thống đánh giá khả năng đưa ra giải pháp kỹ thuật cho một bài toán mở. Không có một đáp án đúng duy nhất, và cuộc phỏng vấn mang tính trao đổi hai chiều giữa ứng viên và người phỏng vấn.

## Variants

- **Khung bảy bước** — làm rõ yêu cầu (chức năng, phi chức năng, mở rộng) → ước tính và ràng buộc → mô hình dữ liệu → thiết kế API → thiết kế cấp cao → thiết kế chi tiết → xác định và xử lý nút thắt.
- **Case study kinh điển** — URL shortener, WhatsApp, Twitter, Netflix, Uber.

## Đánh đổi

- Tránh khẳng định tuyệt đối kiểu "NoSQL tốt hơn, SQL không mở rộng được"; hãy khiêm tốn về những gì mình biết và không biết.
- Bước ước tính quyết định hướng thiết kế: tỉ lệ đọc/ghi cho biết cần bản sao đọc và bộ đệm; dung lượng 10 năm cho biết cần sharding và lưu trữ đối tượng.

## Trong các case study

| Case study | Ước tính chính | Quyết định nổi bật |
|---|---|---|
| URL shortener | ~40 ghi/s, ~4.000 đọc/s, ~6 TB/10 năm | Sinh khoá bằng ZooKeeper cấp dải hoặc KGS; NoSQL; HTTP 301 |
| WhatsApp | ~24K RPS, ~38 PB/10 năm | WebSocket; thông báo qua hàng đợi; API gateway đa giao thức |
| Twitter | ~12K RPS, ~19 PB/10 năm | News feed lai push/pull theo số follower |
| Netflix | ~500 TB/ngày, đọc/ghi 200:1 | Chia video theo cảnh; Open Connect (CDN riêng) |
| Uber | ~12K RPS, ~1,4 PB/10 năm | Quadtree + Redis; WebSocket cho vị trí; mutex khi ghép chuyến |

## Key sources

- [[sources/system-design]] — khung phỏng vấn (pp. 91–93) và năm case study (pp. 93–134).
- Ghi chú đọc: [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/scalability]]
- [[concepts/availability]]
- [[concepts/caching]]
- [[concepts/data-partitioning]]

## Mentioned in

## Notes
