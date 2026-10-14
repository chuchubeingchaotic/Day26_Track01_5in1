# Day26 — Dashboard Hành Động Cho Áp Dụng AI — Nhóm 5in1

## Thành viên — Nhóm 5in1 (Phân nhóm 5in1-A)

Nhóm đã phản biện chéo: **Nhóm 5in1-B** (Trợ lý AI Hỗ trợ Chăm sóc Khách hàng & Phân loại Ticket) · Chi tiết: [docs/phan_bien_cheo.md](docs/phan_bien_cheo.md)

| Họ và tên | MSSV | Phần phụ trách | Góp ý đã đưa cho nhóm bạn (5in1-B) |
|---|---|---|---|
| Chu Thuỳ Dương | 2A202602660 | Trưởng nhóm · Khoá phạm vi · Gartner-Lite (readiness, governance & absorption) · Memo quyết định | Nhóm 5in1-B: Phạm vi đang ôm cả chatbot trả lời khách hàng lẫn phân loại ticket nội bộ đa kênh; đề xuất khoá lại 1 nhóm người dùng chính là tư vấn viên CSKH bậc 1 (Tier 1 Support) và 2 quy trình cụ thể: phân loại/gắn tag ticket + tạo nháp phản hồi. |
| Phạm Hương Giang | 2A202602359 | Mollick (chia việc người–AI 3 vùng) · Thiết kế quy trình AS-IS / TO-BE · Kiến trúc tin cậy (Trust Architecture) | Nhóm 5in1-B: Quy trình TO-BE đang để AI tự động gửi email phản hồi khách hàng mà không có người duyệt; đề xuất áp dụng Mollick chia 3 vùng rõ ràng: vùng xanh cho FAQ chuẩn, vùng vàng cho nháp có người duyệt, vùng đỏ (khiếu nại hoàn tiền/hủy dịch vụ) bắt buộc CSKH Lead duyệt. |
| Lê Thanh Tình | 2A202602449 | ADKAR (chẩn đoán điểm nghẽn người dùng: Desire & Reinforcement) · Lộ trình 30–60–90 ngày & Tiêu chí Gate | Nhóm 5in1-B: Roadmap 30–60–90 đang là lịch triển khai kỹ thuật, hết thời gian tự chuyển; đề xuất mỗi cổng phải có bằng chứng định lượng: Gate 30 cần đo baseline 100 ticket, Gate 60 chỉ mở rộng khi tỷ lệ CSKH sửa lại nháp $\le 20\%$ và CSAT $\ge 85\%$. |
| Lưu Mạnh Hùng | 2A202602942 | Dashboard chỉ số 5 tầng (v1 → v2) · Phân biệt Activity vs Decision metrics · Logic baseline/target/owner/hành động xấu | Nhóm 5in1-B: Đang đo "Số câu hỏi chatbot xử lý" và "Tỷ lệ login" (activity metric); đề xuất thay bằng FCR (First Contact Resolution từ log ticketing) và tỷ lệ escalations phải chuyển cấp do AI phân loại sai. |
| Trần Vũ Gia Huy | 2A202602705 | Rà soát rủi ro AI & Quản trị dữ liệu PII · Cơ chế giám sát HITL (Human-in-the-Loop) & Thiết kế bộ kiểm thử Golden set | Nhóm 5in1-B: Chưa có cơ chế xử lý khi AI hallucination về chính sách hoàn tiền; đề xuất bổ sung bộ kiểm thử Golden set 50 ca khiếu nại biên, bắt buộc trích dẫn link điều khoản và có nút báo lỗi cho tư vấn viên. |

## Phạm vi

**Hệ thống AI Sàng lọc CV P-092 (Jev-based scoring engine)** · **Đội ngũ chuyên viên tuyển dụng nội bộ (Talent Acquisition / HR Recruiters, ~8 người)** · 3 quy trình: **(1) Bóc tách & Sàng lọc tiêu chí cứng → (2) Chấm điểm rubric & Duyệt vùng xám → (3) Xếp hạng ứng viên & Chốt danh sách phỏng vấn**.
Vấn đề: ~92% CV nạp qua AI (~1.800 CV/tháng), nhưng Time-to-Hire (~38 ngày) không giảm; thời gian HR sàng lọc tăng từ 18 lên 24 phút/CV do HR phải đọc lại toàn bộ file PDF vì không tin điểm số AI; tỷ lệ ứng viên AI điểm cao bị Hiring Manager loại ở phỏng vấn vòng 1 lên tới 44%.

## Nguyên nhân gốc

1. **Chia việc người–AI chưa rõ và thiếu cơ chế kiểm chứng bằng chứng** (Mollick + Gartner-Lite/Readiness): AI tự động chấm điểm toàn diện mà không trích xuất dẫn chứng cụ thể (quote văn bản + bounding box toạ độ trang); AI can thiệp vào cả vùng rủi ro cao (chuyên môn sâu) mà không phân định ranh giới giữa luật cứng, AI hỗ trợ và thẩm định con người. Bằng chứng: case công khai [Reuters 2018 (Amazon AI Recruitment Tool)](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G) (thuật toán tự loại trừ ứng viên nữ do thiếu chuẩn hóa) và [Harvard Business School 2021](https://www.hbs.edu/managing-the-future-of-work/Documents/hidden_workers_untapped_talent.pdf) (88% nhà tuyển dụng bị bộ lọc tự động loại nhầm nhân tài); dấu hiệu trong workflow là Hiring Manager loại 44% ứng viên AI shortlist ở vòng 1.
2. **Điểm nghẽn về Niềm tin + Đo lường củng cố sai lệch** (ADKAR — Desire, Reinforcement): HR sợ chịu trách nhiệm cá nhân khi điểm AI không có căn cứ giải trình; KPI cũ đo số lượng CV upload thúc đẩy nạp hồ sơ đối phó mà không khuyến khích chất lượng kiểm chứng. Bằng chứng: [Prosci 12th Edition](https://www.prosci.com/methodology/adkar) (68% từ chối phụ thuộc vào AI nếu rủi ro cá nhân phải tự chịu mà không có cơ chế kiểm chứng); telemetry log cho thấy HR rời trang kết quả AI chỉ sau 12 giây để tải PDF về đọc lại thủ công; dashboard v1 chỉ có activity metric.

## Cách làm mới

- **Nguồn kiểm chứng:** Trích dẫn nguyên văn (citation quote) kèm số trang và toạ độ highlight (bbox) trên file PDF gốc; Rule engine log cho tiêu chí cứng; giao diện đối chiếu 3 cột (CV gốc - Trích dẫn AI - Rubric điểm).
- **Người chịu trách nhiệm:** HR phụ trách vị trí chịu trách nhiệm về tính xác thực của trích dẫn trước khi chuyển tiếp; Hiring Manager giữ quyền quyết định chốt danh sách mời phỏng vấn (Shortlist); Lead Recruiter là owner quy trình; HR Tech Specialist là owner kỹ thuật/AI.
- **Khi AI không chắc hoặc sai:** Nếu AI không trích được bằng chứng thì mặc định cho 0 điểm tiêu chí đó; hồ sơ vùng xám ($T_{low} \le \text{Score} < T_{high}$) tự động chuyển vào hàng đợi `PENDING_REVIEW` cho Senior HR duyệt; HR bấm nút "Báo lỗi trích dẫn" trực tiếp trên UI; QA Lead kiểm định mẫu 30 CV/tuần; tổ chức retro 30 phút/2 tuần để hiệu chuẩn rubric giữa HR và Hiring Manager.

## Chỉ số

| Cấp | Chỉ số | Baseline | Target (Gate 90) | Nguồn dữ liệu | Owner | Hành động khi chỉ số xấu |
|---|---|---|---|---|---|---|
| Product | Q1 · % Tỷ lệ đồng thuận giữa HR và AI Rubric trên mẫu kiểm định | ~54% | $\ge 80\%$ | Báo cáo kiểm định QA tuần (30 CV/tuần) | QA Lead | < 65%: Tổ chức phiên retro 30 phút hiệu chuẩn prompt và trọng số rubric với chuyên gia |
| Product | Q2 · Tỷ lệ ứng viên Shortlist được Hiring Manager duyệt phỏng vấn | ~56% | $\ge 75\%$ | ATS Interview Scheduling Log | TA Director | < 60%: Dừng đẩy shortlist tự động, tổ chức họp 1-1 với Hiring Manager rà soát lại tiêu chí |
| Workflow | P1 · Thời gian sàng lọc trung bình / CV (median) | ~24 phút | $\le 10$ phút | Web App Access Log | Lead Recruiter | > 18 phút sau 2 sprint: Kiểm tra lại độ rõ của trích dẫn và độ trễ tải PDF trên giao diện |
| Workflow | P2 · Thời gian hoàn tất vòng lọc hồ sơ (Screening Lead Time) | ~4,2 ngày | $\le 2,0$ ngày | ATS Timeline Log | Lead Recruiter | > 3,5 ngày: Rà soát hàng đợi vùng xám, phân bổ thêm người hỗ trợ duyệt backlog |

Đủ 10 chỉ số qua 5 tầng (gồm ngưỡng xấu và hành động can thiệp tức thì) nằm trong [dashboard v2](dashboard/dashboard_hanh_dong_v2.xlsx), sheet `4_Dashboard`. Số có dấu "~" là ước tính khởi điểm, được đo lại từ hệ thống log trong giai đoạn 0–30 ngày.

## Quyết định

**SỬA.** Tiếp tục duy trì hệ thống P-092 nhưng **KHÔNG mở rộng ồ ạt** sang các phòng ban khác; chạy pilot 1 squad tuyển dụng (3 HR chính, mảng Tech & Sales) theo quy trình TO-BE và các cổng quyết định Gate 30–60–90. 5 thay đổi so với v1:

- **C1:** Bỏ số lượng CV upload và tỷ lệ login làm KPI ép buộc, chuyển sang Q1 (Đồng thuận rubric) và Q2 (Duyệt phỏng vấn).
- **C2:** Bỏ "thời gian tiết kiệm tự khai" qua khảo sát, đo P1 (thời gian sàng lọc/CV) và P2 (lead time) từ log hệ thống.
- **C3:** Mọi chỉ số có Role Owner cụ thể, target định lượng, ngưỡng xấu và hành động; bổ sung B1, B2, W3, Q3.
- **C4:** Roadmap chuyển từ lịch triển khai cứng sang cổng quyết định có ngưỡng bằng chứng (Gate 90 có 3 nhánh).
- **C5:** Chẩn đoán lại RC2 từ Knowledge sang Desire + Reinforcement; giải pháp là UI 3 cột trích dẫn trực quan và cơ chế phân vùng Mollick thay vì mở lớp đào tạo.

Chi tiết: [memo/memo_quyet_dinh.md](memo/memo_quyet_dinh.md).

## Tệp nộp bài

- [`dashboard/dashboard_hanh_dong_v2.xlsx`](dashboard/dashboard_hanh_dong_v2.xlsx) — Dashboard v2 sau phản biện chéo (7 sheet, có sheet `5_Thay_doi_v1_v2` và `6_Quyet_dinh`).
- [`memo/memo_quyet_dinh.md`](memo/memo_quyet_dinh.md) — Memo quyết định (chuẩn 5 phần).
- [`v1/dashboard_hanh_dong_v1.xlsx`](v1/dashboard_hanh_dong_v1.xlsx) — Dashboard v1 trước phản biện, dùng để đối chiếu.
- [`docs/phan_bien_cheo.md`](docs/phan_bien_cheo.md) — Biên bản phản biện chéo 2 chiều giữa Nhóm 5in1-A và Nhóm 5in1-B.
