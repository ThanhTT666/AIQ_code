# 🌍 AIQ (Air Intelligence Quality) Pipeline

Một Pipeline xử lý dữ liệu ở mức production cho phép xử lý dữ liệu chất lượng không khí từ 7 thành phố châu Á sử dụng Parquet Data Lake và DuckDB Warehouse.

## 📊 Tổng Quan Dữ Liệu

- **Thành phố**: Bangkok, Beijing, Hà Nội, Thành phố Hồ Chí Minh, Jakarta, Nantong, Singapore
- **Khoảng thời gian**: Tháng 8 năm 2022 - Tháng 2 năm 2026
- **Số bản ghi**: 9.085 quan sát
- **Các tính năng**: 11 chỉ số chất lượng không khí (PM2.5, PM10, CO, NO2, SO2, O3, v.v.)
- **Dung lượng**: ~2.6 MB (nhẹ - bao gồm trong repo)

## 📥 Nguồn Dữ Liệu

**Dataset**: Khả dụng trên Kaggle  
🔗 [nitirajkulkarni/datasets](https://www.kaggle.com/nitirajkulkarni/datasets)

Dữ liệu chất lượng không khí được lấy từ Kaggle và bao gồm các bản ghi lịch sử cho 7 thành phố lớn ở châu Á.

## 🏗️ Kiến Trúc

```
DỮ LIỆU GỐC (CSV) → INGESTION → CLEANING → VALIDATION → DATA LAKE (Parquet) + WAREHOUSE (DuckDB) → REPORTS (HTML)
```

## 🚀 Bắt Đầu Nhanh

### Yêu Cầu Trước
- Python 3.8+
- Git

### Cài Đặt

```bash
# Clone repository
git clone https://github.com/ThanhTT666/AIQ-Pipeline.git
cd AIQ-Pipeline

# Tạo virtual environment
python -m venv .venv

# Kích hoạt virtual environment
# Trên Windows:
.\.venv\Scripts\Activate.ps1
# Trên macOS/Linux:
source .venv/bin/activate

# Cài đặt dependencies
pip install -r requirements.txt
pip install duckdb pyarrow
```

### Chạy Pipeline

```bash
# Điều hướng đến thư mục pipeline
cd src/pipeline

# Thực thi pipeline (7 giai đoạn)
python run_pipeline.py
```

### Tạo Báo Cáo

```bash
# Từ thư mục gốc dự án
cd src/inspection
python generate_report.py

# Mở báo cáo HTML trong trình duyệt
# Vị trí file: ../../../reports/pipeline_report.html
```

## 📂 Cấu Trúc Dự Án

```
AIQ-Pipeline/
├── AIQ_datasets/              # Dữ liệu gốc (bao gồm - 2.6 MB)
│   ├── Bangkok/
│   ├── Beijing/
│   ├── Hanoi/
│   ├── HoChiMinh/
│   ├── Jakarta/
│   ├── Nantong/
│   └── Singapore/
│
├── src/
│   ├── ingestion/             # Tải dữ liệu
│   │   └── load_data.py
│   ├── pipeline/              # Orchestration
│   │   └── run_pipeline.py
│   ├── processing/            # Chuyển đổi dữ liệu
│   │   ├── clean_data.py
│   │   ├── transform_data.py
│   │   ├── parquet_lake.py
│   │   └── duckdb_warehouse.py
│   ├── quality/               # Validation & Logging
│   │   ├── data_quality.py
│   │   └── logger.py
│   └── inspection/            # Báo cáo
│       ├── generate_report.py
│       └── inspect_results.py
│
├── requirements.txt
├── README.md
├── PROJECT_SUMMARY.md
└── .gitignore
```

## 🔄 Các Giai Đoạn Pipeline

| Giai Đoạn | Mô Tả | Đầu Ra |
|-----------|--------|--------|
| 1 | Tải CSV từ 7 thành phố | DataFrame kết hợp (9.085 hàng) |
| 2 | Làm sạch & xác thực dữ liệu | Loại bỏ bản sao, chuẩn hóa ngày |
| 3a | Xuất sang Parquet Data Lake | city=Bangkok/, city=Beijing/, ... |
| 3b | Tính toán phân tích | summary_metrics.csv |
| 4 | Tải sang DuckDB Warehouse | fact_air_quality, dim_city, daily_city_metrics |
| Báo Cáo | Tạo dashboard tương tác | pipeline_report.html |

## 💡 Các Tính Năng Chính

✅ **Relative Paths** - Hoạt động trên Windows, macOS, Linux  
✅ **Automatic City Detection** - Trích xuất thành phố từ cấu trúc thư mục  
✅ **Multi-format Date Parsing** - Xử lý M/D/YYYY và YYYY-MM-DD  
✅ **Structured Logging** - Theo dõi quá trình thực thi pipeline  
✅ **Data Validation** - Kiểm tra chất lượng tại mỗi giai đoạn  
✅ **Parquet Partitioning** - Tổ chức Data Lake hiệu quả  
✅ **DuckDB OLAP** - Truy vấn phân tích nhanh  
✅ **HTML Reports** - Dashboard tương tác  

## 🛠️ Tech Stack

- **Python 3.8+** - Ngôn ngữ lập trình
- **Pandas** - Thao tác dữ liệu
- **PyArrow** - Hỗ trợ Parquet
- **DuckDB** - OLAP Database
- **Logging** - Giám sát Pipeline

## 📈 Hiệu Năng

- **Thời gian chạy**: 3-5 giây
- **Dung lượng Data Lake**: ~2.5 MB (Parquet)
- **Dung lượng Warehouse**: ~1.2 MB (DuckDB)
- **Sử dụng Bộ nhớ**: <500 MB

## 📄 Giấy Phép

MIT License

## 👤 Tác Giả

ThanhTT666
