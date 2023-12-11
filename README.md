# Final-Project-4 Group-6. BootCamp: Data Visualization and Data Analytics
Air Quality Predictions in Beijing, China

Project Team: Alex Calametti, Brian Guenther, Gabriela Delgado, Naseema Omer 

# Objectives: 
Explore, build different prediction models / Train algorithm(s) using Supervised Machine Learning to classify air quality feature(s) for a Target Variable. 

Build additional models to predict other Targets. 

Models built with Target variable O3, and CO. 


# Summary /Next Steps / Recommendations

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

Variables removed: 'station' 
Cleaned Data Files: Two cleaned.csv files placed in AWS S3Bucket:
1. [Data_drop S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_drop.csv)

2. [Data_med S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_med.csv)

Variables removed:  'Station' and 'No' 
3. [Data_     :](https://                 )

Variables removed: 'No' 
4. [Data_Tableau.7z is in Resources Folder](https://github.com/NaseemaO/Air_Quality_Predictions_in_Beijing.git\tree\main\Resources\data_tableau.7z)

### Loading 
Cleaned data 3 files stored in AWS S3 Bucket, and zipped files placed in project Resources folder.

Read and Loaded appropriate cleaned data file(s) in the various code files for predictions and analysis 

## Programs 
Python, Pandas 
Machine Learning
Scikit-learn
Spark 
AWS S3 Bucket
Tableau

Prediction Models: 
Supervised Machine Learning: 
Linear Regression - Single Variable, Linear Regression - Multiple Variable,  Decision Trees, Neural Networks.
Visualization and data analysis in Tableau.  

## Analysis
### Supervised Machine Learning Methods.
### Linear Regression Models performed with Single Feature, and Multiple Features.

Data Exploration by performing Linear Regression Prediction Models with Single Features using 2 different cleansed datasets: 
1. Without Zero or Null Values
2. With Zero Values replaced with Median Values of their respective columns
Conclusion
* Dataset 2 with the Zero values replaced with Median value of the respective column adds a lot of bias to the result.
* Decided to proceed with using Dataset 1 with data_drop for the Project Analysis. 

#### Single Feature Linear Regression Prediction Models 
With SciKit-learn, Manual Predictions, Predict Function
I need to put a chart together and have an image of it in here for the Single, and Multi Regressions so its not so wordy and long here. 
And a chart with the Evaluations for both

Sample of data values with dropped date/time and wd columns


<img src="Images\LR_sample_data.PNG" alt="Predict Function" width="600" height="350">


Independent Single Variable: TEMP (Temperature)  
Target Feature: O3 (Ozone)
Linear Regression
Model's slope: 2.96365606
Model's y-intercept: 17.31191562019925
Best Fit Line: Model's formula: y = 17.31191562019925 + 2.963656055355665X

Manual Predictions
Model's formula: y = 17.31191562019925 + 2.963656055355665 * 100
Predicted Ozone (O3) metrics 313.68

Predict Function


<img src="Images\LR_PredictFunction_O3.PNG" alt="Predict Function" width="200" height="150">

Assessing the Model

  The score is 0.3565257008834236.

  The r2 is 0.3565257008834236.

  The mean squared error is 2069.351378037146.

  The root mean squared error is 45.490123961549564.

  The standard deviation is 56.70893843043617.


#### Multiple Variables Linear Regression Predictions: 
Data exploration for predictions with different Target Features
1. Target Feature: O3 

mean_squared_error :  1378.584450481671

mean_absolute_error :  27.07180456217113

2. Target Feature: CO 

mean_squared_error :  370530.05017968314

mean_absolute_error :  376.8932019597799

Visualized relationships between features using pair plots


<img src="Images\LR_relationships_features.PNG" alt="Relationship Between Features" width="800" height="800">


Visualized multicollinearity between independent features using a heatmap for Dependent Feature: O3


<img src="Images\LR_Multi_Heatmap_PearsonCorrCoefMatrix.PNG" alt="Multicollinearity Between Independent Features" width="800" height="400">

Intercept:  -117.03237018427141
Coefficients array:  [ 1.57294634e-01  3.93318439e-02  2.84525105e-01 -7.97442020e-01
  1.33234639e-03  4.33588565e+00  1.31796078e-01 -1.58767871e+00
  8.68608179e-01  2.29319850e+00]

### Decision Trees



### Neural Networks



## Tableau 
  [Beijing Air Quality Data Analysis on Tableau](https://public.tableau.com/views/BeijingAirQualityDataAnalysis/Story1?:language=en-US&:display_count=n&:origin=viz_share_link)

  Explored data, and analysis including 12 Stations in Tableau.

<img src="Images\TableauDashboard.PNG" alt="By Month and Date 2013-2017 for O3, and CO" width="800" height="500">


# Acknowledgements: 
Instructor: Hunter Hollis, TAs: Sam Espe and Randy Sendek, and Tutors for their guidance on this project.
