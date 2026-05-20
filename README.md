# The Impact of Geopolitics on Russian Oil & Metallurgical Stocks

Research project for the HSE Bachelor’s Programme **Data Science and Business Analytics**.

Author: **Ruslan Saadetdinov**  
Supervisor: **Daria Bashminova**  
University: **National Research University Higher School of Economics**  
Year: **2026**

---

## Project Overview

This project studies how geopolitical risk affects the stock prices and volatility of major Russian oil & gas and metallurgical companies.

The main contribution of the project is the construction of a custom Russian news-based geopolitical risk index:

**NASH — Russia-Adjusted Geopolitical Risk Index**

Unlike the global GPR index by Caldara & Iacoviello, NASH is based on Russian-language news sources and is designed to capture the local information environment in which Russian investors form expectations.

---

## Research Question

Does a locally constructed geopolitical risk index explain Russian stock returns and volatility better than the global Geopolitical Risk Index?

---

## Hypotheses

1. An increase in NASH leads to lower stock returns of Russian companies.
2. NASH explains stock returns and volatility better than the global GPR index.
3. NASH has predictive power for future stock volatility.

---

## Data

The project combines three main data blocks:

### Stock Market Data

Daily stock price data for major Russian oil, gas, and metallurgical companies.

Main variables:

- `datetime` — trading date
- `open` — opening price
- `high` — highest daily price
- `low` — lowest daily price
- `close` — closing price
- `volume` — trading volume

### Global Risk and Financial Indicators

The project uses global financial and macroeconomic controls, including:

- `GPRD` — global geopolitical risk index
- `VIX` — market volatility index
- `S&P 500`
- `DJIA`
- `HSI`
- `EPU`
- U.S. interest rate indicators

### Russian News Corpus

Russian-language news articles were collected from:

- **RBC**
- **Lenta.ru**

The news corpus covers the period from **2010 to 2020** and is used to construct the NASH index.

---

## NASH Index Construction

The NASH index is built using a dictionary-based NLP approach inspired by Caldara & Iacoviello (2022), adapted to the Russian language.

The index is based on the daily share of news articles containing geopolitical-risk-related terms.

The dictionary includes:

- war-related terms
- sanctions-related terms
- conflict-related terms
- terrorism-related terms
- nuclear-risk terms
- Russia-specific geopolitical terms such as:
  - `санкции`
  - `эмбарго`
  - `Крым`
  - `Донбасс`
  - `НАТО`
  - `ДНР`
  - `ЛНР`

To reduce false positives, the dictionary is divided into:

- **Strong geopolitical terms**
- **Weak context-dependent terms**

A relief lexicon is also used to detect de-escalation events such as peace talks, sanction removal, or ceasefires.

Final index variants:

- `NASH_tension`
- `NASH_relief`
- `NASH_net = NASH_tension - NASH_relief`
- `NASH_index100`

---

## Methodology

The empirical analysis uses several complementary methods:

- AR(1) baseline model
- OLS regression
- Ridge regression
- Lasso regression
- Welch’s t-test
- Granger causality test
- Augmented Dickey-Fuller stationarity test

The models are evaluated using a chronological train-test split:

- 80% training sample
- 20% test sample

Main metrics:

- MAE
- RMSE
- out-of-sample R²
- directional accuracy for returns

---

## Key Results

### Returns

The NASH-based model slightly improves return prediction compared to the AR(1) baseline and GPR-only model.

However, the economic effect is modest, which is consistent with market efficiency: publicly available news is quickly incorporated into prices.

### Volatility

The strongest result is found for volatility.

The full model with NASH substantially outperforms both:

- the AR(1) baseline
- the global GPR-only model

Volatility results:

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| AR(1) baseline | 0.000182 | 0.000353 | 0.149 |
| GPRD-only model | 0.000165 | 0.000321 | 0.218 |
| Full model with NASH | 0.000142 | 0.000287 | 0.314 |

The NASH model increases out-of-sample R² by:

- **+16.5 percentage points** compared to AR(1)
- **+9.6 percentage points** compared to GPRD-only model

---

## Hypothesis Testing

### Welch’s t-test

High-NASH days are associated with:

- lower average returns
- significantly higher volatility
- higher absolute returns
- higher trading volume

### Granger Causality

Main findings:

- NASH does not strongly predict the direction of returns.
- NASH strongly predicts future volatility with a one-day lag.
- NASH has stronger predictive power for volatility than the global GPR index.

---

## Conclusions

The results show that geopolitical news primarily affects **market volatility**, rather than the average level of returns.

The locally constructed NASH index provides additional explanatory and predictive power compared to the global GPR index, especially for volatility forecasting.

This supports the idea that country-specific news environments matter for financial markets and that local geopolitical risk indicators can be more informative than global benchmarks.

---

## Limitations

The main limitations of the project are:

- only two Russian news sources are used
- automatic text classification may contain false positives and false negatives
- the sample excludes events after 2020
- the analysis focuses only on large surviving Russian companies
- daily macroeconomic Russian controls are not fully included

---

## References

- Caldara, D., & Iacoviello, M. (2022). *Measuring Geopolitical Risk*.
- Aprigliano et al. (2022). *The power of text-based indicators in forecasting Italian economic activity*.
- Chen, R., Yang, L., & Zhang, X. (2026). *Geopolitical risk and the cross-section of stock returns: International evidence*.
- Li, Z., Zhao, P., Ma, C., & Wang, Q. (2026). *The test of financial resilience in emerging market economies*.
- Pan, L. et al. (2024). *Natural resources: A determining factor of geopolitical risk in Russia?*
- Pichiyan, V. et al. (2024). *Web Scraping using Natural Language Processing*.
