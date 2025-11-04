# 2024 SHED Survey Codebook - Key Information Summary

## Survey Overview

**Survey Name:** 2024 Survey of Household Economics and Decisionmaking (SHED)

**Sponsor:** Board of Governors of the Federal Reserve System

**Data Collection:** Ipsos KnowledgePanel (online probability-based panel)

**Sample Size:** 12,295 respondents

**Field Period:** October 18-31, 2024

**Citation:** Board of Governors of the Federal Reserve System Survey of Household Economics and Decisionmaking [dataset] (Washington: Board of Governors, 2025), https://doi.org/10.17016/datasets.002

---

## Analysis Weights

Two weight sets are available:

1. **Single-year analysis:** `weight` and `weight_pop`
   - Use for 2024 cross-sectional analysis
   - `weight`: scaled to sample size
   - `weight_pop`: scaled to U.S. population (March 2024 CPS)

2. **Panel analysis:** `panel_weight` and `panel_weight_pop`
   - Use when analyzing respondents who completed both 2023 and 2024 surveys
   - 4,039 respondents completed both years

---

## Major Topic Areas

### Financial Well-Being
- **B2**: Overall financial management (4-point scale: difficult to get by → living comfortably)
- **B3**: Financial situation compared to 12 months ago
- **B0_a-c, B1_a-b**: Financial stress and control measures
- **EF1-EF7**: Emergency savings and ability to handle expenses

### Employment
- **D1A**: Work status last month
- **D3A**: Employment type (employee, self-employed, other)
- **D44_a-f**: Job transitions (raises, promotions, layoffs, new jobs)
- **D22_a-i**: Reasons for not working/working <35 hours

### Housing
- **GH1**: Housing tenure (own with mortgage, own free and clear, rent, neither)
- **R3**: Monthly rent amount
- **M4**: Monthly mortgage payment
- **GH3_a-e**: Neighborhood satisfaction

### Income & Spending
- **I40**: Total household income (15 categories: <$5,000 to $200,000+)
- **I0_a-f**: Income sources (wages, Social Security, pensions, etc.)
- **I20**: Spending relative to income
- **INF3_a-g**: Actions taken due to price increases

### Credit & Banking
- **C2A**: Credit card ownership
- **C3P**: Credit card payment behavior
- **A0**: Applied for credit in past 12 months
- **BK1**: Has checking/savings/money market account
- **BK47_a-b**: Experience with financial fraud

### Education & Student Loans
- **ED0**: Highest education level (9 categories)
- **SL1**: Has student loan debt
- **SL3**: Amount owed on student loans
- **SL6**: Behind on student loan payments

### Retirement
- **D1I**: Considers self retired
- **K0**: Retirement savings on track
- **K21_a-f**: Types of retirement savings/assets

### Healthcare
- **E1_a-e**: Went without needed healthcare due to cost
- **E2**: Unexpected major medical expenses
- **E4_a-f**: Types of health insurance coverage

### Demographics (from Ipsos profile)
- **ppage**: Age (18-97)
- **ppgender**: Gender
- **ppethm/race_5cat**: Race/ethnicity (5 categories)
- **ppeduc5/ppeducat**: Education (4-5 categories)
- **ppinc7**: Household income (7 categories)
- **ppreg4**: Census region

---

## Key Constructed Variables

- **atleast_okay**: Doing at least okay financially (B2 = 3 or 4)
- **pay_casheqv**: Can handle $400 expense with cash/equivalent
- **educ_4cat**: Education in 4 categories
- **inc_4cat_50k**: Income in 4 categories with $50k breakpoint

---

## Special Features

- **Panel component:** Links to 2023 (caseid2023) and 2022 (caseid2022) surveys
- **Experimental variations:** Some respondents received different question wording (DOV_* flags)
- **Imputation flags:** Variables ending in "_iflag" indicate imputed values
- **Missing data:** Coded as "." with varying amounts by variable

---

## Important Notes

- Not all survey variables are in the public dataset (geography details and free-text excluded)
- Demographic profile variables (prefix "pp") collected by Ipsos before SHED administration
- Survey duration ranges from 385 to 1,038,184 seconds (median: 1,319 seconds ≈ 22 minutes)