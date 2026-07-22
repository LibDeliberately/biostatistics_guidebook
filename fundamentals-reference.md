# Fundamentals Reference

A quick-reference outline for statistics, R, SQL, Python, and SAS. Use this document to locate core concepts, common syntax, and typical workflows.

---

## Table of Contents

1. [Statistics](#statistics)
2. [R](#r)
3. [SQL](#sql)
4. [Python](#python)
5. [SAS](#sas)

---

## Statistics

### Descriptive Statistics

| Concept | Definition / Use |
|---|---|
| Mean | Average; sensitive to outliers |
| Median | Middle value; robust to outliers |
| Mode | Most frequent value |
| Standard deviation | Spread around the mean |
| Variance | SD squared; used in many models |
| IQR | Q3 − Q1; basis for outlier rules |
| Range | Max − min |

### Probability & Distributions

- **Random variable**: Numeric outcome of a random process (discrete or continuous)
- **Common distributions**:
  - Normal — symmetric, bell-shaped; basis for many tests
  - Binomial — count of successes in *n* trials
  - Poisson — count of rare events
  - *t*, *F*, Chi-square — used in hypothesis testing
- **Central Limit Theorem**: Sample means approach a normal distribution as *n* increases

### Inference

| Term | Meaning |
|---|---|
| Null hypothesis (H₀) | No effect / no difference |
| Alternative (H₁) | Effect or difference exists |
| *p*-value | Probability of observed (or more extreme) data if H₀ is true |
| α (significance level) | Threshold for rejecting H₀ (commonly 0.05) |
| Type I error | Reject H₀ when it is true (false positive) |
| Type II error | Fail to reject H₀ when it is false (false negative) |
| Power | 1 − P(Type II error); ability to detect a true effect |
| Confidence interval | Range likely to contain the true parameter |

### Common Tests

| Scenario | Typical Test |
|---|---|
| One sample mean vs. known value | One-sample *t*-test |
| Two independent group means | Two-sample *t*-test |
| Paired / repeated measures | Paired *t*-test |
| Three or more group means | ANOVA |
| Two proportions | Chi-square or Fisher's exact |
| Association between two categorical variables | Chi-square test of independence |
| Correlation between two continuous variables | Pearson or Spearman |
| Predict continuous outcome from predictors | Linear regression |
| Predict binary outcome | Logistic regression |
| Time-to-event / survival | Kaplan–Meier, Cox regression |

### Regression Essentials

- **Linear regression**: Y = β₀ + β₁X₁ + … + ε
- **Logistic regression**: log-odds of Y = linear combination of predictors
- **Key outputs**: coefficients, standard errors, *p*-values, R² / pseudo-R², residuals
- **Assumptions** (linear): linearity, independence, homoscedasticity, normality of residuals

### Sample Size & Power

- Larger samples → narrower confidence intervals, higher power
- Effect size, α, and power jointly determine required *n*
- Always specify primary endpoint and analysis plan before collecting data

---

## R

### Getting Started

```r
# Install and load packages
install.packages("dplyr")
library(dplyr)

# Help
?mean
help(lm)
```

### Data Structures

| Object | Description |
|---|---|
| Vector | 1-D sequence of values |
| Matrix | 2-D numeric array |
| Data frame | Table with named columns (most common for analysis) |
| List | Collection of heterogeneous objects |
| Factor | Categorical variable with levels |

### Import / Export

```r
# CSV
data <- read.csv("file.csv")
write.csv(data, "output.csv", row.names = FALSE)

# Excel (readxl package)
library(readxl)
data <- read_excel("file.xlsx", sheet = 1)
```

### Data Manipulation (dplyr)

```r
data %>%
  filter(age >= 18) %>%
  select(id, age, sex, outcome) %>%
  mutate(age_group = ifelse(age < 65, "young", "old")) %>%
  group_by(sex) %>%
  summarise(mean_outcome = mean(outcome, na.rm = TRUE))
```

### Descriptive Statistics

```r
summary(data)
mean(x, na.rm = TRUE)
sd(x, na.rm = TRUE)
table(data$category)
prop.table(table(data$category))
```

### Visualization (ggplot2)

```r
library(ggplot2)

ggplot(data, aes(x = group, y = value, fill = group)) +
  geom_boxplot() +
  labs(title = "Value by Group", x = "Group", y = "Value") +
  theme_minimal()
```

### Statistical Tests

```r
# t-test
t.test(outcome ~ group, data = data)

# Chi-square
chisq.test(table(data$var1, data$var2))

# Linear regression
model <- lm(outcome ~ age + sex, data = data)
summary(model)

# Logistic regression
glm(outcome ~ age + sex, data = data, family = binomial)
```

### Useful Packages

| Package | Purpose |
|---|---|
| `dplyr`, `tidyr` | Data wrangling |
| `ggplot2` | Visualization |
| `readr`, `readxl` | Data import |
| `survival` | Survival analysis |
| `broom` | Tidy model output |

---

## SQL

### Core Clauses (order of execution differs from writing order)

```sql
SELECT   column1, column2, AGG(column3) AS alias
FROM     schema.table
WHERE    condition          -- filter rows
GROUP BY column1, column2   -- aggregate
HAVING   aggregate_condition -- filter groups
ORDER BY column1 DESC       -- sort
LIMIT    100;                -- row cap (syntax varies by dialect)
```

### Joins

```sql
-- Inner join: matching rows only
SELECT a.id, b.value
FROM table_a a
INNER JOIN table_b b ON a.id = b.id;

-- Left join: all rows from left table
SELECT a.id, b.value
FROM table_a a
LEFT JOIN table_b b ON a.id = b.id;
```

| Join Type | Result |
|---|---|
| INNER | Rows with matches in both tables |
| LEFT | All left rows + matching right rows |
| RIGHT | All right rows + matching left rows |
| FULL OUTER | All rows from both tables |
| CROSS | Cartesian product |

### Filtering & Aggregation

```sql
-- Distinct values
SELECT DISTINCT category FROM patients;

-- Conditional aggregation
SELECT
  sex,
  COUNT(*) AS n,
  AVG(age) AS mean_age,
  SUM(CASE WHEN outcome = 1 THEN 1 ELSE 0 END) AS n_events
FROM patients
WHERE age >= 18
GROUP BY sex
HAVING COUNT(*) >= 10;
```

### Subqueries & CTEs

```sql
-- Common Table Expression (preferred for readability)
WITH adult_patients AS (
  SELECT *
  FROM patients
  WHERE age >= 18
)
SELECT sex, COUNT(*) AS n
FROM adult_patients
GROUP BY sex;
```

### Window Functions

```sql
SELECT
  id,
  value,
  ROW_NUMBER() OVER (PARTITION BY group_id ORDER BY date) AS row_num,
  AVG(value) OVER (PARTITION BY group_id) AS group_mean
FROM measurements;
```

### Data Modification

```sql
INSERT INTO table_name (col1, col2) VALUES ('a', 1);
UPDATE table_name SET col1 = 'b' WHERE id = 5;
DELETE FROM table_name WHERE id = 5;
```

---

## Python

### Getting Started

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import scipy.stats as stats
import statsmodels.api as sm
```

### Data Structures (pandas)

```python
# Read data
df = pd.read_csv("file.csv")
df = pd.read_excel("file.xlsx")

# Inspect
df.head()
df.info()
df.describe()

# Select and filter
df["column"]
df[["col1", "col2"]]
df[df["age"] >= 18]
df.loc[df["sex"] == "F", "outcome"]
```

### Data Manipulation

```python
# New column
df["age_group"] = np.where(df["age"] < 65, "young", "old")

# Group and aggregate
df.groupby("sex")["outcome"].agg(["count", "mean", "std"])

# Merge
pd.merge(df_a, df_b, on="id", how="inner")

# Handle missing values
df.dropna(subset=["outcome"])
df["col"].fillna(df["col"].median())
```

### Descriptive Statistics

```python
df["age"].mean()
df["age"].median()
df["age"].std()
df["category"].value_counts(normalize=True)
df.corr(numeric_only=True)
```

### Visualization

```python
df.boxplot(column="value", by="group")
plt.scatter(df["x"], df["y"])
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Scatter Plot")
plt.show()
```

### Statistical Tests

```python
# Independent t-test
stats.ttest_ind(group_a, group_b)

# Chi-square
contingency = pd.crosstab(df["var1"], df["var2"])
stats.chi2_contingency(contingency)

# Linear regression (statsmodels)
X = sm.add_constant(df[["age", "sex"]])
model = sm.OLS(df["outcome"], X).fit()
print(model.summary())

# Logistic regression
logit = sm.Logit(df["outcome"], X).fit()
```

### Useful Libraries

| Library | Purpose |
|---|---|
| `pandas` | Data frames and wrangling |
| `numpy` | Numerical operations |
| `matplotlib`, `seaborn` | Visualization |
| `scipy` | Statistical tests |
| `statsmodels` | Regression and inference |
| `scikit-learn` | Machine learning |

---

## SAS

### Program Structure

```sas
/* Comment style in SAS */
OPTIONS NOCENTER;

LIBNAME mylib 'C:\data';

DATA work.adults;
  SET mylib.patients;
  WHERE age >= 18;
RUN;

PROC PRINT DATA=work.adults;
  VAR id age sex outcome;
RUN;
```

### DATA Step Essentials

```sas
DATA work.new;
  SET work.old;

  /* Create / recode variables */
  IF age < 65 THEN age_group = 'young';
  ELSE age_group = 'old';

  /* Conditional logic */
  IF outcome = 1 THEN event = 'yes';
  ELSE event = 'no';

  /* Keep / drop columns */
  KEEP id age sex outcome age_group;
RUN;
```

### PROC Steps (Common Procedures)

| PROC | Purpose |
|---|---|
| `PROC PRINT` | Display data |
| `PROC CONTENTS` | Dataset metadata |
| `PROC MEANS` | Descriptive statistics |
| `PROC FREQ` | Frequency tables, chi-square |
| `PROC UNIVARIATE` | Detailed distribution stats |
| `PROC TTEST` | *t*-tests |
| `PROC ANOVA` / `PROC GLM` | Analysis of variance |
| `PROC REG` | Linear regression |
| `PROC LOGISTIC` | Logistic regression |
| `PROC PHREG` | Cox proportional hazards |
| `PROC SQL` | SQL queries within SAS |

### Descriptive Statistics

```sas
PROC MEANS DATA=work.adults N MEAN STD MEDIAN;
  VAR age outcome;
  CLASS sex;
RUN;

PROC FREQ DATA=work.adults;
  TABLES sex * outcome / CHISQ;
RUN;
```

### Statistical Modeling

```sas
/* Linear regression */
PROC REG DATA=work.adults;
  MODEL outcome = age sex;
RUN;

/* Logistic regression */
PROC LOGISTIC DATA=work.adults;
  MODEL outcome(event='1') = age sex;
RUN;
```

### SQL in SAS (PROC SQL)

```sas
PROC SQL;
  SELECT sex,
         COUNT(*) AS n,
         MEAN(age) AS mean_age
  FROM work.adults
  GROUP BY sex
  HAVING COUNT(*) >= 10;
QUIT;
```

### Export

```sas
PROC EXPORT DATA=work.adults
  OUTFILE='C:\output\adults.csv'
  DBMS=CSV REPLACE;
RUN;
```

---

## Cross-Language Quick Comparison

| Task | R | Python | SAS |
|---|---|---|---|
| Filter rows | `filter()` | `df[condition]` | `WHERE` / `IF` |
| Select columns | `select()` | `df[["cols"]]` | `KEEP` / `DROP` |
| Group summary | `group_by() %>% summarise()` | `groupby().agg()` | `PROC MEANS` / `GROUP BY` |
| Linear model | `lm()` | `sm.OLS()` | `PROC REG` |
| Logistic model | `glm(family=binomial)` | `sm.Logit()` | `PROC LOGISTIC` |
| Cross-tab / chi-square | `chisq.test(table())` | `chi2_contingency()` | `PROC FREQ / CHISQ` |

---

## Notes

- Always document your data dictionary, analysis plan, and software versions.
- Handle missing data explicitly; do not assume defaults are appropriate.
- Report effect sizes and confidence intervals, not just *p*-values.
- Validate results by cross-checking across tools when possible.
