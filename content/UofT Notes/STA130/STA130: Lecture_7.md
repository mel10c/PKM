# Linear Regression

## Visualizing between 2 or more variables

- <u>Scatterplot</u> - the **position** of each point is determined by the values of two numerical variables: one on the horizontal (x) axis, the other on the vertical (y) axis (one point for each observation)

### Features of the association between the two numerical variables

- **<u>Form</u>** - describes the pattern that the two variables follow together

  > Ex. Linear, non-linear, quadratic, exponential...

- **<u>Direction</u>**

  - ***Positive association*** - values of one variable tend to increase as the other's increase
  - ***Negative association*** - values of one variable tend to decrease as the other's increase

- **<u>Strength</u>** - describes how concentrated the values of the variable are around the *pattern*

  - Strong, moderate, weak

```R
<data_set> %>% ggplot(aes(x=<variable_1>, y=<variable_2>)) + 
	geom_point() +
	labs(x = "Name of x-axis (unit)",
         y = "Name of y-axis (unit)") +
	theme_minimal()  # optional, makes the backgroun white
```

#### Example of the `heights` dataset

- `heights` - the name of the dataset in use (<data_set>)
- `shoePrint` - the name of the numerical variable you want to display on the x-axis (<variable_1>)
- `height` - the name of the numerical variable you want to display on the y-axis (<variable_2>)

### Visualizing the numerical variable with categorical variable

1. Add `ggplot(aes(... color = <varaible_3>))` displays each point based on the value of the categorial variable 

   > Ex. `ggplot(aes(... color = sex))` 
   > <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gofbhw7hboj30te0meq73.jpg" alt="Screen Shot 2021-03-10 at 12.20.42" style="zoom:20%;" />

2. Use `facet_wrap()`, and specify the name of a categorial variable, then would get a separate plot for each value of this variable (2 cases) (Can create side-by-side histograms or barplots...)

   > Ex. `facet_wrap(~sex)` 
   > <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gofbhy1729j30y80pitef.jpg" alt="Screen Shot 2021-03-10 at 12.20.47" style="zoom:20%;" />

- Its a good idea to try both cases and see which one is more effective representation

## Quantifying association: correlation

- <u>Correlation</u> summarizes the **strength** and **direction** of the **linear** relationship between two numerical variables (non-linear relationship is not represented in correlation)

- <u>Sample correlation</u> between variables $x, y$ for $n$ observations $(x_1, y_1) \dots (x_n, y_n)$:
  $$
  r = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}
  {\sum_{i=1}^n (x_i - \bar{x})^2 \cdot \sum_{i=1}^n (y_i - \bar{y})^2}
  $$
  
- The *sign* of $r$ gives the **direction** ($r>0$ - positive, $r<0$ - negative)
  - The *magnitude* of $r$ is a measure of the **strength of the leaner association**
    - $-1 \le r \le 1$
    - $r = \pm 1$ If and only if there is a *perfect* linear relationship between $x$ and $y$
  
> ```R
  > cor(x = heights$shoePrint,  # '$' exrtract a column vector from a tibble
  >  	y = heights$height)
  > 
  > ## [1] 0.812948
  > ```
  >
  > The correlation between shoe print length and height in this sample of 40 individuals is 0.081

## Linear Regression Models

### 1: Numerical predictor

- Goal of linear regression: understand variation, predict pattern (both needs a **model**)

- <u>[[Simple linear regression]] model</u> - assumes there is a "best" straight line that explains the real relationship between $x$ and $y$ and that the values observed randomly deviate from this line
  $$
  Y_i = (\beta_0 + \beta_1 x_i) + \epsilon_i
  $$
  
- $Y_1$ - response variable (or dependent variable, target variable...) for observation $i$
  
  - Values are random, and observed in the sample data
  
- $x_i$ - independent variable (or predictor, covariate, feature, input...) for observation $i$
  
  - Fixed (constant) and observed in sample data
  
- $\beta_0$ - intercept parameter (closed-form math expression for estimated regression coefficient)
    $$
    \hat{\beta}_0 = \bar{y} - \hat{\beta}_1 \bar{x}
    $$
  
- $\beta_1$ - slope parameter (closed-form math expression for estimated regression coefficient)
    $$
    \hat{\beta}_1 =
    \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}
    {\sum_{i=1}^n (x_i - \tilde{x})^2}
    $$
  
  - Both $\beta$ are fixed (constants) but unknown
  
- $\epsilon_i$ - random error term for observation $i$ (random deviation)
  
  - Random, but cannot be calculated directly (don't know true value of $\beta_0, \beta_1$) 
  - $\epsilon_i = y_i - \hat{y}_i$
  
- *Population* regression is unknown, need to **estimate** a line in which is as close as possible to as many points as possible in the sample

  - Most common approach is to define *the sum of squared vertical differences between each observation and the fitted (estimated) line*
  - <u>Least Squares Regression Line</u> - the straight line which *minimizes* the sum of squared vertical distances between each point and the fitted line (compared to all other possible straight lines)

- Use `lm()` function to fit a linear regression model

  -  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gofavwv52yj30gy032dg4.jpg" alt="Screen Shot 2021-03-07 at 02.13.07" style="zoom:50%;" />

  > ```R
  > model1 <- lm(height ~ shoePrint, data= heights)
  > summary(model1)$coefficients
  > 
  > ##				Estimate	Std. Error	t-value		Pr(>|t|)
  > ## (Intercept)	80.930409	10.8933945	7.429310	6.504368e-09
  > ## shoePrint	3.218561	0.3740081	8.605591	1.863474e-10
  > ```
  >
  > - `(Intercept)` is the **estimate** of $\beta_0$ (ie,  $\hat{\beta}_0$)
  > - `shoePrint` is the **estimated** of $\beta_1$ (ie. $\hat{\beta}_1$)

- ```R
  geom_smooth(method="lm", se=FALSE)
  ```

  - To add the fitted regression line to a plot
  - <img src="https://tva1.sinaimg.cn/large/008eGmZEly1goboskfhatj30j20fqdhz.jpg" alt="Screen Shot 2021-03-07 at 08.59.05" style="zoom:30%;" />

#### Interpretation of regression coefficients

- The estimated simple regression of $y$ on $x$ is: (<u>fitted regression line</u> or <u>fitted regression equation</u>) 
  $$
  \hat{y} = \hat{\beta}_0 + \hat{\beta}_1x
  $$
  
- $\hat{y}$ Is the <u>fitted value</u> or the <u>predicted value</u> is the estimated average value of $y$ when the predictor is equal to $x$
  - The *slope* $\hat{\beta}_1$ is the average change in $y$ for 1-unit change in $x$
  - The *intercept* $\hat{\beta}_0$ is the average of $y$ when $x=0$ (often this doesn't make sense, but it tells use the height of the line)
  - The difference between the observed and predicted value of $y$ for the $i^{th}$ observation is called the <u>residual</u> ($e_i = y_i - \hat{y}_i$) [distance between the point and the estimated line]
  
- **In general, it is not ok to say that a change in the predictor $x$ *causes* a change in $y$. It is only ok to talk about the association observed**

  > ##### Suppose you wake up to find that your bike has been stolen, but there is a fresh shoeprint in the mud nearby. You measure it and it is 30cm long. Based on this fitted regression model, how tall would you predict that the person who left the shoeprint was?
  >
  > General equation for the fitted line: ($\ref{ref3}$)
  > $$
  > \begin{align*}
  > \hat{\text{height}} &= (\text{intercept }cm) + (\text{slope}) \cdot 
  > (\text{length of shoeprint }cm) \\
  > \hat{y} &= 80.930409 cm + 3.218561 \times (30 cm) \\
  > \hat{y} &= 177.48cm
  > \end{align*}
  > $$

- <u>Extrapolation</u> - means trying to predict the response variable for values of the explanatory variable beyond those contained in the data 

  - A model is only as good as the data it was trained on
  - NO reason to think that the trend for the observed range would be valid outside of the range

- The coefficient of determination ($R^2$) is the proportion of the variability in $y$ which is explain by the fitted regression model
  $$
  R^2 = \frac{\sum_{i=1}^n (y_i - \bar{y})^2 - \sum_{i=1}^n (y_i - \hat{y}^2_i)}
  {\sum_{i=1}^n (y_i - \bar{y})^2} = 
  1 - \frac{\sum_{i=1}^n (y_i - \hat{y}_i)}{\sum_{i=1}^n (y_i - \bar{y})^2}
  $$

  - $R^2$ close to 1 indicates that most of the variability in $y$ is explain by the regression model
  - $R^2$ close to 0 indicates that very little of the variability in $y$ is explained by the regression model
  - Conveniently $R^2$ is equal to the square of the correlation $r$ ($\ref{ref1}$)

  ```R
  summary(model1)$r.squared
  ## [1] 0.6608845
  cor(x = height$shoePrint, y = heights$height)^2
  ## [1] 0.6608845
  ```

### 2: Categorical predictor

- For the equation for a simple regression line with one numerical predictor: ($\ref{ref2}$), for categorical data, the $x_i$ value needs a <u>indicator variable</u> to encode the categorial data
  $$
  x_i = I(\text{individual $i$ is male}) = 
  \left\{\begin{matrix}
  1 & \text{if }individual~ i~ is male \\
  0 & \text{if }individual~ i~ is female
  \end{matrix}\right.
  $$
  This also needs a <u>baseline value</u> (the level corresponding to $x=0$), here F(female) is the value
  
> ```R
  > model2 <- lm(height ~ sex, data= heights)
  > summary(model2)$coefficients
  > 
  > ##				Estimate	Std. Error	t-value		Pr(>|t|)
  > ## (Intercept)	166.82381	1.357760	122.866909	5.085412e-51
  > ## sexM			15.79198	1.970046	8.016048	1.085391e-09
  > ```
  >
  > - `(Intercept)` is the **estimate** of $\beta_0$ (ie,  $\hat{\beta}_0$)
  > - `sexM` is the **estimated** of $\beta_1$ (ie. $\hat{\beta}_1$)

#### Intrerpreting $\hat{\beta}_0$ and $\hat{\beta}_1$

- Combining the equation ($\ref{ref3}$) and equation ($\ref{ref4}$), get:
  - When $x=0$, have $\hat{y} = \hat{\beta}_0 + \hat{\beta}_1 \times 0 = \hat{\beta}_0$, implies this is the predicted value of $y$ for individuals with $x=0$ (in ex. $\hat{\beta}_0$ Is the predicted height for women)
  - When $x=1$, have $\hat{y} = \hat{\beta}_0 + \hat{\beta}_1 \times 1 = \hat{\beta}_0 + \hat{\beta}_1$, implies that this is the predicted value of $y$ for individuals with $x=1$ 
  - $\hat{\beta}_1$ Is the average *differences* in the response variable $y$ between the two categories

## Inference for Simple Linear Regression

- Fitted regression line: $\hat{Y} = \hat{\beta}_0 + \hat{\beta}_1 x$ (similar to $\ref{ref3}$)
- However, the estimates $(\hat{\beta}_0, \hat{\beta}_1)$ does not equal to the Tre parameter values $(\beta_0, \beta_1)$ 
  - The estimation is based on the sample data, so they are subject tot sampling variability

- For the linear model ($\ref{ref2}$), write a pair of hypotheses to test if the slope parameter in this regression model is different from 0
  - $H_0: \beta_1 = 0$ 	vs 	$H_A: \beta_1 \neq 0$
  - Under the linear model, if the slope parameter is 0, then $x$ does not predict $y$, then predicting the sample mean of $y$ for all observation is fine; If the slope ($\beta_1$) is different from 0, then knowing $x$ does help to better predict $y$

### Assumptions for statistical inference on regression coefficients

> In STA130, these assumptions did not need to be verified before doing the inference

- The p-values in the output of `lm()` is based on the *Student's distribution* (a continuous probability distribution). So for this to be value, need to make a few assumptions
  1. There is a linear association between $x,y$
  2. Constant variance in $y$ for all values of $x$ (scatterplot is not cone-shaped)
  3. The observations are independent
  4. The residual follow a normal distribution

- If one or more assumptions above is not reasonable, then the inference may not be valid

### Using `R` for hypothesis testing

- `R` auto gives the p-value for hypothesis test of the form $H_0: \beta_1 = 0$ 	vs 	$H_A: \beta_1 \neq 0$ 

  - P-value is the `Pr(>|t|)` in the code above (view code for `model1`)

  > In the example for `model1`, the p-value is very small (p-value < $1.86 \times 10^{-10}$), then this indicates there is *very* strong evidence gains the null hypothesis.

---

- Advantage of randomization test 
  - NO assumptions about the distribution of the data
  - More flexible (can be used to compare any statistic across two groups, [not just mean])
- Advantage of linear regression approach
  - Only requires 1 (or 2) lines of code (but only valid *if* the assumptions are valid)