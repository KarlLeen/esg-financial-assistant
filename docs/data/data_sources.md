# Data Sources

## Overview

This document outlines the primary data sources for the ESG Financial Assistant project, focusing on the datasets currently implemented and validated in the data-cleaning.ipynb notebook.

## Primary Datasets

### 1. Public Company ESG Ratings Dataset

- **File**: `public-company-esg-ratings-dataset.csv`
- **Location**: `data/public-company-esg-ratings-dataset.csv`
- **Description**: Core dataset containing ESG ratings and scores for public companies
- **Key Fields**:
  - `ticker`: Company stock ticker symbol
  - `name`: Company name
  - `exchange`: Stock exchange listing
  - `industry`: Company industry classification
  - `environment_score`: Environmental performance score
  - `social_score`: Social responsibility score
  - `governance_score`: Corporate governance score
  - `total`: Overall ESG score
- **Data Quality**: Processed in data-cleaning.ipynb with missing industry mappings
- **Update Frequency**: [To be determined]

### 2. Investment Survey Dataset

- **File**: `investment_survey.csv`
- **Location**: `data/investment_survey.csv`
- **Description**: Survey data on investment preferences and demographics
- **Key Fields**: [To be documented after analysis]
- **Integration Status**: [Framework ready for implementation]
- **Update Frequency**: [To be determined]

## External Data Sources

### Yahoo Finance API

- **Access Method**: `yfinance` Python library
- **Purpose**: Real-time stock price data
- **Implementation**: Integrated in data-cleaning.ipynb
- **Usage**: Fetches latest stock prices for companies in ESG dataset
- **Rate Limits**: [Document API limitations]
- **Error Handling**: Implemented with try-catch blocks

## Data Integration Architecture

### Current Implementation

```python
# Data loading pattern from data-cleaning.ipynb
import pandas as pd
import yfinance as yf

# Load ESG data
df = pd.read_csv("public-company-esg-ratings-dataset.csv")

# Fetch stock prices
latest_prices = {}
for ticker in df["Ticker"].unique():
    stock = yf.Ticker(ticker)
    # Price fetching logic with error handling
```

### Data Flow

1. **ESG Data Loading** → Data cleaning → Missing value handling
2. **Stock Price Fetching** → API calls → Error handling → Data merge
3. **Survey Data** → [Integration framework ready]

## Data Quality Considerations

### Known Issues

- Missing industry classifications for acquisition companies
- Stock price API failures for some tickers
- Data freshness varies by source

### Data Validation

- ESG score range validation
- Ticker symbol standardization
- Missing value identification and handling

## Future Data Sources

### Planned Integrations

- [Document additional data sources as they are identified]
- [Economic indicators]
- [Market sentiment data]

### Evaluation Criteria

- Data quality and completeness
- Update frequency
- API reliability
- Cost considerations

## Data Refresh Strategy

### Current Process

Based on data-cleaning.ipynb implementation:

1. Manual data loading from CSV files
2. Real-time stock price fetching via yfinance
3. Data validation and cleaning

### Future Improvements

- [Automated data refresh schedules]
- [Data quality monitoring]
- [Error notification systems]