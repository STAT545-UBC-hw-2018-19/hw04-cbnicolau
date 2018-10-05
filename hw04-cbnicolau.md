Homework\_04
================
Coni
October 4, 2018

Homework 04: Tidy data and joins
================================

In this assignment we use `tidyr` and `dplyr`

``` r
library(tidyr)
library(dplyr)
```

Data Reshaping Prompts (and relationship to aggregation)
--------------------------------------------------------

*Problem:* You have data in one “shape” but you wish it were in another. Usually this is because the alternative shape is superior for presenting a table, making a figure, or doing aggregation and statistical analysis.

*Solution:* Reshape your data. For simple reshaping, `gather()` and `spread()` from `tidyr` will suffice. Do the thing that is possible / easier now that your data has a new shape.

Before getting into the assignment activity, let's remember what `gather()` and `spread()` do

-   `gather()` is used for making untidy data tidy

*Format:* gather(`data`, `key = "key_name"`, `value = "value"`, `...`) where:

*"key\_name"* is what we want to call the column headers that became a variable,

*"value"* is what we want to call the stacked columns that became a variable

and the last argument *...* correspond to the items we want to include or not include in the new table
