p8105_HW1_nck2132
================
Nina Knitowski
09-25-2026

\#Question 0: Load Library

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

\#Question 1 Load Dataset

``` r
data("penguins", package = "palmerpenguins")
```

\#1.1 Names of Dataset/Values of Important Variables

``` r
names(penguins)
```

    ## [1] "species"           "island"            "bill_length_mm"   
    ## [4] "bill_depth_mm"     "flipper_length_mm" "body_mass_g"      
    ## [7] "sex"               "year"

``` r
janitor::clean_names(penguins)
```

    ## # A tibble: 344 × 8
    ##    species island    bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
    ##    <fct>   <fct>              <dbl>         <dbl>             <int>       <int>
    ##  1 Adelie  Torgersen           39.1          18.7               181        3750
    ##  2 Adelie  Torgersen           39.5          17.4               186        3800
    ##  3 Adelie  Torgersen           40.3          18                 195        3250
    ##  4 Adelie  Torgersen           NA            NA                  NA          NA
    ##  5 Adelie  Torgersen           36.7          19.3               193        3450
    ##  6 Adelie  Torgersen           39.3          20.6               190        3650
    ##  7 Adelie  Torgersen           38.9          17.8               181        3625
    ##  8 Adelie  Torgersen           39.2          19.6               195        4675
    ##  9 Adelie  Torgersen           34.1          18.1               193        3475
    ## 10 Adelie  Torgersen           42            20.2               190        4250
    ## # ℹ 334 more rows
    ## # ℹ 2 more variables: sex <fct>, year <int>

\#columns and rows of dataset

``` r
nrow(penguins)
```

    ## [1] 344

``` r
ncol(penguins)
```

    ## [1] 8

\#The mean flipper length included in the skim function AND important
values in the dataset

``` r
skimr::skim(penguins)
```

|                                                  |          |
|:-------------------------------------------------|:---------|
| Name                                             | penguins |
| Number of rows                                   | 344      |
| Number of columns                                | 8        |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |          |
| Column type frequency:                           |          |
| factor                                           | 3        |
| numeric                                          | 5        |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |          |
| Group variables                                  | None     |

Data summary

**Variable type: factor**

| skim_variable | n_missing | complete_rate | ordered | n_unique | top_counts |
|:---|---:|---:|:---|---:|:---|
| species | 0 | 1.00 | FALSE | 3 | Ade: 152, Gen: 124, Chi: 68 |
| island | 0 | 1.00 | FALSE | 3 | Bis: 168, Dre: 124, Tor: 52 |
| sex | 11 | 0.97 | FALSE | 2 | mal: 168, fem: 165 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate | mean | sd | p0 | p25 | p50 | p75 | p100 | hist |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|:---|
| bill_length_mm | 2 | 0.99 | 43.92 | 5.46 | 32.1 | 39.23 | 44.45 | 48.5 | 59.6 | ▃▇▇▆▁ |
| bill_depth_mm | 2 | 0.99 | 17.15 | 1.97 | 13.1 | 15.60 | 17.30 | 18.7 | 21.5 | ▅▅▇▇▂ |
| flipper_length_mm | 2 | 0.99 | 200.92 | 14.06 | 172.0 | 190.00 | 197.00 | 213.0 | 231.0 | ▂▇▃▅▂ |
| body_mass_g | 2 | 0.99 | 4201.75 | 801.95 | 2700.0 | 3550.00 | 4050.00 | 4750.0 | 6300.0 | ▃▇▆▃▂ |
| year | 0 | 1.00 | 2008.03 | 0.82 | 2007.0 | 2007.00 | 2008.00 | 2009.0 | 2009.0 | ▇▁▇▁▇ |

The data set names are species, island, bill_length_mm, bill_depth_mm,
flipper_length_mm, body_mass_g, sex, year. Species, island, and sex are
categorical variables and bill length, bill depth, flipper length, body
mass, and year continuous variables. There are 344 rows in the dataset
and 8 columns. There are 344 observations and 8 variables. Here are some
important values of the continuous variables of the table. The mean
flipper length is 200.9152047 with a standard deviation of 14.0617137.
The mean bill depth is 17.1511696 with a standard deviation of
1.9747932. The mean body mass is 4201.754386 with a standard deviation
of 801.9545357. The mean year is 2008.0290698 and with a standard
deviation of 0.8183559. The mean bill length is 43.9219298 with a
standard deviation of 5.4595837. The skimr package shows me the missing
values in the dataset and does not include NA when preforming
calculations of the mean and standard deviation, but for the inline code
when I compute mean and SD separately I must purposefully exclude these
values.

\#Scatterplot of flipper_length_mm (y) vs bill_length_mm

``` r
ggplot(penguins, aes(x=bill_length_mm, y=flipper_length_mm, color=species))+geom_point()
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](template--2-_files/figure-gfm/scatterplot%20flipper%20legnth%20vs.%20bill-1.png)<!-- -->

``` r
ggsave("scatter_plot.pdf")
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

\#Question 2 \#2.1 Create Data Frame

``` r
HWProb2_df = tibble(
  norm_samp = rnorm(10),
  norm_samp_pos = (norm_samp > 0),
  vec_char = c("My", "name", "is", "Nina", "Knitowski","and", "I", "currently","live", "in NYC"),
  vec_factor = factor(c("a", "b", "c", "c", "b", "a", "a", "b", "c", "a"))
)
```

\#2.2 Try Means Using Pull

``` r
mean(pull(HWProb2_df, norm_samp))
```

    ## [1] -0.04059459

``` r
mean(pull(HWProb2_df, norm_samp_pos))
```

    ## [1] 0.6

``` r
mean(pull(HWProb2_df, vec_char))
```

    ## [1] NA

``` r
mean(pull(HWProb2_df, vec_factor))
```

    ## [1] NA

# I was able to calculate the mean of numeric vector (norm_samp), the logical vector (norm_samp_pos), but not able to calculate the mean of the character factor (vec_char) and factor vector (vec_fac).

\#2.3 Convert logical, character, and factor variables to numeric

``` r
as.numeric(pull(HWProb2_df, norm_samp_pos))
as.numeric(pull(HWProb2_df, vec_char))
```

    ## Warning: NAs introduced by coercion

``` r
as.numeric(pull(HWProb2_df, vec_factor))
```

# Logical and factor variables can be converted into numeric values, but character variables cannot. R tells us “\## Warning: NAs introduced by coercion” when we try to convert a character variable into a numeric one because it is not able to convert letters and words into numbers.This helps explain why we could only take the mean of logical and numeric variables because these variables have number values. The factor vector is a categorical variable but can be converted to a numeric values for each category (1,2,3) R does not take the mean because they are numerical values used to represent the categories are not quantitative measurements. The character vector cannot be converted because it is just a set of words there is no way to turn text into a numeric value and therefore you cannot take the mean without numbers. Essentially, R does not want to take the average of character variables and categorical variables because it does not make sense.
