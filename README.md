[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573993&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** tronganhsl93@gmail.com
**Name:** Bùi Trọng Anh

---

## Mô tả

Bài lab này tập trung vào việc xây dựng một ETL Pipeline cơ bản để xử lý dữ liệu sản phẩm, sau đó kiểm tra tác động của chất lượng dữ liệu đến câu trả lời của AI Agent.

Nội dung đã thực hiện:
- Đọc dữ liệu từ file JSON (`extract`).
- Kiểm tra và loại bản ghi không hợp lệ (`validate`): giá <= 0 hoặc category rỗng.
- Chuẩn hóa dữ liệu (`transform`): chuẩn hóa category, tính `discounted_price = price * 0.9`, thêm `processed_at`.
- Lưu dữ liệu sạch ra CSV (`load`).
- Chạy mô phỏng Agent với dữ liệu sạch và dữ liệu rác để quan sát sự khác biệt.

---

## Cách chạy (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chạy ETL Pipeline
```bash
python solution.py
```

Sau khi chạy thành công, hệ thống sẽ tạo file `processed_data.csv`.

### Tạo dữ liệu rác (nếu cần)
```bash
python generate_garbage.py
```

### Chạy Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

Kịch bản kiểm thử:
- Dữ liệu sạch: `processed_data.csv`
- Dữ liệu rác: `garbage_data.csv`

---

## Cấu trúc thư mục

```
├── solution.py                # Script ETL chính
├── agent_simulation.py        # Mô phỏng AI Agent trả lời theo dữ liệu
├── generate_garbage.py        # Tạo dữ liệu rác để stress test
├── raw_data.json              # Dữ liệu nguồn ban đầu
├── processed_data.csv         # Dữ liệu sau khi ETL
├── garbage_data.csv           # Dữ liệu rác để thử nghiệm
├── experiment_report.md       # Báo cáo kết quả thí nghiệm
├── tests/
│   └── test_autograder.py     # Bộ test chấm tự động
└── README.md                  # Tài liệu dự án
```

---

## Kết quả

Kết quả chạy ETL với `raw_data.json`:
- Tổng bản ghi đầu vào: 5
- Bản ghi hợp lệ sau validate: 3
- Bản ghi bị loại: 2

Lý do bản ghi bị loại:
- 1 bản ghi có `price <= 0`
- 1 bản ghi có `category` rỗng

Kết quả chạy Agent:
- Với dữ liệu sạch (`processed_data.csv`), Agent đưa ra gợi ý hợp lý.
- Với dữ liệu rác (`garbage_data.csv`), Agent bị ảnh hưởng bởi outlier và dữ liệu lỗi nên đưa ra gợi ý thiếu thực tế.

Chi tiết phân tích nằm trong file `experiment_report.md`.
