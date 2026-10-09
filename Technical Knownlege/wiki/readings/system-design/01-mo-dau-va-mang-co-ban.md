---
id: readings/system-design/01-mo-dau-va-mang-co-ban
title: "Phần 1: Mở đầu và mạng cơ bản (pp. 1–10)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 1
pages: "1-10"
---

Part 1 of [[sources/system-design]] (pp. 1–10).

## Question this unit answers

Thiết kế hệ thống là gì, và những khối nền tảng về mạng (địa chỉ IP, mô hình OSI, TCP/UDP, DNS) vận hành ra sao để một máy khách tìm và nói chuyện được với máy chủ?

## Key terms

- **Thiết kế hệ thống (system design)** — quá trình xác định kiến trúc, giao diện và dữ liệu cho một hệ thống thỏa mãn yêu cầu cụ thể (p. 2).
- **Địa chỉ IP** — định danh duy nhất của thiết bị trên mạng; IPv4 32 bit (~4 tỷ địa chỉ), IPv6 128 bit (~340e+36 địa chỉ) (pp. 2–3).
- **IP công khai / riêng tư / tĩnh / động** — bốn cách phân loại địa chỉ IP; IP động do máy chủ DHCP cấp và là loại phổ biến nhất (p. 3).
- **Mô hình OSI** — mô hình khái niệm chia giao tiếp mạng thành bảy lớp: ứng dụng, trình bày, phiên, vận chuyển, mạng, liên kết dữ liệu, vật lý (pp. 3–5).
- **TCP** — giao thức hướng kết nối, có kiểm tra lỗi, đảm bảo thứ tự, đổi lại tốn thêm chi phí (p. 5).
- **UDP** — giao thức không kết nối, không kiểm lỗi/khôi phục, nhanh hơn, hợp với truyền thông thời gian thực (pp. 5–6).
- **DNS** — hệ thống đặt tên phân cấp, dịch tên miền sang địa chỉ IP (p. 6).
- **TTL** — số giây một bản ghi DNS được phép nằm trong bộ đệm (p. 9).

## Propositions

- Thiết kế hệ thống là một trong những quyết định sớm nhất khi xây dựng hệ thống, và các quyết định này khó sửa về sau, nên cần suy nghĩ ở cấp cao ngay từ đầu (p. 2).
- Mô hình OSI không được triển khai trực tiếp trong mạng TCP/IP ngày nay, nhưng vẫn hữu ích như ngôn ngữ chung để khắc phục sự cố và tách một chức năng phức tạp thành phần đơn giản (pp. 3–4).
- Nên chọn UDP thay TCP khi cần độ trễ thấp nhất và dữ liệu đến muộn còn tệ hơn mất dữ liệu (p. 6).
- Một lượt tra cứu DNS đi qua tám bước: trình phân giải → máy chủ gốc → máy chủ TLD → máy chủ tên có thẩm quyền → trả IP về trình duyệt (p. 7).
- Hạ tầng DNS gồm bốn nhóm máy chủ: trình phân giải đệ quy, máy chủ gốc, máy chủ TLD, máy chủ có thẩm quyền (pp. 7–8).
- Có 13 "loại" máy chủ tên gốc, mỗi loại có nhiều bản sao khắp thế giới nhờ định tuyến Anycast (p. 8).
- Truy vấn DNS có ba kiểu: đệ quy, lặp, không đệ quy (p. 8).
- Tra cứu DNS ngược (dùng bản ghi PTR) chủ yếu được máy chủ email dùng để kiểm tra máy gửi có hợp lệ không (p. 9).

## Arguments

- **Vì sao cần DNS:** máy tính định vị nhau bằng số IP, nhưng con người nhớ tên tốt hơn số → cần một hệ thống dịch tên thành IP (p. 6).
- **TCP hay UDP:** TCP có cơ chế phản hồi để đảm bảo tin cậy → tốn thêm băng thông và chậm hơn; UDP bỏ cơ chế đó → nhanh nhưng không đảm bảo giao hàng. Vì vậy chọn theo việc ứng dụng chịu được mất dữ liệu hay chịu được trễ (pp. 5–6).
- **Bộ đệm DNS và TTL:** bản ghi được lưu kèm TTL, đếm ngược về 0 thì bị xóa và phải phân giải lại → TTL cân bằng giữa tốc độ và độ mới của dữ liệu (p. 9).

## Evidence

- Bảng so sánh TCP/UDP: kết nối, đảm bảo giao hàng, truyền lại, tốc độ, phát sóng; ví dụ dùng TCP (HTTP/HTTPS, SMTP, FTP) và UDP (video streaming, DNS, VoIP) (p. 6).
- Danh sách bản ghi DNS: A, AAAA, CNAME, MX, TXT, NS, SOA, SRV, PTR, CERT (pp. 8–9).
- Ví dụ dịch vụ DNS được quản lý: Route53, Cloudflare DNS, Google Cloud DNS, Azure DNS, NS1 (pp. 9–10).

## Quotes

- "Thiết kế hệ thống là quá trình xác định kiến trúc, giao diện và dữ liệu cho một hệ thống thỏa mãn các yêu cầu cụ thể." (p. 2)
- "Chúng ta nên sử dụng UDP qua TCP khi cần độ trễ thấp nhất và dữ liệu trễ còn tệ hơn việc mất dữ liệu." (p. 6)
- "TTL chỉ định số giây mà bản ghi có thể được lưu trữ bởi máy khách hoặc máy chủ DNS." (p. 9)

## Tensions and links

- Bộ đệm DNS là trường hợp riêng của [[concepts/caching]] — phần 2 (pp. 16–19) khái quát hóa ý tưởng này.
- Cân bằng tải bằng DNS (phần 2, p. 11) dựa trên DNS ở đây nhưng bị chỉ ra là không kiểm tra máy chủ chết.
- Lớp 4 / lớp 7 của OSI được dùng lại để phân loại bộ cân bằng tải (p. 11).

## Open questions

- Bản dịch máy ở vài chỗ khó hiểu (ví dụ "IP công khai: mỗi thiết bị được kết nối đều có cùng một địa chỉ IP", p. 3) — nên đối chiếu bản gốc tiếng Anh khi cần độ chính xác.
