The Relationship Between World Happiness Report and WHO Country Suicide
Rates - an Analysis
================
Lab rats

``` r
library(tidyverse)
library(broom)
```

``` r
 # write_csv(whr, "whr.csv")
 whr <- read_csv("whr.csv")
```

    ## Rows: 850 Columns: 10
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): country, perceptions_of_corruption
    ## dbl (8): overall_rank, happiness_score, gdp_per_capita, social_support, life...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# write_csv(suicide, "suicide.csv")
suicide <- read_csv ("suicide.csv")
```

    ## Rows: 17019 Columns: 12
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (7): WHO Region Code, WHO Region, Country Code, Country, Sex, Age Group,...
    ## dbl (4): Year, Crude suicide rates (per 100 000 population) (numeric), Crude...
    ## lgl (1): IsLatestYear
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# write_csv(suicide_2, "suicide_2.csv")
suicide_2 <- read_csv("suicide_2.csv")
```

    ## Rows: 32940 Columns: 5
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (3): country, sex, age_group
    ## dbl (2): year, suicide_rates
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# write_csv(whr_2, "whr_2.csv")
whr_2 <- read_csv ("whr_2.csv")
```

    ## Rows: 840 Columns: 10
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): country, perceptions_of_corruption
    ## dbl (8): overall_rank, happiness_score, gdp_per_capita, social_support, life...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## 1. Introduction

Our group had a common interest in public health and thought the topic
would have ample opportunity for data analysis. We were able to find
large data sets on suicide mortality rates from around the world, but
wanted to know what factors contributed to higher or lower suicide rates
in various countries. We decided that comparing suicide rates to World
Happiness Report (WHR) scores would allow us to see how the data
narrates mental health for each country, and what specific variables
show large contribution. WHR includes many independent variables, such
as GDP per capita, family size, trust in government, generosity, etc. We
agreed that GDP per capita would allow us to see exactly how economy
affects peoples’ happiness, and therefore increase or decrease rates of
happiness.

Primary research question: How does the ranking of a certain country on
the World Happiness Report correlate with their respective suicide
mortality rate? Secondary research question: How does GDP per capita
impact happiness, and to what extent does that data correlate with
suicide mortality rates?

## 2. Data

We chose two main datasets for our project. The first one was a
compilation of suicide rates from the majority of countries created by
the World Health Organization (WHO) for the period 2000 to 2019 (source:
<https://www.kaggle.com/datasets/mikekzan/who-crude-suicide-mortality-rate>).
The second one was a collection of scores of the WHR from 2015 to 2019,
with data for each year located in a separate subdataset (source:
<https://www.kaggle.com/datasets/unsdsn/world-happiness>).

However, we plan to modify these datasets to a significant degree to fit
our needs. For example, we first intend to merge the separate
subdatasets of the WHR in one large dataset (with an additional column
“year”). In addition, we want to harmonise the names of countries all
datasets (e.g., the WHO dataset has the “Syrian Arab Republic”, whereas
the WHR dataset has “Syria”). Afterwards, we will filter out countries
that do not appear in all datasets. Lastly, we will assign consistent
regions for all countries, which will not be an easy endeavour,
recognising the inherent limitations of categorising countries with
their unique characteristics.

Our first graph will be a scatterplot showing the correlation between
the WHR scores and suicide mortality rates of all countries. Then we
plan to create such a graph for each region. Afterwards, we want to plot
the correlation between GDP per capita (a variable in the WHR datasets)
and the happiness score on a global and regional scale. Lastly, we want
to create graphs showing the correlation of the two aforementioned
variables with suicide mortality rates. However, it is of utmost
importance to state that our plans are subject to change as the project
evolves.

``` r
# whr_2015 <- read_csv("data_copy/whr_2015.csv")
# whr_2016 <- read_csv("data_copy/whr_2016.csv")
# whr_2017 <- read_csv("data_copy/whr_2017.csv")
# whr_2018 <- read_csv("data_copy/whr_2018.csv")
# whr_2019 <- read_csv("data_copy/whr_2019.csv")
# whr <- rbind(whr_2015, whr_2016, whr_2017, whr_2018, whr_2019)
whr %>%
  glimpse() 
```

    ## Rows: 850
    ## Columns: 10
    ## $ overall_rank              <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 1…
    ## $ country                   <chr> "Switzerland", "Iceland", "Denmark", "Norway…
    ## $ happiness_score           <dbl> 7.587, 7.561, 7.527, 7.522, 7.427, 7.406, 7.…
    ## $ gdp_per_capita            <dbl> 1.39651, 1.30232, 1.32548, 1.45900, 1.32629,…
    ## $ social_support            <dbl> 1.34951, 1.40223, 1.36058, 1.33095, 1.32261,…
    ## $ life_expectancy           <dbl> 0.94143, 0.94784, 0.87464, 0.88521, 0.90563,…
    ## $ freedom                   <dbl> 0.66557, 0.62877, 0.64938, 0.66973, 0.63297,…
    ## $ generosity                <dbl> 0.29678, 0.43630, 0.34139, 0.34699, 0.45811,…
    ## $ perceptions_of_corruption <chr> "0.41978", "0.14145", "0.48357", "0.36503", …
    ## $ year                      <dbl> 2015, 2015, 2015, 2015, 2015, 2015, 2015, 20…

## 3. Data analysis plan

Variables we will consider for our analysis:

``` r
names(whr)
```

    ##  [1] "overall_rank"              "country"                  
    ##  [3] "happiness_score"           "gdp_per_capita"           
    ##  [5] "social_support"            "life_expectancy"          
    ##  [7] "freedom"                   "generosity"               
    ##  [9] "perceptions_of_corruption" "year"

World Happiness Report dataset, for the years between 2015-2019: \$
`Country`  
\$ `Region`  
\$ `Happiness Rank`  
\$ `Happiness Score`  
\$ `Economy (GDP per Capita)`  
\$ `Social Support`  
\$ `Health (Life Expectancy)`  
\$ `Freedom`  
\$ `Trust (Government Corruption)` \$ `Generosity`

World Suicide rates dataset, for the years between 2015-2019:

# Initially, we would also like to make an analysis associating light exposure to the happiness index and suicide rates. However, in our preliminary research so far we could not find a dataset with this information by country. We will continue the research to see if it is possible to add this variable from another dataset.

\$`WHO Region Code`  
\$ `WHO Region`  
\$ `Country Code`  
\$ `Country`  
\$ `Year`  
\$ `IsLatestYear`  
\$ `Sex`  
\$ `Age Group`  
\$ `Crude suicide rates (per 100 000 population) (numeric)`  
\$ `Crude suicide rates (per 100 000 population) (low estimation)` \$
`Crude suicide rates (per 100 000 population) (high estimation)` \$
`Crude suicide rates (per 100 000 population) (string)`

Initially, we would also like to make an analysis associanting light
exposure to the happiness index and suicide rates. However, in our
preliminary research so far we could not find a dataset with this
information byt country. We will continue the research to see if it is
possible to add this variable from another dataset.

Since our dataset has a large set of observations, considering 155-158
countries out of the total countries in the world, we envision several
possibilities to run our analysis. We could: \* consider all of the
countries in the dataset, grouping them by their regions \* select a
specific number of regions to analyze \* equalize the population numbers
for each region, trying to sample an equal amount of people per
region/continent to be analyzed. Doing so, we would have to randomly
exclude some countries of the analysis. \* choose specific countries to
compare and contrast, dimishing considerably the number of observations.
\>\>\>\>\>\>\> 7a61a61afe8d6263d8900c921a4fafad95e325cf
