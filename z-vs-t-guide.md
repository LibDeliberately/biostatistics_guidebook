# Choosing Between a *z*-Test and a *t*-Test

This guide helps you decide whether a **z-test** or a **t-test** is the right reference distribution when you are doing hypothesis testing for a mean (and, briefly, for a proportion).

---

## What *z* and *t* Are

Statisticians use *z* and *t* as **standardized test statistics**. You turn a sample result (a mean, a difference in means, a proportion) into a number that says how many **standard errors** you are from the null value. Then you compare that number to a known distribution to get a *p*-value or decide whether it clears a critical value.

- ***z*** refers to the **standard normal** distribution. You use it when the sampling variability is treated as **known**. Classic case: testing a mean when the population standard deviation σ is known. Large-sample tests for proportions also use *z*.
- ***t*** refers to **Student’s *t* distribution**, which depends on **degrees of freedom**. You use it when variability is **estimated from the sample** (you plug in *s* instead of σ). The *t* distribution has heavier tails than the normal, especially with small samples. As *n* gets large, *t* looks almost the same as *z*.

In software and papers, you usually see the test statistic (*z* or *t*), the degrees of freedom when it is a *t*-test, and the *p*-value. The logic underneath is the same: is this sample result surprising under the null?

---

## The One Question That Matters

For tests about **means**, ask:

**Do I know the population standard deviation σ, or only the sample standard deviation *s*?**

- **σ known** → *z*-test  
- **σ unknown** (you estimate it with *s*) → *t*-test  

In practice, σ is almost never known from real data. So for means, the default is a *t*-test.

---

## Quick Decision Guide

| Situation | Use |
|---|---|
| Mean(s); population σ known | *z*-test |
| Mean(s); σ unknown (use sample *s*) | *t*-test |
| Large *n*, but σ still unknown | Still *t* (answers will be close to *z*, but *t* is the right procedure) |
| Proportion; large sample | *z*-test (normal approximation) |
| Small *n*, skewed continuous outcome | Prefer a nonparametric alternative (see [bivariate-hypothesis-test-guide.md](bivariate-hypothesis-test-guide.md)) |

**Tip:** A large sample does **not** turn a mean test with unknown σ into a *z*-test. It just makes *t* and *z* give similar answers. Use *t* anyway.

---

## Why *t* Exists

When you replace σ with *s*, you add extra uncertainty. The *t* distribution accounts for that. With small degrees of freedom, critical values are larger (wider intervals, harder to reject the null) than the corresponding *z* cutoffs. With large *n*, that extra uncertainty fades and *t* ≈ *z*.

---

## One-Sample *z*-Test (Mean)

**When to use it**  
Compare a sample mean to a hypothesized value (for example, mean systolic BP vs. a known population target) when the **population** standard deviation σ is known.

**Requirements**  
- One continuous outcome  
- A hypothesized mean under the null  
- Known population σ  

**Assumptions**  
- Observations are independent  
- The outcome is approximately normal, or *n* is large enough for the sampling distribution of the mean to be roughly normal  

**If significant, what can you say?**  
There is evidence that the **population mean** differs from the hypothesized value. Report the sample mean, the difference from the null value, and a confidence interval. Do not claim a cause unless the study design supports that.

---

## One-Sample *t*-Test (Mean)

**When to use it**  
Same setup as the one-sample *z*-test, but σ is **unknown** and you estimate it with the sample SD *s*. This is the usual case.

**Requirements**  
- One continuous outcome  
- A hypothesized mean under the null  
- Sample SD used in place of σ  

**Assumptions**  
- Observations are independent  
- The outcome is approximately normal, or *n* is large enough for the sampling distribution of the mean to be roughly normal  

**If significant, what can you say?**  
Same interpretation as the one-sample *z*-test: evidence that the population mean differs from the hypothesized value. Report the mean difference and its confidence interval (the interval will use *t* critical values).

---

## Two-Sample and Paired Mean Tests

The same rule carries over:

- **Two independent groups** (mean BP in drug vs. placebo): use a two-sample *t*-test when σ is unknown (almost always). A two-sample *z*-test would require known population SDs.
- **Paired or matched data** (before vs. after on the same people): use a paired *t*-test on the differences when the SD of the differences is estimated from the sample.

For help choosing between independent, paired, ANOVA, and nonparametric options, see [bivariate-hypothesis-test-guide.md](bivariate-hypothesis-test-guide.md).

---

## Proportions Use *z* (Large Samples)

Tests and confidence intervals for a **proportion** (or a difference in proportions) commonly use a *z* (normal) approximation when the sample is large enough that expected counts are not too small. That is a different setup from testing a **mean** with unknown σ. Do not treat “we used *z*” for a proportion as a reason to use *z* for means when you only have *s*.

---

## Common Pitfalls to Avoid

- Using a *z*-test for a mean just because *n* is “large,” while still estimating σ with *s*  
- Treating the sample SD as if it were the known population σ  
- Forgetting that two-sample and paired mean comparisons also default to *t* when SDs are estimated  
- Mixing up mean tests (*t* by default) with large-sample proportion tests (*z*)  
- Reporting only a *p*-value without the **direction** and **size** of the effect  

---

## Reminder About “Significant”

A statistically significant result means: **if the null hypothesis were true, results as extreme as yours would be uncommon**. Practical next steps:

1. State the finding in plain language for your variables.  
2. Quantify the effect (mean difference and confidence interval, or proportion and CI).  
3. Respect the study design when deciding whether the finding can be interpreted causally.
