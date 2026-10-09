---
id: geospatial-indexing
title: "Chỉ mục không gian: Geohash và Quadtree"
type: concept
created: 2026-09-21
updated: 2026-09-21
key_sources: [system-design]
related_concepts: [database-indexing, real-time-communication, caching]
confidence: medium
tags: [database, geospatial]
---

## Definition

Chỉ mục không gian là cách tổ chức dữ liệu vị trí (kinh độ, vĩ độ) để trả lời nhanh các câu hỏi kiểu "những điểm nào nằm gần đây". Tính khoảng cách Euclid trên mọi bản ghi tốn CPU và không mở rộng được, nên cần cấu trúc chia không gian thành ô.

## Variants

- **Geohash** — mã hoá toạ độ thành một chuỗi Base-32 ngắn; hai điểm có tiền tố chung càng dài thì càng gần nhau. Do Gustavo Niemeyer tạo năm 2008. Độ dài 6 ký tự ≈ ô 1,22 km × 0,61 km; 8 ký tự ≈ 38,2 m × 19,1 m.
- **Quadtree (cây tứ phân)** — cây mà mỗi nút trong có đúng bốn con, chia không gian 2 chiều đệ quy thành bốn góc phần tư; chỉ chia nhỏ một nút khi số điểm vượt ngưỡng.

## Đánh đổi

- Truy vấn SQL kiểu `lat BETWEEN X-R AND X+R AND long BETWEEN Y-R AND Y+R` đơn giản nhưng chậm trên dữ liệu lớn.
- Geohash cho phép so sánh chuỗi tiền tố và lập chỉ mục trong bộ nhớ; quadtree cho truy vấn phạm vi hiệu quả hơn nữa.

## Trong các case study

- Uber dùng quadtree để tìm tài xế gần, cập nhật khi tài xế gửi vị trí mới, và đệm cập nhật mới nhất bằng Redis để giảm tải cho máy chủ quadtree.

## Key sources

- [[sources/system-design]] — geohash (pp. 76–77); quadtree (pp. 77–78); Uber (pp. 131–132).
- Ghi chú đọc: [[readings/system-design/08-van-hanh-do-tin-cay-bao-mat]], [[readings/system-design/11-uber-va-phu-luc]].

## Related concepts

- [[concepts/database-indexing]]
- [[concepts/real-time-communication]]
- [[concepts/caching]]

## Mentioned in

## Notes
