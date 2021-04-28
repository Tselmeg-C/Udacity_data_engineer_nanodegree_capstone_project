## Data dictionary 
### fact table 
Includes following columns with corresponding data types       
 |-- cic_id: integer (nullable = true)       id numbers of immigrants         
 |-- port: string (nullable = true)          three alphabetic identity codes of port through which the immigrants arrived             
 |-- mode: integer (nullable = true)         the way the immigrants arrived, 1 = 'Air', 2 = 'Sea', 3 = 'Land', 9 = 'Not reported'             
 |-- arrival_date: date (nullable = true)    the date the immigrants arrived in US            
 |-- arrive_year: integer (nullable = true)  the year the immigrants arrived in US            
 |-- arrive_month: integer (nullable = true) the month the immigrants arrived in US          
 |-- departure_date: date (nullable = true)  the date the immigrants leave US          
 |-- airline: string (nullable = true)       the name of airline the immigrants took        
 |-- flight_num: string (nullable = true)    the number of flight the immigrants tool       
 |-- arrive_city: string (nullable = true)   the city the immigrants first arrived in        
 |-- arrive_state: string (nullable = true)  the US state the immigrants first arrived in
 
 ### dim_immigrant 
Dimension table of information on immigrants, including following columns       
 |-- cic_id: integer (nullable = true) unique identity of immigrants       
 |-- age: integer (nullable = true) age of immigrants        
 |-- birth_year: integer (nullable = true) birth year of immigrants        
 |-- gender: string (nullable = true) gender of immigrants       
 |-- occupation: string (nullable = true) occupation of immigrants       
 |-- citizen_country: integer (nullable = true) three digit number indicating the citizenship country of the immigrants, country names are included in I94_SAS_Lables_Description          
 |-- resident_country: integer (nullable = true) three digit number indicating the residentship country of the immigrants, country names are included in I94_SAS_Lables_Description           
 |-- arrive_state: string (nullable = true)  the US state the immigrants first arrived, could be used as foreign combined with cic_id when joining with fact table     
 
 ### dim_city
Includes demography information of the cities that appeared in the fact table        
|-- city: string (nullable = true)    name of the city     
 |-- state: string (nullable = true)  state the city belongs to      
 |-- latitude: string (nullable = true)  coordinates latitude      
 |-- longitude: string (nullable = true)  coordinates longitude      
 |-- median_age: float (nullable = true)  median age of populations      
 |-- male_population: integer (nullable = true) number of male population       
 |-- female_population: integer (nullable = true) number of female population       
 |-- total_population: integer (nullable = true)  total number of population       
 |-- veterans_num: integer (nullable = true)  number of veterans      
 |-- foreign_born_population: integer (nullable = true) number of foreign_born population      
 |-- avg_household_size: float (nullable = true) average size of household        
 |-- american_indian_alaska_native: integer (nullable = true) number of population of the race as indicated in the column name               
 |-- asian: integer (nullable = true) number of population of the race as indicated in the column name        
 |-- african_american: integer (nullable = true) number of population of the race as indicated in the column name        
 |-- hispanic_latino: integer (nullable = true) number of population of the race as indicated in the column name        
 |-- white: integer (nullable = true)  number of population of the race as indicated in the column name        
 |-- state_code: string (nullable = true) state code
 
 ### dim_visa
Dimension table with information about visa of each immigrant     
 |-- cic_id: integer (nullable = true)  unique ids of immigrants       
 |-- visa_class: integer (nullable = true) one digit integer indicating the class of visa, 1 = Business, 2 = Pleasure, 3 = Student      
 |-- visa_issue_state: string (nullable = true) the code representing the place where visa was issued   |-- arrive_flag: string (nullable = true) Arrival Flag - admitted or paroled into the U.S.       
 |-- departure_flag: string (nullable = true) Departure Flag - Departed, lost I-94 or is deceased     
 |-- update_flag: string (nullable = true) Update Flag - Either apprehended, overstayed, adjusted to perm residence        
 |-- match_flag: string (nullable = true) Match flag - Match of arrival and departure records     
 |-- allowed_date: date (nullable = true) Date to which admitted to U.S. (allowed to stay until)       
 |-- visa_type: string (nullable = true)  Class of admission legally admitting the non-immigrant to temporarily stay in U.S. Detailed description is provided in the I94_SAS_Lables_Description       
 
 ### dim_airport
Dimension table of information about airport, including following columns 
 |-- ident: string (nullable = true)  ID of airport      
 |-- type: string (nullable = true)  type of airport     
 |-- name: string (nullable = true)  name of airport      
 |-- elevation_ft: string (nullable = true) elevation of airport   
 |-- municipality: string (nullable = true)  city of airport    
 |-- gps_code: string (nullable = true) gps_code of airport      
 |-- iata_code: string (nullable = true) unique iata_code of airport      
 |-- local_code: string (nullable = true) local_code of airport    
 |-- longitude: string (nullable = true) coordinates longitude
 |-- latitude: string (nullable = true)   coordinates  latitude     
 |-- iso_region: string (nullable = true) iso_region of airport      
