# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Capstone Project: Understanding and Predicting Crime in San Francisco

by: Elton Yeo, DSI13

### Context and Problem Statement

Police departments have limited policy and frontline resources, and need to prioritise areas to focus their efforts to reduce crime, through greater prevention and/or deterrence. 

This project will analyse crime data for San Francisco city to: 
1. Develop insights into the areas with the most crimes, and consider policy and operational measures which might help to bring down crime in those areas based on those insights
2. Predict the number of preventable crime given a specific zipcode, day of the week, and hour, which will help the police plan their patrol schedules and resources (Police patrols are important because they project presence, which can deter criminals and increase the sense of safety for residents) 

For the prediction, the data will be run through 5 regression models: linear regression, lassoCV,  ridgeCV, random forest with gridsearchCV, and XGBoost with gridsearchCV. 

The models will be trained on 2018 data, and tested on 2019 data, and evaluated by their r-squared and mean squared error (MSE) scores. 

Success for the final model is defined as:
- a MSE score higher than the baseline, which means that predictions had a closer fit to the data than the baseline, and 
- a r-squared score of 0.8 and above, which means that the model explains 80% or more of the variability of the target data that is predictable from the independent variables. 

### Data Analysis, Cleaning and Feature Engineering

We researched to understand the different variables in the dataset. We dropped unnecessary or repeated variables and imputed null values for the remaining variables. We engineered the features where necessary e.g. removing or combining selected rows or categories to allow for more meaningful analysis and modeling. 

We performed exploratory data analysis to understand the spread of crime across the various variables. We further collapsed crime categories to create five final categories: 
- Preventable crime
- Violent crime
- Non-violent crime
- White-collar crime
- Drug crime

We read in data which allowed us to convert the latitude and longitude of each crime incident to zipcodes and corresponding population numbers. This allowed us to create the number of each category of crime per capita for each zipcode. 

We produced heatmaps to show us the spread of crime per capita for each zipcode throughout San Francisco city. 

### Modelling

We used 5 regression models: linear regression, lassoCV,  ridgeCV, random forest with gridsearchCV, and XGBoost with gridsearchCV. Among our 5 models, XGBoost had the lowest MSE score of 38 (beating the baseline of 247) and the highest r-squared score of 0.85 when predicting from our train set which contains 2018 data.

We proceeded to use this XGBoost model with the best hyperparameters to predict and score our test set which contains 2019 data.

Using the test data, our final model had a MSE score of 44 (beating the baseline of 247) and a r-squared score of 0.80, which means that the model explains 80% of the variability of the response data that is predictable from the independent variables. This meets our criteria for success.

### Conclusion and Recommendations

#### Objective 1: Understanding different types of crime in San Francisco

The aim was to develop insights into the areas with the most crimes, and consider policy and operational measures which might help to bring down crime in those areas based on those insights.

We learnt that:
- zipcode 94111 had the highest number of total and preventable crime per capita in all of SF city. This zipcode corresponds with Embarcadero and the Financial District, which houses mainly offices and shopping malls. 
- zipcode 94103 had the highest number of violent, non-violent and drug crime per capita in all of SF city. This zipcode corresponds with parts of the Tenderloin neighborhood, which is notorious for gangs and drug crime. It is unsurprising that it has the highest number of such crime per capita. (https://en.wikipedia.org/wiki/Tenderloin,_San_Francisco) 
- zipcode 94104 had the highest number of white-collar crime per capita in all of SF city. This zipcode corresponds with a small area of offices in the financial district. Based on GoogleMaps, it appears that only office buildings are found within that zipcode, which might explain why white-collar crime per capita is the highest there, compared with other zipcodes which have a mix of building types e.g. malls, shops, residential. 

These insights are useful for the SF mayor, Police Commanders and district supervisors, and are the starting point for further investigation and analysis to finetune policies and operational methods. For example, within 94104, we could consider which buildings contributed to the most white-collar crime, why, and how to address the specific cause. Across zipcodes which have similar building demographics e.g. 94112 and 94134 which both mainly comprise residential buildings, we could ask why 94134 has almost two times the number of violent crime, and consider if measures implemented in 94112 could be implemented in 94134 as well. We could also consider diverting more resources in addressing drug crime to zipcode 94103, or set up a dedicated drug crime taskforce there.

#### Objective 2: Predicting the number of preventable crime in San Francisco

The aim was to predict the number of preventable crime given a specific zipcode, day of the week, and hour, which will help the police plan their patrol schedules and resources. We managed to predict the number of preventable crime well using the XGBoost model, with a r-squared score of 0.8.

Based on the above table, the San Francisco police can expect approximately 1 to 2 crimes to take place in the evening hours (6 to 8pm) of most days (with Saturday being a bit more frequent) at zipcode 94103. Therefore, they should send more resources to patrol zipcode 94103 during such evening hours to prevent such crime from taking place, and calibrate their resources for other zipcodes, days of the week, and hours accordingly.

### Next Steps

For objective 1:
- We should gather demographic data (population size, breakdown by age, employment status, profile, race etc.) for each zipcode, police district, and supervisor district so that we can tailor the analysis for each police commander and supervisor. The additional variables may also give rise to new insights or correlations which could be the impetus for taking different policy or operational approaches. 
- We should include data from previous years for sharper insights. 

For objective 2: 
- Similarly, we should gather demographic data which may be able to sharpen our model. We could also use it to help us understand which other variables have a strong influence on the number of preventable crimes in an area, which could give rise to new policy or operational approaches. 
- We should include data from previous years for sharper predictions. 

Besides quantitative data analysis, we should also corroborate our insights and findings with qualitative experiences of Police officers and policymakers who know the ground. Their experiences can augment the recommendations that arise from our quantitative analysis, and capture realities that may not be observable through quantitative data. 