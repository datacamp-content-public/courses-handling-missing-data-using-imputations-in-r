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
- PMM is the method of imputing missing values by predicting the values by selecting donors from complete cases.
- Originally developed for monotonic missing pattern where only a single variable is missing data
- It builds a **linear regression model** on complete observations to find the coefficients
- Uses the coefficients to predict values for missing and non-missing cases 
- One donor is randomly drawn from a set of candidates whose predicted value is closer to predicted value of missing case and the observed value of the donor is taken to replace the missing value.


`@citations`
1. https://stefvanbuuren.name/fimd/sec-pmm.html
2. https://statisticalhorizons.com/predictive-mean-matching


`@script`
PMM is another attractive method of imputing missing values. PMM is the method of imputing missing values by predicting the values based by selecting donors from complete cases. 

Here you will have high-level understanding of the PMM.  
- Originally developed for monotonic missing pattern where only a single variable is missing data. 
- It builds a **linear regression model** on complete observations to find the coefficients
- Uses the coefficients to predict values for missing and non-missing cases and creates a new set of coefficients and uses them to predict values for all cases;missing and non-missing cases both. 
- One donor is randomly drawn from a set of candidates whose predicted value is closer to predicted value of missing case and the observed value of the donor is taken to replace the missing value.
PMM is less vulnerable to model misspecification by making it implicit which means there is no need to explicitly define distribution of missing values and avoid meaningless imputations.


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
## Let's practice!

```yaml
type: "FinalSlide"
key: "c8fbb9fbbe"
```

`@script`


