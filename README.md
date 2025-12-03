# VN-Index Stock Data Crawler

Python crawler để thu thập dữ liệu chứng khoán Việt Nam từ **cafef.vn** (OHLC) và **TCBS** (fundamental), lưu trữ vào SQLite database để phục vụ alpha research.

## Tính năng

- ✅ **Historical OHLC** - Dữ liệu lịch sử giá từ cafef API
- ✅ **Fundamental Data** - Chỉ số tài chính từ TCBS API
- ✅ **Financial Statements** - Báo cáo tài chính (income, balance sheet, cash flow)
- ✅ **SQLite Database** - Lưu trữ tối ưu cho alpha research
- ✅ **Realtime Polling** - Poll giá realtime theo chu kỳ

## Cài đặt

```bash
git clone https://github.com/NgokNgo/crawl-data.git
cd crawl-data
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Sử dụng

### Crawl dữ liệu

```bash
# Historical OHLC
python crawl.py historical --symbol VIC
python crawl.py historical --symbols-file symbols.txt

# Fundamental
python crawl.py fundamental --symbol VIC
python crawl.py fundamental --symbols-file symbols.txt
python crawl.py fundamental --symbol VIC --latest  # chỉ xem, không lưu
```

### Quản lý Database

```bash
python managedb.py init                    # Khởi tạo schema
python managedb.py import                  # Import CSV -> DB
python managedb.py info                    # Xem thống kê
python managedb.py query --type prices     # Query giá
python managedb.py query --type fundamentals
python managedb.py query --type merged --symbols VIC,VCB
python managedb.py export --type all       # Export ra CSV
```

### Realtime Polling

```bash
python crawl.py realtime --symbol VIC \
  --url-template 'https://cafef.vn/thi-truong-chung-khoan/hose/{symbol}.chn' \
  --interval 60
```

### Python API

```python
from crawler.database import get_price_matrix, get_merged_data

# Lấy price matrix
prices = get_price_matrix('close', start_date='2024-01-01')

# Lấy merged data cho alpha
data = get_merged_data(
    symbols=['VIC', 'VCB', 'VNM'],
    price_cols=['close', 'volume'],
    fund_cols=['pe', 'pb', 'roe', 'eps']
)
```

## Workflow

```bash
# 1. Crawl
python crawl.py historical --symbols-file symbols.txt
python crawl.py fundamental --symbols-file symbols.txt

# 2. Import
python managedb.py import

# 3. Verify
python managedb.py info
```

## Cấu trúc

```
crawl-data/
├── crawl.py               # CLI crawl data
├── managedb.py            # CLI quản lý database
├── symbols.txt            # Danh sách mã CK
├── requirements.txt
├── docs/
│   └── API_REFERENCE.md   # Chi tiết API & data dictionary
├── crawler/
│   ├── database.py        # SQLite module
│   ├── fundamental.py     # TCBS API
│   ├── historical.py      # Cafef API
│   └── ...
└── data/
    ├── historical/        # CSV OHLC
    ├── fundamental/       # CSV fundamental
    └── stock_data.db      # SQLite database
```

## Tài liệu

- [API Reference & Data Dictionary](docs/NOTE.md) - Chi tiết các API endpoints và định nghĩa trường dữ liệu

## Lưu ý

- Realtime polling: khuyến nghị interval >= 30 giây
- Fundamental data từ TCBS cập nhật theo quý
