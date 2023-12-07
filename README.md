# Final-Project-4 Group-6. BootCamp: Data Visualization and Data Analytics
Air Quality Predictions in Beijing, China

Project Team: Alex Calametti, Brian Guenther, Gabriela Delgado, Naseema Omer 

# Objectives: 
Pediction models / Train algorithm(s) to classify air quality feature(s) / measurements and predict the level of O3, the Target. 
Build additional models to predict other Targets for eg. CO

# Analysis

# Results

# Summary 

## Next Steps

# Technical Details
## Process 
Extraction, Transformation, and Loading (Backend ETL)

Data Selection:  https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data
12 files, one for each station downloaded in .csv format and placed in the Resources folder

Data Cleansing: Import into Panda Data Frames, concatenate the Pandas DataFrames, remove or impute Null rows (if between 5-10% of the total # or rows)
May as example: Export as Parquet file, then use Spark. 

Cleaned Data Files: Two cleaned.csv files placed in AWS S3Bucket:
1. Data drop S3 bucket: https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_drop.csv

2. Data_med S3 bucket: https://project-4-group-6-air-quality.s3.us-east-2.amazonaws.com/data_med.csv


## Programs 
Python, Pandas 
Machine Learning
Scikit-learn
Spark and SQL 

# Acknowledgements: 
Instructor: Hunter Hollis, TAs: Sam Espe and Randy Sendek, and Tutors for their guidance on this project.

