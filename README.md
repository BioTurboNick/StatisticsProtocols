# Statistics Protocols
A manual for working through statistical analysis of a dataset.

Statistics is voodoo with numbers. Like any magic spell in a story, if you don’t know what you’re doing, it’s easy to accidentally turn a person into a toad. Experimental biologists often only have minimal training in statistics, and even less formal, guided practice. This guide turns current (2020) statistical testing recommendations into an easy-to-follow protocol, as best I understand it. The goal is to guide a scientist to apply statistics in an effective, rigorous way, and to guide them away from common pitfalls and misunderstandings.

What this document doesn’t do is try to teach statistical theory. Reading a textbook like “Discovering Statistics Using IBM SPSS Statistics” by Andy Field for example is an excellent, readable guide with practical examples. This document also doesn’t currently describe specific tools to use to accomplish the task, although it would be great to add more pointers to packages implementing them. Free, open source technical computing languages like R, Julia, or Python are great choices, with different packages available.

**Please contribute!** This guide is my own synthesis of knowledge from several sources. But I am not a statistics expert. Please do provide input and corrections. I have placed this on GitHub to encourage modifiation and updates.

Important general points
------------------------
- Statistical tests provide **guidelines** for your conclusions, not binary truth
    - p = 0.051 and p = 0.049 is not the difference between real and false
- Measure and report effect sizes
- Report everything needed to justify and reproduce your analysis
- Beware threshold effects; adjusting any threshold shouldn’t drastically change results
- Show all the data points and descriptive statistics
- No SEM, only SD or 95% (or more) confidence interval
- After adopting a solution, start analysis again with that solution in mind
- Don’t reverse your decisions based on effects on statistical tests
- Large sample sizes can lead to significant normality tests with small effect sizes

Contents
--------
- [General Methods](https://github.com/BioTurboNick/StatisticsProtocols/blob/master/General%20Methods.md)
- [Linear Regression](https://github.com/BioTurboNick/StatisticsProtocols/blob/master/Linear%20Regression.md)
- 1-Factor Analysis of Variance (ANOVA)
- 1-Factor Analysis of Covariance (ANCOVA)
- Factorial ANOVA
- Repeated Measures ANOVA
- Logistic Regression
- Multilevel Models
