# Real Estate Time Series Project

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/main/Images/Oahu.jpg?raw=true'>

## Overview
The real estate market in the United States offers a wide range of housing options but there’s little knowledge on how to value them to guide buyers and sellers.It is therefore a huge advantage to know which properties will provide a substantial Return On Investment(ROI) and which properties will most likely bring losses before making a decision on the property to buy.By using technical machine learning techniques,time series models can be built and analysed using historical information and thereafter,forecasting can be possible.

## Problem Statement
Housing You Too Ltd, a consulting and real estate firm, has been approached by a client eager to invest in properties with the goal of achieving the highest possible Return on Investment (ROI). The client is looking for our expert guidance to identify the top 5 zip codes in California that promise the best ROI. Recognizing the complexity and layered nature of this question, we are committed to providing a thorough and data-driven analysis. To achieve this, we will utilize the extensive Zillow dataset, which contains historical real estate data. By analyzing trends, property values, and other key metrics, we aim to deliver the most accurate and insightful recommendations to guide our client's investment decisions for maximum profitability.

## Objectives
- Identify the 5 best zip codes in California that will bring our clients the highest ROI.

- Build a time series regression model in order to predict the 5 most profitable zip codes.

- Using the dataset and the model created investigate the growth rate of the real estate industry in relation to sales value of properties.

- Identify the 5 worst zip codes in California that our client should avoid in order to prevent incurring losses.

## Challenges
- Data Ambiguity and Unpredictability: Since we are using real-world data, there is a possibility of ambiguity and unpredictability, which can lead to some inaccuracies in our analysis and predictions.

- Changing Market Conditions: Real estate markets are influenced by various external factors such as economic shifts, policy changes, and unforeseen events like natural disasters or pandemics. These factors can alter market conditions rapidly, making historical data less reliable for future predictions.

## Solutions
- We will implement robust data cleaning and preprocessing techniques to handle missing values, outliers, and inconsistencies. We will also use advanced statistical methods and machine learning algorithms that can manage noisy data and enhance prediction accuracy.

- Integrate real-time data sources and economic indicators into the analysis to account for current market conditions. Use adaptive models that can update predictions based on the latest data.

## Data Understanding
We will use a dataset containing information about the median house prices of different zipcodes in the United States from 1996 to 2018,contained in a csv file.
The columns in the dataset are:
- RegionID: Unique index, 58196 through 753844

- RegionName: Unique Zip Code, 1001 through 99901

- City: City in which the zip code is located

- State: State in which the zip code is located

- Metro: Metropolitan Area in which the zip code is located

- CountyName: County in which the zip code is located

- SizeRank: Numerical rank of size of zip code, ranked 1 through 14723

- 1996-04 through 2018-04: refers to the median housing sales values for April 1996 through April 2018, that is 265 data points of monthly data for each zip code


The datatypes involved are:
- float values
- integers
- objects

## Data Preparation and Analysis
The data was analysed and the first step was to check for missing/null and duplicate values.
There were no duplicates in the dataset.However,there were some missing values in the 'date' and 'metro' columns.
The missing values in the metro column were replaced with the string 'missing'.
Columns with missing date values were dropped.

The next step was to rename the column 'Region Name' to 'Zipcode'.

The final step was to generate two new columns; one for calculating the return on investment (ROI) and another for determining the coefficient of variation. The coefficient of variation measures the extent of data point dispersion around the mean and indicates the ratio of standard deviation to the mean. This enables investors to evaluate the level of risk involved relative to the ROI.

## Exploratory Data Analysis
Here we will visually analyze our data. This will help us gain an even deeper understanding of our data before modelling.

The first visual  is a bar plot reflecting the 5 locations with the highest median house sales values in April 2018.
In order,the top 5 were;
- Wichita,Kansas
- Deer Trail,Colorado
- Mount Ulla,North Carolina
- West Phalia,Michigan
- Florence,South Carolina

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%201.PNG?raw=true'>


Before proceeding,a melted copy of the dataframe is created to transform the dataframe into a more manageable format where all datetime columns are consolidated into a single column and their corresponding values in another. This process, known as “melting” the dataframe, enhances the ease of data manipulation and interpretation.

The new dataset has 3626260 rows and 11 columns.The data is from 4th April 1996 to 4th April 2018.The house with the lowest price has a price of 11300 dollars and the one with the highest price has a price of 8558700 dollars. The highest ROI on a house is 11.2% and the lowest ROI on a house is -53.3%.

The second visual is a line plot showing the overall trend of median house sales values.


<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%202.PNG?raw=true'>

As we can see the trend is an increasing linear trend, where we can see the median housing sales value increases every year.

The third visual is a bar plot showing the 10 metros in California with the highest median house sales values.It shows us which Metro areas have the highest potential in terms of amount of investment.

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%203.PNG?raw=true'>

After removing columns we do not need and  changing the date format to reflect the year only to further reduce our computational cost.,modelling can begin.

## Modelling
Our reference here is a dataframe containing a list of all the zipcodes in California,which we create from the mlted df.Each column represents a different zipcode in california(they are 1224 in total).
We will use of one this columns to guideus on making our model.

So we decompose it,make it stationary,then plot the autocorrelation and partial autocorrelation plots.

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%204.PNG?raw=true'>

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%205.PNG?raw=true'>

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%206.PNG?raw=true'>

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%207.PNG?raw=true'>

we can now build the 4 ARIMA and  3 SARIMA models and evaluate the mean squared error to determine the bset model.The ARIMA model with order(1,0,1) is the best model.

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%208.PNG?raw=true'>

Lastly,we fit our time series  on this model,perform forecasting and write a function to do the same to all columns in the dataframe containing California zipcodes,and return the 5 zipcodes with the highest forecasted ROIs and the 5 zipcodes with the lowest forecasted ROIs.

## Conclusion

<img src='https://github.com/FrankOyugi/Phase-4-Project/blob/modelling-edits/Images/projvis%209.PNG?raw=true'>

## Recommendation
- Invest in these 5 zipcodes:93241,93505,93588,95341 and 95485.
- Do not invest in these 5 zipcodes:91008,95436,91916,91101 and 91204.
- Increased use of digital marketting strategy to promote sales in future. The sales team should also consider discounts in future so as to entice customers thereby increasing sales.
- Since there is probability of decline in sales in the future, the company should avoid overstocking.









