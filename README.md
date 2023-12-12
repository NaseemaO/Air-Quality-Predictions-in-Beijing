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
  * Linear Regression - Multiple Variable with plots.  
  * Decision Trees - multiple Variables
  * Neural Networks - 
  * Tableau - visualization and data analysis. 

See Technical Details below. 


# Analysis Summary

* Linear Regression Models:
  * As the temperature rises, the Ozone measures increase. 
  Slope of 2.96 in single variable Model with Temperature, and Target Ozone (O3). 
  r2 value of 0.356525701 indicates 35% variability of the data; 65% of data is not represented. 

  * Target Ozone (O3) measure predictions multiple variables: 
  There is a positive correlation between pollutant variables carbon monoxide, nitrogen dioxide, suplhur dioxide, PM2.5, and PM10 and O3. 
  The r2 is 0.5724457157382516 indicates 57% variability of the data. 

  * Target Carbon Monoxide (CO) measure predictions with multiple variables:
  There is a positive correlation between pollutant variables ozone, nitrogen dioxide, suplhur dioxide, PM2.5, and PM10 and CO.
  The r2 is 0.723158568713435 indicates 72% variability of the data. 

  * Using Pair Plots to visualize Feature Relationships, it appears that there is:
  The weather variables Temperature, Pressure, Dewpoint, Rain, and Windspeed do not have a significant impact on either O3, or CO. 
  There is a slight correlation between Temperature and both the O3, and CO.
  The O3 increases with temperature increase. (This matches the findings in the exploration of data in Tableau).
  The CO decreases with temperature increase. (This matches the findings in the exploration of data in Tableau).

  * Visualizing Multicollinearity with Pearson Correlation Coefficient Matrix between All Features (as Independent Features) and Heatmap shows:
  A positive correlation between Temperature and O3. (This matches the findings in the exploration of data in Tableau).
  A negative correlation between Temperature and CO. (This matches the findings in the exploration of data in Tableau).

  Models may be improved by getting more data / selecting a larger data set, fewer independent variables, or modifying some parameters for example Test Size.

* Tableau: 
Exploration done with, and without the additonal variable. Results are similar in both visualization sets.   
  * O3 has highest levels in the summer months.  Measures start climbing in April and start to decline in Sept.    

  * CO  starts declining in March, climbs in September. Exception year 2013 and part of  2015  drop in March and re-peak in  June, decline and re-peak in   Sept. 2015 yr continues its decline after June and follows the overall trend after.        

  * Temperatures in the warmer months may be a contributing feature for increaseing the O3 measures in the warmer summer months. 
  Linear Regression with single variable does show that as temperature increases, the ozone measure increases. 

# Technical Details
## Data Selection / Background
[Dataset Selected](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data) from UCI (University of California, Irvine) Machine Learning Repository that allows sharing given appropriate credit. 

This data set includes hourly air pollutants data from 12 nationally-controlled air-quality monitoring sites from the Beijing Municipal Environmental Monitoring Center which are matched with the nearest weather station from the China Meteorological Administration. 

The time period: March 1st, 2013 to February 28th, 2017. 

## Extraction, Transformation, and Loading (ETL)
### Extraction
12 files downloaded, one for each station downloaded in .csv format.  Raw_12_data_files.7z placed in the project Resources folder. 

Data / Variables in data files:
No: row number 
year: year of data in this row 
month: month of data in this row 
day: day of data in this row 
hour: hour of data in this row 
PM2.5: PM2.5 concentration (ug/m^3)   Particles that are 2.5 microns or less in diameter 
PM10: PM10 concentration (ug/m^3)     Particles with a diameter of 10 micrometres or less
SO2: SO2 concentration (ug/m^3)       Sulfur dioxide  
NO2: NO2 concentration (ug/m^3)       Nitrogen Dioxide
CO: CO concentration (ug/m^3)         Carbon Monoxide
O3: O3 concentration (ug/m^3)         Ozone
TEMP: temperature (degree Celsius)    
PRES: pressure (hPa)
DEWP: dew point temperature (degree Celsius)
RAIN: precipitation (mm)
wd: wind direction
WSPM: wind speed (m/s)
station: name of the air-quality monitoring site

1 PPM = 1,000 microgram per meter cubed. Similarly, 1 microgram per meter cubed = 0.001 PPM. To quickly convert from PPM to micrograms, multiply by 1,000

### Transformation 
Data Cleansing: 
Import into Panda Data Frames, concatenate the Pandas DataFrames, remove or impute Null rows (if between 5-10% of the total # or rows). May for example export as Parquet file, then use Spark. 

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
Cleaned data 3 files stored in AWS S3 Bucket, and zipped files placed in project Resources folder.

Read and Loaded appropriate cleaned data file(s) in the various code files for predictions and analysis 

## Programs 
AWS S3 Bucket
Decision Trees
Google Colaboratory 
Jupyter Notebook
Keras
Machine Learning
Neural Networks
Python, Pandas 
Scikit-learn
Spark 
Tableau
Tensor Flow 

## Models 
Supervised Machine Learning Methods.

#### Linear Regression Models performed with Single Feature, and Multiple Features.
SINGLE Feature Linear Regression Prediction Models: [Code Notebook](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\LinearR_Single_Variable.ipynb)

Data Exploration by performing Linear Regression Prediction Models with Single Features using 2 different cleansed datasets: 
1. Without Zero or Null Values
2. With Zero Values replaced with Median Values of their respective columns
Conclusion
* Dataset 2 with the Zero values replaced with Median value of the respective column adds a lot of bias to the result.
* Decided to proceed with using Dataset 1 with data_drop for the Project Analysi

Data Sample:

<img src="Images\LR_sample_data.PNG" alt="Sample of Data" width="600" height="350">


<img src="Images\LR_single_superposed_scatter_best_fit_line.PNG" alt="Linear Regression Single Variables Model" width="1000" height="600"> 

MULTIPLE Features Linear Regression Prediction Models: [Code Notebook](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\LinearR_Multi_Variables.ipynb) 

Model 1 with Target: O3

<img src="Images\LR_Multi_Variables_Model1_O3.PNG" alt="Linear Regression Multi Target O3" width="800" height="700"> 



Model 2 with Target: CO

<img src="Images\LR_Multi_Variables_Model2_CO.PNG" alt="Linear Regression Multi Target CO" width="750" height="650"> 


Relationships between features using pair plots visualized


<img src="Images\LR_relationships_features.PNG" alt="Relationship Between Features" width="800" height="800">


Visualized multicollinearity between independent features using a heatmap for Dependent Feature: O3


<img src="Images\LR_Multi_Heatmap_PearsonCorrCoefMatrix.PNG" alt="Multicollinearity Between Independent Features" width="800" height="500">




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

  Explored data, and analysis including 12 Stations in Tableau.

<img src="Images\TableauDashboard.PNG" alt="By Month and Date 2013-2017 for O3, and CO" width="800" height="500">

O3 levels are higher in the summer months.  Temperature is higher in the summer months. 
CO levels seem to be lower in the summer months in comparison to the colder weathered months. 


### Next Steps / Recommendations
Models may be improved by getting more data / selecting a larger data set, fewer independent variables, or modifying some parameters for example Test Size.
Trying out more different models and selecting the better / best models. 

# Acknowledgements: 
Instructor: Hunter Hollis, TAs: Sam Espe and Randy Sendek, and Tutors for their guidance on this project.
