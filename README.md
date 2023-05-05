###  Condition

In the context of some hypothesis testing the target group was offered a new payment mechanics on the site, while the control group was left with the basic mechanics. It's necessary to analyze the results of the experiment and draw a conclusion as to whether it's worth launching the new payment mechanics on all users.

### Determining metrics

Since the target group was offered a new payment mechanic on the site, it will primarily affect **conversion to purchase**. It is exactly this metric that we will take as the basis for our conclusions. The secondary metrics that we will look at will be **ARPU** (average revenue per active user) and **ARPPU** (average revenue per paying user)

### EDA

Visualize our input data and plot the :
- A histogram of the distribution of students by group
- Distribution histogram of the average check
- Boxplot by the average check
- QQ plot to check the normality of the distribution

***
**Histogram of distribution of students by group**

![](https://i.ibb.co/CJsrNrk/image.jpg)

_Graphics conclusion:_  

Sample sizes do not coincide in size (the target is ~ 4.4 times larger) this can significantly affect the A/B test, namely lead to a decrease in test power and complicate the identification of statistically significant differences between the groups. At this stage, I would advise to conduct an additional A/A test to make sure that the experimental platform settings are correct

**Histogram of distribution of the average check**

![](https://i.ibb.co/0rwttTZ/image.jpg)

_Graphics conclusion:_

As you can see, the distribution is not normal. If we test with this metric, we will have to turn to non-parametric statistical tests, such as the Mann-Whitney test or the bootstrap method.
We see on the graph, an abnormally large cohort with a mean check of 1800 -1999 in group "B." This suggests that users in this group, in addition to the new payment mechanics, were offered some other changes that we were not told about. Consequently, it could lead to a misinterpretation of the results of the experiment

**Boxplot by the average check**

![](https://i.ibb.co/JRhjGnB/image.jpg)

_Graphics conclusion:_

We can see that the groups have differences in the average check, in the median, in the target group there is a larger interquartile range, as well as in both samples there are outliers. If we noted that there is a shift in the average receipt, then most likely our samples are formed taking into account additional conditions, which were not announced to us in advance. What will be the final result of the experiment to do not in our favor and adds to the problem of interpretability

**QQ-plot to check the normality of the distribution**

![](https://i.ibb.co/6w3pRZT/QQ.jpg)

_Graphics conclusion:_

On the QQ plot of two samples A and B and a normal distribution, the data do not lie on the line, this may indicate that the data deviate from the normal distribution. In this case we can conclude that the data distribution is not normal
***

### A/B - test

To understand how statistically significant the difference in conversion to purchase is, let's conduct an A/B test.
- (H0): There is no difference between the conversion to purchase in the test group and the control group.
- (H1): There is a difference between purchase conversion in the test group and the control group.

Since data in "purchase" and "group" fields are categorical variables, we will use Chi-square test

`Test results`

![](https://i.ibb.co/v1ShCh0/image.jpg)

_Conclusion of the experiment:_

As a result of the Chi-square test, we get two main indicators: test statistic and p-value.
The value of the test statistic reflects the degree of difference between the observed and expected values in the contingency table. The greater the value of the test statistic, the greater the differences between the variables and the less likely it is that such differences are due to chance.
The P-value (p-value) shows the probability of obtaining the same or even more extreme test statistic than the observed one, provided the null hypothesis is true. The null hypothesis is that there is no statistically significant relationship between the variables, and any differences we see can be explained by random factors.

In our case, the **test statistic value is 0.53**, indicating that the differences between the variables are small. **The P-value is 0.468**, which means that assuming the null hypothesis is true, we can obtain a test statistic equal to or greater than the observed one with probability 0.468.

**Assuming a 5% level of significance**, we can conclude that the **p-value is greater than the alpha** and that **we do not reject the null hypothesis**. Simply put, there is **no significance in pay conversion between the old and new payment mechanics**.
***
#### Analysis of the secondary metric ARPPU by Bootstrap 

![](https://i.ibb.co/L5vfpjm/ARPPU.jpg)

_Conclusion of the experiment:_

p_value < 0.05 and 0 is not within the confidence interval. At the significance level of 0.05, we can reject the null hypothesis of equality of the average ARPPU values of the two samples

## Summary

In this task we established that the key metric of the experiment should be conversion to purchase (CR), as we investigate the mechanics of improving payment for services on the site. During the test (Chi-square) we found no statistically significant differences between the control and target groups.

If we only take these factors into account, we shouldn't "roll out" the update to all users. But as it seems to me not everything is unambiguous:

* First, we need to verify that the splitting system by group and the experimental platform settings are correct.
* Secondly, analyze more thoroughly the reasons for the increase in the average check in the target group. If it turns out that in addition to changes in payment mechanics in the target group, there were other changes that increased the average bill, and they were not made public, we should stop the experiment because we will face the problem of interpreting the results on it.
* Thirdly, the revenue figures ARPU and ARRPU are statistically significantly different from the control group, the consequence of running the update will be an increase in business income.
