# Operating Dashboard — AURA UrbanWeather Agent

> Đây là **worksheet nguồn** để validator và rubric truy vết evidence. Sau khi
> hoàn tất, rút gọn phần vận hành sang `one-page-dashboard.md`; không ép bảng 12 cột này lên một trang.

- Học viên: Hoàng Thị Thuyên
- Mã học viên: 2A202601910
- Mô hình: B2B
- Cập nhật: 2026-08-28
- North Star: Median time-to-first-value dưới 7 ngày

## Chẩn đoán mô hình

AURA là giải pháp B2B vì Ban Quản Lý Khu Đô Thị Vinhomes Smart City là bên ký hợp đồng và chi trả từ ngân sách vận hành và giảm thiểu rủi ro, cán bộ kỹ thuật trực ban của Ban Quản Lý là người vận hành dashboard điều phối máy bơm và phát cảnh báo dốc hầm, và sản phẩm tập trung mang lại giá trị ngăn ngừa thiệt hại tài sản cho tổ chức trước khi mở rộng quan hệ độc lập tới từng cư dân.

| Dữ liệu đầu vào | Trạng thái | Nằm ở đâu hoặc cần gì để đo | Ngày có số |
|---|---|---|---|
| Unit economics Day 24 | Đo được | File mô hình tài chính 2A202601910_HoangThiThuyen_Day24.xlsx tab Unit Economics | 2026-08-28 |
| Value Metric và Cost/Job Day 25 | Đo được | File mô hình HoangThiThuyen_Day25_model.xlsx và Evidence Pack Day 25 | 2026-08-28 |

## Kiểm kê đèn ứng viên

| Đèn ứng viên từ handbook | Tầng | Trạng thái | Bằng chứng hiện có hoặc kế hoạch đo |
|---|---|---|---|
| Time-to-first-value (TTFV) | L | ✅ | Nhật ký triển khai trạm đo và log sự kiện Nowcast tại phân khu Sapphire 1 |
| Pipeline coverage | L | 🔧 | Chuẩn hóa stage và deal size cho 5 Ban Quản Lý phân khu trong CRM trước 2026-09-15 |
| % deal chết ở khâu security/procurement | L | ✅ | Hồ sơ thẩm định an toàn thông tin và Risk Checklist Nghị định 13/2023/NĐ-CP đã nghiệm thu |
| POC → paid | O | 🔧 | Theo dõi tỷ lệ chuyển đổi sau 4 tuần pilot tại phân khu Sapphire 1 trước 2026-09-30 |
| Sales cycle (ngày) | O | 🔧 | Bổ sung mốc ngày tiếp cận ban đầu cho 10 cơ hội BQL trong CRM trước 2026-09-20 |
| Usage depth trong tài khoản | O | ✅ | Tỷ lệ ca trực ban mở dashboard và xác nhận chỉ thị điều phối qua Webhook trong event log |
| Chi phí triển khai ÷ ACV | O | 🔧 | Gắn chi phí nhân công lắp 3 trạm sensor với mã hợp đồng pilot trước 2026-09-18 |
| Tập trung doanh thu | O | ✅ | Báo cáo doanh thu xuất từ hệ thống thanh toán theo từng phân khu Ban Quản Lý |
| NRR | G | 🔧 | Chưa đủ lịch sử 2 quý; chốt baseline sau hai đợt gia hạn phân khu vào 2027-02-28 |
| Gross Margin | G | ✅ | Bảng đối soát chi phí token Claude Haiku 4.5, Speech TTS và chi phí HITL từ Day 25 |
| CAC payback | G | 🔧 | Chuẩn hóa chi phí tiếp cận Ban Quản Lý theo kênh Partner-Led trước 2026-10-15 |

## Đèn báo sớm

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| L-01 | Time-to-first-value | Số ngày từ khi ký pilot/bàn giao trạm đo đến khi hệ thống phát hiện trận mưa và gửi cảnh báo Nowcast đầu tiên đạt chuẩn F1-score ≥85% có xác nhận của BQL; median theo cohort | Tuần · Product Operations | 6 ngày | ≤7 ngày | 8–14 ngày | >14 ngày | [TB] Dùng 2 đợt pilot đầu tại phân khu Sapphire 1 làm mốc tạm thời và chốt baseline sau 4 cohort vào 2026-10-31 | 2026-08-28 | Pilot activation và chuyển đổi hợp đồng trả phí | R-01 |
| L-02 | BQL weekly dispatch action rate | Số cán bộ trực ban BQL thực hiện ít nhất 2 lần xác nhận chỉ thị điều phối máy bơm hoặc phát loa qua AURA mỗi tuần chia tổng số cán bộ trực active | Tuần · Customer Success | 75% | ≥70% | 50–69% | <50% | [TB] Đo trên 3 ca trực bão tại phân khu Sapphire bằng telemetry log rồi chốt baseline vào 2026-10-31 | 2026-08-28 | Time-to-first-value và Usage depth | R-02 |

## Đèn vận hành

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| O-01 | Tỷ lệ tự động hoàn thành (Containment rate) | Số sự kiện cảnh báo ngập được AI tự động xử lý và gửi thông báo thành công không cần chuyên viên can thiệp chia tổng số sự kiện cảnh báo | Tuần · AI Engineering | 82,0% | ≥80,0% | 72,4–79,9% | <72,4% | [MH] MH-02 suy từ điểm hòa vốn Gross Margin 60% và chi phí HITL escalation trong Day 25 | 2026-08-28 | Chi phí AI trên mỗi job và Gross margin | R-03 |
| O-02 | Chi phí AI trên mỗi job cảnh báo thành công | Tổng chi phí token LLM Claude Haiku, Speech TTS và hạ tầng GIS chia số job cảnh báo thành công | Tuần · FinOps | 426 đ | ≤1.000 đ | 1.001–2.826 đ | >2.826 đ | [MH] MH-01 suy từ giá bán 15.600 đ và gross margin an toàn tối thiểu 60% của Day 25 | 2026-08-28 | Gross margin sau chi phí AI | R-04 |
| O-03 | POC-to-paid conversion | Số phân khu BQL ký hợp đồng thuê bao chính thức chia tổng số phân khu kết thúc pilot trong kỳ | Tháng · Growth Lead | 50% | ≥50% | 35–49% | <35% | [BM] ICONIQ State of Go-to-Market 2026 https://www.iconiq.com/growth/reports/state-of-go-to-market-2026; lấy mốc trung vị ~50% năm 2026 làm tham chiếu chuyển đổi B2B | 2026-08-28 | ARR mới và Runway | R-03 |

## Đèn kết quả

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| G-01 | Gross margin sau chi phí AI và HITL | (Doanh thu dịch vụ − toàn bộ chi phí biến đổi API LLM, TTS, Infra, Retry, HITL) chia Doanh thu dịch vụ | Tháng · Finance | 74,4% | ≥70% | 60–69% | <60% | [MH] MH-01 đặt trần chi phí AI và HITL để gross margin không thấp hơn ngưỡng hòa vốn an toàn 60% | 2026-08-28 | Runway và CAC payback | R-05 |
| G-02 | Net revenue retention | Doanh thu cohort BQL cuối kỳ chia doanh thu cohort đầu kỳ sau khi mở rộng thêm phân khu và trừ churn | Quý · Finance | 100% | ≥110% | 100–109% | <100% | [BM] Benchmarkit 2025 SaaS Performance Metrics https://www.benchmarkit.ai/2025benchmarks; lấy trung vị SaaS NRR 101% làm ngưỡng sàn cảnh báo | 2026-08-28 | LTV | R-05 |

## Luật quyết định

| ID | NẾU | TRONG | VÀ | THÌ | KHÔNG THÌ | Luật dừng? |
|---|---|---|---|---|---|---|
| R-01 | Median TTFV >14 ngày | 2 cohort liên tiếp | Mỗi cohort có ít nhất 3 phân khu BQL pilot | Đóng băng nhận pilot mới trong 14 ngày và chuẩn hóa cấu hình trạm đo thành một quy trình cắm-là-chạy duy nhất | Không giảm giá gói dịch vụ để bù cho việc chậm trễ thấy giá trị | CÓ |
| R-02 | BQL action rate <50% | 3 tuần liên tiếp | Có ít nhất 6 cán bộ trực ban được cấp tài khoản | Cử một Product Owner xuống trực bão trực tiếp cùng BQL trong 3 ca trực liên tiếp để tái thiết kế luồng xác nhận | Không gửi tin nhắn thông báo đôn đốc hàng loạt qua Zalo | KHÔNG |
| R-03 | POC-to-paid conversion <35% hoặc Containment <72,4% | 2 chu kỳ pilot | Có ít nhất 6 phân khu BQL hoàn thành thử nghiệm | Đóng băng toàn bộ hoạt động tiếp cận BQL mới và thiết kế lại báo cáo chứng minh thiệt hại tránh được trong một sprint | Không nới rộng thời gian pilot miễn phí để níu giữ khách hàng | CÓ |
| R-04 | Chi phí AI mỗi job >2.826 đ | 2 tuần liên tiếp | Có ít nhất 500 job cảnh báo được xử lý | Bật prompt caching cho bản tin thời tiết, chuyển model dự phòng sang tier nhẹ hơn và giới hạn context GIS trước kỳ billing tiếp theo | Không tắt khâu kiểm định an toàn HITL để làm đẹp chi phí AI | KHÔNG |
| R-05 | Gross margin <60% hoặc NRR <100% | 2 tháng liên tiếp | Tổng doanh thu tháng đạt ít nhất 30 triệu đồng | Đàm phán phụ phí trực bão khẩn cấp cho các sự kiện thời tiết cực đoan và đóng gói module nâng cao cho các BQL hiện hữu | Không cắt giảm chi phí kiểm thử an toàn hoặc server GIS để bù biên lợi nhuận | KHÔNG |

## Cổng gác 90 ngày

| Ngày | Metric gác cổng | Ngưỡng | Bằng chứng vật lý | Nếu đạt | Nếu trượt |
|---:|---|---|---|---|---|
| 30 | Tỷ lệ Ban Quản Lý xác nhận độ tin cậy cảnh báo ngập Nowcast | ≥85% trên ít nhất 20 sự kiện mưa ngập thực tế | Biên bản nghiệm thu kỹ thuật và log đối soát cảm biến thực địa | GO | FIX |
| 60 | Tỷ lệ tự động hoàn thành Containment rate | ≥75% trên tối thiểu 500 job cảnh báo | Báo cáo phân tích log hệ thống và nhật ký can thiệp trực ban | GO | PIVOT |
| 90 | Gross margin sau chi phí AI và HITL | ≥65% trên ít nhất 2.000 job cảnh báo | Báo cáo quyết toán tài chính nội bộ và hóa đơn API Cloud | GO | KILL |

## Kill criteria

KILL dừng hẳn hướng phát triển sản phẩm B2B cho Ban Quản Lý vào ngày 90 nếu Gross Margin vẫn dưới 50% sau 2 vòng tối ưu hóa Prompt Caching và tỷ lệ POC-to-paid dưới 30% trên 10 phân khu thử nghiệm.

## Chưa đo được

| Đèn hoặc giả định | Cần gì để đo | Ai chịu trách nhiệm | Ngày có số |
|---|---|---|---|
| Chi phí khấu hao cảm biến thực tế trên mỗi điểm ngập chia theo ACV | Dữ liệu độ bền cảm biến sau 3 tháng mưa bão thực địa tại 3 hầm chui | Hardware & IoT Operations Lead | 2026-11-30 |

## Phụ lục ngưỡng suy từ mô hình

| ID | Metric | Input Day 24–25 | Phép tính | Kết quả và ngưỡng áp dụng |
|---|---|---|---|---|
| MH-01 | Chi phí AI tối đa trên mỗi job cảnh báo | Giá bán 15.600 đ ($0.60); GM mục tiêu 60%; chi phí biến đổi khác 3.414 đ ($0.1313) | 15.600 × (1 − 60%) − 3.414 = 2.826 đ/job ($0.1087) | Xanh khi chi phí AI ≤1.000 đ/job; vàng 1.001–2.826 đ/job; đỏ >2.826 đ/job áp dụng cho O-02 và G-01 |
| MH-02 | Tỷ lệ Containment tự động tối thiểu để bảo toàn Gross Margin | Doanh thu 15.600 đ/job ($0.60); chi phí HITL 13.000 đ/ca ($0.50); chi phí kỹ thuật 634 đ/job ($0.0244); trần COGS 40% là 6.240 đ | 1 − (6.240 − 634) ÷ 13.000 = 56,88% (đối chiếu điểm hòa vốn độ nhạy GM ≥60% là 72,4%) | Xanh khi Containment ≥80%; vàng 72,4–79,9%; đỏ <72,4% vì khi đó GM tụt dưới 60% áp dụng cho O-01 |

## Ghi nhận AI critique

| Phản biện | Chấp nhận hay bác bỏ | Thay đổi đã thực hiện | Lý do |
|---|---|---|---|
| TTFV thiếu định nghĩa sự kiện giá trị đầu tiên cho BQL | Chấp nhận | Bổ sung điều kiện phát hiện trận mưa và gửi cảnh báo Nowcast đạt F1 ≥85% có BQL xác nhận | Giúp 2 người cùng đo theo một cách khách quan không thể tranh cãi |
| Nên lấy benchmark NRR 101% của SaaS làm ngưỡng đỏ | Chấp nhận | Đặt mốc đỏ khi NRR <100% và xanh khi ≥110% | Chu kỳ gia hạn B2B cần bảo toàn nguyên vẹn giá trị hợp đồng để nuôi sống CAC |
| Cần tách bạch chi phí token AI và chi phí nhân sự can thiệp HITL | Chấp nhận | Tách thành 2 ngưỡng MH-01 kiểm soát chi phí token AI và MH-02 kiểm soát tỷ lệ Containment HITL | Đảm bảo FinOps và AI Engineering đều có đòn bẩy riêng để hành động |
