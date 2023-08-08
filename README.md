# project-four
This was a group project worked on by Eric Matthews, Samson Zewde and Sean Seaforth. It is a continued exploration of suicide rates, utilizing different tools at different points.
## Background and Scope
For this project, we changed our focus slightly. We decided to look at worldwide data, as opposed to the United States specific data from the Centers for Disease Control and Prevention. Instead, we utilized a combined dataset sourced from Kaggle (the citations for the sources used by the creator of that set are also included in our data sources section below). It included the country, year, sex and the GDP's country. This allowed us to explore trends on a global basis, as well as a sizable amount of data in order to create a machine learning model. 
## Data Sourcing and Cleaning
For the most part, the source data in the CSV was largely fine. A few of the numbers needed to be converted to integers instead of strings, and a few column names caused issues when processing in Pandas. This was an easy fix, and was done in Microsoft Excel as pre-processing. A new column was also added in the Excel pre-processing, grouping the records' suicide rates into six groups:
  * 0-20 per 100k
  * 20-40 per 100k
  * 40-60 per 100k
  * 60-80 per 100k
  * 80-100 per 100k
  * 100+ per 100k

The next step was to pull the CSV into the Jupyter Notebook. This was accomplished using PySpark. A secondary dataframe was then created by a PySpark query to hold the two integer columns that would be used in the final dataframe for the machine learning model. Both dataframes were then converted from PySpark dataframes to Pandas dataframes for ease of manipulation. This also required setting the columns to the appropriate datatypes (as many were originally "objects"), in order to later make dummied data with Pandas. Dummies were made for the country, age and sex columns, which were then concatenated with the other two integer columns from before.
## Creating the Machine Learning Model
There were many false starts and multiple models that did not manage to exceed 10% accuracy. The issue became apparent, as they were trying to predict the suicide rates, which meant that it had a prediction set of 0 through 244.97. This realization led to the creation of groups, as discussed in the section above. This reduced the prediction set to only six potential outcomes, which led to much better success.

The final approach used Keras tuner for hypertuning a neural net model. With better organized data and a clearer purpose, the model exceeded 86% accuracy. At this point, the model was successfully predicting the suicide rate grouping of records. A few minor tweaks gave us a final model hitting 86.73% accuracy.
## Visualizing the Data and Creating Dashboards
Utilizing Tableau for visualizations, we wanted to show the domestic suicide rates in comparison to the world suicide rates. Within that comparison, we looked at suicide rates, not only by country, but also by gender. You will also notice that we did the percentage of suicides per country based on total suicides in the world. 

## Data Sources
[russellyates88]. (2018). Suicide Rates Overview 1985 to 2016 [dataset]. Retrieved from https://www.kaggle.com/datasets/russellyates88/suicide-rates-overview-1985-to-2016

United Nations Development Program. (2018). Human development index (HDI). Retrieved from http://hdr.undp.org/en/indicators/137506

World Bank. (2018). World development indicators: GDP (current US$) by country:1985 to 2016. Retrieved from http://databank.worldbank.org/data/source/world-development-indicators#

[Szamil]. (2017). Suicide in the Twenty-First Century [dataset]. Retrieved from https://www.kaggle.com/szamil/suicide-in-the-twenty-first-century/notebook

World Health Organization. (2018). Suicide prevention. Retrieved from http://www.who.int/mental_health/suicide-prevention/en/ 
