---
type: source
title: How to Lie with Statistics
slug: how-to-lie-with-statistics
date_added: 2026-07-31
authors:
  - Darrell Huff
source_type: book
importance: 4
confidence: unverified
tags:
  - statistics
  - critical-thinking
  - data-literacy
provenance: replayable
raw_paths:
  - raw/sources/HowToLieWithStatistics.pdf
urls: []
ingest_status: finalized
id: sources/how-to-lie-with-statistics
created: 2026-07-31
updated: 2026-07-31
year: 1954
verify_status: passed
findings:
  - {id: 1, reviewer: grounding, class: defer, claim: "Cuốn sách được viết với giọng văn hài hước, châm biếm, kèm theo minh họa của Mel Calman.", evidence: Bản gốc 1954 do Irving Geis minh họa. Mel Calman chỉ vẽ lại cho bản Pelican 1973. PDF đang dùng là bản Pelican 1973 nên claim vẫn khớp với raw., action: "Có thể thêm ghi chú rằng minh họa trong bản PDF là của Mel Calman (1973), không phải bản gốc 1954."}
---

## Summary

*How to Lie with Statistics* (1954) là một cuốn sách kinh điển giải thích cách số liệu thống kê bị bóp méo — dù cố ý hay vô tình — trong báo chí, quảng cáo, chính trị và khoa học. Darrell Huff dẫn dắt người đọc qua 10 chương, mỗi chương vạch trần một thủ thuật: từ mẫu thiên lệch (biased sample), chọn loại trung bình gây hiểu lầm (mean vs median), bỏ qua sai số và độ phân tán, thao túng biểu đồ, đánh lừa thị giác bằng pictograph, gán con số không liên quan (semi-attached figure), cho đến ngụy biện nhân quả (post hoc). Chương cuối tổng kết bằng 5 câu hỏi đơn giản để "nói lại" với bất kỳ con số thống kê đáng ngờ nào. Dù đã hơn 70 năm tuổi, những bài học của cuốn sách vẫn còn nguyên giá trị — và có lẽ còn cấp thiết hơn trong thời đại big data và AI.

Cuốn sách được viết với giọng văn hài hước, châm biếm, kèm theo minh họa của Mel Calman. Huff không chỉ vạch trần thủ thuật — ông còn dạy độc giả cách tự vệ: "The crooks already know these tricks; honest men must learn them in self-defence."

## Key Claims

- **Mẫu thiên lệch là nguồn gốc của hầu hết kết luận sai**: mẫu không đại diện (do self-selection, non-response, hoặc phương pháp chọn mẫu kém) tạo ra kết quả có vẻ khoa học nhưng vô giá trị. Literary Digest 1936 dự đoán Landon thắng Roosevelt từ 10 triệu người trả lời — nhưng danh sách mẫu thiên về người giàu, và Roosevelt đã thắng (§1)
- **"Average" không có ngữ cảnh là vô nghĩa**: mean (trung bình số học) bị kéo lên bởi outliers; median (trung vị) kháng outliers tốt hơn; mode (yếu vị) là giá trị phổ biến nhất. Cùng một khu phố: mean = £10,000, median = £2,000 — cả hai đều là "average" hợp pháp (§2)
- **Đồ thị và hình ảnh có thể nói dối mà không làm giả số liệu**: cắt trục tung, thay đổi tỷ lệ khung hình, dùng hình ảnh 2D/3D làm tỷ lệ 1:2 về chiều cao trở thành 1:8 về thể tích trong mắt người đọc (§5, §6)
- **Tương quan không phải là nhân quả**: post hoc ergo propter hoc là ngụy biện phổ biến và nguy hiểm nhất trong thống kê. Cò và trẻ sơ sinh, mục sư và giá rum, chấy và sức khỏe — mọi tương quan đều có ít nhất 4 cách giải thích (§8)
- **Thống kê là nghệ thuật nhiều như là khoa học**: những lựa chọn phương pháp hoàn toàn hợp pháp (kỳ gốc, loại trung bình, chỉ số) có thể tạo ra những kết luận trái ngược nhau từ cùng một dữ liệu. Người làm thống kê thương mại hiếm khi chọn phương pháp bất lợi cho khách hàng (§9)

## Evidence

- **Literary Digest 1936**: 10 triệu người khảo sát, dự đoán Landon 370 phiếu — Roosevelt thắng thực tế (§1)
- **Gallup vs báo Chủ nhật**: 33% vs 98% biết về hệ mét — cùng câu hỏi, hai phương pháp chọn mẫu (§0)
- **Kem đánh răng Doakes**: "23% fewer cavities" — thử nghiệm trên 12 người; tung đồng xu 10 lần ra 8 mặt ngửa = "80%" (§3)
- **Old Gold**: tất cả nhãn hiệu thuốc lá "virtually identical" về độc tố, nhưng Old Gold đứng cuối bảng → quảng cáo "ít độc tố nhất" (§4)
- **Columbia Gas**: chi phí sinh hoạt +60%, gas -4% → cắt trục tung ở 90% → trông như +200% và -33% (§5)
- **Iron and Steel Institute**: năng lực thép +42.5% → vẽ lò cao tạo ấn tượng thị giác +1,500% (§6)
- **Russell Sage Foundation**: "gia đình trung bình $5,004" — lấy tổng thu nhập ÷ dân số × 4, bỏ qua phân phối thực tế (§9)
- **Chỉ số giá sữa/bánh mì**: cùng dữ liệu → 3 kết luận khác nhau (tăng 25%, giảm 25%, không đổi) tùy cách chọn kỳ gốc và loại trung bình (§9)

## Related Concepts

- [[thien-lech-mau]] — sampling bias, nền tảng của hầu hết các thủ thuật thống kê
- [[tuong-quan-va-nhan-qua]] — phân biệt correlation và causation
- [[thao-tung-thong-ke]] — statistical manipulation / statisticulation
- [[y-nghia-thong-ke]] — statistical significance, cỡ mẫu, sai số
- [[trung-binh-thong-ke]] — mean, median, mode và cách chúng bị lạm dụng

## Related Sources

_Chưa có nguồn liên quan trong wiki._

## People

- [[darrell-huff]]

## Open Questions

- Cuốn sách xuất bản lần đầu năm 1954 — các ví dụ cụ thể có còn áp dụng được trong bối cảnh thống kê và truyền thông hiện đại không?
- Những kỹ thuật "nói dối bằng thống kê" nào đã trở nên tinh vi hơn với sự ra đời của big data và machine learning (p-hacking, HARKing, data dredging)?
- Liệu "causality revolution" (Judea Pearl) có phải là câu trả lời cho vấn đề post hoc mà Huff mô tả?
- 5 câu hỏi của Huff có cần câu hỏi thứ 6 cho thời đại AI: "What's the algorithm?"
