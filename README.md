# VN-Index Stock Data Crawler

Python crawler để thu thập dữ liệu chứng khoán Việt Nam từ **cafef.vn** (OHLC) và **TCBS** (fundamental), lưu trữ vào SQLite database để phục vụ alpha research.

## Tính năng

- ✅ **Historical OHLC** - Dữ liệu lịch sử giá từ cafef API
- ✅ **Fundamental Data** - Chỉ số tài chính từ TCBS API
- ✅ **Financial Statements** - Báo cáo tài chính (income, balance sheet, cash flow)

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
