1-Factor Analysis of Covariance (ANCOVA)
========================================

1: Planning
-----------

1. See 1-Factor ANOVA 1: Planning
2. Attempt to ensure covariate is independent of factor levels
    - Randomizing group assignment usually suffices

2: Basic ANOVA assumption checks
--------------------------------

1. See 1-Factor ANOVA 2: Check unusual cases
2. See 1-Factor ANOVA 3: Check assumption of homoscedasticity
3. See 1-Factor ANOVA 4: Check assumption of normality

3: Check assumption of independence of covariate
------------------------------------------------

1. Test for independence of covariate
    - Run an ANOVA using the same groups with the covariate as the outcome
    - Can also run a linear regression on factor levels vs. covariate

    | p-value | Meaning                                            |
    |:------- |:-------------------------------------------------- |
    | ≤ 0.05  | Covariate is dependent on factor levels            |
    | > 0.05  | Covariate is likely not dependent on factor levels |

2. If dependence of covariate is suspected
    - Consequences:
        - Interpretation complicated
    - Solutions:
        - Bootstrap for model parameters and post hoc tests (not F)
        - Robust ANCOVA on trimmed means

4: Check assumption of homogeneity of regression slopes (crude)
---------------------------------------------------------------

1. Run linear regression within each factor level
2. Generate scatter plots with regression line for each factor
3. Inspect lines

    | Observation                        | Meaning                                 |
    |:---------------------------------- |:--------------------------------------- |
    | Lines are close to parallel        | Regression slopes are homogeneous       |
    | One or more lines are not parallel | Regression slopes are not heterogeneous |

4. If unsure if slopes are homogeneous
    - Continue analysis, test after
5. If heterogeneity of regression slopes is suspected
    - Consequences:
        - F-statistic invalid, type I error inflated, power reduced
            - Worse with unequal group sizes and when standardized regression slopes differ by more than 0.4
    - Solutions:
        - Multilevel model
        - Bootstrap CIs, model parameters, and post hoc tests (F unaffected)
        - Robust ANCOVA for trimmed means

5: Conduct ANCOVA tests
-----------------------

- See ANOVA 5: Conduct ANOVA tests for basics
    - Robust test is ANCOVA on trimmed means

6: Interpret main effects
-------------------------

- Examine F test for the covariate to determine if it significantly accounted for variance in the outcome, and the model parameter for the covariate to determine the relationship

6: Check assumption of homogeneity of regression slopes
-------------------------------------------------------

1. Recompute model with interaction term between covariate and factor

    | Interaction p-value | Meaning                                    |
    |:------------------- |:------------------------------------------ |
    | ≤ 0.05              | Regression slopes are likely heterogeneous |
    | > 0.05              | Regression slopes are likely homogeneous   |

2. If heterogeneity of regression slopes is suspected
    - See 4: Check assumption of homogeneity of regression slopes (crude)

7: Analyze factor levels
------------------------

- Contrasts and post-hoc tests are more limited

8: Calculate effect sizes
-------------------------

- Partial η2 = SSEffect / (SSEffect + SST)
    - Fraction of sample variance explained by group means excluding others
- r or ω – Effect size

    | Value | Meaning |
    |:----- |:------- |
    | 0.10  | Small   |
    | 0.30  | Medium  |
    | 0.50  | Large   |

    - Guidelines
- rContrast – Effect size for each contrast, tested with t test
    - = √(t2/(t2 + df))

9: Report results
-----------------

- “The covariate, [covariate>, was significantly related to [outcome], F([df1], [df2]) = [result], p = [p-value], r = [effect size]. There was/was not a significant effect of [independent factor> on <variable> after controlling for the effect of [covariate], F([df1], [df2]) = [result], p = [p-value], partial η2 = [effect size].”
- Planned contrasts: “Planned contrasts revealed that [levels of chunk 1] significantly changed [variable] compared to [levels of chunk 2], t([df]) = [result], p = [p-value], r = [effect size], but [level 1 of chunk 2] did not significantly change [variable] in [level 2 of chunk 2], t([df]) = [result], p = [p-value], r = [effect size].”
