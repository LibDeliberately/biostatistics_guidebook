# Choosing a Hypothesis Test for Simple Bivariate Analyses

When we have **two variables** and want to ask whether they are related—or whether groups differ in some meaningful way—this guide is where I start for picking a test.

---

## Before We Pick a Test

**Bivariate** means we are looking at the relationship between two variables at a time (for example, treatment group and blood pressure, or smoking status and disease).

Before choosing, I walk through three questions:

1. **What is my outcome (the thing I care about measuring)?**  
   Is it continuous (numbers like age, BMI, blood pressure) or categorical (categories like yes/no, mild/moderate/severe)?

2. **What is my predictor / grouping variable?**  
   Is it also continuous, or is it categorical (groups like drug vs. placebo, or male vs. female)?

3. **Are my observations independent or paired?**  
   - **Independent**: each person (or unit) appears in only one group.  
   - **Paired / matched**: the same person is measured twice (before/after), or people are matched in pairs.

Also worth keeping in mind:

- A **significant result** (*p* < your chosen α, often 0.05) means the data are unlikely under the null hypothesis. It does **not** by itself prove cause and effect.
- Always check whether the data roughly meet the test’s **assumptions**. If they do not, use the nonparametric alternative listed below, or transform / use a different method.
- Report the **effect size** and/or a **confidence interval**, not only the *p*-value.

---

## Quick Decision Guide

Use this table to find a starting point. Then read that test’s section for when it applies, assumptions, hypotheses, and how to interpret a significant result.

| Outcome variable | Predictor / comparison | Relationship of observations | Usual first choice | Common alternative if assumptions fail |
|---|---|---|---|---|
| Continuous | Two independent groups | Independent | Two-sample *t*-test | Wilcoxon rank-sum (Mann–Whitney) |
| Continuous | Same subjects measured twice, or matched pairs | Paired | Paired *t*-test | Wilcoxon signed-rank |
| Continuous | Three or more independent groups | Independent | One-way ANOVA | Kruskal–Wallis |
| Continuous | Another continuous variable | Independent pairs of measurements | Pearson correlation (or simple linear regression) | Spearman correlation |
| Binary / categorical | Another categorical variable | Independent | Chi-square test of independence | Fisher’s exact test (small samples) |
| Binary (yes/no) | Same subjects measured twice (or matched pairs) | Paired | McNemar’s test | Exact McNemar / related exact methods |

**Tip:** If we are unsure whether a continuous outcome is “normal enough,” look at histograms or Q–Q plots by group, and consider whether sample sizes are large. When in doubt for small samples with skewed data, the nonparametric option is often safer.

---

## Continuous Outcome, Two Independent Groups

### Two-sample (independent) *t*-test

**When:** Continuous outcome variable, two independent groups in the predictor, and independence between observations. Example: mean systolic BP (mmHg) in drug vs. placebo.

**Assumptions:** Normal distribution of outcomes in each group, and variances in each group are similar. (With larger samples, normality is less critical. If variances differ, Welch’s *t*-test is a common default.)

**Null Hypothesis:** The population difference in means between the two groups is 0.

$H_0: \mu_1 - \mu_2 = 0$

**Alternative Hypothesis:** The population difference in means between the two groups is statistically different from 0.

$H_A: \mu_1 - \mu_2 \ne 0$

Using alpha = 0.05, a significant result means there is sufficient evidence that the **population means differ** between the two groups. Say *how much* they differ (mean difference and confidence interval, with units). Do not claim the grouping variable *caused* the difference unless the study design supports causal inference (for example, a randomized trial).

---

### Wilcoxon rank-sum test (also called Mann–Whitney *U* test)

**When:** Same setup as the two-sample *t*-test—continuous (or ordinal) outcome, two independent groups—but the outcome is skewed, has outliers, or is better thought of as ordered ranks than as a normal mean.

**Assumptions:** Independence of observations. Under the usual interpretation, the two groups have similarly shaped distributions (then a significant result points to a shift in location, often summarized with medians).

- **Note:** If variances are not similar, the test can still be run, but it no longer showcases a clean median difference. Significance where shapes differ can mean **stochastic dominance**.

**Null Hypothesis:** The population difference in medians (or location) between the two groups is 0.

$H_0: M_1 - M_2 = 0$

**Alternative Hypothesis:** The population difference in medians (or location) between the two groups is statistically different from 0.

$H_A: M_1 - M_2 \ne 0$

Using alpha = 0.05, a significant result means there is sufficient evidence that the **distributions differ** between groups. Commonly this means that one group tends to have higher values than the other. Focus on **medians** or ranks rather than means unless we have explicitly checked that the means are still meaningful.

---

## Continuous Outcome, Paired or Matched Data

### Paired *t*-test

**When:** For when we want to compare the means of two related groups. Continuous dependent variable, dependent paired observations (before vs. after on the same subjects, or matched pairs).

**Assumptions:** Independence of pairs, normality of the within-pair differences.

**Null Hypothesis:** The mean within-pair difference is 0.

$H_0: \mu_d = 0$

**Alternative Hypothesis:** The mean within-pair difference is statistically different from 0.

$H_A: \mu_d \ne 0$

Using alpha = 0.05, a significant result means there is sufficient evidence that the **mean difference** within pairs is not zero (for example, scores changed from baseline to follow-up). Report the mean change and its confidence interval, with units.

---

### Wilcoxon signed-rank test

**When:** For when we want to compare two related measurements, but paired differences are not normally distributed, the dependent variable is ordinal, and/or the sample size is too small to assume normality.

**Assumptions:** Independence of pairs, paired observations, symmetric distribution of differences (for the standard interpretation).

**Null Hypothesis:** The median within-pair difference is 0.

$H_0: M_d = 0$

**Alternative Hypothesis:** The median within-pair difference is statistically different from 0.

$H_A: M_d \ne 0$

Using alpha = 0.05, a significant result means there is sufficient evidence of a **systematic change** between the paired measurements (one condition tends to produce higher values than the other). Summarize with the median difference where possible.

---

## Continuous Outcome, Three or More Independent Groups

### One-way ANOVA

**When:** For comparing a continuous outcome between 3+ groups (for example, three different diets, or 3 species of penguins!).

**Assumptions:** Continuous dependent variable, independence of observations, normality, homogeneity of variances (homoskedasticity).

**Null Hypothesis:** All group means are not statistically different from each other.

$H_0: \mu_1 = \mu_2 = \mu_3 = \cdots$

**Alternative Hypothesis:** At least one group mean is statistically different from the others.

$H_A:$ at least one $\mu$ differs

Using alpha = 0.05, a significant one-way ANOVA means there is sufficient evidence that **not all group means are equal**—at least one group mean differs from another. ANOVA alone does **not** tell us *which* groups differ. Now that we know at least one group is different, we can perform a post-hoc Tukey HSD test (or another appropriate pairwise procedure) to determine which group(s) differ. Report means or mean differences and confidence intervals, not only *p*-values.

---

### Kruskal–Wallis test

**When:** Same setup as one-way ANOVA when normality or equal-variance assumptions are doubtful, or when the outcome is ordinal.

**Assumptions:** Three or more independent, categorical groups; continuous or ordinal outcome; independence of observations; similar distribution shapes across groups if we want to interpret the result mainly as a difference in medians / location.

**Null Hypothesis:** All group medians are not statistically different from each other.

$H_0: M_1 = M_2 = M_3 = \cdots$

**Alternative Hypothesis:** At least one group median is statistically different from the others.

$H_A:$ at least one $M$ differs

Using alpha = 0.05, a significant result means there is sufficient evidence that **at least one group’s distribution differs** from the others. Follow up with pairwise nonparametric comparisons (for example, Dunn’s test) if we need to know which groups differ.

---

## Two Continuous Variables

### Pearson correlation

**When:** For measuring the strength and direction of a **linear** relationship between two quantitative & continuous variables (for example, age and cholesterol).

**Assumptions:** Two continuous variables, a roughly linear relationship, normal distribution (or residuals that behave reasonably), no extreme outliers, independence of observations. Sensitive to outliers.

**Null Hypothesis:** There is no linear relationship between the two variables in the population.

$H_0: \rho = 0$

**Alternative Hypothesis:** There is a significant linear relationship between the two variables in the population.

$H_A: \rho \ne 0$

Using alpha = 0.05, a significant result means there is sufficient evidence of a **nonzero linear correlation**. The correlation coefficient *r* tells direction (positive/negative) and strength (closer to ±1 is stronger). Correlation is **not** causation, and it does not describe curved relationships well.

- **Note:** Visualizing the data first matters a lot—Simpson’s paradox and curved patterns can make a single *r* misleading.

---

### Spearman correlation

**When:** For measuring the strength of association between two continuous (or ordinal) variables when we care about a **monotonic** relationship, ordinal data, or skewed distributions. Unlike Pearson, Spearman is better when the relationship is not a straight line but still consistently increasing or decreasing.

**Assumptions:** Two ordinal or continuous variables, monotonic relationship, data represent paired observations, independent pairs.

**Null Hypothesis:** There is no monotonic relationship between the two variables in the population.

$H_0: \rho_s = 0$

**Alternative Hypothesis:** There is a significant monotonic relationship between the two variables in the population.

$H_A: \rho_s \ne 0$

Using alpha = 0.05, a significant result means there is sufficient evidence of a **monotonic association** between the variables. Interpret the Spearman coefficient similarly to Pearson for direction and strength, but remember it is based on **ranks**, not raw linear slope.

---

### Simple linear regression (one predictor)

**When:** When we want to **predict** or **estimate the average change** in a continuous outcome for a one-unit change in a continuous predictor. Closely related to Pearson correlation when there is one continuous predictor.

**Assumptions** (check residuals): Linear relationship between predictor and mean outcome; independent observations; roughly constant variance of residuals (homoscedasticity); residuals approximately normal (mainly for inference in smaller samples). One continuous outcome; one predictor (continuous, or a binary predictor coded 0/1).

**Null Hypothesis:** The slope for the predictor is 0.

$H_0: \beta_1 = 0$

**Alternative Hypothesis:** The slope for the predictor is not 0.

$H_A: \beta_1 \ne 0$

Using alpha = 0.05, a significant coefficient means there is sufficient evidence that the **slope is not zero**: the average outcome changes as the predictor changes. Report the estimated slope and confidence interval, with units.

- **Note:** Significance alone does not establish causality.

---

## Two Categorical Variables

### Chi-square test of independence

**When:** Test whether two categorical variables are associated in a contingency table (for example, exposure yes/no vs. disease yes/no, or treatment arm vs. response category). Independent observations; usually a 2×2 (or larger) table.

**Assumptions:** Independence of observations; *expected* cell counts are large enough (a common rule of thumb: most expected counts ≥ 5; no expected count too small).

- **Note:** To determine expected cell counts: Expected = (Row Total × Column Total) / Grand Total.

**Null Hypothesis:** The two categorical variables are independent in the population.

$H_0:$ no association (independence)

**Alternative Hypothesis:** The two categorical variables are not independent.

$H_A:$ association present

Using alpha = 0.05, a significant result means there is sufficient evidence that the two variables are **not independent**—the distribution of one variable differs across levels of the other. Inspect percentages (and risk ratios / odds ratios in 2×2 tables) to describe **how** they are associated.

---

### Fisher’s exact test

**When:** Same question as the chi-square test, especially for **small samples** or tables with small expected cell counts (very common in 2×2 tables).

**Assumptions:** Independence of observations. In the classic 2×2 version, row and column totals are treated as fixed (exact enumeration of tables).

**Null Hypothesis:** The two categorical variables are independent in the population.

$H_0:$ no association (independence)

**Alternative Hypothesis:** The two categorical variables are not independent.

$H_A:$ association present

Using alpha = 0.05, interpretation matches chi-square: there is sufficient evidence of an **association** between the two categorical variables. Still describe the direction and size of the association with percentages or an odds ratio.

---

### McNemar’s test

**When:** Two **paired** binary outcomes (for example, positive/negative before and after an intervention on the same people, or matched case–control pairs). Focus is on pairs that **disagree** (changed from yes→no or no→yes).

**Assumptions:** Pairs are independent; suitable for dichotomous paired data.

**Null Hypothesis:** Among discordant pairs, the probability of changing in each direction is the same (no net change in the marginal proportions).

$H_0:$ no net change between paired conditions

**Alternative Hypothesis:** There is a net change in the proportion of “yes” responses between the two paired conditions.

$H_A:$ net change present

Using alpha = 0.05, a significant result means there is sufficient evidence of a **net change** in the proportion of “yes” responses between the two paired conditions (the changes are not balanced in both directions). This is not the same as a chi-square test on unpaired groups.

---

## Common Pitfalls to Avoid

- Using an **independent** test on **paired** data (or the reverse)  
- Running many pairwise *t*-tests across 3+ groups instead of ANOVA / Kruskal–Wallis plus proper follow-up  
- Treating a significant correlation or group difference as **proof of causation**  
- Ignoring small expected counts in a chi-square table  
- Reporting only a *p*-value without the **direction** and **magnitude** of the effect  

---

## Reminder About “Significant”

Across all of these tests, a statistically significant result means: **if the null hypothesis were true, results as extreme as yours would be uncommon**. Practical next steps are always the same:

1. State the finding in plain language for your variables.  
2. Quantify the effect (difference in means/medians, correlation, odds ratio, etc.).  
3. Respect the study design when deciding whether the finding can be interpreted causally.
