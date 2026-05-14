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
One-sided CUSUM applied to daily high temperatures, with a July-August baseline for each year. Hyperparameters were tuned across multiple combinations and selected for stability, where consistent crossover years across threshold values mattered more than sensitivity. Unofficial end-of-summer dates were identified for each year, ranging from early September to mid-October.

**Summer Warming Trend**  
CUSUM applied to annual mean summer temperatures against a 1996-1998 baseline. Nine hyperparameter combinations were tested. The threshold was crossed only in 2011, an isolated spike that quickly returned below threshold.

**Holt-Winters and CUSUM Combined**  
Simple exponential smoothing was applied directly to the 20 end-of-summer dates from the CUSUM analysis (converted to day-of-year values), creating one observation per year rather than smoothing the raw daily temperature series. Alpha was set manually to 0.3 after the optimizer collapsed to near-zero (0.000066), which produced a near-constant output of ~263 for all years and made trend detection impossible.

A linear regression model fit to the smoothed end-of-summer dates produced a slope of 0.088 days per year, R²=0.018, and p=0.588. CUSUM on the smoothed values crossed the threshold in only one of nine hyperparameter combinations, and only in the final year of the dataset. There is no statistical evidence that the unofficial end of summer has gotten later in Atlanta over the 1996-2015 period.

---

## Key Findings

Summer mean temperatures showed no sustained warming trend in this 20-year dataset. The 2011 spike was real but isolated. The CUSUM statistic crossed the threshold and quickly returned, indicating a single anomalous year rather than a shift in the underlying pattern.

The end-of-summer timing analysis reached the same conclusion from a different direction. Applying exponential smoothing to the annual end-of-summer dates and fitting a linear trend produced no statistically significant result (slope=0.088 days/year, R²=0.018, p=0.588). Both analyses point to the same answer: no meaningful trend in either summer temperatures or summer length is evident in this dataset over the 1996-2015 period.

---

## What This Demonstrates

This one was interesting for reasons beyond the methods. The unofficial end of summer is a genuinely compelling question. Official calendar dates don't reflect when temperatures actually stop feeling like summer, and the answer varies by nearly two months across the 20-year dataset. The 2011 spike was visually striking and worth investigating, but CUSUM correctly identified it as a single anomalous year rather than the start of something sustained.

Whether 20 years is enough to detect a meaningful climate trend is a fair question. The results here don't rule one out — they just don't find one in this dataset.

---

*R code available upon request. As Georgia Tech OMSA coursework, it is not posted publicly out of respect for academic integrity for future students.*
