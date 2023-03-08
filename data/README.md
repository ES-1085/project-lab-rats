# Data

For our visualizations, we are using information from the World Happiness Report and the WHO suicide rates from 2015 to 2019. 

## suicide and suicide_2

Dataset `suicide` contains 5 variables and 8784 observations. This is the matrix dataset with information as reported by the WHO. 

Dataset `suicide_2` contains 5 variables and 32940 observations. We used the `expand()` function to have all possible combinations generated. This enables us to view the missing reported values of the dataset.  

Both datasets have the following set of variables: 

- `country`: the nation state where the data was collected 
- `year`: the year the data was collected 
- `sex`: the sex of individuals on reported data 
- `age_group`: classed category of people of similar age.
- `suicide_rates` : numerical value of suicide rates in the respective country. 



## whr and whr_2

Dataset `whr`contains 10 variables and 782 observations. This is the matrix dataset with information as reported in the World Happiness Report.

Dataset `whr_2` contains 10 variables and 777 observations.We used the `expand()` function to have all possible combinations generated. This enables us to view the missing reported values of the dataset.  

- `overall_rank`: World Happiness Report rank    
- `country`: the nation state where the data was collected         
- `happiness_score`: Happiness score in scale from 0 to 10     
- `gdp_per_capita`: income calculated by overall GDP divided per total population                         
- `social_support`: having someone to count on in times of trouble
- `life_expectancy`: Healthy life expectancy                      
- `freedom`: Freedom to make life choices     
- `generosity`: overall attitudes to help one another           
- `perceptions_of_corruption`: trust in the absence of corruption in business and government                                     
- `year`: the year the data was collected


 ...


