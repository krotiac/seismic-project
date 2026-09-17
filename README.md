# Seismic Ground Motion Prediction

Machine learning framework for predicting seismic ground motion intensity measures using a Bidirectional LSTM with attention and an Explainable Boosting Machine (EBM), trained on the Engineering Strong-Motion (ESM) database.

## Overview

Accurate ground motion prediction is important for seismic hazard analysis and earthquake-resistant engineering design.

This project develops and compares two machine learning approaches for predicting earthquake ground motion:

- **Bidirectional LSTM (BiLSTM)** with an attention mechanism
- **Explainable Boosting Machine (EBM)** with interpretable shape functions

Both models predict ground motion across **36 spectral periods from 0.01 s to 10.0 s**, together with PGA, allowing the complete response spectrum to be predicted from earthquake and site characteristics.

The models are evaluated under two configurations:

- **Case A:** Without focal depth
- **Case B:** With focal depth

The same train/test split is used for both models to ensure a fair comparison.

## Dataset

The models are trained using the **Engineering Strong-Motion (ESM) database**.

After filtering, the dataset contains:

- **8,543** three-component strong-motion records
- Moment magnitude: **4.1 – 7.7 Mw**
- Joyner-Boore distance: **0.5 – 199.9 km**
- Vs30: **198 – 2,104 m/s**
- Focal depth: **0.1 – 40 km**

The records contain earthquake source, propagation path, and site-condition information. :contentReference[oaicite:1]{index=1}

### Input Features

The models use physically motivated predictors:

- Moment magnitude (`Mw`)
- Joyner-Boore distance (`Rjb`)
- `log(Rjb)`
- `log(Vs30)`
- Fault mechanism
  - Strike-Slip
  - Reverse
  - Normal
- Focal depth for Case B

Fault mechanism is one-hot encoded rather than represented using ordinal integer values. Continuous features are standardized using statistics calculated only from the training set. :contentReference[oaicite:2]{index=2}

## Prediction Target

The target is the natural logarithm of pseudo-spectral acceleration:

```text
y = ln(PSA)
