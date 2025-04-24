# <span style="color: #1E90FF;">Logistic Regression Summary</span>

## <span style="color: #228B22;">Introduction</span>

This guide provides a comprehensive overview of **`Logistic Regression`**, covering key concepts such as **Likelihood**, **Log-Likelihood**, **Odds**, **Log Odds**, the role of parameters ($a$ and $b$ or $\beta_0$ and $\beta_1$), **Gradient Descent**, and **Log Loss**. It explains how these concepts interconnect and function within logistic regression, using a consistent example of predicting whether a student passes an exam based on hours studied.

---

## <span style="color: #228B22;">1. Likelihood</span>

### <span style="color: #FF8C00;">Definition</span>

**Likelihood** measures how probable the observed data is given a set of model parameters. It evaluates how well the parameters fit the observed outcomes. In logistic regression, it shows how likely the observed labels ($y_i$) are, given the predicted probabilities ($P_i$).

> ⚠️ Likelihood is **not** the probability of the parameters being correct—it’s the probability of the data given those parameters.

### <span style="color: #FF8C00;">Equation</span>

The likelihood function is:

$$ L(\beta_0, \beta_1) = \prod_{i=1}^n P_i^{y_i} \cdot (1-P_i)^{1-y_i} $$

- $P_i$: Predicted probability, calculated as $P_i = \frac{1}{1 + e^{-(\beta_1 x_i + \beta_0)}}$, where $\beta_0$ is the intercept ($b$) and $\beta_1$ is the coefficient ($a$).
- $y_i$: Actual value (0 or 1).
- If $y_i = 1$: Contribution is $P_i$.
- If $y_i = 0$: Contribution is $1 - P_i$.

### <span style="color: #FF8C00;">Range</span>

- From 0 to 1.
- High value = good model fit.
- Low value = poor model fit.

### <span style="color: #FF8C00;">Goal</span>

Maximize the likelihood by adjusting parameters to make observed labels as probable as possible.

### <span style="color: #FF8C00;">Graph</span>

- **Shape:** Bell-shaped curve.
- **X-axis:** Values of $\beta_0$ ( $b$ ).
- **Y-axis:** Likelihood (0 to 1).
- **Peak:** Best value for $\beta_0$.

![Image 1: Likelihood Graph](https://i.imgur.com/Ch5A8Lg.png)

**Image Description:** A graph showing Likelihood as a bell-shaped curve. The x-axis is $\beta_0$ values (-10 to 10), and the y-axis is Likelihood (0 to 1). The peak shows the best $\beta_0$ value for an accurate model.

### <span style="color: #FF8C00;">Example</span>

If a student studied for $x = 4$ hours and the model predicts $P = 0.5$:
- If $y = 1$ (pass): Likelihood = $0.5$.
- If $y = 0$ (fail): Likelihood = $0.5$.
A higher $P$ for the true label increases the likelihood, indicating better model fit.

---

## <span style="color: #228B22;">2. Log-Likelihood</span>

### <span style="color: #FF8C00;">Definition</span>

**`Log-Likelihood`** is the **natural logarithm** of the likelihood, transforming multiplication into addition for easier computation.

### <span style="color: #FF8C00;">Equation</span>

$$ \ln(L) = \sum_{i=1}^n \left[ y_i \cdot \ln(P_i) + (1-y_i) \cdot \ln(1-P_i) \right] $$

### <span style="color: #FF8C00;">Range</span>

- From $-\infty$ to 0.
- Close to 0 = good model.
- Large negative = poor model.

### <span style="color: #FF8C00;">Graph</span>

> ⚠️ **Note:** Log-Likelihood is similar to Likelihood but with negative values.
> 
> ![Image 2: Loss Function Graph](https://i.imgur.com/YBiigO6.png)

---

## <span style="color: #228B22;">3. Loss Function (Log Loss / Negative Log-Likelihood)</span>

### <span style="color: #FF8C00;">Definition</span>

The **Loss Function**, also known as **Log Loss** or **Negative Log-Likelihood**, is the negative of the log-likelihood. It is minimized by algorithms instead of maximizing the likelihood (`Minimizing the error`).

### <span style="color: #FF8C00;">Equation</span>

$$ \text{(Total cost) Loss} = - \ln(L) = - \sum_{i=1}^n \left[ y_i \cdot \ln(P_i) + (1-y_i) \cdot \ln(1-P_i) \right] $$


Normalized for the dataset:

$$ \text{(Cost function) Log Loss} = -\frac{1}{n} \sum_{i=1}^n \left[ y_i \ln(P_i) + (1 - y_i) \ln(1 - P_i) \right] $$

### <span style="color: #FF8C00;">Range</span>

- From 0 to $\infty$.
- Small value = good model.
- Large value = poor model.

### <span style="color: #FF8C00;">Connection to the Model</span>

The predicted probability $P_i$ is calculated using the sigmoid function:

$$ P_i = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_i)}} $$

Log Loss measures how far $P_i$ is from the true label $y_i$.

### <span style="color: #FF8C00;">Graph</span>

- **Shape:** U-shaped curve.
- **X-axis:** Values of $\beta_0$ (or $b$).
- **Y-axis:** Loss (0 to $\infty$).
- **Lowest point:** Best value for $\beta_0$.

![Image 2: Loss Function Graph](https://i.imgur.com/rOdqn2d.png)

**Image Description:** A graph showing Loss as a red U-shaped curve. The x-axis is $\beta_0$ values (-10 to 10), and the y-axis is Loss (0 to $\infty$). The lowest point is the best $\beta_0$ value.

---

## <span style="color: #228B22;">4. Odds</span>

### <span style="color: #FF8C00;">Definition</span>

**Odds** is the ratio of the probability of an event `happening` to the probability of it `not happening`.

### <span style="color: #FF8C00;">Equation</span>

$$ \text{Odds} = \frac{P}{1-P} $$

### <span style="color: #FF8C00;">Range</span>

- From 0 to $\infty$.
- High Odds = high probability.
- Low Odds = low probability.

### <span style="color: #FF8C00;">Interpretation</span>

| Probability | Odds | Meaning |
|-------------|------|---------|
| $P = 0$     | 0    | Event is impossible. |
| $0 < P < 1$ | $0 < \text{Odds} < \infty$ | Odds are positive real values. |
| $P = 1$     | $\infty$ | Event is certain. |

### <span style="color: #FF8C00;">Examples</span>

- **Equal Chance**: If a student’s chance of passing is $P = 0.5$:
  $$ \text{Odds} = \frac{0.5}{0.5} = 1 $$
  **Meaning**: Passing and failing are equally likely.

- **Less Likely**: If the chance of rain is $P = 0.2$:
  $$ \text{Odds} = \frac{0.2}{0.8} = 0.25 $$
  **Meaning**: Rain is 4 times less likely than no rain.

- **More Likely**: If a football team’s chance of winning is $P = 0.8$:
  $$ \text{Odds} = \frac{0.8}{0.2} = 4 $$
  **Meaning**: Winning is 4 times more likely than losing.

- **Logistic Regression Example**: If $P = 0.75$:
  $$ \text{Odds} = \frac{0.75}{0.25} = 3 $$
  **Meaning**: The event is 3 times more likely to occur than not.

> ⚠️ **Note :** Odds are represent as a Exponential distribution 
> 
>  ![Odds VS EXP_Func](https://i.imgur.com/IMvfOku.png)
>  
> 👉 **Logistic Regression** deal with a `Linear Line` and the **problem** on using Odds for logistic regression is the distribution of odds `Exponential`
> 
> 👉 **Log Odds** solve this problem as the distribution became **linear line**
> 
>  ![Odds VS Log Odds](https://i.imgur.com/cVKeYPY.png)

---

## <span style="color: #228B22;">5. Log Odds</span>

### <span style="color: #FF8C00;">Definition</span>

**Log Odds** is the natural logarithm of the odds, directly modeled in logistic regression.

### <span style="color: #FF8C00;">Equation</span>

$$ \text{Log Odds} = \ln\left(\frac{P}{1-P}\right) = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots $$

This is converted to probability using the sigmoid function:

$$ P = \frac{1}{1 + e^{-(\text{Log Odds})}} $$

### <span style="color: #FF8C00;">Range</span>

- From $-\infty$ to $\infty$.
- Positive = $P > 0.5$.
- Negative = $P < 0.5$.
- Zero = $P = 0.5$.

### <span style="color: #FF8C00;">Interpretation</span>

- If $P = 0.5$: Log Odds = $\ln(1) = 0$.
- If $P = 0.731$: Log Odds $\approx \ln(2.718) \approx 1$.
- If $P > 0.5$: Log Odds > 0.
- If $P < 0.5$: Log Odds < 0.

### <span style="color: #FF8C00;">In Logistic Regression</span>

Log odds are modeled as a linear equation:

$$ \ln\left(\frac{P}{1-P}\right) = \beta_0 + \beta_1 x $$

The odds are an exponential transformation:

$$ \frac{P}{1-P} = e^{\beta_0 + \beta_1 x} $$

---

## <span style="color: #228B22;">6. Role of Parameters $\beta_0$ and $\beta_1$</span>

### <span style="color: #FF8C00;">Definition</span>

- $\beta_0$ (or $b$): The **intercept** in the logistic regression equation.
- $\beta_1$ (or $a$): The **coefficient** for the input variable $x$.

Equation:

$$ \text{Log Odds} = \beta_0 + \beta_1 x $$

### <span style="color: #FF8C00;">Role of $\beta_0$</span>

1. **Starting Point**: Log Odds when $x = 0$:
   $$ P = \frac{1}{1 + e^{-\beta_0}} $$
2. **Adjusts Curve**: Shifts the sigmoid curve.
3. **Bias**: Reflects the natural tendency of the data.

### <span style="color: #FF8C00;">Role of $\beta_1$</span>

- Determines the **slope** of the log odds with respect to $x$.
- Affects how quickly the probability changes as $x$ increases.

### <span style="color: #FF8C00;">In Graphs</span>

- The x-axis in Likelihood and Loss graphs represents $\beta_0$ values.
- Peak in Likelihood = lowest point in Loss = best $\beta_0$.

![B0 & B1](https://i.imgur.com/4NQWB5X.png)

---

## <span style="color: #228B22;">7. Gradient Descent</span>

### <span style="color: #FF8C00;">Definition</span>

**Gradient Descent** is an algorithm that adjusts parameters ($\beta_0$, $\beta_1$) to minimize the Loss (Log Loss).

### <span style="color: #FF8C00;">How It Works</span>

1. Start with random values for $\beta_0$ and $\beta_1$.
2. Calculate the gradient:
   $$ \frac{\partial \text{Loss}}{\partial \beta_0} = \sum_{i=1}^n (P_i - y_i) $$
   $$ \frac{\partial \text{Loss}}{\partial \beta_1} = \sum_{i=1}^n (P_i - y_i) x_i $$
3. Update parameters:
   $$ \beta_0 \gets \beta_0 - \eta \cdot \frac{\partial \text{Loss}}{\partial \beta_0} $$
   $$ \beta_1 \gets \beta_1 - \eta \cdot \frac{\partial \text{Loss}}{\partial \beta_1} $$
   where $\eta$ is the learning rate.
4. Repeat until Loss stabilizes.

### <span style="color: #FF8C00;">Graphs</span>

- **Gradient Descent Graph (Collage):**
  - **Shape:** Red U-shaped curve with moving blue dots for each step.
  - **X-axis:** $\beta_0$ values.
  - **Y-axis:** Loss.

![Image 3: Gradient Descent Collage](https://i.imgur.com/I4c0Wka.png)

**Image Description:** A collage of 7 images. Each shows the Loss Function (red U-shaped curve) with blue dots marking $\beta_0$ at specific steps (e.g., steps 0, 2, 5, 8, 12, 16, 20). The x-axis is $\beta_0$ (-10 to 10), and the y-axis is Loss (0 to $\infty$). It shows $\beta_0$ moving from a random value (e.g., $\beta_0=-5$) to the best value (e.g., $\beta_0=2$).
**Notes:** Run the code in Section 11.2 in Jupyter Notebook to generate the images and collage, saving as `gradient_descent_collage.png`.

- **Loss vs. Steps Graph (Collage):**
  - **Shape:** Blue curve decreasing gradually.
  - **X-axis:** Number of steps (iterations).
  - **Y-axis:** Loss.

![Image 4: Loss vs. Steps Collage](https://i.imgur.com/pZlqodI.png)
**Image Description:** A collage of 7 images. Each shows the Loss curve (blue) up to a specific step (e.g., steps 0, 2, 5, 8, 12, 16, 20). The x-axis is steps (0 to 20), and the y-axis is Loss. It shows Loss decreasing until it stabilizes at a small value.
**Notes:** Run the code in Section 11.2 in Jupyter Notebook to generate the images and collage, saving as `loss_vs_iterations_collage.png`.

---

## <span style="color: #228B22;">8. Odds vs. Log Odds in Logistic Regression</span>

### <span style="color: #FF8C00;">Comparison</span>

| Concept      | Formula            | Scale           | Interpretation               |
|--------------|--------------------|-----------------|------------------------------|
| **Odds**     | $P/(1 - P)$        | 0 to $\infty$   | Ratio of success to failure. |
| **Log Odds** | $\ln(P/(1 - P))$   | $-\infty$ to $\infty$ | Linear for modeling.         |

### <span style="color: #FF8C00;">How Odds Describe Data Points</span>

For each data point, odds express the relative likelihood of the positive outcome:

$$ \frac{P_i}{1 - P_i} = e^{\beta_0 + \beta_1 x_i} $$

### <span style="color: #FF8C00;">Why Odds Are Not the Line</span>

**Misconception**: The odds $\frac{P}{1-P}$ might be thought to equal the linear model.

**Correction**: The model is linear for **log odds**:

$$ \ln\left(\frac{P}{1-P}\right) = \beta_0 + \beta_1 x $$

The odds are exponential:

$$ \frac{P}{1-P} = e^{\beta_0 + \beta_1 x} $$

The probability is derived via the sigmoid function:

$$ P = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x)}} $$

---

## <span style="color: #228B22;">9. Connecting Concepts to Logistic Regression</span>

### <span style="color: #FF8C00;">Relationships</span>

1. **Odds and Log Odds**: The model calculates log odds ($\beta_0 + \beta_1 x$), then converts to probabilities using the sigmoid function.
2. **Likelihood and Log-Likelihood**: Likelihood measures model fit, and log-likelihood simplifies calculations.
3. **Loss (Log Loss)**: Negative log-likelihood, minimized to optimize the model.
4. **Parameters $\beta_0$ and $\beta_1$**: $\beta_0$ sets the starting point for log odds, and $\beta_1$ adjusts the slope.
5. **Gradient Descent**: Adjusts $\beta_0$ and $\beta_1$ to minimize Loss and maximize Likelihood.

### <span style="color: #FF8C00;">How They Work Together</span>

- The model computes log odds, then probabilities ($P_i$).
- Likelihood and Log Loss are calculated based on $P_i$ and $y_i$.
- Gradient Descent adjusts $\beta_0$ and $\beta_1$ to minimize Log Loss (maximize Likelihood).

---

## <span style="color: #228B22;">10. Practical Examples</span>

### <span style="color: #FF8C00;">Example 1: Fake Data</span>

- **Data**: $x = [1, 2, 3, 4]$, $y = [0, 0, 1, 1]$.
- If $\beta_0 = 2$: Loss is small, probabilities are accurate.
- If $\beta_0 = -5$: Loss is large.
- Gradient Descent moves $\beta_0$ toward 2.

### <span style="color: #FF8C00;">Example 2: Student Exam</span>

- **Scenario**: Predict if a student passes ($y = 1$) or fails ($y = 0$) based on hours studied ($x$).
- **Model**: $\ln\left(\frac{P}{1-P}\right) = -2 + 0.5 x$.
- For $x = 4$ hours:
  - Log Odds = $-2 + 0.5 \cdot 4 = 0$.
  - Odds = $e^0 = 1$.
  - Probability = $\frac{1}{1 + e^0} = 0.5$.
  - **Interpretation**: Equal chance of passing or failing.
- If the student passes ($y = 1$), Likelihood = $0.5$; if fails ($y = 0$), Likelihood = $0.5$.

### <span style="color: #FF8C00;">Example 3: Odds and Log Odds</span>

- If $P = 0.75$:
  $$ \text{Odds} = \frac{0.75}{0.25} = 3, \quad \text{Log Odds} = \ln(3) \approx 1.099 $$
- If $P = 0.731$:
  $$ \text{Odds} \approx 2.718, \quad \text{Log Odds} \approx \ln(2.718) \approx 1 $$

---

## <span style="color: #228B22;">11. Conclusion</span>

- **Logistic Regression** models log odds ($\beta_0 + \beta_1 x$), which are converted to probabilities via the sigmoid function.
- **Likelihood** and **Log-Likelihood** measure how well the model fits the data.
- **Log Loss** (Negative Log-Likelihood) is minimized to optimize the model.
- **Odds** and **Log Odds** describe the relative likelihood of outcomes, with log odds being linear for modeling.
- **Parameters $\beta_0$ and $\beta_1$** define the starting point and slope of the log odds.
- **Gradient Descent** adjusts parameters to minimize Log Loss, improving model accuracy.
- Visualizations (collages) illustrate how $\beta_0$ moves on the Loss Function and how Loss decreases over iterations.
- The student exam example shows how these concepts apply to real-world predictions.

---