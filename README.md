# A/B_testing_cookiecats

## Executive Summary
This project analyses an A/B test dataset from the mobile puzzle game Cookie Cats. The experiment evaluates the impact of shifting the game's first progression gate from level 30(Control) to level 40(Treatment).

## Key Takeaways
- Day 1 retention: No statistically significant difference(p-value = 0.0739).
- Day 7 retention: Statistically significant drop of ~0.82% in retention when moving from level 30 to level 40(Z-score = 3.1574, p-value = 0.0016).
- Recommendation: Keeping the gate at level 30 encourages long-term player retention.

## Experimental design and data integrity
### Pre-experiment Power Analysis
To ensure that the dataset had sufficient data to detect small changes during the test.
- The minimum required sample size calculated was 24657. The total number of data points in the dataset was 90189.

### Data quality and sanity checking
To ensure data integrity and a goodness-of-fit check on the observed user splits to rule out sample allocation.
- There were no missing values in the entire dataset also, no duplicates were found.
- One outlier(sum_gamerounds = 49854) was found using Box plot visual, and it was removed.
  ![outlier]('boxplot_outlier.png').
  
- Sample Ratio Mismatch(SRM) check: SRM check was done using Chi-Square goodness-of-fit test and the observed split was [44699, 45489] and the expected was [45094,45094]. The chi-square test = 6.9200 and the p-value = 0.0085 indicates a statistically significant sample ratio mismatch.(The experiment was continued with sample ratio mismatch in mind.)
- A/A testing was conducted to confirm the user groups behaved identically before encountering any gate and a Welch's T-test was conducted on pre-game activity.(sum_gamerounds <  30), and the results t-stat = 1.8009 and p-value = 0.0717 indicate randomization was clean and had zero bias.

## Evaluating Player Retention
To evaluate whether moving the gate from level 30 to level 40 impacted player retention, a two-sample proportion Z-test was conducted on primary metrics: Day  retention and Day 7 retention.
### Statistical Hypothesis
- Null Hypothesis(H0): There is no true difference in player retention rates between the level 30 and level 40 gate placements. Any observed deviation in sample rates is due to random sampling noise.
- Alternative Hypothesis(H1): There is a statistically significant difference in player retention rates between the control and treatment groups.
### Statistical findings
- Day 1 retention analysis yielded a Z-statistic of  1.7871 and a p-value of 0.07389, which exceeds the 0.05 threshold and thus the null hypothesis could not be rejected.
- Day 7 retention analysis yielded a Z-statistic of 3.1574 and a p-value of 0.0016. Because p_value < 0.05, the null hypothesis can be rejected in favour of the alternative hypothesis.
### Guardrail Metric Analysis
To ensure that higher retention doesn't negatively impact player engagement, 'sum_gamerounds'(total number of rounds played by a player) was evaluated as a guardrail metric using Welch's t-test, and the results: t-statistic = 0.0634 and p-value = 0.9495 suggest that total game rounds played are stable without affecting player engagement.

## Conclusion
Analysing day 1 retention suggests that a 24-hour period is not enough to judge the impact of the gate as most players don't reach gate level 30 or gate level 40 within a day. So retention day 7 was taken as the primary metric and from its analysis, players in the treatment group experienced an absolute drop of ~0.82% and a relative drop of ~4.3%. SO moving the gate from level 30 to level 40 caused a statistically significant drop in day 7 retention from 19.02% down to 18.20%.

## Business takeaway
The extra 10 levels of uninterrupted gameplay in gate 40 led to greater player fatigue, leading to over 220 fewer players retained by day 7 compared to gate 30. Maintaining the gate at level 30 is crucial to preserving long-term player engagement.
