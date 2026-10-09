---
id: load-balancing
title: "Cân bằng tải (Load balancing)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [scalability, availability, consistent-hashing, microservices]
confidence: medium
tags: [system-design, networking]
---

## Definition

Cân bằng tải là việc phân phối lưu lượng đến nhiều máy chủ hoặc tài nguyên, và chỉ gửi yêu cầu tới những tài nguyên đang hoạt động. Bộ cân bằng tải đứng trước nhóm máy chủ, chuyển lưu lượng khỏi máy bị hỏng và tự động dùng máy mới được thêm vào. Đây là thành phần giúp mở rộng theo chiều ngang trở nên khả thi.

## Variants

- **Lớp 4 / lớp 7** — lớp 4 định tuyến theo thông tin mạng (IP, cổng) và không đọc nội dung; lớp 7 đọc toàn bộ yêu cầu và định tuyến theo nội dung.
- **Thuật toán định tuyến** — round-robin, round-robin có trọng số, ít kết nối nhất, thời gian phản hồi ít nhất, băng thông tối thiểu, theo băm.
- **Phiên cố định (sticky session)** — gán một người dùng vào cùng một máy để giữ trạng thái phiên.
- **Cân bằng tải bằng DNS** — đơn giản nhưng kém tin cậy vì DNS không kiểm tra máy chủ còn sống hay không.
- **Proxy ngược (reverse proxy)** — có thể làm bộ cân bằng tải, nhưng bộ cân bằng tải không làm được mọi việc của proxy ngược.

## Đánh đổi

- Bản thân bộ cân bằng tải có thể là điểm lỗi duy nhất. Nguồn đề xuất chạy thêm một (hoặc N) bộ cân bằng ở chế độ cụm, theo kiểu chủ động–bị động.
- Khác với phân cụm: các máy sau bộ cân bằng tải không biết nhau, còn máy trong một cụm biết nhau và cùng làm một việc.
- Phiên cố định giúp giữ trạng thái nhưng làm giảm khả năng chịu lỗi và mở rộng (nguồn nhắc lại điều này khi bàn rate limiting phân tán).

## Trong các case study

- Ở bước xử lý nút thắt, cả năm case study đều đề xuất đặt bộ cân bằng tải giữa máy khách, máy chủ, CSDL và máy chủ bộ đệm (pp. 100, 108, 117, 125, 134).
- WhatsApp dùng API gateway thay cho nhiều bộ cân bằng tải lớp 4/lớp 7 riêng cho từng giao thức (HTTP, WebSocket, TCP/IP), vì dựng riêng từng cái rất tốn kém.

## Key sources

- [[sources/system-design]] — lớp 4/7, thuật toán, tính năng, ví dụ sản phẩm (pp. 10–13); proxy ngược (p. 23); WhatsApp (p. 107); case study (pp. 100, 108, 117, 125, 134).
- Ghi chú đọc: [[readings/system-design/02-can-bang-tai-phan-cum-bo-nho-dem]], [[readings/system-design/03-cdn-proxy-kha-dung-mo-rong-luu-tru]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/scalability]]
- [[concepts/availability]]
- [[concepts/consistent-hashing]]
- [[concepts/microservices]]

## Mentioned in

## Notes
