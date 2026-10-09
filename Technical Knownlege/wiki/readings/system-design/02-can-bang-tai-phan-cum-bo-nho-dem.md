---
id: readings/system-design/02-can-bang-tai-phan-cum-bo-nho-dem
title: "Phần 2: Cân bằng tải, phân cụm, bộ nhớ đệm (pp. 10–19)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 2
pages: "10-19"
---

Part 2 of [[sources/system-design]] (pp. 10–19).

## Question this unit answers

Làm sao để một hệ thống phục vụ được nhiều yêu cầu hơn, nhanh hơn và bền hơn bằng cách dùng nhiều máy (cân bằng tải, phân cụm) và giữ dữ liệu hay dùng ở chỗ nhanh (bộ nhớ đệm)?

## Key terms

- **Cân bằng tải (load balancing)** — phân phối lưu lượng đến nhiều tài nguyên, chỉ gửi yêu cầu tới tài nguyên đang trực tuyến (p. 10).
- **Bộ cân bằng tải lớp 4 / lớp 7** — lớp 4 định tuyến theo thông tin mạng (IP), không đọc nội dung; lớp 7 đọc toàn bộ yêu cầu và định tuyến theo nội dung (p. 11).
- **Thuật toán định tuyến** — round-robin, round-robin có trọng số, ít kết nối nhất, thời gian phản hồi ít nhất, băng thông tối thiểu, băm (pp. 11–12).
- **Phiên cố định (sticky session)** — gán cùng một người dùng vào cùng một tài nguyên để giữ trạng thái phiên (p. 12).
- **Cụm (cluster)** — nhóm hai hay nhiều máy chạy song song vì một mục tiêu chung, hoạt động như một hệ thống duy nhất (pp. 13–14).
- **Chủ động–chủ động / chủ động–bị động** — hai cấu hình cụm sẵn sàng cao phổ biến nhất (pp. 14–15).
- **Cache hit / cache miss** — tìm thấy / không tìm thấy dữ liệu trong bộ đệm (pp. 16–17).
- **Ghi xuyên (write-through), ghi vòng (write-around), ghi sau (write-back)** — ba chiến lược ghi của bộ đệm (pp. 17–18).
- **Chính sách loại bỏ (eviction)** — FIFO, LIFO, LRU, MRU, LFU, thay thế ngẫu nhiên (p. 18).
- **Bộ đệm phân tán / bộ đệm toàn cục** — gộp RAM của nhiều máy thành một kho; hoặc một bộ đệm chung cho mọi nút ứng dụng (pp. 18–19).

## Propositions

- Bộ cân bằng tải đứng trước các máy chủ, chuyển hướng lưu lượng khỏi máy chết và tự động dùng máy mới được thêm vào (p. 10).
- Cân bằng tải bằng DNS kém tin cậy vì DNS không kiểm tra máy chủ có đang hoạt động hay không (p. 11).
- Bản thân bộ cân bằng tải có thể là điểm lỗi duy nhất; cách khắc phục là chạy thêm bộ cân bằng thứ hai (hoặc N) ở chế độ cụm, active–passive (p. 12).
- Khác biệt giữa phân cụm và cân bằng tải: máy trong cụm biết nhau và cùng làm một việc; máy sau bộ cân bằng tải không biết nhau (p. 15).
- Thách thức lớn nhất của phân cụm là độ phức tạp cài đặt, bảo trì, giám sát và đồng bộ lưu trữ (p. 15).
- Bộ đệm đánh đổi dung lượng lấy tốc độ, dựa trên nguyên lý "dữ liệu được yêu cầu gần đây có thể được yêu cầu lại" (p. 16).
- Ghi sau cho độ trễ thấp và thông lượng cao nhưng có nguy cơ mất dữ liệu nếu lớp đệm gặp sự cố (p. 18).
- Không nên dùng bộ đệm khi truy cập đệm chậm ngang kho chính, khi yêu cầu ít lặp lại, hoặc khi dữ liệu thay đổi liên tục; và không bao giờ coi bộ đệm là nơi lưu trữ vĩnh viễn (p. 19).

## Arguments

- **Vì sao cân bằng tải:** trang web lớn phải phục vụ hàng trăm nghìn đến hàng triệu yêu cầu đồng thời; cách mở rộng hiệu quả về chi phí là thêm máy → cần một thành phần phân phối yêu cầu để không máy nào quá tải (p. 10).
- **Chọn chiến lược ghi bộ đệm:** ghi xuyên giữ bộ đệm và CSDL nhất quán nhưng ghi chậm hơn; ghi vòng giảm trễ ghi nhưng tăng cache miss khi đọc lại ngay; ghi sau giảm độ trễ và tăng thông lượng cho ứng dụng ghi nhiều nhưng rủi ro mất dữ liệu → chọn theo tỉ lệ đọc/ghi và mức chịu mất mát (pp. 17–18).

## Evidence

- Danh sách tính năng thường có ở bộ cân bằng tải: tự động mở rộng, phiên cố định, kiểm tra sức khỏe, kết nối liên tục (WebSocket), mã hóa TLS, nén, bộ đệm, ghi log, theo dõi yêu cầu, chuyển hướng (pp. 12–13).
- Ví dụ sản phẩm: AWS ELB, Azure/GCP load balancer, Nginx, HAProxy (p. 13); cụm: Kubernetes, Amazon ECS, Cassandra, MongoDB, Redis (pp. 15–16); bộ đệm: Redis (p. 19).
- Câu nói của Phil Karlton về hai điều khó nhất trong khoa học máy tính (p. 16).

## Quotes

- "Bản thân bộ cân bằng tải có thể là một điểm lỗi duy nhất." (p. 12)
- "Nhưng với cân bằng tải, các máy chủ không nhận biết được nhau." (p. 15)
- "Có nguy cơ mất dữ liệu trong trường hợp lớp bộ nhớ đệm gặp sự cố." (p. 18)
- "không nên sử dụng bộ đệm làm nơi lưu trữ dữ liệu vĩnh viễn" (p. 19)

## Tensions and links

- Tầng 4/7 ở đây dựa trên mô hình OSI của phần 1.
- Loại bỏ theo LRU được dùng lại trong mọi case study ở phần 9–11 (URL shortener, WhatsApp, Twitter, Netflix, Uber).
- Cân bằng tải và phân cụm là hai công cụ chính để đạt [[concepts/availability]] và [[concepts/scalability]] (phần 3).
- Khái niệm liên quan: [[concepts/caching]], [[concepts/load-balancing]].

## Open questions

- Nguồn gộp bộ đệm CPU (L1/L2/L3, "nóng/ấm/lạnh") vào chung phần caching hệ thống phân tán — hai tầng khái niệm khác nhau, dễ gây nhầm.
