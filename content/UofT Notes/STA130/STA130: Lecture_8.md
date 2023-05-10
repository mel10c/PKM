# Multiple L.R. and Assessing Prediction models

### Branches of statistical inference

- <u>Testing</u> - a **hypothesis test** evaluates evidence against a particular value for a parameter
  - Hypothesis test for one proportion
  - Randomization test to compare the values of a parameter across two groups
- <u>Estimation</u> - **confidence interval** estimating a parameter (gives a range of plausible values for a parameter)
  - Bootstrap confidence interval
- <u>Prediction</u> - predict value of a variable for an observation using a statistical model based on other variables 
  - Simple linear regression (one predictor) -- useful when response $y$ is numerical
  - Multiple linear regression (multiple predictors) -- useful when response $y$ is numerical
  - Classification trees - [next lecture] -- useful when response $y$ is categorical

## Measuring and assessing prediction accuracy

### Strategy

1. Randomly divide the sample data into "training" and "testing" datasets

   > Ex: 80% for training and 20% for testing

2. Fit the prediction model based on the training data

3. Run the "test" data through the fitted prediction model & look at how accurate the prediction model was

- When fit a prediction model, it uses the $(x_i, y_i)$ pair of observations sets to get to the estimations of the regression coefficient $\hat{\beta}$. Therefore it would me more *fair* to use a different observation set for **fitting (or building** and **testing** a prediction model

- The Root Mean Squared Error (**RMSE**) measure can help to summarize the "accuracy" of the prediction. More specifically, it **measures prediction error for predictions from a linear regression model.**
  $$
  RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
  $$
  It can be used to compare different sizes of datasets (as long as they are all in the same unit) and to compare different models not he same dataset

- `rowid_to_column()` - the "index" for data in a dataset, a built-in `tydiverse` function
- `%in%` - a function that filter whether an element in found in a dataset
- `predict(<model_name>, newdata = <prediction_data>)` - make prediction for new observations

> ##### R Code to create training and testing datasets & make predictions using a fitted regression model
>
> ```R
> library(tidyverse)
> heights <- read.csv("heights.csv") %>% select(-X)
> 
> set.seed(123);
> n <- nrow(heights)  # number of observations in heights data (40)
> 
> # Pick 80% of observations to go into the training dataset (32 out of 40)
> training_indices <- sample(1:n, size=round(0.8*n)) 
> # Add a column caled "rowid" to our heights tibble
> heights <- heights %>% rowid_to_column()
> 
> # Create training dataset
> train <- heights %>% filter(rowid %in% training_indices)
> # Testing dataset includes all observations NOT in the training data
> test <- heights %>% filter(!(rowid %in% training_indicces))
> 
> # Build model using the training data only
> model <- lm(height ~ shoePrint, data = train)
> 
> # Make predictions for test data using the training model
> y_hat_test <- predict(model, newdata = test)
> y_test <- test$height
> 
> # Calculate RMSE for prediction in the test dataset
> sqrt( sum( (y_test - y_hat_test)^2) / nrow(test) )
> ```

### Interpretation and purpose of the RMSE

- A small value of RMSE indicates that on average, the predictions for the response are close to the true (observed) values. (**small implies good prediction accuracy**)
- The coefficient of determination $R^2$ only tells the proportion fo variability in $y$, not does not directly indicates the accuracy of the predictions

| $R^2$                                                        | $RMSE$                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| $1 - \frac{\sum_{i=1}^n (y_i - \hat{y}_i)}{\sum_{i=1}^n (y_i - \bar{y})^2}$ | $\sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$ |
| Range: 0 to 1                                                | Range: 0 to infinity                                    |
| **Larger** value indicates larger proportion of <br />variation of the response explained by the model | **Smaller** value indicates better prediction accuracy  |
| No units                                                     | Same units as $y$ (the response variable)               |

## Multiple linear regression: Building richer prediction models

### Parallel lines

- Linear regression models with 2 (or more) predictors, these predictors can be numerical or categorial 
  $$
  y_i = \beta_0 + \beta_1 x_{1i} + \beta_2 x_{2i} + \dots + \epsilon_i
  $$
  Where $x_{1i}$ is the first predictor, and $x_{2i}$ is the second predictor

  - Fitted line for predictor 1 (assume $x_{2i}$ is categorical):     $\hat{y}_i = \hat{\beta}_0 +\hat{\beta}_2 x_{1i} + \hat{\beta}_2 (0)  = \hat{\beta}_0 + \hat{\beta}_1 x_{1i}$ 
  - Fitted line for predictor 2 (assume $x_{2i}$ is categorical): $\hat{y}_i = \hat{\beta}_0 +\hat{\beta}_2 x_{1i} + \hat{\beta}_2 (1)  = (\hat{\beta}_0 + \hat{\beta}_2) + \hat{\beta}_1 x_{1i}$ 
  - Equation for the regression line:     $\hat{y}_i = \hat{\beta}_0 +\hat{\beta}_2 x_{1i} + \hat{\beta}_2  x_{2i} $ 
  
- The second variable would produce multiple parallel lines (**common slope** of $\hat{\beta}_1$), different intercepts

  - Intercept for predictor 2 is $\hat{\beta}_0 + \hat{\beta}_2$; **difference** between the two predictor is $\hat{\beta}_2$

- New functions to plot multiple lines in `R`

  - The `augment(model_name)` functions from the `broom` library creates a data frame with **predicted values** (named the `.fitted` column), residuals, etc

```R
# Fitted model for 2 predictors
model2 <- lm(<target_variable> ~ <x_i> + <x_2>, data = <dataset>)
summary(model2)$coefficients
##					Estimate	Std. Error	t-value		Pr(>|t|)
## (Intercept)	 	...			...			...			...
## variable_1	 	...			...			...			...
## variable_2	 	...			...			...			...

library(broom)
augment(model2)
## A tibble: (num of rows) x (number of columns)
##			variable_y 	durtation	cond		.fitted		.se.fit		.resid		.hat		.sigma		.cooksd
## 			<dbl>		<int>		<fct>		<dbl>		<dbl>		<dbl>		<dbl>		<dbl>		<dbl>
## 1		...			...			...			...			...			...			...			...			...
## 2		...			...			...			...			...			...			...			...			...
## 3		...			...			...			...			...			...			...			...			...
## ... with (num of rows - 3) more rows, and (number of columns - 9) more 

# Plot the parallel lines model
<dataset> %>% ggplot(aes(x=<x_1>, y=<target_variable>, color=<x_2>)) +
		geom_point(alpha=0.5) +
		geom_line(data=augment(model2), aes(y=.fitted, colour=<x_2>)) +
		labs(x="name of x_1 varaible(unit)", y="name of target variable (unit)")
# This would output a graph
```

> ##### Parallel regression line created for the `mariokart` dataset from the `openintro` library
>
> - Use `geom_line()` function, with template from above for the regression lines
>
>  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gonwx19wxmj30wy0kmq79.jpg" alt="Screen Shot 2021-03-17 at 23.32.23" style="zoom:30%;" />

### Non-parallel lines

- <u>Simpson's paradox</u> - adding an extra predictor changes the direction of the association in a L.R model

- If the new predictor **modifies the relationship** between the first predictor and the target variable, create a new model that represent this:
  $$
  y_i = \beta_0 + \beta_1 x_{1i} + \beta_2 x_{2i} + \beta_3 x_{1i} x_{2i} + \epsilon_i
  $$

  - <u>Interaction term</u> - new independent variable, which is the *product* of $x_1$ and  $x_2$
  - Fitted line for predictor 1 (assume $x_{2i}$ is categorical): [does not change]
    $\hat{y}_i = \hat{\beta}_0 +\hat{\beta}_2 x_{1i} + \hat{\beta}_2 (0) + \hat{\beta}_3x_{1i} (0)  = \hat{\beta}_0 + \hat{\beta}_1 x_{1i}$ 
  - Fitted line for predictor 2 (assume $x_{2i}$ is categorical): [change of slope]
    $\hat{y}_i = \hat{\beta}_0 +\hat{\beta}_2 x_{1i} + \hat{\beta}_2 (1) + \hat{\beta}_3 x_{1i}(1)  = (\hat{\beta}_0 + \hat{\beta}_2) + (\hat{\beta}_1 + \hat{\beta}_3)~ x_{1i}$ 

```R
# Fit the linear model with an interaction term (use * instead of + between predictors)
model3 <- lm(<target_variable> ~ <x_i> * <x_2>, data = <dataset>)
summary(model3)$coefficients
## 								Estimate	Std. Error		t-value		Pr(>|t|)
## (Intercept)			  		...			...			...				...
## variable_1				   	...		  	...			...				...
## variable_2				   	...		  	...			...				...
## variable_1: variable_2 		...		  	...			...				...
```

> ##### Non-parallel regression line created for the `mariokart` dataset from the `openintro` library
>
> - Use `geom_smooth()` function, same template with [[simple linear regression]] plots
>
>  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gonwxnk8v8j30q60gcq5v.jpg" alt="Screen Shot 2021-03-17 at 23.47.18" style="zoom:40%;" />

## Comparing prediction models (criteria for choosing the best)

- A model with **good prediction accuracy on average** (small RMSE)
- A model which doesn't exhibit evidence of **overfitting** (RMSE for training and test data are similar
  - <u>Overfitting</u> - not "fairly trained", predict good for trained data, doesn't predict new data well. RMSE for training dataset is much smaller than the testing dataset
- A model which **as simple as possible** (not too many predictors), while still catering the association between the predictors and the response

### Steps to choose between different models

1. Input the data and add new ID column called `rowid`
2. Create training dataset
3. Testing dataset inlaces all observations NOT in the training data
4. Fit the models to training data
5. Make predictions for **testing** and **training** data using training model
6. Calculate RMSE for **testing** and **training** data
7. Comparing the different models
   - Prediction accuracy from the RMSE for test data
   - Evidence for overfitting (compare RMSE for training and testing data)
   - Simplicity of the model
   - Conclusion

> ##### Compaering prediction models for the `mariokart` dataset
>
> - Models
>
>   - A: $y_i = \beta_0 + \beta_1 \times \text{duration}_i + \epsilon_i$
>   - B: $y_i = \beta_0 + \beta_1 \times I(\text{game i is used}) + \epsilon_i$
>   - C: $y_i = \beta_0 + \beta_1 \times \text{duration}_i + \beta_2 \times I(\text{game i is used}) + \epsilon_i$
>   - D: $y_i = \beta_0 + \beta_1 \times \text{duration}_i + \beta_2 \times I(\text{game i is used}) + \beta_3 \times \left[\text{duration}_i \cdot  I(\text{game i is used}) \right] + \epsilon_i$
>
> - Creating training/testing datasets & firing models
>
>   ```R
>   # Set up
>   set.seed(1211);
>   n <- nrow(mariokart2)
>   training_indices <- sample(1:n, size=round(0.8*n))
>   mariokart2 <- mariokart2 %>% rowid_to_column()
>   
>   # Create training dataset
>   train <- mariokart2 %>% filter(rowid %in% training_indices)
>   y_train <- train$total_pr;
>   
>   # Testing dataset includes all observations NOT in the training data
>   test <- mariokart2 %>% filter(! (rowid %in% training_indecies))
>   y_test <- test$total_pr;
>   
>   # Fit models to training data
>   modA_train <- lm(total_pr ~ duration, data=train)
>   modB_train <- lm(total_pr ~ cond, data = train) 
>   modC_train <- lm(total_pr ~ duration + cond, data=train) 
>   modD_train <- lm(total_pr ~ duration * cond, data=train)
>   ```
>
> - Making predictions for observations using either training or testing data (separately)
>
>   ```R
>   # Make prediction for training data using training model
>   yhat_modA_train <- predict(modA_train, newdata = train) 
>   yhat_modB_train <- predict(modB_train, newdata = train) 
>   yhat_modC_train <- predict(modC_train, newdata = train) 
>   yhat_modD_train <- predict(modD_train, newdata = train)
>   
>   # Make predcitions for testing data using training model
>   yhat_modA_test <- predict(modA_train, newdata = test)
>   yhat_modB_test <- predict(modB_train, newdata = test) 
>   yhat_modC_test <- predict(modC_train, newdata = test) 
>   yhat_modD_test <- predict(modD_train, newdata = test)
>   ```
>
> - Calculating RMSE
>
>   ```R
>   # Calculate RMSE for training data
>   modA_train_RMSE <- sqrt(sum((y_train - yhat_modA_train)^2) / nrow(train)) 
>   modB_train_RMSE <- sqrt(sum((y_train - yhat_modB_train)^2) / nrow(train)) 
>   modC_train_RMSE <- sqrt(sum((y_train - yhat_modC_train)^2) / nrow(train)) 
>   modD_train_RMSE <- sqrt(sum((y_train - yhat_modD_train)^2) / nrow(train))
>   
>   # Calculate RMSE for testing data
>   modA_test_RMSE <- sqrt( sum( (y_test - yhat_modA_test)^2 ) / nrow(test) )
>   modB_test_RMSE <- sqrt( sum( (y_test - yhat_modB_test)^2 ) / nrow(test) )
>   modC_test_RMSE <- sqrt( sum( (y_test - yhat_modC_test)^2 ) / nrow(test) )
>   modD_test_RMSE <- sqrt( sum( (y_test - yhat_modD_test)^2 ) / nrow(test) )
>   ```
>
> - Comparing the four models
>
>   ```R
>   mytable <- tibble(Model = c("A","B","C","D"),
>                     RMSE_testdata = c(modA_test_RMSE, modB_test_RMSE,
>                                       modC_test_RMSE, modD_test_RMSE), 
>                     RMSE_traindata = c(modA_train_RMSE, modB_train_RMSE,
>                                        modC_train_RMSE, modD_train_RMSE), 
>                     ratio_of_RMSEs = RMSE_testdata / RMSE_traindata)
>   ```
>
>    <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gony20lai5j30r608e410.jpg" alt="Screen Shot 2021-03-18 at 00.26.32" style="zoom:50%;" />
>
> - Analyze of the result and make a conclusion
>   - *Prediction accuracy*
>     Model D has a much lower RMSE for the test data than the other models. Models B and C are similar to each other in terms of RMSE, and model A has a much higher RMSE.
>   - *Evidence of overfitting*
>     The RMSE for model D is about 15% higher for the test data than the training data, while for the other models, this ranges from 17% to 21%. Model D shows the least evidence of overfitting among these models.
>   - *Simplicity of the model*
>     Models A and B each have one predictor, while model C has two predictors and model D has two predictors and one interaction term (total of 4 regression coefficients).
>   - *Conclusion*
>     Although model D is the most complex of these models, with four regression coefficients, it exhibits the best prediction accuracy (i.e. lowest RMSE for test data) and shows the least evidence of overfitting. Thus, it is reasonable to choose model D to predict the sale price of Mario Kart games sold on eBay around October 2019.