# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600857
**Name:** Phạm Trần Nguyên Phú
**Date:** 2026-06-10

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Kết quả hợp lý, đúng sản phẩm, giá chính xác |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Bị sai hoàn toàn do outlier giá 999999 |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

`garbage_data.csv` chứa nhiều vấn đề chất lượng dữ liệu nghiêm trọng khiến Agent đưa ra kết quả sai hoàn toàn:

- **Extreme Outlier (giá 999999):** Record `Nuclear Reactor` có giá $999,999 — một giá trị bất thường, không phản ánh thực tế. Agent sử dụng logic `idxmax()` để chọn sản phẩm có giá cao nhất trong danh mục Electronics, nên nó chọn luôn record này thay vì sản phẩm hợp lý như Laptop.

- **Duplicate ID:** Có 2 records đều có `id = 1` (Laptop và Banana). Điều này có thể gây nhầm lẫn khi join hoặc tra cứu dữ liệu theo ID, dẫn đến kết quả không nhất quán.

- **Wrong Data Type:** Record `Broken Chair` có giá là chuỗi `"ten dollars"` thay vì số. Nếu Agent có xử lý số học hoặc so sánh giá, điều này sẽ gây lỗi runtime.

- **Null Values:** Record `Ghost Item` có `id = None` và `category = None`. Nếu Agent lọc theo category, record này có thể gây lỗi hoặc bị bỏ qua không đúng cách.

Kết luận trung gian: Dữ liệu bẩn có thể "phá hoại" kết quả của AI Agent hoàn toàn, dù cho prompt rất tốt. Agent tin tưởng dữ liệu đầu vào là chính xác, nên bất kỳ sai số nào trong dữ liệu đều khuếch đại thành sai số trong kết quả cuối cùng.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** Đồng ý.

Thí nghiệm này chứng minh rằng dù cho Agent có logic xử lý đúng đắn và prompt rõ ràng, nếu dữ liệu đầu vào bị "poisoned" bởi outlier, null values, hay wrong types thì kết quả vẫn sai. Chất lượng dữ liệu là nền tảng — một ETL pipeline tốt (validate + transform) là điều kiện cần thiết trước khi bất kỳ AI Agent nào có thể hoạt động chính xác.
