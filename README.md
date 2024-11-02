# Road Accident Dashboard

#### Dashboard Link: https://drive.google.com/file/d/1EiDM9nb1fkwvPQQ3tzyCAsQ4Otf_VcBe/view?usp=drive_link

## Problem Statement

This dashboard will help the organizations like GRSP, NISCHA Bangladesh etc. and even the government to understand the casualties better. It will help the organizaions to know about casualties happened by what types of vehicles and how much, in which type of roads casualties happened the minimum or maximum. hrough different ratings and percentages they will get to know which areas are the most accident prone. They will also get a comparison of previous year and current year's accident scenario.

### Requirements
1. Finding total casualties and total accident values for the current year and year-on-year growth (Primary KPI)
2. Finding total casualties by accident severity for the current year and year-on-year growth (Primary KPI)
3. Finding total casualties concerning vehicle type for the current year (Secondary KPI)
4. Find out monthly trends showing the comparison of casualties for the current year and the previous year
5. Find out casualties by road type for the current year
6. Find out the current year's casualties by area/location and by day/night
7. Finding total casualties and total accidents by location

### Steps followed

- Step 1: Load data into Power BI Deskop, dataset is a csv file
- Step 2: Select the dataset and go o table view to check every atribute individually and look for any unusual value possible
- Step 3: It was found that in the column named 'Accident_Severity' there was error in a value which was a typo mistake and it created two different values- Fatal and Fetal. Using 'Replace values' option the problem was solved.
- Step 4: To findout Primary KPIs it was needed to perform Data Modeling and build new data table named 'Calendar' which had the attributes named 'Date', 'Year', 'Month, 'Month Number'. Data Analysis Expressions (DAX Query) was used to do so.
- Step 5: Build up One to Many relationship with Data table's Accident Date with Calendar table's Date
![Cardinality](https://github.com/user-attachments/assets/b0375d0a-7d75-422c-8020-54aaf50d36e3)
- Step 6: To find out primary and secondary KPIs new measures like 'CY Casualties', 'PY Casualties', 'YoY Casualties', 'CY Accidents', 'PY Accidents', 'YoY Accidents' were calculated using DAX Query
- Step 7: A total number of 5 unique cards were generated for data visualization using those new measures mentioned in Step 6
- Step 8: Two donut chat and one stacked bar cahrt chart were generated presenting casualties regarding Area, light and road condittions
- Step 9: Comparison between current and previous year's casualties was presented through a stacked bar chart
- Step 10: Casualties caused by different vehicle types and numbers were calculated and presented individually. While doing so, all the mentioned vehicles were grouped ino six (6) different types.
- Step 11: Casualtiesd by proper location were measured by plotting lattitude, longitude and current year casualties in a map visualizer
- Step 12: Two different slicers were introduced based on road and weather conditions

### Customizations with DAX

- Calendar Table (Date Column)
DAX: Calendar = CALENDAR(MIN(Data[Accident Date]), MAX(Data[Accident Date]))
![Calendar Table](https://github.com/user-attachments/assets/828e1b20-498d-4ef2-9292-fedea6fea020)

- Month Column
DAX: Month = FORMAT('Calendar'[Date], "mmmm")
- Month Number Column
DAX: Month Number = MONTH('Calendar'[Date])
- Year Column
DAX: Year = YEAR('Calendar'[Date])


![Current Year Cards](https://github.com/user-attachments/assets/893ab1cf-965d-4cf8-bfdf-13c58d97afe5)
- Current Year Accidents (New Measure)
DAX: CY Accidents = TOTALYTD(COUNT(Data[Accident_Index]), 'Calendar'[Date])
- Current Year Casualies (New Measure)
DAX: CY Casualties = TOTALYTD(SUM(Data[Number_of_Casualties]), 'Calendar'[Date])
- Previous Year Accidents (New Measure)
DAX: PY Accidents = CALCULATE(COUNT(Data[Accident_Index]), SAMEPERIODLASTYEAR('Calendar'[Date]))
- Previous Year Casualies (New Measure)
DAX: PY Casualties = CALCULATE(SUM(Data[Number_of_Casualties]), SAMEPERIODLASTYEAR('Calendar'[Date]))
- Year on Year Accidents (New Measure)
DAX: YoY Accidents = ([CY Accidents] - [PY Accidents]) / [PY Accidents]
- Year on Year Casualies (New Measure)
DAX: YoY Casualties = ([CY Casualties] - [PY Casualties]) / [PY Casualties]

### Groups

- Road Surface Conditions
![Road Group](https://github.com/user-attachments/assets/5e868781-0012-47ce-9aad-c751ca53ea25)

- Vehicle
![Vehicle Group](https://github.com/user-attachments/assets/66bb68e4-2382-42a4-b11e-4d5a8d5c2516)

- Weather
![Weather Group](https://github.com/user-attachments/assets/cc37b12f-ae19-4691-89d8-61d4e084cb72)

### Insights
A single page report was created in Power BI Desktop
![Road Accident Dashboard](https://github.com/user-attachments/assets/6c85d4b5-1985-45ec-a44e-b330ded255c6)
Following inferences can be drawn from the dashboard -

#### [1] Total Number of Casualties: 195700, which is 11.9% less than previous year
	a) Fatal Casualtties: 2900, 33.3% lesser than previous year
	b) Serious Casualies: 27000, 16.2% lesser than previous year
	c) Slight Casualties: 165800, 10.6% lesser than previous year

#### [2] Total Number of Accidents: 14440, which is 11.7% less than previous year

From these numbers it can be determined that accidents and the casualties are being lower year to year

#### [3] Casualties based on location is Urban: 61.95% and Rural: 38.05%
#### [4] Casualties based on Daylight condition is Day time: 73.84% and Night time: 26.16%
