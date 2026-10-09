---
id: readings/system-design/07-su-kien-cqrs-api-giao-tiep
title: "Phần 7: EDA, event sourcing, CQRS, API gateway, REST/GraphQL/gRPC, long polling/WebSocket/SSE (pp. 63–76)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 7
pages: "63-76"
---

Part 7 of [[sources/system-design]] (pp. 63–76).

## Question this unit answers

Các dịch vụ trao đổi với nhau và với máy khách bằng những cách nào — qua sự kiện, qua một cổng API chung, qua kiểu API nào (REST, GraphQL, gRPC), và làm sao máy chủ đẩy dữ liệu thời gian thực về máy khách?

## Key terms

- **Kiến trúc hướng sự kiện (EDA)** — dùng sự kiện để giao tiếp, thường qua broker, bất đồng bộ; gồm nhà sản xuất, bộ định tuyến, người tiêu dùng sự kiện (pp. 63–64).
- **Sự kiện (event)** — điểm dữ liệu thể hiện một thay đổi trạng thái; không chỉ định điều gì sẽ xảy ra tiếp (p. 63).
- **Event sourcing (tìm nguồn cung ứng sự kiện)** — lưu toàn bộ chuỗi hành động vào kho chỉ-ghi-thêm thay vì chỉ lưu trạng thái hiện tại (p. 65).
- **CQRS** — tách hành động thành lệnh (command, thay đổi trạng thái, không trả giá trị) và truy vấn (query, không tác dụng phụ); do Greg Young mô tả đầu tiên (p. 66).
- **API gateway** — điểm truy cập duy nhất giữa máy khách và các dịch vụ phụ trợ, lo xác thực, giám sát, cân bằng tải, bộ đệm, giới hạn tốc độ, ghi log (p. 67).
- **Backend for Frontend (BFF)** — mỗi loại giao diện có một backend riêng; do Sam Newman mô tả (p. 69).
- **REST** — kiểu kiến trúc do Roy Fielding giới thiệu năm 2000; đơn vị cơ bản là tài nguyên; sáu ràng buộc (giao diện đồng nhất, client–server, không trạng thái, có thể đệm, phân lớp, mã theo yêu cầu) (p. 70).
- **GraphQL** — ngôn ngữ truy vấn cho API, do Facebook phát triển và mở nguồn năm 2015; đơn vị cơ bản là truy vấn (p. 71).
- **gRPC** — khung RPC hiệu năng cao, dùng Protocol Buffers làm ngôn ngữ định nghĩa giao diện (pp. 72–73).
- **Long polling / WebSocket / SSE** — ba cách để máy chủ đẩy dữ liệu: giữ yêu cầu mở tới khi có tin / kênh song công toàn phần qua một kết nối TCP / kênh một chiều từ máy chủ (pp. 74–76).

## Propositions

- EDA chỉ đơn giản là một cách đạt liên kết lỏng giữa các dịch vụ; nhà xuất bản không biết ai nhận, người nhận không biết nhau (p. 63).
- Các mẫu hiện thực EDA: saga, pub/sub, event sourcing, CQRS (p. 64).
- Thách thức của EDA: đảm bảo giao hàng, xử lý lỗi, độ phức tạp, xử lý đúng một lần và theo thứ tự (p. 65).
- Event sourcing khác EDA: EDA dùng sự kiện để giao tiếp qua ranh giới dịch vụ; event sourcing dùng sự kiện làm trạng thái — là một trong các mẫu hiện thực EDA (p. 66).
- Event sourcing là cách ưu tiên để có nhật ký kiểm toán trong hệ thống tuân thủ cao, nhưng cần hạ tầng mạng hiệu quả và sổ đăng ký lược đồ (p. 66).
- CQRS thường đi kèm event sourcing: kho sự kiện là mô hình ghi và nguồn sự thật; mô hình đọc là các view cụ thể hoá, thường phi chuẩn hoá mạnh (p. 67).
- API gateway cần vì microservices cung cấp API chi tiết, còn máy khách cần một điểm truy cập; nhược điểm: điểm lỗi duy nhất, có thể thành nút cổ chai (pp. 67–68).
- REST: đơn giản, hỗ trợ bộ đệm tốt, nhưng lấy thừa dữ liệu và nhiều vòng khứ hồi (pp. 70–71). GraphQL: bỏ lấy thừa nhưng khó đệm, dễ gặp N+1 (pp. 71–72). gRPC: nhẹ, nhanh, truyền hai chiều, nhưng hỗ trợ trình duyệt hạn chế và con người không đọc được (p. 73).
- Không có công nghệ API nào tốt hơn tuyệt đối — tập trung vào miền và yêu cầu (p. 74).
- Long polling dễ làm nhưng thường không mở rộng được; WebSocket song công nhưng kết nối đứt không tự phục hồi; SSE đơn giản nhưng một chiều, không hỗ trợ dữ liệu nhị phân (pp. 75–76).

## Arguments

- **Vì sao CQRS:** lệnh và truy vấn đóng vai trò khác nhau → tách ra thì mỗi bên tối ưu và mở rộng độc lập; cái giá là thiết kế phức tạp hơn và phải xử lý nhất quán cuối cùng (pp. 66–67).
- **So sánh API theo 8 tiêu chí** (khớp nối, "chatty", hiệu năng, độ phức tạp, bộ đệm, sinh mã, khả năng khám phá, phiên bản): REST khớp nối thấp nhưng nói nhiều; gRPC hiệu năng tuyệt nhưng khớp nối cao và phiên bản khó (p. 74).
- **Vì sao cần cơ chế đẩy:** web ban đầu theo mô hình client khởi tạo mọi giao dịch → máy chủ không có cách tự đẩy dữ liệu → sinh ra long polling, WebSocket, SSE (p. 74).

## Evidence

- Bảng so sánh REST / GraphQL / gRPC (p. 74).
- Ví dụ REST trên tài nguyên `/users`, lược đồ GraphQL `User`/`Query`, định nghĩa `HelloService` bằng protobuf (pp. 71–73).
- Ví dụ công nghệ: EventBridge, SNS, Kafka, NATS (p. 65); Amazon API Gateway, Apigee, Azure, Kong (p. 69).

## Quotes

- "Kiến trúc hướng sự kiện chỉ đơn giản là một cách để đạt được sự kết nối lỏng lẻo giữa các dịch vụ trong một hệ thống." (p. 63)
- "tìm nguồn cung ứng sự kiện là sử dụng các sự kiện làm trạng thái" (p. 66)
- "Nguyên tắc cốt lõi của CQRS là tách biệt các lệnh và truy vấn." (p. 66)
- "Không có viên đạn bạc nào vì mỗi công nghệ này đều có những ưu điểm và nhược điểm riêng." (p. 74)

## Tensions and links

- API gateway giải vấn đề do microservices tạo ra (phần 6) nhưng lại tái tạo điểm lỗi duy nhất — cùng mẫu với bộ cân bằng tải và proxy ngược (phần 2–3).
- WebSocket được chọn cho case study WhatsApp và Uber; long polling cho cập nhật vị trí tài xế (phần 9, 11).
- gRPC được khuyên cho giao tiếp nội bộ giữa microservices trong các case study.
- Liên quan tới [[concepts/asynchronous-messaging]]; API gateway là một mẫu kiến trúc riêng của phần này.
- Khái niệm liên quan: [[concepts/api-design]], [[concepts/event-driven-architecture]], [[concepts/microservices]], [[concepts/rate-limiting]], [[concepts/real-time-communication]].

## Open questions

- Nguồn gọi gRPC là "tương đối mới" — nhận định này có thể đã lỗi thời.
