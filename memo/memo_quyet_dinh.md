# Memo quyết định — Hệ thống AI Sàng lọc CV P-092 — Nhóm 5in1

**Gửi:** Talent Acquisition Director (Giám đốc Tuyển dụng) · **Từ:** Nhóm 5in1-A · **Quyết định:** **SỬA**

---

## 1. Vấn đề và nguyên nhân gốc

Hệ thống AI Sàng lọc CV P-092 (Jev-based scoring engine) đã được triển khai cho toàn bộ đội ngũ tuyển dụng (~8 chuyên viên HR) được 2 tháng. Dashboard kỹ thuật báo cáo tỷ lệ CV nạp vào hệ thống đạt ~92% (~1.800 CV/tháng), cho thấy công cụ đã được cấp phát (deployment) và có người thao tác (usage). Tuy nhiên, **thời gian tuyển dụng (Time-to-Hire ~38 ngày) không hề giảm**, và **thời gian sàng lọc của HR tăng từ 18 lên 24 phút/CV**. Nguyên nhân là HR không tin tưởng kết quả nên phải tải file PDF gốc về đọc lại toàn bộ từ đầu; tỷ lệ ứng viên do AI chấm điểm cao bị Hiring Manager (trưởng bộ phận chuyên môn) loại ngay tại vòng phỏng vấn đầu tiên lên tới **~44%**. 

Như vậy, công cụ mới chỉ dừng ở mức usage/deployment cơ học mà **chưa đạt tới adoption thật** (chưa thay đổi workflow, chưa phân định trách nhiệm bàn giao và cơ chế kiểm soát).

- **RC1. Chia việc người–AI chưa rõ và thiếu cơ chế kiểm chứng bằng chứng (Mollick + Gartner-Lite / Readiness & Absorption):** Hệ thống chấm điểm toàn diện mọi tiêu chí mà không trích xuất đoạn văn bản dẫn chứng (quote) và toạ độ trang (bounding box) trong CV; AI can thiệp vào cả vùng rủi ro cao (năng lực chuyên môn sâu) mà không có phân định ranh giới giữa luật cứng, AI hỗ trợ và quyền thẩm định của con người. Thiếu Golden test set và thiếu cơ chế phản hồi lỗi.
- **RC2. Điểm nghẽn về Niềm tin (Desire) và Đo lường củng cố sai lệch (Reinforcement) (ADKAR):** HR sợ chịu trách nhiệm cá nhân khi hồ sơ do AI gợi ý bị Hiring Manager phàn nàn; trong khi đó, KPI nội bộ lại đo số lượng CV upload và tỷ lệ chạy AI (activity metric), thúc đẩy HR nạp hồ sơ đối phó nhưng sau đó vẫn đọc thủ công. Điểm nghẽn không nằm ở Knowledge (đào tạo), nên mở lớp hướng dẫn không giải quyết được vấn đề.

---

## 2. Framework đã dùng và bằng chứng

| Framework | Đánh giá & Kết luận |
|---|---|
| **Gartner-Lite** | **Direction:** Đạt một phần — Mục tiêu "tự động hóa sàng lọc CV" còn chung chung, chưa gắn với chất lượng tuyển dụng.<br/>**Readiness:** Thiếu — Rubric tuyển dụng giữa HR và Hiring Manager chưa chuẩn hóa trọng số; thiếu cơ chế ẩn danh PII (Blind recruiting) để tránh thiên kiến; thiếu Golden test set 100 CV có gắn nhãn chuẩn.<br/>**Absorption:** Thiếu — Chưa có Data Owner hiệu chỉnh rubric; chưa có quy trình phản hồi khi HR override điểm số AI; thiếu buổi đối soát chất lượng giữa HR và Hiring Manager.<br/>*Kết luận:* Chưa thể rollout diện rộng; cần pilot nhỏ để sửa readiness và absorption. |
| **Mollick** | Phân chia công việc theo 3 vùng nghiêm ngặt:<br/>- **Vùng đỏ (Người giữ quyền quyết định):** Quyết định loại ứng viên (Final Rejection); chốt danh sách mời phỏng vấn (Shortlist); giải quyết ngoại lệ khiếu nại. AI tuyệt đối không tự động loại/nhận.<br/>- **Vùng vàng (AI hỗ trợ, người kiểm):** AI bóc tách kinh nghiệm, trích dẫn bằng chứng (quote/bbox) theo từng tiêu chí rubric và đề xuất điểm nháp. HR bắt buộc đối chiếu trên UI 3 cột trước khi bấm duyệt. Không có trích dẫn = 0 điểm.<br/>- **Vùng xanh (AI tự động có kiểm soát):** Chống trùng CV (sha256 + MinHash); che thông tin PII (họ tên, ảnh, giới tính, trường cấp 3); kiểm tra format file và quét virus. |
| **ADKAR** | Điểm nghẽn nằm ở **Desire** (HR không tin điểm số vô căn cứ, sợ bị khiển trách) và **Reinforcement** (KPI đo số lượng upload vô nghĩa). Không nghẽn ở Awareness hay Knowledge, do đó giải pháp trọng tâm là xây dựng niềm tin bằng trích dẫn minh bạch và đổi KPI, chứ không phải mở lớp đào tạo. |

**Bằng chứng thực tế:**
- **Amazon AI Recruitment Tool Bias Case (Reuters, 2018):** Hệ thống tự động chấm điểm CV của Amazon bị thiên kiến và thiếu khả năng giải trình theo ngữ cảnh, buộc phải hủy bỏ khi tự động loại trừ ứng viên nữ do học dữ liệu lịch sử thiếu chuẩn hóa.
- **Harvard Business School & Accenture (2021) — "Hidden Workers: Untapped Talent":** Hơn 88% nhà tuyển dụng xác nhận các bộ lọc tự động vô tình loại bỏ hàng triệu ứng viên tiềm năng do thiếu cơ chế kiểm chứng ngữ cảnh linh hoạt.
- **Prosci Change Management Research (12th Edition):** 68% nhân viên từ chối phụ thuộc vào AI nếu phải tự chịu trách nhiệm rủi ro sai sót mà thiếu cơ chế kiểm chứng bảo vệ.
- **Dấu hiệu thực tế trong workflow:** Log telemetry cho thấy HR rời màn hình kết quả AI chỉ sau 12 giây để tải PDF về đọc lại thủ công; tỷ lệ Hiring Manager từ chối ứng viên AI shortlist ở vòng 1 lên đến 44%.

---

## 3. Thay đổi sau phản biện chéo (v1 → v2)

Nhóm đã tiếp thu toàn diện góp ý từ Nhóm 5in1-B và thực hiện 5 thay đổi cốt lõi:

1. **C1.** Bỏ hoàn toàn chỉ số số lượng CV upload và tỷ lệ login làm KPI chính. Product metric chính chuyển sang **Q1 (% Tỷ lệ đồng thuận giữa HR và AI Rubric trên mẫu kiểm định)** và **Q2 (Tỷ lệ ứng viên Shortlist được Hiring Manager duyệt phỏng vấn)**. Chỉ số upload (U1) chỉ giữ để theo dõi kỹ thuật.
2. **C2.** Bỏ "thời gian tiết kiệm tự khai" qua biểu mẫu Google Forms; thay bằng **P1 (Thời gian sàng lọc trung bình/CV)** và **P2 (Screening Lead Time)** đo lường tự động từ Web App Audit Log và ATS Timeline Log.
3. **C3.** Mọi chỉ số có Role Owner cụ thể (Lead Recruiter, HR Tech Specialist, TA Director), target định lượng, ngưỡng xấu và hành động can thiệp ngay lập tức; bổ sung **B1** (% hồ sơ được kiểm tra trích dẫn), **B2** (duyệt tắt vùng vàng), **W3** (độ chính xác bóc tách), và **Q3** (tỷ lệ lọt lỗi tiêu chí cứng).
4. **C4.** Chuyển roadmap từ lịch trình cơ học ("hết 30 ngày") sang **Cổng quyết định dựa trên bằng chứng (Evidence-based Gates)**; Gate 90 là cổng quyết định 3 nhánh (mở rộng / sửa / dừng).
5. **C5.** Chẩn đoán lại RC2 từ Knowledge sang **Desire + Reinforcement**. Giải pháp chính là giao diện 3 cột trích dẫn văn bản, cơ chế phân vùng Mollick và đổi KPI đánh giá chất lượng; workshop đào tạo chỉ còn là bước phụ.

*Chi tiết đối chiếu: Xem [docs/phan_bien_cheo.md](../docs/phan_bien_cheo.md) và sheet `5_Thay_doi_v1_v2` trong dashboard v2.*

---

## 4. Quyết định

**SỬA.** Tiếp tục duy trì hệ thống P-092 nhưng **KHÔNG mở rộng ồ ạt** sang các phòng ban khác. Chạy chương trình pilot tại 1 squad tuyển dụng (3 HR chính, phụ trách khối Kỹ thuật & Kinh doanh) theo quy trình TO-BE và các cổng quyết định Gate 30–60–90.

---

## 5. Lý do, bước tiếp theo và owner

**Lý do:** P-092 mang lại giá trị rất lớn ở vùng xanh (chống trùng CV, ẩn danh PII fail-closed, format file) và vùng vàng (trích dẫn bằng chứng, gợi ý rubric nháp). Tuy nhiên, do thiếu cơ chế kiểm chứng trích dẫn và đo sai chỉ số nên đang gây lãng phí thời gian đọc lại; dừng hẳn sẽ mất lợi thế tự động hóa, nhưng mở rộng ngay sẽ nhân rộng mâu thuẫn giữa HR và Hiring Manager.

| Gate | Việc chính | Owner | Điều kiện qua cổng (Gate Criteria) |
|---|---|---|---|
| **0–30 ngày** (Readiness & Baseline) | Khóa rubric chuẩn 2 job profiles; cập nhật UI 3 cột đối chiếu trích dẫn (quote/bbox); bật PII anonymization fail-closed; đo baseline từ 100 CV mẫu qua log. | Lead Recruiter (quy trình) + HR Tech Specialist (kỹ thuật) | Baseline có từ $\ge 100$ CV; tỷ lệ điểm AI có trích dẫn nguồn $\ge 85\%$; 100% HR trong pilot thực hành UI mới; 0 sự cố rò rỉ PII. |
| **31–60 ngày** (Quality & Reliability) | Chạy TO-BE đầy đủ. QA Lead kiểm mẫu 30 CV/tuần. Kích hoạt hàng đợi vùng xám. Retro hiệu chuẩn rubric 30 phút/2 tuần giữa HR và Hiring Manager. Kênh #p092-feedback. | QA Lead (chất lượng) + Lead Recruiter | $Q1 \ge 70\%$; $Q2 \ge 70\%$ (so với baseline ~56%); $Q3 \le 5\%$; $B1 \ge 90\%$; $B2 = 0$; Tỷ lệ đọc lại toàn bộ CV $\le 30\%$. |
| **61–90 ngày** (Value & Decision) | So sánh bộ chỉ số 5 tầng với Target. Chốt Data Owner và AI Champion vận hành lâu dài. Rà soát governance với Pháp chế/HR Director. Họp hội đồng tuyển dụng ra quyết định. | Talent Acquisition Director (owner quyết định) | Chọn 1 trong 3 nhánh theo quy tắc quyết định dưới đây. |

**Quy tắc ra quyết định ở Gate 90:**

| Nhánh quyết định | Điều kiện định lượng bắt buộc |
|---|---|
| **Mở rộng sang toàn bộ 5 khối phòng ban** | $P1 \le 10$ phút/CV VÀ $Q1 \ge 80\%$ VÀ $Q2 \ge 75\%$ VÀ $Q3 \le 3\%$ VÀ $V1$ đạt tiến độ tuyển dụng. |
| **Tiếp tục sửa thêm 1 chu kỳ 30 ngày** | Cải thiện một phần ($P1$ giảm còn $\le 14$ phút, $Q1 \ge 70\%$ nhưng $Q2$ hoặc $V1$ chưa đạt mục tiêu). |
| **Thu hẹp / Dừng (chỉ dùng vùng xanh)** | $Q2 < 60\%$ kéo dài HOẶC phát hiện vi phạm thiên kiến nhạy cảm / rò rỉ dữ liệu cá nhân PII lặp lại. |

**Hành động tức thì trong tuần 1:**
1. Lead Recruiter ban hành hướng dẫn phân vùng Mollick 3 vùng và mẫu biên bản duyệt ứng viên.
2. HR Tech Specialist cập nhật UI 3 cột đối chiếu trích dẫn và kích hoạt kiểm tra PII fail-closed.
3. Kích hoạt script trích xuất baseline tự động từ Audit log và ATS.

---
*> Toàn bộ số liệu có dấu "~" là ước tính khởi điểm của nhóm để đặt ngưỡng; nhóm sẽ đo đạc chính xác qua hệ thống log trong giai đoạn 0–30 ngày.*

