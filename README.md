# A comparison of open time-series foundation models for industrial manufacturing applications

**Supplementary Material Repository**

This repository contains the supplementary data, experimental results, and hyperparameter configurations for the paper:

> **A comparison of open time-series foundation models for industrial manufacturing applications**
> 
> *Authors: Can Calisir, Simon Leszek*
> 
> *Conference: ESANN 2025*


## 📌  Summary
We benchmark three open-source Time-Series Foundation Models (Chronos 2, MOMENT, GTT) against classical baselines on real-world **Steel** (energy consumption) and **CNC** (milling tool wear) datasets.

**Key Finding:** TSFMs consistently outperform baselines in pattern-heavy tasks (Steel) but trail behind simple regressors in dynamic, control-based environments (CNC) where domain-specific covariates are essential.

---

<details>
<summary><strong>Click to view full Abstract</strong></summary>

Large-scale, pre-trained foundation models have recently been introduced for time-series modeling. While typically evaluated on broad forecasting benchmarks, we assess their suitability for industrial manufacturing. We benchmark three open-source time series foundation models (TSFMs) on two representative datasets: steel-plant energy consumption and computer numerical control (CNC) milling spindle current. In the structured, pattern driven steel setting, TSFMs consistently outperform classical baselines, even without task-specific training. In contrast, the highly dynamic CNC process reveals limited TSFM gains without domainspecific signals, with simple models excelling once control covariates are provided. These results highlight both the promise and current limitations of TSFMs for real-world industrial applications.
</details>

## 1. Experimental Results
The complete numerical results (MAE) for all models and baselines across all experimental settings (Zero-shot, Linear Probing, Fine-tuning) are available in the `results/` folder.

* [Download Full Results (Excel)](results/)
* [View Model Parameter Counts](results/model_sizes.xlsx)

## 2. Target Variable Analysis
We evaluate two datasets representing distinct industrial regimes.

### A. Steel Industry Energy Consumption
* **Regime:** Structured, Pattern-Driven
* **Characteristics:** High regularity with strong daily and weekly seasonality.
* **Resolution:** 15-minute intervals.
* **Insight:** This dataset represents a classic forecasting task where historical patterns strongly predict future values, favoring models that capture long-term dependencies.


### B. CNC Milling Spindle Current
* **Regime:** Highly Dynamic, Control-Based
* **Characteristics:** Non-stationary and irregular. The target variable (current) is driven by machine control commands rather than historical seasonality.
* **Resolution:** 10 Hz (High Frequency).
* **Insight:** This dataset represents a "dynamic" task where the target variable changes largely due to external control signals (covariates), making it difficult for models to predict based on history alone.
