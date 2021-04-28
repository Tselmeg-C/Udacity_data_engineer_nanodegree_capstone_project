# Udacity_data_engineer_nanodegree_capstone_project
Data Engineering for Analysis on i94Immigration Data from US      
Key concepts: Data modelling, ETL, PySpark

## Overview    
The purpose of the data engineering capstone project is to to combine what I've learned throughout the Data Engineering Nanodegree program. I have chosen to complete the project provided by Udacity, which is provided with four datasets. The main dataset include data on immigration to the United States, and supplementary datasets include data on airport codes, U.S. city demographics, and temperature data.

## Project Summary
I worked with four datasets from different sources, designed a Star Schema and prepared them ready for interested analysis on immigration to USA. 

## Project Steps
### Step 1: Scope the Project and Gather Data

#### Scope 
I started from exploring the raw datasets, loading, checking size, schema, columns etc. and find out the connections between tables and do necessary cleanings. Then designed a Star Schema for the datasets which is fit to the analytical purpose of this project and selecting columns and join them to create the fact and dimension tables and save them back to the Udacity provided workspace. Data will be processed mainly with PySpark and the final tables will be stored back to the workspace as parquet files.

#### Datasets
The following datasets are gathered. 

**I94 Immigration Data**: This data comes from the US National Tourism and Trade Office. A data dictionary is included in the workspace.[This](https://travel.trade.gov/research/reports/i94/historical/2016.html) is where the data comes from.           
**World Temperature Data**: This dataset came from Kaggle. Read more about it [here](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data).                  
**U.S. City Demographic Data**: This data comes from OpenSoft. Read more about it [here](https://public.opendatasoft.com/explore/dataset/us-cities-demographics/export/).       
**Airport Code Table**: This is a simple table of airport codes and corresponding cities. It comes from [here](https://datahub.io/core/airport-codes#data).

The immigration data and the global temperate data is in an attached disk of Udacity provided workspace. They were not uploaded in thie repo. 
End data were loaded as parquet files back into the Udacity cloud storage and did not uploaded in the repo either.

### Step 2: Explore and Assess the Data
* Explore the data to identify data quality issues, like missing values, duplicate data, etc.
* Document steps necessary to clean the data

### Step 3: Define the Data Model
#### 3.1 Conceptual Data Model    
My data modeling concept is to keep the most relevant information together in one table and reserve the most frequently requested information (from my perspective) in the fact table. In this way a lightweight fact table is produced to retrieve often needed information, in case further information is need for the analysis, joining another table (dimension table) under the Star Schema framework is also not so costly. Ideally, the dimension tables could be further normalized, a Snowflake Schema will possibly more proper considering the some metadata of dimension tables, but it will possibly cause more costly joins among tables and reduce database integrity. After consideration, I decided on a Star Schema, specifically the fact and dimension tables look like the following:       

#### Fact table

__fact_immigration_record__:        
*__cic_id (PK)__, port(FK), arrival_date, arrive_year, arrive_month, departure_date, ariline, flight_num, arrive_city (FK), arrive_state (FK), mode*

#### Dimention Tables   
1. __dim_immigrant__: *__cic_id (PK)__, age, occupation, gender, birth_year, citizen_country,resident_country*

2. __dim_city__: *city, state, state_code, longitude, latitude, median_age, avg_household_size, total_population,
male_population, female_population, veterans_num, foreign_born_population, american_indian_alaska_native, asian,african_american, hispanic_latino, white, __(city,state PK)__*

3. __dim_airport__: *__id (PK)__, type, name, elevation_ft, iso_region, municipality, gps_code, iata_code (FK) reference fact_port, local_code, longitude, latitude*

4. __dim_visa__: *__cic_id (PK)__, visa_type, visa_class, visa_issue_state, rrive_flag, departure_flag, update_flag, match_flag, allowed_date*

#### 3.2 Mapping Out Data Pipelines
When creating tables I kept some "null" values when makes sense, only duplicated records were excluded, because it makes no sense to exclude records with "null" values out of the database, with the cost of deleting other usefull information about the immigrant, considering one of the most possible important usages of the database is to keep track of every immigrant. 

The steps necessary to pipeline the data into the chosen data model are:

1. Extract: load datasets (sas_data, demography, coordinate, airport) from the sources (parquet files stored in local/cloud after the data cleaning step)    

2. Transform: selecting target columns from each data set and join them to compose fact and dimension tables  

3. Load: write the final tables back to local/cloud as parquet files (I loaded back the tables directly to the Udacity provided workspace storage, for self implication on cloud self-configuration of cloud infrastructure is necessary)

### Step 4: Run ETL to Model the Data
* Create the data pipelines and the data model
* Include a data dictionary (seperatly stored as data_dictionary.md)
* Run data quality checks to ensure the pipeline ran as expected
  * Integrity constraints on the relational database (e.g., unique key, data type, etc.)
  * Unit tests for the scripts to ensure they are doing the right thing
  * Source/count checks to ensure completeness

## Instruction
This project was complete using PySpark and Pandas, libraries imported are as following:

import pandas as pd     
import os      
from pyspark import SparkConf, SparkContext      
from pyspark.sql import SparkSession,Window       
from pyspark.sql.types import *      
from pyspark.sql.functions import *       

## Files description
* Capstone Project Template-Copy2.ipynb: all the scripting is done in this Jupyter Notebook 
* data_dictionary.md: explanations of tables (columns, datatypes, descriptions)
* airport-codes_csv.csv: Udacity provided airport data  
* I94_SAS_Labels_Descriptions.SAS: Description file about the immigration data set.
* immigration_data_sample.csv: Sample of immigration data to provide a glimps of the data structure. The complete dataset was not uploaded in this repo.
* us-cities-demographics.csv: Udacity provided US demography data.


## Acknowledgment
Thanks to Udacity for creating this Nanodegree program and the dedicated mentors, reviewers, and peer students for helping me out when I am stuck and providing valuable feedback!
