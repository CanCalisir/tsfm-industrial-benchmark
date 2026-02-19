# Baseline Configurations

This document details the hyperparameters used for the baseline models (AutoARIMA, CatBoost, MLP, DLinear) reported in the paper.

## 1. AutoARIMA
* **Search Space:**
  * **AR / MA terms (max_p, max_q):** 5 / 5
  * **Seasonal terms (max_P, max_Q):** 2 / 2
  * **Differencing (d, D):** Automatically determined
* **Configuration:**
  * **Seasonality:** Enabled (Period auto-inferred from data frequency)
  * **Max Time Steps:** 2500 (Uses only the last 2500 steps for fitting)
  * **Optimization:** Stepwise search using Information Criterion


## 2. CatBoost (CAT)

* **Architecture:**
  * **Tree Depth (`depth`):** 6 (Yielding 64 leaves per tree)
  * **Max Trees (`iterations`):** 10,000 

* **Training & Convergence:**
  * `learning_rate`: Auto-selected by dataset size properties
  * `loss_function`: MAE (Mean Absolute Error)
  * **Convergence Strategy:** Relies heavily on Early Stopping. The algorithm is permitted to build up to 10,000 trees but will halt and save the best model if validation metrics stall, determining the final active parameter count dynamically.

## 3. MLP (SimpleFeedForward)
* **Architecture:**
  * **Hidden Layers:** [256, 128, 64]
  * **Activation:** ReLU
  * **Normalization:** BatchNorm1d (applied after every dense layer)
  * **Dropout:** 0.2 (Layer 1) / 0.1 (Layer 2) / None (Layer 3)
 
* **Training:**
  * `batch_size`: 256
  * `learning_rate`: 1e-3
  * `optimizer`: AdamW (`weight_decay=1e-4`)
  * `scheduler`: ReduceLROnPlateau (`factor=0.5`, `patience=5`)
  * `early_stopping`: patience=10 (stops if validation loss fails to improve for 10 total epochs)
  * `loss`: L1Loss (MAE)

## 4. DLinear
* **Architecture:**
  * **Hidden Dimension:** 20
  * **Scaling:** Mean Absolute Scaling
  * **Output:** Student-T Distribution
* **Training:**
  * `epochs`: 100
  * `batch_size`: 64
  * `learning_rate`: 1e-3
  * `weight_decay`: 1e-8
  * `early_stopping`: Patience = 20 epochs
