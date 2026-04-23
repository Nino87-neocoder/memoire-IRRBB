# memoire-IRRBB

# IRRBB — NII/EVE Efficient Frontier

**Did the 2022–2024 rate shock render IRRBB compliance and NII preservation incompatible for retail banks?**

*Nino Petiard — Master 1 MBFA, Université Paris 1 Panthéon-Sorbonne — 2025/2026*

---

## Overview

This project constructs a full quantitative simulation of interest rate risk management (IRRBB) for a stylised French retail bank, calibrated on the March 2024 EUR OIS curve.

The central question is whether IRRBB regulatory compliance and NII preservation are structurally incompatible after the 450 bp ECB tightening cycle of 2022–2024, or whether the specific macro-financial configuration of March 2024 opens a compatibility window.

---

## Context & Motivation

Between July 2022 and September 2023, the ECB raised its deposit rate by 450 basis points, the fastest tightening cycle since the creation of the euro area. This shock exposed a structural vulnerability that had quietly accumulated over a decade of near-zero rates: French retail banks had massively extended long-term fixed-rate mortgages while funding them with short-term deposits. A classic liability-sensitive balance sheet, perfectly rational in a low-rate environment, suddenly faced a brutal repricing asymmetry.

The tension this creates is well-known in theory: protecting economic value (EVE) against rising rates requires hedging instruments that cost on the income statement (NII). But what made March 2024 unusual, and worth studying, is that the inverted yield curve flipped this trade-off. Pay-fixed swaps, which had historically generated 30–40 M€/year of negative carry, were suddenly generating *positive* carry. Hedging was not only a regulatory necessity; it had become economically attractive.

This project investigates whether this alignment between regulatory compliance and economic optimality is real, how wide the compatibility window actually is, and crucially whether it holds under uncertainty.

## Approach

Rather than a purely theoretical treatment, the paper follows the operational logic of an ALM committee: starting from a calibrated balance sheet, computing NII and EVE under the six EBA regulatory stress scenarios, designing a hedging strategy bucket by bucket, and then constructing the NII/EVE efficient frontier inspired by Markowitz to map all accessible (NII, EVE) pairs as a function of hedge coverage.

Two extensions then challenge the deterministic conclusions. A Hull-White Monte Carlo simulation (1,000 trajectories calibrated on the March 2024 OIS curve) probabilises the compliance zone, revealing that it is accessible with 83.3% probability but that 16.7% of plausible rate trajectories still leave the balance sheet in prudential alert despite hedging. A second extension integrates endogenous client behaviours, prepayment logistic functions and rate-sensitive demand deposit durations, to test whether the conclusions hold when the balance sheet itself adapts to the rate path.

The result is a decision-making tool, not just a diagnostic: the efficient frontier transforms a complex multidimensional optimisation problem into a legible map of trade-offs for institutional governance.

## Key Results

- Without hedging, **4 out of 6 EBA scenarios** trigger a prudential alert, with |ΔEVE| reaching **37.3% of Tier 1** (2.5× the regulatory threshold)
- A swap portfolio representing **33% of the balance sheet**, calibrated via formal SLSQP optimisation, brings all 6 scenarios into compliance
- The **NII/EVE efficient frontier** reveals a compatibility zone between **50% and 110%** of hedge coverage
- A **Hull-White Monte Carlo simulation** (1,000 trajectories) probabilises this zone: **83.3% compliance probability**
- The compatibility window is transitory: inverted curve carry (+29.8 M€/year in March 2024) turns negative upon rate normalisation

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
