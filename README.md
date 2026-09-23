# Elderly Healthcare Access Analysis

## Health Spending and Life Expectancy in East Africa

This project explores whether **higher current health expenditure per capita is associated with longer life expectancy at birth** across five East African countries: **Rwanda, Kenya, Uganda, Burundi, and Tanzania**. The analysis is intended as an initial investigation into regional healthcare investment and outcomes, with particular relevance to questions about access to healthcare for older adults.

The main analysis is contained in [`Stats.ipynb`](Stats.ipynb).

**Important:** Life expectancy at birth is used as a broad population-level proxy. It is not an elderly-specific measure of healthy life expectancy or healthcare access for older adults.

## Research question

Does higher current health expenditure per capita predict longer life expectancy at birth among the selected East African countries?

## Data

The CSV files contain World Bank Open Data indicators for the five countries listed above. The source files include annual columns from **1960 through 2025**; the notebook narrows the analytical window to **2000–2022**, where the two indicators can be joined for the country-year observations used in the model.

| File | Indicator | World Bank indicator code | Unit |
| --- | --- | --- | --- |
| `health_expenditure.csv` | Current health expenditure per capita | `SH.XPD.CHEX.PC.CD` | Current US dollars per person |
| `life_expectancy.csv` | Life expectancy at birth, total | `SP.DYN.LE00.IN` | Years |

The files use a wide format: identifying fields are followed by one column per year. The notebook converts both datasets to a country-year format before merging them.

## Analysis workflow

The notebook performs the following steps:

1. Loads the two CSV files with pandas.
2. Selects the year columns from 2000 through 2022.
3. Reshapes the health expenditure and life expectancy tables from wide to long format.
4. Merges the indicators on country and year and removes incomplete observations.
5. Produces exploratory visualizations:
   - health spending versus life expectancy by country;
   - the same relationship with a fitted trend line;
   - average health spending and average life expectancy by country; and
   - life expectancy trends over time.
6. Fits an ordinary least squares (OLS) regression with life expectancy as the dependent variable and health spending per capita as the explanatory variable.

The resulting analysis contains **115 country-year observations**: five countries across 23 years.

## Key findings from the notebook

- Health spending is positively and statistically significantly associated with life expectancy in the sample (`p < 0.001`).
- The fitted model reports **R² = 0.406**, meaning health spending alone explains approximately 41% of the observed variation in life expectancy in this dataset.
- The notebook estimates that each additional **$10 per person** in health spending is associated with approximately **1.6 additional years** of life expectancy. This is an association, not a causal estimate.
- Kenya appears as a high-spending outlier whose life expectancy does not rise proportionally with expenditure.
- Rwanda shows strong improvement in life expectancy despite relatively low per-capita spending, suggesting that the efficiency and allocation of spending may matter as much as its volume.
- The relationship appears to flatten at higher spending levels, consistent with a possible diminishing-returns pattern.

These findings should be treated as exploratory. Country-level averages cannot establish that spending caused changes in life expectancy.

## Requirements

The notebook uses Python and the following packages:

- Python 3.9 or newer
- Jupyter Notebook or JupyterLab
- pandas
- matplotlib
- seaborn
- statsmodels

Install the dependencies with:

```bash
python -m pip install jupyter pandas matplotlib seaborn statsmodels
```

A virtual environment is recommended:

```bash
python -m venv .venv
source .venv/bin/activate        # macOS/Linux
# .venv\\Scripts\\activate     # Windows PowerShell
python -m pip install --upgrade pip
python -m pip install jupyter pandas matplotlib seaborn statsmodels
```

## Run the analysis

From the directory that contains the `stats/` folder, launch Jupyter:

```bash
jupyter notebook
```

Open `stats/Stats.ipynb` and run the cells from top to bottom.

The notebook currently reads the data with paths of the form:

```python
pd.read_csv('stats/health_expenditure.csv')
pd.read_csv('stats/life_expectancy.csv')
```

Therefore, start Jupyter from the project’s parent directory, or update those paths if you open the notebook with a different working directory.

## Project structure

```text
stats/
├── README.md
├── Stats.ipynb
├── health_expenditure.csv
└── life_expectancy.csv
```

## Interpretation and limitations

This is an ecological, observational analysis based on country level aggregates. It does not control for education, sanitation, income, disease burden, nutrition, healthcare quality, demographic change, governance, or other factors that may affect life expectancy. Within-country inequalities, including urban-rural and income-related differences, are also hidden by national averages.

The OLS model uses one explanatory variable and should not be interpreted as evidence that additional spending directly causes longer lives. Reverse causality, omitted variables, measurement differences, and the use of life expectancy at birth rather than an elderly-specific outcome may all affect the results.

## Author

Sandra Kayirangwa