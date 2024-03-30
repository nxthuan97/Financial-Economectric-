# This homework is written by Nguyen Xuan Thuan (412707007)

## ch02.01 (a)

#### Question: Complete the entries in the table. Put the sums in the last row. What are the sample means $\bar{x}$ and $\bar{y}$?

#### Define the data

    x <- c(3, 2, 1, -1, 0)
    y <- c(4, 2, 3, 1, 0)

    mean_x=mean(x)

    x_minus_mean_x= x - mean(x)
    square_x_minus_x_mean= (x - mean(x))^2

    mean_y=mean(y)

    y_minus_mean_y= y - mean(y)
    x_minus_meanx_multiply_y_minus_meany=(x - mean(x))*(y - mean(y))

|      $x$      |      $y$       |       $x-\bar{x}$       |      $(x-\bar{y})^2$       |       $y-\bar{y}$       |       $(x-\bar{x})(y-\bar{y})$       |
|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
|       3       |       4        |            2            |             4              |            2            |                  4                   |
|       2       |       2        |            1            |             1              |            0            |                  0                   |
|       1       |       3        |            0            |             0              |            1            |                  0                   |
|      -1       |       1        |           -2            |             4              |           -1            |                  2                   |
|       0       |       0        |           -1            |             1              |           -2            |                  2                   |
| $\sum{x_i}=5$ | $\sum{y_i}=10$ | $\sum{(x_i-\bar{x})}=0$ | $\sum{(x_i-\bar{x})^2}=10$ | $\sum{(y_i-\bar{y})}=0$ | $\sum{(x_i-\bar{x})(y_i-\bar{y})}=8$ |

#### Answer

$\bar{x}$ = 1 $\bar{y}$ = 2

    sum_x=sum(x)
    sum_y=sum(y)
    sum_x_minus_mean_x = sum(x_minus_mean_x)

    sum_square_x_minus_x_mean = sum(square_x_minus_x_mean)
    sum_y_minus_mean_y = sum(y_minus_mean_y)
    sum_x_minus_x_mean_multiply_y_minus_meany = sum(sum(x_minus_meanx_multiply_y_minus_meany))

## ch02.01 (b)

#### Question: Calculate b1 and b2 using (2.7) and (2.8) and state their interpretation.

$b2 = \frac{\sum{(x_i-\bar{x}) \cdot (y_i -\bar{y})}}{\sum{(x_i - \bar{x})^2}} \quad (2.7)$\
$b1 = \bar{y} - b_2\bar{x} \quad (2.8)$

    b2=sum(x_minus_meanx_multiply_y_minus_meany)/sum(square_x_minus_x_mean)
    b1=mean(y)-b2*mean(x)

#### Answer

b1=1.2 
b2=0.8

we can obtain the least squares estimates for the intercept and slope parameters $\beta_1$ and $\beta_2$

$\hat{Y}$ = 1.2 + 0.8${X_i}$

When $X$ increases by 1, $Y$ is expected to increase by 0.8, when $X$ equal 0, $Y$ is expected equal 1.2

## ch02.01 (c)

#### Question: Compute $\sum_{i=1}^{5} x^2_i$, $\sum_{i=1}^{5}x_i y_i$ Using these numerical values, show that $\sum{(x_i-\bar{x})^2} = \sum{x^2_i - N \bar{x}^2}$ and $\sum{(x_i - \bar{x}) (y_i - \bar{i}) = \sum{x_i y_i - N \bar{x} \bar{y}}}$


    N <- length(x)

    x_square <- x^2
    sum_of_x_square <- sum(x_square)
    x_mul_y <- x*y
    sum_x_mul_y <- sum(x_mul_y)

    sum_of_square <- (sum_of_x_square - (N*mean_x^2))
    covariance_xy <- (sum_x_mul_y - (N*mean_x*mean_y))

$x = [3,2,1,-1,0]$\
$y = [4,2,3,1,0]$\
$\bar{x} = 1$\
$\bar{y} = 2$

#### Answer

$\sum_{i=1}^{5} x^2_i = 15$\
$\sum_{i=1}^{5} x_i y_i = 18$\
$\sum{(x_i-\bar{x})^2} = 10$\
$\sum{x^2_i - N \bar{x}^2} = 10$\
$\sum{(x_i - \bar{x}) (y_i - \bar{i})} = 8$\
$\sum{x_i y_i - N \bar{x} \bar{y}} = 8$

# ch02.01 (d)

#### Question: Use the least squares estimates from part (b) to compute the fitted values of $y$, and complete the remainder of the table below. Put the sums in the last row. Calculate the sample variance of $y$, $s^2_y = \sum_{i=1}^{N}(y_i - \bar{y})^2 / (N-1)$, the sample variance of $x$, $s^2_x = \sum_{i=1}^{N}(x_i - \bar{x})^2 / (N-1)$, the sample covariance between $x$ and $y$, $s_{xy} = \sum_{i=1}^N (y_i-\bar{y})(x_i - \bar{x}) / (N-1)$ the sample correlation between $x$ and $y$, $r_{xy} = s_{xy} / (s_x s_y)$ and the coefficient of variation of $x$, $CV_x= 100(s_x/\bar{x})$. What is the median, 50th percentile, of $x$? \### The Ordinary Least Squares (OLS) Estimators $b_2 = \frac{\sum{(x_i-\bar{x}) \cdot (y_i -\bar{y})}}{\sum{(x_i - \bar{x})^2}} \quad (2.7)$

$b_1 = \bar{y} - b_2\bar{x} \quad (2.8)$\

**The calculate result is:**  $b_2 = 0.8$\
$b_1 = 1.2$

    mean_x = mean(x)
    mean_y = mean(y)

    sum_of_square = sum((x-mean_x)^2)
    covariance_xy = sum((x-mean_x)*(y-mean_y))

    N = length(x)

    b2 = covariance_xy / sum_of_square # 0.8
    b1 = mean_y - b2*mean_x # 1.2

------------------------------------------------------------------------

| $x_i$ | $y_i$ | $\hat{y}_i$ | $\hat{e}_i$ | $\hat{e}_i^2$ | $x_i \hat{e}_i$ |
|:-----:|:-----:|:-----------:|:-----------:|:-------------:|:---------------:|
|   3   |   4   |     3.6     |     0.4     |     0.16      |       1.2       |
|   2   |   2   |     2.8     |    -0.8     |     0.64      |      -1.6       |
|   1   |   3   |      2      |      1      |       1       |        1        |
|  -1   |   1   |     0.4     |     0.6     |     0.36      |      -0.6       |
|   0   |   0   |     1.2     |    -1.2     |     1.44      |        0        |
|   5   |  10   |     10      |  -2.22e-16  |      3.6      |    -1.33e-15    |

------------------------------------------------------------------------

    sample_variance_y = sum((y-mean_y)^2)/(N-1)
    sample_variance_x = sum((x-mean_x)^2)/(N-1)
    covariance_x_y = sum((y-mean_y) * (x-mean_x))/(N-1)
    correlation_x_y = covariance_x_y/(sqrt(sample_variance_x) * sqrt(sample_variance_y))
    coefficient_variation_x = 100*(sqrt(sample_variance_x)/mean_x)
    quantile(x, probs = c(.25, .5, .75))
    median(x)

#### Answer

The sample variance of $y$ = 2.5\
The sample variance of $x$ = 2.5\
The sample covariance between $x$ and $y$ = 2\
The sample correlation between $x$ and $y$ = 0.8\
The coefficient of variation of $x$ = 158.1139\
The median, 50th percentile, of $x$ = 1

# ch02.01 (e)

#### Question:On graph paper, plot the data points and sketch the fitted regression line $\hat{y} = b1+b2*x$

**According to the part (d)**\

| $x_i$ | $y_i$ | $\hat{y}_i$ |
|:-----:|:-----:|:-----------:|
|   3   |   4   |     3.6     |
|   2   |   2   |     2.8     |
|   1   |   3   |      2      |
|   0   |   0   |     1.2     |
|  -1   |   1   |     0.4     |

    x = c(3,2,1,0,-1)
    y = c(4,2,3,0,1)
    estimate_y = c(3.6,2.8,2,1.2,0.4)

    plot(x, y,
         xlab="x", 
         ylab="y",
         pch = 16, 
         col = 1
         )
    points(x,estimate_y, 
           pch=16,                
           col="blue")  
    lines(x, estimate_y, col = "blue")

#### Answer

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot1e.png?raw=true)

# ch02.01 (f)

#### Question: On the sketch in part (e), locate the point of the means ( $\bar{x}$, $\bar{y}$ ). Does your fitted line pass through that point? If not, go back to the drawing board, literall.

**According to the part (d)**, $\bar{x} = 1, \bar{y} = 2$

( $\bar{x}$, $\bar{y}$ ) = ( 1, 2 )，on the sketch in part (e), we can see fitted line pass through the point of the means ( 1, 2 ).

| $x_i$ | $y_i$ | $\hat{y}_i$ |
|:-----:|:-----:|:-----------:|
|   3   |   4   |     3.6     |
|   2   |   2   |     2.8     |
|   1   |   3   |      2      |
|   0   |   0   |     1.2     |
|  -1   |   1   |     0.4     |

    x = c(-1,0,1,2,3)
    y = c(1,0,3,2,4)
    estimate_y = c(0.4,1.2,2,2.8,3.6)

    plot(x, y,
         xlab="x", 
         ylab="y",
         pch = 16, 
         col = 1
         )
    points(x,estimate_y, 
           pch=16,                
           col="blue")  
    lines(x, estimate_y, col = "blue")


    points(1,2, 
           pch=16,                
           col="red")  

#### Answer

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot1f.png?raw=true)

# ch02.01 (i)

#### Question: Compute $\hat{σ^2}$

**According to the part (d)**, $b1=1.2, b2=0.8$

    y_hat <- b1 + b2 * x
    residuals <- y - y_hat
    residuals_var <- sum(residuals^2) / (n - 2)

#### Answer

$\hat{σ}^2 = 1.2$

# ch02.01 (j)

### Question: Compute $\hat{var}(b2|x)$ and $se(b2)$

    var_b2 <- residuals_var / sum_of_square
    se_b2 <- sqrt(var_b2)

#### Answer

$\hat{var}(b2|x) = 0.12$\
$se(b2) = 0.346$

## ch02.25 (a)

#### Question: Construct a histogram of FOODAWAY and its summary statistics. What are the mean and medianvalues? What are the 25th and 75th percentiles?

```
library("POE5Rdata")
data("cex5_small")
foodaway = cex5_small$foodaway
hist(x = foodaway,main = "Histogram of foodaway",xlab = "Foodaway", col = "light green")
```

#### Answer

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot25a.png?raw=true)

```
summary(foodaway)
```

mean = 49.27 
medianvalues = 32.55 
25th percentile = 12.04 
75th percentile = 67.50.

## ch02.25 (b)

#### Question: What are the mean and median values of FOODAWAY for households including a member with an advanced degree? With a college degree member? With no advanced or college degree member?

```
?cex5_small
```

#### Answer: For households including a member with an advanced degree

```
summary(subset(cex5_small,advanced == 1)$foodaway)
```

mean = 73.15 
median = 48.15.

#### Answer: For households including a member with a college degree member

```
summary(subset(cex5_small,college == 1)$foodaway)
```

mean = 48.60 
median = 36.11. 

#### Answer: For households including a member with no advanced or college degree member

```
summary(subset(cex5_small,(advanced == 0 & college == 0))$foodaway)
```

mean = 39.01 
median = 26.02.

# ch02.25 (c)

#### Question: Construct a histogram of ln(FOODAWAY) and its summary statistics. Explain why FOODAWAY and ln(FOODAWAY) have different numbers of observations.  

```
cex5_small$lnfoodaway <- log(cex5_small$foodaway)
cex5_small$lnfoodaway[is.infinite(cex5_small$lnfoodaway)] <- NA
hist(cex5_small$lnfoodaway, main = "Histogram of lnfoodaway",xlab = "Foodaway", col = "light green")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot25c.png?raw=true)

```
summary(cex5_small$lnfoodaway)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot25c1.png?raw=true)

##### Explain: There are 178 fewer values of ln(FOODAWAY) because 178 households reported spending 0$ on food away from home per person, and ln(0) is undefined.

# ch02.25 (d)

#### Question: Estimate the linear regression $\ln(FOODAWAY)=\beta_1 + \beta_2 INCOME+ e$. Interpret the estimated slope.

```
lm_Income_lnFoodaway <- lm(cex5_small$lnfoodaway ~ income, data = cex5_small)
b1 <- coef(lm_Income_lnFoodaway) [[1]]
b2 <- coef(lm_Income_lnFoodaway) [[2]]
summary(lm_Income_lnFoodaway)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot25d.png?raw=true)

#### Answer: $\hat{\ln(FOODAWAY)}=3.1293 + 0.0069 INCOME$

#### Explain: 
We estimate that each additional $100 household income increases food away expenditures per person of about 0.69%, other factors held constant.

# ch02.25 (e)

#### Question: Plot ln(FOODAWAY) against INCOME, and include the fitted line from part (d).

```
plot(cex5_small$income, cex5_small$lnfoodaway, xlab = "Income", ylab = "ln(foodaway)",main = "Scatterplot + Fitted Line")
abline(a = b1, b = b2, col = "red")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot25e.png?raw=true)

# ch02.25 (f)

#### Question: Calculate the least squares residuals from the estimation in part (d). Plot them vs. INCOME. Do you find any unusual patterns, or do they seem completely random?

```
residuals <- resid(lm_Income_lnFoodaway)
residuals[is.infinite(cex5_small$lnfoodaway)] <- NA
plot(cex5_small$income, residuals, xlab = "Income", ylab = "Residuals", main = "Residuals vs. INCOME", pch=19)
```
![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot25f1.png?raw=true)

#### Answer
The OLS residuals do appear randomly distributed with no obvious patterns. There are fewer observations at higher incomes, so there is more “white space”.

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

# ch02.28 (b)

#### Question: Estimate the linear regression $WAGE = \beta1 + \beta2 EDUC + e$ and discuss the results.

```
lm_Wage_Educ <- lm(cps5_small$wage ~ cps5_small$educ, data = cps5_small)
summary(lm_Wage_Educ)
```
![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28b.png?raw=true)

$WAGE = -10.4 + 2.3968EDUC + e$

#### Discuss
The coefficient 2.3968 represents the estimated increase in the expected hourly wage rate for an extra year of education. The coefficient −10.4 represents the estimated wage rate of a worker with no years of education.

# ch02.28 (c)

#### Question: Calculate the least squares residuals and plot them against *EDUC*. Are any patterns evident? If assumptions SR1–SR5 hold, should any patterns be evident in the least squares residuals?

```
yhat <- predict(lm_Wage_Educ)
residual = cps5_small$wage-yhat 
plot(cps5_small$educ, residual, 
     xlab="Educ", 
     ylab="Residual", 
     main = "Residual vs. Education",col = "red")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28c.png?raw=true)

#### Discuss
When *EDUC* increases, the magnitude of the residuals also increases, suggesting that the error variance is larger for larger values of *EDUC*.

# ch02.28 (d)

#### Question: Estimate separate regressions for males, females, blacks, and whites. Compare the results.

```
#Males
Wage_of_males <- Wage[which(cps5_small$female==0)]
Educ_of_males <- Educ[which(cps5_small$female==0)]
lm_gender_males <- lm(Wage_of_males ~ Educ_of_males, data = cps5_small)
summary(lm_gender_male)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d1.png?raw=true)


```
#Females
Wage_of_females <- Wage[which(cps5_small$female==1)]
Educ_of_females <- Educ[which(cps5_small$female==1)]
lm_gender_females <- lm(Wage_of_females ~ Educ_of_females, data = cps5_small)
summary(lm_gender_females)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d2.png?raw=true)

```
#Blacks
Wage_of_blacks <- Wage[which(cps5_small$black==1)]
Educ_of_blacks <- Educ[which(cps5_small$black==1)]
lm_blacks <- lm(Wage_of_blacks ~ Educ_of_blacks, data = cps5_small)
summary(lm_blacks)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d3.png?raw=true)

```
#Whites
Wage_of_whites <- Wage[which(cps5_small$black==0)]
Educ_of_whites <- Educ[which(cps5_small$black==0)]
lm_whites <- lm(Wage_of_whites ~ Educ_of_whites, data = cps5_small)
summary(lm_whites)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28d4.png?raw=true)

#### Compare the results
The white equation is obtained from those workers who are black. From the results, we can see that an extra year of education increases the expected wage rate of a white worker more than it does for a black worker. And an extra year of education increases the expected wage rate of a female worker more than it does for a male worker.

# ch02.28 (e)

#### Question: Estimate the quadratic regression $WAGE = α1 + α2EDUC2 + e$ and discuss the results. Estimate the marginal effect of another year of education on wage for a person with 12 years of education and for a person with 16 years of education. Compare these values to the estimated marginal effect of education from the linear regression in part (b).

```
quad_model <- lm(Wage ~ I(Educ^2), data= cps5_small)
summary(quad_model)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot28e.png?raw=true)

# ch02.28 (f)

#### Question: Plot the fitted linear model from part (b) and the fitted values from the quadratic model from part (e) in the same graph with the data on *WAGE* and *EDUC*. Which model appears to fit the data better?

