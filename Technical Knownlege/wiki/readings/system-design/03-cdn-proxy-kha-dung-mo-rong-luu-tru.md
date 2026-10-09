---
id: readings/system-design/03-cdn-proxy-kha-dung-mo-rong-luu-tru
title: "Phần 3: CDN, proxy, tính khả dụng, khả năng mở rộng, lưu trữ (pp. 19–27)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 3
pages: "19-27"
---

Part 3 of [[sources/system-design]] (pp. 19–27).

## Question this unit answers

Làm sao đưa nội dung đến gần người dùng, che chắn máy chủ, đo và tăng thời gian hệ thống hoạt động, mở rộng khi tải tăng, và chọn kiểu lưu trữ phù hợp?

## Key terms

- **CDN (mạng phân phối nội dung)** — nhóm máy chủ phân bố theo địa lý, thường phục vụ file tĩnh (HTML/CSS/JS, ảnh, video) (p. 20).
- **Máy chủ gốc / máy chủ biên (origin / edge)** — gốc giữ bản chính; biên giữ bản đệm tại các vị trí gần người dùng (p. 21).
- **Push CDN / Pull CDN** — đẩy nội dung lên CDN khi có thay đổi / CDN tự kéo từ gốc khi có yêu cầu mà chưa có (p. 21).
- **Proxy chuyển tiếp (forward proxy)** — đứng trước nhóm máy khách, thay mặt họ liên lạc với máy chủ (p. 22).
- **Proxy ngược (reverse proxy)** — đứng trước máy chủ gốc, chặn yêu cầu từ máy khách (p. 23).
- **Tính khả dụng (availability)** — tỉ lệ thời gian hệ thống hoạt động; đo bằng "số chín": Availability = Uptime / (Uptime + Downtime) (p. 24).
- **Khả năng chịu lỗi (fault tolerance)** — không gián đoạn dịch vụ khi có lỗi, cần dự phòng toàn bộ phần cứng (p. 24).
- **Khả năng mở rộng (scalability)** — mức hệ thống đáp ứng thay đổi nhu cầu bằng cách thêm/bớt tài nguyên; theo chiều dọc (nâng máy) hoặc chiều ngang (thêm máy) (p. 25).
- **RAID 0/1/5/6/10** — các cấp độ ghép đĩa, đánh đổi tốc độ, dung lượng và khả năng chịu lỗi (p. 26).
- **Lưu trữ tệp / khối / đối tượng, NAS, HDFS** — các mô hình lưu trữ (pp. 26–27).

## Propositions

- CDN tăng tính khả dụng, dự phòng và bảo mật, giảm chi phí băng thông, vì người dùng được phục vụ từ trung tâm dữ liệu gần họ (p. 20).
- Push CDN hợp với trang ít truy cập hoặc ít cập nhật; Pull CDN hợp với trang lưu lượng lớn (pp. 21–22).
- Nhược điểm CDN: chi phí, bị chặn ở một số quốc gia, không có máy chủ ở nơi khán giả sống (p. 22).
- Proxy ngược có thể làm bộ cân bằng tải, nhưng bộ cân bằng tải không làm được proxy ngược; proxy ngược hữu ích cả khi chỉ có một máy chủ (p. 23).
- Một proxy ngược duy nhất là điểm lỗi duy nhất (p. 23).
- Hai thành phần nối tiếp làm giảm tính khả dụng tổng (99,9% × 99,9% ≈ 99,8%); hai thành phần song song làm tăng (≈ 99,9999%) (p. 24).
- Hệ thống tin cậy thì khả dụng, nhưng khả dụng chưa chắc đã tin cậy (p. 24).
- Mở rộng dọc đơn giản, dữ liệu nhất quán nhưng có thể là điểm lỗi duy nhất; mở rộng ngang tăng dư thừa và chịu lỗi nhưng phức tạp hơn và dữ liệu có thể không nhất quán (pp. 25–26).

## Arguments

- **Chịu lỗi so với sẵn sàng cao:** chịu lỗi không bị gián đoạn nhưng tốn kém hơn nhiều vì phải dự phòng toàn bộ phần cứng; sẵn sàng cao chấp nhận gián đoạn tối thiểu với chi phí thấp hơn → chọn theo mức độ gián đoạn chấp nhận được (p. 24).
- **Công thức song song/nối tiếp** là lý do kỹ thuật cho việc nhân bản thành phần (dư thừa): mỗi lớp nối tiếp nhân xác suất lỗi lên, mỗi bản sao song song giảm nó xuống (p. 24).

## Evidence

- Bảng "số chín": 99,9% ≈ 8,77 giờ ngừng/năm; 99,99% ≈ 52,6 phút/năm; 99,999% ≈ 5,25 phút/năm (p. 24).
- Bảng so sánh RAID: số đĩa tối thiểu, hiệu suất đọc/ghi, chi phí, số đĩa lỗi chịu được, dung lượng dùng được (p. 26).
- Ví dụ: CloudFront, Google Cloud CDN, Cloudflare, Fastly (p. 22); Nginx, HAProxy, Traefik, Envoy (pp. 23–24); EFS, EBS, S3, Azure Blob (pp. 26–27).

## Quotes

- "Proxy ngược cũng có thể hoạt động như một bộ cân bằng tải nhưng không phải ngược lại." (p. 23)
- "Nếu một hệ thống đáng tin cậy, nó có sẵn. Tuy nhiên, nếu nó có sẵn thì nó không nhất thiết phải đáng tin cậy." (p. 24)
- "Tính khả dụng tổng thể giảm khi hai thành phần theo thứ tự." (p. 24)

## Tensions and links

- Tính khả dụng ở đây là chữ "A" trong định lý CAP (phần 5) và nền cho SLA/SLO (phần 8).
- Mở rộng ngang gây "dữ liệu không nhất quán" — vấn đề được xử lý ở phần 4–5 (sao chép, nhất quán, sharding).
- Lưu trữ đối tượng (S3) và HDFS được dùng lại để lưu media trong case study WhatsApp/Twitter/Netflix.
- Khái niệm liên quan: [[concepts/availability]], [[concepts/caching]], [[concepts/load-balancing]], [[concepts/scalability]].

## Open questions

- Nguồn gọi NAS là "nhanh hơn, ít tốn kém hơn" so với đám mây công cộng mà không nêu bối cảnh — cần kiểm chứng.
