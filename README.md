# Adaptive Trend Following Strategy: Kalman Filter & Meta-Labeling

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Status](https://img.shields.io/badge/Status-Research-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## 📖 Overview

This project presents a quantitative trading strategy for **ETH/USDT** designed to address the **Non-Stationary (Non-IID)** nature of financial markets. Unlike traditional Moving Averages which suffer from lag, this system utilizes a **Dual Kalman Filter** approach for adaptive trend detection.

To mitigate drawdown risks inherent in trend-following systems, the strategy incorporates a **Machine Learning (Random Forest)** layer for **Meta-Labeling**. This allows for **Dynamic Leverage** adjustment based on the predicted probability of signal success.

**Key Performance (Out-of-Sample 2023-Present):**
- **Sharpe Ratio:** 1.03
- **Max Drawdown:** Reduced from -73% (Fixed) to **-52% (ML Optimized)**.

## 🛠️ Key Features

### 1. Adaptive Signal Generation (Dual Kalman Filter)
- Treats the "true price" as a hidden state in a noisy environment.
- **Advantage:** Significantly reduces lag compared to SMA/EMA, allowing for earlier entries and faster exits during trend reversals.
- **Logic:** Long Entry when `Fast_Kalman > Slow_Kalman`.

### 2. Machine Learning Risk Management (Meta-Labeling)
- Implements **Marcos Lopez de Prado’s Meta-Labeling** technique.
- A **Random Forest Classifier** is trained to predict whether a Kalman signal will result in a profit.
- **Features Used:** Kalman Spread, Volatility, RSI, and Volume Trend.
- **Dynamic Leverage:**
  - High Confidence (>55%): **2.0x Leverage**
  - Neutral (>50%): **1.0x Leverage**
  - Low Confidence: **0.5x Leverage** (Defensive Mode)

### 3. Strict Backtesting Standards
- **Look-Ahead Bias Free:** All ML predictions are shifted (`t+1`) to ensure signals are available before the candle opens.
- **Out-of-Sample Testing:** The model is trained on 2019-2022 data and tested on unseen 2023-Present data.

## 📊 Performance Analysis

The integration of Machine Learning transformed the strategy from a high-risk system into a robust investment vehicle.

| Metric | Fixed Leverage (1.5x) | ML Dynamic Leverage | Improvement |
| :--- | :---: | :---: | :---: |
| **Annualized Return** | 56.41% | 33.98% | Risk-Adjusted |
| **Sharpe Ratio** | 1.02 | **1.03** | **+1%** |
| **Max Drawdown** | -73.32% | **-52.56%** | **+28% Safety** |
| **Avg Win/Loss** | 3.67 | 3.67 | Maintained |

### Equity Curve Comparison
![Equity Curve](docs/images/equity_fixed_1_5x.png)
*Figure 1: Comparison between Strategy (Red) and Buy & Hold (Gray).*

### Impact of ML Optimization
![ML Comparison](docs/images/ml_comparison_chart.png)
*Figure 2: The ML Dynamic model (Purple) significantly reduces drawdown during market corrections compared to the Fixed Leverage model (Gray).*

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- Jupyter Notebook

### Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/yourusername/Adaptive-Kalman-ML-Trading.git](https://github.com/yourusername/Adaptive-Kalman-ML-Trading.git)
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

📜 License
Distributed under the MIT License. See LICENSE for more information.
