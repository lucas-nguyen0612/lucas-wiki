---
id: readings/system-design/08-van-hanh-do-tin-cay-bao-mat
title: "Phần 8: Geohash, circuit breaker, rate limit, service discovery, SLA, DR, VM/container, OAuth, SSO, TLS (pp. 76–91)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 8
pages: "76-91"
---

Part 8 of [[sources/system-design]] (pp. 76–91).

## Question this unit answers

Những kỹ thuật chuyên biệt nào giúp hệ thống xử lý dữ liệu vị trí, tự bảo vệ trước lỗi dây chuyền và lạm dụng, tìm thấy nhau khi chạy động, cam kết chất lượng dịch vụ, phục hồi sau thảm hoạ, được đóng gói để triển khai, và xác thực/bảo mật giao tiếp?

## Key terms

- **Geohash** — mã hoá toạ độ thành chuỗi Base-32 ngắn; tiền tố chung càng dài thì hai điểm càng gần; do Gustavo Niemeyer tạo năm 2008 (pp. 76–77).
- **Quadtree (cây tứ phân)** — cây mà mỗi nút trong có đúng bốn con, chia không gian 2 chiều đệ quy thành bốn góc phần tư (pp. 77–78).
- **Bộ ngắt mạch (circuit breaker)** — gói lời gọi được bảo vệ, đếm lỗi; vượt ngưỡng thì "ngắt" và trả lỗi ngay; ba trạng thái: đóng, mở, nửa mở (pp. 79–80).
- **Giới hạn tốc độ (rate limiting)** — chặn tần suất một thao tác vượt giới hạn; thuật toán: leaky bucket, token bucket, fixed window, sliding log, sliding window (pp. 80–81).
- **Khám phá dịch vụ (service discovery)** — phía client (hỏi sổ đăng ký) hoặc phía server (qua bộ cân bằng tải); tự đăng ký hoặc đăng ký bên thứ ba; service mesh (Istio, Envoy) (pp. 81–83).
- **SLA / SLO / SLI** — thoả thuận với người dùng / mục tiêu cụ thể trong thoả thuận / chỉ số đo thực tế (pp. 83–84).
- **Khắc phục thảm hoạ (DR)**, **RTO** (độ trễ tối đa chấp nhận được tới khi khôi phục dịch vụ), **RPO** (lượng dữ liệu mất tối đa chấp nhận được); chiến lược: sao lưu, site lạnh, site nóng (pp. 84–85).
- **Máy ảo (VM) / hypervisor / container** — VM ảo hoá phần cứng, mỗi VM có hệ điều hành khách; container ảo hoá hệ điều hành, dùng chung nhân, nhẹ hơn nhiều (pp. 85–86).
- **OAuth 2.0** — giao thức *uỷ quyền* (không phải xác thực); các vai trò: chủ tài nguyên, client, máy chủ uỷ quyền, máy chủ tài nguyên, scope, access token (pp. 86–87).
- **OpenID Connect (OIDC)** — lớp mỏng trên OAuth 2.0 thêm thông tin đăng nhập và hồ sơ; token dạng JWT (pp. 87–88).
- **SSO / IdP / SAML** — đăng nhập một lần qua nhà cung cấp danh tính; SAML dùng XML (pp. 88–89).
- **SSL / TLS / mTLS** — SSL đã bị thay bằng TLS; TLS lo mã hoá, xác thực, toàn vẹn; mTLS xác thực cả hai phía (pp. 90–91).

## Propositions

- Tính khoảng cách Euclid trên kinh/vĩ độ không mở rộng được với dữ liệu lớn vì tốn CPU → cần quadtree để tìm điểm trong phạm vi 2 chiều hiệu quả (p. 78).
- Lời gọi từ xa có thể thất bại hoặc treo tới hết thời gian chờ; nhiều caller chờ một nhà cung cấp không phản hồi có thể cạn tài nguyên và gây lỗi dây chuyền → cần circuit breaker (p. 79).
- Rate limiting giúp chống DoS, kiểm soát chi phí tự mở rộng, điều tiết luồng dữ liệu (p. 80).
- Rate limit trong hệ phân tán gặp hai vấn đề: không nhất quán giữa các nút và điều kiện tranh chấp (race condition) với kiểu "get-then-set" (p. 81).
- Sổ đăng ký dịch vụ phải có tính sẵn sàng cao và luôn cập nhật (p. 83).
- Site nóng tốn kém và mất công thiết lập hơn site lạnh nhưng giảm đáng kể thời gian ngừng (p. 85).
- Lý do hàng đầu dùng VM là hợp nhất máy chủ để tận dụng phần cứng (p. 85).
- OAuth 2.0 là giao thức uỷ quyền, không phải xác thực; OIDC bổ sung phần xác thực (pp. 86–87).
- Nhược điểm SSO: lộ một mật khẩu là lộ mọi ứng dụng; xác thực chậm hơn (p. 90).
- mTLS ngày nay thường dùng giữa các microservices trong mô hình bảo mật zero trust (p. 91).

## Arguments

- **Rate limit phân tán — các cách giải và cái giá:** phiên cố định → mất khả năng chịu lỗi và mở rộng; kho tập trung như Redis → tăng độ trễ và tranh chấp; khoá phân tán → thành nút cổ chai; tác giả đề xuất "set-then-get" dùng phép toán nguyên tử (p. 81).
- **Sliding window là thoả hiệp:** kết hợp chi phí thấp của fixed window với điều kiện biên tốt của sliding log, bằng cách cộng thêm phần có trọng số của cửa sổ trước (p. 81).
- **Container so với VM:** VM phải chứa cả hệ điều hành khách và bản sao ảo phần cứng; container chỉ chứa ứng dụng và phụ thuộc, dùng chung nhân → nhẹ hơn nhiều (p. 86).

## Evidence

- Bảng kích thước ô geohash theo độ dài: độ dài 6 ≈ 1,22 km × 0,61 km; độ dài 8 ≈ 38,2 m × 19,1 m (p. 77).
- Ví dụ geohash San Francisco `9q8yy9mf` và điểm lân cận `9q8yy9vx` chung tiền tố `9q8yy9` (p. 77).
- Luồng OAuth 2.0 năm bước và luồng SSO năm bước (pp. 87, 89).
- Công cụ: etcd, Consul, Apache Thrift, ZooKeeper (p. 83); Okta, Google, Auth0, OneLogin (p. 90).

## Quotes

- "Khi lỗi đạt đến một ngưỡng nhất định, bộ ngắt mạch sẽ ngắt" (p. 79)
- "Giới hạn tỷ lệ trở nên phức tạp khi có sự tham gia của các hệ thống phân tán." (p. 81)
- "OAuth 2.0 là giao thức ủy quyền chứ không phải giao thức xác thực." (p. 86)
- "Sổ đăng ký dịch vụ phải có tính sẵn sàng cao và cập nhật." (p. 83)

## Tensions and links

- Tác giả tự hạ tầm quan trọng của DR và SSL/TLS với phỏng vấn thiết kế hệ thống (pp. 84, 90) — phần này thiên về kiến thức nền.
- Geohash/quadtree là lõi của case study Uber (phần 11); circuit breaker và rate limiting là tính năng của API gateway (phần 7).
- Service discovery là điều kiện để microservices (phần 6) chạy trong môi trường container thay đổi liên tục.
- Nhóm kỹ thuật chịu lỗi này thuộc [[concepts/availability]].
- Khái niệm liên quan: [[concepts/circuit-breaker]], [[concepts/geospatial-indexing]], [[concepts/microservices]], [[concepts/rate-limiting]].

## Open questions

- Đề xuất "set-then-get" cho race condition (p. 81) được nêu rất ngắn, không có chi tiết — cần nguồn khác (ví dụ INCR nguyên tử của Redis).
