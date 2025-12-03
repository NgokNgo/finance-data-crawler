# API Reference & Data Dictionary

## API Endpoints

### 1. Cafef - Historical OHLC

**Endpoint:**
```
GET https://cafef.vn/du-lieu/Ajax/PageNew/DataHistory/PriceHistory.ashx
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| Symbol | string | Yes | Mã chứng khoán (VD: VIC, VCB) |
| StartDate | string | No | Ngày bắt đầu (DD/MM/YYYY) |
| EndDate | string | No | Ngày kết thúc (DD/MM/YYYY) |
| PageIndex | int | Yes | Trang (bắt đầu từ 1) |
| PageSize | int | Yes | Số record mỗi trang (max 10000) |


**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| Ngay | string | Ngày giao dịch (DD/MM/YYYY) |
| GiaMoCua | float | Giá mở cửa (nghìn VND) |
| GiaCaoNhat | float | Giá cao nhất trong phiên |
| GiaThapNhat | float | Giá thấp nhất trong phiên |
| GiaDongCua | float | Giá đóng cửa |
| GiaDieuChinh | float | Giá điều chỉnh (adjusted for splits/dividends) |
| KhoiLuongKhopLenh | int | Khối lượng khớp lệnh (shares) |
| GiaTriKhopLenh | float | Giá trị khớp lệnh (VND) |
| KLThoaThuan | int | Khối lượng thỏa thuận (block deal) |
| GtThoaThuan | float | Giá trị thỏa thuận (VND) |
| ThayDoi | string | Thay đổi giá (format: "change(percent%)") |

---

### 2. TCBS - Company Overview

**Endpoint:**
```
GET https://apipubaws.tcbs.com.vn/tcanalysis/v1/ticker/{symbol}/overview
```

**Response:**
```json
{
  "ticker": "VIC",
  "exchange": "HOSE",
  "shortName": "VINGROUP",
  "industry": "Bất động sản",
  "industryEn": "Real Estate",
  "noEmployees": 45000,
  "noShareholders": 12345,
  "foreignPercent": 0.25,
  "outstandingShare": 3850000000,
  "issueShare": 3850000000,
  "stockRating": 3.5,
  "deltaInWeek": 0.02,
  "deltaInMonth": -0.05,
  "deltaInYear": 0.15
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| ticker | string | Mã chứng khoán |
| exchange | string | Sàn giao dịch (HOSE, HNX, UPCOM) |
| shortName | string | Tên viết tắt công ty |
| industry | string | Ngành (tiếng Việt) |
| industryEn | string | Ngành (tiếng Anh) |
| noEmployees | int | Số nhân viên |
| noShareholders | int | Số cổ đông |
| foreignPercent | float | Tỷ lệ sở hữu nước ngoài (0-1) |
| outstandingShare | float | Số cổ phiếu lưu hành |
| issueShare | float | Tổng số cổ phiếu phát hành |
| stockRating | float | Đánh giá cổ phiếu (1-5) |
| deltaInWeek | float | % thay đổi giá trong tuần |
| deltaInMonth | float | % thay đổi giá trong tháng |
| deltaInYear | float | % thay đổi giá trong năm |

---

### 3. TCBS - Financial Ratios

**Endpoint:**
```
GET https://apipubaws.tcbs.com.vn/tcanalysis/v1/finance/{symbol}/financialratio
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| yearly | int | No | 1 = yearly, 0 = quarterly |
| isAll | string | No | "true" = all data, "false" = recent only |


**Response Fields:**

| Field | Type | Description | Formula |
|-------|------|-------------|---------|
| ticker | string | Mã chứng khoán | - |
| quarter | int | Quý (1-4, 5=annual) | - |
| year | int | Năm | - |
| **Valuation Ratios** | | | |
| priceToEarning | float | P/E ratio | Price / EPS |
| priceToBook | float | P/B ratio | Price / BVPS |
| valueBeforeEbitda | float | EV/EBITDA | Enterprise Value / EBITDA |
| **Profitability** | | | |
| roe | float | Return on Equity | Net Income / Equity |
| roa | float | Return on Assets | Net Income / Total Assets |
| grossProfitMargin | float | Biên lợi nhuận gộp | Gross Profit / Revenue |
| operatingProfitMargin | float | Biên lợi nhuận hoạt động | Operating Profit / Revenue |
| postTaxMargin | float | Biên lợi nhuận ròng | Net Income / Revenue |
| **Per Share** | | | |
| earningPerShare | float | EPS (VND) | Net Income / Shares |
| bookValuePerShare | float | BVPS (VND) | Equity / Shares |
| dividend | float | Cổ tức (VND/share) | - |
| **Efficiency** | | | |
| daysReceivable | float | Số ngày thu tiền | AR / (Revenue/365) |
| daysInventory | float | Số ngày tồn kho | Inventory / (COGS/365) |
| daysPayable | float | Số ngày trả tiền | AP / (COGS/365) |
| cashCirculation | float | Chu kỳ tiền mặt | DSO + DIO - DPO |
| revenueOnAsset | float | Vòng quay tài sản | Revenue / Total Assets |
| **Liquidity** | | | |
| currentPayment | float | Khả năng thanh toán hiện hành | Current Assets / Current Liab |
| quickPayment | float | Khả năng thanh toán nhanh | (CA - Inventory) / CL |
| **Leverage** | | | |
| debtOnEquity | float | D/E ratio | Total Debt / Equity |
| debtOnAsset | float | D/A ratio | Total Debt / Total Assets |
| ebitOnInterest | float | Interest coverage | EBIT / Interest Expense |
| equityOnTotalAsset | float | Equity ratio | Equity / Total Assets |
| **Growth** | | | |
| epsChange | float | EPS growth YoY | (EPS - EPS_prev) / EPS_prev |
| yearRevenueGrowth | float | Revenue growth YoY | - |
| bookValuePerShareChange | float | BVPS growth | - |

---

### 4. TCBS - Income Statement

**Endpoint:**
```
GET https://apipubaws.tcbs.com.vn/tcanalysis/v1/finance/{symbol}/incomestatement
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| yearly | int | No | 1 = yearly, 0 = quarterly |
| isAll | string | No | "true" = all data |

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| ticker | string | Mã chứng khoán |
| quarter | int | Quý |
| year | int | Năm |
| revenue | float | Doanh thu thuần (tỷ VND) |
| costOfGoodSold | float | Giá vốn hàng bán |
| grossProfit | float | Lợi nhuận gộp |
| operationExpense | float | Chi phí hoạt động |
| operationProfit | float | Lợi nhuận hoạt động |
| interestExpense | float | Chi phí lãi vay |
| preTaxProfit | float | Lợi nhuận trước thuế |
| postTaxProfit | float | Lợi nhuận sau thuế |
| shareHolderIncome | float | LN thuộc cổ đông công ty mẹ |
| ebitda | float | EBITDA |
| yearRevenueGrowth | float | Tăng trưởng doanh thu YoY |
| quarterRevenueGrowth | float | Tăng trưởng doanh thu QoQ |
| yearShareHolderIncomeGrowth | float | Tăng trưởng LNST YoY |
| quarterShareHolderIncomeGrowth | float | Tăng trưởng LNST QoQ |

---

### 5. TCBS - Balance Sheet

**Endpoint:**
```
GET https://apipubaws.tcbs.com.vn/tcanalysis/v1/finance/{symbol}/balancesheet
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| ticker | string | Mã chứng khoán |
| quarter | int | Quý |
| year | int | Năm |
| **Assets** | | |
| asset | float | Tổng tài sản (tỷ VND) |
| shortAsset | float | Tài sản ngắn hạn |
| cash | float | Tiền và tương đương tiền |
| shortInvest | float | Đầu tư ngắn hạn |
| shortReceivable | float | Phải thu ngắn hạn |
| inventory | float | Hàng tồn kho |
| longAsset | float | Tài sản dài hạn |
| fixedAsset | float | Tài sản cố định |
| **Liabilities** | | |
| debt | float | Tổng nợ phải trả |
| shortDebt | float | Nợ ngắn hạn |
| longDebt | float | Nợ dài hạn |
| **Equity** | | |
| equity | float | Vốn chủ sở hữu |
| capital | float | Vốn góp |
| centralBankDeposit | float | Tiền gửi NHNN (cho ngân hàng) |
| otherBankDeposit | float | Tiền gửi TCTD khác |
| unDistributedIncome | float | Lợi nhuận chưa phân phối |

---

### 6. TCBS - Cash Flow

**Endpoint:**
```
GET https://apipubaws.tcbs.com.vn/tcanalysis/v1/finance/{symbol}/cashflow
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| ticker | string | Mã chứng khoán |
| quarter | int | Quý |
| year | int | Năm |
| fromSale | float | Dòng tiền từ hoạt động kinh doanh (CFO) |
| fromInvest | float | Dòng tiền từ hoạt động đầu tư (CFI) |
| fromFinancial | float | Dòng tiền từ hoạt động tài chính (CFF) |
| investCost | float | Chi đầu tư (CAPEX) |
| freeCashFlow | float | Dòng tiền tự do (FCF = CFO - CAPEX) |

---

## Database Schema

### Table: symbols

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK (Primary Key) |
| name | TEXT | Tên công ty |
| exchange | TEXT | Sàn (HOSE/HNX/UPCOM) |
| industry | TEXT | Ngành |
| industry_en | TEXT | Ngành (EN) |
| no_employees | INTEGER | Số nhân viên |
| foreign_percent | REAL | % sở hữu NN |
| outstanding_shares | REAL | CP lưu hành |
| listed_date | DATE | Ngày niêm yết |

### Table: daily_prices

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK |
| date | DATE | Ngày giao dịch |
| open | REAL | Giá mở cửa |
| high | REAL | Giá cao nhất |
| low | REAL | Giá thấp nhất |
| close | REAL | Giá đóng cửa |
| adj_close | REAL | Giá điều chỉnh |
| volume | INTEGER | Khối lượng |
| value | REAL | Giá trị |
| deal_volume | INTEGER | KL thỏa thuận |
| deal_value | REAL | GT thỏa thuận |
| change_pct | REAL | % thay đổi |
| returns | REAL | ln(close/prev) |
| volatility_20d | REAL | Vol 20 ngày |
| avg_volume_20d | REAL | KLGD TB 20 ngày |

### Table: fundamentals_quarterly

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK |
| year | INTEGER | Năm |
| quarter | INTEGER | Quý (1-4, 5=annual) |
| report_date | DATE | Ngày công bố |
| pe | REAL | P/E |
| pb | REAL | P/B |
| ps | REAL | P/S |
| ev_ebitda | REAL | EV/EBITDA |
| roe | REAL | ROE |
| roa | REAL | ROA |
| gross_margin | REAL | Biên LN gộp |
| operating_margin | REAL | Biên LN HĐ |
| net_margin | REAL | Biên LN ròng |
| eps | REAL | EPS |
| bvps | REAL | BVPS |
| dividend | REAL | Cổ tức |
| revenue_growth_yoy | REAL | Tăng trưởng DT |
| eps_growth_yoy | REAL | Tăng trưởng EPS |
| asset_turnover | REAL | Vòng quay TS |
| days_receivable | REAL | DSO |
| days_inventory | REAL | DIO |
| days_payable | REAL | DPO |
| cash_cycle | REAL | CCC |
| debt_to_equity | REAL | D/E |
| debt_to_assets | REAL | D/A |
| current_ratio | REAL | Current ratio |
| quick_ratio | REAL | Quick ratio |
| interest_coverage | REAL | ICR |

### Table: income_statement

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK |
| year | INTEGER | Năm |
| quarter | INTEGER | Quý |
| revenue | REAL | Doanh thu |
| cost_of_goods | REAL | Giá vốn |
| gross_profit | REAL | LN gộp |
| operating_expense | REAL | CP hoạt động |
| operating_profit | REAL | LN hoạt động |
| interest_expense | REAL | CP lãi vay |
| pretax_profit | REAL | LN trước thuế |
| net_profit | REAL | LN sau thuế |
| shareholder_income | REAL | LN CĐCTM |
| ebitda | REAL | EBITDA |
| revenue_growth_yoy | REAL | Tăng trưởng DT YoY |
| revenue_growth_qoq | REAL | Tăng trưởng DT QoQ |
| profit_growth_yoy | REAL | Tăng trưởng LN YoY |
| profit_growth_qoq | REAL | Tăng trưởng LN QoQ |

### Table: balance_sheet

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK |
| year | INTEGER | Năm |
| quarter | INTEGER | Quý |
| total_assets | REAL | Tổng tài sản |
| current_assets | REAL | TS ngắn hạn |
| cash | REAL | Tiền |
| short_term_investments | REAL | ĐT ngắn hạn |
| receivables | REAL | Phải thu |
| inventory | REAL | Tồn kho |
| fixed_assets | REAL | TSCĐ |
| total_liabilities | REAL | Tổng nợ |
| current_liabilities | REAL | Nợ ngắn hạn |
| short_term_debt | REAL | Vay ngắn hạn |
| long_term_debt | REAL | Vay dài hạn |
| total_debt | REAL | Tổng vay |
| total_equity | REAL | Vốn CSH |
| retained_earnings | REAL | LNCPP |

### Table: cashflow

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK |
| year | INTEGER | Năm |
| quarter | INTEGER | Quý |
| cfo | REAL | Cash from Operations |
| cfi | REAL | Cash from Investing |
| cff | REAL | Cash from Financing |
| net_cash_change | REAL | Thay đổi tiền ròng |
| capex | REAL | Capital Expenditure |
| fcf | REAL | Free Cash Flow |
| dividends_paid | REAL | Cổ tức đã trả |

### Table: alpha_factors

| Column | Type | Description |
|--------|------|-------------|
| symbol | TEXT | Mã CK |
| date | DATE | Ngày |
| mom_1m | REAL | Momentum 1 tháng |
| mom_3m | REAL | Momentum 3 tháng |
| mom_6m | REAL | Momentum 6 tháng |
| mom_12m | REAL | Momentum 12 tháng |
| mom_12m_1m | REAL | Momentum 12-1 tháng |
| rev_5d | REAL | Reversal 5 ngày |
| rev_20d | REAL | Reversal 20 ngày |
| vol_20d | REAL | Volatility 20 ngày |
| vol_60d | REAL | Volatility 60 ngày |
| idio_vol | REAL | Idiosyncratic vol |
| turnover_20d | REAL | Turnover 20 ngày |
| amihud_illiq | REAL | Amihud illiquidity |
| market_cap | REAL | Vốn hóa |
| log_market_cap | REAL | Log vốn hóa |
| pe_ttm | REAL | P/E trailing 12m |
| pb_mrq | REAL | P/B most recent Q |
| ps_ttm | REAL | P/S trailing 12m |
| roe_ttm | REAL | ROE TTM |
| roa_ttm | REAL | ROA TTM |
| gross_margin_ttm | REAL | Gross margin TTM |
| eps_growth_ttm | REAL | EPS growth TTM |
| revenue_growth_ttm | REAL | Revenue growth TTM |

---

## Abbreviations

| Abbreviation | Full Name | Vietnamese |
|--------------|-----------|------------|
| OHLC | Open, High, Low, Close | Giá mở, cao, thấp, đóng |
| EPS | Earnings Per Share | Lợi nhuận trên cổ phiếu |
| BVPS | Book Value Per Share | Giá trị sổ sách/CP |
| P/E | Price to Earnings | Giá trên lợi nhuận |
| P/B | Price to Book | Giá trên giá trị sổ sách |
| P/S | Price to Sales | Giá trên doanh thu |
| ROE | Return on Equity | Tỷ suất lợi nhuận trên VCSH |
| ROA | Return on Assets | Tỷ suất lợi nhuận trên TS |
| EBITDA | Earnings Before Interest, Tax, Depreciation, Amortization | LN trước lãi vay, thuế, KH |
| EV | Enterprise Value | Giá trị doanh nghiệp |
| D/E | Debt to Equity | Nợ trên vốn CSH |
| D/A | Debt to Assets | Nợ trên tổng TS |
| DSO | Days Sales Outstanding | Số ngày thu tiền |
| DIO | Days Inventory Outstanding | Số ngày tồn kho |
| DPO | Days Payable Outstanding | Số ngày trả tiền |
| CCC | Cash Conversion Cycle | Chu kỳ chuyển đổi tiền |
| CFO | Cash Flow from Operations | Dòng tiền từ HĐKD |
| CFI | Cash Flow from Investing | Dòng tiền từ HĐĐT |
| CFF | Cash Flow from Financing | Dòng tiền từ HĐTC |
| FCF | Free Cash Flow | Dòng tiền tự do |
| CAPEX | Capital Expenditure | Chi đầu tư TSCĐ |
| TTM | Trailing Twelve Months | 12 tháng gần nhất |
| MRQ | Most Recent Quarter | Quý gần nhất |
| YoY | Year over Year | So với cùng kỳ năm trước |
| QoQ | Quarter over Quarter | So với quý trước |
