# Atlanta Climate Analysis

**Domain:** Environmental Analysis · Time Series  
**Tools:** R, CUSUM, Holt-Winters  

---

## The Problem

Two related questions about Atlanta daily high temperature data spanning 20 years (1996-2015):

1. When does summer unofficially end each year, and has that date been shifting later?
2. Has Atlanta's summer climate gotten measurably warmer over that period?

---

## The Approach

**End of Summer Detection**  
One-sided CUSUM applied to daily high temperatures, with a July-August baseline for each year. Hyperparameters were tuned across multiple combinations and selected for stability — consistent crossover years across threshold values mattered more than sensitivity. Unofficial end-of-summer dates were identified for each year, ranging from early September to mid-October.

**Summer Warming Trend**  
CUSUM applied to annual mean summer temperatures against a 1996-1998 baseline. Nine hyperparameter combinations were tested. The threshold was crossed only in 2011 — an isolated spike that quickly returned below threshold.

**Holt-Winters and CUSUM Combined**  
Holt-Winters triple exponential smoothing applied to the full 20-year series to extract the seasonal component before running CUSUM. Removing short-term noise before change detection surfaces patterns that raw data alone may not clearly show. *(Results to be updated.)*

---

## Key Findings

Summer mean temperatures showed no sustained warming trend in this 20-year dataset. The 2011 spike was real but isolated — the CUSUM statistic crossed the threshold and quickly returned, indicating a single anomalous year rather than a shift in the underlying pattern.

End-of-summer detection and the Holt-Winters combined analysis address the seasonal timing question from two different angles.

---

## What This Demonstrates

- CUSUM hyperparameter selection based on stability over sensitivity
- Applying the same method to different questions with appropriate configurations
- Combining exponential smoothing and change detection to separate signal from noise
