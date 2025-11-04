# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a data analysis project analyzing household financial vulnerability using the **2024 Survey of Household Economics and Decisionmaking (SHED)** from the Federal Reserve Board. The analysis focuses on financial well-being patterns, particularly examining Hispanic populations, age-based vulnerabilities, and interconnected financial stress indicators.

**Data Source**: Board of Governors of the Federal Reserve System Survey of Household Economics and Decisionmaking [dataset] (Washington: Board of Governors, 2025), https://doi.org/10.17016/datasets.002

**Sample**: 12,295 respondents surveyed October 18-31, 2024

## Environment Setup

The project uses a Python virtual environment located at `.venv/`.

**Activate environment:**
```bash
source .venv/bin/activate
```

**Install dependencies:**
```bash
.venv/bin/pip install pandas numpy matplotlib seaborn plotly jupyter jupyterlab kaleido scikit-learn
```

**Run Jupyter Lab:**
```bash
.venv/bin/jupyter lab
```

## Data Files

- `data.csv` - Full SHED 2024 dataset (40MB, 12,295 respondents)
- `data_optimized.csv` - Filtered dataset excluding retired respondents (16MB, ~7,858 respondents)
- `data_hispanic.csv` - Hispanic population subset (2.7MB)
- `codebook.md` - Complete variable definitions and response codes
- `codebooksummary.md` - Quick reference for key survey variables

**Important**: Most analyses use `data_optimized.csv` which excludes retired respondents to focus on working-age financial vulnerability.

## Analysis Notebooks Structure

All notebooks follow a consistent pattern:

1. **Setup**: Import libraries (pandas, numpy, matplotlib, seaborn, plotly), configure visualization settings, set custom color palettes
2. **Data Loading**: Load CSV with pandas, apply filters, create derived variables
3. **Weighted Analysis**: All percentages must use `weight_pop` (population weights) for accurate estimates
4. **Visualization**: Publication-quality charts with annotations, exported as PNG (300 DPI) and SVG

### Common Analysis Patterns

**Weighted percentage calculation:**
```python
def weighted_pct(df, condition_col, weight_col='weight_pop'):
    total_weight = df[weight_col].sum()
    condition_weight = df[df[condition_col] == 'Yes'][weight_col].sum()
    return (condition_weight / total_weight) * 100
```

**Age group consolidation:**
Most analyses use 3 consolidated age groups: `18-29`, `30-44`, `45+` derived from `ppagect4`

**Hispanic analysis:**
Uses `pphispan` for Hispanic origin subgroups (Mexican, Puerto Rican, Cuban, Other)

## Key Survey Variables

### Financial Well-Being
- `B2` - Overall financial situation (4-point scale: comfortable → difficult)
- `atleast_okay` - Derived: doing at least okay financially
- `pay_casheqv` - Can handle $400 emergency with cash
- `EF1` - Has emergency/rainy day funds (Yes/No)
- `EF7` - Largest emergency expense you could handle

### Employment & Income
- `D3A` - Employment type (employee, self-employed, other)
- `I40` - Total household income (15 categories)
- `inc_4cat_50k` - Income in 4 categories with $50k breakpoint
- `I20` - Spending relative to income

### Credit & Alternative Finance
- `A0` - Applied for credit in past 12 months
- `A1_a/b/c` - Credit denial, reduction, or avoidance
- `BK2_a-f` - Alternative financial services (money orders, check cashing, payday loans, pawn shops, tax advances, overdraft fees)
- `C3P` - Credit card payment behavior

### Healthcare & Housing
- `E1_a-e` - Healthcare cost barriers (prescription, doctor, mental health, dental, follow-up)
- `GH1` - Housing tenure (own with mortgage, own free/clear, rent, neither)

### Demographics (Ipsos profile)
- `ppage` - Age (18-97)
- `ppgender` - Gender
- `ppethm` / `race_5cat` - Race/ethnicity
- `ppeduc5` / `ppeducat` - Education level
- `ppreg4` - Census region

**Reference**: See `codebook.md` for complete variable definitions and response codes.

## Visualization Standards

### Color Palettes
- **Age groups**: Red (`#E63946`) for 18-29, Orange (`#F77F00`) for 30-44, Blue (`#06AED5`) for 45+
- **Financial health gradient**: Green (positive) → Orange (moderate) → Red (negative/predatory)

### Figure Settings
```python
plt.style.use('seaborn-v0_8-darkgrid')
plt.rcParams['figure.figsize'] = (12, 6)
plt.rcParams['font.size'] = 11
```

### Export Requirements
All publication-ready visualizations should be exported as both:
- PNG at 300 DPI (scale=2): `fig.write_image("filename.png", width=1200, height=700, scale=2)`
- SVG for scalability: `fig.write_image("filename.svg", width=1200, height=700)`

## Analysis Approach

### Weighted Analysis Requirement
All percentage calculations MUST use population weights (`weight_pop`) to generate accurate population estimates. Never use raw counts for percentages.

### Interconnected Vulnerability Focus
Analyses examine relationships between financial stress indicators rather than isolated metrics:
- Credit exclusion → alternative finance usage patterns
- Emergency savings gaps → retirement account raids
- Healthcare cost barrier clustering
- Income volatility → financial coping mechanisms

### Segmentation Strategy
Primary segmentation by:
1. Age groups (3 consolidated groups: 18-29, 30-44, 45+)
2. Financial stress profiles (combinations of emergency funds, bill payment struggles, credit access)
3. Hispanic origin subgroups when analyzing ethnic disparities

## Special Considerations

- **Missing data**: Handle missing values in survey responses (often coded as NaN or specific numeric codes)
- **Panel data**: Subset of respondents (4,039) completed both 2023 and 2024 surveys; use `panel_weight_pop` for longitudinal analysis
- **Retired respondents**: Most working-age analyses exclude retired respondents using filters on `D1I`
- **Survey duration**: Ranges from 385 to 1,038,184 seconds (median ~22 minutes); extreme values may indicate data quality issues
