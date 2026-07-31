---
type: concept
title: "Thanh khoản"
slug: thanh-khoan
date_added: "2026-07-26"
confidence: unverified
tags:
  - trading
  - smc
  - liquidity
created: "2026-07-26"
updated: "2026-07-26"
---

## Definition

Thanh khoản (liquidity) trong SMC là khối lượng lệnh giao dịch tập trung tại các vùng giá cụ thể, nơi trader nhỏ lẻ thường đặt lệnh chờ (limit order) hoặc dừng lỗ (stop loss). Các tổ chức lớn cần thanh khoản để thực hiện lệnh khối lượng lớn mà không gây trượt giá — họ thường đẩy giá về các vùng thanh khoản này để khớp lệnh, sau đó đảo chiều thị trường. Trong SMC, trader tìm cách xác định các vùng thanh khoản để dự đoán nơi giá sẽ bị hút về, đồng thời tránh bị "quét dừng lỗ".

## Variants

- **Equal Lows (EQL)** — vùng đáy tương đương trong xu hướng tăng, nơi tập trung dừng lỗ của phe mua
- **Equal Highs (EQH)** — vùng đỉnh tương đương trong xu hướng giảm, nơi tập trung dừng lỗ của phe bán
- **Vùng giá thanh khoản** (liquidity zone) — vùng giá tự nhiên nơi trader đặt lệnh chờ mua/bán, thường trùng với hỗ trợ/kháng cự
- **Thanh khoản phía trên/bên dưới** — vùng thanh khoản nằm trên đỉnh cũ hoặc dưới đáy cũ, nơi dừng lỗ của trader bị phá vỡ tập trung

## Key Sources

- [[he-thong-smart-money-concept-smc]] — phần 5 trình bày chi tiết về thanh khoản, EQL/EQH và cách thị trường thu thập thanh khoản

## Related Concepts

- [[order-block]]
- [[break-of-structure]]
- [[cau-truc-thi-truong]]

## Mentioned in

_Chưa có bài tổng hợp nào đề cập đến khái niệm này._

## Notes

- Khái niệm thanh khoản trong SMC khác với định nghĩa thanh khoản truyền thống trong tài chính (khối lượng giao dịch, spread)
- "Quét thanh khoản" (liquidity sweep) là hành động giá phá vỡ một vùng EQL/EQH để kích hoạt dừng lỗ trước khi đảo chiều
