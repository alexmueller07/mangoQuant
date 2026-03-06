# MangoQuant 🥭
### Systematic Modeling of Agricultural Commodity Prices

MangoQuant is a **quantitative research framework** for modeling and trading mango commodity prices using time-series feature engineering, regularized regression models, and disciplined risk management.

## PRESENTATION: https://docs.google.com/presentation/d/17l1LMqoJQXy-SG0KYzmLTlTCudXaA0Hv1zekz3wimHs/edit?usp=sharing

The project explores a simple question:

> Can weak predictive signals in agricultural commodity prices be transformed into a systematic trading strategy?

While agricultural commodities are critical to global markets, they are rarely explored in retail quantitative research compared to equities or crypto. MangoQuant uses historical price and weather data to build a **predictive pipeline and risk-managed trading system**.

---

# Overview

The system:

1. Engineers predictive time-series features  
2. Trains regularized regression models  
3. Predicts next-day price direction  
4. Converts predictions into a trading strategy  
5. Applies volatility-based position sizing  
6. Evaluates performance strictly out-of-sample  

Rather than focusing purely on prediction accuracy, the system emphasizes **risk-adjusted capital allocation and realistic backtesting**.

---

# Key Features

- Time-series feature engineering (lags, rolling statistics, seasonality)
- Weather data integration from major mango-producing regions
- ElasticNet regularization for multicollinearity control
- Systematic long/short trading strategy
- Volatility-targeted position sizing
- Transaction cost and slippage modeling
- Strict chronological train/test split
- Out-of-sample performance evaluation

---

# Feature Engineering

Features are constructed using **strictly historical data** to avoid look-ahead bias.

### Lag Features

Previous price observations:

```
P(t-1), P(t-2), P(t-3), P(t-7), P(t-14), P(t-30)
```

### Rolling Statistics

Rolling mean and volatility:

```
μ(t) = mean(P(t-n))
σ(t) = std(P(t-n))
```

### Seasonality Encoding

To capture annual agricultural cycles:

```
sin(2π * day / 365)
cos(2π * day / 365)
```

### Weather Data

Weather indicators from **India and Mexico**, two major mango-producing countries, were incorporated as potential explanatory variables.

---

# Modeling Approach

Several models were evaluated:

- Linear Regression  
- Ridge Regression  
- ElasticNet  

Due to multicollinearity and the relatively large feature set, **ElasticNet regularization** performed best.

ElasticNet minimizes:

```
Loss + λ₁ * L1 penalty + λ₂ * L2 penalty
```

The model predicts **next-day price direction**, reframing the problem as a classification task.

### Out-of-Sample Accuracy

```
≈ 51.3%
```

Although accuracy is only slightly above random, weak signals can still be profitable when combined with proper **risk management and capital allocation**.

---

# Trading Strategy

Predictions are translated into trades:

```
Long  if prediction = Up
Short if prediction = Down
```

Trading rules:

- One trade per day
- Strict chronological train/test split
- Fully out-of-sample evaluation

---

# Risk Management

The strategy uses **volatility-targeted position sizing**:

```
Position Size = Target Risk / σ(t)
```

Where:

- Target Risk = 2% of equity
- σ(t) = rolling realized volatility

Additional controls include:

- Transaction costs
- Slippage
- Leverage cap
- Turnover penalties

These mechanisms help ensure **realistic backtesting results**.

---

# Results

Initial Capital:

```
$10,000
```

Final Equity:

```
~$11,243
```

Total Return:

```
≈ 12%
```

Performance metrics:

| Metric | Value |
|------|------|
| Sharpe Ratio | ~0.73 |
| Max Drawdown | ~-16% |
| Win Rate | ~51.3% |

These results demonstrate how **weak predictive signals can become profitable when combined with disciplined risk management**.

---

# Project Structure

```
MangoQuant/
│
├── data/
│   ├── mango_prices.csv
│   └── weather_data.csv
│
├── features/
│   └── feature_engineering.py
│
├── models/
│   └── elasticnet_model.py
│
├── strategy/
│   └── trading_strategy.py
│
├── backtest/
│   └── backtest_engine.py
│
├── notebooks/
│   └── research_analysis.ipynb
│
└── main.py
```

---

# Challenges

Several practical issues emerged during development:

- Multicollinearity across engineered features
- Overfitting risk with limited observations
- Strict prevention of look-ahead bias
- Realistic modeling of transaction costs
- Balancing predictive performance with risk management

Reducing model complexity and incorporating execution friction helped avoid overly optimistic backtests.

---

# Key Lessons

Some key insights from the project:

- Commodity price magnitude is highly noisy.
- Directional signals can exist even with near-random accuracy.
- Risk management often matters more than prediction accuracy.
- Feature engineering must be paired with regularization.
- Realistic backtesting requires transaction cost modeling.

---

# Future Improvements

Potential extensions include:

- Incorporating mango futures pricing data
- Adding export/import macroeconomic indicators
- Expanding weather inputs to regional granularity
- Implementing regime detection models
- Testing nonlinear ensemble models

---

# Technologies Used

- Python
- NumPy
- Pandas
- Scikit-learn
- Matplotlib

---

## Author

Alexander Mueller

- GitHub: [alexmueller07](https://github.com/alexmueller07)
- LinkedIn: [Alexander Mueller](https://www.linkedin.com/in/alexander-mueller-021658307/)
- Email: amueller.code@gmail.com
