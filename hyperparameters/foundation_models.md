# TSFM Configurations

This document details the hyperparameters used for the foundation models (Chronos 2, GTT, MOMENT) reported in the paper.

## 1. Chronos 2

## 2. GTT (General Time Transformer)

* **Creator:** Siemens
* **Architecture:** Encoder-only Transformer (adapted for Time Series)
* **Model Size:** Large Variant (`MODE = "large"`) (~57M parameters)

### A. Linear Probing Configuration
* **Strategy:** Name-Based Layer Freezing. The Transformer Encoder and RevIN blocks are frozen; only the final projection head (`head`) is trainable.
* **Optimization:**
  * `optimizer`: Adam
  * `learning rate`: 1e-4
  * `loss function`: MAE (Mean Absolute Error)
  * `Batch Size`: 256
  * `Early Stopping`: Patience = 5 epochs (monitoring Validation Loss)

### B. Full Fine-Tuning Configuration
* **Strategy:** Unfrozen Encoder. Both the Transformer Encoder and the final projection head are trainable. (RevIN remains frozen).
* **Optimization:**
  * `optimizer`: Adam
  * `learning rate`: 1e-5 (Lower learning rate utilized to preserve pre-trained backbone features)
  * `loss function`: MAE (Mean Absolute Error)
  * `batch size`: 256
  * `early stopping`: Patience = 5 epochs (monitoring Validation Loss)

## 3. MOMENT

* **Creator:** Carnegie Mellon University (Auton Lab)
* **Architecture:** Transformer Encoder (adapted from T5)
* **Variant Used:** `MOMENT-1-large` (~385M parameters)
* **Global Task Settings:**
  * `task_name`: 'forecasting'
  * `loss_function`: MSE (Mean Squared Error)

### A. Linear Probing Configuration
* **Strategy:** The pre-trained backbone is completely frozen. Only the newly initialized forecasting head is trained.
* **Model Configuration:**
  * `freeze_encoder`: True
  * `freeze_embedder`: True
  * `freeze_head`: False
* **Training:**
  * `optimizer`: Adam
  * `learning_rate`: 1e-4

### Full Fine-Tuning Configuration
* **Strategy:** All model weights are updated. Differential learning rates are applied to preserve pre-trained structural knowledge while adapting the final forecasting head.
* **Model Configuration:**
  * `freeze_encoder`: False
  * `freeze_embedder`: False
  * `freeze_head`: False
  * `head_dropout`: 0.1
* **Training:**
  * `optimizer`: AdamW (`weight_decay=1e-4`)
  * `gradient_clipping`: 1.0 (Max Norm)
  * **Differential Learning Rates:**
    * Encoder & Embedder (Backbone): `2e-5`
    * Forecasting Head: `1e-4`







