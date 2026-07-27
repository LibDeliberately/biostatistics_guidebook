# Choosing a Hypothesis Test for Simple Bivariate Analyses

This guide helps you pick an appropriate statistical test when you have **two variables** and want to ask whether they are related or whether groups differ. It is written for people who are new to choosing tests: start with the decision steps below, then read the short section for the test you land on.

---

## Before You Choose a Test

**Bivariate** means you are looking at the relationship between two variables at a time (for example, treatment group and blood pressure, or smoking status and disease).

Ask yourself three questions:

1. **What is my outcome (the thing I care about measuring)?**  
   Is it continuous (numbers like age, BMI, blood pressure) or categorical (categories like yes/no, mild/moderate/severe)?

2. **What is my predictor / grouping variable?**  
   Is it also continuous, or is it categorical (groups like drug vs. placebo, or male vs. female)?

3. **Are my observations independent or paired?**  
   - **Independent**: each person (or unit) appears in only one group.  
   - **Paired / matched**: the same person is measured twice (before/after), or people are matched in pairs.

Also remember:

- A **significant result** (*p* < your chosen α, often 0.05) means the data are unlikely under the null hypothesis. It does **not** by itself prove cause and effect.
- Always check whether your data roughly meet the test’s **assumptions**. If they do not, use the nonparametric alternative listed below, or transform / use a different method.
- Report the **effect size** and/or a **confidence interval**, not only the *p*-value.

---

## Quick Decision Guide

Use this table to find a starting point. Then read that test’s section for requirements, assumptions, and how to interpret a significant result.

| Outcome variable | Predictor / comparison | Relationship of observations | Usual first choice | Common alternative if assumptions fail |
|---|---|---|---|---|
| Continuous | Two independent groups | Independent | Two-sample *t*-test | Wilcoxon rank-sum (Mann–Whitney) |
| Continuous | Same subjects measured twice, or matched pairs | Paired | Paired *t*-test | Wilcoxon signed-rank |
| Continuous | Three or more independent groups | Independent | One-way ANOVA | Kruskal–Wallis |
| Continuous | Another continuous variable | Independent pairs of measurements | Pearson correlation (or simple linear regression) | Spearman correlation |
| Binary / categorical | Another categorical variable | Independent | Chi-square test of independence | Fisher’s exact test (small samples) |
| Binary (yes/no) | Same subjects measured twice (or matched pairs) | Paired | McNemar’s test | Exact McNemar / related exact methods |

**Tip:** If you are unsure whether a continuous outcome is “normal enough,” look at histograms or Q–Q plots by group, and consider whether sample sizes are large. When in doubt for small samples with skewed data, the nonparametric option is often safer.

---

## Continuous Outcome, Two Independent Groups

### Two-sample (independent) *t*-test

**When to use it**  
Compare the **mean** of a continuous outcome between **two separate groups** (for example, mean systolic BP in drug vs. placebo).

**Requirements**  
- One continuous outcome  
- One binary grouping variable (exactly two groups)  
- Each observation belongs to only one group  

**Assumptions**  
- Observations are independent within and between groups  
- The outcome is approximately normally distributed **in each group** (less critical with larger samples)  
- The two groups have roughly similar variances (use Welch’s *t*-test if variances differ; it is a common default)  

**If significant, what can you say?**  
There is evidence that the **population means differ** between the two groups. Say *how much* they differ (mean difference and confidence interval). Do not claim the grouping variable *caused* the difference unless the study design supports causal inference (for example, a randomized trial).

---

### Wilcoxon rank-sum test (also called Mann–Whitney *U* test)

**When to use it**  
Same setup as the two-sample *t*-test, but the outcome is skewed, has outliers, or is better thought of as ordered ranks than as a normal mean.

**Requirements**  
- Continuous or ordinal outcome  
- Two independent groups  

**Assumptions**  
- Observations are independent  
- Under the usual interpretation, the two groups have similarly shaped distributions (then a significant result points to a shift in location, often summarized with medians)  

**If significant, what can you say?**  
There is evidence that the **distributions differ** between groups—commonly that one group tends to have higher values than the other. Prefer talking about **medians** or ranks rather than means unless you have checked that means are still meaningful.

---

## Continuous Outcome, Paired or Matched Data

### Paired *t*-test

**When to use it**  
Compare two related continuous measurements on the **same subjects** (before vs. after) or on **matched pairs**.

**Requirements**  
- Two continuous measurements that form natural pairs  
- You analyze the **differences** within pairs  

**Assumptions**  
- Pairs are independent of other pairs  
- The **within-pair differences** are approximately normally distributed  

**If significant, what can you say?**  
There is evidence that the **mean difference** within pairs is not zero (for example, scores changed from baseline to follow-up). Report the mean change and its confidence interval.

---

### Wilcoxon signed-rank test

**When to use it**  
Paired continuous (or ordinal) data when the paired differences are skewed or not approximately normal.

**Requirements**  
- Paired measurements  
- You can rank the absolute differences  

**Assumptions**  
- Pairs are independent  
- Differences are symmetric around their median (for the standard interpretation)  

**If significant, what can you say?**  
There is evidence of a **systematic change** between the paired measurements (one condition tends to produce higher values than the other). Summarize with the median difference when possible.

---

## Continuous Outcome, Three or More Independent Groups

### One-way ANOVA

**When to use it**  
Compare **means** of a continuous outcome across **three or more** independent groups (for example, three diet arms).

**Requirements**  
- Continuous outcome  
- One categorical grouping variable with 3+ levels  
- Independent observations  

**Assumptions**  
- Independence of observations  
- Approximate normality of the outcome within each group  
- Similar variances across groups (homogeneity of variance)  

**If significant, what can you say?**  
There is evidence that **not all group means are equal**—at least one group mean differs from another. ANOVA alone does **not** tell you *which* groups differ. Use planned contrasts or adjusted pairwise comparisons (for example, Tukey) for that follow-up question.

---

### Kruskal–Wallis test

**When to use it**  
Same setup as one-way ANOVA when normality or equal-variance assumptions are doubtful, or when the outcome is ordinal.

**Requirements**  
- Continuous or ordinal outcome  
- Three or more independent groups  

**Assumptions**  
- Independent observations  
- Similar distribution shapes across groups if you want to interpret the result mainly as a difference in medians / location  

**If significant, what can you say?**  
There is evidence that **at least one group’s distribution differs** from the others (often, values tend to be higher in one group). Follow up with pairwise nonparametric comparisons if you need to know which groups differ.

---

## Two Continuous Variables

### Pearson correlation

**When to use it**  
Measure the strength of a **linear** association between two continuous variables (for example, age and cholesterol).

**Requirements**  
- Two continuous variables measured on the same observations  

**Assumptions**  
- Pairs of observations are independent  
- The relationship is roughly **linear**  
- Both variables are approximately bivariate normal (or residuals behave reasonably); sensitive to outliers  

**If significant, what can you say?**  
There is evidence of a **nonzero linear correlation**. The correlation coefficient *r* tells direction (positive/negative) and strength (closer to ±1 is stronger). Correlation is **not** causation, and it does not describe curved relationships well.

---

### Spearman correlation

**When to use it**  
Assess a **monotonic** association (as one variable goes up, the other tends to go up or down, not necessarily in a straight line), or when data are ordinal / non-normal / have outliers.

**Requirements**  
- Two continuous or ordinal variables  

**Assumptions**  
- Independent pairs of observations  
- The association, if present, is monotonic (consistently increasing or decreasing)  

**If significant, what can you say?**  
There is evidence of a **monotonic association** between the variables. Interpret the Spearman coefficient similarly to Pearson for direction and strength, but remember it is based on **ranks**, not raw linear slope.

---

### Simple linear regression (one predictor)

**When to use it**  
When you want to **predict** or **estimate the average change** in a continuous outcome for a one-unit change in a continuous predictor. Closely related to Pearson correlation when there is one continuous predictor.

**Requirements**  
- Continuous outcome  
- One predictor (continuous, or a binary predictor coded 0/1)  

**Assumptions** (check residuals)  
- Linear relationship between predictor and mean outcome  
- Independent observations  
- Roughly constant variance of residuals (homoscedasticity)  
- Residuals approximately normal (mainly for inference in smaller samples)  

**If the predictor’s coefficient is significant, what can you say?**  
There is evidence that the **slope is not zero**: the average outcome changes as the predictor changes. Report the estimated slope and confidence interval. Again, significance alone does not establish causality.

---

## Two Categorical Variables

### Chi-square test of independence

**When to use it**  
Test whether two categorical variables are associated in a contingency table (for example, exposure yes/no vs. disease yes/no, or treatment arm vs. response category).

**Requirements**  
- Two categorical variables  
- Independent observations (each subject contributes to one cell)  
- Usually a 2×2 or larger table  

**Assumptions**  
- Independence of observations  
- Expected cell counts are large enough (a common rule of thumb: most expected counts ≥ 5; no expected count too small)  

**If significant, what can you say?**  
There is evidence that the two variables are **not independent**—the distribution of one variable differs across levels of the other. Inspect percentages (and risk ratios / odds ratios in 2×2 tables) to describe **how** they are associated.

---

### Fisher’s exact test

**When to use it**  
Same question as the chi-square test, especially for **small samples** or tables with small expected cell counts (very common in 2×2 tables).

**Requirements**  
- Two categorical variables in a contingency table  
- Independent observations  

**Assumptions**  
- Independence of observations  
- In the classic 2×2 version, row and column totals are treated as fixed (exact enumeration of tables)  

**If significant, what can you say?**  
Same interpretation as chi-square: evidence of an **association** between the two categorical variables. Still describe the direction and size of the association with percentages or an odds ratio.

---

### McNemar’s test

**When to use it**  
Two **paired** binary outcomes (for example, positive/negative before and after an intervention on the same people, or matched case–control pairs).

**Requirements**  
- Binary outcome measured twice on the same subject, or matched pairs  
- Focus is on pairs that **disagree** (changed from yes→no or no→yes)  

**Assumptions**  
- Pairs are independent  
- Suitable for dichotomous paired data  

**If significant, what can you say?**  
There is evidence of a **net change** in the proportion of “yes” responses between the two paired conditions (the changes are not balanced in both directions). This is not the same as a chi-square test on unpaired groups.

---

## A Short Worked Path (Example)

**Question:** Do patients on Drug A have different mean LDL cholesterol than patients on Drug B?

1. Outcome = LDL (continuous). Predictor = drug (two groups).  
2. Patients are in only one arm → **independent**.  
3. Check normality / outliers in each arm.  
4. If reasonable → **two-sample *t*-test** (often Welch’s).  
5. If skewed / small *n* with outliers → **Wilcoxon rank-sum**.  
6. If significant → report that mean (or median) LDL differs between drugs, with the size of the difference and CI—not just “*p* < 0.05.”

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
