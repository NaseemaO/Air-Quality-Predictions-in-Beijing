# Final-Project-4 Group-6. BootCamp: Data Visualization and Data Analytics
Air Quality Predictions in Beijing, China

Project Team: Alex Calametti, Brian Guenther, Gabriela Delgado, Naseema Omer 

# Objectives: 
Prediction models / Train algorithm(s) using Supervised Machine Learning to classify air quality feature(s) / measurements and predict the target variable for example Ozone (O3). 
Build additional models to predict other Targets for eg. CO

# Summary /Next Steps / Recommendations

# Technical Details
## Extraction, Transformation, and Loading (ETL)

### Extraction
[Dataset Selected](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data)

12 files downloaded, one for each station downloaded in .csv format. 

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

### Transformation 
Data Cleansing: 
Import into Panda Data Frames, concatenate the Pandas DataFrames, remove or impute Null rows (if between 5-10% of the total # or rows). May for example export as Parquet file, then use Spark. 

Variables removed: station

Cleaned Data Files: Two cleaned.csv files placed in AWS S3Bucket:
1. [Data drop S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_drop.csv)

2. [Data_med S3 bucket:](https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_med.csv)

### Loading 
Cleaned data files stored in AWS S3 Bucket
Read and Loaded in the various code programs for predictions and analysis 

## Programs 
Python, Pandas 
Machine Learning
Scikit-learn
Spark 
AWS S3 Bucket
Prediction Models: Supervised Machine Learning: Linear Regression, Decision Trees, Neural Networks.  

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

2. Target Feature: CO (Carbon Monoxide)
I will run it with another feature CO.  Yet to-do. 

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
  link 
  image


# Acknowledgements: 
Instructor: Hunter Hollis, TAs: Sam Espe and Randy Sendek, and Tutors for their guidance on this project.
