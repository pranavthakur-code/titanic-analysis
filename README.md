# Titanic Survival Analysis

**Project type:** Data Analytics / Exploratory Data Analysis (EDA)\
**Prepared by:** Pranav Thakur\
**Internship context:** Data Analyst Internship --- Yuva Intern

## Project Overview

This project analyzes Titanic passenger records to understand which
passenger characteristics were associated with survival. It explores
factors such as sex, ticket class, age, family size, fare, and port of
embarkation. A logistic regression model is also used as a simple
predictive check.

The analysis is based on 891 passenger records and 15 columns from the
Titanic dataset available in the [`seaborn-data`
repository](https://github.com/mwaskom/seaborn-data/blob/master/titanic.csv).

## Objectives

-   Explore and summarize the Titanic passenger dataset.
-   Identify and handle missing values and redundant columns.
-   Analyze survival rates across passenger groups.
-   Use statistical tests to assess selected associations.
-   Create visualizations to communicate findings.
-   Evaluate a logistic regression model against a simple baseline.

## Tools and Technologies

-   **Python**
-   **Pandas** and **NumPy** --- data handling and feature engineering
-   **Matplotlib** and **Seaborn** --- visualizations
-   **SciPy** --- statistical tests
-   **Scikit-learn** --- logistic regression, train/test split,
    cross-validation, and accuracy evaluation
-   **Jupyter Notebook** --- analysis environment

## Dataset

The dataset contains 891 rows and 15 columns. Important fields include:

  Column          Description
  --------------- ------------------------------------
  `survived`      Target: `1` = survived, `0` = died
  `pclass`        Ticket class: 1st, 2nd, or 3rd
  `sex`           Passenger sex
  `age`           Passenger age in years
  `sibsp`         Number of siblings/spouses aboard
  `parch`         Number of parents/children aboard
  `fare`          Ticket fare
  `embark_town`   Port of embarkation
  `deck`          Cabin deck; mostly missing

The dataset also contains derived or redundant fields. The notebook
checks redundancy before removing duplicate-information columns.

## Workflow

1.  **Load and inspect data** --- review shape, data types, summary
    statistics, missing values, and duplicate rows.
2.  **Clean and preprocess**:
    -   Remove `alive`, `class`, and `embarked` after verifying they
        duplicate other fields.
    -   Replace the mostly missing `deck` field with a `has_cabin_info`
        indicator.
    -   Fill missing `embark_town` values with the mode.
    -   Impute missing `age` values using the median for the same sex
        and passenger class, and retain an `age_was_missing` flag.
    -   Keep identical rows because the dataset has no passenger ID and
        identical records may represent different passengers.
    -   Keep fare and age outliers when they may be valid observations;
        use a log-transformed fare feature for analysis/modeling.
3.  **Engineer features** --- create `family_size`, `age_group`, and
    `log_fare`.
4.  **Exploratory data analysis** --- compare survival by sex, ticket
    class, age group, embarkation port, fare, and family size.
5.  **Statistical analysis** --- use chi-square tests for sex/class
    associations, a Welch t-test for age, and a Mann--Whitney U test for
    fare.
6.  **Predictive check** --- train a logistic regression model using an
    80/20 stratified train/test split and evaluate with test accuracy
    and 5-fold cross-validation.

## Key Findings

-   The overall survival rate was **38.4%**.
-   **Sex showed a strong association with survival:** 74.2% of female
    passengers survived, compared with 18.9% of male passengers.
-   **Ticket class was associated with survival:** survival rates were
    63.0% in first class, 47.3% in second class, and 24.2% in third
    class.
-   The combined effect of sex and class was substantial: first-class
    women had a survival rate of 96.8%, while third-class men had a
    survival rate of 13.5%.
-   Survivors paid higher fares in this dataset; the median fare was
    26.0 for survivors and 10.5 for passengers who died.
-   The age comparison between survivors and passengers who died was not
    statistically significant at the 5% level in the reported Welch
    t-test (`p = 0.082`).
-   Family size showed a non-linear pattern: groups of around two to
    four family members had higher observed survival rates than people
    travelling alone or in very large groups.

These results describe associations in this dataset; they do not prove
that any single characteristic caused survival differences.

## Visualizations

The notebook generates plots including:

-   Survival rate by sex and ticket class
-   Age distribution by survival outcome
-   Fare by ticket class and outcome (log scale)
-   Survival percentage by sex and class (heatmap)
-   Survival rate by family size

The notebook saves the figures as `fig1_sex_class.png`,
`fig2_age_hist.png`, `fig3_fare_box.png`, `fig4_heatmap.png`, and
`fig5_family.png` when executed.

## Predictive Model

A **Logistic Regression** model was trained using ticket class, sex,
age, family size, and log-transformed fare.

-   Train/test split: 80/20, stratified, with `random_state=0`
-   Baseline accuracy (predicting no one survives): **61.5%**
-   Test accuracy: **78.8%**
-   Mean 5-fold cross-validation accuracy: **79.4%**

This is a simple predictive check, not a production-ready survival
prediction system.

## Repository Files

Suggested repository structure:

``` text
titanic-survival-analysis/
├── Titanic_Analysis.ipynb
├── Titanic_Analysis_Report.docx
├── titanic.csv
├── README.md
└── fig1_sex_class.png
    fig2_age_hist.png
    fig3_fare_box.png
    fig4_heatmap.png
    fig5_family.png
```

The dataset and generated images should be included in the repository if
the notebook is expected to run and display all outputs. The notebook
reads the dataset from `titanic.csv` in its working directory.

## How to Run

1.  Clone or download the repository.

2.  Ensure Python and Jupyter Notebook are installed.

3.  Install the required libraries:

    ``` bash
    pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
    ```

4.  Place `titanic.csv` in the same working directory as
    `Titanic_Analysis.ipynb`.

5.  Open Jupyter Notebook and run the notebook cells in order.

## Limitations and Next Steps

-   The dataset contains 891 passenger records, not the complete set of
    everyone aboard.
-   About 20% of age values were imputed, which can reduce observed age
    variation.
-   The analysis identifies associations, not causation.
-   Further work could extract passenger titles from names, test
    tree-based models, and compare results with a fuller passenger list.

## Author

**Pranav Thakur**\
- GitHub: [pranavthakur-code](https://github.com/pranavthakur-code)\
- LinkedIn: [Pranav
Thakur](https://www.linkedin.com/in/pranav-thakur013)
