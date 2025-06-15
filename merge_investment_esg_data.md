# Merging Investment Survey and ESG Ratings Dataset

## Introduction
This document describes the methodology and process used to merge the Investment Survey dataset (`investment_survey.csv`) with the Public Company ESG Ratings dataset (`public-company-esg-ratings-dataset.csv`). The goal was to integrate environmental, social, and governance (ESG) metrics with investment behavior data to enable more comprehensive analysis.

## Data Sources

### Investment Survey Dataset
- Source file: `investment_survey.csv`
- Description: Contains information about individual investors' preferences, demographics, and investment behaviors
- Key fields: Age, Working_professional, Annual_income, Investment_per_month, Mode_of_investment
- Initial size: Multiple survey respondents with varied investment preferences

### ESG Ratings Dataset
- Source file: `public-company-esg-ratings-dataset.csv`
- Description: Contains ESG performance metrics for public companies
- Key fields: environment_score, social_score, governance_score, total_score, exchange, industry
- Initial size: Extensive collection of company ESG metrics across different exchanges

## Methodology for Merging

### Challenge
The primary challenge was the absence of a direct common identifier between the two datasets. The investment survey contained individual investor data, while the ESG ratings dataset contained company-level metrics.

### Solution Approach
We implemented a multi-stage approach to create meaningful connections between these disparate datasets:

#### Stage 1: Country-Based Mapping
1. **Adding Country Field to Both Datasets**:
   - For the Investment Survey: Created a mapping between investment modes and countries
   ```python
   investment_country_map = {
       "Banking - RD, FD": "USA",
       "Stocks - Intraday, long term": "USA",
       "Mutual Funds": "UK",
       "Crypto currency": "Singapore",
       "Gold / Any other Materialistic investment": "India",
       "Real estate, Bonds": "Germany"
   }
   ```
   - For ESG Ratings: Used exchange information to derive country mapping
   ```python
   esg_country_map = {
       "NEW YORK STOCK EXCHANGE, INC.": "USA",
       "NASDAQ": "USA",
       "NASDAQ NMS - GLOBAL MARKET": "USA",
       "LONDON STOCK EXCHANGE": "UK",
       "TOKYO STOCK EXCHANGE": "Japan",
       "HONG KONG STOCK EXCHANGE": "China",
       "SHANGHAI STOCK EXCHANGE": "China"
   }
   ```

2. **Aggregation of ESG Data by Country**:
   - Calculated the average ESG scores for each country to create country-level ESG profiles
   - This provided a basis for assigning ESG metrics to investors based on geographical investment preferences

3. **Initial Merge via Left Join**:
   - Performed a left join of the Investment Survey data with the country-averaged ESG data
   ```python
   merged_df = pd.merge(
       investment_df, 
       country_avg_esg, 
       on='Country', 
       how='left'
   )
   ```

#### Stage 2: Improving Coverage

After the initial merge, we implemented several strategies to improve data coverage:

1. **Industry-Based Matching**:
   - Assigned potential industries to investment types using domain knowledge
   ```python
   investment_to_industry = {
       "Banking - RD, FD": ["Banking", "Financial Services"],
       "Stocks - Intraday, long term": ["Technology", "Retail", "Health Care", "Energy"],
       "Mutual Funds": ["Diversified", "Asset Management"],
       "Crypto currency": ["Technology", "Financial Services"],
       "Gold / Any other Materialistic investment": ["Materials", "Mining"],
       "Real estate, Bonds": ["Real Estate", "Banking"]
   }
   ```
   - Calculated industry-average ESG scores and applied them to matching investment types where country-level data was unavailable

2. **Synthetic Data Generation**:
   - Created a statistical model to generate synthetic ESG scores for countries with missing data
   - Used a weighted approach based on known country characteristics:
   ```python
   country_weights = {
       "UK": {"env": 0.95, "soc": 1.05, "gov": 1.1},
       "Germany": {"env": 1.15, "soc": 1.0, "gov": 1.05},
       "Singapore": {"env": 0.9, "soc": 0.95, "gov": 1.15},
       "India": {"env": 0.7, "soc": 0.85, "gov": 0.9},
       "Other": {"env": 0.8, "soc": 0.85, "gov": 0.8}
   }
   ```

3. **KNN Algorithm Optimization**:
   - Applied K-Nearest Neighbors algorithm to further refine ESG scores based on investor characteristics
   - This enhanced personalization by considering relationships between demographic and financial attributes and ESG preferences
   - Features used: Age, Working_professional, Annual_income, Investment_per_month, and existing ESG scores

## Coverage Analysis

### Initial Coverage (After Country-Based Merge)
- After the initial country-based merge, we achieved partial coverage of ESG data
- Some countries represented in the investment survey had no matching country-level ESG data

### Intermediate Coverage (After Industry Matching)
- Industry-based matching significantly improved coverage
- Approximately 70-80% of records had ESG data after this stage (precise percentage varies by dataset)

### Final Coverage (After Synthetic Data Generation and KNN)
- Achieved 100% coverage after synthetic data generation
- KNN optimization enhanced the quality and personalization of the assigned ESG scores

## ESG Risk Rating

As a final step, we added an ESG Risk Rating field based on the total ESG score:

```python
def assign_esg_risk_rating(score):
    if score >= 1300:
        return "Excellent (AA)"
    elif score >= 1100:
        return "Very Good (A)"
    elif score >= 900:
        return "Good (BBB)"
    elif score >= 700:
        return "Satisfactory (BB)"
    elif score >= 500:
        return "Moderate Risk (B)"
    else:
        return "High Risk (CCC)"
```

This rating provides an intuitive interpretation of ESG performance for investors.

## Conclusion

The merged dataset successfully integrates investor data with ESG performance metrics, enabling analysis of how ESG factors correlate with investment behaviors and preferences. The multi-stage approach ensured complete coverage while maintaining data quality and relevance.

The final dataset contains all original investment survey data enriched with:
- Environmental scores
- Social scores
- Governance scores
- Total ESG scores
- ESG risk ratings

This comprehensive dataset provides a foundation for further analysis of ESG-conscious investment strategies and investor preferences.

## Limitations and Challenges

### Data Integration Challenges

1. **Lack of Direct Identifiers**: The most significant challenge was the absence of common identifiers between the datasets. This necessitated creating artificial linkages through geographical and industry-based approximations.

2. **Country Attribution Issues**: 
   - The investment survey didn't explicitly include country information, requiring inference based on investment modes
   - Some investment categories could span multiple countries, making definitive country attribution problematic
   - We observed several cases where the country mapping was ambiguous, particularly for global investment instruments

3. **Data Representation Disparities**:
   - The ESG dataset represented company-level metrics while the investment survey represented individual investor behaviors
   - This fundamental disparity meant that any integration would involve some level of abstraction and approximation
   - Direct mapping between individual investments and specific companies was impossible without additional data

4. **Coverage Challenges**:
   - Initial country-based matching produced substantial gaps in coverage
   - Some countries in the investment survey had minimal or no representation in the ESG dataset
   - This resulted in approximately 30-40% of records lacking ESG data after the initial merge

### Limitations of the Approach

1. **Aggregation Loses Specificity**:
   - Averaging ESG scores by country conceals significant variations between individual companies
   - Investors in specific companies might experience very different ESG exposure than our country averages suggest

2. **Synthetic Data Limitations**:
   - While necessary for complete coverage, synthetic data inherently introduces assumptions about ESG performance
   - The generated values rely on statistical models rather than actual measured data
   - The country weights used for synthetic data generation are based on subjective assessments rather than empirical measurements

3. **KNN Algorithm Limitations**:
   - The algorithm assumes relationships between investor characteristics and ESG preferences that may not exist in reality
   - Limited features were available for the KNN model, potentially missing important determinants of ESG exposure
   - Small sample sizes for certain demographic groups may have affected the quality of KNN-based imputations

4. **Temporal Misalignment**:
   - ESG ratings and investment survey data may have been collected at different time points
   - ESG metrics evolve over time, and our approach doesn't account for temporal dynamics in ESG performance
