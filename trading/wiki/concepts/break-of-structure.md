---
type: concept
title: "Break of Structure (BOS)"
slug: break-of-structure
date_added: "2026-07-26"
confidence: unverified
tags:
  - trading
  - smc
  - price-action
created: "2026-07-26"
updated: "2026-07-26"
---

## Definition

Break of Structure (BOS) — phá vỡ cấu trúc — là thời điểm giá phá vỡ một đỉnh hoặc đáy đã được xác định trong cấu trúc thị trường hiện tại, báo hiệu sự tiếp diễn hoặc thay đổi của xu hướng. Trong xu hướng tăng, BOS xảy ra khi giá phá vỡ đỉnh trước để tạo đỉnh cao hơn (HH); phá vỡ đáy cao hơn để tạo đáy thấp hơn (LL) là tín hiệu cấu trúc tăng có thể kết thúc. Trong SMC, BOS là tín hiệu then chốt để xác định vùng order block và tìm điểm vào lệnh.

## Variants

- **Phá vỡ cấu trúc bởi thân nến** — thân nến đóng cửa vượt qua mức đỉnh/đáy; tác giả SMC khuyến nghị dùng kiểu này vì độ xác nhận cao hơn
- **Phá vỡ cấu trúc bởi đuôi nến** — đuôi nến (wick) chạm qua mức đỉnh/đáy nhưng thân nến không đóng cửa vượt qua; tín hiệu yếu hơn, dễ bị phá vỡ giả (fakeout)
- **Phá vỡ giả** (fakeout / false break) — giá phá vỡ cấu trúc nhưng nhanh chóng quay đầu, thường là bẫy thanh khoản

## Key Sources

- [[he-thong-smart-money-concept-smc]] — phần 3 trình bày chi tiết về BOS, kèm backtest so sánh hai kiểu phá vỡ

## Related Concepts

- [[cau-truc-thi-truong]]
- [[order-block]]
- [[thanh-khoan]]

## Mentioned in

_Chưa có bài tổng hợp nào đề cập đến khái niệm này._

## Notes

- BOS là viết tắt được sử dụng xuyên suốt trong tài liệu SMC
- Một BOS rõ ràng cần: (1) nến mạnh phá vỡ cấu trúc, (2) không có đuôi nến dài tại điểm phá vỡ (không do dự)
