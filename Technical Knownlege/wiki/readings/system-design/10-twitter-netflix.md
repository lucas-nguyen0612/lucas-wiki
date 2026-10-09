---
id: readings/system-design/10-twitter-netflix
title: "Phần 10: Case study Twitter và Netflix (pp. 108–126)"
type: reading
created: 2026-09-21
updated: 2026-09-21
source: system-design
part: 10
pages: "108-126"
---

Part 10 of [[sources/system-design]] (pp. 108–126).

## Question this unit answers

Thiết kế một mạng xã hội kiểu Twitter (trọng tâm: news feed) và một dịch vụ phát video kiểu Netflix (trọng tâm: xử lý và phân phối video) theo khung phỏng vấn đã nêu như thế nào?

## Key terms

- **News feed: sinh (generation) và xuất bản (publishing)** — lấy ID người được theo dõi → lấy tweet → xếp hạng → trả theo trang; rồi đẩy dữ liệu feed tới từng người dùng (pp. 112–113).
- **Fan-out khi tải (pull) / fan-out khi ghi (push) / lai (hybrid)** — ba cách xuất bản feed (p. 113).
- **EdgeRank** — thuật toán xếp hạng Facebook từng dùng: Rank = Affinity × Weight × Decay (pp. 113–114).
- **Elasticsearch** — công cụ tìm kiếm/phân tích phân tán dựa trên Apache Lucene (p. 114).
- **Đồ thị xã hội** — mỗi nút là một người dùng, cạnh có hướng biểu diễn quan hệ theo dõi, dùng cơ sở dữ liệu đồ thị (Neo4j, ArangoDB) cho gợi ý bạn chung (p. 115).
- **Đường ống xử lý video** — chia khối (chunking), lọc nội dung, chuyển mã (transcoding), chuyển đổi chất lượng (pp. 121–122).
- **Netflix Open Connect / OCA** — CDN riêng của Netflix, đặt thiết bị tại ISP (pp. 122–123).
- **Truyền phát bitrate thích ứng (HLS)** — tự điều chỉnh chất lượng theo tốc độ mạng (p. 123).
- **Chặn địa lý (geo-blocking)** — giới hạn nội dung theo khu vực, dựa trên IP hoặc cài đặt vùng (p. 124).

## Propositions

- Twitter là hệ thống đọc nhiều; ước tính 200 triệu DAU × 5 tweet → 1 tỷ tweet/ngày (~12K RPS), ~5,1 TB/ngày, ~19 PB trong 10 năm (p. 109).
- Sinh feed tốn kém, nhất là với người theo dõi nhiều người → sinh trước và đệm, cập nhật định kỳ (p. 113).
- Pull giảm ghi nhưng người dùng không thấy feed mới nếu không "kéo"; push làm feed tức thời nhưng tăng ghi; hybrid dùng push cho người ít follower, pull cho người nổi tiếng (p. 113).
- Ngày nay xếp hạng feed dùng mô hình học máy xét hàng nghìn yếu tố (p. 114).
- Retweet có thể cài đơn giản là một tweet mới có `type = tweet` và `content` là ID tweet gốc (p. 114).
- Netflix: 1 tỷ lượt xem/ngày, tỉ lệ đọc/ghi 200:1 → 5 triệu video tải lên/ngày, 100 MB/video → ~500 TB/ngày, ~1.825 PB trong 10 năm, băng thông ~5,8 GB/giây (p. 118).
- Netflix chia khối theo cảnh thay vì theo thời lượng cố định, để mỗi lần tải là trọn một cảnh, ít gián đoạn hơn (pp. 121–122).
- Xử lý video là tác vụ dài → đặt sau hàng đợi tin, tách khỏi chức năng tải lên; video vi phạm được đẩy vào DLQ cho kiểm duyệt viên (p. 122).
- Khoảng 95% lưu lượng Netflix toàn cầu đi qua kết nối trực tiếp giữa Open Connect và ISP; OCA có ở hơn 1000 địa điểm (p. 123).
- Tiếp tục xem từ chỗ đã dừng bằng thuộc tính `offset` lưu trong bảng `views` (p. 123).

## Arguments

- **Vì sao mô hình lai cho feed:** push cho người nổi tiếng với hàng triệu follower sẽ bùng nổ số thao tác ghi; pull cho mọi người sẽ bùng nổ số thao tác đọc → phân nhánh theo số follower lấy ưu điểm của cả hai (p. 113).
- **Vì sao cần đường ống xử lý:** cảnh quay 8K thô hai giờ có thể lên tới 4 TB → phải chuyển mã và tạo nhiều độ phân giải để giảm chi phí lưu trữ và phân phối (p. 121).
- **Mẫu dữ liệu chung** cho mọi case study: mô hình trông quan hệ nhưng không đặt hết vào một CSDL — chia theo dịch vụ, chọn PostgreSQL hoặc Cassandra (pp. 110–111, 119).

## Evidence

- Bảng ước tính cấp cao Twitter (pp. 109–110) và Netflix (p. 118).
- Bảng ví dụ biểu diễn retweet (p. 114).
- API: `postTweet`, `follow`/`unfollow`, `getNewsfeed` (p. 111); `uploadVideo`, `streamVideo`, `searchVideo`, `comment` (pp. 119–120).
- Công cụ: Kafka + Apache Spark cho phân tích (pp. 115, 124); FFmpeg, AWS Elemental MediaConvert cho chuyển mã (p. 122); CloudFront, Route53 geolocation routing cho chặn địa lý (p. 124).

## Quotes

- "Tạo nguồn cấp dữ liệu là một quá trình chuyên sâu và có thể mất khá nhiều thời gian" (p. 113)
- "Mô hình kết hợp chỉ cho phép người dùng có số lượng người theo dõi ít hơn sử dụng mô hình đẩy." (p. 113)
- "Netflix lại chia các phần dựa trên cảnh" (p. 121)

## Tensions and links

- Mâu thuẫn trong nguồn: phần ước tính Twitter giả định 200 triệu DAU nhưng bảng tổng hợp ghi 100 triệu (pp. 109–110).
- Netflix được dùng ở phần 6 làm ví dụ "chúng ta không phải Netflix", nhưng ở đây lại được thiết kế bằng microservices — nhất quán với lập luận rằng microservices hợp khi quy mô và tổ chức đòi hỏi.
- Chia sẻ video dùng lại thiết kế URL shortener (phần 9) — các case study xây trên nhau.
- Phân phối video là ví dụ lớn nhất cho [[concepts/caching]] qua CDN và cho [[concepts/data-partitioning]].
- Khái niệm liên quan: [[concepts/api-design]], [[concepts/asynchronous-messaging]], [[concepts/consistent-hashing]], [[concepts/database-replication]], [[concepts/load-balancing]], [[concepts/microservices]], [[concepts/system-design-interview]].

## Open questions

- Nguồn gộp Netflix và YouTube (tải lên bởi người dùng, bình luận) vào một thiết kế — hai mô hình nội dung khác nhau về kiểm duyệt và tỉ lệ đọc/ghi.
