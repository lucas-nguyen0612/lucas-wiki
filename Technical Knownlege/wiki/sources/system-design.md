---
id: system-design
title: Thiết kế hệ thống (System Design) — Karan Pratap Singh
type: source
created: 2026-09-21
updated: 2026-09-21
authors:
  - Karan Pratap Singh
year: 2022
source_type: book
importance: 3
provenance: replayable
confidence: unverified
raw_paths:
  - raw/sources/System_design.pdf
urls:
  - "https://karanpratapsingh.com/courses/system-design"
tags:
  - system-design
  - distributed-systems
  - interview
  - ban-dich-tieng-viet
ingest_status: finalized
verify_status: passed
findings:
  - {id: 1, reviewer: grounding, class: dismiss, claim: "Với bộ cân bằng tải và proxy ngược, nguồn đề xuất chạy thêm bản dự phòng (pp. 12, 23)", evidence: "p. 12 explicitly proposes a second/N load balancers in cluster mode. p. 23 only notes that configuring multiple reverse proxies (failover) adds complexity, which implies the remedy rather than recommending it. Meaning is preserved.", action: "None required; optionally soften 'đề xuất' for the reverse proxy case."}
  - {id: 2, reviewer: grounding, class: dismiss, claim: "Các nguồn được tham khảo nhưng chưa có trong wiki: ... Martin Kleppmann, microservices.io (p. 135)", evidence: "The reference list spans pp. 134–135: Kleppmann lectures, Insider's Guide and microservices.io are on p. 134; System Design Primer and Grokking are on p. 135.", action: Optionally change locator to (pp. 134–135).}
---

## Summary

Bản dịch tiếng Việt (dịch máy) khoá học mở "System Design" của [[people/karan-pratap-singh]], dài 135 trang, chia năm chương. Chương I–IV đi từ nền mạng (IP, OSI, TCP/UDP, DNS) lên các khối xây dựng hạ tầng (cân bằng tải, bộ đệm, CDN, proxy, lưu trữ). Sau đó là tầng dữ liệu (SQL/NoSQL, sao chép, chỉ mục, ACID/BASE, CAP/PACELC, giao dịch phân tán, sharding, băm nhất quán), rồi các mẫu kiến trúc và giao tiếp (N tầng, hàng đợi, pub/sub, microservices, EDA, CQRS, API gateway, REST/GraphQL/gRPC, WebSocket), cuối cùng là các kỹ thuật vận hành và bảo mật (circuit breaker, rate limiting, service discovery, SLA, DR, container, OAuth/OIDC, SSO, TLS). Chương V gom tất cả thành một khung phỏng vấn thiết kế hệ thống bảy bước, rồi áp dụng khung đó cho năm case study: URL shortener, WhatsApp, Twitter, Netflix, Uber.

Mỗi chủ đề được trình bày theo cùng một khuôn: định nghĩa → phân loại → ưu/nhược điểm → ví dụ sản phẩm. Thông điệp xuyên suốt là mọi lựa chọn đều là đánh đổi, không có "viên đạn bạc". Nội dung chi tiết theo từng phần nằm ở 11 ghi chú đọc (xem mục Notes).

## Key claims

- Thiết kế hệ thống là quá trình xác định kiến trúc, giao diện và dữ liệu thoả mãn yêu cầu cụ thể; đây là quyết định sớm và khó sửa về sau (p. 2). — confidence: high
- Bộ cân bằng tải, proxy ngược, API gateway và bộ đếm đơn đều có thể trở thành điểm lỗi duy nhất (pp. 12, 23, 68, 97). Với bộ cân bằng tải và proxy ngược, nguồn đề xuất chạy thêm bản dự phòng (pp. 12, 23); với API gateway, nguồn chỉ nêu nhược điểm (p. 68); với bộ đếm, chạy nhiều bộ đếm lại gây trùng khoá, nên nguồn đề xuất dùng ZooKeeper cấp dải số cho từng máy chủ và chạy nhiều phiên bản ZooKeeper (p. 97). — confidence: high
- Hai thành phần nối tiếp làm giảm tính khả dụng tổng (99,9% × 99,9% ≈ 99,8%), hai thành phần song song làm tăng (≈ 99,9999%) (p. 24). — confidence: high
- Mở rộng ngang tăng dư thừa và chịu lỗi nhưng gây phức tạp và dữ liệu có thể không nhất quán; mở rộng dọc đơn giản nhưng là điểm lỗi duy nhất (pp. 25–26). — confidence: high
- Bộ đệm đánh đổi dung lượng lấy tốc độ; ghi sau (write-back) giúp giảm độ trễ và cho thông lượng cao với ứng dụng ghi nhiều, nhưng có nguy cơ mất dữ liệu nếu lớp đệm gặp sự cố (p. 18); không bao giờ dùng bộ đệm làm nơi lưu trữ vĩnh viễn (pp. 16–19). — confidence: high
- Hầu hết NoSQL hy sinh ACID để lấy hiệu năng và khả năng mở rộng; SQL vẫn tốt hơn khi cần độ tin cậy giao dịch (p. 33). — confidence: high
- Vì mạng không thể ổn định tuyệt đối, CSDL phân tán phải chịu phân vùng (P), nên thực chất phải chọn giữa nhất quán và khả dụng; PACELC thêm đánh đổi độ trễ–nhất quán khi không có phân vùng (pp. 41–42). — confidence: high
- Băm nhất quán chỉ phải di chuyển K/N khoá khi thêm/bớt nút, khác băm modulo phải xáo trộn phần lớn; nút ảo giảm điểm nóng (pp. 48–50). — confidence: high
- Nên bắt đầu bằng monolith; microservices giải một vấn đề tổ chức, không phải viên đạn bạc (p. 63). — confidence: high
- Không có công nghệ API (REST, GraphQL, gRPC) nào tốt hơn tuyệt đối; chọn theo miền và yêu cầu (p. 74). — confidence: high
- Rate limiting trong hệ phân tán gặp hai vấn đề: không nhất quán giữa các nút và điều kiện tranh chấp khi "get-then-set" (p. 81). — confidence: high
- Phỏng vấn thiết kế hệ thống nên đi theo trình tự: làm rõ yêu cầu → ước tính → mô hình dữ liệu → API → thiết kế cấp cao → thiết kế chi tiết → xử lý nút thắt (pp. 91–93). — confidence: high
- Với ứng dụng thời gian thực (nhắn tin, vị trí tài xế), mô hình đẩy qua WebSocket tốt hơn kéo vì kéo tạo nhiều yêu cầu rỗng (pp. 104, 131). — confidence: high
- News feed dùng mô hình lai: đẩy cho người ít follower, kéo cho người nổi tiếng (p. 113). — confidence: high

## Evidence

- Các phép ước tính quy mô trong các case study, ví dụ URL shortener ~40 ghi/giây, ~4.000 đọc/giây, 6 TB trong 10 năm (pp. 94–95); WhatsApp ~24K RPS, ~38 PB trong 10 năm (p. 101); Netflix ~500 TB/ngày (p. 118).
- Bảng "số chín" về thời gian ngừng hoạt động (p. 24), bảng so sánh RAID (p. 26), bảng so sánh REST/GraphQL/gRPC (p. 74), bảng kích thước ô geohash (p. 77).
- Ví dụ dị thường chèn/cập nhật/xoá trên một bảng nhân viên chưa chuẩn hoá (pp. 37–38).
- Hầu như mọi khái niệm đều kèm danh sách sản phẩm thực tế (Redis, Kafka, Cassandra, Nginx, Elasticsearch...), nhưng không có số liệu đo đạc hay thí nghiệm — đây là tài liệu tổng quan, không phải nghiên cứu.

## Related concepts

- [[concepts/scalability]] — mở rộng dọc/ngang, xuyên suốt mọi chương.
- [[concepts/availability]] — số chín, nối tiếp/song song, chịu lỗi, circuit breaker, DR.
- [[concepts/caching]] — chiến lược ghi, chính sách loại bỏ, CDN, LRU trong mọi case study.
- [[concepts/database-replication]] — master–slave, master–master, đồng bộ/bất đồng bộ.
- [[concepts/data-partitioning]] — sharding, tiêu chí phân vùng, băm nhất quán, federation.
- [[concepts/cap-theorem]] — CAP, PACELC, ACID vs BASE.
- [[concepts/asynchronous-messaging]] — hàng đợi, pub/sub, broker, EDA.
- [[concepts/system-design-interview]] — khung bảy bước và năm case study.
- [[concepts/load-balancing]] — lớp 4/7, thuật toán định tuyến, điểm lỗi duy nhất.
- [[concepts/consistent-hashing]] — vòng băm, K/N khoá, nút ảo; dùng trong cả năm case study.
- [[concepts/database-indexing]] — chỉ mục dày/thưa, chuẩn hoá, phi chuẩn hoá.
- [[concepts/distributed-transactions]] — 2PC, 3PC, saga.
- [[concepts/microservices]] — monolith vs microservices, cạm bẫy, API gateway.
- [[concepts/event-driven-architecture]] — EDA, event sourcing, CQRS.
- [[concepts/api-design]] — REST, GraphQL, gRPC, BFF.
- [[concepts/real-time-communication]] — long polling, WebSocket, SSE.
- [[concepts/rate-limiting]] — năm thuật toán và vấn đề trong hệ phân tán.
- [[concepts/circuit-breaker]] — ba trạng thái, thất bại nhanh.
- [[concepts/geospatial-indexing]] — geohash, quadtree trong Uber.

## Related sources

_Chưa có nguồn nào khác trong wiki._

## People

- [[people/karan-pratap-singh]] — tác giả khoá học.
- Những người được nhắc tới nhưng chưa có trang riêng: Phil Karlton (câu nói về cache invalidation, p. 16), Daniel J. Abadi (PACELC, p. 42), Greg Young (CQRS, p. 66), Sam Newman (BFF, p. 69), Roy Fielding (REST, p. 70), Gustavo Niemeyer (geohash, p. 76), Martin Kleppmann và Chris Richardson (tài liệu đọc thêm, p. 134).

## Open questions

- Tác giả được xác nhận gián tiếp: trang 1 viết khoá học "cũng có sẵn trên trang web của tôi và dưới dạng sách điện tử trên leanpub", và mọi liên kết nội bộ trỏ về karanpratapsingh.com (p. 1). Năm 2022 vẫn chỉ là suy đoán — PDF không ghi năm.
- Đây là bản dịch máy; nhiều thuật ngữ bị dịch sai hoặc lệch nghĩa (ví dụ "Tìm nguồn cung ứng sự kiện" cho event sourcing, "đột kích" cho RAID). Khi cần chính xác nên đối chiếu bản gốc tiếng Anh.
- Nguồn có vài chỗ không nhất quán: Twitter giả định 200 triệu DAU nhưng bảng ghi 100 triệu (pp. 109–110); KGS ghi 300 GB nhưng công thức cho ~390 GB (p. 97); xếp PostgreSQL vào loại "CA" trong khi lập luận rằng hệ phân tán phải chọn P (p. 41).
- Các nguồn được tham khảo nhưng chưa có trong wiki: System Design Primer (donnemartin), Grokking the System Design Interview, System Design Interview – An Insider's Guide, bài giảng Distributed Systems của Martin Kleppmann, microservices.io (pp. 134–135).
- Những chủ đề thiếu: mức cô lập giao dịch, mã hoá đầu-cuối, idempotency trong thanh toán, quan sát hệ thống (observability).

## Notes

Ghi chú đọc theo từng phần (có trích số trang, trích dẫn đã được đối chiếu với PDF):

1. [[readings/system-design/01-mo-dau-va-mang-co-ban]] — Mở đầu và mạng cơ bản (pp. 1–10)
2. [[readings/system-design/02-can-bang-tai-phan-cum-bo-nho-dem]] — Cân bằng tải, phân cụm, bộ nhớ đệm (pp. 10–19)
3. [[readings/system-design/03-cdn-proxy-kha-dung-mo-rong-luu-tru]] — CDN, proxy, khả dụng, mở rộng, lưu trữ (pp. 19–27)
4. [[readings/system-design/04-co-so-du-lieu-sql-nosql-sao-chep-chi-muc]] — Cơ sở dữ liệu (pp. 27–39)
5. [[readings/system-design/05-nhat-quan-giao-dich-sharding]] — Nhất quán, giao dịch, sharding (pp. 39–52)
6. [[readings/system-design/06-n-tang-nhan-tin-microservices]] — N tầng, nhắn tin, microservices (pp. 52–63)
7. [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]] — EDA, CQRS, API, giao tiếp thời gian thực (pp. 63–76)
8. [[readings/system-design/08-van-hanh-do-tin-cay-bao-mat]] — Vận hành, độ tin cậy, bảo mật (pp. 76–91)
9. [[readings/system-design/09-phong-van-url-shortener-whatsapp]] — Phỏng vấn, URL shortener, WhatsApp (pp. 91–108)
10. [[readings/system-design/10-twitter-netflix]] — Twitter, Netflix (pp. 108–126)
11. [[readings/system-design/11-uber-va-phu-luc]] — Uber, bước tiếp theo, tài liệu tham khảo (pp. 126–135)
