# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi chạy live, temperature `0.0`, `0.5` và `1.0` đều trả lời khá ổn định quanh cùng một sự thật về hang Sơn Đoòng, chỉ khác mức độ diễn đạt và chi tiết. Ở temperature `1.5`, phản hồi đổi sang một sự thật khác về cà phê Việt Nam, cho thấy temperature cao làm câu trả lời đa dạng và sáng tạo hơn nhưng cũng khó đoán hơn. Vì vậy, temperature thấp phù hợp khi cần câu trả lời nhất quán, còn temperature cao phù hợp hơn cho nội dung mở hoặc cần nhiều biến thể.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt khoảng `0.2` đến `0.4` cho chatbot hỗ trợ khách hàng, vì loại chatbot này cần trả lời nhất quán, rõ ràng và ít bịa thông tin. Mức này vẫn cho phép câu trả lời tự nhiên hơn `0.0`, nhưng hạn chế rủi ro mô hình đưa ra phản hồi quá sáng tạo.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Workload mỗi ngày là `10.000 * 3 * 350 = 10.500.000` token. Theo bảng giá trong `template.py`, GPT-4o có giá input `5.00 / 0.150 = 33.33` lần GPT-4o-mini và giá output `20.00 / 0.600 = 33.33` lần, nên GPT-4o đắt hơn khoảng **33,3 lần** cho workload này. Nếu giả sử 350 token được chia đều input/output, chi phí ước tính là khoảng `$131.25/ngày` cho GPT-4o và `$3.94/ngày` cho GPT-4o-mini.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi tác vụ có độ rủi ro cao hoặc cần chất lượng lập luận tốt hơn, ví dụ phân tích hợp đồng, xử lý khiếu nại phức tạp, hoặc tạo câu trả lời quan trọng cho khách hàng doanh nghiệp. GPT-4o-mini phù hợp hơn cho các tác vụ khối lượng lớn, chi phí nhạy cảm và độ phức tạp thấp như phân loại ticket, trả lời FAQ, tóm tắt ngắn hoặc gợi ý câu trả lời nháp.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi phản hồi dài hoặc người dùng đang tương tác trực tiếp với chatbot, vì họ có thể thấy câu trả lời xuất hiện ngay thay vì chờ toàn bộ kết quả hoàn thành. Điều này làm trải nghiệm nhanh và tự nhiên hơn, đặc biệt với trợ lý hội thoại, giải thích bài học, viết nội dung dài hoặc coding assistant. Non-streaming phù hợp hơn khi phản hồi ngắn, cần xử lý hậu kỳ trước khi hiển thị, cần validate toàn bộ JSON/schema, hoặc khi hệ thống chỉ cần kết quả cuối cùng để dùng trong pipeline tự động.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
