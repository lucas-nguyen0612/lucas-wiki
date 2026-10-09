---
id: readings/system-design/06-n-tang-nhan-tin-microservices
title: "Phần 6: Kiến trúc N tầng, nhắn tin, pub/sub, ESB, monolith và microservices (pp. 52–63)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 6
pages: "52-63"
---

Part 6 of [[sources/system-design]] (pp. 52–63).

## Question this unit answers

Nên chia một ứng dụng thành những phần nào, các phần đó nói chuyện với nhau ra sao (đồng bộ, hàng đợi, pub/sub, ESB), và khi nào thật sự cần microservices?

## Key terms

- **Kiến trúc N tầng** — chia ứng dụng thành lớp logic và tầng vật lý; lớp đóng (chỉ gọi lớp ngay dưới) và lớp mở (gọi bất kỳ lớp dưới); ví dụ 3 tầng: trình bày, nghiệp vụ, truy cập dữ liệu (pp. 52–53).
- **Nhà môi giới tin nhắn (message broker)** — phần mềm xác thực, lưu, định tuyến và gửi tin giữa các ứng dụng; hai mô hình: điểm–điểm và pub/sub (p. 54).
- **Nền tảng truyền phát sự kiện (event streaming)** — chỉ hỗ trợ pub/sub, mở rộng tốt hơn nhưng ít đảm bảo giao hàng hơn broker (p. 54).
- **Hàng đợi tin nhắn (message queue)** — giao tiếp bất đồng bộ; mỗi tin được đúng một consumer xử lý một lần (p. 55).
- **At-least-once / exactly-once** — gửi ít nhất một lần (có thể trùng) / chính xác một lần (lọc trùng, thường với hàng đợi FIFO) (p. 56).
- **Dead-letter queue** — hàng đợi chứa tin không xử lý được, để kiểm tra riêng mà không chặn hàng đợi chính (p. 56).
- **Áp lực ngược (backpressure)** — giới hạn kích thước hàng đợi; khi đầy thì trả HTTP 503 để client thử lại với lùi thời gian theo cấp số nhân (pp. 56–57).
- **Xuất bản–đăng ký (pub/sub)** — tin xuất bản lên một chủ đề được đẩy ngay tới mọi subscriber; có fanout, lọc (p. 57–58).
- **ESB (enterprise service bus)** — thành phần tập trung lo tích hợp: chuyển đổi dữ liệu, định tuyến, chuyển giao thức (p. 58).
- **Monolith / monolith mô-đun / microservices** — một khối duy nhất / một khối nhưng chia mô-đun độc lập / tập dịch vụ nhỏ tự trị, mỗi dịch vụ một khả năng kinh doanh trong một bối cảnh giới hạn (bounded context), dữ liệu riêng (pp. 59–61).
- **Monolith phân tán (distributed monolith)** — trông như microservices nhưng liên kết chặt như monolith (p. 62).

## Propositions

- Tách tầng vật lý tăng khả năng mở rộng và phục hồi, nhưng thêm độ trễ mạng (p. 53).
- Broker cho phép bên gửi không cần biết bên nhận ở đâu, có đang chạy không, có bao nhiêu → tách rời các dịch vụ (p. 54).
- Broker là lựa chọn "nhẹ" thay ESB, phù hợp với microservices vốn phổ biến hơn khi ESB mất ưu thế (pp. 54–55).
- Lợi ích hàng đợi: mở rộng, tách rời, hiệu năng (bất đồng bộ), độ tin cậy khi có phần ngoại tuyến (p. 55).
- Khác biệt pub/sub và hàng đợi: trong pub/sub nhà xuất bản không cần biết ai nhận; trong hàng đợi bên gửi thường biết đích (p. 57).
- ESB tập trung dễ thành nút thắt cổ chai và điểm lỗi làm hỏng toàn bộ liên lạc (p. 59).
- Monolith dễ phát triển, gỡ lỗi, hỗ trợ ACID; nhưng khó bảo trì khi lớn, khó mở rộng, mỗi bản cập nhật phải triển khai lại toàn bộ (p. 60).
- Cạm bẫy microservices: ranh giới không theo nghiệp vụ, đánh giá thấp độ khó hệ phân tán, dùng chung CSDL, cố làm mọi thứ ACID thay vì BASE (p. 62).
- Khác biệt microservices và SOA nằm ở phạm vi: SOA tối đa hoá tái sử dụng qua giao diện chung; microservices tối đa hoá tự chủ và tách rời của nhóm (p. 63).
- Nên bắt đầu bằng monolith khi xây hệ thống mới; microservices giải một vấn đề tổ chức, không phải viên đạn bạc (p. 63).

## Arguments

- **Khi nào cần microservices:** tác giả đưa ra danh sách câu hỏi tự kiểm (nhóm có quá lớn cho một codebase? các nhóm có chặn nhau? có giá trị kinh doanh rõ ràng? tổ chức đủ trưởng thành?) → nếu không, không cần tách (p. 63).
- **Lập luận "chúng tôi không phải là Netflix":** Netflix đi đến microservices qua nhiều vòng lặp khi đã xác định rõ vấn đề; sao chép kiến trúc mà không có vấn đề đó là sai (p. 63).
- **Monolith phân tán:** lý do chính để dùng microservices là khả năng mở rộng độc lập; nếu dịch vụ phụ thuộc nhau, dùng chung CSDL, đòi độ trễ thấp giữa nhau → mất lợi ích mà vẫn gánh độ phức tạp (p. 62).

## Evidence

- Danh sách tính năng hàng đợi: push/pull, FIFO, trì hoãn giao hàng, at-least-once, exactly-once, DLQ, thứ tự, poison-pill, bảo mật, task queue, backpressure (pp. 56–57).
- Ví dụ: NATS, Kafka, RabbitMQ, ActiveMQ (p. 55); SQS, ZeroMQ (p. 57); SNS, Google Pub/Sub (p. 58); Azure Service Bus, IBM App Connect, Apache Camel, Fuse ESB (p. 59).

## Quotes

- "Lớp cao hơn có thể sử dụng các dịch vụ ở lớp thấp hơn, nhưng không phải ngược lại." (p. 52)
- "Mỗi tin nhắn chỉ được xử lý một lần bởi một người tiêu dùng." (p. 55)
- "Điều quan trọng là phải hiểu rằng microservice không phải là viên đạn bạc, thay vào đó, chúng giải quyết một vấn đề của tổ chức." (p. 63)
- "nếu doanh nghiệp của bạn không gặp vấn đề phức tạp thì bạn không cần chúng" (p. 63)

## Tensions and links

- Phần ưu điểm của ESB (p. 59) thực ra mô tả lợi ích kiểu microservices ("mỗi vi dịch vụ...") — có vẻ là lỗi biên tập ở bản gốc hoặc bản dịch.
- Pub/sub và hàng đợi là nền của [[concepts/asynchronous-messaging]], dùng lại trong EDA (phần 7) và mọi case study (thông báo qua Kafka/NATS).
- "Thất bại nhanh chóng bằng cách sử dụng bộ ngắt mạch" (p. 62) được giải thích ở phần 8.
- Saga (phần 5) là cách giữ nhất quán dữ liệu khi mỗi microservice có CSDL riêng.
- Khái niệm liên quan: [[concepts/circuit-breaker]], [[concepts/microservices]].

## Open questions

- Nguồn không đề cập cách đo "đủ trưởng thành" cho microservices — lời khuyên còn định tính.
