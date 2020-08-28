Linear Regression
=================

1: Planning
-----------

1. Plan to collect sample size sufficient for your expected effect size and number of predictors
    - Central limit theorem: Over 30 for normal distributions, 100 or 160 for heavy-tailed distributions
    - Calculate power for your experimental design
    - Sample size guidelines for linear models for 80% power:

    | Predictors         | 1   | 2   | 3   | 4   | 5   | 6   | 10  |  20  |
    |:------------------ | ---:| ---:| ---:| ---:| ---:| ---:| ---:| ----:|
    | Small (R2 = 0.02)  | 387 | 476 | 539 | 590 | 635 | 667 | 806 | 1043 |
    | Medium (R2 = 0.13) |  55 |  68 |  77 |  85 |  92 |  98 | 119 |  157 |
    | Large (R2 = 0.26)  |  25 |  31 |  36 |  40 |  43 |  46 |  55 |   77 |

2. Choose variables that have some direct relationship with the outcome and include all the variables that may have such a relationship
     - Correlated external variables complicate interpretation
3. Attempt to ensure factors are independent, and at least not completely redundant
4. Evaluate variable relationships for model entry
    - Hierarchical preferred, order chosen by user based on existing theory
    - Simultaneous (forced entry) if order unknown
    - Do not do stepwise (backwards slightly better)
5. If you have enough data, split your data into halves (or e.g. 80%/20%) randomly for cross-validation
    - Training set should be larger part

2: Check assumption of linearity (crude) and unusual cases
----------------------------------------------------------

1. Check for unusual values within each variable
    - See General Methods: Check unusual cases
2. Generate scatterplots of each predictor vs. outcome
3. Inspect scatterplots for linearity
    - Not useful for multivariate linearity for more than 2 predictors. Need other methods.
4. If relationship appears nonlinear, consider a transformation and apply it
    - See General Methods: Transform data
5. Inspect (transformed) scatterplot for outliers
6. Make decisions about outliers
    - See General Methods: Check unusual cases

3: Run regression model
-----------------------

- Regular
- Robust confidence intervals and significance tests of model parameters
    - Bootstrap (Bias corrected and accelerated)
    - Can skip checks for homoscedasticity, normality; effect of outliers reduced
- Standard errors for heteroscedastic residuals for regression
    - E.g. SPSS PROCESS tool 
    - Can skip checks for homoscedasticity
- Robust model parameters
    - Iteratively reweighted least squares (IRLS) method
        
4: Check assumption of independence
-----------------------------------

1. Use Durbin-Watson test for independence
     - Tests if adjacent residuals have correlated errors

    | Score   | Meaning              |
    |:------- |--------------------- |
    | < 1.5   | Positive correlation |
    | 1.5-2.5 | No correlation       |
    | > 2.5   | Negative correlation |

2. If residuals aren’t independent:
    - Consequences:
        - CIs and significance tests invalid
        - Model parameters valid but suboptimal
    - Solutions:
        - Multi-level model
3. If residuals are independent, okay to continue

5: Check assumptions of homoscedasticity and linearity
------------------------------------------------------

1. See General Methods: Inspect plot of standardized residuals and predicted values
2. (QQ/PP plot?)
3. If heteroscedasticity is suspected
    - Consequences:
        - CIs and significance tests invalid
        - Model parameters valid but suboptimal
    - Solutions:
        - Weighted least squares regression
            - Weighted by a function of variance
        - Bootstrap CIs for regression
        - Apply a transformation
            - See General Methods: Transform data (not preferred)
4. If nonlinearity is suspected
    - Consequences:
        - Model invalid
    - Solutions:
        - Multilevel model
        - Apply a transformation
            - See General Methods: Transform data

6: Check assumption of normality
--------------------------------

1. See General Methods: Check for normality of residuals
2. If nonnormality is suspected and central limit theorem cannot be invoked
    - Consequences:
        - CIs and significance tests invalid
        - Model parameters valid but suboptimal
    - Solutions:
        - Collect more data to invoke central limit theorem
        - Multilevel model
        - Bootstrap CIs for regression

7: Check assumption of non-multicolinearity (if 2 or more predictors)
---------------------------------------------------------------------

1. Generate correlation matrix for all predictors
2. Inspect correlation matrix for r values over 0.8 or 0.9
3. Calculate and inspect multicollinearity diagnostics
    - Variance inflation factor (VIF) and tolerance (1/VIF)
        - Indicates strong linear relationship with other predictors

    | VIF                                              | Tolerance | Meaning                  |
    |:------------------------------------------------ |:--------- |:------------------------ |
    | Average (VIF / k) >> 1, k = number of predictors | n/a	     | Regression may be biased |
    | > 5                                              | < 0.2     | Potential problem        |
    | > 10                                             | < 0.1     | Serious problem          |

   - Eigenvalues and variance proportions
        - Indicator of orthogonality
        - In the absence of multicollinearity, each predictor’s variance will only be associated with one eigenvalue
        - If multiple predictors contribute significant variance to the small eigenvalues, this indicates the predictors are colinear
4. If high degree of multicollinearity is suspected
   - Consequences:
        - Untrustworthy model parameters
        - Size of R limited
        - Hard to interpret the contributions of colinear predictors
   - Solutions
        - Omit one of the variables
            - Renders theoretical conclusions meaningless b/c the variables are interchangeable
            - If you do this, best to add another non-collinear variable
        - Collect more data
            - Collinearity may have been incidental to the sample
        - If 3 or more colinear
            - Principle component analysis, replace variables with the component scores
        - Don’t do anything, acknowledge model’s unreliability (safest)

8: Check for influential cases
------------------------------

1. Re-run regression model with each point excluded to calculate and inspect diagnostics
   - Adjusted predicted value: The predicted outcome value at the predictor values of the excluded point
   - Deleted residual: Adjusted predicted value – observed value
   - Studentized deleted residual: deleted residual / standard error
   - Cook’s distance
        - Accounts for how well the case-deleted model fits remaining points
        - Values > 1 may be a concern
   - Leverage (or hat values)
        - Gauge of influence of observed outcome over the predicted values
        - Average is (k + 1) / n, k = number of predictors (normal influence)
        - Maximum is (N – 1) / N, but may show as 1 (complete influence)
        - Investigate cases > 2 or 3 times the average leverage
   - Mahalanobis distances
        - Related to leverage
        - Distance of cases from mean(s) of the predictor(s)
        - Chi-square distribution, df = number of predictors
        - Critical value for chi-square as cutoff to identify cases to investigate
   - Standardized DFBeta
        - Difference between parameter value with and without the case, converted to z-score
        - Values above 1 indicate a problem
   - Standardized DFFit
        - Difference between predicted outcome with and without the case, converted to z-score
        - Values above 1 indicate a problem
   - Covariance Ratio (CVR)
        - Complicated stat that quantifies the degree to which a case influences the variance of the regression parameters
        - Threshold 1 + [3(k + 1) / n]
            - Over this value means deleting the point harms precision of some model parameters
            - Under this value means deleting the point improves precision of some model parameters
2. Decide how to handle influential cases
   - Remove points that severely violate diagnostics
        - DO NOT inspect significance values for model parameters when making decision
        - Hesitate before removing outliers that have small influence
   - Consider a correction method
        - See General Methods D: Reduce impact of outliers
3. Make note of removed values for further investigation, discussion.

9: Assess model fit
-------------------

1. Examine R
   - Pearson’s correlation coefficient; estimate of overall fit
   - Generally, ±0.1 small, ±0.3 medium, ±0.5 large
2. Examine R2
   - Fraction of variance in the data explained by the model
   - Equivalent to SSM / SST
3. Examine F-tests (ANOVA)
   - Is the model significantly different from no model (mean)?
   - F = MSM / MSR = (N – k – 1) R2 / k(1 – R2)
   
    | p-value | Meaning                                    |
    |:------- |:------------------------------------------ |
    | ≤ 0.05  | Model fits better than original            |
    | > 0.05  | Model doesn’t fit any better than original |

4. If predictors were entered hierarchically, examine R, R2, and ANOVA comparing each new model to the old model 
   - Each level should pass the F test and explain substantially more variance than the last.
5. Examine model parameter T-tests
   - Is the coefficient significantly different from 0?
   - t =  bx / SEbx

    | p-value | Meaning                             |
    |:------- |:----------------------------------- |
    | ≤ 0.05  | Model parameter contributes         |
    | > 0.05  | Model parameter does not contribute |

       - If you decide not to accept it, rerun regression without the variable (forced to 0)
   - Intercept (b0): the expected outcome when all predictors are 0.
   - Each coefficient (b1…): The amount the outcome changes with a unit change in this predictor.

10: Cross-validate
------------------

1. If multiple predictors, note Adjusted R2
   - Reduces R2 based on sample size and number of predictors
   - Gives idea of how model generalizes to the population
   - R2adj = 1 – [((n-1)/(n-k-1))((n-2)/(n-k-2))((n+1)/n)](1 – R2) – Stein’s formula
   - Beware using different formula (Wherry’s) which doesn’t help predict different samples
2. If data was split, use model against test set
3. If significant loss of predictive power seen
    - Consequences:
        - Model does not generalize
    - Solutions:
        - Do robust linear regression
            - If find similar values, can stick with standard regression
            - If values are very different, rely on robust results

11: Apply model
---------------

- Enter various predictor values to obtain a predicted outcome value for that situation

12: Report Model
----------------

- Summary table
    - Model coefficients
    - Confidence interval
    - Standard errors
    - Standardized coefficient (beta)
    - t-test p-value
    - Include each level if hierarchical
