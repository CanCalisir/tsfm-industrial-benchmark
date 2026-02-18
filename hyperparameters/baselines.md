# Classical Baseline Configurations

This document details the hyperparameters used for the classical baseline models (AutoARIMA, CatBoost, MLP, DLinear) reported in the paper. All baselines used Early Stopping with a patience of 5 epochs monitoring the Validation Loss to prevent overfitting.

## 1. AutoARIMA


## 2. CatBoost (CAT)

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
  * `scheduler`: ReduceLROnPlateau (`factor=0.5`, `patience=3`)
  * `loss`: L1Loss (MAE)

## 4. DLinear
