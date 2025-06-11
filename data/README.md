# Overview of the Data Directory

This directory contains datasets used in the Youth ESG Financial Assistant project. The data is essential for developing the machine learning model that will assist younger investors in making informed investment decisions based on both financial performance and ESG (Environmental, Social, and Governance) criteria.

## Contents

- **Public Company ESG Ratings Dataset** (`public-company-esg-ratings-dataset.csv`): This dataset includes ESG ratings for various public companies, which will be used to evaluate their performance based on ESG criteria. Each company has scores for environmental, social, and governance factors, as well as an overall ESG score.

- **Investment Survey Dataset** (`investment_survey.csv`): Contains survey responses about investment preferences, risk tolerance, and ESG awareness across different demographic groups. This dataset helps tailor recommendations to specific age groups and their preferences.

- **Additional Datasets**: Several additional datasets will be downloaded and integrated during the project:
  - **S&P 500 Historical Prices**: Financial performance data for major companies
  - **World Bank ESG Indicators**: Global ESG metrics for contextual analysis
  - **Student Spending Dataset**: Insights into younger demographics' spending patterns

## Dataset Structure

### Public Company ESG Ratings Dataset

Key columns in this dataset include:
- `ticker`: Stock ticker symbol
- `name`: Company name
- `industry`: Industry classification
- `environment_score`: Score for environmental performance
- `social_score`: Score for social responsibility
- `governance_score`: Score for governance practices
- `total`: Overall ESG score

### Investment Survey Dataset

Key columns in this dataset include:
- `age_group`: Demographic age category
- `investment_preference`: Preferred investment types
- `risk_tolerance`: Risk tolerance level (1-5)
- `esg_awareness`: Awareness of ESG factors
- `esg_importance`: Importance of ESG in investment decisions

## Data Flow

1. **Data Collection**: All required datasets are either stored locally or accessed via APIs
2. **Data Cleaning**: Preprocessing steps to handle missing values and standardize formats
3. **Feature Engineering**: Creation of derived metrics and normalized scores
4. **Integration**: Combining datasets to create a unified data model
5. **Analysis**: Exploratory data analysis to understand patterns and relationships
6. **Model Development**: Using the processed data to train recommendation algorithms

## Usage

To utilize the datasets in this directory, follow these steps:

1. **Load the Data**: Use the provided Jupyter notebooks or Python scripts to load the datasets into your environment.
2. **Data Cleaning**: Ensure that the data is cleaned and preprocessed as outlined in the `data_processing.md` document.
3. **Integration**: Combine the ESG ratings with financial data to prepare for analysis and model training.

## Documentation

For more detailed information on the datasets and their usage, refer to:

- `docs/data/data_sources.md`: Details about data sources and acquisition
- `docs/data/data_processing.md`: Data cleaning and preprocessing steps
- `docs/data/data_exploration.md`: Exploratory data analysis findings
- `docs/data/dataset_integration_plan.md`: Plan for integrating multiple datasets

## Data Updates

The ESG ratings and financial data will be periodically updated to ensure the model has access to the latest information. The update process is documented in the project's development guide.