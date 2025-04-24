# <span style="color: #1E90FF;">Linear Regression Summary</span>

## <span style="color: #228B22;">Introduction</span>

This guide provides a comprehensive overview of **Linear Regression**, covering key concepts such as **Least Squares**, **Likelihood**, **Log-Likelihood**, **Loss Function**, the role of parameters ($\beta_0$) and ($\beta_1$), and **Gradient Descent**. It explains how these concepts interconnect and function within linear regression.

---

## <span style="color: #228B22;">1. Least Squares</span>

### <span style="color: #FF8C00;">Definition</span>

**Least Squares** is the core method in linear regression for finding the best-fitting straight line. It minimizes the sum of squared differences (errors) between the observed values $y_i$ and predicted values $\hat{y}_i$.

> ⚠️ Least Squares assumes errors are normally distributed with mean 0 and constant variance.

### <span style="color: #FF8C00;">Equation</span>

The sum of squared errors (SSE) is:

$$ \text{SSE} = \sum_{i=1}^n (y_i - \hat{y}_i)^2 $$

- $y_i$ : Actual value (e.g., exam score).
- $\hat{y}_i$ = $\beta_0$ + $\beta_1 x_i$ : Predicted value, where $\beta_0$ is the intercept and $\beta_1$ is the slope.
- $x_i$ : Input variable (e.g., hours studied).

### <span style="color: #FF8C00;">Range</span>

- From 0 to $\infty$.
- Low value = good model fit.
- High value = poor model fit.

### <span style="color: #FF8C00;">Goal</span>

Minimize SSE by adjusting $\beta_0$ and $\beta_1$ to make predicted values as close as possible to observed values.

### <span style="color: #FF8C00;">Graph</span>

- **Shape:** Parabolic (U-shaped) curve.
- **X-axis:** Values of $\beta_0$.
- **Y-axis:** SSE (0 to $\infty$ ).
- **Lowest point:** Best value for $\beta_0$.

![Image 1: Least Squares Graph](https://i.imgur.com/LeastSquaresGraph.png)

**Image Description:** A graph showing SSE as a red parabolic curve. The x-axis is $\beta_0$ values (-10 to 10), and the y-axis is SSE (0 to $\infty$). The lowest point shows the best $\beta_0$ value for an accurate model.

### <span style="color: #FF8C00;">Example</span>

If a student studied for $x = 4$ hours and the model predicts $\hat{y} = 80$ (score), but the actual score is $y = 85$ :
- Error = $85 - 80 = 5$.
- Squared error = $5^2 = 25$.
A smaller error increases model fit, reducing SSE.

---

## <span style="color: #228B22;">2. Likelihood</span>

### <span style="color: #FF8C00;">Definition</span>

**Likelihood** measures how probable the observed data is given the model parameters. In linear regression, it assumes errors ($\epsilon_i = y_i - \hat{y}_i$) follow a normal distribution with mean 0 and variance \(\sigma^2\).

> ⚠️ Likelihood is **not** the probability of the parameters being correct—it’s the probability of the data given those parameters.

### <span style="color: #FF8C00;">Equation</span>

The likelihood function is:

$$ L(\beta_0, \beta_1, \sigma^2) = \prod_{i=1}^n \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(y_i - (\beta_0 + \beta_1 x_i))^2}{2\sigma^2}\right) $$

- $y_i$ : Actual value.
- $\hat{y}_i = \beta_0 + \beta_1 x_i$ : Predicted value.
- $\sigma^2$ : Variance of errors.

### <span style="color: #FF8C00;">Range</span>

- From 0 to 1.
- High value = good model fit.
- Low value = poor model fit.

### <span style="color: #FF8C00;">Goal</span>

Maximize the likelihood by adjusting $\beta_0$ and $\beta_1$ to make observed data most probable.

### <span style="color: #FF8C00;">Graph</span>

- **Shape:** Bell-shaped curve.
- **X-axis:** Values of $\beta_0$.
- **Y-axis:** Likelihood (0 to 1).
- **Peak:** Best value for $\beta_0$.

![Image 2: Likelihood Graph](https://i.imgur.com/LikelihoodGraph.png)

**Image Description:** A graph showing Likelihood as a green bell-shaped curve. The x-axis is $\beta_0$ values (-10 to 10), and the y-axis is Likelihood (0 to 1). The peak shows the best $\beta_0$ value.

### <span style="color: #FF8C00;">Example</span>

For a student with $x = 4$ hours and actual score $y = 85$, if the model predicts $\hat{y} = 80$ :
- Error = $85 - 80 = 5$.
- Likelihood contribution depends on how close $\hat{y}$ is to $y$, assuming normal errors.

---

## <span style="color: #228B22;">3. Log-Likelihood</span>

### <span style="color: #FF8C00;">Definition</span>

**Log-Likelihood** is the natural logarithm of the likelihood, converting multiplication to addition for easier computation.

### <span style="color: #FF8C00;">Equation</span>

$$ \ln(L) = -\frac{n}{2} \ln(2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i))^2 $$

### <span style="color: #FF8C00;">Range</span>

- From $-\infty$ to a negative value.
- Close to 0 = good model.
- Large negative = poor model.

### <span style="color: #FF8C00;">Graph</span>

> ⚠️ **Note:** Log-Likelihood is similar to Likelihood but with negative values. The Loss graph (below) covers this concept visually.

---

## <span style="color: #228B22;">4. Loss Function (Mean Squared Error)</span>

### <span style="color: #FF8C00;">Definition</span>

The **Loss Function**, also known as **Mean Squared Error (MSE)**, is the average of squared errors. It is equivalent to minimizing the negative log-likelihood (assuming normal errors) and is used to optimize the model.

### <span style="color: #FF8C00;">Equation</span>

$$ \text{Loss (MSE)} = \frac{1}{n} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i))^2 $$

Sometimes scaled for gradient computation:

$$ \text{Loss} = \frac{1}{2n} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i))^2 $$

### <span style="color: #FF8C00;">Range</span>

- From 0 to $\infty$.
- Small value = good model.
- Large value = poor model.

### <span style="color: #FF8C00;">Connection to the Model</span>

The predicted value is:

$$ \hat{y}_i = \beta_0 + \beta_1 x_i $$

MSE measures how far \(\hat{y}_i\) is from \(y_i\), penalizing larger errors more heavily.

### <span style="color: #FF8C00;">Graph</span>

- **Shape:** Parabolic (U-shaped) curve.
- **X-axis:** Values of $\beta_0$.
- **Y-axis:** Loss (0 to $\infty$).
- **Lowest point:** Best value for $\beta_0$.

![Image 3: Loss Function Graph](https://i.imgur.com/LossFunctionGraph.png)

**Image Description:** A graph showing Loss (MSE) as a red parabolic curve. The x-axis is $\beta_0$ values (-10 to 10), and the y-axis is Loss (0 to $\infty$). The lowest point is the best $\beta_0$ value.

---

## <span style="color: #228B22;">5. Role of Parameters $\beta_0$ and $\beta_1$</span>

### <span style="color: #FF8C00;">Definition</span>

- $\beta_0$ : The **intercept** in the linear regression equation.
- $\beta_1$ : The **slope** for the input variable $x$.

Equation:

$$ \hat{y}_i = \beta_0 + \beta_1 x_i $$

### <span style="color: #FF8C00;">Role of $\beta_0$</span>

1. **Starting Point**: Predicted value when $x = 0$ :
   $$ \hat{y} = \beta_0 $$
2. **Adjusts Line**: Shifts the regression line up or down.
3. **Bias**: Reflects the baseline value of the outcome.

### <span style="color: #FF8C00;">Role of $\beta_1$</span>

- Determines the **slope** of the line with respect to $x$.
- Indicates how much $\hat{y}$ changes per unit increase in $x$.
- Positive $\beta_1$ = positive relationship; negative = negative relationship.

### <span style="color: #FF8C00;">In Graphs</span>

- The x-axis in Likelihood and Loss graphs represents $\beta_0$ values.
- Peak in Likelihood = lowest point in Loss = best $\beta_0$.

![Image 4: \(\beta_0\) and \(\beta_1\) Graph](https://i.imgur.com/BetaParametersGraph.png)

**Image Description:** A graph showing a regression line with data points. The line’s position ($\beta_0$) and slope ($\beta_1$) are labeled, with $\beta_0$ as the y-intercept and $\beta_1$ as the slope.

---

## <span style="color: #228B22;">6. Gradient Descent</span>

### <span style="color: #FF8C00;">Definition</span>

**Gradient Descent** is an algorithm that adjusts parameters ($\beta_0, \beta_1$) to minimize the Loss (MSE).

### <span style="color: #FF8C00;">How It Works</span>

1. Start with random values for $\beta_0$ and $\beta_1$.
2. Calculate the gradients:
   $$ \frac{\partial \text{Loss}}{\partial \beta_0} = -\frac{2}{n} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i)) $$
   $$ \frac{\partial \text{Loss}}{\partial \beta_1} = -\frac{2}{n} \sum_{i=1}^n (y_i - (\beta_0 + \beta_1 x_i)) x_i $$
3. Update parameters:
   $$ \beta_0 \gets \beta_0 - \eta \cdot \frac{\partial \text{Loss}}{\partial \beta_0} $$
   $$ \beta_1 \gets \beta_1 - \eta \cdot \frac{\partial \text{Loss}}{\partial \beta_1} $$
   where $\eta$ is the learning rate.
4. Repeat until Loss stabilizes.

### <span style="color: #FF8C00;">Graphs</span>

- **Gradient Descent Graph (Collage):**
  - **Shape:** Red parabolic curve with moving blue dots for each step.
  - **X-axis:** $\beta_0$ values.
  - **Y-axis:** Loss.

![Image 5: Gradient Descent Collage](https://i.imgur.com/GradientDescentCollage.png)

**Image Description:** A collage of 7 images. Each shows the Loss Function (red parabolic curve) with blue dots marking \(\beta_0\) at specific steps (e.g., steps 0, 2, 5, 8, 12, 16, 20). The x-axis is \(\beta_0\) (-10 to 10), and the y-axis is Loss (0 to \(\infty\)). It shows \(\beta_0\) moving from a random value (e.g., \(\beta_0=-5\)) to the best value (e.g., \(\beta_0=2\)).
**Notes:** Run the code in Section 11.1 in Jupyter Notebook to generate the images and collage, saving as `gradient_descent_collage.png`.

- **Loss vs. Steps Graph (Collage):**
  - **Shape:** Blue curve decreasing gradually.
  - **X-axis:** Number of steps (iterations).
  - **Y-axis:** Loss.

![Image 6: Loss vs. Steps Collage](https://i.imgur.com/LossVsIterationsCollage.png)

**Image Description:** A collage of 7 images. Each shows the Loss curve (blue) up to a specific step (e.g., steps 0, 2, 5, 8, 12, 16, 20). The x-axis is steps (0 to 20), and the y-axis is Loss. It shows Loss decreasing until it stabilizes at a small value.
**Notes:** Run the code in Section 11.1 in Jupyter Notebook to generate the images and collage, saving as `loss_vs_iterations_collage.png`.

---

## <span style="color: #228B22;">7. Connecting Concepts to Linear Regression</span>

### <span style="color: #FF8C00;">Relationships</span>

1. **Least Squares and Loss**: The Loss (MSE) is derived from SSE, aiming to minimize errors.
2. **Likelihood and Log-Likelihood**: Likelihood measures model fit, and log-likelihood simplifies calculations.
3. **Loss (MSE)**: Equivalent to minimizing negative log-likelihood under normal error assumptions.
4. **Parameters $\beta_0$ and $\beta_1$**: $\beta_0$ sets the baseline, and $\beta_1$ defines the relationship strength.
5. **Gradient Descent**: Adjusts $\beta_0$ and $\beta_1$ to minimize Loss and maximize Likelihood.

### <span style="color: #FF8C00;">How They Work Together</span>

- The model computes predicted values ($\hat{y}_i = \beta_0 + \beta_1 x_i$).
- Likelihood and Loss are calculated based on errors ($y_i - \hat{y}_i$).
- Gradient Descent adjusts $\beta_0$ and $\beta_1$ to minimize Loss.

---

## <span style="color: #228B22;">8. Conclusion</span>

- **Linear Regression** models a linear relationship ($\hat{y}_i = \beta_0 + \beta_1 x_i$) to predict continuous outcomes.
- **Least Squares** and **Loss (MSE)** measure how well the model fits the data.
- **Likelihood** and **Log-Likelihood** provide a probabilistic view of model fit.
- **Parameters $\beta_0$ and $\beta_1$** define the intercept and slope of the regression line.
- **Gradient Descent** adjusts $\beta_0$ and $\beta_1$ to minimize Loss, improving accuracy.
- Visualizations (collages) illustrate how $\beta_0$ moves on the Loss Function and how Loss decreases over iterations.
- The student exam score example shows how these concepts apply to real-world predictions.