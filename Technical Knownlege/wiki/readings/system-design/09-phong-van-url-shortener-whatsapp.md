---
id: readings/system-design/09-phong-van-url-shortener-whatsapp
title: "Phần 9: Phỏng vấn thiết kế hệ thống, URL shortener, WhatsApp (pp. 91–108)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 9
pages: "91-108"
---

Part 9 of [[sources/system-design]] (pp. 91–108).

## Question this unit answers

Nên tiến hành một buổi phỏng vấn thiết kế hệ thống theo trình tự nào, và trình tự đó áp dụng ra sao cho hai bài toán cụ thể: dịch vụ rút gọn URL và ứng dụng nhắn tin kiểu WhatsApp?

## Key terms

- **Yêu cầu chức năng / phi chức năng / mở rộng** — hệ thống phải làm gì / các ràng buộc chất lượng (độ trễ, sẵn sàng, mở rộng) / "có thì tốt" (pp. 91–92).
- **Ước tính và ràng buộc (back-of-the-envelope)** — tính quy mô: tỉ lệ đọc/ghi, RPS, băng thông, lưu trữ, bộ đệm (pp. 91–92).
- **Base62 / MD5 / bộ đếm / KGS** — bốn cách sinh khoá ngắn cho URL; KGS (key generation service) sinh sẵn khoá duy nhất (pp. 96–97).
- **ZooKeeper cấp dải bộ đếm** — mỗi máy chủ nhận một dải số riêng để tránh trùng (p. 97).
- **Dọn dẹp tích cực / thụ động** — xoá link hết hạn định kỳ bằng dịch vụ riêng / xoá lười khi có người truy cập (p. 99).
- **Mô hình kéo / đẩy** — client hỏi định kỳ (long polling) / server đẩy qua kết nối lâu dài (WebSocket, SSE) (p. 104).
- **Heartbeat (nhịp tim)** — client ping định kỳ để báo đang hoạt động, dùng cho "last seen" (p. 105).

## Propositions

- Phỏng vấn thiết kế hệ thống không có một đáp án cụ thể; điểm độc đáo là tính hai chiều giữa ứng viên và người phỏng vấn (p. 91).
- Trình tự đề xuất: làm rõ yêu cầu → ước tính → mô hình dữ liệu → thiết kế API → thiết kế thành phần cấp cao → thiết kế chi tiết → tìm và xử lý nút thắt (pp. 91–93).
- Tránh các phát biểu kiểu "Tôi tin rằng cơ sở dữ liệu NoSQL tốt hơn, cơ sở dữ liệu SQL không có khả năng mở rộng"; hãy khiêm tốn về những gì mình biết và không biết (p. 92).
- URL shortener là hệ thống đọc nhiều (giả định đọc/ghi 100:1) → cần bản sao chỉ-đọc, bộ đệm (pp. 94, 100).
- Base62 đơn giản nhưng không chống trùng; MD5 gây trùng và tốn tính lại; bộ đếm đơn là điểm lỗi duy nhất → dùng ZooKeeper cấp dải hoặc KGS (pp. 96–97).
- Vì dữ liệu URL không có quan hệ chặt, NoSQL (DynamoDB, Cassandra, MongoDB) là lựa chọn tốt hơn (p. 95).
- Luồng đọc URL: hỏi bộ đệm → nếu trượt thì hỏi CSDL và trả HTTP 301 → không có thì HTTP 404 (p. 98).
- WhatsApp: mô hình dữ liệu có vẻ quan hệ, nhưng không nên để tất cả trong một CSDL — chia dữ liệu theo dịch vụ, mỗi dịch vụ sở hữu bảng của mình (pp. 102–103).
- Mô hình kéo không mở rộng được vì đa số phản hồi rỗng; đẩy bằng WebSocket tốt hơn vì song công (pp. 104–105).
- Thông báo đẩy dùng hàng đợi tin (không phải pub/sub thuần) vì mỗi nền tảng thiết bị xử lý thông báo khác nhau qua FCM/APNS (p. 105).
- Bộ đệm trong ứng dụng nhắn tin phải cẩn thận vì người dùng muốn dữ liệu mới nhất → chỉ đệm tin cũ, thêm phân trang (p. 106).

## Arguments

- **Ước tính URL shortener:** 100 triệu link mới/tháng → ~40 ghi/giây; ×100 → ~4.000 đọc/giây; 500 byte/bản ghi × 12 tỷ bản ghi trong 10 năm → ~6 TB; theo quy tắc 80/20, đệm 20% của ~350 triệu yêu cầu/ngày → ~35 GB/ngày (pp. 94–95).
- **Ước tính WhatsApp:** 50 triệu DAU × 40 tin/ngày → 2 tỷ tin/ngày (~24K RPS); 100 byte/tin → ~200 GB/ngày; 5% là media × 100 KB → ~10 TB/ngày; 10 năm → ~38 PB; băng thông ~120 MB/giây (p. 101).
- **Vì sao API gateway cho WhatsApp:** hệ thống dùng nhiều giao thức (HTTP, WebSocket, TCP/IP); dựng bộ cân bằng tải L4/L7 riêng cho từng giao thức rất tốn kém → một gateway hỗ trợ đa giao thức (p. 107).

## Evidence

- Bảng ước tính cấp cao cho URL shortener (p. 95) và WhatsApp (p. 101).
- Không gian khoá Base62: 62^6 ≈ 56,8 tỷ; 62^7 ≈ 3,5 nghìn tỷ (p. 96).
- API: `createURL`, `getURL`, `deleteURL` với khoá API để giới hạn tốc độ (pp. 95–96); `getAll`, `getMessages`, `sendMessage`, `joinGroup`/`leaveGroup` (pp. 103–104).
- Dịch vụ WhatsApp: user, chat (WebSocket), notification, presence, media (p. 104).
- "Sự thật thú vị": WhatsApp xoá media trên máy chủ sau khi người dùng tải xuống (p. 107).

## Quotes

- "Làm rõ yêu cầu" (p. 91)
- "hãy khiêm tốn về những gì bạn biết và những gì bạn không biết" (p. 92)
- "Đây là giải pháp đơn giản nhất ở đây, nhưng nó không đảm bảo các khóa không trùng lặp hoặc chống va chạm." (p. 96)
- "Cách tiếp cận mô hình kéo không thể mở rộng vì nó sẽ tạo ra chi phí yêu cầu không cần thiết trên máy chủ của chúng tôi" (p. 104)

## Tensions and links

- Mâu thuẫn số học trong nguồn: KGS "56,8 tỷ khóa dài 6 ký tự duy nhất, điều này sẽ dẫn đến việc chúng tôi phải lưu trữ 300 GB khóa" nhưng công thức cho ~390 GB (p. 97).
- Bước "tìm và xử lý nút thắt" lặp lại gần như nguyên văn ở mọi case study: nhiều phiên bản dịch vụ, bộ cân bằng tải, bản sao đọc, bộ đệm phân tán có bản sao — cho thấy một "công thức" chung cho [[concepts/availability]] và [[concepts/scalability]].
- Dùng lại: sharding + băm nhất quán (phần 5), LRU (phần 2), WebSocket (phần 7), hàng đợi (phần 6), lưu trữ đối tượng/CDN (phần 3), API gateway (phần 7).
- Khung phỏng vấn này là [[concepts/system-design-interview]].
- Khái niệm liên quan: [[concepts/api-design]], [[concepts/asynchronous-messaging]], [[concepts/caching]], [[concepts/consistent-hashing]], [[concepts/data-partitioning]], [[concepts/database-indexing]], [[concepts/database-replication]], [[concepts/load-balancing]], [[concepts/microservices]], [[concepts/real-time-communication]].

## Open questions

- Nguồn không bàn về mã hoá đầu-cuối — một đặc tính cốt lõi của WhatsApp thật.
