# Operating Dashboard — AURA UrbanWeather Agent

> Bản rút gọn để xuất trang 1 PDF. Mọi giá trị khớp chuẩn xác worksheet nguồn `operating-dashboard.md`; chi tiết nguồn và hai phép tính `[MH]` nằm ở phụ lục trang 2.

**Model:** B2B · **Cập nhật:** 2026-08-28 · **Owner phiên họp:** Product Operations Lead (Hoàng Thị Thuyên)

**Chẩn đoán:** BQL Vinhomes Smart City trả tiền từ ngân sách vận hành; cán bộ kỹ thuật BQL vận hành hệ thống điều phối; AURA giải quyết triệt để rủi ro ngập tài sản trước khi mở rộng quan hệ cư dân.

**North Star:** Median time-to-first-value · hiện tại 6 ngày · mục tiêu ≤7 ngày · trạng thái 🟢

## Cây đèn 3 tầng

| Tầng · ID | Metric và định nghĩa ngắn | Hiện tại · 🟢 / 🟡 / 🔴 · Nguồn | Nhịp · Owner | Báo trước cho · Luật |
|---|---|---|---|---|
| L · L-01 | Median ngày bàn giao trạm đo → Nowcast đạt F1 ≥85% có BQL xác nhận | 6 ngày · ≤7 / 8–14 / >14 · `[TB]` | Tuần · Product Ops | Pilot activation + paid · R-01 |
| L · L-02 | Tỷ lệ cán bộ trực ban BQL có ≥2 action điều phối/tuần ÷ active | 75% · ≥70% / 50–69% / <50% · `[TB]` | Tuần · Customer Success | TTFV + Usage depth · R-02 |
| O · O-01 | Sự kiện cảnh báo AI tự hoàn thành (Containment) ÷ tổng sự kiện | 82,0% · ≥80% / 72,4–79,9% / <72,4% · `[MH]` | Tuần · AI Engineering | AI Cost + Gross margin · R-03 |
| O · O-02 | Tổng token LLM Claude, TTS và GIS ÷ job thành công | 426 đ · ≤1.000 / 1.001–2.826 / >2.826 · `[MH]` | Tuần · FinOps | Gross margin · R-04 |
| O · O-03 | Phân khu BQL ký thuê bao chính thức ÷ BQL kết thúc pilot | 50% · ≥50% / 35–49% / <35% · `[BM]` | Tháng · Growth Lead | ARR mới + Runway · R-03 |
| G · G-01 | (Doanh thu dịch vụ − toàn bộ chi phí biến đổi) ÷ Doanh thu | 74,4% · ≥70% / 60–69% / <60% · `[MH]` | Tháng · Finance | Runway + Payback · R-05 |
| G · G-02 | Ending cohort BQL revenue ÷ Starting cohort BQL revenue | 100% · ≥110% / 100–109% / <100% · `[BM]` | Quý · Finance | LTV · R-05 |

## Luật quyết định

| ID | NẾU · TRONG · VÀ | THÌ | KHÔNG THÌ | Dừng? |
|---|---|---|---|---|
| R-01 | TTFV >14 ngày · 2 cohort · ≥3 phân khu BQL pilot | Đóng băng nhận pilot mới 14 ngày; chuẩn hóa cấu hình trạm đo thành 1 quy trình cắm-là-chạy | Không giảm giá gói dịch vụ để bù TTFV | CÓ |
| R-02 | BQL action <50% · 3 tuần · ≥6 cán bộ trực có tài khoản | Product Owner trực bão cùng BQL 3 ca liên tiếp để tái thiết kế luồng xác nhận | Không gửi tin nhắn đôn đốc hàng loạt qua Zalo | KHÔNG |
| R-03 | Paid conversion <35% hoặc Containment <72,4% · 2 chu kỳ · ≥6 BQL | Đóng băng tiếp cận BQL mới; thiết kế lại báo cáo thiệt hại tránh được trong 1 sprint | Không nới rộng thời gian pilot miễn phí | CÓ |
| R-04 | Chi phí AI >2.826 đ/job · 2 tuần · ≥500 job cảnh báo | Bật prompt caching, chuyển model dự phòng sang tier nhẹ, giới hạn context GIS | Không tắt khâu kiểm định an toàn HITL | KHÔNG |
| R-05 | Gross margin <60% hoặc NRR <100% · 2 tháng · Doanh thu ≥30tr đ | Đàm phán phụ phí bão cực đoan; đóng gói module nâng cao cho BQL hiện hữu | Không cắt giảm chi phí an toàn/server GIS | KHÔNG |

## Cổng 90 ngày

| Ngày | Một metric · ngưỡng | Evidence | Đạt / Trượt |
|---:|---|---|---|
| 30 | BQL xác nhận độ tin cậy Nowcast · ≥85% trên ≥20 sự kiện | Biên bản nghiệm thu kỹ thuật và log đối soát cảm biến thực địa | GO / FIX |
| 60 | Tỷ lệ tự động hoàn thành Containment · ≥75% trên ≥500 job | Báo cáo phân tích log hệ thống và nhật ký trực ban | GO / PIVOT |
| 90 | Gross margin sau chi phí AI & HITL · ≥65% trên ≥2.000 job | Báo cáo quyết toán tài chính nội bộ và hóa đơn API Cloud | GO / KILL |

**Kill criteria:** KILL dừng hẳn hướng sản phẩm B2B cho Ban Quản Lý vào ngày 90 nếu Gross Margin vẫn dưới 50% sau 2 vòng tối ưu hóa Prompt Caching và tỷ lệ POC-to-paid đạt dưới 30% trên 10 phân khu thử nghiệm.

**Chưa đo được:** Chi phí khấu hao cảm biến thực tế trên mỗi điểm ngập ÷ ACV · cần dữ liệu độ bền cảm biến sau 3 tháng mưa bão thực địa tại 3 hầm chui · owner Hardware & IoT Operations Lead · có số ngày 2026-11-30.

---

# Phụ lục Trang 2 — Phép Tính Suy Ngưỡng [MH] & Truy Vết Bằng Chứng

### MH-01: Chi phí AI tối đa trên mỗi job cảnh báo thành công (Gắn với O-02 & G-01)
* **Input từ Day 24–25:**
  * Giá bán đề xuất: **15.600 đ / job** ($0.60 / job hoàn thành).
  * Gross Margin mục tiêu an toàn: **≥ 60%** (Sàn tài chính bảo toàn lợi nhuận).
  * Chi phí biến đổi khác (Infra GIS, Retry, HITL escalation): **3.414 đ / job** ($0.1313 / job).
* **Phép tính:**
  $$\text{AI Cost trần} = 15.600 \times (1 - 60\%) - 3.414 = 15.600 \times 40\% - 3.414 = 6.240 - 3.414 = \mathbf{2.826\text{ đ / job}} \quad (\$0.1087)$$
* **Ngưỡng áp dụng:**
  * 🟢 **Xanh:** $\le 1.000$ đ/job (Hiện tại đạt 426 đ ~ $0.0164, an toàn vượt trội).
  * 🟡 **Vàng:** $1.001 - 2.826$ đ/job (Cần rà soát độ dài token).
  * 🔴 **Đỏ:** $> 2.826$ đ/job (Kích hoạt ngay luật `R-04` tối ưu hóa prompt cache và context GIS).

### MH-02: Tỷ lệ Containment tự động tối thiểu để bảo toàn Gross Margin (Gắn với O-01)
* **Input từ Day 24–25:**
  * Doanh thu trên mỗi job hoàn thành: **15.600 đ / job** ($0.60).
  * Chi phí mỗi ca can thiệp thủ công HITL: **13.000 đ / ca** ($0.50) (dựa trên lương fully-loaded $6/h × 5 phút trực ban).
  * Chi phí kỹ thuật biến đổi cố định (API LLM + Speech + Infra GIS): **634 đ / job** ($0.0244).
  * Trần tổng chi phí biến đổi COGS cho phép để giữ GM ≥ 60%: **6.240 đ / job** ($0.24).
* **Phép tính:**
  $$\text{COGS} = 634 + (1 - \text{Containment}) \times 13.000 \le 6.240 \implies \text{Containment} \ge 1 - \frac{6.240 - 634}{13.000} = 1 - 0.4312 = \mathbf{56.88\%}$$
  *Đối chiếu phân tích độ nhạy (Sensitivity Analysis Day 25 Tab 3): Điểm gãy mô hình là Containment < 64%; Breakeven Containment để giữ trọn vẹn GM 74.4% là 72.4%.*
* **Ngưỡng áp dụng:**
  * 🟢 **Xanh:** $\ge 80.0\%$ (Hiện tại Eval thực tế đạt 82.0%).
  * 🟡 **Vàng:** $72.4\% - 79.9\%$ (Điều tra nguyên nhân ca phức tạp cần người duyệt).
  * 🔴 **Đỏ:** $< 72.4\%$ (Kích hoạt luật `R-03` đóng băng bán hàng để tinh chỉnh model/guardrails).
