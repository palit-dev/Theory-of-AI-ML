# Hypothesis Testing
Hypothesis testing is a statistical method which is used to make decision about entire population, with the help of only sample data. The question to be answered is translated into 2 competing and non-overlapping hypothesis. 

## Null Hypothesis (H0)
Null Hypothesis is basically saying that your work has no statistical basis and whatever observed was purely by chance. For example, suppose I am stating that the newer product is better than the older one. The Null Hypothesis will be:

H0: Both the New and the old product are one and the Same.

Similarly suppose I am saying that in a Linear Regression, $\beta_1 = 32$. The Null Hypothesis will state:

H0: $\beta_1 \neq 0$

## Alternative Hypothesis (H1)
The Alternative Hypothesis is the one that we want to be correct. It is the hypothesis that states that my work are statistically significant. Simply speaking, that I am not wrong and my observation were not purely by chance. So for the same two examples states previously,

H1: The New Product is better than the Old One

H1: $\beta_1 = 32$

## Significance Level
The significance level is the maximum probability allowed to reject the null hypothesis. So, suppose I want to predict something with 95% confidence, then the significance level will be $1-confidence level$. The significance level is usually determined by domain experts. As a rule of thumb, biomedical applications use a significance level of 0.01 whereas business researches use a significance level of 0.05.

In layman's term, I want the probability of Null Hypothesis (probability that I am wrong) to be less than the significance level i.e., 0.05 or 5%

## p-value
p-value is the probability of the null hypothesis (the probability that our model is meaningless). Thus, we want $p-value < 0.05$ to say that the outcome of our statistical analysis is meaningful. 

## T Statistics
The p-value is used to understand whether the statistics derived from a single group is valid or not whereas the T-Test is used to understand the statistics derived from two different groups are valid or not. The t-test is also used to reject the Null-Hypthesis if it is **greater** than a threshold. It works best when the underlying distributions are normal and there is 30-40 data points. Above that we use Z-score.

![Normal Distribution of Two Groups](/img/normal.png "Normal Distribution of Two Groups")

H0: The statistics obtained from two groups are same

H1: The statistics obtained from two groups are different

The T-score is calculated as

$$
t_{score} = \frac{|\mu_1 - \mu_2|}{\sqrt{\frac{\sigma_1^2}{N_1}+\frac{\sigma_2^2}{N_2}}}
$$

where, $\mu_1, \mu_2, \sigma_1, \sigma_2$ are the means and standard deviation of the two groups respectively and $N_1$ and $N_2$ are the number of data points in each group. We compare this $t_{score}$ with the threshold in the t-table corresponding to the degrees of freedom and the required p-value. 

$$
dof = N_1 + N_2 - 2
$$

If the  $t_{score}>threshold$, we reject the Null Hypothesis and the corresponding p-value is less than 0.05 (or whatever value required).

![T-table](/img/t-table.jpg "t-table")

Simply speaking the p-value for the corresponding t-value is the probability that we will see such t-values.

### Types of t-test

* If the groups come from a single population (e.g. measuring before and after an experimental treatment), perform a paired t-test.
* If the groups come from two different populations (e.g. two different species, or people from two separate cities), perform a two-sample t-test (a.k.a. independent t-test).
* If there is one group being compared against a standard value (e.g. comparing the acidity of a liquid to a neutral pH of 7), perform a one-sample t-test.
* If you only care whether the two populations are different from one another, perform a two-tailed t-test.
* If you want to know whether one population mean is greater than or less than the other or care about the direction of difference, perform a one-tailed t-test.

### Assumptions for t-Statistics

The Underlying distributions are gaussian with similar means and standard deviation

## Chi-Square Test
A chi-square test is a statistical test used to compare observed results with expected results. The purpose of this test is to determine if a difference between observed data and expected data is due to chance, or if it is due to a relationship between the variables you are studying. Therefore, a chi-square test is an excellent choice to help us better understand and interpret the relationship between **categorical** variables.

### Assumptions of Chi-Square Test
* The categories are mutually exclusive i.e. each subject fits in only one category. 
* The data should be in the form of frequencies or counts of a particular category and not in percentages
* The observations should be independent of each other.

### Procedure
For a given dataset, we determine the critical value corresponding to our significance level and the degrees of freedom from a Chi-Squared table. For a dataset with $n$ categorical features,

$$
dof = n-1
$$

The Chi-Squared values is given as,

$$
\chi^2=\frac{\sum_{i=1}^n (x_i-\bar{x})^2 }{\bar{x}}
$$

If chi-squared value is greater than the critical value, we reject the Null hypothesis.

### Example
**Q: A School principle would like to know on which days of the week students are more likely to be absent. The Principle expects that the students will be absent equally throughout the week. The principle selects a random sample of 100 teachers asking them which day of the week they had the highest number of student absences. Based on the following results, do the days for the highest number of absences occurs with equal frequencies.**

|  | Monday | Tuesday | Wednesday | Thursday | Friday |
|---|---|---|---|---|---|
| Observed Value  | 23 | 16 | 14 | 19 | 28 |
| Expected Value  | 20 | 20 | 20 | 20 | 20 |


Let us propose our Hypothesis as:

H0: Absence occur with equal frequencies
H1: Absence occur with unequal frequences

$dof = n-1 = 5-1=4$

Hence, Critical value = 9.49 for significance level of 0.05

The $\chi^2$ value is given as:

$$
\chi^2=\frac{\sum_{i=1}^n (x_i-\bar{x})^2 }{\bar{x}} = \frac{3^2}{20} + \frac{4^2}{20}+\frac{6^2}{20}+\frac{1^2}{20}+\frac{8^2}{20} = 6.3<9.49
$$

Hence, we cannot reject the Null Hypothesis. Thus, absence occurs with equal freqiencies.

## Annova Test
