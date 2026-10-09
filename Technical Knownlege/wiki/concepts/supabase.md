---
id: supabase
title: "Supabase: nền tảng backend trên PostgreSQL"
type: concept
created: 2026-10-07
updated: 2026-10-07
key_sources: []
related_concepts: [api-design, real-time-communication, database-replication]
confidence: unverified
tags: [backend, baas, postgres]
---

## Definition

Supabase là nền tảng backend mã nguồn mở xây trên **PostgreSQL**, cung cấp sẵn database, đăng nhập, lưu file, API và realtime để không phải tự dựng server. Có thể dùng bản cloud hoặc tự host. Thường được xem là lựa chọn thay thế Firebase nhưng dùng SQL.

## Variants

Các khả năng chính:

- **Database (Postgres)** — đầy đủ SQL, quan hệ, view, trigger, function, extension.
- **Auto API** — tự sinh REST (PostgREST) và GraphQL từ schema, không cần viết CRUD.
- **Auth** — email/mật khẩu, magic link, OTP, OAuth (Google, GitHub, Apple…), SSO/SAML, MFA; dùng JWT.
- **Row Level Security (RLS)** — phân quyền ngay trong DB, ví dụ "user chỉ thấy dòng của mình".
- **Storage** — lưu file với chính sách quyền, CDN, biến đổi ảnh.
- **Realtime** — nhận thay đổi DB, broadcast và presence qua WebSocket.
- **Edge Functions** — code TypeScript/Deno chạy phía server gần người dùng (webhook, Stripe, LLM…).
- **Vector / AI** — extension `pgvector` cho embedding và tìm kiếm ngữ nghĩa (RAG).
- **Cron & Queues** — `pg_cron` lập lịch và hàng đợi message trong Postgres.

Công cụ đi kèm: Studio (giao diện web), CLI và local dev bằng Docker (migration, branching), client libraries (JS/TS, Flutter, Swift, Kotlin, Python), kết nối Postgres trực tiếp qua pooler Supavisor, backup/PITR/read replicas (gói trả phí), MCP server cho AI agent.

## Đánh đổi

- **RLS phải bật và viết đúng** — đây là lỗi bảo mật phổ biến nhất khi dùng Supabase.
- Logic phức tạp vẫn cần Edge Functions hoặc server riêng.
- Gói free bị giới hạn: project bị tạm dừng khi không hoạt động, có hạn mức DB, storage, bandwidth.
- Dựa trên Postgres nên ít bị khóa nhà cung cấp: có thể xuất DB và chạy nơi khác.

## Use case

MVP hoặc SaaS nhanh; app mobile/web có đăng nhập, dữ liệu và file; ứng dụng realtime (chat, cộng tác); ứng dụng AI/RAG; backend nội bộ và dashboard admin.

## Key sources

- Ghi chú gốc: raw/notes/2026-10-07-supabase.md (tổng quan từ cuộc trò chuyện, chưa đối chiếu tài liệu chính thức).

## Related concepts

- [[concepts/api-design]] — Supabase tự sinh REST/GraphQL.
- [[concepts/real-time-communication]] — tính năng Realtime dùng WebSocket.
- [[concepts/database-replication]] — read replicas ở gói trả phí.

## Mentioned in

## Notes

Giá và giới hạn gói thay đổi thường xuyên; kiểm tra tại supabase.com/pricing.
