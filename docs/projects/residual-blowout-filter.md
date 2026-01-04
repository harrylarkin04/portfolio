# Residual-Blowout Filter for Macro Trading

This document summarises my *Residual-Blowout Filter for Macro Trading* white letter.

The objective is to **detect regime failure in rolling macro models** and temporarily **pause trading** when model relationships break down.

> This filter is **not a signal generator**.  
> It is a **model-robustness and regime-failure detector**.

---

## 1. Purpose

Macro regressions can appear stable for long periods and then fail abruptly during regime changes.

This filter monitors **out-of-sample residual behaviour** and triggers a *risk-off / pause* state when model errors become abnormally large or frequent.

---

## 2. Base Model (Rolling Regression)

The macro model is estimated on a rolling window:

$$
r^{EURUSD}_t
=
\beta_0
+ \beta_1 DXY_t
+ \beta_2 r^{SP500}_t
+ \beta_3 VIX_t
+ \beta_4 \left(i^{EU}_t - i^{US}_t\right)
+ \varepsilon_t
$$

where:

- $r^{EURUSD}_t$ = EUR/USD return  
- $DXY_t$ = USD strength  
- $r^{SP500}_t$ = global risk sentiment  
- $VIX_t$ = volatility stress  
- $(i^{EU}_t - i^{US}_t)$ = rate differential  

---

## 3. Residual Definition

The model residual is defined as:

$$
\hat{\varepsilon}_t = r_t - \hat{r}_t
$$

We monitor $\hat{\varepsilon}_t$ for signs that the model has stopped describing market reality.

---

## 4. Filter Construction

The filter combines **error magnitude** and **error frequency**.

---

### Step B — Magnitude: Rolling RMS of Residuals

Compute the rolling RMS over a window $W$:

$$
RMS_t
=
\sqrt{
\frac{1}{W}
\sum_{i=t-W+1}^{t}
\hat{\varepsilon}_i^2
}
$$

This captures **how large** model errors have become.

---

### Step C — Frequency: Large Residual Events

Define a residual scale $\sigma_\varepsilon$ estimated over a calibration period.

Define the fraction of large residuals:

$$
F_t
=
\frac{1}{W_f}
\sum
\mathbf{1}
\left(
\lvert \hat{\varepsilon}_i \rvert
>
k \, \sigma_\varepsilon
\right)
$$

This captures **how often** extreme errors occur.

---

### Step D — Normalisation (Z-Scores)

Convert $RMS_t$ and $F_t$ into z-scores using calibration means and standard deviations:

$$
Z^{RMS}_t = \frac{RMS_t - \mu_{RMS}}{\sigma_{RMS}},
\quad
Z^{F}_t = \frac{F_t - \mu_F}{\sigma_F}
$$

---

## 5. Composite Regime-Failure Score

Combine magnitude and frequency:

$$
S_t = Z^{RMS}_t + Z^{F}_t
$$

---

## 6. Trading Logic

- If $S_t$ exceeds a calibrated threshold:
  - **Pause macro trading**
- Resume trading only once $S_t$ normalises

This avoids deploying macro strategies during **structural regime breaks**.

---

## 7. Interpretation

- High $Z^{RMS}_t$ → model errors are large  
- High $Z^{F}_t$ → model errors are frequent  
- High $S_t$ → **macro relationships unstable**

---

## 8. Limitations

- Filter is diagnostic, not predictive  
- Requires stable calibration periods  
- Extreme structural breaks may require model redesign

---

## 9. Use Case

This framework is suitable for:

- Macro funds
- Systematic FX strategies
- Risk overlays for discretionary trading
