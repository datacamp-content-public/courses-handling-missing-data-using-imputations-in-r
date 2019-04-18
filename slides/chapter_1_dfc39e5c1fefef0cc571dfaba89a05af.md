---
title: Insert title here
key: dfc39e5c1fefef0cc571dfaba89a05af

---
## Predictive Mean Matching (PMM)

```yaml
type: "TitleSlide"
key: "326ebe58c1"
```

`@lower_third`

name: Hafsa Jabeen
title: Instructor at DataCamp


`@script`
By now you have seen imputation under normal-linear and non-normal distributions. Continuing with the univariate imputation methods, Predictive Mean Matching (PMM) is another method for univariate missing data imputation but it imputes values that are more realistic. Let's get stated!


---
## What is PMM?

```yaml
type: "FullSlide"
key: "b992a3ebac"
```

`@part1`
- PMM is the method of imputing missing values by predicting the values by selecting donors (typically 3, 5, or 10) from complete cases.
- Originally developed for monotonic missing pattern where only a single variable is missing data
- It builds a **linear regression model** on complete observations to find the coefficients
- Uses the coefficients to predict values for missing and non-missing cases 
- One donor is randomly drawn from a set of candidates whose predicted value is closer to predicted value of missing case and the observed value of the donor is taken to replace the missing value.


`@citations`
1. https://stefvanbuuren.name/fimd/sec-pmm.html
2. https://statisticalhorizons.com/predictive-mean-matching


`@script`
PMM is the method of imputing missing values by predicting the values based by selecting donors from complete cases. 
  - Originally developed for monotonic missing pattern where only a single variable is missing data. 
- It builds a **linear regression model** on complete observations to find the coefficients
- Uses the coefficients to create a new set of coefficients and uses them to predict values for missing and non-missing cases both. 
- One donor is randomly drawn from a set of candidates whose predicted value is closer to predicted value of missing case and the observed value of the donor is taken to replace the missing value.


---
## title

```yaml
type: "FullSlide"
key: "663c374de2"
hide_title: true
```

`@part1`
- It is used to impute quantitative data that is not normally distributed

- **More realistic values**:
- bounded variables
- E.g age of person is not imputed negative
- original variable is discrete then imputed value will also be discrete


`@citations`
2. https://statisticalhorizons.com/predictive-mean-matching


`@script`
As compared to methods in previous lessons , PMM imputes more realistic values taking care of the problem of boundaries on variable values. For example if a variable is discrete variable then imputed values will also be discrete. For example a study observes the age of respondents so age can't be negative, PMM will make sure that imputed age is never negative. This is because, PMM borrows values from complete observations.


---
## Example

```yaml
type: "FullSlide"
key: "c019d15a0a"
```

`@part1`
![](https://assets.datacamp.com/production/repositories/4908/datasets/66afc95a54577536db91b06971c6e2f24bc3e423/ch03-misspecify-1.png)

Robustness of predictive mean matching (right) relative to imputation under the linear normal model (left).


`@citations`
https://stefvanbuuren.name/fimd/sec-pmm.html#fig:misspecify


`@script`
Figure illustrates the robustness of predictive mean matching relative to the normal model. The figure displays the body mass index (BMI) of children aged 0–2 years. BMI rapidly increases during the first half year of life, has a peak around 1 year and then slowly drops at ages when the children start to walk. 

The imputation model is, however, incorrectly specified, being linear in age. Imputations created under the normal model display in an incorrect slowly rising pattern, and contain several implausible values. 
Look at BMI values that start to drop between 0.5-1.0.

In contrast, the imputations created by predictive mean matching follow the data quite nicely, even though the predictive mean itself is clearly off-target for some of the ages. See BMI points between 0.5-1.0, unlike normal imputation values are according to specification. This example shows that predictive mean matching is robust against misspecification, where the normal model is not.


---
## PMM in R

```yaml
type: "FullSlide"
key: "4d8b556fb3"
```

`@part1`
- PMM now has been implemented in several software packages, MICE in R, Strata, SAS to impute any missing data pattern
- MICE supports both single and multiple imputation using PMM

![](https://assets.datacamp.com/production/repositories/4908/datasets/a3d65bc0d485a974e92d3fae0c918724b5f34e17/Table-1-First-6-Rows-with-Missing-Data-for-Our-Predictive-Mean-Matching-Example.png)


`@script`
Let's apply PMM on this example dataset named 'data' having Y1 as target variable which has missing values and four predictor variables X1, X2, X3 and X4. 

Y1 has 20% missing data.
Let's first apply single imputation using MICE


---
## Insert title here...

```yaml
type: "FullSlide"
key: "5ae674266d"
hide_title: true
```

`@part1`
## Single PMM Imputation using MICE
Install the package:
```
install.packages("mice")
library("mice")
```
Consider the dataset named 'data' having missing values
```
single_imp<- mice(data, m = 1, method = "pmm")
```
To store the imputed data using **'complete()'** function
```
data_imp<- complete(single_imp)
```


`@script`
Here MICE will run PMM to impute missing values once. To install the package use install.packages("mice") and then include it in your program using
library("mice").

use the method mice([datasetname], m=[number of imputations], method="pmm") to impute misisng values because this is single imputation "m=1".

Then save your imputed dataset by using the "complete([imputedobject])" method and store in an object.


---
## Insert title here...

```yaml
type: "FullSlide"
key: "72724df2bf"
hide_title: true
```

`@part1`
## Multiple PMM Imputation using MICE

Consider the dataset named 'data' having missing values
```
multiple_imp<- mice(data, m = 5, method = "pmm")
```
To store the imputed data using **'complete()'** function and use arguments **“repeated”** and **'include = TRUE'**

```
data_imp_all<- complete(multiple_imp, repeated, include=TRUE)
```


`@script`
Here MICE will run PMM to impute missing values more than once.

use the method mice([datasetname], m=[number of imputations], method="pmm") to impute misisng values because this is multiple imputation use the any number of imputations as required. here it is 5.

Then save your multiple imputed dataset by using the "complete([imputedobject])" method along with the arguments: "repeated" and "include=TRUE" that tell complete method how to store the multiple imputed results.


---
## Insert title here...

```yaml
type: "FullSlide"
key: "54aa830fea"
hide_title: true
```

`@part1`
## Output of Multiple PMM imputation
![](https://assets.datacamp.com/production/repositories/4908/datasets/82965dad2056b4622f193c259a3c6fa8e7e3783a/Table-2-First-6-Rows-with-Multiply-Imputed-Values.png)


`@citations`
https://statistical-programming.com/predictive-mean-matching-imputation-method/#references


`@script`
Y.0  is equal to the original Y with missing values.
Y.1–Y.5 are the five imputed versions of Y.
X1–X4 are the four predictor variables that we used as predictors for the imputation.
By comparing rows 4 and 6, i.e. the rows with NAs, you can see the effect of multiple imputation. While Y.0 contains missings, Y.1–Y.5 are filled with imputed values. 

Note that the imputed values are different in all 5 imputations. 

So, why are you seeing such differences? the answer is that this tells how much uncertainty is there in our imputation by which we can calculate standard errors that are more correct. So in way it is a good result.


---
## Things to Remember about PMM

```yaml
type: "FullSlide"
key: "86e2a5ec7c"
```

`@part1`
- Defaut value of donors (d=5) in MICE package in R for continuous data
- Number of donors have an effect on imputed values
- PMM works best large data sets to get better donors
- Does not work well with sparse data
- Cannot be used to impute values outside the range of data
- PMM is less vulnerable to model misspecification and avoids meaningless imputations.


`@citations`
https://stefvanbuuren.name/fimd/sec-pmm.html#fig:misspecify


`@script`
The method works best with large samples
Predictive mean matching cannot be used to extrapolate beyond the range of the data, or to interpolate within the range of the data if the data at the interior are sparse. Also, it may not perform well with small datasets. 
The effect of number of donors on PMM is explained in detail in the given citation in this slide.


---
## Let's practice!

```yaml
type: "FinalSlide"
key: "c8fbb9fbbe"
```

`@script`


