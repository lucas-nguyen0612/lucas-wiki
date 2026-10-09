---
id: api-design
title: "Thiết kế API: REST, GraphQL, gRPC"
type: concept
created: 2026-09-21
updated: 2026-10-07
key_sources: [system-design]
related_concepts: [microservices, real-time-communication, rate-limiting, supabase]
confidence: medium
tags: [api, system-design]
---

## Definition

Thiết kế API là chọn cách các client và dịch vụ trao đổi dữ liệu với nhau: đơn vị trao đổi là gì, định dạng ra sao, và ai quyết định dữ liệu trả về. Nguồn so sánh ba cách phổ biến là REST, GraphQL và gRPC, cùng các mẫu đặt trước API như API gateway và Backend for Frontend.

## Variants

- **REST** — kiểu kiến trúc do Roy Fielding giới thiệu năm 2000; đơn vị cơ bản là tài nguyên; sáu ràng buộc (giao diện đồng nhất, client–server, không trạng thái, có thể đệm, phân lớp, mã theo yêu cầu).
- **GraphQL** — ngôn ngữ truy vấn cho API do Facebook mở nguồn năm 2015; đơn vị cơ bản là truy vấn, client chỉ lấy đúng trường cần.
- **gRPC** — khung RPC hiệu năng cao, dùng Protocol Buffers làm ngôn ngữ định nghĩa giao diện.
- **API gateway** — điểm truy cập duy nhất giữa client và các dịch vụ phụ trợ; lo xác thực, giám sát, cân bằng tải, bộ đệm, giới hạn tốc độ, ghi log.
- **Backend for Frontend (BFF)** — mỗi loại giao diện có một backend riêng; do Sam Newman mô tả.

## Đánh đổi

- REST đơn giản, đệm tốt, khớp nối thấp, nhưng lấy thừa dữ liệu và cần nhiều vòng khứ hồi ("chatty").
- GraphQL bỏ được lấy thừa, nhưng khó đệm và dễ gặp vấn đề truy vấn N+1.
- gRPC nhẹ, nhanh, truyền hai chiều, nhưng khớp nối cao, quản lý phiên bản khó, hỗ trợ trình duyệt hạn chế và con người không đọc được.
- API gateway có thể thành điểm lỗi duy nhất và nút cổ chai.
- Kết luận của nguồn: không có công nghệ nào tốt hơn tuyệt đối — chọn theo miền và yêu cầu.

## Trong các case study

- Mỗi case study đều có bước thiết kế API (ví dụ `createURL` cho URL shortener, p. 95).
- WhatsApp dùng API gateway vì hệ thống dùng nhiều giao thức (p. 107).
- Ở WhatsApp, Twitter, Netflix và Uber, nguồn gợi ý dùng gRPC thay REST/HTTP cho giao tiếp giữa các dịch vụ vì nhẹ và hiệu quả hơn (pp. 104, 112, 121, 130).

## Key sources

- [[sources/system-design]] — API gateway, BFF (pp. 67–69); REST, GraphQL, gRPC và bảng so sánh (pp. 70–74).
- Ghi chú đọc: [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]], [[readings/system-design/09-phong-van-url-shortener-whatsapp]], [[readings/system-design/10-twitter-netflix]].

## Related concepts

- [[concepts/microservices]]
- [[concepts/real-time-communication]]
- [[concepts/rate-limiting]]
- [[concepts/supabase]]

## Mentioned in

## Notes
