# This homework is written by Nguyen Xuan Thuan (412707007)

## ch03.18 (a)

#### Question: Draw a sketch of the fitted relationship identifying the estimated slope and intercept. The sample mean of $INCOME$ = 59.3. What is the sample mean of the amount of insurance held? Locate the point of the means in your sketch.

```r
library(devtools)
b1 = 6.855 
b2 = 3.880 

mean_of_ins = 6.855 + 3.880 * 59.3

plot(NULL, main = "Fitted Relationship", xlab = "INCOME", ylab = "INSURANCE", xlim = c(0, 200), ylim = c(0, 400))
abline(b1, b2, col = "blue", lwd = 3)
points(59.3, mean_of_ins, col = "red", pch = 16, cex = 1.5)
```

#### Answer 

When the least squares estimated relationship is $\widehat{INSURANCE}=\left( 6.855 + 3.880I N C O M E\right)$

the estimated slope = 3.880

the estimated intercept = 6.855

When household income = 59.3, the sample mean of the amount of insurance held = 6.855 + 3.880 * 59.3 = 236.939

The fitted relation passed through the point of the means.

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.18a.png?raw=true)

## ch03.18 (b)

#### Question: How much do we estimate that the average amount of insurance held changes with each additional $1000 of household income? Provide both a point estimate and a 95% interval estimate. Explain the interval estimate to a group of stockholders in the insurance company.

```r
df = 18
se_b1 = 7.383
se_b2 = 0.112
tail_p = (1 - 0.95)/2

tc = qt(tail_p, df)
tc

lowb_b2 = b2 - tc * se_b2
highb_b2 = b2 + tc * se_b2
lowb_b2
highb_b2
```

#### Answer

 As the slope of the regression line is 3.880, the average amount of insurance held will increase  $3.880 * 1,000 = 3,880$  with each additional 1,000 of household income.

$b_1 = 3.880$

two-tailed t value when alpha = 0.05, df = 18

$t_c = 2.101$

The interval estimate is $[ b_1 - t_cse(b_2) , b_1 + t_cse(b_2) ] = [ 3.88 - 2.101 * 0.112 , 3.88 + 2.101 * 0.112 ] = [ 3.645 , 4.115 ]$

We estimate with 95% confidence that a $1000 increase in income will increase average expenditure on insurance by \$3,645 to \$4,115.

## ch03.18 (c)

#### Question: Construct a 99% interval estimate of the expected amount of insurance held by a household with $100,000 income. The estimated covariance between the intercept and slope coefficient is −0.746

```r
cov = -0.746
ins_hat = b1 + b2*100
ins_hat
```

ins_hat = 394.855

$$
\begin{aligned}
\sqrt{var(b_1+100b_2)} &=\sqrt{var(b_1)+100^2var(b_2)+2\times{100}\times{cov(b_1,b_2)}}\\
\end{aligned}
$$

```r
var <- se_b1^2 + 100^2 * se_b2^2 + 2 * 100 * cov
std_er <- sqrt(var)
std_er
```

std_er = 5.54515

```r
tail_prob <- (1 - 0.99) / 2
left_t_value <- qt(tail_prob, df, lower.tail = TRUE)
right_t_value <- qt(tail_prob, df, lower.tail = FALSE)
left_t_value
right_t_value
```

left_t_value = -2.87844

right_t_value = 2.87844

```r
upper_bound <- ins_hat + 2.878 * std_er
lower_bound <- ins_hat - 2.878 * std_er
upper_bound
lower_bound
```

upper_bound = 410.8139

lower_bound = 378.8961

99% interval estimate of the expected amount of insurance held by a household with a
$100,000 income:

$394.855 ± 2.878 × 5.5452 = [378.8959, 410.8141]$

## ch03.18 (d)

#### Question: One member of the management board claims that for every \$1000 increase in income the average amount of life insurance held will increase by \$5000. Let the algebraic model be $INSURANCE = \beta_1 + \beta_2*INCOME + e$. Test the hypothesis that the statement is true against the alternative that it is not true. State the conjecture in terms of a null and alternative hypothesis about the model parameters. Use the 5% level of significance. Do the data support the claim or not? Clearly, indicate the test statistic used and the rejection region.

To test the claim, the relevant hypotheses are:

-   $H_0$: $\beta_2$ = 5 (For every \$1000 increase in income, the average amount of life insurance
    held increases by \$5000).
-   $H_1$: $\beta_2$ ≠ 5 (The statement is not true).
-   
We will test the hypothesis using a t-test. The test statistic is calculated as:

$$
 t = \frac{b_2 - 5}{se(b_2)} = \frac{3.88 - 5}{0.112} = -10
$$

Following part (c) t value when alpha = 0.05, df = 18 is $t_c$ = 2.101
The rejection region (18 degrees of freedom) is $|t|$ > 2.101
As $t$ = -10.00 < -2.101, we reject the null hypothesis and conclude that the estimated relationship does not support the claim.

## ch03.18 (d)

#### Question: Test the null hypothesis that as income increases the amount of life insurance held by the same amount. That is, test the null hypothesis that the slope is one. Use as the alternative that the slope is larger than one. State the null and alternative hypothesis in terms of the model parameters. Carry out the test at the 1% level of significance. Clearly indicate the test statistic used, and the rejection region. What is your conclusion?

Below is the null and alternative hypothesis in terms of model parameters.
- $H_0$ : $b_2$ = $1$ (The amount of life insurance held increases by the same amount as income increases)
- $H_1$ : $b_2$ > $1$ (The amount of life insurance held increases doesn't held by the same amount as income increases)

Model parameters: $\alpha$ = $0.01$ , $b_2$ = $3.88$ , $\text{se}(b_{2})$= $0.112$ , $df=18(20-2)$\
The test statistic is calculated as : 

$$
t_c = \frac{b_2 - 1}{se(b_2)} = \frac{3.88 - 1}{0.112} = 25.7143
$$

```r
b2 = 3.88
se_b2 = 0.112
tc <- (b2-1)/se_b2
tc
```

```r
t_value <- qt(0.01/2,df)
t_value
```

Critical value: $t_{18,0.005} = 2.87844$\
The rejection region is  $|t|$ > 2.87844

Because $t$ in rejection region, we reject the null hypothesis : $b_2$ = $1$, and accept the alternative $b_2$ > $1$. It indicates that the slope is larger than $1$.

---

## ch03.23 (a)

#### Question: Using the quadratic regression model, $PRICE=\alpha_1 + \alpha_2SQFT^2 + e$ , test the hypothesis that the marginal effect on expected house price of increasing the size of a 2000 square foot house by 100 square feet is less than or equal to \$13000 against the alternative that that the marginal effect will be greater than \$13000. Use the 5% level of significance. Clearly state the test statistic used, the rejection region, and the test p-value. What do you conclude?

```
library("POE5Rdata")
data("collegetown")
# Estimate the quadratic regression
quad_model <- lm(price ~ I(sqft^2), data = collegetown)
summary(quad_model)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.23a.png?raw=true)

The estimated model is  
$$\widehat{PRICE}=93.5659+0.1845\ {SQFT}^2$$

```r
sqft_2 = 20
alpha1 = coef(quad_model)[[1]]
alpha2 = coef(quad_model)[[2]]
margine_effect = 2 * alpha2 * sqft_2
sqft_se <- summary(quad_model)$coef[4]
se <- sqft_se * 2 * sqft_2
t_stat <- (margine_effect-13)/se
t_c <- qt(0.95, 498)
df <- dim(collegetown)[1]-2
p_value <- 1 - pt(q = t_stat, df = df, lower.tail = T)
margine_effect
se
t_stat
t_c
df
p_value
```

margine_effect = 7.2808\
se = 0.2102\
t_stat = -26.7277\
t_c = 1.6479\
df = 498\
p_value = 1

#### Answers

- Next, the marginal effect is $\frac{d\ PRICE}{d\ SQFT}=2\hat{\alpha_2}SQFT=2\hat{\alpha_2}(20)=7.2808$.
- Standard error is $\sqrt{\hat{var}(40\hat{\alpha_2})}=\sqrt{40^2\hat{var}(\alpha_2)}=0.2102$.
- The hypothesis is $H_0: 2\alpha_2(20)\leq13 \ v.s. \ H_1: 2\alpha_2(20) > 13$. This is a right-tail test.
- The test statistic is $t=(40\hat{\alpha_2}-13)/\sqrt{\hat{var}(40\hat{\alpha_2})} \sim t_{(498)}$.
- The calculated t_value is −26.72774. The right-tail critical value for the 5% level of significance is  $t_{(0.95, N-2=498)}=1.6479$.
- This falls in the non-rejection region. 
- The $p-value$ = 1
- We cannot conclude that the marginal effect is greater than $13,000.

## ch03.23 (b)

#### Question: Using the quadratic regression model in part (a), test the hypothesis that the marginal effect on expected house price of increasing the size of a 4000 square foot house by 100 square feet is less than or equal to \$13,000 against the alternative that the marginal effect will be greater than \$13,000. 

```r
sqft_2_b = 40
margine_effect_b = 2 * alpha2 * sqft_2_b
se_b <- sqft_se * 2 * sqft_2_b
t_stat_b <- (margine_effect_b-13)/se_b
p_value_b <- 1 - pt(q = t_stat_b, df = df, lower.tail = T)
margine_effect_b
se_b
t_c
t_stat_b
p_value_b
```

margine_effect_b = 14.7615\
se_b = 0.4205\
t_c = 1.6479\
t_stat_b = 4.1895\
p_value_b = 0.0000

#### Answers

- Marginal effect is $\frac{d\ PRICE}{d\ SQFT}=2SQFT\hat{\alpha_2}=2(40)\hat{\alpha_2}=14.762$.
- Hypothesis $H_0:2SQFT\hat{\alpha_2}\leq13 \ v.s.\ H_1:2SQFT\hat{\alpha_2}>13$.
- The standard error $se =\sqrt{\hat{var}(2SQFT\hat{\alpha_2})}=2SQFTse(\alpha_2)=0.4205$.
- The test statistic  $t=\frac{2SQFT\hat{\alpha_2}-13}{2SQFTse(\alpha_2)}\sim t_{(498)}$
  
$t=\frac{2(40)(0.18452)}{2(0.18452)0.0053}=4.189$.
- This falls in the rejection region. 
- The $p-value$ = 0.0000
- We conclude, at the 5% level, that the marginal effect is greater than $13,000.

## ch03.23 (c)

#### Question: Using the quadratic regression model in part (a), estimate the expected price $E(PRICE|SQFT) =  α_1+ α_2×SQFT^2$  for a house of 2000 square feet. Construct a 95% interval estimate of the expected price. Describe your interval estimate to a general audience.

```r
sqft_2 = 20
exp_price <- alpha1 + alpha2 * sqft_2^2
exp_price
alpha1 = coef(quad_model)[[1]]
alpha2 = coef(quad_model)[[2]]
var1 <- vcov(quad_model)[1, 1]
var2 <- vcov(quad_model)[2, 2]
cov <- vcov(quad_model)[1, 2]
var = var1 + (sqft^2)^2 * var2 + 2 * sqft^2 * cov
se <- sqrt(var)
se
df = 498
t_c <- qt(1-0.05/2,df)
t_c
# Interval estimate
lowb <- exp_price - t_c * se
upb <- exp_price + t_c * se
interval <- c(lowb,upb)
interval
```

exp_price = 167.3735\
se = 4.7464\
t_c = 1.9647\
interval = [158.0481 176.6988]

#### Answer

$E(PRICE|SQFT) =  α_1+ α_2×SQFT^2$

100(1-α)% interval estimate for $(c_1 β_1+c_2 β_2) is (c_1 b_1+c_2 b_2) ± t_c se(c_1 b_1+c_2 b_2)$

- The expected price is $\hat{(E)}(PRICE|SQFT=20) =93.5659+0.1845*20^2  = 167.3735$
- The standard error is  $\sqrt{{var}(\hat{α_1}) + 400 * (\hat{α_2})} = \sqrt{{var}(\hat{α_1}) + 400^2 * (\hat{α_2}) + 2(400)cov((\hat{α_1})(\hat{α_2}))}=4.746378$.
- The test statistic $t_{(0.975,498)}$= 1.964739
- The resulting interval estimate is 167.3735  ± (1.964739 )  4.746378 = [158.0481, 176.6988]
- Using this quadratic model, we estimate with 95% confidence that the average price of a 2000 square foot house is between \$158,048.10 and \$176,698.80.

## ch03.23 (d)

#### Question: Locate houses in the sample with 2000 square feet of living area. Calculate the sample mean(average) of their selling prices. Is the sample average of the selling price for houses with $SQFT = 20$ compatible with the result in part (c)? Explain.

```r
price <- collegetown$price
summary(subset(collegetown,sqft == 20)$price)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.23d.png?raw=true)

#### Explain
In the sample there are 3 houses with 2000 square feet ($SQFT = 20$). They sold for $138,000, $169,000 and $183,000 respectively and the sample average is 163.3, which is inside the interval estimate [158.0481, 176.6988].\
The interval estimate in (c) was for the expected, or population average, price for homes with 2000 square feet of living area. The average of the 3 observed house prices is not a population average, but we should not be surprised by the outcome.

---

## ch03.31 (a)

#### Question: Calculate the summary statistics for SAL1 and APR1. What are the sample means, minimum and maximum values, and their standard deviations. Plot each of these variables versus WEEK. How much variation in sales and price is there from week to week?


library("POE5Rdata")
data("tuna")

 ```r
# Calculate summary statistics for SAL1
summary_sal1 <- summary(tuna$sal1)
mean_sal1 <- round(mean(tuna$sal1), 2)
min_sal1 <- round(min(tuna$sal1), 2)
max_sal1 <- round(max(tuna$sal1), 2)
std_dev_sal1 <- round(sd(tuna$sal1), 2)
      
# Calculate summary statistics for APR1
summary_apr1 <- summary(tuna$apr1)
mean_apr1 <- round(mean(tuna$apr1), 2)
min_apr1 <- round(min(tuna$apr1), 2)
max_apr1 <- round(max(tuna$apr1), 2)
std_dev_apr1 <- round(sd(tuna$apr1), 2)
      
summary_df <- data.frame(
Variable = c("SAL1", "APR1"),
Sample_Mean = c(mean_sal1, mean_apr1),
Minimum_Value = c(min_sal1, min_apr1),
Maximum_Value = c(max_sal1, max_apr1),
Standard_Deviation = c(std_dev_sal1, std_dev_apr1))
  
summary_df
```

The summary statistics for SAL1 and APR1
| Variable | Sample_Mean | Minimum_Value | Maximum_Value | Standard_Deviation |
|:--------:|:-----------:|:-------------:|:-------------:|:-----------------:|
|   SAL1   |   6718.71   |    1762.00    |    32820.00   |      6915.08      |
|   APR1   |     0.78    |      0.61     |      0.92     |        0.10       |


```r
tuna$index <- 1:nrow(tuna)
        
# Plot Sales vs. Week
ggplot(tuna, aes(x = index, y = sal1)) + geom_line() +
labs(title = "Sales vs. Week", x = "Week", y = "Sales")
        
# Plot Price vs. Week
ggplot(tuna, aes(x = index, y = apr1)) + geom_line() +
labs(title = "Price vs. Week", x = "Week", y = "Price")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.31a1.png?raw=true)

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.31a2.png?raw=true)

The plots illustrate that these variables have quite a bit of variation from week to week.

## ch03.31 (b)

#### Question: Plot the variable SAL1 (y-axis) against APR1 (x-axis). Is there a positive or inverse relationship? Is that what you expected, or not? Why?

```r
SAL1 <- tuna$sal1
APR1 <- tuna$apr1
plot( x = apr1, y = sal1, main = "Price to Sales", xlab = "Price", ylab = "Sales", col = "red")
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.31b.png?raw=true)

#### Answer

There is an inverse relationship between the weekly sales and weekly price.

## ch03.31 (c)

#### Question: Create the variable $PRICE1 = 100 \times APR1$. Estimate the linear regression $SAL1 = \beta_1 + \beta_2 \times PRICE1 + e$. What is the point estimate for the effect of a one cent increase in the price of brand no.1 on the sales of brand no.1 ? What is a 95% interval estimate for the effect of a one cent increase in the price of brand no.1 on the sales of brand no.1 ?

``` r
SAL1 <- tuna$sal1
APR1 <- tuna$apr1
PRICE1 <- 100*APR1
linear_model <- lm(SAL1~PRICE1)
sum_linear <- summary(linear_model)
b1 <- coef(sum_linear)[1]
b2 <- coef(sum_linear)[2]
se_b2 <-coef(sum_linear)[4]
df <- sum_linear$df[2]
t_value <- qt(0.975,df)
CI_LowerBound <- b2 - t_value * se_b2
CI_UpperBound <- b2 + t_value * se_b2
b2
CI_LowerBound
CI_UpperBound
```
b2 = -434.4473\
CI_LowerBound = -592.2897\
CI_UpperBound = -276.6049

#### Answer

- The effect of a one cent increase in the price means the margin effect of $PRICE1$,that is $\frac{∂SAL1}{∂PRICE1} = \beta_2$.
- The point estimator for $\beta_2$ is $b_2=-434.4473$.

For 95%C.I.

- We need to calculate the standard deviation of $b_2$. se($b_2$) = $\frac{\hat{\sigma}^2}{\sum(x_i-\bar{x})^2}$ and t-statistic $t_{(0.975, N-2)}$.
- The interval is $b_2 \pm se(b_2) \cdot t_{(0.975, N-2)}=[-592.2897,-276.6049]$.
- We estimate that the average weekly sales of brand one tuna will fall by between approximately 592.29 cans to 276.60 cans, with 95% confidence.

## ch03.31 (d)

#### Question: Construct a 90% interval estimate for the expected number of cans sold in a week when the price per can is 70 cents.

```r
lm_model = lm(formula = SAL1 ~ PRICE1, data = tuna)
summary(lm_model)
```

![image](https://github.com/nxthuan97/Financial-Economectric-/blob/main/Rplot03.31d.png?raw=true)

```r
b1d <- coef(lm_model)[1]
b2d <- coef(lm_model)[2]
y_hat <- b1d + b2d *70
alpha_d <- 0.1
df <- summary(lm_model)$df[2]
tc <- qt(1 - alpha_d/2, df)
se_b1 <- summary(lm_model)$coefficients["(Intercept)", "Std. Error"]
se_b2 <- summary(lm_model)$coefficients["PRICE1", "Std. Error"]
cov_matrix <- vcov(lm_model)
cov <- cov_matrix[1, 2]
var <- se_b1^2 + 70^2 * se_b2^2 + 2 * 70 * cov
se <- sqrt(var)
low_b <- y_hat - tc * se 
up_b <- y_hat + tc * se
low_b
up_b
```

low_b = 8624.934\
up_b = 11980.87

The estimated 90% interval for the average number of cans sold is between 8,624.93 and 11,980.87.

## ch03.31 (e)

#### Question: Construct a 95% interval estimate of the elasticity of sales of brand no. 1 with respect to the price of brand no. 1 “at the means.” Treat the sample means as constants and not random variables. Do you find the sales are fairly elastic, or fairly inelastic, with respect to price? Does this make economic sense? Why?

```r
mean_price = mean(PRICE1)
mean_sal = mean(SAL1)
b2d <- coef(lm_model)[2]
ela = b2d * mean_price / mean_sal1
se_b2 <- summary(lm_model)$coefficients["PRICE1", "Std. Error"]
se_ela = se_b2 * mean_price / mean_sal1
alpha = 0.05
df <- summary(lm_model)$df[2]
t_value = qt(1-alpha/2, df)
ci_lower = ela - t_value * se_ela
ci_upper = ela + t_value * se_ela
ci_lower
ci_upper
```
ci_lower = -6.89815
ci_upper = -3.221502

#### Answer
- $SAL1=\beta1+\beta2PRICE1$\
mean($PRICE1$)=78.25\
mean($SAL1$)=6718.712\
$\epsilon =\cfrac{\frac{\Delta y}{y}}{\frac{\Delta x}{x}}$
$=m\frac{x}{y}$
$=\beta2 \frac{PRICE1}{SAL1}=$ -5.0598
- For 95% C.I.\
We need to calculate the standard deviation of $\epsilon$ and t-statistic\
$se(\epsilon)=se(\beta2)\times \frac{PRICE1}{SAL1}=$ 0.9152\
t-statistic $=t_{(0.975, N-2)}$\
The interval is $\epsilon\pm t_{(0.975, N-2)}\times se(\epsilon)$
- From R, we get\
point estimator = -5.0598\
t-statistic = 2.0086\
$se(\epsilon)=$ 0.9152\
so 95% C.I. = [-6.8981,-3.2215]

We estimate with 95% confidence that the elasticity of expected sales of brand 1 tuna is between −6.9% and −3.2%.

## ch03.31 (f)

#### Question: Test the hypothesis that elasticity of sales of brand no. 1 with respect to the price of brand no. 1 from part (e) is minus three against the alternative that the elasticity is not minus three. Use the 10% level of significance. Clearly, state the null and alternative hypotheses in terms of the model parameters, give the rejection region, and the p-value for the test. What is your conclusion?

```r
t_value <- (ela - (-3)) / se_ela
p_value <- 2 * pt((t_value), df)
t_critical <- qt(0.95, df)
t_value
p_value
t_critical
```

t_value = -2.250573\
p_value = 0.02884199\
t_critical = 1.675905

#### Answer
1. The hypothesis is $H_0:  elasticity = -3 \ v.s. \ H_1: elasticity \neq -3$.This is a two-tailed tests.
2. Test statistic: $t_{(0.975, 50)} = 1.675905 $
3. t-value = (-5.059825 +3) /0.9152 = -2.25
4. p-value = 0.0288 < 0.1

We reject the null hypothesis. There is an evidence that the elasticity is 3 is possibly not correct. And we conclude that the elasticity is possibly not -3.

---
