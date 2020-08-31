Logistic Regression
===================

Probability of categorical outcomes or proportion outcomes

**Incomplete**

1: Planning
-----------

1. Plan to collect sample size sufficient for your expected effect size and number of predictors
    - Central limit theorem: Over 30 for normal distributions, 100 or 160 for heavy-tailed distributions
    - Calculate power for your experimental design
    - Sample size guidelines for linear models for 80% power:
        - (same as for linear? not sure)
2. Choose variables that have some direct relationship with the outcome and include all the variables that may have such a relationship
    - Correlated external variables complicate interpretation
3. Attempt to ensure factors are independent, and at least not completely redundant
4. Ensure that data from all combinations of factor levels are collected and in similar amounts
5. Evaluate variable relationships for model entry
    - Hierarchical preferred, order chosen by user based on existing theory
    - Simultaneous (forced entry) if order unknown
    - Do not do stepwise (backwards slightly better)
6. If you have enough data, split your data into halves (or e.g. 80%/20%) randomly for cross-validation
    - Training set should be larger part

2: Check for incomplete information
-----------------------------------

1. Generate a contingency table of the expected and observed frequencies
2. Ensure that they all have at least 1 observation each
3. Ensure that no more than 20% have less than 5 observations
4. May also show up as extremely large standard errors for coefficients
5. If information is incomplete
    - Consequences:
        - Goodness-of-fit tests invalid
    - Solutions:
        - Collect more data

3: Check for complete/perfect separation
----------------------------------------

1. Examine to see if one variable or combination of variables can perfectly predict the outcomes
2. If there is perfect separation
    - Consequences:
        - Regression cannot determine correct slope
    - Solutions:
        - Collect more data to find the overlapping area
        - Rejoice; you didn’t actually need logistic regression

4: Check for overdispersion
---------------------------

1. Calculate dispersion statistic φ = goodness-of-fit χ2 / df

    | Value | Meaning                               |
    |:----- |:------------------------------------- |
    | > 1   | Overdispersion present                |
    | ≳ 2   | Overdispersion likely a problem       |
    | < 1   | Underdispersion present (less common) |

2.	Calculate deviance dispersion statistic = deviance goodness-of-fit χ2 / df

    | Observation                                        | Meaning                                  |
    |:-------------------------------------------------- |:---------------------------------------- |
    | Dispersion and deviance statistics very discrepant | Overdispersion likely present            |
    | Dispersion and deviance statistics similar         | Overdispersion may or may not be present |

3.	If overdispersion is suspected
    - Consequences:
        - Standard errors, CIs, and test statistics invalid
    - Solutions:
        - Apply correction
            - Multiply SEs by the square root of the larger of the two statistics

5: Run regression model
-----------------------

- Build parsimonious model
    - Not good for hypothesis testing, but okay for exploratory
- Beware models that fail to converge
    - Can increase iterations or loosen convergence criteria

6: Check assumption of linearity of the logit
---------------------------------------------

1. Take the natural log of each predictor
2. Rerun regression including as factors the interaction of the predictor and its log
3. Inspect significance of the log-predictor interactions

    | Observation | Meaning                            |
    |:----------- |:---------------------------------- |
    | Any > 0.05  | Assumption invalid for that factor |
    | All < 0.05  | Assumption valid                   |

4. If nonlinearity of the logit is suspected
    - Consequences:
        - ?
    - Solutions:
        - ?

7: Check assumption of non-multicolinearity (for 2 or more predictors)
----------------------------------------------------------------------

1. Run linear regression with the same outcome and predictors
2. See Linear Regression 7: Check assumption of non-multicolinearity (for 2 or more predictors)
