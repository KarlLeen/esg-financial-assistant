# Simple Coding Guidelines

This document provides basic guidelines to help everyone write clean, readable code that the whole team can understand. Our team includes people from finance, computer science, and data science backgrounds - these guidelines help us all work together effectively.

## The Basics: Make Your Code Easy to Read

### 1. Use Clear Names

Choose names that explain what your variables and functions do:

**Good examples:**
```python
esg_score = 85
company_name = "Apple Inc"
stock_price = get_latest_price(ticker)
```

**Avoid:**
```python
x = 85
n = "Apple Inc"
p = get_price(t)
```

### 2. Add Comments to Explain Your Thinking

Help others understand your logic with simple comments:

```python
# Clean the ticker symbol by removing $ signs and making uppercase
ticker = raw_ticker.replace('$', '').upper()

# Skip companies with missing ESG data
if pd.isna(esg_score):
    continue
```

### 3. Keep Things Organized

- Put related code together
- Use empty lines to separate different sections
- Keep your imports at the top of the file

```python
import pandas as pd
import yfinance as yf

# Load the data
df = pd.read_csv("esg-data.csv")

# Clean the data
df = df.dropna()
```

## Working with Data

### Naming Your DataFrames and Columns

Use descriptive names that make sense to everyone:

```python
# Good
esg_data = pd.read_csv("esg-ratings.csv")
stock_prices = pd.read_csv("stock-data.csv")
merged_data = pd.merge(esg_data, stock_prices, on='ticker')

# Instead of
df1 = pd.read_csv("esg-ratings.csv")
df2 = pd.read_csv("stock-data.csv")
df3 = pd.merge(df1, df2, on='ticker')
```

### Explain Your Data Processing Steps

```python
# Remove companies without industry classification
esg_data = esg_data.dropna(subset=['industry'])

# Calculate the average ESG score by industry
industry_averages = esg_data.groupby('industry')['total_esg_score'].mean()
```

## Simple Function Guidelines

### Write Functions That Do One Thing Well

```python
def clean_ticker_symbol(ticker):
    """Remove special characters and make ticker uppercase"""
    return ticker.replace('$', '').strip().upper()

def calculate_portfolio_esg_score(portfolio_data):
    """Calculate weighted average ESG score for a portfolio"""
    weighted_scores = portfolio_data['weight'] * portfolio_data['esg_score']
    return weighted_scores.sum()
```

### Add a Simple Description

Just explain what your function does in plain English:

```python
def get_stock_price(ticker):
    """Get the latest stock price for a given ticker symbol"""
    # Your code here
    pass
```

## File Organization

Keep things simple and organized:

```
notebooks/
    data_cleaning.ipynb       # Clean and prepare data
    analysis.ipynb           # Explore and analyze data
    
src/
    data_processing.py       # Functions for cleaning data
    esg_analysis.py         # Functions for ESG calculations
    stock_data.py           # Functions for getting stock prices
```

## Git Commits: Tell Us What You Did

Write commit messages that explain your changes:

**Good:**
- "Add function to calculate portfolio ESG scores"
- "Fix missing industry data for acquisition companies"
- "Update data cleaning to handle new CSV format"

**Less helpful:**
- "Update code"
- "Fix bug"
- "Changes"

## When You Get Stuck

- Ask questions! Everyone comes from different backgrounds
- Add TODO comments for things you need to figure out later
- Share your notebook outputs so others can see what you're working on

```python
# TODO: Need to handle companies with missing ESG data
# Current approach drops them, but maybe we should estimate scores?
```

## Remember

The goal is to write code that your teammates can understand and build upon. Don't worry about being perfect - focus on being clear and helpful to others!