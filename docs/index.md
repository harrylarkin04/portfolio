# Trading Research Portfolio

Hi, I’m **Harry Larkin**. I build **systematic FX / macro research prototypes** with a focus on **regime instability**, **model robustness**, and **risk sizing**.

**What this site is:** a compact portfolio of research notes, model definitions, diagnostics, and implementation logic.  
**What this site is not:** investment advice or a promise of future returns.

---

## Featured work

### Residual-Blowout Filter (White Letter)
A regime-failure detector for rolling macro regressions: it monitors **out-of-sample residual behaviour** (magnitude + frequency), converts it to **instability scores**, and triggers a **risk-off / pause** state when relationships break down.

➡️ **Read the white letter:** *White Letter → Residual-Blowout Filter*

---

## What you’ll find here

- A clear **model definition** (rolling regression + residual construction)
- A **regime detection layer** (RMS + large-residual frequency + z-score normalisation)
- **Decision rules & thresholds** (pause logic designed for live trading constraints)
- **Simulated diagnostics** and interpretation (how/when the filter triggers)
- **Limitations** and next steps (false positives, calibration risk, heavy tails)

---

## Research interests

- Regime shifts and model breakdown detection  
- Volatility / tail risk and discontinuities  
- Robust sizing and drawdown control (e.g., Kelly-style thinking, volatility targeting)  
- Statistical validation and avoiding overfitting / alpha decay

---

## Tools & methods

- Time-series modelling: rolling regressions, residual diagnostics, stability monitoring  
- Risk: sizing constraints, drawdown-aware rules, stress assumptions  
- Communication: research notes structured like desk memos (model → logic → risk → limits)

---

## Contact

If you’d like to discuss the work or see additional notebooks/results, contact me via:

- **Email:** harry@larkin.me.uk
- **LinkedIn:** https://www.linkedin.com/in/harry-larkin/

---

> **Disclaimer:** This site is for research and educational purposes only, not investment advice.
