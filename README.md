# statistics_with_python

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


## Before analysis

### Checking assumptions for normality

Many statistical tests assume the data is *normally* distributed.

These tests include:

* t-tests
* ANOVA
* Linear regression model residuals

The common ways to check for normality are:

* To plot the histogram and KDE plot to check the distribution of the data
* Plot the Q-Q plot
* Run Shapiro-Wilk test

> H0: Data comes from a normal distribution  
> H1: Data is not normally distributed

We usually combine the plotting with the test.

Regarding the Shapiro-Wilk test:

* With small number of samples the test might fail to detect obvious non-normality (which will be clearly visible in Q-Q plot).

Alternatively, we can use Anderson-Darling test. It's often preferred over Shapiro-Wilk when you care about the tails of the distribution.

It's more sensitive to:

* outliers
* heavy tails
* tail deviations

Other tests:

* D'Agostino-Pearson Normality Test

> It checks if:
> 
> skewness ≈ 0  
> kurtosis ≈ 3

Generally, checking `skewness` and `kurtosis` of data is also useful.

**RULE OF THUMB**

> Samples < 50

* QQ plot
* Shapiro Test

> Samples < 5000

* QQ plot
* D'Agostino-Pearson

> Samples > 5000

Don't obsess with normality.

With enough observations, almost every dataset will fail a significance test as tests become hyper sensitive to tiny devations from the normality.

That's why it's important to combine statistical test with visual confirmation and eventually make a judgement call.

Instead:

* inspect Q-Q plot
* inspect skewness/kurtosis
* decide whether deviations are practically important

Also many parametric tests are fairly robust to moderate departures from normality. E.g. for t-tests or ANOVA:

```text
n < 20    -> normality matters a lot
20-50     -> check carefully
> 50      -> usually not a major concern
> 100     -> often largely irrelevant
```
