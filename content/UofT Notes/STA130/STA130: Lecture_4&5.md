---
title: "STA130: Lecture_4&5"
tags: [Note]
date: [2021-01-17]
---

# Hypothesis testing

> ### Wheel of Destiny Question
>
> >  "Back before COVID, Stella McStat has been running a small-time gambling operation on campus for several months. For a dollar each, Stella sells
> >  one **red** and one **black** ticket for each spin of a wheel (i.e., total \$2), then she spins the Wheel of Destiny. The person who holds the colour where the spinner stops gets ​\$1.75 (Stella keeps $0.25 per spin for running the game and providing snacks).
> >
> > Stella is setting up a new online gambling operation (streaming on Twitch) and just bought a new spinner, the critical piece of equipment for this game. Before she beings using this spinner, she wants to make sure that it is, in fact, fair—she wants both colours to come up equally often. Because of the set-up of the game, Stella has no incentive to cheat and wants the game to be as fair as possible."
>
> #### Test the spinner
>
> > Let's say you spun the spinner 50 times and got **red** 32 times.
> >
> > Based on our observed data, can you answer Stella's question? Is the Wheel of Destiny fair?
>
> We need to *compare* our observed value to something: the distribution of what we would expect to see if the spinner *really* was fair...
>
> - **Core Question:** If the spinner *was* fair, out of 50 spins, what number of *reds* would be usual/unusual?
> - **Histogram:** If you were to spin the spinner 50 times, and record the number of *reds*, and repeated 100 times (100sets of 50 spins with record number of *reds* in each set of 50 recorded) what would this histogram look like?
>
> #### Generalize the program
>
> - If the spinner is fair, then the proportion of *red* in 50 spins would be **equivalent** to the proportion of heads in 50 flips of a fair coin (both 50/50 chance)
> - Possible **explanations** for what is observed
>   1. The new Wheel of Destiny is fair, what is observed 32/50 is gotten by chance
>   2. The new Wheel of Destiny is not fair
> - **Where do things stand now**
>   1. Conclude for certain whether the new spinner is fair or unfair?
>   2. Calculate the probability that the new spinner is fair?
>   3. Calculate the probability that the new spinner is unfair?
> - Answer Stella's question
>   - **Conclusion A:** Our sample results are consistent with results we would observe if the spinner is fair
>   - **Conclusion B:** Our sample results are not consistent with the results we should observe if the spinner was fair. In other words, we have evidence against the hypothesis that the spinner is fair

## Statistical Inference

- <u>Statistical inference</u> - the process of **coming to conclusions** or decisions based on statistical information (information object to randomness and uncertainty)

  - The conclusions are uncertain (can't be 100% sure that it represents the truth because the given information is incomplete)

  > Ex. Making conclusion about **population** using data from a **random sample**

- <u>Parameter</u> ($p$ or $\pi$) - the number that describes the **population** (for the population focused on)

- <u>Statistic</u> - the number that describes the **sample** (change from sample to sample)

  > Ex. Sample mean, median, variance, etc.

- <u>Test statistic</u> ($\hat{p}$ or $\hat{\pi}$) - a special statistic that decides whether the data is compatible with $H_0$

> ##### Wheel fo Destiny:
>
>    | *Term*                | *Wheel of Destiny example*                           |
| :-------------------- | ---------------------------------------------------- |
| <u>Population</u>     | **All spins** of the wheel of destiny                |
| <u>Parameter</u>      | The true(long-run) **probability** of spinner in red |
| <u>Sample</u>         | The 50 **observed** spins                            |
| <u>Test statistic</u> | The sample's **proportions** of red in the 50 spins  |

- <u>Sampling distribution</u> of statistics(proportion) - the distribution fo statistic values taken for all possible samples of the same size ($n$) from the same population

  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gn709vsg71j30mu0fo795.jpg" alt="Screen Shot 2021-01-31 at 01.55.07" style="zoom:25%;" />

### Hypothesis Testing

- <u>Hypothesis Testing</u> is one type of statistical inference

- There is always an element of chance in any sampling. What we are curious about is if **chance is acting alone** or if what we see is due to **chance AND something else.**

- Sometimes statistical inference is not appropriate

  > Ex: if we have data for ALL individuals in the population, there is nothing to *infer*.

- <u>Null hypothesis</u> - use the notation $H_0$ (said as “aitch naught”), the **default setting**

  - **There is *not enough* evidence against the claim that the defendant is innocent** (Think about the null hypothesis as the ‘boring’ or ‘status quo’ or ‘nothing–going-on-option’)
- There is **no differences** in...
  - $H_0:parameter=value$  ($H_0$ is a table, don't put equal marks with it)
  - <u>p-value</u> - the probability of observing data that are **at least as unusual** (or **at least as extreme**) as the sample data, *under the assumption that $H_0$ is true* 
    - Estimate it as the proportion of values in the estimated sampling distribution that are as extreme or more extreme than the test statistic calked from the observed sample data

- <u>Alternative hypothesis</u> - use the notation $H_1$, covers everything that is **not** the value in the null

  - **There is enough evidence against the claim that the defendant is innocent**
  - There **is a difference** in...
  - $H_1:paramter\neq value$

## Steps for Hypothesis Testing (one proportion)

1. State **hypothesis** $H_0$ and $H_1$

2. Calculate a **test statistic** based on the observed sample data

3. Simulate samples under the null hypothesis, and calculate the statistic for each one (estimate **sampling distribution**)

   - Goal: Explore the distribution of values of the statistic if $H_0$ is true. What kind of results are common under the null? What are unusual?

   Simulation: a way to explore random events (use `R`) **(assume $H_0$ is true)**

   - Using `sample()` function that create a sample for the simulation

     ```R
     simdata <- <data> %>%
     	mutate(<varaible> = sample(<variable)) 
     ```

   1. Set values for simulation (sample size, number of repetitions, seed)

      ```R
      sample(c("p1, p2"),  # vecor with all possible outcomes
             size = <int>,  # num of values in sample
             prob = c(<dbl>, <dbl>),  # prob of each outcome (ading to 1)
      								# (default is equal to probs)
             replace = TRUE)  # can outcomes be repeated (default=FALSE)
      ```

   2. Use a `for` loop to simulate many random samples and calculate the statistic of interest of each one

      ```R
      set.seed(<int>)  # Set a starting point (make sure its the same across simulation)
      
      for (i in 1:<int>)
      {
          SOME CODE (loop through sample)
      }
      ```

   3. Turn results into a data frame (`tibble()`) so `ggplot` can be used

      ```R
      <str> <- tibble(<variable> = mean(<sample> == "<interested_condition>"))
      ```

   4. Plot the results

      ```R
      # Dotplot
      <data> %>% ggplot(aes(x=<variable>)) +
      	geom_dotplot() + xlim(0,<int>) + ylim(0,<int>) # <int> is upper limit
      ```

4. Evaluate the evidence against $H_0$ by calculating the **p-value** (probability of more extreme than observed sample)

   - 2 possible reasons for small p-value
     1. $H_0$ Is true and the observed case is an *unlikely extreme value* of the statistic
     2. $H_0$ Is not true
   - **The smaller the p-value, the more "evidence" is against $H_0$, possible reasons**
   - P-value: all values **great or equal to** ($p + |\hat{p}-p|$) and all values **less than or equal to** ($p-|\hat{p}-p|$). This is a **two-sided test** (considers both large and smaller samples)

5. Make a **conclusion**

   | *p-value*              | *Evidence*                                         |
   | ---------------------- | -------------------------------------------------- |
   | 0.10 < p-value         | No evidence against $H_0$                          |
   | 0.05 < p-value < 0.10  | Weak evidence against $H_0$                        |
   | 0.01 < p-value < 0.05  | Moderate evidence against $H_0$ (default $\alpha$) |
   | 0.001 < p-value < 0.01 | Strong evidence against $H_0$                      |
   | p-value < 0.001        | Very strong evidence against $H_0$                 |

   - <u>Statistical significant</u> (or **statistically significance** difference)
     
     - A significance level ($\alpha$) set in advance determines the **cut-off for how unusual/extreme test statistic has to be** (assuming $H_0$ is true) in order to reject the assumption that $H_0$ is true
     - **Reject $H_0$ if p-value $\le \alpha$**
     - $\alpha$ Can be chosen to be any number, but typically $\alpha = 0.05$
     
   - It is **better** to report the p-value and comment of the *strength of evidence against $H_0$* instead of only reporting whether the result is/isn't statistically significant
   
     | $\alpha$ | Ex. 1 (Fail to reject)                                       | Ex. 2 (Reject)                                               |
     | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
     | 0.1/ 10% | P-value = 0.21; "At the 10% significance level we fail to reject $H_0$" | P-value = 0.093; "At the 10% significance level we can reject $H_0$" |
     | 0.05/ 5% | P-value = 0.093; "At the 10% significance level we fail to reject $H_0$" | P-value = 0.037; "At the 10% significance level we can reject $H_0$" |
     | 0.01/ 1% | P-value = 0.037; "At the 10% significance level we fail to reject $H_0$" | P-value = 0.007; "At the 10% significance level we can reject $H_0$" |

> > We had a question about Stella;s new Wheel of Destiny: Is the new Wheel of Destiny fair
>
> 1. State **hypothesis** 
>    - The Wheel of Destiny spinner is fair: $H_0:p_{red}=0.5$, 
>    - The Wheel of Destiny spinner is not fair: $H_1:p_{red} \neq 0.5$
>    - Where $p_{red}$ is the proportion of spins of the new Wheel of Destiny that land on red
>
> > We observed the results of 50 spins and calculated the proportion fo red outcomes
>
> 2. Calculate a **test statistic**: $\hat{p}_{red} = \frac{32}{50} = 0.64$
>
>    ```R
>    test_stat <- 32/50
>    ```
>
> > We looked at the distribution of for 50 spins of a fair spinner (many times); instead of a spinner, lots of students flipped a fair coin 50 times and recorded the proportion of heads (equivalent because both are 50/50 processes)
>
> 3. Estimated **sampling distribution**: assumptions of a 50/50 process ($H_0$)
>
>     ```R
>     # (1) Set values for simulation
>     n_observations <- 50  # num of observations
>     repetitions <- 1000  # num of simulations
>     simulated_stats <- rep(NA, repetitions)  # 1000 missing vlaues to start
>
>     # (2) Automate simulatio for a for loop
>     for (i in 1:repetitions)
>     {
>         new_sim <- sample(c("red", "black"),  
>                           size = n_observations,
>                           prob = c(0.5, 0.5),  
>                           replace = TRUE)
>         sim_p <- sum(new_sim == "red") / n_observations
>
>         simulated_stats[i] <- simp_p;  # add new value to vector of results
>     }
>
>     # (3) Turn results into a data frame
>     sim <- tibble(p_red = simulated_stats)
>
>     # (4) Plot results
>     sim %>% ggplot(aes(x=p_heads)) +
>     	geom_histogram() +
>     	xlabs("Proportion of red coutcomes in 50 spins of a 
>     		  fair Wheel of Destiny \n (p_red = 0.5)")
>     ```
>
>     <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gn70bu875mj31ak0h0whn.jpg" alt="Screen Shot 2021-01-31 at 03.24.40" />
>
> >We compared our observed value to the distribution of proportions observed from the fair spinner (or fair coin) to assess if the new spinner's behaviour is consistent with the behaviour of a fair spinner
>
> 4. Calculating the **p-value** (we have only done this *informally* so far)
>
>    - $H_0: p_{red}=0.5$
>    - Test statistic $\hat{p}_{red} = \frac{32}{50}=0.64$
>    - All values **great or equal to** $\hat{p}_{red}$ and all values **less than or equal to** $0.5-|\hat{p}_{red}-0.5|$.
>
>    ```R
>    test_stat <- 32/50
>    sim %>% gglot(aes(x=p_red)) +
>    	geom_histogram() + 
>    	geom_vline(xintercept = 0.5 - abs(0.5 - test_stat), color = "red") +
>    	geom_vline(xintercept = -.5 + abs(0.5 - test_stat), color = "blue") +
>    	labs(x = "Simulated proportions red outcomes form a fair spinner
>             (proportions based on samples of size n=50)")
>    ```
>
>    ![Screen Shot 2021-01-31 at 03.46.51](https://tva1.sinaimg.cn/large/008eGmZEly1gn70cd2mxej31900cagoa.jpg)
>
>    ```R
>    pvalue <- sim %>%
>    	filter(p_red >= 0.64 | p_red <= 0.36) %>%
>    	summarize(p_value = n() / repetitions)
>    as.numeric(pvalue)
>
>    ## [1] 0.065
>    ```
>
>    - The smaller the p-value, the more "evidence" is against $H_0$
>
> > We answered Stella's question based on the data we collected.
>
> 5. Make a **conclusion**: 
>
>    - Since the p-value is 0.065, we could conclude that we have **weak evidence** **against the null hypothesis** that the Wheel of Destiny spinner is fair. (Not enough evidence to reject $H_0$)
>
>    - *The result of our testing protocol wasn’t so unusual that we would claim the spinner isn’t fair...but it is a little borderline*

## Errors

|               | Fail to reject $H_0$ | Reject $H_0$        |
| ------------- | -------------------- | ------------------- |
| $H_0$ Is true | 👍🏼                   | <u>Type 1 error</u> |
| $H_1$ Is true | <u>Type 2 error</u>  | 👍🏼                  |

- <u>Type 1 error</u> - reject $H_0$ when $H_0$ is true
  - Even when we set chance to be very small (i.e. need a very extreme/unusual observed test statistic to reject $H_0$, we could still observe a very unusual outcome and end up rejecting $H_0$ when we should not).
- <u>Type 2 error</u> - fail to reject $H_0$ when $H_0$ is false (and should be rejected)
  - When we don't reject a null hypothesis (i.e. the results don't look unusual compared to the sampling distribution assuming $H_0$ is true), it is still possible that $H_0$ may not be true.

---

In second year Stats:

- Determine the sampling distribution exactly by using:
- <u>Binomial probability model</u> - used to count the number of "successes" in independent trials, where each trial has two possible outcomes: "success" with probability or "failure" with probability $(1-p)$
  - Probability of successes in trial is $C^{k}_{n}p^{k}(1-p)^{n-k}$