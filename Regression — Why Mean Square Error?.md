## How do I know what is the correct Loss Function for my Algorithm? 
Because if I choose the wrong Loss Function, I’ll get the wrong solution.

----

In Machine Learning, our main goal is to minimize the error which is defined by the Loss Function. 
And every type of Algorithm has different ways of measuring the error. In this article I’ll be going through some basic Loss Functions used in Regression Algorithms and why exactly are they that way. Let’s begin.
Suppose we have gotten 2 loss functions. Both functions will have different minima. 

So if you optimize the wrong loss function, you come to the wrong solution — which is the optimal point or the optimized value of the weights in my loss function. Or we can say that we are solving the wrong optimization problem. So we need to find the appropriate loss function which we will be minimizing.
### 1. Sum of Errors (SE):
Let’s start by considering the most basic loss function which is nothing but the sum of errors in each iteration. 
The error will be the difference in the predicted value and the actual value. So the loss function will be given as:

Ŷ is the predicted value; Y is the actual value
where the summation goes from n=1 to N where N is the number of instances in our dataset. 
Now consider following line fitting our 3 data points:

Certainly not the best fit line you might say! But as per this loss function, this line is a best fitting line as the error is almost 0. For point 3 the error is negative as predicted value is lower. Whereas for point 1, the error is positive and of almost the same magnitude. For point 2 it is 0. Adding all of these up would lead to a total error of 0! But the error is certainly much more than that. If the error is 0 then the algorithm will assume that it has converged when it actually hasn’t — and will exit prematurely. It would show a very less error value where in reality the value would be much larger. So how can you claim that this is the wrong line? You actually cannot. You just chose the wrong loss function.
### 2. Sum of Absolute Errors (SAE):
SE was certainly not the loss function we’d want to use. 
So let’s change it a bit to overcome its shortcoming. Let’s just take the absolute values of the errors for all iterations. 
This should solve the problem.. right? Or no? This is how the loss function would look like:

So now the error terms won’t cancel out each other and will actually add up. 
So any potential problem with this function? Well, yes. This loss function is not differentiable at 0. The graph of the loss function will be:

Y axis is the loss function
The derivative will not exist at 0. We need to differentiate the function and equate it to 0 to find the optimum point. And that won’t be possible here. We won’t be able to solve for the solution.

### 3. Sum of Squared Errors(SSE):
So let’s take the squares instead of the absolutes. The loss function will now become:

which is very much differentiable at all points and gives non-negative errors. 
But you could argue that why cannot we go for higher orders like 4th order or so. 
Then what if we consider to take 4th order loss function, which would look like:

Hence its gradient will vanish at 3 points. So it will have local minima as well — which are not our optimal solution. 
We need to find the point at global minima to find the optimal solution. So let’ s stick with the squares itself.

### 4. Mean Squared Errors (MSE):
Now consider we are using SSE as our loss function. So if we have a dataset of say 100 points, our SSE is, say, 200. 
If we increased data points to 500, our SSE would increase as the squared errors will add up for 500 data points now. 
So let’s say it becomes 800. If we increase the number of data points again, our SSE will further increase. Fair enough? Absolutely not!

The error should decrease as we increase our sample data as the distribution of our data becomes more and more narrower (referring to normal distribution). The more data we have, the less is the error. But in the case of SSE, the complete opposite is happening. Here, finally, comes in our warrior — Mean Squared Error. Its expression is:

We take the average or mean of SSE. So more the data, lesser will be the aggregated error, MSE.

Here as you can see, the error is decreasing as our algorithm is gaining more and more experience. The Mean Squared Error is used as a default metric for evaluation of the performance of most regression algorithms be it R, Python or even MATLAB.

### 5. Root Mean Squared Error (RMSE):
The only issue with MSE is that the order of loss is more than that of the data. As my data is of order 1 and the loss function, MSE has an order of 2. So we cannot directly correlate data with the error. Hence, we take the root of the MSE — which is the Root Mean Squared Error:

Here, we are not changing the loss function and the solution is still the same. All we have done is reduced the order of the loss function by taking the root.

### 6. Huber Loss:
The Huber loss combines the best properties of MSE and MAE (Mean Absolute Error). It is quadratic for smaller errors and is linear otherwise (and similarly for its gradient). It is identified by its delta parameter:

Huber loss is less sensitive or more robust to outliers in data than the MSE. It’s also differentiable at 0. It’s basically absolute error, which becomes quadratic when the error is small. How small that error has to be to make it quadratic depends on a hyperparameter, 𝛿 (delta), which can be tuned. Huber loss approaches MAE when 𝛿 ~ 0 and MSE when 𝛿 ~ ∞ (large numbers.)
