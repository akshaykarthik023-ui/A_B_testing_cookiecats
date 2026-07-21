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
- Sample Ratio Mismatch(SRM) check: SRM check was done using Chi-Square goodness-of-fit test and the observed split was [44699, 45489] and the expected was [45094,45094]. The chi-square test = 6.9200 and the p-value = 0.0085 indicates a statistically significant sample ratio mismatch.(The experiment was continued with sample ratio mismatch in mind.)
- A/A testing was conducted to confirm the user groups behaved identically before encountering any gate and a Welch's T-test was conducted on pre-game activity.(sum_gamerounds <  30) and the results t-stat = 1.8009 and p-value = 0.0717 indicate randomization was clean and had zero bias.
