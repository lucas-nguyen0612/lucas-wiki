---
id: availability
title: "Tính khả dụng (Availability)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [scalability, database-replication, cap-theorem, system-design-interview, asynchronous-messaging, load-balancing, circuit-breaker, rate-limiting]
confidence: medium
tags: [system-design, reliability]
---

## Definition

Tính khả dụng là tỉ lệ thời gian một hệ thống hoạt động và thực hiện được chức năng của nó trong một khoảng thời gian. Thường đo bằng "số chín": Availability = Uptime / (Uptime + Downtime).

## Variants

- **Sẵn sàng cao (high availability)** — chấp nhận gián đoạn tối thiểu, chi phí vừa phải.
- **Chịu lỗi (fault tolerance)** — không gián đoạn, cần dự phòng toàn bộ phần cứng, đắt hơn nhiều.
- **Nối tiếp và song song** — thành phần nối tiếp làm giảm khả dụng tổng (99,9% × 99,9% ≈ 99,8%), thành phần song song làm tăng (≈ 99,9999%).
- **Độ tin cậy (reliability)** — hệ thống tin cậy thì khả dụng, nhưng khả dụng chưa chắc đã tin cậy.

## Đánh đổi

- Bảng số chín: 99,9% ≈ 8,77 giờ ngừng/năm; 99,99% ≈ 52,6 phút/năm; 99,999% ≈ 5,25 phút/năm. Mỗi số chín thêm vào tốn kém hơn nhiều.
- Điểm lỗi duy nhất xuất hiện khắp nơi: bộ cân bằng tải, proxy ngược, API gateway, bộ đếm sinh khoá. Cách chữa chung là dư thừa (chạy song song).
- Trong định lý CAP, khả dụng (A) phải đánh đổi với nhất quán (C) khi có phân vùng mạng.
- Kỹ thuật vận hành hỗ trợ: bộ ngắt mạch, giới hạn tốc độ, SLA/SLO/SLI, khắc phục thảm hoạ (RTO, RPO; sao lưu, site lạnh, site nóng).

## Trong các case study

- Mọi case study đều đặt tính khả dụng cao là yêu cầu phi chức năng. URL shortener chạy nhiều phiên bản ZooKeeper để tránh điểm lỗi duy nhất ở bộ đếm.

## Key sources

- [[sources/system-design]] — số chín, nối tiếp/song song, chịu lỗi (p. 24); điểm lỗi duy nhất (pp. 12, 23, 68, 97); circuit breaker, rate limiting, SLA, DR (pp. 79–85).
- Ghi chú đọc: [[readings/system-design/03-cdn-proxy-kha-dung-mo-rong-luu-tru]], [[readings/system-design/02-can-bang-tai-phan-cum-bo-nho-dem]], [[readings/system-design/08-van-hanh-do-tin-cay-bao-mat]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]].

## Related concepts

- [[concepts/scalability]]
- [[concepts/database-replication]]
- [[concepts/cap-theorem]]
- [[concepts/load-balancing]]
- [[concepts/circuit-breaker]]
- [[concepts/rate-limiting]]
- [[concepts/asynchronous-messaging]]
- [[concepts/system-design-interview]]

## Mentioned in

## Notes
