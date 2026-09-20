# Predicting the Unpredictable: Uncertainty-Aware Water Demand Forecasting

**Mathematics & Data Science Dissertation — University of Exeter**

`Python` · `TensorFlow/Keras` · `Time Series Forecasting` · `Deep Learning` · `Transformers` · `Bayesian Inference`

## Project Overview

Accurate water-demand forecasting is important for helping utility providers balance supply and demand, optimise treatment operations and respond to changing consumption patterns.

This project investigates the use of deep learning for **short- to long-horizon water demand forecasting**, using operational Distribution Input (DI) data from a UK water utility as a real-world case study.

Three neural forecasting architectures were developed and compared:

- **CNN-LSTM** — combining convolutional feature extraction with recurrent sequence modelling.
- **Transformer** — using self-attention to capture long-range temporal dependencies.
- **Informer-inspired architecture** — designed for efficient multi-step forecasting over extended horizons.

The project also investigates **Monte Carlo Dropout as an approximate Bayesian inference technique**, enabling the forecasting model to communicate predictive uncertainty rather than returning point predictions alone.

> **Note:** The operational dataset used for this research is proprietary and therefore is not included in this repository. The modelling code and methodology are provided for demonstration and reproducibility of the modelling approach.

---

## Research Objective

The project explores whether modern attention-based neural architectures can provide accurate and computationally practical forecasts of real-time water demand while also quantifying uncertainty.

Models were evaluated across:

- **1-week forecasts**
- **4-week forecasts**
- **8-week forecasts**

The research places particular emphasis on the trade-off between **forecast accuracy, model complexity, uncertainty and real-world operational applicability**.

---

## Data & Feature Engineering

The original dataset contained **35,138 observations recorded at 15-minute intervals during 2024** across eight Water Treatment Works (WTWs).

The modelling experiments focus primarily on **Restormel Water Treatment Works**, which displayed substantial seasonal and short-term variability.

The preprocessing pipeline included temporal feature engineering such as:

- Hour of day
- Day of week
- Month of year
- Weekend indicator
- Sine/cosine cyclical encodings
- Resampling of high-frequency Distribution Input observations
- Sliding-window sequence generation for supervised forecasting

Operational anomalies and unusually low DI observations were deliberately considered rather than automatically smoothed away, since these events may contain meaningful information about real-world system behaviour.

For further information about the dataset and access restrictions, see [`data/README.md`](data/README.md).

---

## Modelling Approach

### 1. CNN-LSTM

The CNN-LSTM combines **1D convolutional layers** for extracting short-term patterns with an **LSTM layer** for learning longer temporal dependencies.

This provides a hybrid architecture capable of responding to both local demand fluctuations and broader seasonal behaviour.

### 2. Transformer

A Transformer architecture was implemented to investigate whether **self-attention** could improve modelling of long-range dependencies without the sequential processing bottleneck associated with recurrent networks.

The model incorporated:

- Encoder and decoder streams
- Multi-head attention
- Positional encoding
- Residual connections
- Layer normalisation
- Feed-forward neural layers

### 3. Informer-Inspired Model

The final architecture adapted concepts from the Informer for long-horizon time-series forecasting.

A sliding-window approach supplied historical sequences to an encoder-decoder architecture capable of generating the complete forecast horizon in a single forward pass.

For the 8-week experiment, the model used an extended historical context to improve long-range forecasting stability.

---

## Bayesian Uncertainty Estimation

Point forecasts alone do not communicate how confident a model is in its predictions — an important limitation when forecasting demand for critical infrastructure.

To address this, **Monte Carlo Dropout** was applied during inference.

Instead of disabling dropout after training, dropout remained active and the model performed **50 stochastic forward passes**. These predictions were used to estimate:

- Mean forecast
- Predictive variance
- Uncertainty intervals

This provides a computationally lightweight approximation to Bayesian inference and allows periods of higher model uncertainty to be identified.

---

## Results

Model performance was evaluated using **Mean Absolute Error (MAE)**, **Mean Squared Error (MSE)** and **R²**.

| Model | Forecast Horizon | MAE | MSE | R² |
|:---|:---:|---:|---:|---:|
| CNN-LSTM | 1 week | 2.82 | 23.63 | 0.848 |
| CNN-LSTM | 4 weeks | 2.79 | 23.39 | 0.850 |
| CNN-LSTM | 8 weeks | 3.12 | 26.47 | 0.831 |
| Transformer | 1 week | 2.81 | 27.09 | 0.845 |
| Transformer | 4 weeks | 1.09 | 2.56 | 0.985 |
| Transformer | 8 weeks | 1.12 | 2.78 | 0.985 |
| Informer | 1 week | **0.688** | **0.85** | **0.99** |
| Informer | 4 weeks | **0.860** | **1.00** | **0.99** |
| Informer | 8 weeks | **0.863** | **1.08** | **0.99** |

The Informer-based architecture produced the strongest reported performance across the tested forecasting horizons, while MC Dropout enabled uncertainty to be estimated alongside the point forecasts.

---

## Key Findings

The experiments demonstrated that attention-based architectures can model both short-term fluctuations and longer temporal structure in water-demand data.

The **Informer-based model maintained strong reported performance across 1-, 4- and 8-week horizons**, while the Transformer showed substantial improvements at the longer forecasting horizons compared with its 1-week experiment.

Monte Carlo Dropout also demonstrated how uncertainty estimation can be incorporated into deep forecasting architectures without requiring a fully Bayesian neural network.

---

## Limitations

The results should be interpreted alongside several important limitations.

Calendar-based covariates such as hour-of-day and day-of-week encode strong periodic patterns. Although these variables do **not expose future water-demand values**, they may contribute substantially to predictive performance under stable seasonal conditions.

The narrow uncertainty intervals produced in some experiments may also indicate that the model remains overly confident in highly structured periods.

Future work could therefore investigate:

- Exogenous weather variables such as rainfall and temperature
- Deep ensembles
- DeepAR
- N-BEATS
- Temporal Fusion Transformers
- Alternative uncertainty-calibration methods
- Generalisation across multiple Water Treatment Works

---

## Repository Structure

```text
water-demand-forecasting/
│
├── data/
│   └── README.md              # Dataset description and access restrictions
│
├── notebooks/
│   ├── LSTM_CNN2025.ipynb     # CNN-LSTM forecasting model
│   ├── transformer2025.ipynb  # Transformer forecasting model
│   ├── SimpleInformer.ipynb   # Informer-based model
│   └── 8weekInformer.ipynb    # Extended 8-week Informer experiment
│
├── .gitignore                 # Excludes proprietary data and local files
└── README.md
```

---

## Technologies

**Languages & Libraries:** Python, NumPy, Pandas, TensorFlow/Keras, Scikit-learn, Matplotlib

**Machine Learning:** CNNs, LSTMs, Transformers, attention mechanisms, Monte Carlo Dropout

**Techniques:** Time-series forecasting, feature engineering, sliding-window modelling, uncertainty quantification, regression evaluation

---

## Dissertation

**Predicting the Unpredictable with Bayesian Inference: Real Time Water Demand**

Mathematics & Data Science  
University of Exeter

The research investigates the integration of modern sequential neural architectures with uncertainty quantification for real-world water-demand forecasting.

---

## Author

**Nick Belemet**  
Mathematics & Data Science Graduate — University of Exeter
