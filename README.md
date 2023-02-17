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
whr_2015 <- whr_2015 %>%
  mutate(Year = 2015) %>% 
  subset(select = -c(`Standard Error`, `Dystopia Residual`))
```

``` r
whr_2016 <- whr_2016 %>%
  mutate(Year = 2016)
```

``` r
whr_2017 <- whr_2017 %>%
  mutate(Year = 2017)
```

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
