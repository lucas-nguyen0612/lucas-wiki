---
id: readings/system-design/11-uber-va-phu-luc
title: "Phần 11: Case study Uber, bước tiếp theo, tài liệu tham khảo (pp. 126–135)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 11
pages: "126-135"
---

Part 11 of [[sources/system-design]] (pp. 126–135).

## Question this unit answers

Thiết kế một dịch vụ gọi xe kiểu Uber — trọng tâm là theo dõi vị trí thời gian thực và ghép chuyến với tài xế gần nhất — như thế nào, và người học nên đi tiếp đâu sau khoá học?

## Key terms

- **Hai loại người dùng: khách hàng và tài xế** — yêu cầu chức năng tách riêng cho từng bên (p. 126).
- **Theo dõi vị trí (location tracking)** — mô hình kéo (long polling) hay đẩy (WebSocket/SSE) để gửi vị trí trực tiếp (pp. 130–131).
- **Ghép chuyến (ride matching)** — tìm tài xế lân cận: SQL theo bán kính, geohash, quadtree (pp. 131–132).
- **Đường cong Hilbert** — thuật toán ánh xạ giúp truy vấn phạm vi hiệu quả trên quadtree (p. 132).
- **Mutex** — khoá loại trừ để tránh điều kiện tranh chấp khi nhiều khách cùng đặt xe (p. 132).
- **Định giá đột biến (surge pricing)** — giá tạm tăng khi cầu vượt cung (p. 132).
- **Webhook** — cơ chế nhận dữ liệu thanh toán từ bên xử lý thứ ba (Stripe, PayPal) (p. 133).

## Propositions

- Ước tính: 100 triệu DAU, 1 triệu tài xế, 10 triệu chuyến/ngày; 10 hành động/người → 1 tỷ yêu cầu/ngày (~12K RPS); 400 byte/tin → ~400 GB/ngày, ~1,4 PB trong 10 năm, ~5 MB/giây (pp. 126–127).
- Dịch vụ: khách hàng, tài xế, đi xe (ghép chuyến và tổng hợp quadtree), chuyến đi, thanh toán, thông báo, phân tích (pp. 129–130).
- Luồng: khách yêu cầu → dịch vụ tìm tài xế gần và tính ETA → phát yêu cầu tới tài xế → tài xế chấp nhận → khách thấy vị trí trực tiếp → đón, kết thúc, thu tiền → đánh giá (p. 130).
- Đẩy qua WebSocket là lựa chọn tốt hơn kéo cho vị trí; ứng dụng cần công việc nền để ping GPS khi ở chế độ nền (p. 131).
- Truy vấn SQL `lat BETWEEN X-R AND X+R ...` không mở rộng được và chậm trên dữ liệu lớn (p. 131).
- Quadtree "có vẻ hoàn hảo": cập nhật khi tài xế gửi vị trí mới, đệm cập nhật mới nhất bằng Redis để giảm tải cho máy chủ quadtree (p. 132).
- Sau khi có danh sách tài xế gần, xếp hạng theo đánh giá trung bình, độ liên quan, phản hồi trước đây để thông báo tài xế tốt nhất trước (p. 132).
- Có thể shard theo vùng (ví dụ mã zip), dùng băm nhất quán để giảm lệch tải (p. 133).
- Tài nguyên đề xuất tiếp theo: bài giảng Hệ thống phân tán của Martin Kleppmann, sách System Design Interview, microservices.io của Chris Richardson, serverless, Kubernetes, và blog kỹ thuật của các công ty lớn (pp. 134–135).
- Nguồn tham khảo khi viết khoá học: Cloudflare Learning Center, IBM, Fastly, NS1, Grokking the System Design Interview, System Design Primer, AWS, Microsoft Architecture Patterns, Martin Fowler, PagerDuty, VMware (p. 135).

## Arguments

- **Từ SQL sang không gian chỉ mục:** truy vấn theo hộp bán kính trên bảng lớn chậm → geohash cho phép so sánh chuỗi tiền tố và lập chỉ mục trong bộ nhớ → quadtree cho truy vấn phạm vi hiệu quả và chỉ chia nhỏ nút sau một ngưỡng (pp. 131–132).
- **Tránh đặt trùng tài xế:** nhiều yêu cầu đồng thời có thể cùng ghép một tài xế → bọc logic ghép chuyến trong mutex và làm mọi hành động mang tính giao dịch (p. 132).

## Evidence

- Bảng ước tính cấp cao Uber (p. 127).
- API: `requestRide`, `cancelRide`, `acceptRide`/`denyRide`, `startTrip`/`endTrip`, `rateTrip` (pp. 128–129).
- Truy vấn SQL mẫu tìm tài xế theo bán kính (p. 131).

## Quotes

- "Tuy nhiên, điều này không thể mở rộng được và việc thực hiện truy vấn này trên các tập dữ liệu lớn sẽ khá chậm." (p. 131)
- "Xin chúc mừng, bạn đã hoàn thành khóa học!" (p. 134)

## Tensions and links

- Mutex để chống tranh chấp (p. 132) mâu thuẫn nhẹ với cảnh báo ở phần 8 rằng khoá phân tán dễ thành nút cổ chai — nguồn không bàn cái giá này trong case study.
- Case study này là nơi geohash/quadtree (phần 8), WebSocket (phần 7), giao dịch phân tán (phần 5) và hàng đợi thông báo (phần 9) hội tụ.
- Mục "bảng lượt xem" trong phần phân tích của Uber (p. 133) có vẻ sao chép từ Netflix — dấu hiệu các case study dùng chung khuôn.
- Khái niệm liên quan: [[concepts/consistent-hashing]], [[concepts/data-partitioning]], [[concepts/database-replication]], [[concepts/distributed-transactions]], [[concepts/geospatial-indexing]], [[concepts/load-balancing]], [[concepts/real-time-communication]], [[concepts/system-design-interview]].

## Open questions

- Phần thanh toán chỉ uỷ cho bên thứ ba — không bàn idempotency hay đối soát, vốn là vấn đề thực tế lớn.
