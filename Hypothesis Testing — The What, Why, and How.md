Understanding the intuition behind Hypothesis Testing. What exactly it is, why do we do it and how do to perform it. Let’s dive right in!
## The Intuition

Let’s first understand the intuition behind Hypothesis Tests. Consider you are working in an e-commerce company and you come out with a new website design to attract more customers. Your boss wants to know really if your new website design is worth investing on, or it’s just a gimmick. What do you do? You can’t just roll out the website to all your customers and go all out. You will want to confirm if your new design really works by directing the traffic to the new website for a few days. If the result comes out astonishingly good, that means your new website design is indeed great. Otherwise, it could just be a one-off campaign .
Your new website is the hypothesis you want to test. But you want it to compare it with something — right? For that, you make a ‘Null Hypothesis’. Your Null Hypothesis says that your website is crap. It doesn’t have any actual impact. And then you propose an ‘Alternate Hypothesis’. Your Alternate Hypothesis says that your new website actually is great and it really increased your customers. We first assume that our null hypothesis is true. So if you succeed in proving that your null hypothesis is false, you actually prove your alternate hypothesis to be true!
Great! So you now have an intuition as to what we are doing, why we are doing, and how we are doing. Let’s get into the details now.

## Significance level & Confidence Interval
Continuing our example, consider that your company’s average customers per day are around 5430 per day. If you plot a graph for the customers on each day for, say, a year, you will get the below normal distribution with the mean at 5430.

Before you get started with testing your new idea, you set a Significance Level — a threshold probability. This is also known as the critical value — α.
The area under the curve beyond the critical value is the critical region. The critical value defines how far away our sample statistic(our experimental value) must be from the null hypothesis(original mean) value before we can say it is unusual enough to reject the null hypothesis.
You then direct the traffic to your new site for a few days and see the results. Let’s say the average comes out to be 5723 customers. Now this increase in number could be either due to your new design(which your Alternate Hypothesis proposes) or just by luck. We then calculate the test statistic for this experiment — which is the Z-score for Z- tests(more on this below). That means, we need to check how far or how many standard deviations away did the experimental value of 5723 lie from our original distribution mean. This can be calculated using below expression:

X = Sample mean, μ=Population mean, σ=Standard deviation
The critical value can be any value between 0 and 1. It is typically chosen as 0.05. Which means that only if the P-Value of the Z-Score of achieving a value as large as 5723 is less than 0.05, you can reject the null hypothesis. Else, you fail to reject. Now, as you might know that the area under the curve denotes the total probability, the area beyond the critical value will be 5%. Or we can say that we have a confidence interval of 95%. If you decrease your critical value to 0.01, you make your Hypothesis Test more strict as you now want the new p-value to be even lower (less than 0.01) if you want to reject your null hypothesis. This means that your confidence interval will be 99%.

## P-Value
The probability of achieving a value 5723 or more extreme is the P-Value assuming our null hypothesis to be true. Note that it’s not the probability to achieve the point estimate 5723, which would be very low. It is the total probability of achieving a value so rare and even rarer. It is the area under the normal curve beyond the P-Value mark. This P-Value is calculated using the Z score we just found. Each Z-score has a corresponding P-Value. This can be found using any statistical software like R or even from the Z-Table.

Now if this P-Value comes to be less than critical value — signifying that probability of achieving this number of customers was so unlikely that it was indeed not by luck, we can reject our null hypothesis. Now, we cannot say that we accept our alternate hypothesis as statistics is a game of inferences and we can never be 100% sure. But, as we set had set our confidence interval, we can be 95% or even 99% sure. This is where errors creep in!
Type 1 and Type 2 Errors
Now as I said, we can never be 100% sure. There is always a possibility that your conclusion is wrong and the ground truth, the reality, is totally opposite.
If your significance level is 0.05, that means that you indeed have a 5% chance to be wrong! Meaning, you rejected your null hypothesis when it was actually true in reality. This is a Type 1 Error. Hence, the probability of committing a Type 1 error is α.
Conversely, you could also conclude that your null hypothesis is true or in statistical words, you fail to reject your null hypothesis when in reality it was actually false. This is a case of Type 2 Error. The probability of committing a Type 2 error is explained by Beta — β.


Power is the probability of rejecting the null hypothesis when it is false. So the probability of committing a type 2 error is 1-P(Type 2 error) or 1-β.
Now how can we reduce these errors? We could simply increase our confidence level or in other words, decrease our α. Doing so reduces the area under α and hence the probability of committing the type 1 error. But decreasing α increases the probability of committing type 2 error as you will be failing to reject your null hypothesis more! So there is a trade-off.
You can also increase your sample size, n, which will make your distribution curve narrower, hence reducing the probability of committing errors.

## One Tailed vs. Two Tailed Tests
Statistical tests can be directional as well. What this means is that the alternate hypothesis you proposed is for either an increase or a decrease of results. In our example, we wanted to test if the customers increased. So it was a case of One Tailed Test. Hence for confidence interval of 95%, the 5% of the probability distribution is in the direction we are testing (rightwards in our case).
Conversely, we could be testing in the other direction as well. For example, to test if making certain changes to a software significantly reduced the time to process. In this case, we will be considering the leftward portion of our normal curve.


For the case of two tailed tests, there is no specific direction. Our alternate hypothesis just checks if the new statistic has significantly changed i.e., it is significantly greater or less than the original one. Hence for a 95% confidence interval, our 5% probability distribution will be split into two halves of 2.5% each in both the directions. Hence the α will be 0.025.

### Types of Statistical Tests
Z-Test
Z-Test is generally used when the difference in means is to be calculated between two distributions. The standard deviation of the population should be known and the number of samples should be more than 30. One of the most important assumption of z-test is that all sample observations are independent than each other.
T-Test
T-Test is used when the standard deviation of the population is unknown and has to be approximated from the sample. It is generally used when two different populations are to be compared. There are three main types of t-test:
An Independent Samples t-test compares the means for two groups.
A Paired sample t-test compares means from the same group at different times (say, one year apart).
A One sample t-test tests the mean of a single group against a known mean
Chi-Square Test
Chi-Square test is generally used when testing is related to categorical variables. There are mainly two types of chi-square tests — goodness of fit test and test for Association. For One Categorical Variable, the goodness of fit test is used to test whether observations match with a distribution. The association test, on the other hand, is used to compare two variables in a contingency table to see whether they are independent or not.
Chi-Square Test are usually used in feature selection process. We use the Association test to check correlation all the features with the target variable. The top features with highest correlation are then selected to train the model.
These are the statistical tests that are mainly used. There are more tests as well like F-Tests, ANOVA.
If you want to dig in deeper and understand the actual mathematics behind, I suggest you following excellent resources :
https://www.udacity.com/course/intro-to-inferential-statistics--ud201
https://www.khanacademy.org/math/ap-statistics
