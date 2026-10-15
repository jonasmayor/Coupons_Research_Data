# Coupons Research Data — Coupon Acceptance Analysis

## Overview

This repository contains an exploratory data analysis of driver coupon acceptance using Python and a Jupyter Notebook. The goal is to identify patterns that distinguish drivers who accept a coupon from those who do not, with particular attention to coupon type, proximity, weather, travel context, bar-visiting behavior, age, income, occupation, and marital status.

The main analysis is available in [`prompt.ipynb`](prompt.ipynb).

## Data Source

The dataset comes from the **UCI Machine Learning Repository** and was collected through a survey on **Amazon Mechanical Turk**.

Survey participants were presented with hypothetical driving scenarios that varied by destination, time, weather, passenger type, coupon type, and other contextual factors. They were then asked whether they would accept a coupon while driving.

The target variable is `Y`:

- `Y = 1`: the driver would use the coupon right away or later before it expires.
- `Y = 0`: the driver would not use the coupon.

The dataset contains **12,684 observations** and **26 columns**.

Five coupon categories are represented:

- `Coffee House`
- `Restaurant(<20)`
- `Carry out & Take away`
- `Bar`
- `Restaurant(20-50)`

## Dataset Description

The variables can be grouped into three broad categories.

### Driver Attributes

Examples include:

- Gender
- Age
- Marital status
- Children
- Education
- Occupation
- Annual income
- Frequency of visiting bars
- Frequency of visiting coffee houses
- Frequency of buying take-away food
- Frequency of visiting restaurants

### Driving and Environmental Context

Examples include:

- Destination: home, work, or no urgent destination
- Passenger: alone, partner, children, or friends
- Weather: sunny, rainy, or snowy
- Temperature
- Time of day
- Approximate driving time to the coupon location
- Whether the coupon location is in the same or opposite travel direction

### Coupon Attributes

Examples include:

- Coupon type
- Expiration time: two hours or one day
- Coupon acceptance outcome (`Y`)

## Data Preparation

The notebook first investigates missing and potentially problematic data before performing the analysis.

Key cleaning decisions include:

- Missing values in the venue-frequency columns (`Bar`, `CoffeeHouse`, `CarryAway`, `RestaurantLessThan20`, and `Restaurant20To50`) were each below approximately 2%.
- Rows were removed only when the missing venue-frequency value was relevant to the coupon being analyzed. This removed **164 rows**, or about **1.3%** of the original observations.
- The `car` column was missing for approximately 99% of observations. Instead of dropping those rows, several car-related values were consolidated and missing values were treated as `car` for the purposes of the notebook's exploratory analysis.

## Analysis Approach

The notebook uses descriptive statistics and visualization techniques including:

- `value_counts`
- `groupby`
- `crosstab`
- Acceptance-rate calculations
- Bar charts
- Pie charts
- Histograms
- Heatmaps
- Multi-panel visualizations

The analysis focuses first on the complete coupon dataset and then investigates bar coupons in greater detail, followed by an independent comparison of other coupon categories.

## Key Findings

### Overall Coupon Acceptance

- **56.9%** of all coupons were accepted.
- Coupon distribution was not even across coupon types.
- `Coffee House` coupons were distributed most frequently.
- `Restaurant(20-50)` coupons were distributed least frequently.
- Acceptance varied substantially by coupon type:
  - `Carry out & Take away` had the strongest acceptance behavior in the notebook's comparison.
  - `Bar` had the weakest acceptance rate.
  - `Coffee House` coupons were approximately evenly split between accepted and rejected.

### Distance, Direction, and Temperature

- Coupons were more commonly associated with drivers who were closer to the coupon location.
- Coupons were often distributed when the business was in the **opposite direction** from the driver's destination.
- Most coupon observations occurred at temperatures near **80°F**.
- The exploratory analysis suggests that coupon acceptance increased at warmer temperatures, which also tended to coincide with sunnier weather in the dataset.

These relationships are observational and should not be interpreted as causal effects.

## Bar Coupon Analysis

Bar coupons received an overall acceptance rate of **41.0%**.

A strong relationship was observed between prior bar-going frequency and coupon acceptance:

- Drivers who visited bars **three or fewer times per month** accepted approximately **37.1%** of bar coupons.
- Drivers who visited bars **more than three times per month** accepted approximately **76.9%** of bar coupons.

The notebook also notes that drivers who reported never visiting bars can influence low-frequency comparisons. A small number of these drivers accepted a bar coupon, but most rejected it.

Additional bar-coupon comparisons showed:

- Drivers **over age 25 who visited bars more than once per month** had an acceptance rate of approximately **69.5%**, compared with **33.4%** among all other drivers.
- Drivers who visited bars more than once per month, had a passenger who was not a child, and did not work in farming/fishing/forestry had an acceptance rate of approximately **71.3%**, compared with **29.5%** among all others.
- The combined set of behavioral and demographic conditions tested in the notebook produced an acceptance rate of approximately **79.9%**, compared with **29.6%** among drivers outside those conditions.

### Age and Income Patterns

The exploratory analysis found that:

- Drivers roughly **21 to 30 years old** were more likely to accept bar coupons.
- Lower-income groups earning approximately **$37,500 or less** showed relatively strong bar-coupon acceptance.
- Drivers earning **$100,000 or more** also showed relatively strong acceptance.
- Among drivers who accepted bar coupons, the strongest concentration was among customers who visited bars several times per month, particularly around the `1~3` and `4~8` frequency categories.
- The age and income groups with higher acceptance were also concentrated among relatively frequent bar visitors.

## Additional Coupon Findings

The independent analysis compared acceptance patterns across carry-out/take-away and `Restaurant(20-50)` coupons.

### Carry Out & Take Away

Higher acceptance was observed among several occupational groups, including:

- Building & Grounds Cleaning & Maintenance
- Construction & Extraction
- Protective Service

The notebook also observed relatively high acceptance among widowed respondents for this coupon category.

### Restaurant ($20–$50)

Higher acceptance was observed among occupational groups including:

- Construction
- Healthcare
- Office & Administrative Support
- Production occupations

Singles and unmarried partners also showed relatively high acceptance in this portion of the analysis.

## Technologies Used

- Python
- Jupyter Notebook
- pandas
- NumPy
- Matplotlib
- Seaborn

## Repository Structure

```text
.
├── README.md
├── prompt.ipynb
└── data/
    └── coupons.csv
```

## Running the Notebook

1. Clone the repository.
2. Install the required Python packages:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

3. Confirm that the dataset is available at:

```text
data/coupons.csv
```

4. Start Jupyter Notebook:

```bash
jupyter notebook
```

5. Open `prompt.ipynb` and run the cells in order.

## Notes and Limitations

This project is an **exploratory data analysis**, so the results describe associations in the survey data rather than causal relationships.

Some categories, particularly occupations and marital-status groups, may contain relatively few observations. Acceptance percentages for smaller groups should therefore be interpreted carefully. In addition, treatment of the highly incomplete `car` column is based on an explicit assumption made in the notebook and may not be appropriate for every downstream analysis.

## Summary

The analysis indicates that coupon acceptance depends strongly on both the type of coupon and the driver's context. Bar-coupon acceptance is especially associated with prior bar-going behavior, while age, income, passenger type, occupation, proximity, weather, and travel context also show meaningful patterns in the exploratory results.
