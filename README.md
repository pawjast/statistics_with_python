# statistics_with_python

## TODO:

[ ] Create a notebook showing how Q-Q plot looks for various distributions.


## Inferencial statistics

### Typical workflow:

#### 1. Define the question

All analysis starts with a solid scientific or business reason.

> Has new algorithm improved accuracy?

> Is the test score different between regions?

> Is there a relationship between A and B?


#### 2. Define a hypothesis.

Formulate $H_0$.

> No effect. No difference. No relationship. They're the same.

Formulate $H_1$.

Choose significance level $\alpha$. Typical value: `0.05`.

> Interpretation:
> 
> If p < 0.05 → reject H₀  
> If p ≥ 0.05 → fail to reject H₀

Choose statistical power $1 - \beta$.

Run power analysis to determine in the sample size is enough to detect the meaningful effect.

Decide if the test is to be *one-sided* or *two-sided* **before** looking at the data.


#### 3. Explore the data.

Check for:
* missing data
* outliers
* shape of distribution
* any potential data errors


#### 4. Choose a test.

Match your test to your data types, distributions, and experimental design:

**Parametric Tests:**  
(e.g., Independent samples $t$-test, Paired $t$-test, ANOVA, Pearson correlation) require assumptions like normality, homogeneity of variance, and continuous data.

**Non-Parametric Tests:**  
(e.g., Mann-Whitney $U$, Wilcoxon signed-rank, Kruskal-Wallis, Spearman correlation) are used when assumptions of normality are violated or data is ordinal.

**Categorical Tests:**  
(e.g., Chi-square test of independence, Fisher's exact test) for proportions and frequency counts.


#### 5. Check assumptions.

It's often an iterative process bewtween exploring the data, checking assumptions and deciding on the test to choose.


#### 6. Calculate a test statistic and p-value.

#### 7. Compute effect size and confidence intervals.

#### 8. Interpret results.


## Glossary

### Significance level (alpha)

Alpha is the probability of rejecting the null hypothesis when it is actually true.

Alpha is a probability of commiting Type I error (false positive).

Typical values:
* `0.01` (1%)
* `0.05` (5%)
* `0.10` (10%)

**Interpretation**

I accept 5% chance I might reject the null hypothesis when it's true.


### Hypothesis test

The hypothesis test generally asks:

> "If the null hypothesis were true, how surprising would my observed data be?"

The process is always:

* State hypotheses
* Calculate a test statistic from the sample
* Determine how unusual that statistic is under H₀
* Convert that into a p-value (or compare with a critical value)
* Reject or fail to reject H₀


### Test statistics

They answer a general question of:

> "How many standard-error units away from the null hypothesis value am I?"

For the normal distirbution we've got *z-score*:

$$
z = \frac{x - \mu}{\sigma}
$$

And *z-score* of 1 means:

"We're one population standard deviation away from the mean."

Standard deviation is the *standard error unit*.

For a t-distribution, we've got a *t-score*:

$$
t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}
$$

Here the deviation from the mean is not measured in the units of the standard deviation of the data.

The deviation is measured in the units of the *standard error of the sample mean*:

$$
SE = \frac{s}{\sqrt{n}}
$$

And *t-score* of 1 means:

"The sample mean is 1 standard error away from the hypothesized mean."

The hypothesis formulation involving the t-score asks the question of:

> "How unusual is the observed sample mean $H_0$​ is true??"


#### Generalization

It can be generalized that test statistics describes:

$$
\text{Test Statistic}
=
\frac{\text{Signal}}
{\text{Noise}}
$$

Where:

* `Signal`: how far your estimate is from what $H_0$​ predicts
* `Noise`: uncertainty in the estimate

For distributions like normal or t-distribution, this can be written as:

$$
\text{Test Statistic}
=
\frac{\text{Estimate} - \text{Null Value}}
{\text{Estimated Standard Error}}
$$

But in other cases the formula take slightly different generic form.

F-distribution:

$$
\text{Test Statistic}
=
\frac{\text{Explained variability}}
{\text{Unexplained variability}}
$$

Chi-square:

$$
\text{Test Statistic}
=
\sum
\frac
{
(\text{Observed}-\text{Expected})^2
}
{
\text{Expected}
}
$$


### Statistical power

Statistial power is the probability that your test will correctly detect a real effect when one actually exists.

In other words, it is the likelihood of rejecting the null hypothesis (saying "yes, there is an effect") when the null hypothesis is genuinely false.


## A/B test

WIP


## Bootstrapping

WIP


## Before analysis

### Checking assumptions of normality of data

Many statistical tests assume the data is *normally* distributed.

These tests include:

* t-tests
* ANOVA
* Linear regression model residuals

The common ways to check the normality of data are:

* To plot the histogram and KDE plot to check the distribution of the data
* Plot the Q-Q plot
* Run test:
  * Shapiro-Wilk test
  * Anderson-Darling test
  * D'Agostino-Pearson test

> H0: Data comes from a normal distribution  
> H1: Data does not come from a normal distribution

**❗Note:** It's a good practice to combine visual check with empirical test.

**Shapiro-Wilk test**

* Test statistics: `W`
  * `W` ranges between `0` and `1`
  * `W = 1`: data fits normal distribution
  * `W = 0`: data deviates from normal distribution significantly

* It works only with continous data and to detect normality of data
* With small number of samples the test might fail to detect obvious non-normality (which will be clearly visible in Q-Q plot).

**Anderson-Darling test**

Alternatively, we can use Anderson-Darling test. It's often preferred over Shapiro-Wilk when you care about the tails of the distribution.

* Test statistics: `A^2`
  * `low A^2`: data fits the target distribution
  * `high A^2`: data deviates from the target distribution

It's more sensitive to:

* Outliers
* Heavy tails
* Tail deviations

This is especially relevant in applications where extreme values are important e.g.:

* Fraud Detection
* Anomaly detection

In those cases extreme values are more important than the central values.

Also, Anderson-Darling test can be used to detect various distributions, not just the normal distribution.

It can assess fit to:

* Normal
* Exponential
* Weibull
* Logistic
* Gumbel

**D'Agostino-Pearson normality test**

It checks if:

> skewness ≈ 0  
> kurtosis ≈ 3

Generally, checking `skewness` and `kurtosis` of data is also useful.

It works best for moderate to large sample sizes and is often used when Shapiro-Wilk becomes overly sensitive or computationally less suitable for very large datasets.

**RULE OF THUMB**

> Samples < 50

* QQ plot
* Shapiro Test

> Samples < 5000

* Q-Q plot
* Shapiro-Wilk or D'Agostino-Pearson

If tail behaviour is especially important:

* Anderson-Darling

> Samples > 5000

* Q-Q plot
* Skewness and kurtosis
* Focus on practical significance rather than formal normality tests

**❗Note:** Don't obsess with normality.

With enough observations, almost every dataset will fail a significance test as tests become hyper sensitive to tiny deviations from the normality.

That's why it's important to combine statistical test with visual confirmation and eventually make a judgement call.

Instead:

* inspect Q-Q plot
* inspect skewness/kurtosis

And then:

> Decide whether deviations are practically important❗

Also many parametric tests are fairly robust to moderate departures from normality. E.g. for t-tests or ANOVA:

```text
n < 20     ->  normality matters a lot
  = 20-50  ->  check carefully
  > 50     ->  usually not a major concern
  > 100    ->  often largely irrelevant
```


## Test types

### One sample t-test

**Application**

Used when you have a single sample of independent observations on a continuous variable and want to determine whether the population mean differs from a known or hypothesized value.

**Assumptions**

* The variable being measured should be continuous (or approximately continuous).
* The population should be approximately normally distributed, particularly for small sample sizes.
* Observations MUST be independent
  * ✅ 5 different parts measured
  * ❌ the same part measured 5 times
* Minimum 2 observations required (but the statitical power is going to be very low)

**Test statistics**

$$
t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}
$$

Where:

* $\bar{x}$: sample mean
* $\mu_0$: Hypothesized population mean under $H_0$
* $s$: sample standard deviation
* $n$: sample size
* $t$: test statistic

The *t-statistic* is compared against a Student's t-distribution with degrees of freedom: $df = n - 1$.

**Test workflow**

* Calculate test statistics: `t`
* Calculate the critical value from Student's t-distribution using `alpha`, `n` (actually `df`) and whether the test is one sided or two sided
* compare `t` vs `critical value`
  * Two-sided test: reject H₀ if $|t| > t_{critical}$
  * Right-tailed test: reject H₀ if $t > t_{critical}$
  * Left-tailed test: reject H₀ if $t < -t_{critical}$

Or:

* Calculate `p-value` for the obtained test statistics: `t`
* Compare `p-value` with `alpha`:
* if $p_{value} < α$ then reject H₀ 


**Examples**

* Check if this school's average score different from the national average of 70?
* Check if the average load time for a new page differs from a historic value of 2s?
* Check if the fuel consuption differs from the average of 45MPG as advertised by the manufacturer?
* Check if the battery life time is indeed 1000hrs as per manufacturer's claim?