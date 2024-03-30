# This homework is written by Nguyen Xuan Thuan (412707007)

# ch02.11 (a)

#### Question: Using 2013 data from three-person households (N = 2334), we obtain least squares estimates $\hat{y}$ = 13.77 + 0.52x. Interpret the estimated slope and intercept from this relation.

#### Answer:

Slope 0.52 means each additional 100 dollars per month income is associated with an additional 52 cents per person expenditure, on average, on food away from home. If monthly income is zero, we estimate that household will spend an average of $13.77 per person on food away from home.

---

# ch02.11 (b)

#### Question: Predict the expenditures on food away from home for a household with $2000 a month income.

```
# The expenditures on food away
y = 13.77 + 0.52 * (2000 / 100)
y
```

#### Answer:

y = 24.17

---

# ch02.11 (c)

#### Question: Calculate the elasticity of expenditure on food away from hohme with respect to income when household income is $2000 per month. [ Hint: Elasticity must be calculated for a point on the fitted regression.]


#### Equation of elasticity:

$$ \varepsilon = \frac{\frac{\Delta y}{y}}{\frac{\Delta x}{x}} = \beta_2 \times \frac{x}{\beta_1 + \beta_2x} $$

```
# The elasticity of expenditure on food away
x <- 2000/100
b1 <- 13.77
b2 <- 0.52
yhat <- b1 + b2 * x
elas <- b2 * x / yhat
elas
```

#### Answer:

elasticity = 24.17. The result show that a 1% increase in income will increase expected food expenditure by 0.43% per person.

---

# ch02.11 (d)

#### Question: We estimate the log-linear model to be $\widehat{ln(y)}$ = 3.14 + 0.007x. What is the estimated elasticity of expenditure on food away from home with respect to income, if household income is $2000 per month?

```
# The estimate elasticity of expenditure on food away
b1 <- 3.14
b2 <- 0.007
x <- 2000/100
est_elas <- b2 * x
est_elas
```

#### Answer:

The estimate elasticity = 0.14

---

# ch02.11 (e)
#### Question: For the log-linear model in part (d), calculate $\hat{y}$ = exp(3.14 + 0.007x) when x = 20 and when x = 30. Evaluate the slope of the relation between y and x, dy/dx, for each of these $\hat{y}$ values. Based on these calculations for the log-linear model, is expenditure on food away from home increasing with respect to income at an increasing or decreasing rate?

```
# when x = 20
x1 <- 20
y_hat1 <- exp(3.14 + 0.007 * x1)
slope1 <- 0.007 * exp(3.14 + 0.007 * x1)

# when x = 30
x2 <- 30
y_hat2 <- exp(3.14 + 0.007 * x2)
slope2 <- 0.007 * exp(3.14 + 0.007 * x2)

slope1
slope2
```

#### Answer:

slope1 = 0.1860304\
slope2 = 0.1995191

The increasing of slope when x is increasing shows that y increasing with respect to x at an increasing rate.
Expenditure on food away from home increasing with respect to income at an increasing

---

# ch02.11 (f)
#### Question: When estimating the log-linear model in part (d), the number of observations used in the regression falls to *N* = 2005. How many households in the sample reported no expenditures on food away from home in the past quarter?

#### Answer:

The number of zeros is 2334 – 2005 = 329. The reason for the reduction in the number of observations is that the logarithm of zero is undefined and creates a missing data value.

---

# ch02.28 (a)

#### Question: Obtain the summary statistics and histograms for the variables *WAGE* and *EDUC*. Discuss the data characteristics.

```
library("POE5Rdata")
data("cps5_small")
Wage = cps5_small$wage
Educ = cps5_small$educ
summary_statistics_wage <- summary(Wage)
summary_statistics_educ <- summary(Educ)
hist(Wage, main="Histogram of Wage", xlab="Wage", breaks=30, col="light blue")
hist(Educ, main="Histogram of Educ", xlab="Educ", breaks=30, col="light green")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28a1.png?raw=true)
![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28a2.png?raw=true)
![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28a3.png?raw=true)

#### Discuss: 

The observations for *WAGE* are skewed to the right indicating that most of the observations lie between the hourly wages of 5 to 50,the maximum earned in this sample is *221.10$* per hour and the least earned in this sample is *3.94* per hour.
There are a few observations for *EDUC* at less than 12, representing those who did not complete high school. The majority of surveyed values are in the 12-16 year range.

---

# ch02.28 (b)

#### Question: Estimate the linear regression $WAGE = \beta_{1} + \beta_{2} EDUC + e$ and discuss the results.

```
lm_Wage_Educ <- lm(Wage ~ Educ, data = cps5_small)
summary(lm_Wage_Educ)
```
![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28b.png?raw=true)

$WAGE = -10.4 + 2.3968EDUC + e$

#### Discuss:

The coefficient 2.3968 represents the estimated increase in the expected hourly wage rate for an extra year of education. The coefficient −10.4 represents the estimated wage rate of a worker with no years of education.

---

# ch02.28 (c)

#### Question: Calculate the least squares residuals and plot them against *EDUC*. Are any patterns evident? If assumptions SR1–SR5 hold, should any patterns be evident in the least squares residuals?

```
yhat <- predict(lm_Wage_Educ)
residual = Wage-yhat 
plot(cps5_Educ, residual, 
     xlab="Educ", 
     ylab="Residual", 
     main = "Residual vs. Education",col = "red")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28c.png?raw=true)

#### Discuss:

When *EDUC* increases, the magnitude of the residuals also increases, suggesting that the error variance is larger for larger values of *EDUC*.

---
# ch02.28 (d)

---

#### Question: Estimate separate regressions for males, females, blacks, and whites. Compare the results.

```
# Males
Wage_of_males <- Wage[which(cps5_small$female==0)]
Educ_of_males <- Educ[which(cps5_small$female==0)]
lm_gender_males <- lm(Wage_of_males ~ Educ_of_males, data = cps5_small)
summary(lm_gender_male)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d1.png?raw=true)


```
# Females
Wage_of_females <- Wage[which(cps5_small$female==1)]
Educ_of_females <- Educ[which(cps5_small$female==1)]
lm_gender_females <- lm(Wage_of_females ~ Educ_of_females, data = cps5_small)
summary(lm_gender_females)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d2.png?raw=true)

```
# Blacks
Wage_of_blacks <- Wage[which(cps5_small$black==1)]
Educ_of_blacks <- Educ[which(cps5_small$black==1)]
lm_blacks <- lm(Wage_of_blacks ~ Educ_of_blacks, data = cps5_small)
summary(lm_blacks)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d3.png?raw=true)

```
# Whites
Wage_of_whites <- Wage[which(cps5_small$black==0)]
Educ_of_whites <- Educ[which(cps5_small$black==0)]
lm_whites <- lm(Wage_of_whites ~ Educ_of_whites, data = cps5_small)
summary(lm_whites)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d4.png?raw=true)

#### Compare the results:

The white equation is obtained from those workers who are black. From the results, we can see that an extra year of education increases the expected wage rate of a white worker more than it does for a black worker. And an extra year of education increases the expected wage rate of a female worker more than it does for a male worker.

---

# ch02.28 (e)

#### Question: Estimate the quadratic regression $WAGE = α_{1} + α_{2} EDUC^2 + e$ and discuss the results. Estimate the marginal effect of another year of education on wage for a person with 12 years of education and for a person with 16 years of education. Compare these values to the estimated marginal effect of education from the linear regression in part (b).

```
# Estimate the quadratic regression
quad_model <- lm(Wage ~ I(Educ^2), data= cps5_small)
summary(quad_model)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28e.png?raw=true)


```
# Estimate the marginal effect
a1 <- coef(quad_model)[1]
a2 <- coef(quad_model)[2]

# Marginal effect = 2a2Educ
me_Educ12 <- 2*a2*12 
me_Educ16 <- 2*a2*16
```

#### Answer:

me_Educ12 = 2.139216\
me_Educ16 = 2.852288

#### Compare:

The linear model in (b) suggested that an additional year of education is expected to increase wage by $2.3968 regardless of the number of years of education attained. 
The quadratic model suggests that the effect of an additional year of education on wage increases with the level of education already attained. That is, an additional year of education for a person with 12 years of education is expected to increase wage by 2.1392 dollars. For a person with 16 years of education, the marginal effect of an additional year of education is 2.8523 dollars.

---

# ch02.28 (f)

#### Question: Plot the fitted linear model from part (b) and the fitted values from the quadratic model from part (e) in the same graph with the data on *WAGE* and *EDUC*. Which model appears to fit the data better?

```
# Plot graph
install.packages("ggplot2")
library(ggplot2)
ggplot(cps5_small, aes(x = Educ, y = Wage)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE, color = "blue") +
  geom_smooth(method = "lm", formula = y ~ poly(x, 2), se = FALSE, color = "red")+
  labs(title = "Quadratic Regression Model and Linear Regression Model")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28f.png?raw=true)

The quadratic model appears to fit the data slightly better than the linear equation, especially at lower levels of education.

---

# ch02.29 (a)

#### Question: Create the variable $LWAGE = ln(WAGE)$. Construct a histogram and calculate detailed summary statistics. Does the histogram appear bell shaped and normally distributed? A normal distribution is symmetrical with no skewness, skewness = 0. The tails of the normal distribution have a certain “thickness.” A measure of the tail thickness is kurtosis, discussed in Appendix C.4.2. For a normal distribution, the kurtosis = 3, discussed in Appendix C.7.4. How close are the measures of skewness and kurtosis for LWAGE to 0 and 3, respectively?

```
# Histogram and statistics for ln(WAGE)
library("POE5Rdata")
data("cex5_small")
LWAGE <- log(cps5_small$wage)
hist(LWAGE, breaks = 100, col = "green")
# detailed summary statistics
summary((LN_WAGE))
skewness(LWAGE)
kurtosis(LWAGE)
# or
library(psych)
describe(LWAGE)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot29a.png?raw=true)

| $variable$ |  $N$   |  $mean$  | $median$ |  $min$   |  $max$   | $skewness$ | $kurtosis$ |
|:----------:|:------:|:--------:|:--------:|:--------:|:--------:|:----------:|:----------:|
| $ln(WAGE)$ | $1200$ | $2.9994$ | $2.9601$ | $1.3712$ | $5.3986$ |  $0.2306$  |  $2.6846$  |

The histogram shows the distribution of ln(WAGE) to be almost symmetrical. Note that the mean and median are similar, which is not the case for skewed distributions. The skewness coefficient is not quite zero. Similarly, the kurtosis is not quite three, as it should be for a normal distribution.

---

# ch02.29 (b)

#### Question: Obtain the OLS estimates from the log-linear regression model $ln(WAGE) = \beta_{1} + \beta_{2} EDUC + e$ and interpret the estimated value of $\beta2$.

```
# The OLS estimates from the log-linear regression model
Educ <- cps5_small$educ
lm(LWAGE ~ Educ, data = cps5_small)
b1 <- coef(lm(LWAGE ~ Educ))[1]
b2 <- coef(lm(LWAGE ~ Educ))[2]
b1
b2
```

#### Answer:

$\hat{ln(WAGE)} = 1.5968 + 0.0987EDUC$
We estimate that each additional year of education predicts a 9.87% higher wage, all else held constant.

---

# ch02.29 (c)

#### Question: Obtain the predicted wage, $\widehat{W A G E}=\exp \left(b_{1}+b_{2} E D U C\right)$, for a person with 12 years of education and for a person with 16 years of education.

```
# Predicted wage
Educ12 <- 12
Educ16 <- 16
Wage12 <- exp(b1 + b2 * Educ12)
Wage16 <- exp(b1 + b2 * Educ16)
Wage12
Wage16
```

#### Answer:

Wage12 = 16.14929\
Wage16 = 23.97208

---

# ch02.29 (d)

#### Question: What is the marginal effect of additional education for a person with 12 years of education and for a person with 16 years of education? [Hint: This is the slope of the fitted model at those two points.]

```
# Marginal effect = b2 * exp(b1 + b2 * Educ)
me_Educ12 <- b2 * exp(b1 + b2 * Educ12)
me_Educ16 <- b2 * exp(b1 + b2 * Educ16)
me_Educ12
me_Educ16
```

#### Answer:

me_Educ12 = 16.14929\
me_Educ16 = 23.97208

---

# ch02.29 (e)

#### Question: Plot the fitted values $\widehat{W A G E}=\exp \left(b_{1}+b_{2} E D U C\right)$ versus EDUC in a graph. Also include in the graph the fitted linear relationship. Based on the graph, which model seems to fit the data better, the linear or log-linear model?

```
Wage <- cps5_small$wage
Educ <- cps5_small$educ
lm_Wage_Educ <- lm(Wage ~ Educ, data = cps5_small)
lm(LWAGE ~ Educ, data = cps5_small)
b1 <- coef(lm(LWAGE ~ Educ))[1]
b2 <- coef(lm(LWAGE ~ Educ))[2]

plot(Educ, Wage, col = "blue", main = "Linear vs Log-linear model")
abline(lm_Wage_Educ, col = "red", lwd = 2)
curve(exp(b1 + b2 * x), add = TRUE, col = "green", lwd = 2)

legend("topleft", legend = c("Actual Data", "Linear", "Log-linear"),
       col = c("blue", "red", "green"), pch = c(1, NA, NA), lwd = c(NA, 1, 2))
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot29f.png?raw=true)

#### Answer:

The log-linear model fits the data better at low levels of education and the linear model better at high levels of education.

---

# ch02.29 (f)

#### Question: Using the fitted values from the log-linear model, compute $\sum (WAGE - \widehat{W A G E})^2$ . Compare this value to the sum of squared residuals from the estimated linear relationship. Using this as a basis of comparison, which model fits the data better?

```
linear_resdiuals <- lm_Wage_Educ$residuals
fitted_log_linear <- exp(b1 + b2 * Educ)
log_linear_residuals <- Wage - fitted_log_linear
SSR_linear <- sum(linear_resdiuals^2)
SSR_log_linear <- sum(log_linear_residuals^2)
SSR_linear
SSR_log_linear
```
#### Answer:

SSR_linear = 220062.3\
SSR_log_linear = 228573.5\
Based on this measure the linear model fits the data better than the linear model.

---