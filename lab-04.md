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

``` r
dennys %>%
  mutate(country = "United States")
```

    ## # A tibble: 1,643 × 7
    ##    address                        city    state zip   longitude latitude country
    ##    <chr>                          <chr>   <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 2900 Denali                    Anchor… AK    99503    -150.      61.2 United…
    ##  2 3850 Debarr Road               Anchor… AK    99508    -150.      61.2 United…
    ##  3 1929 Airport Way               Fairba… AK    99701    -148.      64.8 United…
    ##  4 230 Connector Dr               Auburn  AL    36849     -85.5     32.6 United…
    ##  5 224 Daniel Payne Drive N       Birmin… AL    35207     -86.8     33.6 United…
    ##  6 900 16th St S, Commons on Gree Birmin… AL    35294     -86.8     33.5 United…
    ##  7 5931 Alabama Highway, #157     Cullman AL    35056     -86.9     34.2 United…
    ##  8 2190 Ross Clark Circle         Dothan  AL    36301     -85.4     31.2 United…
    ##  9 900 Tyson Rd                   Hope H… AL    36043     -86.4     32.2 United…
    ## 10 4874 University Drive          Huntsv… AL    35816     -86.7     34.7 United…
    ## # ℹ 1,633 more rows

``` r
dennys <- dennys %>% 
  mutate(country = "United States")
```

### Exercise 7

Based on the website, there are La Quinta locations in Canada: British
Columbia (Kelowna and Richmond), and Ontario (Oshawa). In Mexico:
Aguascalientes, Ciudad Juarez, Poza Rica, Puebla, Reynosa, and San Jose
Chiapa. In China: Chengdu, Qionghai, Suzhou, Taiyuan, Turpan, Weifang,
and Zunyi. In New Zealand: Auckland and Queenstown. In Georgia: Batumi.
In Turkiye: Bodrum, Cesme, Giresun, and Istanbul. In United Arab
Emirates: Abu Dhabi and Dubai. In Colombia: Medellin. In Ecuador: Quito.

### Exercise 8

``` r
laquinta <- laquinta %>%
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT" ~ "Colombia",
    state == "FM" ~ "Honduras",
    state %in% c("AG", "CH", "PU", "SL", "QR", "NL", "VE") ~ "Mexico"
  ))
```

``` r
laquinta <- laquinta %>% 
  filter(country == "United States")
```

### Exercise 9

``` r
dennys %>% 
  count(state, name = "n") %>% 
  arrange(n)
```

    ## # A tibble: 51 × 2
    ##    state     n
    ##    <chr> <int>
    ##  1 DE        1
    ##  2 DC        2
    ##  3 VT        2
    ##  4 AK        3
    ##  5 IA        3
    ##  6 NH        3
    ##  7 SD        3
    ##  8 WV        3
    ##  9 LA        4
    ## 10 MT        4
    ## # ℹ 41 more rows

Delaware has the fewest Denny’s locations and California, Texas, and
Florida has the most.

``` r
laquinta %>% 
  count(state, name = "n") %>% 
  arrange(n)
```

    ## # A tibble: 48 × 2
    ##    state     n
    ##    <chr> <int>
    ##  1 ME        1
    ##  2 AK        2
    ##  3 NH        2
    ##  4 RI        2
    ##  5 SD        2
    ##  6 VT        2
    ##  7 WV        3
    ##  8 WY        3
    ##  9 IA        4
    ## 10 MI        4
    ## # ℹ 38 more rows

Maine has the fewest La Quinta locations and California, Texas, and
Florida has the most.

It is not surprising to me that the most populous states have the most
locations and the lesser populous states have the least.

``` r
dennys %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

    ## # A tibble: 51 × 4
    ##    state     n name                     area
    ##    <chr> <int> <chr>                   <dbl>
    ##  1 AK        3 Alaska               665384. 
    ##  2 AL        7 Alabama               52420. 
    ##  3 AR        9 Arkansas              53179. 
    ##  4 AZ       83 Arizona              113990. 
    ##  5 CA      403 California           163695. 
    ##  6 CO       29 Colorado             104094. 
    ##  7 CT       12 Connecticut            5543. 
    ##  8 DC        2 District of Columbia     68.3
    ##  9 DE        1 Delaware               2489. 
    ## 10 FL      140 Florida               65758. 
    ## # ℹ 41 more rows
