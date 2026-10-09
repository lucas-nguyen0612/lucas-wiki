---
id: npkill
title: "npkill — dọn thư mục node_modules"
type: concept
created: 2026-10-02
updated: 2026-10-02
key_sources: []
related_concepts: []
confidence: medium
tags: [tooling, nodejs, cli]
---

## Definition

npkill là công cụ dòng lệnh (CLI, chạy trên Node.js) giúp tìm và xóa nhanh các thư mục `node_modules` — cùng một số thư mục build/cache khác — để giải phóng dung lượng ổ đĩa. Mỗi dự án JavaScript có `node_modules` nặng từ hàng trăm MB đến vài GB, nên nhiều dự án cũ dễ chiếm nhiều chỗ mà không được để ý.

## Variants

Cách chạy:

- `npx npkill` — chạy trực tiếp, không cần cài.
- `npm i -g npkill` rồi `npkill` — cài toàn cục.

Tuỳ chọn hữu ích:

- `-d <đường dẫn>` — quét từ thư mục chỉ định.
- `-t <tên>` — tìm thư mục khác (ví dụ `-t dist`, `-t .next`).
- `-s` — sắp xếp theo kích thước.
- `-D` — xóa tất cả (cẩn thận).

Cách hoạt động: quét thư mục hiện tại và các thư mục con, liệt kê kèm dung lượng và thời gian sửa đổi lần cuối; dùng phím mũi tên để chọn, `Space` hoặc `Del` để xóa mục đang chọn.

## Key sources

- Bản gốc: `raw/notes/2026-10-02-npkill.md` (từ cuộc trò chuyện).

## Related concepts

_(chưa có)_

## Mentioned in

_(chưa có)_

## Notes

- Xóa `node_modules` an toàn vì có thể cài lại bằng `npm install`, nhưng tránh xóa của dự án đang làm dở để khỏi mất thời gian cài lại.
- Kiểm tra kỹ đường dẫn trước khi xóa, nhất là khi dùng `-D`.
- Nội dung chưa đối chiếu với tài liệu chính thức của npkill (`confidence: medium`).
