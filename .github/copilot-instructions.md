# Portfolio Analysis Codebase - AI Agent Instructions

This repository contains Jupyter notebooks for financial portfolio analysis, with a focus on factor investing and returns analysis. Here's what you need to know to work effectively with this codebase:

## Project Structure

```
portfolio_exercises/          # Core analysis notebooks
├── E.6.1. Reversal Factor.ipynb  # Reversal factor analysis
├── factor_pricing.ipynb     # Factor pricing models
└── other analysis notebooks...

assignment_*/                # Grouped analysis assignments
├── data/                   # Data files per assignment
└── analysis notebooks...   # Factor analysis, DFA studies etc.

data/                       # Shared data directory
└── *.xlsx                 # Excel files with factor returns data
```

## Key Patterns & Conventions

### Data Loading
- Factor data is stored in Excel files with standardized sheet names:
  - "factors (excess returns)" for factor returns
  - "(total returns)" suffix for raw returns
  - Example: `reversal_data.xlsx`, `factor_pricing_data_monthly.xlsx`

```python
# Standard data loading pattern
df = pd.read_excel("../data/file.xlsx", sheet_name="sheet_name").set_index('Date')
```

### Analysis Functions
- Use the `summary()` function for standardized return statistics:
  ```python
  def summary(rets):
      """Summary statistics for a DataFrame of returns."""
      ann_rets = rets.mean() * 12  # Annualize monthly returns
      ann_vols = rets.std() * (12 ** 0.5)
      sharpe = ann_rets / ann_vols
      return pd.DataFrame({
          'Annualized Return': ann_rets,
          'Annualized Volatility': ann_vols,
          'Sharpe Ratio': sharpe
      })
  ```

### Visualization Standards
- Default figure size is (10,6) for time series plots
- Use title and proper axis labels
- Example:
  ```python
  prices.plot(title='Cumulative Returns', figsize=(10,6))
  ```

## Common Operations

### Return Calculations
- Convert returns to prices: `prices = (1 + returns).cumprod()`
- Subsetting by date: `df.loc['YYYY-MM-DD':]`
- Annualization factor (FREQ) = 12 for monthly data

### Factor Analysis Workflow
1. Load factor returns data
2. Calculate summary statistics
3. Generate time series plots
4. Compare performance metrics
5. Analyze correlations when relevant

## Working with Notebooks
- Execute cells in sequence to maintain state
- Configure Python environment with required packages:
  - pandas
  - numpy
  - matplotlib
  - seaborn
  - statsmodels
  - sklearn (for some regression analysis)

## Dependencies
Key libraries required:
- pandas: Data manipulation and analysis
- matplotlib/seaborn: Visualization
- statsmodels: Statistical analysis
- scipy: Statistical computations
- sklearn: Machine learning tools used in factor analysis