# SK hynix 3Q26 Earnings Forecast

**Pre-Earnings Report v1.0**  
**Independent Research**  
**Forecast date:** 2026-09-26  
**Information cutoff:** 2026-09-26

> **Key question:** How much do shipments, product mix and ASP, and foreign exchange each contribute to 3Q26 growth?

This repository records an independently researched SK hynix 3Q26 earnings forecast prepared before the earnings release. The model uses company disclosures and guidance, government price and trade data, observed exchange rates, and independent market data. Brokerage and consensus forecasts are **not** used as model inputs.

The official evaluation target is the **3Q26 Base Case**. Bear and Bull scenarios represent uncertainty ranges and do not replace the Base Case in the post-earnings accuracy review.

---

## Official Base Case

| Metric | 3Q26 Base Case |
|---|---:|
| Revenue | **KRW 100.0 trillion** |
| Operating Profit | **KRW 79.2 trillion** |
| Operating Margin | **79.2%** |

### Scenario Summary

| Scenario | Revenue | Operating Profit | OP Margin |
|---|---:|---:|---:|
| Bear | KRW 96.2 tn | KRW 75.2 tn | 78.3% |
| **Base** | **KRW 100.0 tn** | **KRW 79.2 tn** | **79.2%** |
| Bull | KRW 102.9 tn | KRW 82.3 tn | 79.9% |

---

## Executive Summary

The 3Q26 Base Case assumes:

- **DRAM shipment growth:** +10.0% QoQ
- **NAND shipment growth:** +3.0% QoQ
- **DRAM dollar ASP growth:** +25.73%
- **NAND dollar ASP growth:** +17.58%
- **FX translation:** -5.5%

The FX effect compares the 2Q26 average of **KRW 1,501.60/USD** with the estimated 3Q26 average of **KRW 1,418.71/USD**.

The resulting Base Case forecast is:

- **Revenue:** KRW 100.0 trillion
- **Operating Profit:** KRW 79.2 trillion
- **Operating Margin:** 79.2%

The price assumptions are based on linear regressions of the April-August monthly contract-price series labeled `DDR516Gb` and `NAND128Gb` in the MOTIR source. September prices are estimated from those regressions, and the model compares the 2Q averages with the estimated 3Q averages.

The M15X production contribution is treated as already included in company DRAM shipment guidance and is **not added again**.

---

## 2Q26 Actual Results Baseline

| Item | DRAM | NAND | Other | Total Revenue | Operating Profit | Operating Costs |
|---|---:|---:|---:|---:|---:|---:|
| 2Q26 Actual | 56.983 | 21.960 | 0.376 | 79.319 | 60.543 | 18.776 |

All figures are in **KRW trillion**.

Operating costs are calculated as:

```text
79.3187 - 60.5426 = KRW 18.7761 trillion
```

---

## 3Q26 Drivers

| Driver | Direct Observation | Base Input | Interpretation |
|---|---|---:|---|
| DRAM Shipments | Company guidance of approximately +10% | +10.0% | Server-led shipment growth |
| NAND Shipments | Company guidance of low-single-digit growth | +3.0% | Midpoint of qualitative range |
| DRAM Dollar ASP | Linear regression of Apr-Aug DDR516Gb prices | +25.73% | September estimate: USD 49.95 |
| NAND Dollar ASP | Linear regression of Apr-Aug NAND128Gb prices | +17.58% | September estimate: USD 32.88 |
| FX Translation | 2Q avg KRW 1,501.60 → est. 3Q KRW 1,418.71 | -5.5% | Won appreciation |

### ASP model details

**DRAM**
- 2Q average: USD **37.50**
- Estimated 3Q average: USD **47.15**
- Estimated September price: USD **49.95**
- Implied 3Q ASP growth: **+25.73%**

**NAND**
- 2Q average: USD **26.50**
- Estimated 3Q average: USD **31.16**
- Estimated September price: USD **32.88**
- Implied 3Q ASP growth: **+17.58%**

These ASP growth rates are **model estimates, not company guidance**.

---

## New Fab Ramp Check

| Facility | Confirmed Schedule | Treatment in 2026 Forecast |
|---|---|---|
| Cheongju M15X | Cleanroom opened Oct 2025; wafer input in 1Q26; gradual ramp | Included in 3Q shipment guidance |
| Yongin Phase 1 | First cleanroom expected in early 2027 | Excluded from 2026 production |
| Cheongju M17 | Cleanroom target Dec 2028 | Excluded |
| Yongin Y2 | Cleanroom target Jun 2029 | Excluded |

---

## Forecast Model

Product revenue is estimated by separating shipments, dollar ASP, and FX translation:

```text
Product revenue(t)
= Product revenue(t-1)
× (1 + bit shipment growth)
× (1 + dollar ASP growth)
× (1 + FX translation effect)
```

Operating profit is estimated as:

```text
Operating profit
= Total revenue - Estimated operating costs
```

Operating costs begin with actual 2Q26 costs, increase with weighted shipment growth, and include an **M15X/HBM4 ramp cost allowance of KRW 0.5 trillion**.

The weighting uses approximate product-revenue shares of:

- **DRAM:** 72%
- **NAND:** 28%

---

## 3Q26 Base Case Calculation

| Item | Formula | Result |
|---|---|---:|
| DRAM Revenue | 56.983 × 1.10 × 1.2573 × 0.945 | 74.47 |
| NAND Revenue | 21.960 × 1.03 × 1.1758 × 0.945 | 25.13 |
| Other Revenue | 0.376 × 0.945 | 0.36 |
| Total Revenue | 74.47 + 25.13 + 0.36 | 99.96 → 100.0 |
| Weighted Shipment Growth | 72% × 10% + 28% × 3% | 8.04% |
| Estimated Operating Costs | 18.776 × 1.0804 + 0.50 | 20.79 |
| Operating Profit | 99.9625 - 20.7857 | 79.1768 → 79.2 |
| Operating Margin | 79.1768 ÷ 99.9625 | 79.2% |

Calculations retain full precision and are rounded only for presentation.

---

## Bear / Base / Bull Scenarios

| Scenario | DRAM Shipments | DRAM ASP | NAND Shipments | NAND ASP | FX | Revenue | Operating Profit | Margin |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bear | +8% | +24.61% | +1% | +16.20% | -6.5% | 96.2 | 75.2 | 78.3% |
| **Base** | **+10%** | **+25.73%** | **+3%** | **+17.58%** | **-5.5%** | **100.0** | **79.2** | **79.2%** |
| Bull | +11% | +26.86% | +4% | +18.97% | -4.5% | 102.9 | 82.3 | 79.9% |

ASP scenarios add or subtract one standard prediction error from the September regression estimate. The report states September prediction errors of **USD 1.26 for DRAM** and **USD 1.10 for NAND**. Each regression uses only five observations, which limits confidence in the range.

---

## Post-Earnings Scorecard

Complete this after the 3Q26 earnings release. The v1.0 forecast values should not be revised.

| Driver | Forecast | Actual | Error | Postmortem |
|---|---:|---:|---:|---|
| DRAM shipment QoQ | +10.0% |  |  |  |
| DRAM ASP QoQ | +25.73% |  |  |  |
| NAND shipment QoQ | +3.0% |  |  |  |
| NAND ASP QoQ | +17.58% |  |  |  |
| FX translation | -5.5% |  |  |  |
| Revenue | 99.96 |  |  |  |
| Operating Cost | 20.79 |  |  |  |
| Operating Profit | 79.18 |  |  |  |
| OP Margin | 79.2% |  |  |  |

```text
Forecast Error = (Actual - Forecast) / Actual
```

A positive value indicates **underforecasting** and a negative value indicates **overforecasting**.

---

## Sources

1. SK hynix, *SK hynix Announces 2Q26 Financial Results*, 2026-07-29  
   https://news.skhynix.com/en/q2-2026-business-results/

2. SK hynix, *2026 Half Year Report*, 2026-08-14

3. SK hynix, *Q2 2026 Earnings Call Transcript*, 2026-07-29  
   https://stockanalysis.com/quote/krx/000660/transcripts/653208-q2-2026/

4. SK hynix SEC filing, M15X disclosures  
   https://www.sec.gov/Archives/edgar/data/2120882/000119312526280172/d32785df1.htm

5. Ministry of Trade, Industry and Resources, *August 2026 Export and Import Trends*, 2026-09-01  
   https://www.motir.go.kr/kor/article/ATCL3f49a5a8c/172145/view

6. Korea Customs Service, *Preliminary August 2026 Trade Data*, 2026-09-01

7. X-Rates, *2026 USD/KRW Monthly Averages*  
   https://www.x-rates.com/average/?amount=1&from=USD&to=KRW&year=2026

8. OECD/FRED, *Cross Check of the 2Q26 Average Exchange Rate*  
   https://fred.stlouisfed.org/series/CCUSMA02KRQ618N

9. SK hynix, *Yongin Y2 and Cheongju M17 Investment Announcement*, 2026-08-07

---

## Locked Methodology

| Item | Locked Method |
|---|---|
| Information Cutoff | 2026-09-26 |
| Official Evaluation Target | 3Q26 Base Case: Revenue KRW 100.0 tn; Operating Profit KRW 79.2 tn |
| Use of External Forecasts | Brokerage and consensus forecasts are not used as inputs |
| Version Policy | Preserve v1.0 and issue a separate post-earnings review |

---

## Disclaimer

This report is an independent research record for learning and forecast validation. It is **not investment advice or a solicitation**. Actual results, disclosures, accounting classifications, and market prices may differ from this forecast.
