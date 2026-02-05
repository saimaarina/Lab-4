Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Saima Arina
02/04/2026

### Load packages and data

``` r
library(tidyverse) 
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

``` r
nrow(dennys)
```

    ## [1] 1643

``` r
ncol(dennys)
```

    ## [1] 6

``` r
dim(dennys)
```

    ## [1] 1643    6

The Denny’s dataset has 1,643 rows and 6 columns. Each row represents a
Denny’s location. The variables are: address, city, state, zip,
longitude, and latitude.

### Exercise 2

``` r
nrow(laquinta)
```

    ## [1] 909

``` r
ncol(laquinta)
```

    ## [1] 6

``` r
dim(laquinta)
```

    ## [1] 909   6

The La Quinta dataset has 909 rows and 6 columns. Each row represents a
La Quinta location. The variables are: address, city, state, zip,
longitude, and latitude.

### Exercise 3

There are La Quinta locations in Canada, Mexico, China, New Zealand,
Georgia (the country), Turkiye, the United Arab Emirates, Colombia, and
Ecuador. There are no Denny’s locations outside of the United States.

### Exercise 4

To find a location outside the US using just the data, you could filter
for any location that either has no state or an abbreviated state that
does not match any of the states of the USA.

### Exercise 5

``` r
dennys %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 × 6
    ## # ℹ 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

There are no Denny’s locations outside of the US.

### Exercise 6

…

Add exercise headings as needed.
