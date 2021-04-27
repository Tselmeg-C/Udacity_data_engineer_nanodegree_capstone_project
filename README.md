# Udacity_data_engineer_nanodegree_capstone_project
Data Engineering for Analysis on i94Immigration Data from US      
Key concepts: Data modelling, ETL, PySpark, Data Lake

## Overview    
The purpose of the data engineering capstone project is to to combine what I've learned throughout the Data Engineering Nanodegree program. I have chosen to complete the project provided by Udacity, which is provided with four datasets. The main dataset include data on immigration to the United States, and supplementary datasets include data on airport codes, U.S. city demographics, and temperature data.

## Project Summary
I worked with four datasets from different sources, designed a Star Schema and prepared them ready for interested analysis on immigration to USA. 

## Outline
### Step 1: Scope the Project and Gather Data
Since the scope of the project will be highly dependent on the data, these two things happen simultaneously. In this step, I have:

* Identify and gather the data I will be using for this project. 
* Explain what end use cases you'd like to prepare the data for (e.g., analytics table, app back-end, source-of-truth database, etc.)

### Step 2: Explore and Assess the Data
* Explore the data to identify data quality issues, like missing values, duplicate data, etc.
* Document steps necessary to clean the data

### Step 3: Define the Data Model
* Map out the conceptual data model and explain why I chose that model
* List the steps necessary to pipeline the data into the chosen data model

### Step 4: Run ETL to Model the Data
* Create the data pipelines and the data model
* Include a data dictionary
* Run data quality checks to ensure the pipeline ran as expected
  * Integrity constraints on the relational database (e.g., unique key, data type, etc.)
  * Unit tests for the scripts to ensure they are doing the right thing
  * Source/count checks to ensure completeness

## Datasets
The following datasets are included in the project. 

**I94 Immigration Data**: This data comes from the US National Tourism and Trade Office. A data dictionary is included in the workspace. [This] (https://travel.trade.gov/research/reports/i94/historical/2016.html) is where the data comes from.           
**World Temperature Data**: This dataset came from Kaggle. Read more about it [here](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data).                  
**U.S. City Demographic Data**: This data comes from OpenSoft. Read more about it [here](https://public.opendatasoft.com/explore/dataset/us-cities-demographics/export/).       
**Airport Code Table**: This is a simple table of airport codes and corresponding cities. It comes from [here](https://datahub.io/core/airport-codes#data).

## Instruction
This project was complete using PySpark and Pandas, library imported are as following:

import pandas as pd
import os
from pyspark import SparkConf, SparkContext
from pyspark.sql import SparkSession,Window
from pyspark.sql.types import *
from pyspark.sql.functions import *
