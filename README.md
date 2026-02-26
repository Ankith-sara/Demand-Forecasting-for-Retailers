# Demand Forecasting for Retail Inventory Optimization

A hybrid demand forecasting system that combines **SARIMA** (statistical time-series) with **LSTM** (deep learning) to predict product demand and support inventory decisions for small and medium retailers.

Built with real Indian retail market data in mind, where seasonal patterns, regional buying behavior, and demand volatility make single-model approaches unreliable.

---

## The Problem

Retailers — particularly in diverse regional markets — routinely face overstocking, wastage, and revenue loss because their forecasting tools are too rigid. Statistical models like ARIMA handle trend and seasonality well but miss non-linear demand spikes. Pure deep learning models capture complexity but sacrifice interpretability and require large datasets. Neither alone is sufficient.

This project addresses that gap with a **hybrid architecture** that uses each model for what it does best.

---

## How It Works

```
Raw Sales Data
     ↓
Preprocessing & Feature Engineering
     ↓
SARIMA  →  Captures trend + seasonality
     ↓
LSTM    →  Learns residual non-linear patterns
     ↓
Hybrid Forecast Output
     ↓
Inventory & Procurement Insights
```

SARIMA runs first, providing a structured baseline forecast. Its output is then passed as an input signal to the LSTM, which learns the non-linear demand behavior that SARIMA can't model. The combination reduces variance and improves robustness over either model alone.

---

## Methodology

**Data Preprocessing** — missing value handling, normalization, and time-index alignment to prepare retail sales data for both model types.

**SARIMA Modeling** — captures seasonal cycles and long-run trends, acts as an interpretable baseline, and provides the structured signal fed into the LSTM.

**LSTM Modeling** — learns complex, non-linear demand patterns and handles sudden fluctuations that pure statistical models miss.

**Hybrid Integration** — SARIMA output is used as a feature input to the LSTM, letting the deep learning layer focus on what the statistical model leaves unexplained.

---

## Results

- ~82% forecasting accuracy on real retail datasets
- Measurable reduction in stock inefficiencies
- Applicable across product categories and regional demand profiles

---

## Tech Stack

| Layer              | Technology                |
| ------------------ | ------------------------- |
| Language           | Python                    |
| Time-Series Models | ARIMA, SARIMA             |
| Deep Learning      | LSTM (Keras / TensorFlow) |
| Data Processing    | Pandas, NumPy             |
| Visualization      | Matplotlib, Seaborn       |
| Evaluation Metrics | MAE, RMSE, MAPE           |

---

## Project Structure

```
data/             → Retail sales datasets
preprocessing/    → Data cleaning and feature engineering
sarima_model/     → Statistical time-series forecasting
lstm_model/       → Deep learning forecasting
hybrid_model/     → SARIMA + LSTM integration
evaluation/       → Accuracy metrics and validation
visualization/    → Forecast plots and analysis
```

---

## Getting Started

### 1. Clone the repo

```bash
git clone <your-repo-url>
cd demand-forecasting
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Preprocess data

```bash
python preprocessing/preprocess.py
```

### 4. Train models

```bash
python sarima_model/train.py
python lstm_model/train.py
```

### 5. Generate forecasts

```bash
python hybrid_model/forecast.py
```

---

## What I Learned

- **Hybrid model design** — learning when to layer models rather than choosing between them; the key insight was that SARIMA's residuals carry non-linear signal that LSTM can learn from, making the combination more powerful than stacking them independently
- **Time-series data discipline** — proper time-index alignment and avoiding data leakage in train/test splits are easy to get wrong and have a large effect on reported accuracy
- **Interpretability vs. accuracy trade-offs** — SARIMA alone is explainable to a non-technical stakeholder; LSTM alone is opaque but more accurate; the hybrid forces a deliberate decision about how much interpretability to preserve at each stage
- **Evaluation metric selection** — MAPE is intuitive for retail contexts (percentage error maps to business impact) but breaks down near zero-demand periods; understanding when to prefer MAE vs. RMSE vs. MAPE matters for honest model comparison

---

## Limitations

- Cyclic demand patterns (e.g. multi-year product cycles) not explicitly modeled
- LSTM trained on historical sales only — no external signals such as weather, local festivals, or promotions
- Real-time forecasting not yet implemented

---

## Roadmap

- [ ] Cyclic demand modeling
- [ ] External factor integration (weather, festival calendars, promotional events)
- [ ] Real-time forecasting API
- [ ] Transformer-based time-series models (e.g. Temporal Fusion Transformer)
- [ ] Direct retailer–manufacturer integration for procurement automation

---

## References

- Box, Jenkins, Reinsel. *Time Series Analysis: Forecasting and Control* — [Wiley](https://www.wiley.com/en-us/Time+Series+Analysis%3A+Forecasting+and+Control-p-9780470272848)
- Hochreiter & Schmidhuber (1997). *Long Short-Term Memory*. Neural Computation — [PDF](https://www.bioinf.jku.at/publications/older/2604.pdf)
- Hyndman & Athanasopoulos. *Forecasting: Principles and Practice* — [otexts.com/fpp3](https://otexts.com/fpp3/)
