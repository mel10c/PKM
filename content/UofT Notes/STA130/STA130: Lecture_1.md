# Intro to Statistics

- <u>Statistics</u> - arts and science of **learning from data**. Its a way to quantify **uncertainty**
- <u>Data Science</u> - includes the computational aspects and acquiring, managing, and analyzing data
  - **Reasoning** and **computing** are both important aspects in data science

### Statistical Thinking

- Always be aware of the ==assumptions== made, are they **justified**?
- **Think about where the data came from**
  - Is the data a <u>==random sample==</u> (**representatives** of all sample) ? 
    - <u>Survivorship Bias</u> - only data that survived the phenomena were left, therefore these data would not be random sample
  - Are the data and the assumptions **correlated**?

## Introduction to `R` and RStudio

> - <u>Console</u> - excites each line of code
> - <u>Source</u> - open, view, and edit code and save for later
> - <u>Environment</u> - list objects (variables, data frames)

- Assigning variables: using `<-` operator
- Comment using `#` symbol in R

- <u>Element</u> - a single piece of data, can be one fo several data types:

| **Data Type** | **R Sytax** | **Description**                                   | **Examples**         |
| ------------- | ----------- | ------------------------------------------------- | -------------------- |
| Integer       | `int`       | Numbers (integers)                                | -4, -2, 1, 3         |
| Double        | `dbl`       | Numbers (floats)                                  | 2, 2.02, 22222       |
| Logical       | `lgl`       | Booleans                                          | TRUE, FALSE          |
| Character     | `chr`       | Strings                                           | "I", "I love stats"  |
| Factor        | `fct`       | Characters taken only out of a pre specified list | "China" out of Asian |

- <u>Vector</u> - can be made by grouping values to the **same data type** (simplest data <u>structure</u>)

  - `c()` <u>c</u>ombines single elements into a vector
  - Use `is.` Function to check the data type [ `is.numeric()` , `is.character()`]
  - ==Similar to list?==

- R **switches** between data types automatically for some operations

  - Logical -> Numeric -> Character | Logical -> Character

  ```R
  > sum(c(TRUE, FALSE)) == sum(c(1, 0))
  [1] TRUE
  > sum(c(TRUE, FALSE))
  [1] 1
  ```

- <u>Data Frame</u> - stores data sets 
  - Row: individual records; Column: variables
  - A data frame can contain multiple type of data, but **within a column every cell must be the same type of data**
  
- <u>Packages</u> in R provide collections of functions and data sets in addition to the things 'base R' can do

  - <u>Function</u> - a shortcut to run a bunch of code
    - <u>Parameters</u> - a preset setting for the expected input
    - <u>Argument</u> - provided input
  - **tydyverse** - need to be loaded into every problem set using the `library()` function
    - `read_csv()` is a function that load data in, the resulting object type is called a <u>tibble</u>
    - `glimpse()` out the number of rows and colum and listing out the column names, its data type and a few of first values (a summary out the data)
    - `head()` shows the top couple rows of the data (first 6 by default)

- <u>Pipe</u>(`%>%`) - a tool that makes applying functions easy (step-by-step)

  > Ex. The tibble would be piped in as the input the `glimpse()` function

  - Tip1: read pip as "AND THEN" when reading the code
  - Tip2: use CMD + SHIFT + M to make a pipe