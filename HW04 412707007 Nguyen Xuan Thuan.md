# This homework is written by Nguyen Xuan Thuan (412707007)

## ch04.03 (a)

#### Question: the predicted value of $y$ for $x_0$ = 4.

```r
b1 = 1.2
b2 = 0.8
x_0 = 4
y_0 <- b1 + b2 * x_0
y_0
```

#### Answer 

$\hat{y_0} = b1 + b2 * x_0 = 1.2 + 0.8 * 4 = 4.4$

## ch04.03 (b)

#### Question: the $se(f)$ corresponding to part (a).


```r
x <- c(3, 2, 1, -1, 0)
y <- c(4, 2, 3, 1, 0)
n <- length(y)
SSE <- 3.6
SSX <- 10
SSY <- 10
mean_x <- mean(x)
mean_y <- mean(y)
mse <- SSE / (n - 2)
se <- sqrt(mse * (1+ 1/n + (x_0 - mean_x)^2 / SSX))
n
mse
se
```

#### Answer

$\widehat{var}(f|x) = \hat{\sigma}^2 \left[ 1 + \frac{1}{N} + \frac{(x_0 - \overline{x})^2}{\sum(x_i - \overline{x})^2} \right] = 1.2 \left[ 1 + \frac{1}{5} + \frac{(4 - 1)^2}{10} \right] = 2.52$

$se(f) = \sqrt{2.52} = 1.5875$

## ch04.03 (b)

#### Question: a 95% prediction interval for $y$ given $x_0 = 4$.

```r
alpha = 0.95
df <- n - 2
t_c <- qt((1 - alpha)/2,df)
t_c
pre_int_down <- y_0 + (t_c * se)
pre_int_up <- y_0 - (t_c * se)
pre_int_down
pre_int_up
```

t_c = 3.1824\
pre_int_down = -0.6520\
pre_int_up = 9.4520

#### Answer

$\hat{y}_{0}\pm t_{c}se(f)=4.4\pm3.1824\times1.5875=(-0.6520,9.4520)$

## ch04.03 (c)

#### Question: a 99% prediction interval for $y$ given $x_0 = 4$.

```r
alpha1 = 0.99
df <- n - 2
t_c1 <- qt((1 - alpha1)/2,df)
t_c1
pre_int_down1 <- y_0 + (t_c1 * se)
pre_int_up1 <- y_0 - (t_c1 * se)
pre_int_down1
pre_int_up1
```

t_c1 = 5.8509\
pre_int_down1 = -4.8722\
pre_int_up1 = 13.6722

#### Answer

$\hat{y}_{0}\pm t_{c}se(f)=4.4\pm5.8509\times1.5875=(-4.8722,13.6722)$

## ch04.03 (d)

#### Question: a 95% prediction interval for y given $x = \overline{x}$. Compare the width of this interval to the one computedin part (c).


```r
x <- c(3, 2, 1, -1, 0)
y <- c(4, 2, 3, 1, 0)
n <- length(y)
SSE <- 3.6
SSX <- 10
SSY <- 10
mean_x <- mean(x)
mean_y <- mean(y)
x_0 = mean_x
y_0_2 <- b1 + b2 * x_0
mse <- SSE / (n - 2)
se2 <- sqrt(mse * (1+ 1/n + (x_0 - mean_x)^2 / SSX))
n
mse
se2
alpha = 0.95
df <- n - 2
t_c <- qt((1 - alpha)/2,df)
pre_int_down2 <- y_0_2 + (t_c * se2)
pre_int_up2 <- y_0_2 - (t_c * se2)
y_0_2
t_c
pre_int_down2
pre_int_up2
```

y_0_2 = 2\
t_c = 3.1824\
se2 = 1.2\
pre_int_down = -1.8189\
pre_int_up = 5.8189

#### Answer

$\hat{y}_{0}\pm t_{c}se(f)=2\pm3.1824\times1.2=(-1.8189,5.8189)$

The width in part (e) is smaller than the width in part (c), as expected. Predictions are more precise when made for $x$ values close to the mean.

---

## ch04.25 (a)

#### Question: Estimate the log-linear model $ln(PRICE) = \beta_{1} + \beta_{2}SQFT + e$. Interpret the estimated model parameters. Calculate the slope and elasticity at the sample means, if necessary.

```r
library("POE5Rdata")
data("collegetown")
sqft <- collegetown$sqft
price <- collegetown$price
log_linear_model <- lm(log(price)~sqft,data = collegetown)
sum_log_linear_model = summary(log_linear_model)
sum_log_linear_model
b1 <- coef(log_linear_model) [1]
b2 <- coef(log_linear_model) [2]
mean_sqft <- mean(sqft)
mean_price <- mean(price)
slope <- b2 * mean_price
elasticity <- b2 * mean_sqft
slope
elasticity
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25a.png?raw=true)

#### Answer

The result show that each additional 100 square feet of interior space the expected price increases by approximately 3.6%.

slope = 9.0197\
elasticity = 0.98\
The slope = 9.0197 . At the mean values, we estimate that an added 100 square feet of interior space increases expected price by $9,019.70. The elasticity is estimated as 0.98 estimated to increase expected priced by 0.98%.

## ch04.25 (b)

#### Question: Estimate the log-log model $ln(PRICE) = \alpha_{1} + \alpha_{2}ln(SQFT) + e$. Interpret the estimated parameters. Calculate the slope and elasticity at the sample means, if necessary.

```r
log_log_model <- lm(log(price)~log(sqft),data = collegetown)
sum_log_log_model = summary(log_log_model)
sum_log_log_model
a1 <- coef(log_log_model) [1]
a2 <- coef(log_log_model) [2]
slope1 <- a2 * (mean_price/mean_sqft)
elasticity1 <- a2
slope1
elasticity1
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25b.png?raw=true)

#### Answer

slope1 = 9.3999\
elasticity1 = 1.0248\
The estimated coefficient is an elasticity. We estimate a 1% increase in SQFT to increase expected priced by 1.02%. The slope = 9.4, at the mean values, the result show that an added 100 square feet of interior space increases expected price by $9,400.

## ch04.25 (c)

#### Question: Compare the $R^2$ value from the linear model $PRICE = \delta_{1} + \delta_{2}SQFT + e$ to the “generalized” $R^2$ measure for the models in (b) and (c).

```r
linear_model <- lm(price~sqft,data = collegetown)
sum_linear_model = summary(linear_model)
sum_linear_model
d1 <- coef(linear_model) [1]
d2 <- coef(linear_model) [2]
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25c.png?raw=true)

```r
y_hat_log_linear = exp(b1 + b2 * sqft)
y = price
general_R_log_linear = cor(y,y_hat_log_linear)^2

y_hat_log_log = exp(a1 + a2 * sqft)
general_R_log_log = cor(y,y_hat_log_log)^2

y_hat_linear = exp(d1 + d2 * sqft)
general_R_linear = cor(y,y_hat_linear)^2

sum_log_linear_model$r.squared
sum_log_log_model$r.squared
sum_linear_model$r.squared

general_R_log_linear
general_R_log_log
general_R_linear
```

#### Answer

|   $model$    |    $R^2$    | $generalized\ R^2$ |
|:------------:|:-----------:|:------------------:|
| $log-linear$ | $0.5417259$ |    $0.6621612$     |
|  $log-log$   | $0.4738445$ |    $0.6445084$     |
|   $linear$   | $0.6413167$ |    $0.6413167$     |

The generalized $R^2$ for the log-linear model is largest, indicating that it fits the data better than the other two models, at least based on this measure.

## ch04.25 (d)

#### Question: Construct histograms of the least squares residuals from each of the models in (a)–(c) and obtain the Jarque–Bera statistics. Based on your observations, do you consider the distributions of the residuals to be compatible with an assumption of normality?

```r
install.packages("tseries")
library(tseries)

res_log_linear_model = residuals(log_linear_model)
hist(res_log_linear_model,xlab = "Least squares residuals",breaks = 20,main = 'Log-Linear residual',col = "light green")
jarque.test(res_log_linear_model)

res_log_log_model = residuals(log_log_model)
hist(res_log_log_model,breaks = 20,xlab = "Least squares residuals",main = 'Log-Log residual',col = "red")
jarque.test(res_log_log_model)

res_linear_model = residuals(linear_model)
hist(res_linear_model,breaks = 20,xlab = "Least squares residuals",main = 'Linear residual',col = "light blue")
jarque.test(linear_model)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25d1.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25d2.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25d3.png?raw=true)

#### Answer

None of the histograms is very bell- shaped. The distributions of the residuals do not follow the assumption of normality.

## ch04.25 (e)

#### Question: For each of the models in (a)–(c), plot the least squares residuals against $SQFT$. Do you observe any patterns?

```r
plot(res_log_linear_model~sqft, main = "Log_Linear residual and SQFT", col = "dark green")
plot(res_log_log_model~sqft, main = "Log_Log residual and SQFT", col = "red")
plot(res_linear_model~sqft, main = "Linear residual and SQFT", col = "dark blue")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25e1.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25e2.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.25e3.png?raw=true)

The linear model residuals show a clear pattern. The log-linear and log-log models plots are less definitive. There are only a few homes with very large SQFT so the figures may indicate a pattern just because of data sparsity.The logarithmic models have the violation of the homoskedasticity assumption.

## ch04.25 (f)

#### Question: For each model in (a)–(c), predict the value of a house with 2700 square feet.

```r
sqft_f=2700/100

y_hat_log_linear_pre = exp(b1 + b2 * sqft_f)
y_hat_log_log_pre = exp(a1 + a2 * log(sqft_f))
y_hat_linear_pre = d1 + d2 * sqft_f

y_hat_log_linear_pre
y_hat_log_log_pre
y_hat_linear_pre
```

#### Answer

y_hat_log_linear_pre = 214.2336\
y_hat_log_log_pre = 227.5386\
y_hat_linear_pre = 246.4557

## ch04.25 (g)

#### Question: For each model in (a)–(c), construct a 95% prediction interval for the value of a house with 2700 square feet.

```r
df <- sum_log_linear_model$df[2]
t_value = qt(0.975,498)
mean_sqft = mean(sqft)

exp_price_1 = b1 + 27 * b2
exp_price_2 = a1 + log(27) * a2
exp_price_3 = d1 + 27 * d2

var_1_2 = vcov(log_linear_model)[2,2]
sigma_1 <- sum_log_linear_model$sigma^2
var_1 = sigma_1 + sigma_1/500 + (27- mean_sqft)^2 * var_1_2
se_1 = sqrt(var_1)
lowb_1 = exp(exp_price_1 - t_value * se_1)
upb_1 = exp(exp_price_1 + t_value * se_1)

var_2_2 = vcov(log_log_model)[2,2]
sigma_2 <- sum_log_log_model$sigma^2
var_2 = sigma_2 + sigma_2/500 + (27- mean_sqft)^2 * var_2_2
se_2 = sqrt(var_2)
lowb_2 = exp(exp_price_2 - t_value * se_2)
upb_2 = exp(exp_price_2 + t_value * se_2)

var_3_2 = vcov(linear_model)[2,2]
sigma_3 <- sum_linear_model$sigma^2
var_3 = sigma_3 + sigma_3/500 + (27- mean_sqft)^2 * var_3_2
se_3 = sqrt(var_3)
lowb_3 = exp_price_3 - t_value * se_3
upb_3 = exp_price_3 + t_value * se_3
```

#### Answer:

To calculate the prediction interval , we need to find the unbiased predictor ${\hat{y}}$ and the standard error of the forecast $se(f) = \sqrt{var(f)}$ and t-statistic $t_\frac{\alpha}{2}(n-2)$ .

$$
var(f) = {\sigma^2} \cdot [1 + \frac{1}{N} + \frac{(x_0 - \bar{x}^2)}{\sum(x_i - \bar{x})^2}]
$$

The interval for linear model is

$$
[{\hat{y} \pm se(f) \cdot t_\frac{\alpha}{2}(n-2) }]
$$

The interval for log-linear & log-log model is

$$
[\exp{({\hat{y} \pm se(f) \cdot t_\frac{\alpha}{2}(n-2) })}]
$$


PI_log_linear_model = [109.768,418.116]\
PI_log_log_model = [111.087,466.067]\
PI_linear_model = [44.277,448.634] 

## ch04.25 (h)

#### Question: Based on your work in this problem, discuss the choice of functional form. Which functional form would you use? Explain.

The $R^2$ for the linear model is largest part (c).\
None of the histograms is very bell- shaped but the distributions of linear model is better to compare with log-linear model and log-log model part (d).\
The linear model residuals show a clear pattern, the log-linear and log-log models plots are less definitive part (e).\
Based on conclusions, linear model is better for use.

---

## ch04.28 (a)

#### Question: Estimate each of the four equations. Taking into consideration (i) plots of the fitted equations, (ii) plots of the residuals, (iii) error normality tests, and (iii) values for R2, which equation do you think is preferable? Explain.

```r
library(POE5Rdata)

data <- POE5Rdata::wa_wheat
Y <- data$northampton
X <- data$time
df <- data.frame(X,Y)   

# Model 1:

model1 <- lm(Y~X)
result1<- summary(model1)
residual1 <- model1$residuals

plot(residual1, xlab = "Time", ylab = "Residual",main = "Residuals Model1", col = "dark blue")

b1 <- coef(model1) [1]
b2 <- coef(model1) [2]
fitted_model_1 <- function(X){return(b1 + b2 * X)}

plot(x = X,y = Y,main = "Fitted Model1",
     xlab = "Time" ,ylab = "Yield", col = "dark blue")
abline(model1,lwd=2, col = "red")

shapiro.test(residual1) # H0: The data is normal dist 
                        # H1: reject H0 

R_squared1 <- result1$r.squared

```

```r
# Model 2:

X2 <- log(data$time)

model2 <- lm(Y~X2)
result2<- summary(model2)
residual2 <- model2$residuals

plot(residual2, xlab = "Time", ylab = "Residual",main = "Residuals Model2", col = "dark blue")

a1 <- coef(model2) [1]
a2 <- coef(model2) [2]
fitted_model_2 <- function(X){return(a1 + a2 * log(X))}

plot(df,main = "Fitted Model2", xlab = "Time", ylab = "Yield", col = "dark blue")
curve(fitted_model_2, from = 1, to = 100, n = 101, add = TRUE, col = "red")

shapiro.test(residual2) # H0: The data is normal dist 
                        # H1: reject H0 

R_squared2 <- result2$r.squared

```

```r
# Model 3

X3 <- data$time ** 2 

model3 <- lm(Y~X3)
result3 <- summary(model3)
residual3 <- model3$residuals

plot(residual3, xlab = "Time", ylab = "Residual",main = "Residuals Model3", col = "dark blue")

d1 <- coef(model3) [1]
d2 <- coef(model3) [2]
fitted_model_3 <- function(X){return(d1 + d2 * X**2)}
plot(df$X, df$Y, main = "Fitted Model3", xlab = "Time", ylab = "Yield", col = "dark blue")
curve(fitted_model_3, from = min(df$X), to = max(df$X), add = TRUE, col = "red")

shapiro.test(residual3)  # H0: THe data is normal dist 
                         # H1: reject H0 
R_squared3 <- result3$r.squared
```

```r
# Model 4

Y4 <- log(data$northampton)

model4 <- lm(Y4~X)
result4<- summary(model4)
residual4 <- model4$residuals

plot(residual4, xlab = "Time", ylab = "Residual",main = "Residuals Model4", col = "dark blue")

p1 <- coef(model4) [1]
p2 <- coef(model4) [2]
fitted_model_4 <- function(X){return(exp(p1 + p2 * X))}
plot(df$X, df$Y, main = "Fitted Model4", xlab = "Time", ylab = "Yield", col = "dark blue")
curve(fitted_model_4, from = min(df$X), to = max(df$X), add = TRUE, col = "red")

shapiro.test(residual4)  # H0: THe data is normal dist 
                         # H1: reject H0
R_squared3 <- result3$r.squared
```

#### Answer

#### (i) plot of the fitted equations 

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a2.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a5.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a8.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a11.png?raw=true)

#### (ii) plot of the residuals 

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a1.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a4.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a7.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a10.png?raw=true)

In this case two of the models, the linear and linear-log can be eliminated immediately. Consulting Figure 4.1 we see that neither of those functional forms can capture curvature of the data.\
Comparing the quadratic and log-linear fitted curves we see that both capture the shape of the relationship. The quadratic model has a higher R2 and the residual plot does not show as much of a dip in the center region. Thus, we choose the quadratic model as our preferred specification.

#### (iii) error normaility tests

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a3.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a6.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a9.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28a12.png?raw=true)

#### (iv) values for $R^2$

|           | linear-linear | linear-log | linear-quadratic | log-linear |
|-----------|:-------------:|:----------:|:----------------:|:----------:|
| $R^2$     |     0.578     |    0.339   |      0.689       |    0.507   |

Based on the R-square value, the linear-quadratic model is better than others.

## ch04.28 (b)

#### Question: Interpret the coefficient of the time-related variable in your chosen specification.

```r
summary(model3)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28b1.png?raw=true)

#### Answer

The elasticity is $2 \gamma_1 TIME$.\
For the quadratic model the estimated coefficient is 0.0004986, carried out to more decimals. The marginal effect is 2(0.0004986)TIME. Thus, the slope changes at each point in time. Evaluating the marginal effect at TIME = 10, 20, 30, and 40, the marginal effects on YIELD are estimated to be 0.0099724, 0.0199447, 0.0299171 and 0.0398894. The marginal effect increases as time passes as the cumulative effect of technology increases output by larger and larger amounts with time.

## ch04.28 (b)

#### Question: Using your chosen specification, identify any unusual observations, based on the studentized residuals, LEVERAGE, DFBETAS, and DFFITS.

``` r
library(olsrr)     
ols_plot_resid_stand(model3)
ols_plot_resid_lev(model3)
ols_plot_dfbetas(model3)
ols_plot_dffits(model3)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28c1.png?raw=true)

Observation 14, 28, 43 are outliers.

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28c2.png?raw=true)

An observation is considered to have high leverage if it has a value for the predictor variables that are much more extreme compared to the rest of the observations in the dataset. Observation 14, 28, 43 has a great influence.

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28c3.png?raw=true)

Observation 6, 14 has a great influence on the intercept. Observation 14, 43, 44, 48 has a great influence on the quadratic term.

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/Rplots/Rplot04.28c4.png?raw=true)

DFFIT stands for difference in fits, is used to identify influential data points.  Observation 14, 43, 48 has a great influence.

Looking at the fitted quadratic model, observation 14 stands out with a large negative residual.

## ch04.28 (b)

#### Question: Using your chosen specification, use the observations up to 1996 to estimate the model. Construct a 95% prediction interval for $YIELD$ in 1997. Does your interval contain the true value?

```r
new_X <- X[1:length(X)-1]
new_X3 <- X3[1:length(X3)-1]
new_Y <- Y[1:length(Y)-1]
new_model <- lm(new_Y ~ new_X3)
g1 <- coef(new_model)[[1]]
g2 <- coef(new_model)[[2]]
y_hat <- g1 + g2 * 48^2
sigma_hat <- summary(new_model)$sigma ^ 2
var <- sigma_hat + sigma_hat / length(new_X3) + sigma_hat * ((48-mean(new_X))^2 / sum((new_X - mean(new_X))^2))
se <- sqrt(var)

alpha = 0.05
tc <- qt(1-alpha/2,47-2)

up_b <- y_hat + tc * se
low_b <- y_hat - tc * se
up_b
low_b
```

#### Calculation Process

Time: 1~47 (1950-1996)

Yield: Average wheat yield in tonnes per hectare in Northampton Shire from 1950-1996

Model: $YIELD_t = \gamma_0 + \gamma_1 \times TIME^2 + e_t$

The predictor: $\widehat{YIELD_t} = 0.7842 + 0.00048 \times TIME^2$

Predicting the yield of 1997: $\widehat{YIELD_{48}} = 0.7842 + 0.00048 \times 48^2 = 1.881$

Calculating the standard error of forecast: $se(f) = \sqrt{\hat{var}(f)} = \sqrt{\hat{\sigma}[1 + \frac{1}{N} + \frac{(x_0 - \bar{x})^2}{\sum (x_i - \bar{x})^2}]} = \sqrt{0.0563[1 + \frac{1}{47} + \frac{(48 - 24)^2}{\sum (x_i - 24)^2}]} = 0.2474$

Construcing a 95% prediction interval : $\alpha = 0.05$

The critical value: $t_c = t_{N-2,\frac{\alpha}{2}} = t_{47-2,\frac{0.05}{2}} = t_{45,0.025} = 2.014$

The 95% prediction interval for $YIELD_{48}$ is $\widehat{YIELD_{48}} \pm t_{45,0.025} se(f) = 1.881 \pm 2.014 \times 0.2474 = [1.383 , 2.3794]$

It contains the true yield in 1997: 2.2318.

---