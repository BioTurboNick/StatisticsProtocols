Multilevel Model
================

Allows variability in regression slopes to be modeled. Allows dependence between observations to be modeled. Does not require complete data (though still strive to minimize missing data). Extremely complex and kind of confusing. Beware.

**Incomplete**

1: Planning
-----------

- Consider or plan for factors that may lead to correlations between measurements and make them a higher level in hierarchy
- Identify which factors are random effects or fixed effects
    - Fixed effects are only valid within similar conditions
        - Predictors usually considered as this
        - Means all possible factor levels of interest are included
    - Random effects are generalizable, assuming they are representative
        - Could consider predictors as random samplings from distribution
        - Model coefficients are allowed to vary for each identical value of the predictor
            - Random intercept is simplest – allows a different baseline value for the factor level
            - Random slopes – allows a different slope value for the factor level
                - Usually coupled with random intercepts
            - Done by adding a adding a term to each fixed intercept/slope to account for the variability in the factor

2: Check assumption of linearity (crude) and unusual cases
----------------------------------------------------------

1. Check for unusual values within each variable and factor level
    - See General Methods A: Check unusual cases
2. Generate scatterplots of each predictor vs. outcome
3. Inspect scatterplots for linearity
    - Not useful for multivariate linearity for more than 2 predictors. Need other methods.
4. If relationship appears nonlinear, consider a transformation and apply it
    - See General Methods C: Transform data
5. Inspect (transformed) scatterplot for outliers
6. Make decisions about outliers
    - See General Methods A: Check unusual cases

3: Measure intraclass correlation
---------------------------------

1. For each hierarchy level, measure the intraclass correlation.

    | Observation  | Meaning                                       |
    |:------------ |:--------------------------------------------- |
    | ICC is small | Little variation due to the grouping variable |
    | ICC is large | Large variation due to the grouping variable  |

2.	If ICC is small, may not need grouping variable

4: Run Multilevel Linear Regression
-----------------------------------
