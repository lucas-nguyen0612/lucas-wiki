---
id: readings/system-design/04-co-so-du-lieu-sql-nosql-sao-chep-chi-muc
title: "Phần 4: Cơ sở dữ liệu — SQL/NoSQL, sao chép, chỉ mục, chuẩn hoá (pp. 27–39)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 4
pages: "27-39"
---

Part 4 of [[sources/system-design]] (pp. 27–39).

## Question this unit answers

Có những loại cơ sở dữ liệu nào, khi nào chọn SQL hay NoSQL, và làm sao tăng độ bền, tốc độ đọc và tính nhất quán của dữ liệu (sao chép, chỉ mục, chuẩn hoá / phi chuẩn hoá)?

## Key terms

- **DBMS** — phần mềm làm giao diện giữa cơ sở dữ liệu và người dùng/chương trình (p. 27).
- **Cơ sở dữ liệu SQL (quan hệ)** — dữ liệu dạng bảng có quan hệ xác định trước, khoá chính/khoá ngoại, thường tuân theo ACID (pp. 28–29).
- **Materialized view (chế độ xem cụ thể hoá)** — tập dữ liệu tính trước từ một truy vấn, lưu lại để truy vấn nhanh hơn (p. 29).
- **Vấn đề truy vấn N+1** — lớp truy cập dữ liệu chạy thêm N câu SQL để lấy dữ liệu lẽ ra lấy được trong một truy vấn; hay gặp ở ORM và GraphQL (p. 29).
- **NoSQL** — cơ sở dữ liệu không dùng SQL làm ngôn ngữ chính, lược đồ không cố định, tuân theo BASE; gồm tài liệu, khoá–giá trị, đồ thị, chuỗi thời gian, cột rộng, đa mô hình (pp. 29–32).
- **Sao chép (replication)** — chia sẻ thông tin giữa các tài nguyên dư thừa để tăng độ tin cậy, chịu lỗi, khả năng truy cập; kiểu master–slave và master–master; đồng bộ và bất đồng bộ (pp. 33–35).
- **Chỉ mục dày / thưa (dense / sparse index)** — chỉ mục cho mọi hàng / chỉ cho một số hàng (pp. 36–37).
- **Dị thường chèn / cập nhật / xoá** — lỗ hổng dữ liệu do thiết kế bảng phẳng (p. 37).
- **Dạng chuẩn 1NF, 2NF, 3NF, BCNF** — các bậc quy tắc chuẩn hoá (p. 38).
- **Phi chuẩn hoá (denormalization)** — cố ý thêm dữ liệu dư thừa để tránh phép nối tốn kém (p. 39).

## Propositions

- Thách thức khi chạy CSDL quy mô lớn: khối lượng dữ liệu tăng, bảo mật, truy cập thời gian thực, chi phí vận hành, giới hạn mở rộng, yêu cầu chủ quyền dữ liệu (p. 28).
- Nhược điểm của CSDL quan hệ: đắt để duy trì, khó tiến hoá lược đồ, khó mở rộng ngang (p. 29).
- SQL thường mở rộng theo chiều dọc; NoSQL mở rộng theo chiều ngang và nhiều hệ tự phân phối dữ liệu (pp. 32–33).
- Khi cần độ tin cậy của giao dịch, SQL vẫn là lựa chọn tốt hơn; hầu hết NoSQL hy sinh ACID để lấy hiệu năng và khả năng mở rộng (p. 33).
- Chọn SQL khi dữ liệu có cấu trúc, quan hệ, cần join phức tạp và giao dịch; chọn NoSQL khi lược đồ linh hoạt, không cần join, khối lượng dữ liệu và IOPS rất cao (p. 33).
- Master–slave: nếu master ngừng, hệ thống có thể chạy chỉ-đọc cho đến khi một slave được nâng cấp; càng nhiều slave thì độ trễ sao chép càng tăng (pp. 33–34).
- Master–master: cả hai nút cùng đọc/ghi, chuyển đổi dự phòng nhanh, nhưng tính nhất quán lỏng hoặc độ trễ ghi tăng, và phải giải quyết xung đột (pp. 34–35).
- Chỉ mục đổi chi phí lưu trữ và tốc độ ghi lấy tốc độ đọc (p. 35).
- Một quan hệ thường được gọi là "đã chuẩn hoá" khi đạt 3NF; hầu hết quan hệ 3NF không có dị thường chèn/cập nhật/xoá (p. 38).
- Phi chuẩn hoá tăng hiệu năng đọc nhưng giảm hiệu năng ghi, và không có nghĩa là đảo ngược chuẩn hoá (p. 39).

## Arguments

- **Chỉ mục dày hay thưa:** chỉ mục dày tìm nhanh bằng tìm kiếm nhị phân nhưng tốn bộ nhớ và chi phí duy trì khi ghi; chỉ mục thưa ghi nhanh, ít bộ nhớ nhưng đọc chậm hơn vì phải quét sau tìm kiếm nhị phân, và chỉ dùng được với dữ liệu có thứ tự (pp. 36–37).
- **Vì sao phi chuẩn hoá trong hệ phân tán:** khi dữ liệu đã bị chia bằng liên kết (federation) và sharding, join qua mạng càng phức tạp → phi chuẩn hoá tránh được join đó, chấp nhận dữ liệu dư thừa và rủi ro không nhất quán (p. 39).

## Evidence

- Ví dụ bảng nhân viên chưa chuẩn hoá (Peter, Brian, Hailey, Steve) minh hoạ cả ba loại dị thường: chèn người chưa có đội, cập nhật Hailey ở hai hàng, xoá đội B làm mất tên người (pp. 37–38).
- Ví dụ sản phẩm: PostgreSQL, MySQL, MariaDB, Aurora (p. 29); MongoDB, DynamoDB, Redis, Neo4j, InfluxDB, Cassandra, BigTable, Cosmos DB (pp. 30–32).

## Quotes

- "Hầu hết các giải pháp NoSQL đều hy sinh việc tuân thủ ACID để có được hiệu suất và khả năng mở rộng." (p. 33)
- "Càng đọc nhiều Slave thì chúng ta càng phải sao chép nhiều, điều này sẽ làm tăng độ trễ của quá trình sao chép." (p. 34)
- "Nó cố gắng cải thiện hiệu suất đọc nhưng lại làm giảm hiệu suất ghi." (p. 39)

## Tensions and links

- Mâu thuẫn tiềm ẩn: nhược điểm của CSDL tài liệu liệt kê "Không có sơ đồ" vừa là ưu điểm vừa là nhược điểm (p. 30) — là cách tác giả nhấn mạnh sự đánh đổi, không phải lỗi.
- ACID/BASE được nhắc ở đây nhưng định nghĩa ở phần 5.
- Sao chép và phi chuẩn hoá là nền cho [[concepts/database-replication]] và cho các case study (bản sao đọc, dữ liệu dư thừa trong News Feed Twitter).
- Khái niệm liên quan: [[concepts/cap-theorem]], [[concepts/database-indexing]], [[concepts/scalability]].

## Open questions

- Bản dịch gọi "Khóa thay thế" cho cả alternate key và surrogate key (p. 37) — cần tra bản gốc để phân biệt.
