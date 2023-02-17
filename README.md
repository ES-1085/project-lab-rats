The Relationship Between World Happiness Report Scores and WHO Country
Suicide Rates - an Analysis
================
Lab rats

``` r
#install.packages("tidyverse")
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.4.0     ✔ purrr   1.0.1
    ## ✔ tibble  3.1.8     ✔ dplyr   1.1.0
    ## ✔ tidyr   1.3.0     ✔ stringr 1.5.0
    ## ✔ readr   2.1.3     ✔ forcats 1.0.0
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

## Summary

Write-up of your project and findings go here. Think of this as the text
of your presentation. The length should be roughly 5 minutes when read
out loud. Although pacing varies, a 5-minute speech is roughly 750
words. To use the word count addin, select the text you want to count
the words of (probably this is the Summary section of this document, go
to Addins, and select the `Word count` addin). This addin counts words
using two different algorithms, but the results should be similar and as
long as you’re in the ballpark of 750 words, you’re good! The addin will
ignore code chunks and only count the words in prose.

You can also load your data here and present any analysis results /
plots, but I strongly urge you to keep that to a minimum (maybe only the
most important graphic, if you have one you can choose). And make sure
to hide your code with `echo = FALSE` unless the point you are trying to
make is about the code itself. Your results with proper output and
graphics go in your presentation, this space is for a brief summary of
your project.

    ## Rows: 158 Columns: 12
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (2): Country, Region
    ## dbl (10): Happiness Rank, Happiness Score, Standard Error, Economy (GDP per ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 157 Columns: 13
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (2): Country, Region
    ## dbl (11): Happiness Rank, Happiness Score, Lower Confidence Interval, Upper ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 155 Columns: 12
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (1): Country
    ## dbl (11): Happiness.Rank, Happiness.Score, Whisker.high, Whisker.low, Econom...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 156 Columns: 9
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Country or region, Perceptions of corruption
    ## dbl (7): Overall rank, Score, GDP per capita, Social support, Healthy life e...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 156 Columns: 9
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Country or region
    ## dbl (8): Overall rank, Score, GDP per capita, Social support, Healthy life e...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 17019 Columns: 12
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (7): WHO Region Code, WHO Region, Country Code, Country, Sex, Age Group,...
    ## dbl (4): Year, Crude suicide rates (per 100 000 population) (numeric), Crude...
    ## lgl (1): IsLatestYear
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

### Tidying data

``` r
whr_2015 %>%
  mutate(Year = 2015)
```

    ## # A tibble: 158 × 13
    ##    Country Region Happi…¹ Happi…² Stand…³ Econo…⁴ Family Healt…⁵ Freedom Trust…⁶
    ##    <chr>   <chr>    <dbl>   <dbl>   <dbl>   <dbl>  <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 Switze… Weste…       1    7.59  0.0341    1.40   1.35   0.941   0.666   0.420
    ##  2 Iceland Weste…       2    7.56  0.0488    1.30   1.40   0.948   0.629   0.141
    ##  3 Denmark Weste…       3    7.53  0.0333    1.33   1.36   0.875   0.649   0.484
    ##  4 Norway  Weste…       4    7.52  0.0388    1.46   1.33   0.885   0.670   0.365
    ##  5 Canada  North…       5    7.43  0.0355    1.33   1.32   0.906   0.633   0.330
    ##  6 Finland Weste…       6    7.41  0.0314    1.29   1.32   0.889   0.642   0.414
    ##  7 Nether… Weste…       7    7.38  0.0280    1.33   1.28   0.893   0.616   0.318
    ##  8 Sweden  Weste…       8    7.36  0.0316    1.33   1.29   0.911   0.660   0.438
    ##  9 New Ze… Austr…       9    7.29  0.0337    1.25   1.32   0.908   0.639   0.429
    ## 10 Austra… Austr…      10    7.28  0.0408    1.33   1.31   0.932   0.651   0.356
    ## # … with 148 more rows, 3 more variables: Generosity <dbl>,
    ## #   `Dystopia Residual` <dbl>, Year <dbl>, and abbreviated variable names
    ## #   ¹​`Happiness Rank`, ²​`Happiness Score`, ³​`Standard Error`,
    ## #   ⁴​`Economy (GDP per Capita)`, ⁵​`Health (Life Expectancy)`,
    ## #   ⁶​`Trust (Government Corruption)`

``` r
whr_2016 %>%
  mutate(Year = 2016)
```

    ## # A tibble: 157 × 14
    ##    Country Region Happi…¹ Happi…² Lower…³ Upper…⁴ Econo…⁵ Family Healt…⁶ Freedom
    ##    <chr>   <chr>    <dbl>   <dbl>   <dbl>   <dbl>   <dbl>  <dbl>   <dbl>   <dbl>
    ##  1 Denmark Weste…       1    7.53    7.46    7.59    1.44   1.16   0.795   0.579
    ##  2 Switze… Weste…       2    7.51    7.43    7.59    1.53   1.15   0.863   0.586
    ##  3 Iceland Weste…       3    7.50    7.33    7.67    1.43   1.18   0.867   0.566
    ##  4 Norway  Weste…       4    7.50    7.42    7.58    1.58   1.13   0.796   0.596
    ##  5 Finland Weste…       5    7.41    7.35    7.48    1.41   1.13   0.811   0.571
    ##  6 Canada  North…       6    7.40    7.34    7.47    1.44   1.10   0.828   0.574
    ##  7 Nether… Weste…       7    7.34    7.28    7.39    1.46   1.03   0.812   0.552
    ##  8 New Ze… Austr…       8    7.33    7.26    7.40    1.36   1.17   0.831   0.581
    ##  9 Austra… Austr…       9    7.31    7.24    7.38    1.44   1.10   0.851   0.568
    ## 10 Sweden  Weste…      10    7.29    7.23    7.36    1.45   1.09   0.831   0.582
    ## # … with 147 more rows, 4 more variables:
    ## #   `Trust (Government Corruption)` <dbl>, Generosity <dbl>,
    ## #   `Dystopia Residual` <dbl>, Year <dbl>, and abbreviated variable names
    ## #   ¹​`Happiness Rank`, ²​`Happiness Score`, ³​`Lower Confidence Interval`,
    ## #   ⁴​`Upper Confidence Interval`, ⁵​`Economy (GDP per Capita)`,
    ## #   ⁶​`Health (Life Expectancy)`

``` r
whr_2017 %>%
  mutate(Year = 2017)
```

    ## # A tibble: 155 × 13
    ##    Country     Happines…¹ Happi…² Whisk…³ Whisk…⁴ Econo…⁵ Family Healt…⁶ Freedom
    ##    <chr>            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>  <dbl>   <dbl>   <dbl>
    ##  1 Norway               1    7.54    7.59    7.48    1.62   1.53   0.797   0.635
    ##  2 Denmark              2    7.52    7.58    7.46    1.48   1.55   0.793   0.626
    ##  3 Iceland              3    7.50    7.62    7.39    1.48   1.61   0.834   0.627
    ##  4 Switzerland          4    7.49    7.56    7.43    1.56   1.52   0.858   0.620
    ##  5 Finland              5    7.47    7.53    7.41    1.44   1.54   0.809   0.618
    ##  6 Netherlands          6    7.38    7.43    7.33    1.50   1.43   0.811   0.585
    ##  7 Canada               7    7.32    7.38    7.25    1.48   1.48   0.835   0.611
    ##  8 New Zealand          8    7.31    7.38    7.25    1.41   1.55   0.817   0.614
    ##  9 Sweden               9    7.28    7.34    7.22    1.49   1.48   0.831   0.613
    ## 10 Australia           10    7.28    7.36    7.21    1.48   1.51   0.844   0.602
    ## # … with 145 more rows, 4 more variables: Generosity <dbl>,
    ## #   Trust..Government.Corruption. <dbl>, Dystopia.Residual <dbl>, Year <dbl>,
    ## #   and abbreviated variable names ¹​Happiness.Rank, ²​Happiness.Score,
    ## #   ³​Whisker.high, ⁴​Whisker.low, ⁵​Economy..GDP.per.Capita.,
    ## #   ⁶​Health..Life.Expectancy.

``` r
whr_2018 <- whr_2018 %>% 
  mutate (Year = 2018)
```

``` r
whr_2019 <- whr_2019 %>% 
  mutate (Year = 2019)
```

## Presentation

``` r
suicide <- suicide %>%
  mutate(Country = case_when(Country %in% "Syrian Arab Republic" ~ "Syria",
                             TRUE ~ Country))

whr_2015 <- whr_2015 %>%
  rename("Social support" = "Family")
```

## Data

Include a citation for your data here. See
<http://libraryguides.vu.edu.au/c.php?g=386501&p=4347840> for guidance
on proper citation for datasets. If you got your data off the web, make
sure to note the retrieval date.

## References

List any references here. You should, at a minimum, list your data
source.
