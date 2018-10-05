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

1.  `gather()` is used for making untidy data tidy

*Format:* `gather`(`data`, `key = "key_name"`, `value = "value"`, `...`) where:

-   `"key_name"` is what we want to call the column headers that became a variable,

-   `"value"` is what we want to call the stacked columns that became a variable

-   and the last argument `...` correspond to the items we want to include or not include in the new table

Let's first have a look at the iris data frame

``` r
colnames(iris)
```

    ## [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width" 
    ## [5] "Species"

And then take a subset of this table by slicing the first appearance of each species

``` r
(mini_iris <-
  iris %>%
  group_by(Species) %>%
  slice(1))
```

    ## # A tibble: 3 x 5
    ## # Groups:   Species [3]
    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species   
    ##          <dbl>       <dbl>        <dbl>       <dbl> <fct>     
    ## 1          5.1         3.5          1.4         0.2 setosa    
    ## 2          7           3.2          4.7         1.4 versicolor
    ## 3          6.3         3.3          6           2.5 virginica

Now we can make this untidy data tidy with gather()

``` r
mini_iris %>% 
  gather(key = flower_att, #creates a new column named flower_att that contains the measurement type
         value = measurement, #contains the value of the measurement type for each species
         -Species) #we include the species name in the new table
```

    ## # A tibble: 12 x 3
    ## # Groups:   Species [3]
    ##    Species    flower_att   measurement
    ##    <fct>      <chr>              <dbl>
    ##  1 setosa     Sepal.Length         5.1
    ##  2 versicolor Sepal.Length         7  
    ##  3 virginica  Sepal.Length         6.3
    ##  4 setosa     Sepal.Width          3.5
    ##  5 versicolor Sepal.Width          3.2
    ##  6 virginica  Sepal.Width          3.3
    ##  7 setosa     Petal.Length         1.4
    ##  8 versicolor Petal.Length         4.7
    ##  9 virginica  Petal.Length         6  
    ## 10 setosa     Petal.Width          0.2
    ## 11 versicolor Petal.Width          1.4
    ## 12 virginica  Petal.Width          2.5
