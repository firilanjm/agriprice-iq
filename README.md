# AgriPrice-IQ: Canadian Retail Price Forecasting & Volatility Analytics

> 🔬 **Research Inspiration:** The idea behind AgriPrice-IQ was inspired by research presented at the **Royal Statistical Society (RSS) International Conference 2026**, Bournemouth, UK.

**AgriPrice-IQ** is an independent end-to-end data science project focused on forecasting Canadian retail food prices while **quantifying and communicating the uncertainty surrounding future price predictions** across 10 Canadian provinces.

The project combines **data engineering, exploratory data analysis, feature engineering, machine learning, probabilistic forecasting, uncertainty quantification, price volatility analysis, and interactive business intelligence** into a complete data science workflow.

The project was developed independently as a personal portfolio project to explore how statistical and machine learning methods can transform retail price data into interpretable forecasts and interactive analytical tools.

---

## 🔎 Project at a Glance

| | |
|---|---|
| 🔬 **Research Inspiration** | RSS International Conference 2026 |
| 🇨🇦 **Geographic Coverage** | 10 Canadian provinces |
| 📅 **Data Frequency** | Monthly retail prices |
| 🔮 **Forecast Horizon** | August 2026 – July 2027 |
| 🤖 **Model** | LightGBM Quantile Regression |
| 📊 **Forecasts** | P10 / P50 / P90 |
| 📈 **Focus** | Price Forecasting & Uncertainty |
| 📉 **Additional Analysis** | Price Volatility |
| 🗄️ **Data Storage** | SQLite |
| 📊 **Dashboard** | Tableau |
| 💻 **Primary Language** | Python |

---

## 📚 Data Source

The historical retail price data are sourced from **Statistics Canada**, Table 18-10-0245-01:

**Food prices, monthly, 2021–2026**

[Statistics Canada — Table 18-10-0245-01](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1810024501)

The dataset contains monthly retail prices for food products across Canadian provinces.

The raw Statistics Canada table required substantial preprocessing before it could be used for analysis and forecasting. The data preparation workflow included:

- Parsing and restructuring the original table format
- Cleaning metadata and headers
- Standardizing province and product names
- Reshaping the data into an analytical panel structure
- Handling missing observations
- Aligning product, category, province, and date information
- Merging and integrating historical price data
- Creating modeling-ready temporal features
- Preparing Tableau-ready datasets
- Integrating historical observations with future forecast outputs

The historical data used in this project cover **July 2021 through July 2026**, while the forecasting pipeline generates predictions for **August 2026 through July 2027**.

This data preparation stage was an important component of the project because the original public dataset was not directly structured for the downstream forecasting and visualization workflow.

---

# 🎯 Project Objectives

The central goal of AgriPrice-IQ is not only to forecast future retail food prices, but also to **measure and communicate the uncertainty associated with those forecasts**.

The project explores questions such as:

- How have Canadian retail food prices changed over time?
- How do price trends differ across provinces?
- Which products exhibit greater historical price volatility?
- What might retail prices look like over the next 12 months?
- How uncertain are those future price forecasts?
- How does forecast uncertainty vary across products and over time?
- How can uncertainty be communicated clearly through an interactive dashboard?

Rather than producing only a single predicted price, AgriPrice-IQ uses **LightGBM Quantile Regression** to estimate multiple points of the predictive distribution and construct prediction intervals around the median forecast.

---

# 📈 Probabilistic Forecasting & Uncertainty Quantification

A central component of AgriPrice-IQ is **forecasting under uncertainty**.

The goal is not simply to answer:

> **"What will the price be?"**

but also:

> **"How uncertain is that prediction?"**

The forecasting pipeline uses **LightGBM Quantile Regression** to estimate three conditional quantiles:

$$
Q_{0.10}(Y|X), \quad Q_{0.50}(Y|X), \quad Q_{0.90}(Y|X)
$$

These correspond to:

| Quantile | Interpretation |
|---|---|
| **P10** | Lower end of the predicted price distribution |
| **P50** | Median forecast |
| **P90** | Upper end of the predicted price distribution |

The **P10–P90 interval** is used to represent forecast uncertainty.

A relatively narrow prediction interval indicates that the model's predicted range is more concentrated, while a wider interval indicates greater uncertainty around the future price.

This allows AgriPrice-IQ to move beyond point forecasting toward **probabilistic forecasting**, where both the predicted future price and the uncertainty surrounding that prediction are communicated.

---

# 🔑 Key Features

## 📊 Probabilistic Price Forecasting

Uses **LightGBM Quantile Regression** to generate:

- **P10** — lower forecast
- **P50** — median forecast
- **P90** — upper forecast

The resulting P10–P90 range provides an interpretable representation of forecast uncertainty.

---

##  12-Month Forecast Horizon

The forecasting pipeline generates recursive monthly forecasts over a 12-month horizon:

**August 2026 → July 2027**

Forecasts are generated at the province-product level, allowing users to examine future price trajectories for individual retail food products.

---

## 🇨🇦 Provincial Analysis

The project analyzes retail food prices across **10 Canadian provinces**.

Users can explore provincial differences through the interactive Tableau dashboard.

Province selection can be performed in clicking directly on a province in the map.

---

## 📉 Price Volatility Analysis

Historical price volatility is measured using the **coefficient of variation (CV)**:

$$
CV = \frac{\text{Standard Deviation}}{\text{Mean}}
$$

This provides a relative measure of price variability, allowing products with different price levels to be compared.

The dashboard uses this measure to display:

- Category-level volatility
- Top 10 most volatile products
- Selected-product volatility

---

# 🧩 End-to-End Data Science Workflow

AgriPrice-IQ was designed as an end-to-end workflow rather than a standalone machine learning model.

```text
Raw Statistics Canada Data
            │
            ▼
      Data Wrangling
            │
            ▼
     Data Cleaning &
      Restructuring
            │
            ▼
    Province / Product /
    Category Standardization
            │
            ▼
     Structured Storage
        SQLite DB
            │
            ▼
 Exploratory Data Analysis
            │
            ▼
   Feature Engineering
            │
            ▼
LightGBM Quantile Regression
            │
            ▼
 P10 / P50 / P90 Forecasts
            │
            ▼
       CSV Export
            │
            ▼
   Tableau Dashboard