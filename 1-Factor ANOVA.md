1-Factor Analysis of Variance (ANOVA)
=====================================

1: Planning
-----------

1. Plan to collect sample size sufficient for your expected effect size
    - Central limit theorem: Over 30 for normal distributions, 100 or 160 for heavy-tailed distributions, per factor level
    - Calculate power for your experimental design
2. Attempt to ensure factors are independent, as are each measurement
3. Equal group sizes are best

2: Check unusual cases
----------------------

1. Check for outliers within each factor level
    - See General Methods A: Check unusual cases
2. Consider applying correction to reduce impact of outliers
    - See General Methods D: Reduce impact of outliers

3: Check assumption of homoscedasticity
---------------------------------------

1. See General Methods B: Inspect plot of standardized residuals and predicted values
    - Linearity doesn’t apply
    - Color by group to distinguish close values
2. Use Levene’s test to test for heteroscedasticity
    - Tests null hypothesis that variances are equal
    - Equivalent to 1-way ANOVA on absolute deviations
    - Deviation from median is slightly preferable to mean (more robust)
3. Interpret Levene’s and Hartley’s Fmax

    | p-value | Meaning                                       |
    |:------- |:--------------------------------------------- |
    | ≤ 0.05  | Very likely heteroscedastic                   |
    | > 0.05  | May or may not be heteroscedastic (low power) |

    - Unequal group sizes reduces power
4. If heteroscedasticity is suspected
    - Consequences:
        - Little impact, if samples are large, group sizes are equal, and variances proportional to means
        - CIs and significance tests invalid
    - Solutions:
        - Apply corrected F
            - Brown-Forsythe F
            - Welch’s F
            - Can always apply, as correction will do nothing if no heteroscedasticity
        - Bootstrap parameter estimates
            - No effect on F
        - Use robust variant
        - Consider transformation (not ideal)
            - See General Methods C: Transform data

4: Check assumption of normality
--------------------------------

1. See General Methods E: Check for normality of residuals
    - Within each factor level
2. If nonnormality is suspected and central limit theorem cannot be invoked
    - Consequences:
        - CIs and significance tests invalid
    - Solutions:
        - Collect more data to invoke central limit theorem
        - Multilevel model
        - Use robust variant

5: Conduct ANOVA tests
----------------------

- Regular
- Brown-Forsythe F
    - Weights variances by group size, reducing impact of larger groups
- Welch’s F
    - Weights by group sizes and group variance
- Bootstrapped CIs
    - No effect on F test, improves CIs, contrasts, post hoc tests
- Robust
    - Bootstrapped and means trimmed ANOVA 

6: Interpret effect
-------------------

- Examine F-test

    | p-value | Meaning                              |
    |:------- |:------------------------------------ |
    | ≤ 0.05  | Outcome differs among levels         |
    | > 0.05  | Outcome likely the same among levels |

7: Analyze factor levels
------------------------

- If you have a specific hypothesis: Planned contrasts
    - Split data into recursive nested sets of 2 chunks of factor levels, weight so that each involved factor level counts as 1, with opposed groups negative.
    - Can decide to reuse contrast, but this increases Type I error
    - Different contrasts are available for different hypotheses
        - E.g. compare adjacent categories, polynomial contrasts / trend analysis
- If you do not have a specific hypothesis: Posthoc tests
    - Less power due to multiple comparisons
    - Robust to small deviations from normality
    - If you are certain of homoscedasticity
        - And have equal group sizes
            - REGWQ – Best, good power and control of Type I error
            - Tukey HSD – Good power and control of Type I error, more powerful with larger number of comparisons
            - Bonferroni – Guaranteed control of Type I error, more powerful with smaller number of comparisons
        - And have slight group size differences
            - Gabriel’s
        - And have large group size differences
            - Hochberg’s GT2
    - If heteroscedasticity is suspected
        - Games-Howell
            - May always try in addition if uncertain.
    - If robust ANOVA used
        - Use bundled posthoc test

8: Calculate effect sizes
-------------------------

- η2 = SSM / SST (same as R2)
    - Fraction of sample variance explained by group means
- Adjusted for population: ω2 = (SSM – (dfM)MSR) / (SST + MSR)
    - Fraction of population variance likely explained by group means
    
    | Value | Meaning |
    |:----- |:------- |
    | 0.01  | Small   |
    | 0.06  | Medium  |
    | 0.14  | Large   |

    - Guidelines
- r or ω – Comparable to regression r
- rContrast – Effect size for each contrast, tested with t test
    - = √(t2/(t2 + df))

9: Report Results
-----------------

- “There was/was not a significant effect of <independent factor> on [variable>, F([df1], [df2]) = [result], p = [p-value], ω = [effect size].”
- Linear contrast: “There was a significant linear trend F([df1], [df2]) = [result], p = [p-value], ω = [effect size].”
- Planned contrasts: “Planned contrasts revealed that [levels of chunk 1] significantly changed [variable] compared to [levels of chunk 2], t([df]) = [result], p = [p-value], r = [effect size], but [level 1 of chunk 2] did not significantly change [variable] in [level 2 of chunk 2], t([df]) = [result], p = [p-value], r = [effect size].”
