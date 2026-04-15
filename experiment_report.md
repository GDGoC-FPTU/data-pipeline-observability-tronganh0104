# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** Bùi Trọng Anh
**Date:** 15/04/2026

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 9/10 | Dữ liệu đầy đủ, đúng kiểu và hợp lý nên agent đưa ra đề xuất phù hợp. |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1/10 | Dữ liệu nhiều lỗi và ngoại lai, dẫn đến agent ưu tiên lựa chọn vô lý. |

---

## 2. Phân tích & nhận xét (Phan tich & nhan xet)

### Tại sao Agent trả lời sai khi dùng Garbage Data? (Tai sao Agent tra loi sai khi dung Garbage Data?)

Khi dùng garbage_data.csv, agent trả lời sai vì chất lượng dữ liệu đầu vào không đảm bảo. Duplicate IDs làm cùng một thực thể bị lặp nhiều lần, gây thiên lệch trong thống kê. Wrong data types (giá dạng chữ, số lượng dạng text) khiến quá trình tính toán và sắp xếp bị sai hoặc bỏ qua bản ghi. Outliers như "Nuclear Reactor at $999999" chiếm ưu thế khi model tìm giá trị lớn nhất/điểm cao nhất. Null values làm mất thông tin quan trọng, buộc hệ thống phải đoán thay hoặc bỏ trống, từ đó giảm độ tin cậy của quyết định cuối cùng.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** (Đồng ý hay không? Giải thích ngắn gọn.)

Đồng ý. Prompt tốt chỉ giúp agent diễn đạt yêu cầu rõ ràng, nhưng nếu dữ liệu sai thì kết quả vẫn sai. Trong thí nghiệm này, cùng một cách hỏi nhưng bộ dữ liệu sạch cho đáp án hợp lý, còn bộ dữ liệu rác cho đáp án phi thực tế. Vì vậy, đảm bảo data quality là điều kiện tiên quyết để agent hoạt động đúng.
