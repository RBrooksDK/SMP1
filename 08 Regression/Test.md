# Calculating Metrics in Simple Linear Regression

## The Slope (and intercept)

In simple linear regression, the slope parameter (often denoted as $\beta_1$) represents the relationship between the independent variable (X) and the dependent variable (Y). The slope indicates how much the dependent variable is expected to increase (or decrease) for a one-unit increase in the independent variable. There are several ways to compute this slope, and here are some of the key methods:

### Least Squares Estimation:
   The most common method for calculating the slope in simple linear regression is the least squares estimation. The formula for the slope ($\beta_1$) using this method is:
   
   $$\boxed{
   \beta_1 = \frac{\sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})}{\sum_{i=1}^n (x_i - \overline{x})^2}}
   $$

   In this expression:
- $\sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})$ is the sum of the products of the deviations of $x$ and $y$ from their respective means. This term captures the covariance between $x$ and $y$, indicating how much $x$ and $y$ vary together from their mean values (though excluding $\frac{1}{n-1}$). This term is often denoted $S_{xy}$.
- $\overline{x}$ and $\overline{y}$ are the means of $x$ and $y$, respectively. These are calculated as $\overline{x} = \frac{1}{n} \sum_{i=1}^n x_i$ and $\overline{y} = \frac{1}{n} \sum_{i=1}^n y_i$, where $n$ is the number of observations.
- $\sum_{i=1}^n (x_i - \overline{x})^2$ represents the sum of the squares of the deviations of $x$ from its mean. This term is a measure of the total variance in $x$ and helps normalize the covariance in the numerator. This term is often denoted $S_{xy}$.
- $n$ is the number of observations, indicating the total number of data points in the dataset.

### Sum of Products
The fundamental expression for the slope is the one stated above. But we can also use the sum of products which is demonstrated here.

*Derivation of $(S_{xy})$*

The regular form for the sum of products of deviations for $x$ and $y$ is:
$$
S_{xy} = \sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})
$$

Expanding this sum:
$$
S_{xy} = \sum_{i=1}^n (x_i y_i - x_i \overline{y} - y_i \overline{x} + \overline{x} \overline{y})
$$

Simplifying this by distributing the summation:
$$
S_{xy} = \sum_{i=1}^n x_i y_i - \sum_{i=1}^n x_i \overline{y} - \sum_{i=1}^n y_i \overline{x} + n \overline{x} \overline{y}
$$

Notice that $\sum_{i=1}^n x_i \overline{y} $ can be rewritten because $\overline{y}$ is a constant:
$$
\sum_{i=1}^n x_i \overline{y} = \overline{y} \sum_{i=1}^n x_i
$$
And similarly for $\sum_{i=1}^n y_i \overline{x}$:
$$
\sum_{i=1}^n y_i \overline{x} = \overline{x} \sum_{i=1}^n y_i
$$

Since $\sum_{i=1}^n x_i = n \overline{x}$ and $\sum_{i=1}^n y_i = n \overline{y}$, the terms simplify to:
 $$
S_{xy} = \sum_{i=1}^n x_i y_i - n \overline{x} \overline{y}
$$

*Derivation of $S_{xx}$*

The regular form for the sum of squares of deviations for $ x $ is:
$$
S_{xx} = \sum_{i=1}^n (x_i - \overline{x})^2
$$

Expanding this sum:
$$
S_{xx} = \sum_{i=1}^n (x_i^2 - 2x_i \overline{x} + \overline{x}^2)
$$

Simplifying this by distributing the summation:
$$
S_{xx} = \sum_{i=1}^n x_i^2 - 2\overline{x} \sum_{i=1}^n x_i + n\overline{x}^2
$$

Since $\sum_{i=1}^n x_i = n\overline{x}$:
$$
S_{xx} = \sum_{i=1}^n x_i^2 - 2n\overline{x}^2 + n\overline{x}^2
$$

Combining the terms results in:
 $$
S_{xx} = \sum_{i=1}^n x_i^2 - n\overline{x}^2
$$

These derivations provide a clear mathematical pathway from the traditional definitions of $ S_{xy} $ and $ S_{xx} $ to the forms that are easily implemented in a python script for instance, and also means we can also formulate the slope as:

 $$\boxed{
\beta_1 = \frac{S_{xy}}{S_{xx}} = \frac{\sum_{i=1}^n x_i y_i - n \overline{x} \overline{y}}{\sum_{i=1}^n x_i^2 - n\overline{x}^2}}
$$




### Breakdown Using Individual Sum Terms

Another way to express this is by explicitly calculating the sums:

$$\boxed{
\beta_1=\frac{n \sum\left(x_i y_i\right)-\sum x_i \sum y_i}{n \sum\left(x_i^2\right)-\left(\sum x_i\right)^2}}
$$

In this expression:
- $n$ is the number of observations.,
- $\sum\left(x_i y_i\right)$ is the sum of the products of corresponding $x$ and $y$ values,
- $\sum x_i$ and $\sum y_i$ are the sums of $x$ and $y$ values, respectively,
- $\sum\left(x_i^2\right)$ is the sum of the squares of $x$ values.

### Covariance and Variance Method:
   This is essentially a rearrangement of the least squares formula, emphasizing the use of covariance and variance:
   $$\boxed{
   \beta_1 = \frac{\text{Cov}(X, Y)}{\text{Var}(X)}}
   $$
   where:
- $\text{Cov}(X, Y) = \frac{\sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})}{n-1}$ (assuming a sample covariance)
- $\text{Var}(X) = \frac{\sum_{i=1}^n (x_i - \overline{x})^2}{n-1}$ (also assuming sample variance)

### Matrix Algebra (Using Normal Equation):
   When dealing with linear regression in matrix terms, the slope can be calculated using the normal equation:
   $$ \boxed{
   \beta = (X^T X)^{-1} X^T Y}
   $$
   Here, $X$ is the matrix of input features (including a column of ones for the intercept if it's included in the model), and $Y$ is the vector of output values, and $\beta$ is a vector that will contain all the coefficients.

### Gradient Descent:
   Though not a formula in the traditional sense, gradient descent is an algorithmic approach used to find the minimum of the cost function (typically mean squared error) in regression. The update rule in each iteration for $\beta_1$ would be:
   $$\boxed{
   \beta_1^{(new)} = \beta_1^{(old)} - \alpha \frac{\partial}{\partial \beta_1} MSE}
   $$
   where $\alpha$ is the learning rate and $\frac{\partial}{\partial \beta_1} MSE$ is the derivative of the mean squared error with respect to $\beta_1$.

## Regression Line Intercept Inclusion

We will also explain how the slope relates to the intercept in the regression equation, presented here as part of the full regression formula:

$$
y = \beta_0 + \beta_1 x
$$

where
$$
\beta_1 = \frac{\sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})}{\sum_{i=1}^n (x_i - \overline{x})^2}
$$
(or one of the alternatives from above) and
$$\boxed{
\beta_0 = \overline{y} - \beta_1 \overline{x}}
$$

## Correlation Coefficient ($r$) and Correlation of Determination ($r^2$)
This section will present different formulations of $r$ or $r^2$. Depending on the formulation, one or the other is shown.

### Pearson Correlation Coefficient ($r$)
The Pearson correlation coefficient ($r$) measures the linear correlation between two variables, $x$ and $y$. It is defined as the ratio of the covariance of the variables to the product of their standard deviations. Mathematically, it's expressed as:

$$\boxed{
r = \frac{\sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})}{\sqrt{\sum_{i=1}^n (x_i - \overline{x})^2 \sum_{i=1}^n (y_i - \overline{y})^2}} = \frac{S_{x y}}{\sqrt{S_{x x} \cdot S_{y y}}}}
$$

Here, $\overline{x}$ and $\overline{y}$ are the means of $x$ and $y$, respectively. This formula essentially scales the covariance between $x$ and $y$ by the product of their standard deviations, ensuring that $r$ is dimensionless and ranges between -1 and +1. Also note

### Coefficient of Determination ($r^2$)
The coefficient of determination, known as $r^2$, is the square of the Pearson correlation coefficient. It represents the proportion of the variance in the dependent variable that is predictable from the independent variable(s). It is calculated simply by squaring $r$:

$$\boxed{
r^2 = \left(\frac{\sum_{i=1}^n (x_i - \overline{x})(y_i - \overline{y})}{\sqrt{\sum_{i=1}^n (x_i - \overline{x})^2 \sum_{i=1}^n (y_i - \overline{y})^2}}\right)^2}
$$

This value ranges from 0 to 1, where 0 indicates no correlation and 1 indicates perfect correlation.

### Alternate Formulas for $r$ and $r^2$ in the Context of Regression
In the context of simple linear regression, where you have calculated the slope ($\beta_1$) and the intercept ($\beta_0$), $r$ and $r^2$ can also be calculated directly from the regression output:

#### Using Standard Deviations and Slope:
  $$\boxed{
  r = \beta_1 \frac{s_x}{s_y}}
  $$
  where $s_x$ and $s_y$ are the standard deviations of $x$ and $y$, respectively, and $\beta_1$ is the slope of the regression line. This formula derives from the relationship that the slope of the regression line in standardized units is the correlation coefficient. Note, $s_x = \sqrt{S_{xx}}$ and Note, $s_y = \sqrt{S_{yy}}$, in both cases omitting $\frac{1}{n-1}$.

#### From the Sum of Squares:
  $$\boxed{
  r^2 = \frac{SSR}{SST} = 1-\frac{SSE}{SST}}
  $$

  In regression analysis, the total sum of squares (SST), the regression sum of squares (SSR), and the sum of squares of errors (SSE) are important quantities for measuring the variability in the data and the performance of the regression model.

  - **Total Sum of Squares (SST)**

    The Total Sum of Squares measures the total variability of the dataset relative to the mean. It is calculated as:
    $$
    \text{SST} = \sum_{i=1}^n (y_i - \overline{y})^2
    $$
    where $y_i$ are the observed values and $\overline{y}$ is the mean of the $y$ values.

  - **Regression Sum of Squares (SSR)**

    The Regression Sum of Squares measures how much of the total variability in the dependent variable can be explained by the independent variable(s) in the model. It is calculated as:
    $$
    \text{SSR} = \sum_{i=1}^n (\hat{y}_i - \overline{y})^2
    $$
    where $\hat{y}_i$ are the predicted values from the regression model.

  - **Sum of Squares of Errors (SSE)**

    The Sum of Squares of Errors measures the variability of the model errors (residuals). It is calculated as:
    $$
    \text{SSE} = \sum_{i=1}^n (y_i - \hat{y}_i)^2
    $$
    where $y_i$ are the observed values and $\hat{y}_i$ are the predicted values from the regression model.

   These three components are related by the identity:
   $$
   \text{SST} = \text{SSR} + \text{SSE}
   $$
   This identity shows that the total variability in the dataset ($\text{SST}$) can be decomposed into the variability explained by the regression model ($\text{SSR}$) and the variability that is not explained by the model ($\text{SSE}$).

   Each of these formulas provides insight into different aspects of the regression analysis, such as the effectiveness of the model in explaining the variation in the data and the amount of error in the predictions.

#### From the $z$-scores:

The formula for calculating the Pearson correlation coefficient using standardized scores is:

$$\boxed{
r = \frac{\sum (z_x \cdot z_y)}{n-1}}
$$

where:
- $z_x = \frac{x - \overline{x}}{s_x}$ and $z_y = \frac{y - \overline{y}}{s_y}$ are the standardized scores of $x$ and $y$. 
- $\overline{x}$ and $\overline{y}$ are the means of $x$ and $y$, respectively.
- $s_x$ and $s_y$ are the standard deviations of $x$ and $y$, respectively.
- The numerator, $\sum (z_x \cdot z_y)$, represents the sum of the products of these standardized scores, effectively capturing the covariance of $x$ and $y$.
- The denominator, $n-1$, corrects for the bias in variance estimation from a sample, making the calculation an unbiased estimator of the population correlation coefficient.

This approach normalizes both variables to have zero mean and unit variance, simplifying the interpretation of the correlation coefficient as it directly measures the degree of linear relationship between the standardized versions of the original variables.

#### Breakdown Using Individual Sum Terms:

  $$\boxed{
  r = \frac{n \cdot \sum (x_i y_i) - \sum x_i \cdot \sum y_i}{\sqrt{n \cdot \sum x_i^2 - (\sum x_i)^2} \cdot \sqrt{n \cdot y_i^2 - (\sum y_i)^2}}}
  $$

  where:
  - $ \sum (x_i y_i) $ is the sum of the products of corresponding $ x $ and $ y $ values.
  - $ \sum x_i $ and $ \sum y_i $ are the sums of all $ x $ values and $ y $ values, respectively.
  - $ \sum x_i^2 $ and $ \sum y_i^2 $ are the sums of the squares of all $ x $ and $ y $ values, respectively.
  - The term $ n $ is the number of data points.

The denominator involves the square roots of the products of $ n $ and the sum of squares of $ x $ and $ y $, minus the square of the sum of $ x $ and $ y $ values, all scaled by $ n $. This structure follows the formula for the standard deviation, scaled to the sample size to adjust for bias, fitting the denominator of the correlation coefficient formula. This formula effectively measures the strength and direction of a linear relationship between two variables.

## Example: Exam 2020, Asignment 7:

**Problem:**

A professor in the School of Engineering in a university polled a dozen colleagues about the number of professional meetings they attended in the past five years $(x)$ and the number of papers they submitted to refereed journals $(y)$ during the same period. The summary data are given as follows:
$$
\begin{aligned}
n & =12, \quad \bar{x}=4, \quad \bar{y}=12 \\
\sum_{i=1}^n x_i^2 & =232, \quad \sum_{i=1}^n x_i y_i=318
\end{aligned}
$$

Fit a simple linear regression model between $x$ and $y$ by finding out the estimates of intercept and slope. Hint: Use the Least Squares Estimates formula from the book.

<details>
  <summary>Click here to see the solution</summary>

<p>Given the values, we can use one of the variations provided earlier:

$$
\beta_1 = \frac{\sum_{i=1}^n x_i y_i - n \overline{x} \overline{y}}{\sum_{i=1}^n x_i^2 - n \overline{x}^2}
$$

Let's plug in the values:

- $n = 12$
- $\overline{x} = 4$
- $\overline{y} = 12$
- $\sum_{i=1}^n x_i^2 = 232$
- $\sum_{i=1}^n x_i y_i = 318$

Calculating $\beta_1$:

$$
\beta_1 = \frac{318 - 12 \times 4 \times 12}{232 - 12 \times 4^2}
$$

In the solution, the following formula, also presented above, is used:

$$
\beta_1=\frac{n \sum\left(x_i y_i\right)-\sum x_i \sum y_i}{n \sum\left(x_i^2\right)-\left(\sum x_i\right)^2}
$$

Plugging these values into the formula:
$$
\beta_1=\frac{(12)(318)-[(12)(4)][(12)(12)]}{(12)(232)-[(12)(4)]^2}
$$


Once we have $\beta_1$, we can calculate the intercept $\beta_0$ using the formula:

$$
\beta_0 = \overline{y} - \beta_1 \overline{x}
$$

We'll compute $\beta_1$ first and then use it to find $\beta_0$.

Using the provided data, the estimated parameters for your linear regression model are:

- Slope ($\beta_1$): $-6.45$
- Intercept ($\beta_0$): $37.8$

Thus, the fitted linear regression model can be expressed as:
$$
y = 37.8 - 6.45x
$$
This equation predicts the value of $y$ based on the value of $x$, with the model suggesting that $y$ decreases by approximately 6.45 units for every one unit increase in $x$.</p>

</details>
