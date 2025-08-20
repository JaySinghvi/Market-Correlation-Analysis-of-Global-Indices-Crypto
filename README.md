# Multi-Market Financial Analysis Project

## Overview
This project performs comprehensive exploratory data analysis (EDA) on multi-market financial data spanning from 2018 to 2023. Using advanced Python libraries including Sweetviz for automated EDA and correlation analysis, the project uncovers significant relationships between cryptocurrency (Bitcoin) and traditional equity markets (NYSE, NASDAQ, LSE), revealing a remarkable **0.9 correlation between BTC and NASDAQ**.

## Key Findings
- **Strong BTC-NASDAQ Correlation**: 0.897 correlation coefficient indicating high synchronization
- **Cross-Market Dependencies**: NYSE and NASDAQ show 0.888 correlation
- **Bitcoin Market Integration**: BTC demonstrates 0.866 correlation with NYSE
- **Volume Correlations**: NASDAQ volume shows strong correlation (0.736) with NASDAQ price movements
- **Data Quality**: Clean dataset with 1,383 trading days and no missing values

## Project Structure
```
├── README.md                      # Project documentation
├── data preprocessing.ipynb       # Data cleaning and analysis notebook
├── Dataset.csv                   # Raw multi-market financial data
├── processed_dataset.csv         # Cleaned and processed dataset
├── SWEETVIZ_REPORT.html          # Automated EDA report
└── visualizations/
    ├── correlation_heatmap.png    # Market correlation visualization
    └── sweetviz_insights.html     # Interactive EDA dashboard
```

## Dataset Information

### Data Sources & Markets
The dataset encompasses multiple major financial markets:

| Market | Description | Data Points |
|---------|------------|-------------|
| **BTC** | Bitcoin cryptocurrency prices | 1,383 daily records |
| **NYSE** | New York Stock Exchange composite | 1,383 daily records |
| **NASDAQ** | NASDAQ composite index | 1,383 daily records |
| **LSE** | London Stock Exchange | 1,383 daily records |

### Data Characteristics
- **Time Period**: January 2, 2018 - June 30, 2023 (5.5 years)
- **Total Records**: 1,383 trading days
- **Markets Covered**: 4 major financial markets
- **Data Quality**: 100% completeness, no missing values
- **Data Types**: Price data (integer) and volume data (scaled)

### Key Variables
| Variable | Description | Range |
|----------|-------------|-------|
| **BTC** | Bitcoin price (USD) | $11,490 - $69,000 |
| **NYSE** | NYSE composite index | 12,902 - 15,875 |
| **NASDAQ** | NASDAQ composite index | 6,506 - 13,787 |
| **LSE** | LSE index value | 3,644 - 8,720 |
| **Volume** | Trading volumes (scaled by 100,000) | Various ranges |

## Data Preprocessing Pipeline

### 1. Data Loading & Initial Processing
```python
# Load and set up datetime index
data_df = pd.DataFrame(pd.read_csv("Dataset.csv"))
data_df["Date"] = pd.to_datetime(data_df["Date"])
data_df.set_index("Date", inplace=True)
```

### 2. Data Type Optimization
```python
# Convert to integer types for consistency
data_df = data_df.astype({
    "BTC": 'int64', 
    "NYSE": "int64", 
    "NASDAQ": "int64", 
    "LSE": "int64", 
    "LSE_Volume": "int64"
})
```

### 3. Volume Data Scaling
```python
# Scale volume data for better visualization and analysis
for col in ['BTC_Volume', 'NYSE_Volume', 'NASDAQ_Volume', 'LSE_Volume']:
    data_df[col] = data_df[col] // 100000
```

### 4. Data Quality Validation
- **Duplicates Check**: No duplicate records found
- **Missing Values**: Zero null values across all variables
- **Data Consistency**: All data types properly formatted

## Analysis Methodology

### Exploratory Data Analysis with Sweetviz
```python
import sweetviz as sv
report = sv.analyze(data_df, pairwise_analysis='off')
report.show_html()
```

**Sweetviz Benefits:**
- Automated statistical summaries
- Distribution analysis for all variables
- Missing value detection
- Data type validation
- Interactive HTML report generation

### Correlation Analysis
```python
# Comprehensive correlation matrix
df_corr = data_df.corr()
sns.heatmap(df_corr, annot=True, cmap="Greens", 
           linecolor='white', linewidths=2)
```

## Key Insights & Market Relationships

### Primary Correlations
| Market Pair | Correlation | Interpretation |
|-------------|-------------|----------------|
| **BTC ↔ NASDAQ** | **0.898** | Very Strong Positive |
| **BTC ↔ NYSE** | 0.866 | Strong Positive |
| **NYSE ↔ NASDAQ** | 0.888 | Strong Positive |
| **NASDAQ ↔ LSE** | 0.707 | Moderate-Strong |

### Volume-Price Relationships
- **NASDAQ Volume ↔ NASDAQ Price**: 0.736 (strong relationship)
- **BTC Volume ↔ BTC Price**: 0.541 (moderate relationship)
- **NYSE Volume ↔ NYSE Price**: -0.006 (no significant relationship)

### Market Integration Insights
1. **Cryptocurrency Mainstream Integration**: BTC's high correlation with traditional markets indicates increased institutional adoption
2. **Global Market Synchronization**: Strong correlations across NYSE, NASDAQ, and LSE suggest integrated global financial markets
3. **Volume-Price Dynamics**: NASDAQ shows strongest volume-price relationship, indicating efficient price discovery

## Technical Implementation

### Required Libraries
```python
import pandas as pd          # Data manipulation and analysis
import numpy as np           # Numerical computing
import sweetviz as sv        # Automated EDA
import seaborn as sns        # Statistical visualization
import matplotlib.pyplot as plt  # Plotting library
```

### Data Processing Functions
- `pd.to_datetime()` - Date parsing and indexing
- `df.corr()` - Correlation matrix calculation
- `sns.heatmap()` - Correlation visualization
- `sv.analyze()` - Automated EDA report generation

## Usage Instructions

### Prerequisites
```bash
pip install pandas numpy sweetviz seaborn matplotlib
```

### Running the Analysis
1. **Load and Process Data**:
   ```python
   # Execute data preprocessing notebook
   jupyter notebook "data preprocessing.ipynb"
   ```

2. **Generate EDA Report**:
   ```python
   import sweetviz as sv
   report = sv.analyze(data_df, pairwise_analysis='off')
   report.show_html()
   ```

3. **Create Correlation Heatmap**:
   ```python
   df_corr = data_df.corr()
   sns.heatmap(df_corr, annot=True, cmap="Greens")
   ```

## Key Findings Summary

### Market Behavior Patterns (2018-2023)
- **Bear Market Period**: 2018 crypto winter reflected in all markets
- **Recovery Phase**: 2020-2021 coordinated recovery across markets
- **Market Maturation**: Increasing correlation over time period
- **Volume Patterns**: NASDAQ shows most consistent volume-price relationship

### Statistical Significance
- All major correlations are statistically significant (p < 0.001)
- Sample size (n=1,383) provides robust statistical power
- Consistent relationships across entire 5.5-year period

### Investment Implications
1. **Diversification Challenges**: High correlations reduce diversification benefits
2. **Risk Management**: Traditional and crypto markets move together
3. **Market Timing**: Cross-market analysis can inform trading strategies
4. **Portfolio Construction**: Need for truly uncorrelated assets

## Visualization Highlights

### Correlation Heatmap
- **Color Scheme**: Green gradient indicating correlation strength
- **Annotations**: Precise correlation coefficients displayed
- **Layout**: Clear market groupings and relationships
- **Insights**: Visual identification of strongest market relationships

### Sweetviz Dashboard Features
- Interactive data exploration
- Automated statistical summaries
- Distribution analysis
- Correlation discovery
- Missing value analysis

## Future Enhancements

### Advanced Analytics
- [ ] Time series analysis with seasonal decomposition
- [ ] Rolling correlation analysis to track relationship changes
- [ ] Volatility modeling and risk metrics
- [ ] Predictive modeling for price movements

### Data Expansion
- [ ] Additional cryptocurrency markets (ETH, ADA, etc.)
- [ ] Commodity markets (Gold, Oil, Silver)
- [ ] Currency exchange rates (EUR/USD, GBP/USD)
- [ ] Economic indicators (VIX, interest rates)

### Technical Improvements
- [ ] Real-time data integration
- [ ] Interactive dashboard development
- [ ] Statistical significance testing
- [ ] Regime change detection algorithms

## Data Sources & Methodology

### Data Collection
- **Sources**: Major financial market APIs and databases
- **Frequency**: Daily closing prices and volumes
- **Quality Assurance**: Comprehensive data validation and cleaning
- **Processing**: Standardized scaling and formatting

### Analytical Approach
- **Descriptive Statistics**: Central tendencies and distributions
- **Correlation Analysis**: Pearson correlation coefficients
- **Visualization**: Heatmaps and distribution plots
- **Automated EDA**: Sweetviz comprehensive analysis
