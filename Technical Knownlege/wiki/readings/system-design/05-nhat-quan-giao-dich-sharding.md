---
id: readings/system-design/05-nhat-quan-giao-dich-sharding
title: "Phần 5: Nhất quán, giao dịch, sharding, băm nhất quán, liên kết CSDL (pp. 39–52)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 5
pages: "39-52"
---

Part 5 of [[sources/system-design]] (pp. 39–52).

## Question this unit answers

Khi dữ liệu nằm trên nhiều máy, ta phải đánh đổi những gì về tính nhất quán, và làm sao chia dữ liệu và giữ giao dịch đúng qua nhiều cơ sở dữ liệu?

## Key terms

- **ACID** — nguyên tử (atomicity), nhất quán (consistency), cô lập (isolation), bền vững (durability) (pp. 39–40).
- **BASE** — khả dụng cơ bản (basically available), trạng thái mềm (soft state), nhất quán cuối cùng (eventual consistency) (p. 40).
- **Định lý CAP** — hệ phân tán chỉ đảm bảo được hai trong ba: nhất quán (C), khả dụng (A), chịu phân vùng (P) (pp. 40–41).
- **Định lý PACELC** — mở rộng CAP: khi có phân vùng (P) chọn A hay C; khác đi (E), khi chạy bình thường, chọn độ trễ (L) hay nhất quán (C); do Daniel J. Abadi mô tả (p. 42).
- **Giao dịch (transaction)** — chuỗi thao tác được xem là một "đơn vị công việc"; các trạng thái: đang hoạt động, cam kết một phần, đã cam kết, thất bại, huỷ bỏ, chấm dứt (pp. 42–43).
- **Giao dịch phân tán** — tập thao tác trên hai hay nhiều CSDL; giải pháp: cam kết hai pha (2PC), cam kết ba pha (3PC), saga (pp. 43–46).
- **Saga** — chuỗi giao dịch cục bộ, mỗi bước phát sự kiện kích bước tiếp; lỗi thì chạy giao dịch bù trừ; điều phối kiểu vũ đạo (choreography) hoặc nhạc trưởng (orchestration) (pp. 45–46).
- **Phân vùng dữ liệu** — ngang (sharding) hoặc dọc (theo cột) (p. 46).
- **Tiêu chí phân vùng** — theo băm, theo danh sách, theo phạm vi, tổng hợp (p. 47).
- **Băm nhất quán (consistent hashing)** — đặt cả khoá và nút trên một vòng băm, định tuyến tới nút gần nhất theo chiều kim đồng hồ; chỉ K/N khoá phải di chuyển khi thêm/bớt nút (pp. 48–50).
- **Nút ảo (VNode)** — mỗi nút vật lý chiếm nhiều vị trí trên vòng để tải đều hơn (p. 50).
- **Liên kết CSDL (federation)** — chia CSDL theo chức năng, nhiều CSDL vật lý hiện ra như một CSDL logic (pp. 51–52).

## Propositions

- Không có câu trả lời đúng chung cho ACID hay BASE; chọn theo yêu cầu ứng dụng. BASE buộc lập trình viên tự lo tính nhất quán; ACID phù hợp khi độ tin cậy dữ liệu là bắt buộc (p. 40).
- Vì mạng không bao giờ ổn định tuyệt đối, CSDL phân tán phải chọn P, nên thực chất là đánh đổi giữa C và A (p. 41).
- Ví dụ phân loại: CA — PostgreSQL, MariaDB; CP — MongoDB, HBase; AP — Cassandra, CouchDB (pp. 41–42).
- PACELC ra đời vì CAP không nói gì về hiệu năng hay độ trễ (p. 42).
- 2PC là giao thức chặn, và gặp vấn đề khi một nút hoặc chính bộ điều phối gặp sự cố (p. 44).
- 3PC thêm pha tiền cam kết để mọi pha đều có thể hết giờ chờ, tránh chờ vô hạn (p. 45).
- Saga khó gỡ lỗi, có nguy cơ phụ thuộc vòng, thiếu cô lập dữ liệu, khó kiểm thử (p. 46).
- Sharding có lợi khi mở rộng ngang bằng nhiều máy rẻ hơn mở rộng dọc; nhưng khó join qua nhiều shard và phải cân bằng lại khi dữ liệu lệch (pp. 47–48).
- Băm theo modulo N hỏng khi N đổi: phần lớn yêu cầu phải phân phối lại (p. 49).
- Trên lý thuyết băm nhất quán chia tải đều, thực tế vẫn có điểm nóng; nút ảo giảm điều này (p. 50).

## Arguments

- **Từ CAP sang lựa chọn thực tế:** (1) phân vùng mạng chắc chắn xảy ra → (2) phải chịu được P → (3) khi phân vùng xảy ra, hoặc tắt nút không nhất quán (CP), hoặc cho nút trả dữ liệu cũ (AP) (pp. 41–42).
- **Vì sao cần băm nhất quán:** băm modulo gắn chặt với số nút → thêm/bớt nút làm xáo trộn gần hết khoá → cần một sơ đồ không phụ thuộc trực tiếp số nút → vòng băm chỉ di chuyển K/N khoá (pp. 48–49).
- **Ví dụ phản bác của PACELC:** theo CAP, một CSDL trả lời sau 30 ngày vẫn là "khả dụng" — vô lý trong thực tế, nên cần thêm trục độ trễ (p. 42).

## Evidence

- Công thức băm modulo `Hash(key) mod N` và công thức R = K/N (pp. 48–49).
- Ví dụ thực tế băm nhất quán: phân vùng dữ liệu Apache Cassandra, phân phối tải trong Amazon DynamoDB (p. 51).

## Quotes

- "Không có câu trả lời đúng cho việc ứng dụng của chúng ta cần mô hình nhất quán ACID hay BASE." (p. 40)
- "Chúng ta đang sống trong thế giới vật lý và không thể đảm bảo tính ổn định của mạng" (p. 41)
- "Mẫu Saga đặc biệt khó gỡ lỗi." (p. 46)

## Tensions and links

- Việc liệt kê PostgreSQL/MariaDB là "CA" trong khi đã lập luận rằng hệ phân tán buộc phải chọn P là điểm dễ gây tranh cãi — CA chỉ có ý nghĩa với hệ không phân tán.
- Saga dùng sự kiện → nối với kiến trúc hướng sự kiện và microservices ở phần 6–7.
- Băm nhất quán được dùng lại trong case study URL shortener và WhatsApp để phân vùng dữ liệu (phần 9).
- Đây là phần trung tâm cho [[concepts/cap-theorem]] và [[concepts/data-partitioning]] (bao gồm băm nhất quán).
- Khái niệm liên quan: [[concepts/consistent-hashing]], [[concepts/distributed-transactions]], [[concepts/event-driven-architecture]].

## Open questions

- Nguồn không nêu mức cô lập giao dịch (isolation levels) cụ thể — khoảng trống cần nguồn khác.
