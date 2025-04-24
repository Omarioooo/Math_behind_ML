# <span style="color: #1E90FF;">Linear Regression Summary </span>

## <span style="color: #228B22;">Introduction</span>

This guide explains _`Linear Regression`_ in a simple, detailed way. i’ll cover everything you need to know, including the Least _**Squares method**_, the _**role of the Normal Distribution**_, _**Likelihood**_, _**Log-Likelihood**_, _**Mean Squared Error**_ (MSE), and _**Gradient Descent**_.

---

## <span style="color: #228B22;">1. What is Linear Regression?</span>

### <span style="color: #FF8C00;">What It Does</span>

Linear Regression is a way to find a straight line that best fits a set of data points. Imagine you have points on a graph, and you want to draw a line that gets as close as possible to all of them. That line can help you predict new values. For example, if you know how many hours a student studies ($x$), you can predict their exam score ($y$).
>⚠️ There must me a linear relation ship between **Features** & **Target**

### <span style="color: #FF8C00;">The Line Equation</span>

The line in linear regression looks like this:

$$ y = \beta_0 + \beta_1 x $$

- $y$: The predicted value (like the exam score).
- $x$: The input value (like hours studied).
- $\beta_0$: The y-intercept (where the line crosses the y-axis when $x = 0$).
- $\beta_1$: The slope (how much $y$ changes when $x$ increases by 1).

### <span style="color: #FF8C00;">Example</span>

Let’s use a small dataset:

| $x$ (Hours Studied) | $y$ (Exam Score) |
|-----------------------|--------------------|
| 1                     | 4                  |
| 2                     | 3                  |
| 4                     | 1                  |
| 6                     | 2                  |
| 8                     | 0                  |

We found the best line to be:

$$ y = 4.05 - 0.489x $$

So, if a student studies for $x = 3$ hours:

$$ y = 4.05 - 0.489 \times 3 = 2.583 $$

The predicted score is about 2.58.


-- _**Here’s where you can see a graph that show the data points and the regression line:**_

### <span style="color: #FF8C00;">Graph Placeholder</span>

![linear Vs non_linear](https://i.imgur.com/FfADo2D.png)

___

## <span style="color: #228B22;">2. The Role of $\beta_0$ and $\beta_1$</span>

### <span style="color: #FF8C00;">What Are $\beta_0$ and $\beta_1$?</span>

- $\beta_0$: The starting point of the line on the y-axis. It’s the predicted $y$ when $x = 0$. In our example, $\beta_0 = 4.05$, so if a student studies 0 hours, the predicted score is 4.05 (though this might not make sense in real life—it’s just the math).
- $\beta_1$: The slope of the line. It tells you how much $y$ changes when $x$ increases by 1. In our example, $\beta_1 = -0.489$, meaning for each extra hour of study, the score decreases by 0.489 (a negative relationship).

### <span style="color: #FF8C00;">Why They Matter</span>

- $\beta_0$ sets the base level of the prediction.
- $\beta_1$ shows the relationship between $x$ and $y$:
  - If $\beta_1 > 0$, $y$ increases as $x$ increases (positive relationship).
  - If $\beta_1 < 0$, $y$ decreases as $x$ increases (negative relationship, like in our example).

### <span style="color: #FF8C00;">Example</span>

In our dataset:

- $\beta_0 = 4.05$: If $x = 0$, the predicted score is 4.05.
- $\beta_1 = -0.489$: For each extra hour of study, the score drops by 0.489.

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add a graph here to show how $\beta_0$ and $\beta_1$ define the line:

![parameters](https://i.imgur.com/fc5yVOj.png)
---

## <span style="color: #228B22;">3. Errors (Residuals) in Linear Regression</span>

### <span style="color: #FF8C00;">What Are Errors?</span>

Errors are the differences between the actual $y$ values and the predicted $\hat{y}$ values from the line:

$$ \epsilon_i = y_i - \hat{y}_i $$

- `Actual value` : $y_i = \beta_0 + \beta_1 x_i$.
- ` Predicted value` : $\hat{y}_i = \beta_0 + \beta_1 x_i + \epsilon$.

### <span style="color: #FF8C00;">Example</span>

Using our dataset and line $y = 4.05 - 0.489x$:

- For $x = 1$:

$$ \hat{y} = 4.05 - 0.489 \times 1 = 3.561 \quad \text{Actual } y = 4 \quad \text{Error} = 4 - 3.561 = 0.439 $$

- For $x = 2$:

$$ \hat{y} = 4.05 - 0.489 \times 2 = 3.072 \quad \text{Actual } y = 3 \quad \text{Error} = 3 - 3.072 = -0.072 $$

All errors: $0.439, -0.072, 0.398, -0.934, 0.168$.

### <span style="color: #FF8C00;">Graph Placeholder</span>

![error](https://i.imgur.com/zCY5Ekc.png)
---

## <span style="color: #228B22;">4.Least Squares Method (OLS)</span>

### <span style="color: #FF8C00;">What is Least Squares?</span>

The Least Squares method, also called Ordinary Least Squares (OLS), is the main way `algorithm` to find the best line in linear regression. It works by **minimizing** the **sum of squared errors (SSE)**:

$$ \text{SSE} = \sum_{i=1}^n (y_i - \hat{y}_i)^2 $$

### <span style="color: #FF8C00;">Why Square the Errors?</span>

- **Positive Values**: Errors can be positive or negative. Squaring makes them all positive so they don’t cancel out.
- **Penalize Big Errors**: Squaring makes big errors (like 2) become much larger ($2^2 = 4$), so the method focuses on fixing them.

![squared_error](https://i.imgur.com/OXi7nLd.png)

### <span style="color: #FF8C00;">Example</span>

Using our errors:

- Squared errors: $0.439^2, (-0.072)^2, 0.398^2, (-0.934)^2, 0.168^2$.
- Values: $0.1927, 0.0052, 0.1584, 0.8716, 0.0282$.
- SSE: $0.1927 + 0.0052 + 0.1584 + 0.8716 + 0.0282 = 1.255$.

The OLS method adjusts $\beta_0$ and $\beta_1$ to make SSE as small as possible.
<span style="color: #FF8C00;"># Derivation of OLS Coefficients</span>

<span style="color: #FF8C00;">## Sum of Squared Errors (SSE)</span>

The Sum of Squared Errors (SSE) is defined as:

$$
\text{SSE} = \sum (\epsilon_i)^2
$$

Substituting $\epsilon_i = y_i - \hat{y}_i$, we get:
 

$$
\text{SSE} = \sum (y_i - \hat{y}_i)^2
$$

Substituting $\hat{y}_i = \beta_0 + \beta_1 x_i$, we get:

$$
\text{SSE} = \sum (y_i - (\beta_0 + \beta_1 x_i))^2
$$

<span style="color: #FF8C00;">### Minimizing SSE</span>

To find the coefficients $\beta_0$ and $\beta_1$, we take partial derivatives of SSE with respect to $\beta_0$ and $\beta_1$ and set them to zero.

<span style="color: #FF8C00;">#### Partial Derivative with Respect to $\beta_0$:</span>

$$
\frac{\partial \text{SSE}}{\partial \beta_0} = \sum 2 (y_i - \beta_0 - \beta_1 x_i) (-1) = 0
$$

$$
\sum (y_i - \beta_0 - \beta_1 x_i) = 0
$$

$$
\sum y_i - n \beta_0 - \beta_1 \sum x_i = 0
$$

$$
n \beta_0 + \sum x_i \beta_1 = \sum y_i \tag{1}
$$

![Deriv](https://i.imgur.com/Ni9dyc7.png)


<span style="color: #FF8C00;">#### Partial Derivative with Respect to $\beta_1$:</span>

$$
\frac{\partial \text{SSE}}{\partial \beta_1} = \sum 2 (y_i - \beta_0 - \beta_1 x_i) (-x_i) = 0
$$

$$
\sum x_i (y_i - \beta_0 - \beta_1 x_i) = 0
$$

$$
\sum x_i y_i - \beta_0 \sum x_i - \beta_1 \sum x_i^2 = 0
$$

$$
\sum x_i \beta_0 + \sum x_i^2 \beta_1 = \sum x_i y_i \tag{2}
$$

![Deriv](https://i.imgur.com/vyJFoGP.png)


<span style="color: #FF8C00;">### System of Linear Equations</span>

From the above, we form the system of equations in matrix form:

$$
\begin{bmatrix}
n & \sum x_i \\
\sum x_i & \sum x_i^2
\end{bmatrix}
\begin{bmatrix}
\beta_0 \\
\beta_1
\end{bmatrix}
=
\begin{bmatrix}
\sum y_i \\
\sum x_i y_i
\end{bmatrix}
$$

This system can also be derived using the OLS formula:

$$
\hat{\beta} = (X^T X)^{-1} X^T y
$$

<span style="color: #FF8C00;">## Example from the Info</span>

Given:

$$
X = \begin{bmatrix}
1 & 1 \\
1 & 2 \\
1 & 4 \\
1 & 6 \\
1 & 8
\end{bmatrix}, \quad y = \begin{bmatrix}
4 \\
3 \\
1 \\
2 \\
0
\end{bmatrix}
$$

Compute:

$$
X^T X = \begin{bmatrix}
n & \sum x_i \\
\sum x_i & \sum x_i^2
\end{bmatrix}
= \begin{bmatrix}
5 & 21 \\
21 & 121
\end{bmatrix}
$$

$$
X^T y = \begin{bmatrix}
\sum y_i \\
\sum x_i y_i
\end{bmatrix}
= \begin{bmatrix}
10 \\
26
\end{bmatrix}
$$

The system becomes:

$$
\begin{bmatrix}
5 & 21 \\
21 & 121
\end{bmatrix}
\begin{bmatrix}
\beta_0 \\
\beta_1
\end{bmatrix}
=
\begin{bmatrix}
10 \\
26
\end{bmatrix}
$$

Solving this system yields:

$$
\beta_0 = 4.05, \quad \beta_1 = -0.489
$$

| Feature          | Description                                                                                              |
|------------------|----------------------------------------------------------------------------------------------------------|
| `n`              | The total number of data points. More data points generally make the predictions in regression more reliable. |
| `sum(x_i)`       | The total of all the values for the independent variable x_i. It affects how the regression line is positioned. |
| `sum(x_i^2)`     | The total of all the squared values of the independent variable x_i. It shows how spread out the values are. A bigger number means more variation in x, which can improve the accuracy of the slope. |
| `sum(x_i * y_i)` | This shows the relationship between the independent variable x_i and the dependent variable y_i. It tells you if the relationship is positive or negative and how strong it is. |
| `sum(y_i)`       | The total of all the values for the dependent variable y_i. It helps set the starting point (intercept) of the regression line based on the average value of y. |


<span style="color: #FF8C00;">## Connection to OLS Formula</span>

The system of equations in the image matches the form derived from the OLS formula **_$X^T X \hat{\beta} = X^T y$_**, confirming that minimizing SSE leads to the same result as the matrix approach.


### <span style="color: #FF8C00;">Graph Placeholder</span>
> Diff between the concept of calculus and algebra approach

![calc_VS_algebra](https://i.imgur.com/TaHT0Fa.png)

> ⚠️ The main concept of `Linear System` is to use algebra to  calculate the coordinates of parameters depending on the linearity features between the data

> ⚠️ The concept of `Calculus` is optimizing the coordinate results until finding the best coordinates and this is the approach of **ML**

---

## <span style="color: #228B22;">5. Mean Squared Error (MSE)</span>

> ⚠️ MSE is sensitive to "outliers"

### <span style="color: #FF8C00;">What is MSE?</span>

MSE is the **average** of the squared errors:

$$ \text{MSE} = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2 $$

- It’s the same as SSE but divided by the number of points ($n$).
- MSE tells us how good the model is on average per point.


### <span style="color: #FF8C00;">Example</span>

From our SSE:

- SSE = 1.255.
- $n = 5$.
- MSE: $\frac{1.255}{5} = 0.251$.

A smaller MSE means the line fits the data better.

### <span style="color: #FF8C00;">Why Use the Mean?</span>

- Without the mean, SSE grows with more data points, making it hard to compare models.
- The mean makes MSE a fair measure, like averaging test scores to compare classes of different sizes.

### <span style="color: #FF8C00;">Why Square Errors?</span>

- **No Cancellation**: Positive and negative errors don’t cancel out.
- **Focus on Big Errors**: A big error (like 2) becomes $2^2 = 4$, while a small error (like 0.5) becomes $0.5^2 = 0.25$.
- **Smooth Math**: Squaring makes MSE easier to work with in math (like finding the minimum).

### <span style="color: #FF8C00;">MSE vs. Mean Absolute Error (MAE)</span>

- **MAE**: Takes the absolute value of errors: $\text{MAE} = \frac{1}{n} \sum_{i=1}^n |y_i - \hat{y}_i|$.
- **Difference**:
  - MSE grows quadratically (e.g., error of 2 becomes $2^2 = 4$), so it’s more sensitive to big errors.
  - MAE grows linearly (e.g., error of 2 becomes $|2| = 2$), so it treats all errors more equally.
- Example:
  - Errors: $0.5, 0.0, 0.5$.
  - MSE: $\frac{0.25 + 0.0 + 0.25}{3} = 0.1667$.
  - MAE: $\frac{0.5 + 0.0 + 0.5}{3} = 0.3333$.
  - If we change one error to 2.5:
    - MSE: $\frac{0.25 + 0.0 + 6.25}{3} = 2.1667$ (big jump!).
    - MAE: $\frac{0.5 + 0.0 + 2.5}{3} = 1.0$ (smaller jump).

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add a graph to compare MSE and MAE:

- **Graph Title**: "MSE vs. MAE Sensitivity to Errors"
- **Description**: Two curves: a parabola for MSE ($y = e^2$) and a V-shape for MAE ($y = |e|$), showing how MSE grows faster for large errors.

---

## <span style="color: #228B22;">6. The Normal Distribution in Linear Regression</span>

### <span style="color: #FF8C00;">Why Normal Distribution?</span>

In OLS, we assume the errors ($\epsilon_i$) follow a Normal Distribution:

$$ \epsilon_i \sim N(0, \sigma^2) $$

- Mean of errors = 0.
- Variance ($\sigma^2$) is constant for all points.

### <span style="color: #FF8C00;">Why This Assumption?</span>

- **Better Estimates**: It ensures $\beta_0$ and $\beta_1$ are accurate (per the Gauss-Markov theorem).
- **Statistical Tests**: It lets us use tests like t-tests to check if $\beta_1$ is significant.
- **Prediction Intervals**: It helps us calculate how certain we are about predictions.

### <span style="color: #FF8C00;">Example</span>

Our errors: $0.439, -0.072, 0.398, -0.934, 0.168$.

- Mean: $\frac{0.439 + (-0.072) + 0.398 + (-0.934) + 0.168}{5} \approx 0$, which fits the assumption.
- If we plot these errors in a histogram, they should look like a bell-shaped curve (Normal Distribution).

### <span style="color: #FF8C00;">What If Errors Aren’t Normal?</span>

- The estimates ($\beta_0, \beta_1$) might be less accurate.
- Statistical tests might not work well.
- But if you have a lot of data (not just 5 points), the errors often look normal anyway (thanks to the Central Limit Theorem).

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add a graph to show the distribution of errors:

- **Graph Title**: "Distribution of Errors"
- **Description**: A histogram of the errors with a red curve showing the ideal Normal Distribution.

---

## <span style="color: #228B22;">7. Likelihood and Maximum Likelihood Estimation (MLE)</span>

### <span style="color: #FF8C00;">What is Likelihood?</span>

Likelihood measures how likely our data is under the model. Since we assume errors are Normally distributed, each $y_i$ follows:

$$ y_i \sim N(\beta_0 + \beta_1 x_i, \sigma^2) $$

The likelihood function is:

$$ L(\beta_0, \beta_1, \sigma^2) = \prod_{i=1}^n \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(y_i - (\beta_0 + \beta_1 x_i))^2}{2\sigma^2}\right) $$

- It’s the probability of seeing our data given $\beta_0, \beta_1, \sigma^2$.
- Range: 0 to 1 (higher = better fit).

### <span style="color: #FF8C00;">Goal of MLE</span>

MLE finds the $\beta_0$ and $\beta_1$ that make the likelihood as big as possible (most likely to explain the data).

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add a graph to show the likelihood:

- **Graph Title**: "Likelihood Curve"
- **Description**: A bell-shaped curve with the x-axis as $\beta_0$ values and the y-axis as likelihood (0 to 1), with the peak showing the best $\beta_0$.

---

## <span style="color: #228B22;">8. Log-Likelihood</span>

### <span style="color: #FF8C00;">Why Log-Likelihood?</span>

The likelihood function has a lot of multiplication, which is hard to work with. Taking the natural log turns multiplication into addition, making it easier to maximize.

### <span style="color: #FF8C00;">Equation</span>

$$ \ln L = -\frac{n}{2} \ln(2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i))^2 $$

- Range: $-\infty$ to a negative value (closer to 0 = better fit).
- To maximize $\ln L$, we need to minimize:

$$ \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i))^2 $$

This is the same as minimizing SSE in OLS!

### <span style="color: #FF8C00;">Connection to OLS</span>

When errors are Normally distributed, maximizing the likelihood (MLE) is the same as minimizing SSE (OLS). That’s why OLS and MLE give the same $\beta_0$ and $\beta_1$ in our example: $\beta_0 = 4.05, \beta_1 = -0.489$.

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add a graph to show the log-likelihood:

- **Graph Title**: "Log-Likelihood Curve"
- **Description**: A curve with the x-axis as $\beta_0$ values and the y-axis as log-likelihood (negative values), with the peak showing the best $\beta_0$.

---

## <span style="color: #228B22;">9. Connecting MSE, OLS, and MLE</span>

### <span style="color: #FF8C00;">How They’re Related</span>

- **OLS**: Minimizes SSE (and thus MSE) to find the best line.
- **MLE**: Maximizes likelihood, which (under Normal errors) also minimizes SSE.
- **MSE**: The average SSE, used as a measure of fit and as an estimate of $\sigma^2$:

$$ \hat{\sigma}^2 = \text{MSE} = 0.251 \text{ in our example} $$

### <span style="color: #FF8C00;">Why Normal Distribution Matters</span>

The Normal Distribution assumption ties OLS and MLE together:

- It lets us write the likelihood function.
- It makes minimizing SSE (OLS) the same as maximizing likelihood (MLE).

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add a graph to show the relationship:

- **Graph Title**: "SSE vs. Likelihood"
- **Description**: Two curves: a U-shaped SSE curve and an inverted bell-shaped likelihood curve, showing how minimizing SSE maximizes likelihood.

---

## <span style="color: #228B22;">10. Gradient Descent: Finding the Best Line</span>

### <span style="color: #FF8C00;">What is Gradient Descent?</span>

Gradient Descent is a method to find the best $\beta_0$ and $\beta_1$ by iteratively adjusting them to minimize MSE (the loss function).

### <span style="color: #FF8C00;">How It Works</span>

1. Start with random values for $\beta_0$ and $\beta_1$ (e.g., $\beta_0 = 0, \beta_1 = 0$).
2. Calculate the gradients (slopes) of the loss function:

$$ \frac{\partial \text{MSE}}{\partial \beta_0} = -\frac{2}{n} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i)) $$

$$ \frac{\partial \text{MSE}}{\partial \beta_1} = -\frac{2}{n} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i)) x_i $$

3. Update the parameters:

$$ \beta_0 \gets \beta_0 - \eta \cdot \frac{\partial \text{MSE}}{\partial \beta_0} $$

$$ \beta_1 \gets \beta_1 - \eta \cdot \frac{\partial \text{MSE}}{\partial \beta_1} $$

- $\eta$: Learning rate (e.g., 0.1), controls step size.

4. Repeat until MSE stops decreasing (or changes very little).

### <span style="color: #FF8C00;">Example</span>

In a real dataset (like the Salary dataset in the code), gradient descent might start with $\beta_0 = 0, \beta_1 = 0$, and after many steps, it converges to values close to the OLS solution.

### <span style="color: #FF8C00;">Graph Placeholder</span>

Add two graphs for gradient descent:

- **Graph 1 Title**: "Gradient Descent Steps on MSE Curve"
- **Description**: A collage showing a U-shaped MSE curve with blue dots moving from a random $\beta_0$ to the best $\beta_0$ over steps (e.g., steps 0, 2, 5, 8, 12, 16, 20).
- **Graph 2 Title**: "Loss (MSE) Over Iterations"
- **Description**: A collage showing a curve of MSE decreasing over iterations, with the x-axis as steps (0 to 20) and the y-axis as MSE.

---

## <span style="color: #228B22;">12. Conclusion</span>

### <span style="color: #FF8C00;">What We Learned</span>

- **Linear Regression** finds a line ($y = \beta_0 + \beta_1 x$) to predict $y$ from $x$.
- **OLS** minimizes SSE to find the best line.
- **Normal Distribution** lets us use MLE, which matches OLS when errors are Normal.
- **MSE** measures how good the line is and estimates the error variance.
- **Gradient Descent** adjusts $\beta_0$ and $\beta_1$ to minimize MSE.
- **Likelihood** and **Log-Likelihood** give a probabilistic view of how well the model fits.

### <span style="color: #FF8C00;">Real-World Use</span>

Linear regression is used in many fields:

- Predicting house prices based on size.
- Estimating sales based on advertising budget.
- Forecasting exam scores based on study hours (like our example).

### <span style="color: #FF8C00;">Final Note</span>

All these concepts—OLS, Normal Distribution, MLE, MSE, and Gradient Descent—work together to make linear regression a powerful tool for prediction and analysis.

---