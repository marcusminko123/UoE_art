Lab 07 - University of Edinburgh Art Collection
================
Marcus Minko
02-26-2022

### Load packages and data

``` r
library(tidyverse) 
library(skimr)
```

``` r
# Remove eval = FALSE or set it to TRUE once data is ready to be loaded
uoe_art <- read_csv("data/uoe-art.csv")
```

### Exercise 9

``` r
uoe_art <- uoe_art %>%
  separate(title, into = c("title", "date"), sep = "\\(") %>%
  mutate(year = str_remove(date, "\\)") %>% as.numeric()) %>%
  select(title, artist, year, link)
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 39 rows [149, 194,
    ## 366, 390, 524, 701, 793, 836, 853, 866, 1000, 1063, 1079, 1141, 1321, 1377,
    ## 1382, 1388, 1456, 1642, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 620 rows [17, 23,
    ## 24, 25, 33, 36, 38, 48, 49, 56, 67, 70, 72, 76, 78, 87, 93, 101, 114, 119, ...].

    ## Warning in str_remove(date, "\\)") %>% as.numeric(): NAs introduced by coercion

### Exercise 10

``` r
skim(uoe_art)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | uoe_art |
| Number of rows                                   | 2910    |
| Number of columns                                | 4       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 3       |
| numeric                                          | 1       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| title         |         1 |          1.00 |   0 |  86 |     8 |     1343 |          0 |
| artist        |       112 |          0.96 |   2 |  55 |     0 |     1100 |          0 |
| link          |         0 |          1.00 |  49 |  52 |     0 |     2910 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate |    mean |  sd |  p0 |  p25 |  p50 |  p75 | p100 | hist  |
|:--------------|----------:|--------------:|--------:|----:|----:|-----:|-----:|-----:|-----:|:------|
| year          |      1369 |          0.53 | 1964.56 |  56 |   2 | 1953 | 1962 | 1980 | 2020 | ▁▁▁▁▇ |

``` r
#1,369 have the year missing

uoe_art %>%
  na.omit() %>% 
  ggplot(aes(x = year)) + geom_histogram(binwidth = 5) + xlim(1818, 2020)
```

    ## Warning: Removed 1 rows containing non-finite values (stat_bin).

    ## Warning: Removed 2 rows containing missing values (geom_bar).

![](lab-07_files/figure-gfm/skim-1.png)<!-- -->

### Exercise 11

…

Add exercise headings as needed.
