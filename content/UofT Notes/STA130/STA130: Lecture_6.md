---
title: "STA130: Lecture_6"
tags: [Note]
date: [2021-01-17]
---

# Estimation and random selection

- Over-dependence on p-values may cause invalid results in the scientific process
- The choice of $\alpha$ is arbitrary, it's better to either comment on the strength of the evidence against $H_0$ by reporting the p-value, or at least make sure to choose a $\alpha$ before calculating the p-value

- 2 main branches of statistical inference

  1. **Testing** - hypothesis test (evaluate evidence against a particular value for parameter)
  2. **Estimation** - confidence interval (estimate of a parameter, gives range of plausible values of parameter)

  - Both based on <u>statistics</u> (estimates of parameters from sample) and <u>sampling distributions</u> (estimates of them of statistics)

- Goals of estimation:

  - Want to find something about a population, resultant value is the **true value** of the **parameter**
  - Can't get to everyone, some take a **random sample** from the population to estimate
  - An estimate is just an estimate, to try to count for the fact that it is probably **wrong**, but hopefully **close** to the true value.

## Estimates, parameters and many samples

- The function `sample_n()` from `dplry` can be used to draw samples of any size form a data frame (default is to sample without replacement)

  ```R
  sample25 <- <dataset> $>$ sample_n(size=25, replace = FALSE)
  ```

  - This function samples **rows** (observations) from a data frame, with or without replacement. While the `sample()` function samples elements from a **vector**, with or without replacement

- As the sample size increase:
  - The mean of the sampling distribution - *stay roughly the same (approx. the parameter)*
  - The shape of the sampling distribution - *less skewed*
  - The spread of the sampling distribution - *less spread out*

## The Bootstrap Method

- The sample must be **representative** of the full population

  ![Screen Shot 2021-02-22 at 03.15.23](https://tva1.sinaimg.cn/large/008eGmZEly1gnwdsudmthj31940u0kjl.jpg)

- Start with a sample of size `n` from the population (assume it is representative)
  1. Draw many bootstrap samples of size `n` (with replacement) from the original sample
  2. For each bootstrap sample, calculate the statistic
- The distribution of the values of the statistics for all bootstrap samples is the **bootstrap sampling distribution** (this is another estimate of the sampling distribution of the statistic)
- Note that bootstrapping does *not* create new data. It simply is a tool to allow us to explore the variability of estimates from our **original** sample.

|                         | Bootstrapping                                                | Hypothesis Test                                              |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Initial data production | Random sample from a population of interest                  | - Random sample from a population of interest AND  assignment of units to treatment groups |
| re-sample               | Random re-sample (with replacement) from the original sample | Random re-assignment of labels                               |
| Goal                    | Create a range of plausible values for the population parameter | Conclude if we can rule out the 'chance-was-acting-alonee' explanation because it's implausible |
