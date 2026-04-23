# memoire-IRRBB

# IRRBB — NII/EVE Efficient Frontier

**Did the 2022–2024 rate shock render IRRBB compliance and NII preservation incompatible for retail banks?**

*Nino Petiard — Master 1 MBFA, Université Paris 1 Panthéon-Sorbonne — 2025/2026*

---

## Overview

This project constructs a full quantitative simulation of interest rate risk management (IRRBB) for a stylised French retail bank, calibrated on the March 2024 EUR OIS curve.

The central question is whether IRRBB regulatory compliance and NII preservation are structurally incompatible after the 450 bp ECB tightening cycle of 2022–2024 — or whether the specific macro-financial configuration of March 2024 opens a compatibility window.

---

## Key Results

- Without hedging, **4 out of 6 EBA scenarios** trigger a prudential alert, with |ΔEVE| reaching **37.3% of Tier 1** (2.5× the regulatory threshold)
- A swap portfolio representing **33% of the balance sheet**, calibrated via formal SLSQP optimisation, brings all 6 scenarios into compliance
- The **NII/EVE efficient frontier** reveals a compatibility zone between **50% and 110%** of hedge coverage
- A **Hull-White Monte Carlo simulation** (1,000 trajectories) probabilises this zone: **83.3% compliance probability**
- The compatibility window is transitory: inverted curve carry (+29.8 M€/year in March 2024) turns negative upon rate normalisation

---

## Structure

```
├── write-up.pdf          # Full paper (26 pages)
├── IRRBB_model.ipynb     # Python simulation notebook
└── README.md
```

---

## Methodology

| Step | Description |
|------|-------------|
| Balance sheet calibration | 10 Bn€ stylised liability-sensitive balance sheet, calibrated on Banque de France & ACPR data |
| Yield curve | EUR OIS zero-coupon curve, March 2024, cubic spline interpolation |
| Client behaviour | Static EBA run-off approach + dynamic endogenous functions (prepayment sigmoid, demand deposit duration) |
| Stress testing | 6 EBA regulatory scenarios (parallel up/down, steepener, flattener, short rate up/down) |
| Hedging optimisation | Bucket-by-bucket SLSQP minimisation of covered notional under bilateral EBA constraints |
| Stochastic extension | Hull-White (κ=0.10, σ=1%), 1,000 trajectories, Euler-Maruyama discretisation |
| Dynamic extension | Endogenous prepayment & demand deposit duration, 500 trajectories |

---

## Tools

`Python` — `NumPy` · `SciPy` · `Matplotlib` · `pandas`

---

## Key Concepts

`IRRBB` · `NII` · `EVE` · `ALM` · `EBA Stress Scenarios` · `IRS Hedging` · `Hull-White` · `Monte Carlo` · `Efficient Frontier`
