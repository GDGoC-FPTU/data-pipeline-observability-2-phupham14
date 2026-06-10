[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112890&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** phamnguyenphu14@gmail.com
**Name:** Phạm Trần Nguyên Phú

---

## Mo ta

Bài lab Day 10 về Data Pipeline & Data Observability. Xây dựng pipeline ETL tự động đọc dữ liệu JSON, kiểm tra chất lượng, chuẩn hóa và xuất ra CSV. Sau đó thực hiện thí nghiệm so sánh ảnh hưởng của dữ liệu sạch vs dữ liệu bẩn lên kết quả của một AI Agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)
```bash
# Tạo garbage_data.csv
python generate_garbage.py

# Chạy thí nghiệm so sánh Clean vs Garbage data
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

Pipeline xử lý 5 records từ `raw_data.json`, giữ lại 3 records hợp lệ và loại 2 records không hợp lệ (giá âm/bằng 0 hoặc category rỗng). Thí nghiệm stress test cho thấy dữ liệu bẩn khiến AI Agent đưa ra kết quả sai hoàn toàn (chọn Nuclear Reactor $999,999 thay vì Laptop $1,200).
