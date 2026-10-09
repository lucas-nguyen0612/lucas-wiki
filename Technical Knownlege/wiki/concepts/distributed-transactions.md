---
id: distributed-transactions
title: "Giao dịch phân tán (Distributed transactions)"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [cap-theorem, microservices, event-driven-architecture]
confidence: medium
tags: [distributed-systems, database]
---

## Definition

Giao dịch là một chuỗi thao tác được xem như một "đơn vị công việc": hoặc tất cả thành công, hoặc không thao tác nào có hiệu lực. Giao dịch phân tán là giao dịch trải trên hai hay nhiều cơ sở dữ liệu. Khó khăn là giữ được tính đúng đắn đó khi các máy có thể hỏng hoặc mất liên lạc giữa chừng.

## Variants

- **Cam kết hai pha (2PC)** — bộ điều phối hỏi mọi nút "sẵn sàng chưa", rồi ra lệnh cam kết hoặc huỷ.
- **Cam kết ba pha (3PC)** — thêm pha tiền cam kết để mọi pha đều có thể hết giờ chờ, tránh chờ vô hạn.
- **Saga** — chuỗi giao dịch cục bộ; mỗi bước phát sự kiện kích hoạt bước tiếp theo, lỗi thì chạy giao dịch bù trừ. Điều phối kiểu vũ đạo (choreography) hoặc nhạc trưởng (orchestration).

## Đánh đổi

- 2PC là giao thức chặn và gặp vấn đề khi một nút hoặc chính bộ điều phối gặp sự cố.
- Saga tránh được việc chặn, nhưng khó gỡ lỗi, có nguy cơ phụ thuộc vòng, thiếu cô lập dữ liệu và khó kiểm thử.
- Nguồn không bàn các mức cô lập giao dịch (isolation levels) — cần nguồn khác.

## Trong các case study

- Uber bọc logic ghép chuyến trong mutex và yêu cầu mọi hành động mang tính giao dịch để tránh hai khách cùng được ghép một tài xế.

## Key sources

- [[sources/system-design]] — trạng thái giao dịch (pp. 42–43); 2PC, 3PC, saga (pp. 43–46); Uber (p. 132).
- Ghi chú đọc: [[readings/system-design/05-nhat-quan-giao-dich-sharding]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/cap-theorem]]
- [[concepts/microservices]]
- [[concepts/event-driven-architecture]]

## Mentioned in

## Notes
