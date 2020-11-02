# Cheat Sheet
Test of Proportions
| Samples | Response Categories | Tests                                               |
| ------- | ------------------- | --------------------------------------------------- |
| 1       | 2                   | One-sample $\chi^2$ test, binomial test             |
| 1       | >2                  | One-sample $\chi^2$ test, multinomial test          |
| >1      | >=2                 | N-sample $\chi^2$ test, G-test, Fisher's exact test |

Analyses of Variance
Factors| Levels| B_W | Parametric Tests | Nonparametric Tests
-|-|-|-|-
1|2|B|Independent-sample t-test (Welch's t-test if unequal variance)|Mann-Whitney U test
1|>2|B|One-way ANOVA (F test)|Kruskal-Wallis test

# Pearson's Chi-squared Test
It tests a null hypothesis stating that the frequency distribution of certain events observed in a sample is consistent with a particular theoretical distribution. The events considered must be mutually exclusive and have total probability 1. ([example](https://sphweb.bumc.bu.edu/otlt/mph-modules/bs/bs704_hypothesistesting-chisquare/bs704_hypothesistesting-chisquare_print.html))
## Tests for Two or More Independent Samples, Discrete Outcome
- step 1: set up hypotheses and determine the level of significance
    - $H_0$: The distribution of the outcome is independent of the groups.
    - $H_a$: there is a difference in the distribution of responses to the outcome variable among the comparison groups.
- step 2: select the appropriate test statistic
    - $$\chi^2=\sum\dfrac{(O-E)^2}{E}$$
    - $$df=(r-1)(c-1)$$
    - Notation: O: observed frequency E: expected frequency df: degree of freedom r: # rows c: # columns
    - The condition for appropriate use of the above test statistic is that each expected frequency is at least 5
- step 3: set up decision rule
get the critical value
- step 4: compute the test statistic
expected cell frequency = (row total * column total) / N
- step 5: conclusion
# p-value
* statistically significant: <0.05, <0.01, <0.001, <0.0001
* "trend": 0.05-0.1 not statistically significant but may be of interest
* non-significant ($n.s.$): >0.05 do not report

# Exact Test and Asymptotic Test
* exact: give exact p-value e.g. binomial test, multinomial test, fisher's test
* asymptotic: give approxiamating p-value, better when sample size gets larger (>1000) e.g. chi-suqared test, g test(increasingly being used where chi-squared tests were previously recommended)

# Type I Error & Type II Error
## Type I Error
A type 1 error is also known as a false positive and occurs when a researcher incorrectly rejects a true null hypothesis. The probability of making a type I error is represented by your alpha level (α), which is the p-value below which you reject the null hypothesis.

You can reduce your risk of committing a type I error by using a lower value for p. However, using a lower value for alpha means that you will be less likely to detect a true difference if one really exists (thus risking a type II error).

## Type II Error
A type II error is also known as a false negative and occurs when a researcher fails to reject a null hypothesis which is really false.

The probability of making a type II error is called Beta (β), and this is related to the power of the statistical test (power = 1- β). You can decrease your risk of committing a type II error by ensuring your test has enough power.

# Bonferroni Correction ([video](https://www.youtube.com/watch?v=rMuNniCTsOw))
An ajustment applied to p-values that is "supposed to be" applied, when two or more statistical analysis have been performed on the same sample of data. This is because the familywise type I error rate is known to be larger than the per analysis error rate.

$$ \alpha_{FW} = 1 - (1-\alpha_{PC})^c $$

Benferroni correction: Divide the per analysis $\alpha$ rate by the number of statistical analysis performed. $e.g.\ .05/3=.017$

## Holm-Bonferroni ([example](https://www.statisticshowto.com/holm-bonferroni-method/))
Order the p-value from smallest to greatest, apply the formula foe every test, stop when the first non-rejected hypothesis is reached.
$$ \alpha_{k} = \dfrac{\alpha}{m + 1 - k} $$
k denotes the ranking

# Fisher's Exact Test ([example](https://mathworld.wolfram.com/FishersExactTest.html))
Exhaustive calculation, often used in small samples.
$$N=\sum_iR_i=\sum_jC_j$$
$$P_{cutoff}=\dfrac{(R_1\,!R2\,!\ldots R_m\,!)(C_1\,!C2\,!\ldots C_n\,!)}{N\,!\prod_{i,j}a_{ij}\,!}$$
All possible combintions sum to 1. The values that are less than the cutoff value sum to p-value (sum of the possibilities of all things equally rare, or rarer).

# Z Test
For a sample of $N >= 100$, our binomial distribution is virtually identical to a normal distribution. This is caused by the central limit theorem.
Advantages:
* We can always use a 2-sided z-test. However, a binomial test is always 1-sided unless $P_0 = 0.5$.
* A z-test allows us to compute a confidence interval for our sample proportion.
* We can easily estimate statistical power for a z-test but not for a binomial test.
* A z-test is computationally less heavy, especially for larger sample sizes.

# Between-Subjects & Within-Subjects
Between subjects factor: One for which only each subject experiences only one value or level of that factor.
Within subjects factor: Only need to be exposed to more than one level of the factor. (partial or fully)

# t-test
Limited to two categories.
## Independent t-test
Equal variance t-test
$$t=\dfrac{\overline{X_1}-\overline{X_2}}{s_p\sqrt{\dfrac{1}{n_1}+\dfrac{1}{n_2}}}$$
$$s_p=\sqrt{\dfrac{(n_1-1)s_1^2+(n_2-1)s_2^2}{n_1+n_2-2}}$$
$$df=n_1+n_2-2$$
## Welch's t-test
Unequal variances t-test
$$t=\dfrac{\overline{X_1}-\overline{X_2}}{\sqrt{\dfrac{S_1^2}{n_1}+\dfrac{S_2^2}{n_2}}}$$
$$df=n_1+n_2-2$$
## Mann-Whitney U test ([example](youtube.com/watch?v=nRAAAp1Bgnw))
Takes ranking. Nonparametirc analyses.

# Three ANOVA Assumption
ANOVA stands for analyses of variants. Many parametric tests requires these assumptions be met.
- Independence
  - Each subject is sampled independently of every other subject. Also means that measures on a subject are independent of measures on every other subject.
  - It doesn't mean in a within subject studies that measures on the same subject are independent because obviously they're not. That's also called repeated measures.
- Normality
  - It isn't actually the response that has to be normally distributed to meet this assumption, it's actually the normality of the residuals that matter. Residuals are differences between your observed data, the response that you measure, and your statistical models predictions. (In R, aov: fitting linear models; fitdistr(..., "lognormal"): fitting in lognormal models)
  - If the residuals are normally distributed means there's no systematic effects going on that you're not taking into account in your statistical model. The intuition is that if there's something going on that's systematic, there may be a variable you're missing, or some other effect that you're not sure of, perhaps this idea of a hidden effect you haven't taken into account. So we want to see that the residuals are normally distributed to meet the ANOVA assumption.
  - However, there are some advantages to look into the distribution of the response variable.
    - Understanding your response and the shape it takes is important in building intuition about your data. Some models do care about the response $e.g.$ Poisson distribution
    - If you do in practice have normally distributed responses, your most likely to be able to fall the normality assumption with your residuals.
  - Common distributions
    - Normal distribution ($\mu,\sigma^2$)
    - Lognormal distribution ($\mu,\sigma^2$) $e.g.$ task time
      - take the logarithm of the data, it would become normal
    - Exponential distribution ($\lambda$) $e.g.$ wealth
    - Gamma distribution ($k$(shape parameter),$\theta$(scale parameter)) $e.g.$ queue waiting time, stress-testung time until failure
      - exponential is a special case of a gamma distribution when $k=1$ and $\beta=1/\theta$, inverse scale parameter, aka rate parameter
      - $\mu=\alpha/\beta$
      - $$f(x\mid\alpha,\beta)=\dfrac{\beta^\alpha x^{\alpha-1}e^{-\beta x}}{\Gamma(\alpha)} \ for \ x>0,\ \alpha,\beta>0$$
    - Poisson distribution ($\lambda$) (discrete) $e.g.$ rare event count
    - Binomial / Multinomial distribution ($n,p$) (discrete)
- Homoscedasticity
  - Homogeneity of variance

# Parametric Analyses & Nonparametirc Analyses
- Parametric analyses
  - Have to comply with certain assumptions that we want to be aware of
  - Gain power
  - There's been a lot longer history of statistical research and analysis on parametric models versus nonparametrics.
- Nonparametirc Analyses
  - Converting your data into ranks first, second, third, fourth, fifth, and so on and then analyzing those ranks in various ways.
  - Don't make underlying, distributional assumptions
  - Often lose power. They're often a little less powerful and sometimes less versatile.

# Shapiro–Wilk Test ([video](https://www.youtube.com/watch?v=dRAqSsgkCUc))
Tests the null hypothesis that a sample comes from a normally distributed population.
$$W=\dfrac{(\sum_{i=0}^na_ix_{(i)})^2}{\sum_{i=0}^n(x_i-\overline{x})^2}$$
Cautions:
- Can encounter problems with many equal values
- Rarely reject $H_0$ at small n
- Reject $H_0$ for tiny differences from normality when n is large
- Shapiro-wilk test is too sensitive. You should use histogram/Q-Q plot when assessing ANOVA assumption

# Kolmogorov–Smirnov Test
K–S test or KS test is a nonparametric test of the equality of continuous or discontinuous, one-dimensional probability distributions that can be used to compare a sample with a reference probability distribution (one-sample K–S test), or to compare two samples (two-sample K–S test).
The Kolmogorov–Smirnov statistic quantifies a distance between the empirical distribution function of the sample and the cumulative distribution function of the reference distribution, or between the empirical distribution functions of two samples.
$$D_n=\sup_x \left|F_n(x)-F(x)\right|$$

# Levene's Test
Levene's test uses arithmetic mean, Brown-Forsythe test uses median. B-f test is more robust.

- \>2 samples, normal data: Levene's test

- 2 or >2 samples, non-normal data: Levene's test better for symmetrical but heavy-tailed distributions; B-f better for skewed

