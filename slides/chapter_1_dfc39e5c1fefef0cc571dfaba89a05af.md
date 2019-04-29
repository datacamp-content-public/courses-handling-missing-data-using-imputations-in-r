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
Continuing with the univariate imputation methods, Predictive Mean Matching (PMM) is another method for univariate missing data imputation but it imputes values that are more realistic. In this lesson you will learn about PMM and how to use it in R.


---
## What is PMM?

```yaml
type: "FullSlide"
key: "b992a3ebac"
```

`@part1`
![](https://assets.datacamp.com/production/repositories/4908/datasets/dabc5246cb9cf8098620f1cf89a44cb38f3e1dfd/pmm1.jpg)


`@script`
- PMM is the method of imputing missing values by predicting the values by selecting donors (typically 3, 5, or 10) from complete cases.
PMM was developed for monotonic missing pattern where only a single variable is missing data. 
So here are the steps of how pmm replaces missing values:
Step1: you have data that has missing values 
Step2: It builds a linear regression model on complete observations to find the coefficients
Step3: Uses the coefficients to create a new set of coefficients
Step4: uses new coefficients to predict values for missing and non-missing cases both. 
Step5: A set of donors is drawn from complete data
whose predicted value is closer to predicted value of missing case
Step 6: One donor is selected randomly and its observed value is taken to replace the missing value.


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
As compared to methods in previous lessons , PMM imputes more realistic values taking care of the problem of boundaries on variable values. For example a study observes the age of respondents so age can't be negative, PMM will make sure that imputed age is never negative. This is because, PMM borrows values from complete observations.


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
Let's apply PMM on this example dataset named 'data' having Y1 as target variable which has missing values and four predictor (indep) variables X1, X2, X3 and X4. 

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

Consider the dataset named 'data' having missing values
```
single_imp<- mice(data, m = 1, method = "pmm")
```
To store the imputed data using **'complete()'** function
```
data_imp<- complete(single_imp)
```


`@script`
to impute missing values use the method mice that uses [datasetname], m which is [number of imputations] and method which will be "pmm").
Because this is single imputation "m=1".

Then save your imputed dataset by using the "complete()" method and pass the imputed data created by mice() method and store in an object.


---
## Insert title here...

```yaml
type: "FullSlide"
key: "72724df2bf"
hide_title: true
```

`@part1`
## Multiple PMM Imputation using MICE

```
multiple_imp<- mice(data, m = 5, method = "pmm")
```
To store the imputed data using **'complete()'** function and use arguments **“repeated”** and **'include = TRUE'**

```
data_imp_all<- complete(multiple_imp, repeated, include=TRUE)
```


`@script`
Here MICE will run PMM to impute missing values more than once.

use the method mice that uses [datasetname], m which is the [number of imputations] and method="pmm") to impute misisng values. because this is multiple imputation use any number of imputations as required. here it is 5.

Then save your multiple imputed dataset by using the "complete()" method passing the imputed data along with the arguments: "repeated" and "include=TRUE" that tell complete method how to store the multiple imputed results.


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
Here is the result of multiple imputation.
Y.0  is equal to the original Y with missing values.
Y.1–Y.5 are the five imputed versions of Y.
X1–X4 are the four predictor variables that we used as predictors for the imputation.
By comparing rows 4 and 6, i.e. the rows with NAs, you can see the effect of multiple imputation. Note that the imputed values are different in all 5 imputations. 

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


