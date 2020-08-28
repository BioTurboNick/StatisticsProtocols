General Methods
===============

These are general methods that re-appear in different types of analyses.

Check unusual cases
-------------------

Data should be examined for points that do not conform with the rest. Outliers contribute error to the analysis and can overly influence the result.

1.	Generate boxplots of each predictor and outcome to identify presence of outliers
    - If ANOVA, do within each combination of factor levels
    - Many boxplots do show outliers, but some may not.
2.	Convert values to z-scores and assess how many absolute values are beyond these thresholds:

    | Z-score	| % expected if normal | Meaning           |
    |:------- |:-------------------- |:----------------- |
    | 1.96	  |  5%	                 | Potential outlier |
    | 2.58	  |  1%	                 | Probable outlier  |
    | 3.29	  | ~0%	                 | Extreme           |

    - Also look at values just before threshold to avoid threshold effect
    - If more in each category than expected in a normal distribution, likely have outliers

3.	Assess reason for any outliers and decide how to act

    | Cause                        | Action                                         |
    |:---------------------------- |:---------------------------------------------- |
    | Data entry error             | Correct if certain of real value, else exclude |
    | Measurement error	           | Exclude                                        |
    | Sample from wrong population | Exclude                                        |
    | Uncertain to any degree	     | Keep but make note of and discuss              |

    - If conducting ANOVA, beware removing a data point if it creates an unequal group size, as this makes the standard tests more dependent on the assumption of normality.
    - Removing points also reduces degrees of freedom and thus reduces power. Trade off of loss of power and decreased error.

Inspect plot of standardized residuals and predicted values
-----------------------------------------------------------

Data should be examined for relationships between the residuals and predicted values to detect heteroscedasticity (and linearity, for linear regression).
1.	Convert predictors and residuals to z-scores
2.	Generate scatter plot of standardized predictors and z-scores (i.e. Zresid/Zpred plot)
3.	Inspect scatterplot pattern

    | Pattern              | Interpretation                |
    |:-------------------- |:----------------------------- |
    | Square	             | Linear and homoscedastic      |
    | Triangle/funnel	     | Linear and heteroscedastic    |
    | Split uniform funnel | Nonlinear and homoscedastic   |
    | Split varying funnel | Nonlinear and heteroscedastic |

    - Might be able to spot non-independence, but better to use test

Transform data
--------------

Adjusting the data can make an unusual distribution more normal, correct for nonlinearity, and reduce impact of outliers.

| Transformation      | Can help                     | Function                                                   |
|:------------------- |:---------------------------- |:---------------------------------------------------------- |
| Log                 | Exponential relationship     | log(Xi); if 0s: log(Xi + 1); if (-)s: log(Xi + 1 + min(X)) |
|                     | Positive skew                |                                                            |
|                     | Positive kurtosis            |                                                            |
|                     | Heteroscedasticity           |                                                            |
| Square root         | Quadratic relationship       | √(Xi); if (-)s: √(Xi + min(X))                             |
|                     | Positive skew                |                                                            |
|                     | Positive kurtosis            |                                                            |
|                     | Heteroscedasticity           |                                                            |
| Reciprocal          | Positive skew                | 1/(max(X) - Xi)                                            |
|                     | Positive kurtosis            |                                                            |
|                     | Heteroscedasticity           |                                                            |
| Other               | Other nonlinear relationship | varies                                                     |
| Reverse score <any> | Negative skew                | Xi,inv = max(X) - Xi; func(Xi,inv)                         |

- If the same variable is collected at different levels and you intend to compare them, must transform the variable for all levels.
- Be careful: an inappropriate transformation can make things worse than not transforming at all
- Reverse the transformation when interpreting downstream statistics.

Reducing impact of outliers
---------------------------

Options for making your data more robust to the presence of outliers:
| Method Name   | Action	                                                                                                       | Rules                                                            |
|:------------- |:-------------------------------------------------------------------------------------------------------------- |:---------------------------------------------------------------- |
| Trim          | Remove extreme observations                                                                                    | 5/10/20% from each end; >2 or 3 SD                               |
| Windsorize    | Replace extreme values with boundary value or inferred value (Xinferred = (z * s) + mean(X))                   | 5/10/20% of each end; >2 or 3 SD |
| Robust method |	Special version of statistical test, may use bootstrapping (sampling from your sample) or may use trimmed mean |	                                                                |
| Transform     | See C: Transform data                                                                                          |                                                                  |

- Be careful if combining these methods
    - E.g. robust methods may trim data, and you don’t want to trim twice.

Check for normality of residuals
--------------------------------

1.	Generate histogram (+ density) plot, P-P or Q-Q plot of standardized residuals
    - Q-Q plot shows fewer points, easier to interpret with lots of data
2.	Inspect plots for normal distribution
    - Histogram/density – deviations from bell-shape, symmetrical
        - Easy to misjudge, so rely more on P-P/Q-Q plot
    - P-P/Q-Q plot – deviations from the diagonal
        - Curve across – skew
        - S shape – kurtosis
        - Tails matter more than center
3.	Calculate and interpret standardized skewness and kurtosis statistics using their respective standard errors

    | Z-score | p-value |
    |:------- |:------- |
    | 1.96    | 0.05    |
    | 2.58    | 0.01    |
    | 3.29    | 0.001   |

4.	For small samples (below CLT level), run Shapiro-Wilk test

    | p-value | Meaning                              |
    |:------- |:------------------------------------ |
    | < 0.05  | Very likely not normal               |
    | > 0.05  | May or may not be normal (low power) |

    - Shapiro-Wilk has more power than Kolmogorov-Smirnov, but not as good in certain situations
5.	If central limit theorem can be invoked, can ignore
    - N ≥ 30 if not heavy-tailed (leptokurtic, highly skewed)
    - N ≥ 100 or 160 if heavy-tailed
