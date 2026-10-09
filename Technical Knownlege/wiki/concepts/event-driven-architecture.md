---
id: event-driven-architecture
title: "Kiến trúc hướng sự kiện, Event sourcing và CQRS"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [asynchronous-messaging, microservices, distributed-transactions]
confidence: medium
tags: [architecture, messaging]
---

## Definition

Kiến trúc hướng sự kiện (event-driven architecture, EDA) dùng sự kiện để các dịch vụ giao tiếp với nhau, thường bất đồng bộ qua một nhà môi giới tin nhắn. Một sự kiện là một điểm dữ liệu ghi lại thay đổi trạng thái; nó không chỉ định điều gì sẽ xảy ra tiếp theo. Nhà xuất bản không biết ai nhận, và những người nhận không biết nhau, nên các dịch vụ được liên kết lỏng.

## Variants

- **EDA** — gồm nhà sản xuất, bộ định tuyến và người tiêu dùng sự kiện. Các mẫu hiện thực: saga, pub/sub, event sourcing, CQRS.
- **Event sourcing** — lưu toàn bộ chuỗi hành động vào một kho chỉ-ghi-thêm thay vì chỉ lưu trạng thái hiện tại. Khác EDA ở chỗ: EDA dùng sự kiện để *giao tiếp*, event sourcing dùng sự kiện *làm trạng thái*. (Bản dịch gọi là "tìm nguồn cung ứng sự kiện".)
- **CQRS** — tách hành động thành lệnh (command: thay đổi trạng thái, không trả giá trị) và truy vấn (query: không tác dụng phụ). Do Greg Young mô tả đầu tiên.

## Đánh đổi

- Thách thức của EDA: đảm bảo giao hàng, xử lý lỗi, độ phức tạp, xử lý đúng một lần và theo thứ tự.
- Event sourcing là cách ưu tiên để có nhật ký kiểm toán trong hệ thống yêu cầu tuân thủ cao, nhưng cần hạ tầng mạng hiệu quả và sổ đăng ký lược đồ.
- CQRS cho phép tối ưu và mở rộng đọc/ghi độc lập, đổi lại thiết kế phức tạp hơn và phải chấp nhận nhất quán cuối cùng. CQRS thường đi kèm event sourcing: kho sự kiện là mô hình ghi, còn mô hình đọc là các view cụ thể hoá, thường phi chuẩn hoá mạnh.

## Key sources

- [[sources/system-design]] — EDA (pp. 63–65); event sourcing (pp. 65–66); CQRS (pp. 66–67).
- Ghi chú đọc: [[readings/system-design/07-su-kien-cqrs-api-giao-tiep]], [[readings/system-design/05-nhat-quan-giao-dich-sharding]] (saga).

## Related concepts

- [[concepts/asynchronous-messaging]]
- [[concepts/microservices]]
- [[concepts/distributed-transactions]]

## Mentioned in

## Notes
