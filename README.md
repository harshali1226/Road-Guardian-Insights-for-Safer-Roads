# Road Guardian: Insights for Safer Roads - Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/f833359b-2e44-4fe6-ba5e-fd1ecfe0148a/ReportSection?experience=power-bi

## Problem Statement

Road accidents are a significant public safety concern, causing a high number of casualties and fatalities each year. Understanding the factors contributing to these accidents such as vehicle type, road conditions, urban vs. rural settings, and time of day can help policymakers and safety authorities take data-driven decisions to reduce accidents and improve road safety.

By analyzing historical accident data, the project aims to identify critical factors influencing road safety, such as accident-prone locations, weather conditions, time of day, and vehicle types involved. The interactive dashboard provides actionable insights for policymakers, urban planners, and the public to foster safer roads.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that data contains 350K of records and 21 columns like "Accident Date", "Accident Severity", "Light conditions", "Road Type" any many more.
- Step 5 : Then I observed that in none of the empty values & errors were present except column named "Accident Serverity". "Fatal" was misprinted as "Fetal".
- Step 6 : Then to work with Time Intelligence functions, I have first created Date/Calendar table with columns Date, month, year, month number.
- Step 7 : So whenever you create an explicit table, data modelling needs to be carried out to create a relationship between the two tables.
- Step 8 : New measure was created to find the current year Number_of_casualties.

Following DAX expression was written for the same,
        
        CY casualties = TOTALYTD(SUM(DATA[Number_of_casualties]), 'Calendar'[Date])

- Step 9 : New measure was created to find the previous year Number_of_casualties.

Following DAX expression was written for the same,
        
        PY casualties = CALCULATE(SUM(DATA[Number_of_casualties]), SAMEPERIODLASTYEAR('Calendar'[Date])

- Step 10 : New measure was created to find YOY casualties.

Following DAX expression was written for the same,
        
        YOY casualties = ([CY casualties]-[PY casualties])/[PY casualties]

- Step 11 : Similarly calculate new measure for current year accidents.

Following DAX expression was written for the same,
        
        CY accidents = TOTALYTD(COUNT(DATA[Accident_Index]), 'Calendar'[Date])

- Step 12 : New measure was created to find the previous year accidents.

Following DAX expression was written for the same,
        
        PY accidents = CALCULATE(COUNT(DATA[Accident_Index]), SAMEPERIODLASTYEAR('Calendar'[Date])

- Step 13 : New measure was created to find YOY accidents.

Following DAX expression was written for the same,
        
        YOY accidents = ([CY accidents]-[PY accidents])/[PY accidents]

- Step 14 : To calculate CY Fatal casualties, CY Serious casualties and CY Slight casualties just apply filter with accident severity.

- Step 15 : In the report view, under the canvas background tab, theme was selected.

- Step 16 : To group the data based on vehicle type and make 6 different groups mentioned below,

  (a) Agricultural

  (b) Bike
  
  (c) Bus
  
  (d) Car
  
  (e) Others
  
  (f) Van

Snap of different vehicle types,

![image](https://github.com/user-attachments/assets/b2829aca-c6fa-4768-9e89-578a27a660f2)


- Step 17 :  Calculated column was created in which, casualties were grouped into various Accident Severity Categort like "High", "Medium" and "Low".

for creating new column following DAX expression was written;
       
        Accident Severity Category = 
            IF(
                Data[Accident Severity] = "Serious" , "High", 
            ElseIF(Data[Accident Severity] = "Fatal, "Medium",
            Else "Low")
        )
        
Snap of new calculated column ,

![image](https://github.com/user-attachments/assets/0040af59-5342-4039-ae68-7f34bee03b83)

- Step 18 : Visual filters (Slicers) were added for two fields named "Road Surface" & "Weather".

Snap of visual filters,

![image](https://github.com/user-attachments/assets/fb98502c-52c6-4512-8fe8-5248de5082ef)

 Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into calculation.

- Step 19 : Five card visuals were added to the canvas
1. Total CY casualties
2. Total CY accidents
3. Total Fatal accidents
4. Total Serious accidents
5. Total Slight accidents

Snap of Five visual filters,

![image](https://github.com/user-attachments/assets/a43d24ad-caf9-4b8e-a9d7-4a1414344a35)
          
- Step 20 : Click on any specific vehicle icon (e.g., Bike, Car) in the left panel to view casualty data specific to that vehicle.
- Step 21 : Urban vs. Rural Split: Use the pie chart to observe the distribution of accidents between urban and rural areas.
- Step 22 : Interact with the map to focus on specific regions where accidents frequently occur.
- Step 23 : Click on the green bars to highlight accident data for specific road types (e.g., Single carriageway, Roundabouts).
- Step 24 : A bar chart was also added to the report design area representing the number of monthly casualties . While creating this visual, field named "year" was also added to the Legends bucket, thus number of casualties are also seggregated according the year.

- Step 25 : The report was then published to Power BI Service.
 
 
![image](https://github.com/user-attachments/assets/1dd9c140-4d2e-47fb-8191-57d4a47705cf)

# Snapshot of Dashboard (Power BI Service)

![image](https://github.com/user-attachments/assets/fa5fc3b3-a889-463e-ab0e-cc955d1d6d82)



 
 # Report Snapshot (Power BI DESKTOP)

 
![image](https://github.com/user-attachments/assets/a30a5978-ea35-43f5-b945-eed5c6af776e)



- Step 26 : In the report view, two text boxes were added to the canvas, in one of them name of the Road Guardian was mentioned & in the other one tagline was written.
 

# Insights

A single page Dashboard was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of casualties 

   Total Number of CY (current year) Casualties = 128400

   Total Number of CY (current year) Accidents = 95900 

   Total Number of CY (current year) Fatal casualties = 1884 

   Total Number of CY (current year) Serious casualties = 18500 

   Total Number of CY (current year) Slight casualties = 108100 


           thus, the highest number of casualties are in Slight conditions.
           
### [2] Casualties by Vehicle Type

    a) Agriculture - 265
    b) Bike - 10537
    c) Bus - 4356
    d) Car - 101903
    e) Others - 962
    f) Van - 10418
  
  These values will change if different visual filters will be applied.  


 ### [3] Some other insights
 
 ### Casualties Monthly Trend (CY vs. PY):
 
Casualties show a significant decline in October and December compared to the previous year, indicating possible seasonal or intervention effects.
 
 ### Urban vs. Rural Casualties:
 
Urban areas account for the majority (65.4%) of casualties, which highlights the need for stricter road safety measures in cities.
         
### Casualties by Day/Night:

Most accidents occur during the day (80.6%), suggesting higher traffic volume or less caution in daylight conditions.

