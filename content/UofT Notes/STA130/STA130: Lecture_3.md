---
title: "STA130: Lecture_3"
tags: [Note]
date: [2021-01-17]
---

# Tidy data and data wrangling

> "Write code for humans, write data for computers" -- Vince Buffalo July 20, 2013

- Tidy - data are in a predictable and expected format (convenient for computer to use)

## Principles of "tidy" data

1. Each **variable** must have its own **column** (ex. Student name)
2. Each **observation** must have its own **row** (ex. Student's grade on one specific HW)
3. Each **value** must have its own **cell** (ex. The grade of the HW)

> ##### Example of a tidy data
>
> ```text
> ##		country			year	cases		population
> ##		<chr>			<int>	<int>		<int>
> ## 1	Afghanistan		1999	745			19987071
> ## 2	Afghanistan		2000	2666		20585360
> ## 3	Brazil			1999	37737		172006362
> ## 4	Brazil			2000	80488		174504898
> ## 5	China			1999	212258		1272915272
> ## 6	China			2000	213766		1280428583
> ```

### Recognizing tidy data

- Its easier to describe functional relationships between variables than between rows
- Its easier to make comparisons between groups of observations than between groups of columns

## Data Wrangling

- <u>Data wrangling</u> -- transform tibbles to make them more useful to answer interesting questions
  - Make it more **tidy**
  - **Extract** subsets observations/remove observations that is not in the interested focus
  - Remove unnecessary variables to **simplify** the data
  - **Create** new interesting/useful variables
  - **Sort** by the values of one fore more variables

### Functions from `dplyr` (included in the `tidyverse` library)

- Using `filter()` to extract only the observations/**rows** where the condition is **TRUE**

  > ```R
  > olympics %>% filter(athletes_total >= 300)
  > ```

- Using `select()` to extract only the interested variable/**columns** 

  > ```R
  > olympics %>% select(Country, athletes_total, gold, silver, bronze)
  > ```

- Combining `filter()` and `select()` to create tibbles to get desired value

  > ```R
  > bigteams <- olympics %>%  # orginal data
  > 	filter(athletes_total >= 300) %>%  # tibble with 8 rows & all columns
  > 	select(Country, athletes_total, gold, silver, bronze)  # 8row & 5columns
  > bigteams ## type the name of the R object to print it
  > ```

- **Create** new **numeric** variables using `mutate()`

  > ```R
  > olynew <- olympics %>%
  > 	mutate(total_medals = gold + sliver + bronze,  # name = def_of_variable
  >            avg_medals = toal_medals / athletes_total) %>%
  > 	select(Country, athletes_total, gold, silver, bronze, total_metals, avg_medals)
  > ```

  - **Define** new **categorial** variables using `case_when()`

    > ```R
    > oly_newvar <- olympics %>%
    > 								# logical condition ~ output value
    > 	mutate(majority = case_when(athletes_f > athletes_m ~ "Female",
    >                                 athletes_f == athletes_m ~ "Balanced",
    >                                	athletes_f < athletes_m ~ "Male"),
    >            total_medals = gold + silver + bronze)
    > oly_newvar %>% select(Country, athletes_total,
    >                       athletes_f, athletes_m, majority, total_medals)
    > ```

- Sort observations based on new or existing variables using `arrange()`

  - `arrange()` sort in increasing order(**small to big**), while `arrange(desc())` sorts in decreasing order(**big to small**)

  > ```R
  > olynew %>%
  > 	arrange(desc(total_medals)) %>%  # arrange from big to small
  > 	select(Country, total_medals, avg_medals) %>%
  > 	head()  # display the output
  > ```

## Summary tables and missing values

- Create a simple summary table using `summarise()`[^1], some helper function

  - `n()` - the number of observations in the current group
  - `mean()` returns the mean of a numeric vector or column in a tibble
  - `min()` returns the min of a numeric vector or column in a tibble
  - `max()` returns the max of a numeric vector or column in a tibble
  - `median()` returns the median value of a numeric vector or column in a tibble
  - `var()` returns the variance of a numeric vector or column in a tibble
  - `sd()` returns the standard deviation of a numeric vector or column in a tibble
  - `sum()` returns the sum of a numeric vector or column in a tibble

  > ```R
  > olympics %>% summarise(n=n(),
  >                        mean_gold=mean(gold),
  >                        min_mod=min(gold),
  >                        max_gold=max(gold))
  > ```

  [^1]: the Canadian/British spelling for the American `summarize()`, both works

- Create more complex summary table using `group_by()` and `summarise()`

  > ```R
  > olympics %>%
  > 	mutate(teamsize = case_when(athletes_total >= 100 ~ "big",
  >                                 athletes_total < 100 & athletes_total >= 20 ~ "medium",
  >                                 athletes_total < 20 ~ "small")) %>%
  > 	group_by(teamsize) %>%
  > 	summarise(n=n(),
  >                        mean_gold=mean(gold),
  >                        min_mod=min(gold),
  >                        max_gold=max(gold))
  > ```

- Use `is.na()` to identify missing values

  - Can be used with `filter()` to extract only observations with missing values

  > ```R
  > > x <- c(1, 2, 3, NA, 5, NA)
  > > is.na(x)
  > [1] FALSE FALSE FALSE TRUE FALSE TRUE
  > ```

> ##### Create a summary table exclude the missing value, grouped by majority(`oly_newvar` from above *case_when()* example), and has the variable mean, min, max
>
> ```R
> oly_newvar %>%
> 	filter(!is.na(majority)) %>%
> 	group_by(majority)
> 	summarize(n=n(),
>            mean_medals=mean(gold + silver + gold),
>            min_medals=min(gold + silver + gold),
>            max_medals=max(gold + silver + gold))
> ```
>
> Output:
>
>
> ```text
> ## # A tibble: 3 x 5
> ##   majority	n		mean_medals	min_medals	max_medals
> ##   <chr>		<int>	<dbl>		<dbl>		<dbl>
> ## 1 Balanced	25		0.6			0			12
> ## 2 Female		34		10.8		0			104
> ## 3 Male		144		4.02		0			65
> ```