# Rhode Island Police Activity Analysis

A data analysis project exploring police stop data from Rhode Island (2005–2015), combined with weather data to uncover patterns in traffic enforcement, arrests, searches, and demographic disparities.

## Dataset

| File | Description |
|---|---|
| `RI-clean_data/RI_cleaned.csv` | Police stop records (Rhode Island, 2005–2015) |
| `RI-clean_data/RI-weather.csv` | Daily weather observations from NOAA (Providence, RI) |

The police dataset is sourced from the [Stanford Open Policing Project](https://openpolicing.stanford.edu/).  
Weather data is sourced from [NOAA Climate Data Online](https://www.ncdc.noaa.gov/cdo-web/).

## Project Structure

```
01_Police_analizing/
├── 01_Preparing_data.ipynb   # Main analysis notebook (all 5 chapters)
├── RI-clean_data/
│   ├── RI_cleaned.csv        # Cleaned police stop data
│   └── RI-weather.csv        # Daily weather data
└── README.md
```

## Notebook Chapters

### Chapter 1 — Data Preparation
- Load and inspect raw data
- Drop irrelevant columns (`county_name`, `state`)
- Handle missing values (remove rows with no `driver_gender`)
- Fix incorrect data types (`is_arrested`, `search_conducted` → bool)
- Parse and combine `stop_date` + `stop_time` into a proper `DatetimeIndex`

### Chapter 2 — Gender and Policing
- Violation frequency breakdown by gender
- Arrest and search rates: male vs. female drivers
- Protective frisk analysis (rate per gender, rate among searched drivers)

### Chapter 3 — Visual EDA
- Hourly arrest rate (line plot)
- Annual drug-related stop trend and search rate (resampled to yearly)
- Violation frequency by district (stacked bar — zone comparison)
- Stop duration mapping to numeric minutes
- Mean stop duration by violation type

### Chapter 4 — Weather Dataset
- Load and select relevant NOAA columns
- Temperature statistics and box plot
- Bad weather conditions score (sum of WT-flags)
- Ordered categorical `rating` column: `good` / `bad` / `worse`
- Merge police and weather data on date
- Arrest rate by weather rating and violation type
- Pivot table: violation × weather rating

### Chapter 5 — Predictive Modeling & Final Conclusions
- Feature engineering: time features (hour, month, weekday), label encoding
- **Logistic Regression** baseline classifier
- **Random Forest** classifier (100 estimators)
- Feature importance visualization
- Confusion matrix comparison (LR vs. RF)
- Arrest rate by driver race and by violation/gender
- Hourly and monthly arrest rate patterns
- Correlation heatmap of numeric variables
- Written conclusions summarizing all key findings

## Requirements

```
pandas>=2.0
matplotlib
seaborn
scikit-learn
jupyter
nbconvert
```

Install with:

```bash
pip install pandas matplotlib seaborn scikit-learn jupyter nbconvert
```

## How to Run

```bash
jupyter notebook 01_Preparing_data.ipynb
```

Or execute non-interactively:

```bash
jupyter nbconvert --to notebook --execute --inplace 01_Preparing_data.ipynb
```

## Key Findings

1. **Violation patterns** — Speeding is the most common violation for both genders. Male drivers are stopped and arrested at higher rates.
2. **Search & frisk** — Males are searched more frequently across all violation types.
3. **Time of day** — Arrest rates peak between midnight and 3 AM.
4. **Weather** — Weather conditions have a modest effect on arrest rates; more arrests occur in good weather (more traffic).
5. **Racial disparities** — Arrest rates differ across racial groups, consistent with national research.
6. **Predictive model** — Random Forest achieves ~85–90% accuracy. Most predictive features: violation type, stop duration, hour, and whether a search was conducted.

## Notes

- All analyses are exploratory and descriptive.
- The model is not intended for operational use in policing.
- Dataset covers Rhode Island only and may not generalize to other states.
