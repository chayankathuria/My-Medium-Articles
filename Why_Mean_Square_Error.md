---
#Optimization: Ordinary Least Squares Vs. Gradient Descent - from scratch#

###What is Optimization?Techniques for optimization - numerical approach and iterative approach, and finally implementation in Python.###
---

**Optimization**

Optimization is at the core of Machine Learning. 
Optimization, in very strict terms, is the process of finding the values for which your Cost Function gives a minimum value. For any Optimization problem with respect to Machine Learning, there can be either a numerical approach or an analytical approach. The numerical problems are Deterministic, meaning that they have a closed form solution which doesn't change. Hence it is also called time invariant problems. These closed form solutions are  solvable analytically. But these are not optimization problems.
Optimization comes in when you have words like 'Min' or 'max' of a function f(x) - the Objective Function or the Cost Function. This Objective Function could define anything with respect to the problem you are optimizing. It could be costs for a company, Losses for another or even revenue etc.
This function will be optimal at a specific point X*. This X* is the optimal point. Hence your optimization problem could be - Find X* for which f(x) is minimum/maximum. This can also be written as argmin(f(x)) - argument where the function f(x) is minimum (or argmax(f(x) conversely).


-----------------------------------------------------------------

**Ordinary Least Squares**
I'm pretty sure you know basics about Linear Regression. And if you don't, no need to worry. Just check this out. Basically, regression means finding the best fit line/curve to your numerical data - a functional approximation of the data. That is you want a mapping function of your input data to the output data (target). This mapping function is written as:
where W0 is the intercept and W1 is the slope of the line and Ŷ is the predicted output. The optimum values of W0 and W1 need to be found. Let's consider this very small dataset:
X = 1,2,3
Y = 5,12,18
So the problem we need to optimize is:
where L is the Loss function or the Cost function or the Error function. Now the next step is to find the correct Loss function for our optimization problem. Because if you minimize the wrong objective function, you will end up with wrong optimal points. The Loss function L we will be using is the Mean Square Error, given as:
Solving for above Loss function, we get to the following formula for finding the optimal weights:
Calculating the above weights using python we get below values:
This is Ordinary Least Squares solution - which is the analytical solution. As we found the least value of squares of the error. 
But this solution is not scalable. Applying this to Linear Regression was fairly easy as we had nice coefficients and linear equations. Applying this to complex and non-linear algorithms like Support Vector Machine will not be feasible. So we will find the numerical approximation of this solution by iterative method - which would be close to (but not exactly equal to) the OLS solution - which gave us the exact solution.


-------------------------------------------------------------------------------

**Gradient Descent**

Let's first understand the intuition behind Gradient Descent Optimization. Consider 20 people(including yourself) are randomly air dropped in a mountain range. Your task is to find the highest peak in the complete range within 30 days. Each one of you has a walkie talkie to communicate and an altimeter to measure the altitude. Each day you all spend hours locating highest peak possible and report your highest altitude of the day to everyone else which they found in the area allotted to them - that is their fitness values. 
Suppose on Day 1 you report 1000ft. , someone else reports 1230 ft. and so on. Then there is person who reports 5000ft. which is the maximum of all. Remember your task was to collectively reach the maxiumum peak of the mountain ranges. What do you do next on Day 2?Next day every one will gather towards the area where maximum altitude was found yesterday. They will think that it's probable that the highest peak of the range would be in this area itself. Why would someone who reported 500ft yesterday once again search that area if there is another area which already has 5000ft. So all the searchers 'greedily' move towards the highest reported point. Now this greed could lead to you to the highest peak of the ranges, but could also lead to a complete blunder. 
The guy that was at 500ft. yesterday could have been at the base of a peak which had a height of 10000ft.! And he greedily ignored it and went towards the other one to maximize that 5000 to say 7000 or 8000 ft. You actually get stuck in a Local Maxima/Optima (Mutation could help here to some extent!).And there is no way could know if you are the Local Optima.
Simulated Annealing is also an algorithm which could save us here. Where the searchers would have searched the complete search space thoroughly and without being biased to most probably find the global maxima.


---

Now back to our optimization problem that we defined using OLS. Let's do the solution using Gradient Descent. Again, the loss function will be the same. But this time we will be iterating step-by-step to reach the optimal point. W start with any arbitrary values of the weights and check the gradient at the point. Our aim is to reach the minima which is the valley bottom. So our gradient should be negative always.

source

Next, we need to update the weights to get them closer to the minima. We have the following equation for it:
This means that weight in next iteration will be weight in previous iteration minus the update. Now this update has 2 components: direction - which is the slope or the gradient, and the value - which is the step size. The gradient will be:
So if at our initial weights, the slope is negative, we are in the right direction. We just need to increase the value of the weights to get it closer. That is exactly what the above equation does. If the slope is negative at the particular point, the second term gets added to the value of weights in previous iteration. Conversely if it is positive, that means we need to go in the opposite direction to get to the minima. In this case the equation subtracts the second term from the value of weights in previous equation. Neat. 
The second component we need to consider is the step size - α. This is a Hyperparameter which you need to decide prior to the start of the algorithm. If the α is too large then your optimizer will be jumping big leaps and never find the minima. Conversely if you set it to be too small, the optimizer will take it forever to reach the minima. Hence we need to set an optimum value for α beforehand.
sourceIf you understood correctly, you would appreciate that the gradient we are talking about here is essentially the Sum of Error. And by we are in essence taking a fraction of that error. And we are propagating that error to update our weights.
Therefore, our equation for weight update becomes:
So let's jot down the clear steps we performed:
Initiate the values of the weights W0, W1 - which can be any value and the step size α - which needs to be a good value.
Find the predictions of target Ŷ = W0 + W1.X for all X.
Calculate the error values (Ŷ-Y) and the MSE.
Update the weights as per the Gradient Descent update rule.
Repeat 2–4.

This is known as Batch Gradient Descent as we are taking the error of the complete batch or the data set per iteration. We also have following variants of Gradient Descent:
Stochastic Gradient Descent, where the updates in the weights are done in every iteration
Mini Batch Gradient Descent, which is a midway between Batch and Stochastic, divides the complete data set into mini batches and then applies weight updates after each batch.

Now finally let's get all of this done in a few lines of code in Python!
Let's begin by initializing our tiny little data set:
Now onto Step 1, initializing weights and the step size which I have chosen as 0.04. You can try tweaking the value and see the results for yourself:
After initializing, we iterate through the complete data set multiple times and calculate Mean Square error per iteration and update the weights:
So we iterate 10 times and hope that our algorithm has converged sufficiently. Let's take a look at our final weights and see how close they got to our OLS solution:
Pretty close! Now let's check the predicted target variable, Ŷ and the Error:
As you can see the predicted variable got pretty close to the actual values. Finally, let's plot the Mean Square Error values per iteration and see how did our algorithm performed:
Great! So we covered :
what at all Optimization is, 
what types of solution it has with respect to Machine Learning, 
what is its analytical approach and its intuition 
its implementation to Linear Regression in python 



---

That is all for the scope of this article. For further read you can follow bellow awesome reads:
https://machinelearningmastery.com/gradient-descent-for-machine-learning/
https://www.youtube.com/watch?v=sDv4f4s2SB8
https://www.amazon.in/Engineering-Optimization-Practice-Singiresu-Rao/dp/0470183527



---

Did this article help? Give it a clap! Do share and comment your thoughts below!
