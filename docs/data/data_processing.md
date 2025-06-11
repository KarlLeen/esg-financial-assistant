# Data Processing Guide

## Overview

This document outlines the data processing pipeline for the ESG Financial Assistant project based on the implemented data-cleaning.ipynb notebook.

## Data Sources

- **ESG Ratings Dataset**: `public-company-esg-ratings-dataset.csv`
- **Investment Survey**: `investment_survey.csv`

## Processing Steps

### 1. Data Loading

Load the ESG dataset and required libraries:

```python
import os
import pandas as pd
import yfinance as yf

# Load ESG dataset
df = pd.read_csv("public-company-esg-ratings-dataset.csv")
df.head()
```

### 2. Data Cleaning

Remove unnecessary columns to streamline the dataset:

```python
columns_to_drop = [
    "logo", "weburl", "environment_grade", "environment_level", 
    "social_grade", "social_level", "governance_grade", "governance_level", 
    "total_grade", "total_level", "cik", "last_processing_date"
]
df.drop(columns=columns_to_drop, inplace=True)
```

### 3. Handle Missing Industry Data

Map missing industry values for acquisition companies:

```python
industry_map = {
    'Armada Acquisition Corp I': 'Financial Services',
    'Acri Capital Acquisition Corp': 'Financial Services',
    'ACE Convergence Acquisition Corp': 'Technology',
    'Edoc Acquisition Corp': 'Healthcare',
    # Add more mappings as needed
}

df['industry'] = df.apply(
    lambda row: industry_map[row['name']] if pd.isna(row['industry']) and row['name'] in industry_map else row['industry'],
    axis=1
)
```

### 4. Stock Price Integration

Fetch latest stock prices and merge with ESG data:

```python
# Clean ticker symbols
df["Ticker"] = df["ticker"].str.replace('$', '', regex=False).str.upper()
tickers = df["Ticker"].unique()

# Fetch latest prices with error handling
latest_prices = {}
for ticker in tickers:
    try:
        stock = yf.Ticker(ticker)
        hist = stock.history(period="1d")
        if not hist.empty:
            latest_prices[ticker] = hist["Close"].iloc[-1]
        else:
            latest_prices[ticker] = None
    except Exception as e:
        latest_prices[ticker] = None

# Merge data
latest_price_df = pd.DataFrame(list(latest_prices.items()), columns=["Ticker", "Latest_Price"])
stock_merged = pd.merge(df, latest_price_df, on="Ticker", how="inner")
```

### 5. Data Validation

- Check for null values: `df.isna().any()`
- Validate data types and consistency
- Ensure successful integration

## Output Dataset

Clean dataset ready for analysis with:

- Company information (ticker, name, exchange, industry)
- ESG scores (environment, social, governance, total)
- Latest stock prices

## Next Steps

- [Define additional processing steps as needed]
- [Document any custom validation rules]
- [Add error handling improvements]