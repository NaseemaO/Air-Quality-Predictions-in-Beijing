# Final-Project-4 Group-6. BootCamp: Data Visualization and Data Analytics
Air Quality Predictions in Beijing, China

Project Team: Alex Calametti, Brian Guenther, Gabriela Delgado, Naseema Omer 

# Objectives: 
Pediction models / Train algorithm(s) using Supervised Machine Learning to classify air quality feature(s) / measurements and predict the target variable for example Ozone (O3). 
Build additional models to predict other Targets for eg. CO

# Analysis

# Summary 

## Next Steps / Recommendations

# Technical Details
## Extraction, Transformation, and Loading (Backend ETL)

### Extraction
Data Selection:  https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data
12 files, one for each station downloaded in .csv format and placed in the Resources folder

Variables in data files:
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
1. Data drop S3 bucket: https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_drop.csv

2. Data_med S3 bucket: https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_med.csv

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

## Process 
### Linear Regression & Predictions using a single feature to predict the O3. Supervised Machine Learning Methods.
Explored by performing prediction models using 2 different cleansed datasets: 
1. Without Zero or Null Values
2. With Zero Values replaced with Median Values of their respective columns
Conclusion
* Decided to go with the Dataset 1 with data_drop.  
* Dataset 2 with the Zero values replaced with Median value of the respective column adds a lot of bias to the result.

## Linear Regression & Predictions using Multiple Variables



## Decision Trees



## Neural Networks


# Acknowledgements: 
Instructor: Hunter Hollis, TAs: Sam Espe and Randy Sendek, and Tutors for their guidance on this project.