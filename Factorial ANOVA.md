Factorial ANOVA
===============

1: Planning
-----------

- See 1-Factor ANOVA 1: Planning

2: Basic ANOVA assumption checks
--------------------------------

1. See 1-Factor ANOVA 2: Check unusual cases
2. See 1-Factor ANOVA 3: Check assumption of homoscedasticity
3. See 1-Factor ANOVA 4: Check assumption of normality

3: Conduct ANOVA tests
----------------------

- See 1-Factor ANOVA 5: Conduct ANOVA tests for basics
    - Robust variant for trimmed means available

4: Check presence of interaction
--------------------------------

1. Examine the F-test for the interaction term
2. Generate interaction graphs and inspect for presence and size of interaction.

    | Obseration                                      | Meaning                         |
    |:----------------------------------------------- |-------------------------------- |
    | Lines are parallel, points evenly spaced        | No interaction                  |
    | Lines cross, space between points widely differ | Significant interaction present |

3. If a non-trivial interaction is present
    - Consequences:
        - Cannot interpret main effects
    - Solutions
        - Simple effects analysis to analyze within one factor within levels of the other
4. If no interaction or trivial interaction is present
    - Interpret main effects

5: Interpret main effects
-------------------------

- Examine the F-test for the main effects
    - F = MSM / MSR
    - Welch’s can be done but it is not trivial, so would need to do robust test.
    - Bootstrapping
        - Doesn’t affect F, does improve CIs, contrasts, post hoc tests
    - Because the error term is reused for all effects, type I error rate is not well-controlled.
    - Ignore any effects that don’t test your substantive hypothesis, or use Bonferroni correction (divide by number of factors reusing the error term).

6: Analyze factor levels
------------------------

- Simple effects
    - Analyze one factor within levels of the other
    - F = MSM,Level / MSR, where MSR is the original error term, and MSM¬,Level is the MS based on the mean within the level of the first factor.
- Planned contrasts and post hoc tests for main effects
    - Only need for a factor if more than two levels
    - See 1-Factor ANOVA 7: Analyze factor levels
- Planned contrasts for interactions
    - Determine first-level contrast coefficients for comparing one factor, then divide by the level of the other factor to get the interaction contrast codes
    - Not entirely sure

7: Calculate effect sizes
-------------------------

- Main effects
    - Variance components
        - σ ̂_α^2=(a-1)(〖MS〗_A-〖MS〗_R )/nab
        - σ ̂_β^2=(b-1)(〖MS〗_B-〖MS〗_R )/nab
        - σ ̂_αβ^2=(a-1)(b-1)(〖MS〗_(A×B)-〖MS〗_R )/nab
        - σ ̂_total^2=σ ̂_α^2+σ ̂_β^2+σ ̂_αβ^2+〖MS〗_R
    - ω_A^2=(σ ̂_α^2)/(σ ̂_total^2 )
        - Fraction of sample variance explained by group means
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

8: Report results
-----------------
- "There was a significant main effect of [factor] on [outcome], F([df1], [df2]) = [result], p = [p-value], ω2 = [effect size]. Bonferroni post hoc tests revealed that [outcome] was significantly higher at [factor A level 1] than at [factor A level 2] (p = [p-value]). [outcome] was not significantly different at [factor A level 3] than at [factor A level 1] (p = [p-value]) or at [factor A level 2] compared with [factor A level 1] (p = [p-value]).”
- “[factor B level 1] [outcome] was significantly higher than [factor B level 2], F([df1], [df2]) = [result], p = [p-value], ω2 = [effect size].”
- “There was a significant interaction between [factor A] and [factor B], F([df1], [df2]) = [result], p = [p-value], ω2 = [effect size]. This effect indicates that [outcome] of [factor B] were affected differently by [factor A]. Simple effects analysis revealed that [outcome] of [factor B level 1] were significantly higher than [factor B level 2] in [factor A level 1], F([df1], [df2]) = [result], p = [p-value], and in [factor A level 2], F([df1], [df2]) = [result], p = [p-value], but not in [factor A level 3], F([df1], [df2]) = [result], p = [p-value].
