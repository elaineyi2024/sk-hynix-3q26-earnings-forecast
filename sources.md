# Sources and Method Notes

This file documents the external sources, company disclosures, and modeling inputs used in the **SK hynix 3Q26 Earnings Forecast — Pre-Earnings Report v1.0**.

**Forecast date:** 2026-09-26  
**Information cutoff:** 2026-09-26

The project is designed as a pre-earnings forecast record. Brokerage and consensus forecasts are **not used as model inputs**. The official evaluation target is the 3Q26 Base Case.

---

## 1. SK hynix — 2Q26 Financial Results

**Source:** SK hynix, *SK hynix Announces 2Q26 Financial Results*  
**Date:** 2026-07-29  
**Link:** https://news.skhynix.com/en/q2-2026-business-results/

### Used for
- 2Q26 operating performance context
- Company commentary on DRAM and NAND demand
- Cross-checking the 2Q26 earnings baseline

---

## 2. SK hynix — 2026 Half-Year Report

**Source:** SK hynix, *2026 Half-Year Report*  
**Date:** 2026-08-14

### Used for
- 2Q26 actual product revenue
- DRAM revenue: **KRW 56.983 trillion**
- NAND revenue: **KRW 21.960 trillion**
- Other revenue: **KRW 0.376 trillion**
- Total revenue: **KRW 79.319 trillion**
- Operating-profit baseline used in the forecast model

### Model role
These figures are the starting point for the 3Q26 product-level revenue forecast.

---

## 3. SK hynix — Q2 2026 Earnings Call Transcript

**Source:** SK hynix, *Q2 2026 Earnings Call Transcript*  
**Date:** 2026-07-29  
**Link:** https://stockanalysis.com/quote/krx/000660/transcripts/653208-q2-2026/

### Used for
- 3Q26 DRAM shipment guidance of approximately **+10% QoQ**
- NAND shipment guidance of **low-single-digit growth**
- Base Case NAND shipment assumption of **+3% QoQ**

### Modeling treatment
The DRAM shipment assumption is taken directly from the approximate company guidance.  
The NAND shipment assumption is the modeler's midpoint interpretation of the qualitative "low-single-digit" guidance.

---

## 4. SK hynix SEC Filing — M15X Disclosures

**Source:** SK hynix SEC filing  
**Link:** https://www.sec.gov/Archives/edgar/data/2120882/000119312526280172/d32785df1.htm

### Used for
- M15X production-ramp timing
- Cross-checking whether incremental capacity should be separately added to 3Q26 shipment growth

### Modeling treatment
M15X contribution is treated as **already reflected in company shipment guidance** and is therefore **not added again** to avoid double counting.

---

## 5. Ministry of Trade, Industry and Resources — August 2026 Export and Import Trends

**Source:** Ministry of Trade, Industry and Resources (MOTIR), *August 2026 Export and Import Trends*  
**Date:** 2026-09-01  
**Link:** https://www.motir.go.kr/kor/article/ATCL3f49a5a8c/172145/view

### Used for ASP forecasting
The Jupyter notebook uses the monthly contract-price observations labeled:

- `DDR516Gb`
- `NAND128Gb`

for April through August 2026.

The notebook inputs are:

| Month | DRAM ASP | NAND ASP |
|---:|---:|---:|
| Apr | 35.0 | 24.2 |
| May | 37.5 | 26.5 |
| Jun | 40.0 | 28.8 |
| Jul | 45.0 | 30.1 |
| Aug | 46.5 | 30.5 |

These values are used in simple linear regressions to estimate September prices.

### Regression outputs used in the model

**DRAM**
- Estimated September price: **USD 49.95**
- 2Q26 average: **USD 37.50**
- Estimated 3Q26 average: **USD 47.15**
- Implied 3Q26 ASP growth: **+25.73%**

**NAND**
- Estimated September price: **USD 32.88**
- 2Q26 average: **USD 26.50**
- Estimated 3Q26 average: **USD 31.16**
- Implied 3Q26 ASP growth: **+17.58%**

These ASP growth rates are **independent model estimates, not SK hynix guidance**.

### Reproducible analysis
See:

`notebooks/Predicting_DRAM_and_NAND_ASP.ipynb`

The notebook performs the linear-regression estimates and calculates the quarterly ASP growth rates.

---

## 6. Korea Customs Service — Preliminary August 2026 Trade Data

**Source:** Korea Customs Service, *Preliminary August 2026 Trade Data*  
**Date:** 2026-09-01

### Used for
- Cross-checking the semiconductor trade environment
- Supporting the broader market-data context around memory pricing and exports

This source is used as a contextual cross-check rather than as a direct numerical forecast input.

---

## 7. X-Rates — 2026 USD/KRW Monthly Averages

**Source:** X-Rates, *2026 USD/KRW Monthly Averages*  
**Link:** https://www.x-rates.com/average/?amount=1&from=USD&to=KRW&year=2026

### Used for
- 2Q26 average USD/KRW: **KRW 1,501.60**
- Estimated 3Q26 average USD/KRW: **KRW 1,418.71**
- Calculated FX translation effect: approximately **-5.52%**
- Applied model assumption: **-5.5%**

### Important limitation
The 3Q average was still provisional at the information cutoff because the final September trading days had not yet occurred. Actual revenue translation can also differ because of invoice timing, settlement timing, hedging, and currency mix.

---

## 8. OECD / FRED — Exchange-Rate Cross-Check

**Source:** OECD/FRED, *Cross Check of the 2Q26 Average Exchange Rate*  
**Link:** https://fred.stlouisfed.org/series/CCUSMA02KRQ618N

### Used for
- Independent cross-check of the 2Q26 USD/KRW average used in the FX model

This source is used for validation rather than as a separate model input.

---

## 9. SK hynix — Yongin Y2 and Cheongju M17 Investment Announcement

**Source:** SK hynix, *Yongin Y2 and Cheongju M17 Investment Announcement*  
**Date:** 2026-08-07

### Used for
- New-fab schedule checks
- Excluding facilities that are not expected to contribute to 2026 production

### Forecast treatment

| Facility | Schedule | 2026 Forecast Treatment |
|---|---|---|
| Cheongju M15X | Cleanroom opened Oct 2025; wafer input in 1Q26; gradual ramp | Included in shipment guidance |
| Yongin Phase 1 | First cleanroom expected in early 2027 | Excluded |
| Cheongju M17 | Cleanroom target Dec 2028 | Excluded |
| Yongin Y2 | Cleanroom target Jun 2029 | Excluded |

---

# Modeling Methodology

## Product revenue

The forecast separates shipment growth, dollar ASP growth, and FX translation:

```text
Product Revenue(t)
= Product Revenue(t-1)
× (1 + Bit Shipment Growth)
× (1 + Dollar ASP Growth)
× (1 + FX Translation Effect)
```

## Operating profit

```text
Operating Profit
= Total Revenue - Estimated Operating Costs
```

Operating costs start from actual 2Q26 costs, increase with weighted shipment growth, and include a **KRW 0.5 trillion M15X/HBM4 ramp-cost allowance**.

The weighting uses approximate revenue shares of:

- DRAM: **72%**
- NAND: **28%**

---

# Base Case Inputs

| Driver | Base Case |
|---|---:|
| DRAM Shipments QoQ | +10.0% |
| DRAM Dollar ASP QoQ | +25.73% |
| NAND Shipments QoQ | +3.0% |
| NAND Dollar ASP QoQ | +17.58% |
| FX Translation | -5.5% |
| Ramp Cost Allowance | KRW 0.5 tn |

---

# Locked Methodology

| Item | Locked Method |
|---|---|
| Information Cutoff | 2026-09-26 |
| Official Evaluation Target | 3Q26 Base Case: Revenue KRW 100.0 tn; Operating Profit KRW 79.2 tn |
| Use of External Forecasts | Brokerage and consensus forecasts are not used as inputs |
| Version Policy | Preserve v1.0 and issue a separate post-earnings review |

---

# Reproducibility Files

Recommended repository structure:

```text
sk-hynix-3q26-earnings-forecast/
│
├── README.md
├── sources.md
├── SK_hynix_3Q26_Pre_Earnings_Report_v1.0_EN.pdf
├── SK_hynix_3Q26_Forecast_Model_v1.0.xlsx
│
└── notebooks/
    └── Predicting_DRAM_and_NAND_ASP.ipynb
```

The notebook contains the ASP regression work, while the Excel file contains the earnings model and scenario calculations.

---

# Methodological Limitations

- The ASP regressions use only **five monthly observations**, so the forecasts are sensitive to the assumed persistence of the linear trend.
- The September price is an estimate rather than an observed final monthly value.
- FX translation is simplified and may differ from realized company revenue translation because of hedging, currency mix, invoice timing, and settlement timing.
- Shipment guidance is qualitative or approximate in part.
- Product-mix effects are not modeled as a separate explicit HBM/DDR5 volume-price bridge.
- Scenario outputs should therefore be interpreted as a structured uncertainty range rather than precise statistical confidence intervals.

---

# Disclaimer

This project is an independent research record for learning and forecast validation. It is **not investment advice or a solicitation to buy or sell securities**. Actual results, disclosures, accounting classifications, exchange rates, and market prices may differ from the assumptions used in this model.
