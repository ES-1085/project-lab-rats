The Relationship Between World Happiness Report Scores and WHO Country
Suicide Rates - an Analysis
================
Lab rats


## Summary

Our group had great interest in public health. Thus, we engaged in the search for data focusing in public and mental health, finding sources from the World Health Organization (WHO) on global suicide rates from 1985 to 2021as the World Happiness Reports (WHR)  from 2015 to 2019. Since the WHR reports we found were bound to the years 2015-2019, we decided to extract the same years from the WHO world suicide dataset, to analyse if levels of happiness measured by the WHR parameters correlated with lower suicide rates. We were guided by the following question when we wwere formulating this project and our future visualizations: 

How does the score of a certain country on the World Happiness Report correlate with its respective suicide mortality rate?
As we continued our preliminary research, we found that taking a closer look at GDP per capita would also be enlightening for our findings. Initially, we also wanted to find the correlation between happiness, suicide rates, and the amount of light exposure received yearly in a certain country. However, after much research, we could not find any datasets that contained the average of light exposure by country and by year. Therefore, we added solely the question of relationship between GDP per capita and suicide rates as one of our research questions, framed as following: 
How does GDP per capita impact happiness, and to what extent does that data correlate with suicide mortality rates?

#### Cleaning data 

In order to make the visualizations we strived to do, we first had to make sure that both datasets we were working with followed the same standards for the categorization of countries and regions, and also that they represented information gathered in the same time frame. Initial data cleaning was composed of deletion of observations outside or our dataframe, as well as the deletion of columns that we deemed unnecessary for the purposes of this project. After discussion, our group decided that we should only use one metric for suicide rates – the suicide rates numeric – and that the country and region codes would not be necessary for the purpose of our visualizations. However, this latest assessment proved to be a mistake when tying to make a map visualization with package `leaflet`. To use `leaflet`, we had to merge our datasets with a shapefile dataset with international standards for country representation. Since the names of countries differed, the map did not show all of our data. This issue would have been easier to resolve if we had not deleted the columns of country codes for both the WHO suicide dataset and the WHR dataset, since country codes are unique to each country. 
Our process of cleaning and the failures and successes made us learn that sometimes, it is better to have more information than having less of it, because it allows for more room for later ideas. 

#### Visualizations and findings 

We wanted to make scaterplots to visualize the correlation of sucide rates and happiness scores and GDP per capita per country. As we continued making plots, we also wanted to visualize how the WHR parameters (perceptions of corruption, generosity, GDP per capita, social support, freedom and life expectancy)  influenced the overall happiness score of each country. We found that most of the WHR metrics show a positive correlation to the happiness scores, but GDP per capita seems to be the strongest. However, we were surprised to see that suicide rates and hapiness scores also had a positive correlation, showing that many countries that rank highly in the WHR report also have high numbers of sucide rates. The same was observed for GDP per capita and suicide rates – a positive correlation. 
Since the WHO suicide dataset was divided between sex categories and age groups, we also wanted to show some visualizaitons that considered sex categories and suicide rates. We made violin plots and bar plots to explore the gender difference of suicide rates. We found through the graphs that person identified as male do have much higher suicide rates across the globe if compared to persons that identify as female. We also found some outliers that either had too high suicide rates or too low, such as Lesotho and South Sudan. We conducted research to understand better the conditions on each country to try to understand what influenced their suicide rates beyond what was shown by the WHR report. 
Lastly, we wanted to make a cloropleth math showing the happiness scores by color gradient, and overlaying it with a bubble plot, with the size of the bubbles representing the suicide rates of each country. However, as stated in the previous question, we had stripped our datasets of crucial data to be able to succesfully merge it with a shapefile. Since we found that out too late in thee term we did not had enough time to comeback and retrieve some of the data lost to make a map visualization. We want to continue working on the map to see if we are capable to deliver this visualization. 


# Presentation

Our presentation can be found here:

https://docs.google.com/presentation/d/e/2PACX-1vTGLc4g4RlIvc3A5DvOiyx5sbPnOCC0YceVKR-iVQePDTLBCN3fi61DQfpZ4NY0-FS5JVHpIVyZ9spd/pub?start=false&loop=false&delayms=3000


## Data 


Mathurin Ache. (2021). World Happiness Report 2015-2021 [Data set]. Kaggle. https://www.kaggle.com/datasets/mathurinache/world-happiness-report-20152021?select=2015.csv Retrieved February 3, 2023.

Omkar Gowda. (2021). Suicide Rates Overview 1985 to 2021 [Data set]. Kaggle. https://www.kaggle.com/datasets/omkargowda/suicide-rates-overview-1985-to-2021 Retrieved February 3, 2023.


## References


Mathurin Ache. (2021). World Happiness Report 2015-2021 [Data set]. Kaggle. https://www.kaggle.com/datasets/mathurinache/world-happiness-report-20152021?select=2015.csv Retrieved February 3, 2023.

Omkar Gowda. (2021). Suicide Rates Overview 1985 to 2021 [Data set]. Kaggle. https://www.kaggle.com/datasets/omkargowda/suicide-rates-overview-1985-to-2021 Retrieved February 3, 2023.

World Bank. (2018). World development indicators: GDP (current US$) by country:1985 to 2016. Retrieved from http://databank.worldbank.org/data/source/world-development-indicators#

World Health Organization. (2018). Suicide prevention. Retrieved from http://www.who.int/mental_health/suicide-prevention/en/

Helliwell, John F., Richard Layard, Jeffrey Sachs, and Jan-Emmanuel De Neve, eds. 2020. World Happiness Report 2020. New York: Sustainable Development Solutions Network

Berghaus, R. (2008, October 6). Confronting Lesotho’s Health-Care Crisis. BU Today. https://www.bu.edu/articles/2009/confronting-lesotho%E2%80%99s-health-care-crisis/