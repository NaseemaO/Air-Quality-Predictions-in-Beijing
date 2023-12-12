# Final-Project-4 Group-6. BootCamp: Data Visualization and Data Analytics
Air Quality Predictions in Beijing, China

Project Team: Alex Calametti, Brian Guenther, Gabriela Delgado, Naseema Omer 

# Objectives: 
Explore, build different prediction models / Train algorithm(s) using Supervised Machine Learning to classify air quality feature(s) for a Target Variable. 

Build additional models to predict other Targets. 

Models built with Target variable O3, and CO. 

# Analysis

Created and performed Prediction Models using Supervised Machine Learning: 
  * Linear Regression - Single Variable with plots: Scatter, Line, Superposed. 
  * Linear Regression - Multivariant with plots.  
  * Decision Trees - multiple Variables
  * Neural Networks - multiple variables and parsing of the data, different neural nets, autotuning.
  * Tableau - visualization and data analysis for trends on original data to compare with prediction models. 

See Technical Details below. 


# Analysis Summary

* Linear Regression Models:
  * Linear Model. As the temperature rises, the Ozone measures increase. 
    * Slope of 2.96 with Temperature, and Target Ozone (O3). 
    * r2 value of 0.356525701 indicates 35% variability of the data; 65% of data is not represented. 

  * Multivariant Model. Target Ozone (O3) measure predictions with multiple variables: 
    * There is a positive correlation between pollutant variables carbon monoxide (CO), nitrogen dioxide (NO2), suplhur dioxide (SO2), PM2.5, and PM10 and Ozone (O3). 
    * The r2 is 0.5724457157382516 indicates 57% variability of the data. 

  * Multivariant Model. Target Carbon Monoxide (CO) measure predictions with multiple variables:
    * There is a positive correlation between pollutant variables ozone, nitrogen dioxide, suplhur dioxide, PM2.5, and PM10 and CO.
    * The r2 is 0.723158568713435 indicates 72% variability of the data. 
    The Model is good. 

  * Using Pair Plots to visualize Feature Relationships, it appears that there is:
    * The weather condition variables Temperature, Pressure, Dewpoint, Rain, and Windspeed do not appear to have a significant impact on either O3, or CO. 
    * There is a some correlation between Temperature and both the O3, and CO.
    * The O3 increases with temperature increase. 
    * The CO decreases with temperature increase. 
    The results match the findings in the Simple and Multivariant Linear Regression Models, and from the exploration of data in Tableau.

  * Visualizing Multicollinearity with Pearson Correlation Coefficient Matrix between All Features (as Independent Features) and Heatmap shows:
    * A positive correlation between Temperature and O3. 
    * A negative correlation between Temperature and CO. 
    The results match the findings in the Simple and Multivariant Linear Regression Models, and from the exploration of data in Tableau.

  Models may be improved by getting more data, selecting a larger data set, fewer independent variables, or modifying some parameters for example Test Size.

* Tableau: 
Exploration performed with, and without the additonal variable 'Station'. Results are similar in both visualization sets. 
The Actual Trends in Tableau agree with the Prediction Model Trend.  

  * O3 has highest levels in the summer months.
  * Measures start climbing in April and start to decline in Sept.

  * CO  starts declining in March, climbs in September. 
    * Exception: Year 2013 and part of  2015 drops in March, re-peaks in June, declines and re-peaks in September.
    * Year 2015 continues its decline after June and follows the overall trend after.

  * Temperatures in the warmer months may be a contributing feature for increaseing the O3 measures in the warmer summer months. 
  Simple Linear Regression does show a positive correlation that as temperature rises, so do the Ozone measures. 

* Neural Networks Model:

* Decision Tree Models:


# Technical Details
## Data Selection / Background
[Dataset Selected](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data) from UCI (University of California, Irvine) Machine Learning Repository that allows sharing given appropriate credit. 

This data set includes hourly air pollutants data from 12 nationally-controlled air-quality monitoring sites from the Beijing Municipal Environmental Monitoring Center which are matched with the nearest weather station from the China Meteorological Administration. The data covers the time period of: March 1st, 2013 to February 28th, 2017. 

## Extraction, Transformation, and Loading (ETL)
### Extraction
12 files downloaded, one for each station downloaded in .csv format.  [Raw_12_data_files.7z placed in the project Resources folder](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\Resources). 

Each file contains approximately 35,000 rows and the following column headings:
No: row number 
year: year of data in this row 
month: month of data in this row 
day: day of data in this row 
hour: hour of data in this row 
PM2.5: PM2.5 concentration (ug/m^3)
PM10: PM10 concentration (ug/m^3)
SO2: SO2 concentration (ug/m^3)
NO2: NO2 concentration (ug/m^3)
CO: CO concentration (ug/m^3)
O3: O3 concentration (ug/m^3)
TEMP: temperature (degree Celsius)
PRES: pressure (hPa)
DEWP: dew point temperature (degree Celsius)
RAIN: precipitation (mm)
wd: wind direction
WSPM: wind speed (m/s)
station: name of the air-quality monitoring site

### Transformation 
Data Cleansing: 
Each of the initial csv files contain null values and were imported individually into Panda Data Frames.  We sought to quantify how many nulls were present in order to determine whether it was reasonable to drop the rows with null values or if too much data would be lost (greater than 10% cutoff).  During this stage,  we were not certain how values differed between stations, so the approach to replacing null values was to repalce null values the median value for a given column for that specific station.  We identified that up to 15% of rows within a given station's data contained null values but the number of nulls varied between stations.  We realized that the decision of drop versus replacement of nulls needed to be made on the final combined dataframe.  So both approaches to dealing with nulls was carried out (drop versus replace) by looping through each individual csv file.  Since the files contained identical column headings, we were able to concatenate the files together.  This produced three dataframes:  data(all original data, including nulls, for comparison), data_med(where nulls were replaced with the median of its respective column for it’s particular station), and data_drop (where rows containing null values were dropped).  Both dataframes data and data_med contain 420768 rows and data_drop has 382168 rows, a 9.2% loss of data due to dropping nulls.  Both data_med and data_drop were placed in an AWS S3Bucket for group usage, with the intention to compare and contrast models success for the different approaches to dealing with nulls.  In order to create a cleaner file, the code was re-run with the inclusion of the "index=False" during writing out the csv file.  This removed the addition of a column for the indexing of the combined dataframe and produced the data_drop2.csv, also placed in an AWS S3Bucket.

Cleaned Data Files: [Zipped cleaned data files](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\Resources)

Temporarily placed first three .csv files placed in AWS S3Bucket. 

1. [Data_drop S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_drop.csv)
Variables removed: 'station'

2. [Data_med S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_med.csv)
Variables removed: 'station'

3. [Data_drop2 S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_drop2.csv)
Variables removed:  'Station' and 'No' 

4. [Data_Tableau.7z is in Resources Folder](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\Resources\data_tableau.7z)
Variables removed: 'No'

### Loading 
Read and Loaded appropriate cleaned data file(s) in the various code files for predictions and analysis 

## Programs / Packages
AWS S3 Bucket
Decision Trees
Google Colaboratory 
Jupyter Notebook
Keras
Linear Regression
Machine Learning
Neural Networks
Python, Pandas 
Scikit-learn
Spark 
Tableau
Tensor Flow 

## Models and Analysis
Supervised Machine Learning Methods:

### Linear Regression performed with Simple and Multvariant Models.
#### Simple Linear Regression Prediction Models: [Code Notebook](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\LinearR_Single_Variable.ipynb)

Data Exploration by performing Linear Regression Prediction Models with Single Features using 2 different cleansed datasets: 
1. Null values dropped
2. Null values filled with the Median Values of their respective columns

Conclusion: 
* Dataset 2 with the Null values filled with Median values may add more bias to results.
* Decided to proceed the remainder of the project using Dataset 1 (data_drop.csv, and data_drop2.csv) for the remainder of the Project.

Data Sample:

<img src="Images\LR_sample_data.PNG" alt="Sample of Data" width="500" height="300">

Simple Linear Regression models performed: Linear Regression, Manual Prediction, and Prediction using Predict Function.  

  * The key slight differences in results of Dataset1 and Dataset2 are the Intercept, Slope, r2, and Predicted Ozone metrics.  

  * The prediction results with the Predict Function are identical in both datasets. 

  * The superposed scatter and best line fit plots are close. Image below shown for Dataset1.

  * Dataset1: Model's Formula y = 17.31191562019925 + 2.963656055355665X
    * The r2 is 0.3565257008834236
    * Predicted Ozone (O3) metrics with Dataset1 313.68

  * Dataset2: Model's formula: y = 18.118847608324636 + 2.866120914930229X
    * The r2 is 0.34434693063035227.
    * Predicted Ozone (O3) metrics with data2 304.73


<img src="Images\LR_simple_superposed_scatter_best_fit_line.PNG" alt="Linear Regression Single Variables Model" width="800" height="400"> 

Dataset 2 with Null Values filled with Median Values


The Predict Function results for both Dataset 1 and Dataset 2 are identical. 

<img src="Images\LR_PredictFunction_O3.PNG" alt="LR Single Variable Model Predict Function" width="200" height="150"> 


#### Multivariate Linear Regression Prediction Models: [Code Notebook](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\LinearR_Multi_Variables.ipynb) 

* Model 1 with Target: O3

<img src="Images\LR_Multivariant_Eval_Model1_O3.PNG" alt="Linear Regression Multi for O3" width="600" height="500"> 


* Model 2 with Target: CO

<img src="Images\LR_Multivariant_Eval_Model2_CO.PNG" alt="Linear Regression Multi for CO" width="600" height="500"> 


* Relationships between features using pair plots visualized


<img src="Images\LR_relationships_features.PNG" alt="Relationship Between Features" width="800" height="800">


* Visualized multicollinearity between independent features using a heatmap for Dependent Feature: O3


<img src="Images\LR_Multi_Heatmap_PearsonCorrCoefMatrix.PNG" alt="Multicollinearity Between Independent Features" width="600" height="400">




### Decision Trees

A decision tree regressor was modeled to evaluate how well ozone (O3) can be predicted based on the other variables present in our dataset. This was done using the Sklearn library. The decision tree was run using various different variables but the model that garnered the best results predicted O3 values from the date (year, month, day, hour). The R^2 value was 0.82 which meets the project requirement of 0.80. Limitations of this model were the time series aspect of the data, as we did not have enough time in class to comduct time series analysis to further optimize the model. This can be a next step to build on what we have completed thus far. 

### Neural Networks
With Keras, sklearn, pandas, and tensor flow

This model uses the O3 as the target variable (y) and the rest of the columns of interest in the dataset as the predictor (X). The data is scaled for better outcomes and autotune is used to optimize the model. The model uses layers with different values to train the model to predict the data from the target variable.

The results of this model are not significant no matter the adjustments made to it, such as the number of layers and the nodes they contain, as well as the parameters for the model compilation. Therefore, this model fails to predict the O3 values for this dataset. Results:
Loss = ~55
MSE = ~6500
MAE = ~56


## Tableau 
  [Beijing Air Quality Data Analysis on Tableau](https://public.tableau.com/app/profile/naseema.omer/viz/BeijingAirQualityDataAnalysis/BeijingAirQualityDataAnalysis)

  Explored data, and analysis on actual data in Tableau to visualize trends. The prediction trends are in agreement with the trends seen in Tableau. 

<img src="Images\TableauDashboard.PNG" alt="By Month and Date 2013-2017 for O3, and CO" width="800" height="500">

* O3 levels are higher in the summer months.  Temperature is higher in the summer months. 

* CO levels seem to be lower in the summer months in comparison to the colder weathered months. 


# Next Steps / Recommendations
* Models may be improved by obtaining more data, selecting a larger data set, including fewer independent variables, or modifying some parameters for example Test Size.
* Trying out additinal different models and selecting the better / best models. 

# Acknowledgements: 
Instructor: Hunter Hollis, TAs: Sam Espe and Randy Sendek, and Tutors for their guidance on this project.
