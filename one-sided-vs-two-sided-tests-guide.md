# Choosing Between One-Sided and Two-Sided Tests

This guide helps you decide whether a **one-sided** or **two-sided** alternative hypothesis is the right choice for a hypothesis test. This is about the **direction** of $H_A$, not which test family to use (*t*-test, ANOVA, chi-square, and so on).

For choosing the test itself, see [bivariate-hypothesis-test-guide.md](bivariate-hypothesis-test-guide.md) and [z-vs-t-guide.md](z-vs-t-guide.md). For one-way vs two-way ANOVA (a different naming scheme), see [one-way-vs-two-way-anova-guide.md](one-way-vs-two-way-anova-guide.md).

---

## What One-Sided and Two-Sided Mean

After you pick a test, you still have to state the alternative hypothesis. That alternative can look in **both directions** or in **only one**.

- **Two-sided** (also called two-tailed): you care about a difference in **either** direction. Example: mean BP on Drug A differs from mean BP on placebo, higher or lower.
- **One-sided** (also called one-tailed): you care about a difference in **only one** pre-specified direction. Example: mean BP on Drug A is **lower** than on placebo (you are not treating “higher” as support for your scientific claim in this test).

- **Note:** “One-sided” / “two-sided” is **not** the same as “one-way” / “two-way” ANOVA, and not the same as “one-sample” / “two-sample” tests. Sidedness is only about the direction of $H_A$.

Most software and journals default to **two-sided** tests unless you clearly justify a one-sided alternative ahead of time.

---

## The One Question That Matters

Ask **before looking at the results**:

**Would a difference in either direction matter for my research question, or only a difference in one direction?**

- Either direction would change the conclusion → **two-sided**
- Only one direction is scientifically of interest, and that direction was chosen **a priori** → **one-sided**
- Unsure, exploratory, or both directions would be interesting → **two-sided**

If you find yourself choosing the side after seeing which way the estimate went, that is a sign to stay two-sided.

---

## Quick Decision Guide

| Situation | Use |
|---|---|
| A difference up or down (or positive or negative association) would both matter | Two-sided |
| Only an increase (or only a decrease) is of interest, and the direction was pre-specified | One-sided |
| Exploratory analysis; no strong directional claim | Two-sided |
| You already saw the data and now want the “easier” *p*-value | Stay two-sided (do not switch after the fact) |
| Default in most papers / software when sidedness is not justified | Two-sided |

**Tip:** “I expect the new treatment to be better” is not always enough by itself. Ask whether an effect in the **opposite** direction would still be scientifically important to detect and report. If yes, use two-sided.

---

## Two-Sided Tests

**When:** For testing whether a parameter differs from a null value in **either** direction. This is the usual choice for comparing two group means, testing a correlation, or asking whether two proportions differ without a one-direction-only claim.

**Null Hypothesis:** No difference (or no association) under the null value.

$H_0: \mu_1 - \mu_2 = 0$

**Alternative Hypothesis:** The difference is not zero—it could be positive or negative.

$H_A: \mu_1 - \mu_2 \ne 0$

Using alpha = 0.05, a significant two-sided test means there is sufficient evidence that the parameter differs from the null value in **some** direction. You still need to look at the estimate (and CI) to say whether the sample went up or down.

- **Note:** A two-sided test with α = 0.05 splits the rejection region across both tails (commonly 0.025 in each tail for symmetric tests). Extreme results in either direction can lead to rejection of $H_0$.

---

## One-Sided Tests

**When:** For testing a difference in **only one** direction that was justified and chosen **before** seeing the results. Example: a new antihypertensive is of interest only if it **lowers** systolic BP relative to control; or a screening tool is of interest only if sensitivity is **greater than** a benchmark.

### Greater-than form

**Null Hypothesis:** The parameter is less than or equal to the null value (often written as equality at the boundary).

$H_0: \mu_1 - \mu_2 = 0$

**Alternative Hypothesis:** The difference is greater than zero.

$H_A: \mu_1 - \mu_2 > 0$

### Less-than form

**Null Hypothesis:** The parameter is greater than or equal to the null value (again often written as equality at the boundary).

$H_0: \mu_1 - \mu_2 = 0$

**Alternative Hypothesis:** The difference is less than zero.

$H_A: \mu_1 - \mu_2 < 0$

Using alpha = 0.05, a significant one-sided test means there is sufficient evidence of an effect **in the pre-specified direction**. An effect of the same size in the opposite direction would **not** count as support for this $H_A$.

- **Note:** Always state which direction you used. “We used a one-sided test” is incomplete without “greater than” or “less than.”

---

## How Sidedness Changes the *p*-Value

For many common tests (for example, a *t*-test), the software computes the same test statistic either way. What changes is **how that statistic is turned into a *p*-value** and where the critical cutoff sits.

- In a **two-sided** test, both extreme high and extreme low values of the statistic count against $H_0$.
- In a **one-sided** test, only extremes in the **chosen** direction count against $H_0$.

That is why, for a result that already points in your predicted direction, the one-sided *p*-value is often about **half** the two-sided *p*-value (for symmetric tests). That smaller *p*-value is **not** free evidence—you paid for it by giving up the ability to reject $H_0$ for effects in the opposite direction.

- **Note:** Do not take a two-sided *p*-value from output, halve it, and call that a planned one-sided test unless a one-sided alternative was truly pre-specified. If the estimate went the “wrong” way, halving is especially inappropriate.

---

## A Short Worked Path

**Question A:** Does a new drug lower mean systolic BP compared with placebo?

1. Only a decrease is of clinical interest for this claim; an increase would not support adopting the drug for BP lowering.  
2. Direction is chosen **before** analysis: drug mean − placebo mean $< 0$ (or placebo − drug $> 0$, depending on coding).  
3. Choose a **one-sided** *t*-test (assuming that test’s other assumptions are met).  
4. If significant at α = 0.05, there is sufficient evidence that mean systolic BP is lower on the drug than on placebo. Report the mean difference and CI as well.  
5. If the drug’s mean is higher, you do **not** treat that as a significant finding under this one-sided $H_A$—you report the estimate and stay consistent with the pre-specified direction.

**Question B:** Do two diets differ in mean systolic BP?

1. Either higher or lower mean BP on Diet A vs Diet B would matter.  
2. Choose a **two-sided** test.  
3. $H_0: \mu_A - \mu_B = 0$; $H_A: \mu_A - \mu_B \ne 0$.  
4. If significant, there is sufficient evidence that the diet means differ; use the estimate to say which diet was higher.

---

## Common Pitfalls to Avoid

- Choosing one-sided vs two-sided **after** seeing which way the data went  
- Halving a two-sided *p*-value after the fact to “get under 0.05”  
- Using a one-sided test mainly to make a borderline result look significant  
- Confusing **one-sided / two-sided** with **one-way / two-way** ANOVA, or with **one-sample / two-sample** tests  
- Reporting a one-sided test without stating the **direction** of $H_A$  
- Ignoring an effect in the opposite direction when a one-sided test was used—still describe what the data showed, even if it does not reject that one-sided null

---

## Reminder About “Significant”

A statistically significant result means: **if the null hypothesis were true, results as extreme as yours (in the sense defined by your $H_A$) would be uncommon**. Practical next steps:

1. State the finding in plain language, including **direction** when you used a one-sided test.  
2. Quantify the effect (estimate and confidence interval), not only the *p*-value.  
3. Be honest about whether sidedness was pre-specified.  
4. Respect the study design when deciding whether findings can be interpreted causally.
