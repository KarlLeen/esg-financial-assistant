# Dataset Integration Plan

## Overview

This document outlines the strategy for integrating multiple datasets in the ESG Financial Assistant project, based on the current implementation in `data-cleaning.ipynb`.

## Integration Architecture

### Current Data Flow

```
ESG Ratings Dataset → Data Cleaning → Stock Price Integration → Merged Dataset
     ↓                     ↓                    ↓                    ↓
CSV Loading         Column Removal      yfinance API         Final Analysis
Missing Values      Industry Mapping    Error Handling       Ready Dataset
```

## Primary Integration Points

### 1. ESG + Stock Price Integration

**Status**: ✅ Implemented in data-cleaning.ipynb

**Integration Method**:
- Join on standardized ticker symbols
- Handle missing price data gracefully
- Maintain data integrity during merge

**Implementation**:
```python
# Clean ticker symbols
df["Ticker"] = df["ticker"].str.replace('$', '', regex=False).str.upper()

# Fetch prices with error handling
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

# Merge datasets
stock_merged = pd.merge(df, latest_price_df, on="Ticker", how="inner")
```

### 2. Survey + ESG Integration

**Status**: 🔄 Framework Ready

**Planned Integration Strategy**:
- Map survey demographics to company preferences
- Weight ESG scores based on user priorities
- Personalize recommendations

**Integration Schema** (To Be Implemented):
```python
# Framework for survey integration
def integrate_survey_preferences(esg_data, survey_data, user_profile):
    """
    Integrate user survey preferences with ESG company data
    
    Args:
        esg_data: Cleaned ESG dataset with stock prices
        survey_data: Investment survey responses
        user_profile: Individual user preferences
    
    Returns:
        Personalized company recommendations
    """
    # Implementation framework
    pass
```

## Data Validation Rules

### Ticker Symbol Standardization

- Remove special characters ($, spaces)
- Convert to uppercase
- Validate against known exchanges
- Handle duplicate/variant tickers

### ESG Score Validation

- Ensure scores are within expected ranges (0-100)
- Validate component scores sum to total
- Flag outliers for review
- Check for data consistency

### Price Data Validation

- Verify price data freshness
- Handle API timeouts and failures
- Validate price ranges against market norms
- Track data source reliability

## Error Handling Strategy

### Current Implementation

From data-cleaning.ipynb:

```python
# Robust error handling for stock price fetching
for ticker in tickers:
    try:
        stock = yf.Ticker(ticker)
        hist = stock.history(period="1d")
        if not hist.empty:
            latest_prices[ticker] = hist["Close"].iloc[-1]
        else:
            print(f"{ticker} has no data.")
            latest_prices[ticker] = None
    except Exception as e:
        print(f"{ticker} failed: {e}")
        latest_prices[ticker] = None
```

### Future Enhancements

- Retry logic for failed API calls
- Fallback data sources
- Data quality scoring
- Automated error reporting

## Integration Testing Framework

### Data Integrity Tests

- [ ] Verify join completeness
- [ ] Check for data loss during merges
- [ ] Validate foreign key relationships
- [ ] Test edge cases (missing data, API failures)

### Performance Tests

- [ ] Measure data loading times
- [ ] Monitor API response times
- [ ] Test with large datasets
- [ ] Optimize merge operations

### Quality Assurance

- [ ] Cross-validate merged data
- [ ] Spot-check random samples
- [ ] Compare with source data
- [ ] Validate business logic

## Future Integration Plans

### Phase 1: Current Implementation
- ✅ ESG data cleaning
- ✅ Stock price integration
- ✅ Basic error handling

### Phase 2: Survey Integration
- [ ] Survey data analysis
- [ ] User preference modeling
- [ ] Personalization engine
- [ ] Recommendation algorithm

### Phase 3: Advanced Features
- [ ] Real-time data updates
- [ ] Historical trend analysis
- [ ] Market sentiment integration
- [ ] Portfolio optimization

## Data Schema Evolution

### Current Schema

```
merged_dataset {
    ticker: string
    name: string
    exchange: string
    industry: string
    environment_score: float
    social_score: float
    governance_score: float
    total: float
    Latest_Price: float
}
```

### Planned Extensions

```
enhanced_dataset {
    // Current fields...
    user_preference_weight: float
    personalized_score: float
    recommendation_rank: int
    last_updated: datetime
    data_quality_score: float
}
```

## Integration Monitoring

### Key Metrics to Track

- Data freshness timestamps
- API success rates
- Integration completion rates
- Data quality scores
- Processing performance

### Alerting Strategy

- Failed integration notifications
- Data quality degradation alerts
- API rate limit warnings
- Processing time anomalies

## Next Steps

1. **Complete Survey Integration**: Implement user preference weighting
2. **Enhance Error Handling**: Add retry logic and fallback mechanisms
3. **Performance Optimization**: Improve data processing efficiency
4. **Quality Monitoring**: Implement automated data quality checks
5. **Documentation**: Maintain integration procedures and troubleshooting guides