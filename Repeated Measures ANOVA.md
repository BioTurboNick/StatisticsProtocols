Repeated Measures ANOVA
=======================

1: Planning
-----------

1. See 1-Factor ANOVA 1: Planning
2. Collect all factor levels from each individual

2: Basic ANOVA assumption checks
--------------------------------

- See 1-Factor ANOVA 2: Check unusual cases
- See 1-Factor ANOVA 3: Check assumption of homoscedasticity
- See 1-Factor ANOVA 4: Check assumption of normality

3: Check assumption of sphericity
---------------------------------

1. If only 2 conditions, can ignore
2. Use Mauchly’s test

    | p-value | Meaning                                 |
    |:------- |:--------------------------------------- |
    | ≤ 0.05  | Very likely aspherical                  |
    | > 0.05  | May or may not be spherical (low power) |

3. Examine Greenhouse-Geisser estimate ε ̂ and Huynh-Feldt estimate ε ̃
    - GG varies between 1/(k – 1) and 1
        - k = # of repeated measures conditions
    - Lower is worse
4. If sphericity is suspected
    - Consequences:
        - Statistical tests invalid for even small departures
    - Solutions:
        - Bonferroni post-hoc test
        - Apply correction
            - If GG > 0.75, use HF correction to df for related F tests
            - If GG < 0.75 or have no knowledge, use GG correction to df for related F tests
            - May also average GG and HF, or average the p-values from each
        - Multilevel model
        - Multivariate ANOVA (MANOVA)
            - Trade off in power

4: Conduct ANOVA tests
----------------------

- See 1-Factor ANOVA 5: Conduct ANOVA tests for basics
    - Between-participant variation removed before considering model and error
    - Robust variant for trimmed means available

6: Interpret main effects
-------------------------

- Examine the F-test for the main effects
    - F = MSM / MSR
    - Brown-Forsythe F
        - Weights variances by group size, reducing impact of larger groups
    - Welch’s F
        - Weights by group sizes and group variance
    - Bootstraping
        - Doesn’t affect F, does improve CIs, contrasts, post hoc tests
    - Because the error term is reused for all effects, type I error rate is not well-controlled.
    - Ignore any effects that don’t test your substantive hypothesis, or use Bonferroni correction (divide by number of factors reusing the error term).

7: Analyze factor levels
------------------------

- Simple effects
    - Analyze one factor within levels of the other
    - F = MSM,Level / MSR, where MSR is the original error term, and MSM¬,Level is the MS based on the mean within the level of the first factor.
- Planned contrasts and post hoc tests for main effects
    - Only need for a factor if more than two levels
    - See ANOVA 7: Analyze factor levels
- Planned contrasts for interactions
    - Determine first-level contrast coefficients for comparing one factor, then divide by the level of the other factor to get the interaction contrast codes
    - Not entirely sure

8: Calculate effect sizes
-------------------------

- Main effects
    - ω^2=[(k-1)/nk (〖MS〗_M-〖MS〗_R )]/(〖MS〗_R+□((〖MS〗_B-〖MS〗_R)/k)+[(k-1)/nk (〖MS〗_M-〖MS〗_R )] ), where MSB is between-subjects variation
    - r or ω – Effect size

        | Value | Meaning |
        |:----- |:------- |
        | 0.10  | Small   |
        | 0.30  | Medium  |
        | 0.50  | Large   |

        - Guidelines
    - rContrast – Effect size for each covariate or contrast, tested with t test
        - = √(t2/(t2 + df))
- Simple effects
    - r=√(□(F(1,〖df〗_R )/(F(1,〖df〗_R )+〖df〗_R ))) 

9: Report results
-----------------

- "The Greenhouse-Geisser estimate of the departure from sphericity was ε = [value]. The [outcome] was not significantly affected by [factor], F([df1], [df2]) = [result], p = [p-value],  ω2 = [effect size].
- If multivariate, report Pillai’s trace, V, and associated F/dfs.
