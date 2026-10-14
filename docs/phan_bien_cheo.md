# Phản biện chéo — chặng 3 — Nhóm 5in1-A

- **Nhóm phản biện bài của 5in1-A:** Nhóm 5in1-B (Trợ lý AI Hỗ trợ Chăm sóc Khách hàng & Phân loại Ticket)
- **Nhóm 5in1-A phản biện:** Nhóm 5in1-B
- **Thời gian:** 20 phút góp ý · 15 phút sửa · 5 phút chốt.

---

## A. Góp ý Nhóm 5in1-A nhận được từ Nhóm 5in1-B → thay đổi trong v2

| # | Trục | Góp ý nhận được từ Nhóm 5in1-B | Thay đổi cụ thể trong v2 | Người sửa |
|---|---|---|---|---|
| 1 | Chỉ số | Số lượng CV upload (~1.800 CV) và tỷ lệ active của HR chỉ là activity metric; target 100% nạp CV ép buộc hành vi cơ học, không chứng minh được chất lượng ứng viên hay giá trị tuyển dụng. | **C1:** Hạ U1 xuống tầng 1 chỉ để theo dõi tiến độ kỹ thuật, bỏ target ép buộc, loại bỏ U2. Product metric chính chuyển sang **Q1** (% Tỷ lệ đồng thuận giữa HR và AI Rubric trên mẫu kiểm định) và **Q2** (Tỷ lệ ứng viên Shortlist được Hiring Manager duyệt phỏng vấn). | Lưu Mạnh Hùng |
| 2 | Chỉ số | "Thời gian tiết kiệm" do HR tự khai qua khảo sát Google Forms không đáng tin cậy; HR có tâm lý khai giảm giờ ảo để báo cáo đẹp hoặc sợ bị đánh giá năng suất. | **C2:** Bỏ hoàn toàn số liệu tự khai; thay bằng **P1** (Thời gian sàng lọc trung bình/CV) và **P2** (Screening Lead Time) trích xuất tự động từ Web App Audit Log và ATS Timeline Log. Căn cứ nghiên cứu METR (2025): người dùng tin mình nhanh hơn ~20% nhưng thực tế có thể chậm hơn 19%. | Lưu Mạnh Hùng |
| 3 | Hành động | Owner ghi chung chung "HR Team", target "Tăng/Giảm", cột "khi xấu" để trống; quy trình (1) bóc tách tiêu chí cứng chưa có chỉ số rủi ro lọt lỗi. | **C3:** Mọi chỉ số có Role Owner cụ thể (Lead Recruiter, HR Tech Specialist, TA Director), target định lượng, ngưỡng xấu và hành động can thiệp tức thì; bổ sung **B1**, **B2**, **W3**, **Q3** để kiểm soát trích dẫn và rủi ro lọt lỗi tiêu chí cứng. | Lưu Mạnh Hùng, Trần Vũ Gia Huy |
| 4 | Hành động | Roadmap là lịch trình cơ học ("hết 30 ngày tự chuyển"); giai đoạn 61–90 mặc định mở rộng toàn công ty là sai nguyên tắc quản trị rủi ro. | **C4:** Chuyển roadmap thành **Cổng quyết định dựa trên bằng chứng (Evidence-based Gates)**; giai đoạn 61–90 là cổng quyết định 3 nhánh (mở rộng / sửa / dừng) dựa trên ngưỡng định lượng. | Lê Thanh Tình |
| 5 | Framework | Nhận định HR không dùng là do thiếu kiến thức (ADKAR Knowledge) và giải pháp mở 3 buổi đào tạo là lỗi tư duy mặc định giải quyết bằng đào tạo. | **C5:** Chẩn đoán lại bằng ADKAR: điểm nghẽn thực sự là **Desire** (HR sợ chịu trách nhiệm khi điểm AI không có trích dẫn) và **Reinforcement** (KPI đo số lượng upload sai lệch). Giải pháp cốt lõi là UI 3 cột trích dẫn trực quan (quote/bbox), cơ chế phân vùng Mollick và đổi KPI; workshop chỉ còn là hỗ trợ. | Lê Thanh Tình, Phạm Hương Giang, Chu Thuỳ Dương |

---

## B. Góp ý Nhóm 5in1-A đưa cho Nhóm 5in1-B

| Thành viên | MSSV | Trục | Góp ý cụ thể cho Nhóm 5in1-B |
|---|---|---|---|
| Chu Thuỳ Dương | 2A202602660 | Phạm vi | Nhóm 5in1-B: Phạm vi đang ôm cả chatbot trả lời khách hàng bên ngoài lẫn trợ lý phân loại ticket nội bộ đa kênh; đề xuất khoá lại 1 nhóm người dùng chính là tư vấn viên CSKH bậc 1 (Tier 1 Support) và 2 quy trình cụ thể: (1) phân loại/gắn tag ticket + (2) tạo nháp câu trả lời phản hồi khách hàng. |
| Phạm Hương Giang | 2A202602359 | Framework | Nhóm 5in1-B: Quy trình TO-BE đang để AI tự động gửi email phản hồi khách hàng mà không có người duyệt; đề xuất áp dụng Mollick chia 3 vùng rõ ràng: vùng xanh cho FAQ chuẩn, vùng vàng cho nháp giải đáp có tư vấn viên kiểm duyệt, vùng đỏ (khiếu nại bồi thường/hủy dịch vụ) bắt buộc CSKH Lead duyệt. |
| Lê Thanh Tình | 2A202602449 | Hành động | Nhóm 5in1-B: Roadmap 30–60–90 đang là lịch triển khai kỹ thuật, hết thời gian tự động chuyển giai đoạn; đề xuất mỗi cổng phải có bằng chứng định lượng: Gate 30 cần đo baseline 100 ticket, Gate 60 chỉ mở rộng khi tỷ lệ CSKH phải sửa lại nháp $\le 20\%$ và CSAT khách hàng $\ge 85\%$. |
| Lưu Mạnh Hùng | 2A202602942 | Chỉ số | Nhóm 5in1-B: Đang đo "Số câu hỏi chatbot xử lý" và "Tỷ lệ login của nhân viên" (activity metric); đề xuất thay bằng FCR (First Contact Resolution từ hệ thống ticketing) và tỷ lệ escalations phải chuyển cấp do AI phân loại sai. |
| Trần Vũ Gia Huy | 2A202602705 | Tin cậy & Rủi ro | Nhóm 5in1-B: Chưa có cơ chế xử lý khi AI hallucination về chính sách hoàn tiền hoặc điều khoản dịch vụ; đề xuất bổ sung bộ kiểm thử Golden set 50 ca khiếu nại biên, bắt buộc trích dẫn link điều khoản và có nút báo lỗi cho tư vấn viên. |
