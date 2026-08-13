# Choosing Between One-Way and Two-Way ANOVA

When we want to compare means of a continuous outcome across groups, this is how I decide whether a **one-way** or **two-way** ANOVA is the right hypothesis test.

---

## What One-Way and Two-Way Mean

ANOVA (analysis of variance) compares **means** of a continuous outcome across levels of one or more **categorical factors**.

- **One-way ANOVA** uses **one** grouping variable (one factor). Example: mean bill depth across penguin species.
- **Two-way ANOVA** uses **two** grouping variables at the same time (two factors). Example: mean bill depth across species **and** sex. This lets you look at each factor’s main effect and whether the two factors **interact**.

- **Note:** “One-way” / “two-way” is **not** the same as “one-sided” / “two-sided” tests. One-sided vs two-sided is about the direction of the alternative hypothesis. One-way vs two-way is about how many categorical factors are in the ANOVA.

If you only have two groups and one factor, a two-sample *t*-test is usually enough. For help choosing among *t*-tests, ANOVA, and nonparametric options in simple bivariate settings, see [bivariate-hypothesis-test-guide.md](bivariate-hypothesis-test-guide.md).

---

## The One Question That Matters

We ask:

**Am I comparing means across levels of one grouping variable, or do I need to account for two grouping variables at once?**

- **One categorical factor** (and we are not bringing a second factor into the analysis) → **one-way ANOVA**
- **Two categorical factors** (we care about both, or about whether one effect depends on the other) → **two-way ANOVA**

If a second factor is sitting in the design—even as a “nuisance” variable we want to adjust for—ignoring it and running a one-way ANOVA on the first factor alone can give a misleading picture. In that case, I’ll usually reach for a two-way ANOVA (or another multivariable approach).

---

## Quick Decision Guide

| Situation | Use |
|---|---|
| Continuous outcome; one categorical factor with 3+ groups | One-way ANOVA |
| Continuous outcome; two categorical factors; interested in each factor and/or their interaction | Two-way ANOVA |
| Two factors present, but you mainly care about one and the second is a nuisance / design factor | Still usually two-way ANOVA (keeps both in the model) rather than dropping the second factor |
| One factor, but normality / equal-variance assumptions fail | Kruskal–Wallis (see [bivariate-hypothesis-test-guide.md](bivariate-hypothesis-test-guide.md)) |
| Only two groups on a single factor | Two-sample *t*-test (or Wilcoxon rank-sum), not ANOVA |

**Tip:** If the research question mentions “does the effect of A depend on B?” we are asking about an **interaction**, which is a two-way ANOVA question.

---

## One-Way ANOVA

**When:** For comparing a continuous outcome between 3+ groups defined by one categorical factor. Example: mean systolic BP across three diet arms, or mean bill depth across Adelie, Gentoo, and Chinstrap penguins.

**Assumptions:** Continuous dependent variable, independence of observations, normality within groups, homogeneity of variances (homoskedasticity).

**Null Hypothesis:** All group means are not statistically different from each other.

$H_0: \mu_1 = \mu_2 = \mu_3 = \cdots$

Example with species:

$H_0: \mu_{\text{Adelie}} = \mu_{\text{Gentoo}} = \mu_{\text{Chinstrap}}$

**Alternative Hypothesis:** At least one group mean is statistically different from the others.

$H_A:$ at least one $\mu$ differs

Using alpha = 0.05, a significant one-way ANOVA means there is sufficient evidence that at least one group mean is significantly different from the others. It does **not** tell you which groups differ.

Now that we know at least one group is different, we can perform a post-hoc Tukey HSD test (or another appropriate pairwise procedure) to determine which group(s) are different from each other. Report means or mean differences and confidence intervals, not only *p*-values.

- **Note:** If assumptions look poor (skewed data, unequal variances, ordinal outcome), prefer Kruskal–Wallis and an appropriate nonparametric post-hoc (for example, Dunn’s test). Details are in [bivariate-hypothesis-test-guide.md](bivariate-hypothesis-test-guide.md).

---

## Two-Way ANOVA

**When:** For comparing a continuous outcome across two categorical factors at once. Use this when you want to know whether means differ by Factor A, by Factor B, and/or whether the effect of one factor depends on the level of the other (interaction). Example: bill length by species and sex; systolic BP by treatment and sex.

**Assumptions:** Continuous dependent variable, independence of observations, approximate normality within cells (each combination of Factor A and Factor B), roughly similar variances across cells. Ideally each cell has enough observations to estimate its mean stably.

Two-way ANOVA gives you three hypothesis tests in one model:

### Main effect of Factor A

**Null Hypothesis:** Mean outcome does not differ across levels of A (averaging over B).

$H_0:$ no main effect of A

**Alternative Hypothesis:** At least one level of A has a different mean outcome (averaging over B).

$H_A:$ main effect of A is present

### Main effect of Factor B

**Null Hypothesis:** Mean outcome does not differ across levels of B (averaging over A).

$H_0:$ no main effect of B

**Alternative Hypothesis:** At least one level of B has a different mean outcome (averaging over A).

$H_A:$ main effect of B is present

### Interaction of A × B

**Null Hypothesis:** The effect of A is the same at every level of B (and vice versa).

$H_0:$ no A × B interaction

**Alternative Hypothesis:** The effect of A differs across levels of B (the factors interact).

$H_A:$ A × B interaction is present

### What “interaction” means in plain language

An **interaction** means the relationship between one factor and the outcome changes across levels of the other factor.

Example: Suppose Drug A lowers BP more than placebo in women, but not in men. Then treatment and sex interact. In that case, a single “overall” treatment effect can be misleading; you need to describe the treatment effect within each sex (simple effects), not only the main effect of treatment.

- **Note:** Check the interaction before leaning hard on main-effect interpretations. If the interaction is significant and meaningful, prioritize describing the pattern by cell or by subgroup rather than quoting one average main effect for everyone.

Using alpha = 0.05:

- **Significant main effect of A (and no meaningful interaction):** There is sufficient evidence that mean outcome differs across levels of A, averaging over B. Follow up with pairwise comparisons among A levels if A has more than two levels.
- **Significant main effect of B (and no meaningful interaction):** Same idea for Factor B.
- **Significant interaction:** There is sufficient evidence that the effect of one factor depends on the level of the other. Report the pattern with cell means, an interaction plot, or simple-effects tests. Do not stop at “the interaction *p*-value was significant.”

- **Note:** If cell sample sizes are very unequal, software may offer different types of sums of squares. For beginners, the practical takeaway is: keep cell sizes visible in your reporting, and be cautious interpreting main effects when the design is badly unbalanced and an interaction is present.

---

## A Short Worked Path

**Question:** Does mean bill length differ by penguin species? Does it also differ by sex, and does the species difference look the same in males and females?

1. Outcome = bill length (continuous).  
2. Factors of interest = species **and** sex → **two** categorical factors.  
3. Research question explicitly asks whether the species pattern depends on sex → that is an **interaction** question.  
4. I’ll choose **two-way ANOVA** with species, sex, and species × sex.  
5. Interpret in order: interaction first; then main effects if the interaction is not important; then pairwise or simple-effects follow-ups as needed.  
6. Report cell means / differences and CIs, not only which *p*-values cleared 0.05.

If the question had been only “Do species differ in mean bill length?” with no second factor in the analysis plan, **one-way ANOVA** by species would be the matching choice—and I’d stop there.

---

## Common Pitfalls to Avoid

- Running **separate one-way ANOVAs** for each factor when both factors belong in the same analysis (you miss the interaction and can mis-attribute effects)
- Interpreting **main effects** without checking whether an **interaction** is present
- Confusing **two-way ANOVA** with a **two-sample *t*-test**, or with a **two-sided** hypothesis test
- Stopping after a significant overall ANOVA (one-way or two-way) without **follow-up** comparisons or a clear description of which means differ
- Dropping a design factor (for example, sex or study site) just to force a one-way analysis when a two-way model fits the question better

---

## Reminder About “Significant”

A statistically significant ANOVA result means: **if the null hypothesis were true, results as extreme as yours would be uncommon**. Practical next steps:

1. State the finding in plain language for your factors (main effects and/or interaction).  
2. Quantify the effect (mean differences, cell means, confidence intervals).  
3. Use post-hoc or simple-effects follow-up when the overall test only tells you that “something differs.”  
4. Respect the study design when deciding whether findings can be interpreted causally.
