# AIRLINE-LOYALTY-PROGRAM
A SQL project analyzing an airline loyalty program. The dataset encompasses customer loyalty profiles, flight activity, enrollment and cancellation details, and calendar data to uncover actionable insights into promotional campaign performance, customer adoption, retention, and flight behavior to improve loyalty program and marketing strategies.

## Table of Content

-	Project Overview
-	Project Scope
-	Business Objective
-	Document Purpose
-	Use Case
-	Data Source
-	Dataset Overview
-	Data Cleaning and Processing
-	Data Analysis and Insight
-	Recommendation
-	Conclusion

##	Project Overview

The project analyses the Airline Loyalty Program dataset to understand customer loyalty behaviour and flight activity. The project focuses on evaluating the performance of the 2018 promotional campaign, identifying customer demographics with higher campaign adoption, and assessing flight activity during the summer period.
The analysis was conducted using SQL Server Management Studio (SSMS) to explore customer and flight data, calculate key performance metrics, identify patterns and trends, and generate insights that can support data-driven decisions for improving customer engagement, loyalty program participation, and flight activity.

##	Project Scope

The scope of this project includes:

-	Time Period: Analysis of customer loyalty and flight activity data covering 2017 and 2018, with specific focus on the 2018 promotional campaign and summer flight activity from June to August 2018.
-	Geographical Scope: Customers across the Canadian provinces and cities represented in the dataset.
-	Customer Focus: Loyalty program membership, promotional campaign adoption, customer demographics, customer lifetime value (CLV), and membership cancellation.
-	Flight Focus: Total flights, distance travelled, points accumulated, points redeemed, and the dollar cost of redeemed points.
-	Key Variables: Enrolment type, loyalty card, gender, education, marital status, salary, CLV, province, city, enrolment and cancellation details, total flights, month, year, distance, points accumulated, and points redeemed.
Analysis:
-	Evaluating the impact of the 2018 promotional campaign on loyalty program membership.
-	Comparing campaign adoption across different customer demographic groups.
-	Identifying customer locations and demographic segments with higher or lower campaign adoption.
-	Comparing summer 2018 flight activity between campaign and Standard loyalty members.
-	Identifying patterns in customer flight behaviour and loyalty program engagement.
-	Generating insights and recommendations to support future loyalty campaigns, customer engagement, and retention strategies.

##	Project Objective

The main business objective of this project is to evaluate the effectiveness of the airline's loyalty program and the 2018 promotional campaign by analysing customer membership and flight behaviour.
The analysis aims to:

- Measure Campaign Performance: Determine the impact of the 2018 promotional campaign on loyalty program membership, including campaign enrolments, cancellations, retention, and net active members.
-	Identify Target Customer Segments: Determine which demographic groups and geographical locations showed higher or lower campaign adoption.
-	Evaluate Customer Engagement: Compare flight activity between campaign and Standard loyalty members during the summer of 2018.
-	Identify Customer Behaviour Patterns: Analyze loyalty membership and flight activity patterns to understand customer engagement with the program.
-	Support Business Decisions: Provide data-driven insights and recommendations that can help improve future promotional campaigns, customer retention, loyalty program participation, and customer engagement.


##	Document Purpose

This document serves as the primary analytical reference for the Airline Loyalty Program project, providing stakeholders with insights into customer loyalty membership, promotional campaign performance, customer demographics, and flight activity. It aims to provide actionable insights into:

- The performance and effectiveness of the 2018 promotional campaign in attracting and retaining loyalty program members.
-	Customer demographic and geographical segments with higher or lower campaign adoption.
-	Differences in flight activity between campaign and Standard loyalty members during the summer of 2018.
-	Recommendations for improving future promotional campaigns, customer engagement, loyalty program participation, and member retention.
  
The analysis presented in this document will support data-driven decision-making by providing a clear understanding of customer behaviour and identifying opportunities to improve the airline's loyalty program strategy.

##	Use Case

This analysis provides valuable insights that can support improvements across several areas of the airline's loyalty program. Key use cases include:

-	Campaign Evaluation: Assess the effectiveness of promotional campaigns in attracting and retaining loyalty members.
-	Customer Segmentation: Identify demographic and geographical groups with higher campaign adoption.
-	Customer Engagement: Understand differences in flight activity between campaign and Standard members.
-	Marketing Strategy: Use customer behaviour insights to improve the targeting and design of future loyalty campaigns.
-	Retention Strategy: Identify opportunities to strengthen member engagement and reduce loyalty program cancellations.

##	Data Source

The dataset utilized for this analysis was obtained from Maven Analytics Website, a reputable online platform known for providing data analytics training, resources, and practice datasets. Maven Analytics offers a wide range of datasets across various domains, allowing users to enhance their analytical skills through hands-on experience with real-world data.


##	Dataset Overview

The Airline Loyalty Program dataset contains customer loyalty and flight activity information used to analyze customer behaviour, loyalty membership, promotional campaign adoption, and flight activity. The dataset covers customer records and flight activity for 2017 and 2018 and consists of three main tables: CUSTOMER_LOYALTY, CUSTOMER_FLIGHT, and CALENDAR.

##### Content and Structure

The dataset is structured to include key attributes such as:

-	Customer Information: Country, province, city, gender, education, salary, and marital status.
-	Loyalty Information: Loyalty card, enrolment type, enrolment date, cancellation details, and customer lifetime value (CLV).
-	Flight Activity: Total flights, distance travelled, points accumulated, points redeemed, and dollar cost of points redeemed.
-	Calendar Information: Date-related fields used to support time-based analysis.
  
The CUSTOMER_LOYALTY table contains 16,737 members, the CUSTOMER_FLIGHT table contains 391,014 flight records, and the CALENDAR table contains 2,557 records.

##### Purpose of the Dataset

The dataset is used to evaluate the performance of the airline's loyalty program, with particular focus on the 2018 promotional campaign, customer adoption across different demographic groups, and flight activity during the summer of 2018. The analysis helps identify customer behaviour patterns and opportunities for improving loyalty program engagement and retention.

##	Data Cleaning and Processing

The data cleaning process was carried out in SQL Server Management Studio (SSMS) to ensure that the Airline Loyalty Program dataset was accurate, consistent, complete, and suitable for analysis. The cleaning process covered the CUSTOMER_FLIGHT, CUSTOMER_LOYALTY, and CALENDAR tables.

The process included reviewing the imported tables, validating their structure and data types, checking for NULL values and duplicates, investigating invalid and inconsistent records, correcting identified data-quality issues, and creating cleaned versions of the tables.

**1. Initial Table and Row Count Assessment**

The first step was to confirm that the three tables had been successfully imported into SQL Server and to establish their initial record counts.

```SQL
SELECT COUNT(*) AS Total_Rows
FROM Calendar;
```

```SQL
SELECT COUNT(*) AS Total_Rows
FROM Customer_Flight;
```

```SQL
SELECT COUNT(*) AS Total_Rows
FROM Customer_Loyalty;
```

The initial assessment established the size of the imported dataset:

-	CALENDAR: 2,557 records
-	CUSTOMER_FLIGHT: 392,936 records
-	CUSTOMER_LOYALTY: 16,737 records

  
The imported tables were also identified using the following query:

```SQL
SELECT 
    TABLE_SCHEMA,
    TABLE_NAME
FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_TYPE = 'BASE TABLE'
ORDER BY TABLE_NAME;
```

This confirmed the tables available in the SQL Server database before the cleaning and validation process began.


**2. CUSTOMER_FLIGHT Data Cleaning**

The CUSTOMER_FLIGHT table contained 392,936 records before cleaning. The table was assessed for its structure, NULL values, duplicate records, valid ranges, and internal consistency.

-	Column and Data Type Assessment

The structure and data types of the flight table were reviewed using:

```SQL
SELECT 
    TABLE_NAME,
    COLUMN_NAME,
    DATA_TYPE,
    CHARACTER_MAXIMUM_LENGTH,
    IS_NULLABLE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME IN ('CUSTOMER_FLIGHT')
ORDER BY TABLE_NAME, ORDINAL_POSITION;
```

This ensured that the flight fields were stored using appropriate data types before analysis.

-	NULL Value Assessment
  
NULL values were assessed across all major flight activity fields:

```SQL
SELECT
    COUNT(*) AS Total_Rows,
    SUM(CASE WHEN [LOYALTY_NUMBER] IS NULL THEN 1 ELSE 0 END) AS Null_Loyalty_Number,
    SUM(CASE WHEN [YEAR] IS NULL THEN 1 ELSE 0 END) AS Null_Year,
    SUM(CASE WHEN [MONTH] IS NULL THEN 1 ELSE 0 END) AS Null_Month,
    SUM(CASE WHEN [TOTAL_FLIGHTS] IS NULL THEN 1 ELSE 0 END) AS Null_Total_Flights,
    SUM(CASE WHEN [DISTANCE] IS NULL THEN 1 ELSE 0 END) AS Null_Distance,
    SUM(CASE WHEN [POINTS_ACCUMULATED] IS NULL THEN 1 ELSE 0 END) AS Null_Points_Accumulated,
    SUM(CASE WHEN [POINTS_REDEEMED] IS NULL THEN 1 ELSE 0 END) AS Null_Points_Redeemed,
    SUM(CASE WHEN [DOLLAR_COST_POINTS_REDEEMED] IS NULL THEN 1 ELSE 0 END) AS Null_Dollar_Cost
FROM [CUSTOMER_FLIGHT];
```

The NULL assessment was used to confirm the completeness of the flight data before further processing.

-	Duplicate Record Identification
  
Duplicate records were identified by comparing all fields that describe a flight activity record:

```SQL
SELECT 
    [LOYALTY_NUMBER],
    [YEAR],
    [MONTH],
    [TOTAL_FLIGHTS],
    [DISTANCE],
    [POINTS_ACCUMULATED],
    [POINTS_REDEEMED],
    [DOLLAR_COST_POINTS_REDEEMED],
    COUNT(*) AS Duplicate_Count
FROM [CUSTOMER_FLIGHT]
GROUP BY
    [LOYALTY_NUMBER],
    [YEAR],
    [MONTH],
    [TOTAL_FLIGHTS],
    [DISTANCE],
    [POINTS_ACCUMULATED],
    [POINTS_REDEEMED],
    [DOLLAR_COST_POINTS_REDEEMED]
HAVING COUNT(*) > 1
ORDER BY Duplicate_Count DESC;
```

A summary query was then used to quantify the duplicate records:

```SQL
SELECT 
    COUNT(*) AS Duplicate_Groups,
    SUM(Duplicate_Count) AS Rows_In_Duplicate_Groups,
    SUM(Duplicate_Count - 1) AS Extra_Duplicate_Rows,
    MAX(Duplicate_Count) AS Highest_Repetition
FROM (
    SELECT 
        [LOYALTY_NUMBER],
        [YEAR],
        [MONTH],
        [TOTAL_FLIGHTS],
        [DISTANCE],
        [POINTS_ACCUMULATED],
        [POINTS_REDEEMED],
        [DOLLAR_COST_POINTS_REDEEMED],
        COUNT(*) AS Duplicate_Count
    FROM [CUSTOMER_FLIGHT]
    GROUP BY
        [LOYALTY_NUMBER],
        [YEAR],
        [MONTH],
        [TOTAL_FLIGHTS],
        [DISTANCE],
        [POINTS_ACCUMULATED],
        [POINTS_REDEEMED],
        [DOLLAR_COST_POINTS_REDEEMED]
    HAVING COUNT(*) > 1
) AS Duplicates;
```


##### The assessment identified:

1.	1,906 duplicate groups 
2.	3,828 rows within duplicate groups 
3.	1,922 extra duplicate records
4.	3 as the highest repetition of a duplicated record

##### Removing Exact Duplicate Records

After identifying the duplicate records, a cleaned table was created using SELECT DISTINCT to retain one occurrence of each unique flight record:

```SQL
SELECT DISTINCT
    [LOYALTY_NUMBER],
    [YEAR],
    [MONTH],
    [TOTAL_FLIGHTS],
    [DISTANCE],
    [POINTS_ACCUMULATED],
    [POINTS_REDEEMED],
    [DOLLAR_COST_POINTS_REDEEMED]
INTO [CUSTOMER_FLIGHT_CLEANED]
FROM [CUSTOMER_FLIGHT];
```

The resulting table was then checked:

```SQL
SELECT COUNT(*) AS Cleaned_Row_Count
FROM [CUSTOMER_FLIGHT_CLEANED];
```

This produced 391,014 unique flight records.

A further duplicate check confirmed that duplicate groups no longer remained:

```SQL
SELECT
    COUNT(*) AS Duplicate_Groups
FROM (
    SELECT
        [LOYALTY_NUMBER],
        [YEAR],
        [MONTH],
        [TOTAL_FLIGHTS],
        [DISTANCE],
        [POINTS_ACCUMULATED],
        [POINTS_REDEEMED],
        [DOLLAR_COST_POINTS_REDEEMED],
        COUNT(*) AS Duplicate_Count
    FROM [CUSTOMER_FLIGHT_CLEANED]
    GROUP BY
        [LOYALTY_NUMBER],
        [YEAR],
        [MONTH],
        [TOTAL_FLIGHTS],
        [DISTANCE],
        [POINTS_ACCUMULATED],
        [POINTS_REDEEMED],
        [DOLLAR_COST_POINTS_REDEEMED]
    HAVING COUNT(*) > 1
) AS Duplicates;
```


**3. CUSTOMER_FLIGHT Value Validation**

After removing duplicates, the numerical flight fields were examined for invalid or unusual values.

-	Total Flights
  
  ```SQL
SELECT
    MIN([TOTAL_FLIGHTS]) AS Minimum_Flights,
    MAX([TOTAL_FLIGHTS]) AS Maximum_Flights,
    AVG(CAST([TOTAL_FLIGHTS] AS DECIMAL(18,2))) AS Average_Flights,
    SUM(CASE WHEN [TOTAL_FLIGHTS] < 0 THEN 1 ELSE 0 END) AS Negative_Flights,
    SUM(CASE WHEN [TOTAL_FLIGHTS] = 0 THEN 1 ELSE 0 END) AS Zero_Flights
FROM [CUSTOMER_FLIGHT];
```

-	Distance

  ```SQL
SELECT
    MIN([DISTANCE]) AS Minimum_Distance,
    MAX([DISTANCE]) AS Maximum_Distance,
    AVG(CAST([DISTANCE] AS DECIMAL(18,2))) AS Average_Distance,
    SUM(CASE WHEN [DISTANCE] < 0 THEN 1 ELSE 0 END) AS Negative_Distance,
    SUM(CASE WHEN [DISTANCE] = 0 THEN 1 ELSE 0 END) AS Zero_Distance
FROM [CUSTOMER_FLIGHT];
```


-	Points Accumulated

  ```SQL
SELECT
    MIN([POINTS_ACCUMULATED]) AS Minimum_Points_Accumulated,
    MAX([POINTS_ACCUMULATED]) AS Maximum_Points_Accumulated,
    AVG([POINTS_ACCUMULATED]) AS Average_Points_Accumulated,
    SUM(CASE WHEN [POINTS_ACCUMULATED] < 0 THEN 1 ELSE 0 END) AS Negative_Points,
    SUM(CASE WHEN [POINTS_ACCUMULATED] = 0 THEN 1 ELSE 0 END) AS Zero_Points
FROM [CUSTOMER_FLIGHT];
```


-	Points Redeemed

  ```SQL
SELECT
    MIN([POINTS_REDEEMED]) AS Minimum_Points_Redeemed,
    MAX([POINTS_REDEEMED]) AS Maximum_Points_Redeemed,
    AVG(CAST([POINTS_REDEEMED] AS DECIMAL(18,2))) AS Average_Points_Redeemed,
    SUM(CASE WHEN [POINTS_REDEEMED] < 0 THEN 1 ELSE 0 END) AS Negative_Points_Redeemed,
    SUM(CASE WHEN [POINTS_REDEEMED] = 0 THEN 1 ELSE 0 END) AS Zero_Points_Redeemed
FROM [CUSTOMER_FLIGHT];
```


-	Dollar Cost of Points Redeemed

  ```SQL
SELECT
    MIN([DOLLAR_COST_POINTS_REDEEMED]) AS Minimum_Dollar_Cost,
    MAX([DOLLAR_COST_POINTS_REDEEMED]) AS Maximum_Dollar_Cost,
    AVG(CAST([DOLLAR_COST_POINTS_REDEEMED] AS DECIMAL(18,2))) AS Average_Dollar_Cost,
    SUM(CASE WHEN [DOLLAR_COST_POINTS_REDEEMED] < 0 THEN 1 ELSE 0 END) AS Negative_Dollar_Cost,
    SUM(CASE WHEN [DOLLAR_COST_POINTS_REDEEMED] = 0 THEN 1 ELSE 0 END) AS Zero_Dollar_Cost
FROM [CUSTOMER_FLIGHT];
```

These checks were used to identify negative values, zero values, and unusual numerical patterns that could affect flight activity and loyalty-point analysis.







##### 	Internal Consistency Checks

Relationships between flight activity and other measures were also investigated.

```SQL
SELECT
    COUNT(*) AS Inconsistent_Records
FROM [CUSTOMER_FLIGHT]
WHERE [TOTAL_FLIGHTS] = 0
  AND [DISTANCE] > 0;
```

```SQL
SELECT
    COUNT(*) AS Inconsistent_Records
FROM [CUSTOMER_FLIGHT]
WHERE [POINTS_REDEEMED] = 0
  AND [DOLLAR_COST_POINTS_REDEEMED] > 0;
```

```SQL
SELECT
    COUNT(*) AS Inconsistent_Records
FROM [CUSTOMER_FLIGHT]
WHERE [POINTS_REDEEMED] > 0
  AND [DOLLAR_COST_POINTS_REDEEMED] = 0;
```

Additional checks were performed to identify records requiring investigation:

```SQL
SELECT
    COUNT(*) AS Records_To_Investigate
FROM [CUSTOMER_FLIGHT]
WHERE [TOTAL_FLIGHTS] = 0
  AND [POINTS_ACCUMULATED] > 0;
```

```SQL
SELECT
    COUNT(*) AS Records_To_Investigate
FROM [CUSTOMER_FLIGHT]
WHERE [TOTAL_FLIGHTS] > 0
  AND [POINTS_ACCUMULATED] = 0;
```

These checks helped determine whether unusual combinations of values represented potential data-quality issues.



**4. CUSTOMER_LOYALTY Data Cleaning**

The CUSTOMER_LOYALTY table was assessed for structure, NULL values, salary quality, customer uniqueness, and the validity of customer attributes.

-	Column and Data Type Assessment

  ```SQL
SELECT
    COLUMN_NAME,
    DATA_TYPE,
    IS_NULLABLE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'CUSTOMER_LOYALTY'
ORDER BY ORDINAL_POSITION;
```


-	NULL Value Assessment
  
NULL values were assessed across the customer loyalty fields:

```SQL
SELECT
    COUNT(*) AS Total_Rows,
    SUM(CASE WHEN [LOYALTY_NUMBER] IS NULL THEN 1 ELSE 0 END) AS Loyalty_Number_NULL,
    SUM(CASE WHEN [COUNTRY] IS NULL THEN 1 ELSE 0 END) AS Country_NULL,
    SUM(CASE WHEN [PROVINCE] IS NULL THEN 1 ELSE 0 END) AS Province_NULL,
    SUM(CASE WHEN [CITY] IS NULL THEN 1 ELSE 0 END) AS City_NULL,
    SUM(CASE WHEN [POSTAL_CODE] IS NULL THEN 1 ELSE 0 END) AS Postal_Code_NULL,
    SUM(CASE WHEN [GENDER] IS NULL THEN 1 ELSE 0 END) AS Gender_NULL,
    SUM(CASE WHEN [EDUCATION] IS NULL THEN 1 ELSE 0 END) AS Education_NULL,
    SUM(CASE WHEN [SALARY] IS NULL THEN 1 ELSE 0 END) AS Salary_NULL,
    SUM(CASE WHEN [MARITAL_STATUS] IS NULL THEN 1 ELSE 0 END) AS Marital_Status_NULL,
    SUM(CASE WHEN [LOYALTY_CARD] IS NULL THEN 1 ELSE 0 END) AS Loyalty_Card_NULL,
    SUM(CASE WHEN [CLV] IS NULL THEN 1 ELSE 0 END) AS CLV_NULL,
    SUM(CASE WHEN [ENROLLMENT_TYPE] IS NULL THEN 1 ELSE 0 END) AS Enrollment_Type_NULL,
    SUM(CASE WHEN [ENROLLMENT_YEAR] IS NULL THEN 1 ELSE 0 END) AS Enrollment_Year_NULL,
    SUM(CASE WHEN [ENROLLMENT_MONTH] IS NULL THEN 1 ELSE 0 END) AS Enrollment_Month_NULL,
    SUM(CASE WHEN [CANCELLATION_YEAR] IS NULL THEN 1 ELSE 0 END) AS Cancellation_Year_NULL,
    SUM(CASE WHEN [CANCELLATION_MONTH] IS NULL THEN 1 ELSE 0 END) AS Cancellation_Month_NULL
FROM [CUSTOMER_LOYALTY];
```

NULL values were reviewed according to the role of each field. In particular, cancellation-year and cancellation-month NULLs were retained because they represent members who had not cancelled.


-	Salary Validation and Cleaning
  
Salary values were specifically investigated for NULL, negative, zero, and positive values.

```SQL
SELECT
    COUNT(*) AS Negative_Salary_Records,
    MIN([SALARY]) AS Lowest_Salary
FROM [CUSTOMER_LOYALTY]
WHERE [SALARY] < 0;
```

Negative salary records were further examined by education:

```SQL
SELECT
    [EDUCATION],
    COUNT(*) AS Negative_Salary_Records,
    MIN([SALARY]) AS Lowest_Salary,
    MAX([SALARY]) AS Highest_Salary
FROM [CUSTOMER_LOYALTY]
WHERE [SALARY] < 0
GROUP BY [EDUCATION]
ORDER BY Negative_Salary_Records DESC;
```

The individual records were also reviewed:

```SQL
SELECT
    [LOYALTY_NUMBER],
    [EDUCATION],
    [SALARY],
    [GENDER],
    [MARITAL_STATUS],
    [LOYALTY_CARD],
    [CLV],
    [ENROLLMENT_TYPE]
FROM [CUSTOMER_LOYALTY]
WHERE [SALARY] < 0
ORDER BY [SALARY];
```

Zero salary records were also checked:

```SQL
SELECT
    COUNT(*) AS Zero_Salary_Records
FROM [CUSTOMER_LOYALTY]
WHERE [SALARY] = 0;
```

After investigating the salary values, a cleaned customer loyalty table was created in which negative salary values were converted to NULL rather than being retained as valid salaries:

```SQL
SELECT
    [LOYALTY_NUMBER],
    [COUNTRY],
    [PROVINCE],
    [CITY],
    [POSTAL_CODE],
    [GENDER],
    [EDUCATION],
    CASE
        WHEN [SALARY] < 0 THEN NULL
        ELSE [SALARY]
    END AS [SALARY],
    [MARITAL_STATUS],
    [LOYALTY_CARD],
    [CLV],
    [ENROLLMENT_TYPE],
    [ENROLLMENT_YEAR],
    [ENROLLMENT_MONTH],
    [CANCELLATION_YEAR],
    [CANCELLATION_MONTH]
INTO [CUSTOMER_LOYALTY_CLEANED]
FROM [CUSTOMER_LOYALTY];
```

The cleaned salary field was then rechecked:

```SQL
SELECT
    COUNT(*) AS Total_Rows,
    SUM(CASE WHEN [SALARY] < 0 THEN 1 ELSE 0 END) AS Negative_Salaries,
    SUM(CASE WHEN [SALARY] IS NULL THEN 1 ELSE 0 END) AS NULL_Salaries,
    SUM(CASE WHEN [SALARY] = 0 THEN 1 ELSE 0 END) AS Zero_Salaries,
    SUM(CASE WHEN [SALARY] > 0 THEN 1 ELSE 0 END) AS Positive_Salaries
FROM [CUSTOMER_LOYALTY_CLEANED];
```

This ensured that negative salary values were no longer treated as valid financial information.








**5. CUSTOMER_LOYALTY Postal Code Cleaning**

Postal codes were investigated because geographical analysis required valid Canadian postal-code formats.
The following query was used to identify records that did not follow the expected Canadian postal-code pattern:

```SQL
SELECT
    [POSTAL_CODE],
    COUNT(*) AS Customer_Count
FROM [CUSTOMER_LOYALTY_CLEANED]
WHERE [POSTAL_CODE] NOT LIKE '[A-Z][0-9][A-Z] [0-9][A-Z][0-9]'
   OR LEFT([POSTAL_CODE], 1) IN ('D','F','I','O','Q','U')
   OR SUBSTRING([POSTAL_CODE], 3, 1) IN ('D','F','I','O','Q','U')
   OR SUBSTRING([POSTAL_CODE], 5, 1) IN ('D','F','I','O','Q','U')
GROUP BY [POSTAL_CODE]
ORDER BY Customer_Count DESC;
```

Further validation was performed to identify invalid leading characters:

```SQL
SELECT
    [POSTAL_CODE],
    COUNT(*) AS Customer_Count
FROM [CUSTOMER_LOYALTY_CLEANED]
WHERE [POSTAL_CODE] NOT LIKE '[A-Z][0-9][A-Z] [0-9][A-Z][0-9]'
   OR LEFT([POSTAL_CODE], 1) IN ('D','F','I','O','Q','U','W','Z')
GROUP BY [POSTAL_CODE]
ORDER BY Customer_Count DESC;
```

Three specific invalid postal codes were identified and investigated:

```SQL
SELECT
    [POSTAL_CODE],
    COUNT(*) AS Customer_Count
FROM [CUSTOMER_LOYALTY_CLEANED]
WHERE [POSTAL_CODE] IN ('U5I 4F1', 'V10 6T5', 'V09 2E9')
GROUP BY [POSTAL_CODE]
ORDER BY Customer_Count DESC;
These invalid values were converted to NULL:
UPDATE [CUSTOMER_LOYALTY_CLEANED]
SET [POSTAL_CODE] = NULL
WHERE [POSTAL_CODE] IN ('U5I 4F1', 'V10 6T5', 'V09 2E9');
The cleaned postal-code field was then checked:
SELECT
    COUNT(*) AS Total_Rows,
    COUNT([POSTAL_CODE]) AS Non_NULL_Postal_Codes,
    SUM(CASE WHEN [POSTAL_CODE] IS NULL THEN 1 ELSE 0 END) AS NULL_Postal_Codes
FROM [CUSTOMER_LOYALTY_CLEANED];
```

A total of 921 invalid postal-code records were identified during the cleaning process, leaving 15,816 valid postal-code records for geographical analysis.



**6. CUSTOMER_LOYALTY Uniqueness Check**

After creating the cleaned customer loyalty table, the number of records and unique loyalty numbers were confirmed:

```SQL
SELECT
    COUNT(*) AS Total_Rows,
    COUNT(DISTINCT [LOYALTY_NUMBER]) AS Unique_Loyalty_Numbers
FROM [CUSTOMER_LOYALTY_CLEANED];
```

The cleaned table contained 16,737 unique loyalty members, confirming that the loyalty number could be used as the customer identifier for subsequent analysis and table relationships.


**7. CALENDAR Table Validation and Cleaning**

The CALENDAR table contained 2,557 records and was reviewed to ensure that the date dimension was complete and that its derived date fields were correctly calculated.

-	Calendar Structure

  ```SQL
SELECT
    COLUMN_NAME,
    DATA_TYPE,
    IS_NULLABLE,
    CHARACTER_MAXIMUM_LENGTH
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_SCHEMA = 'dbo'
  AND TABLE_NAME = 'Calendar'
ORDER BY ORDINAL_POSITION;
```

- Date Range and NULL Assessment

```SQL
SELECT
    MIN([Date]) AS Minimum_Date,
    MAX([Date]) AS Maximum_Date,
    COUNT([Date]) AS Non_NULL_Dates,
    COUNT(DISTINCT [Date]) AS Unique_Dates,
    SUM(CASE WHEN [Date] IS NULL THEN 1 ELSE 0 END) AS NULL_Dates
FROM [Calendar];
```

-	Missing Date Sequence Check
  
The calendar was checked to ensure that dates followed a continuous daily sequence:

```SQL
WITH DateCheck AS
(
    SELECT
        [Date],
        LEAD([Date]) OVER (ORDER BY [Date]) AS Next_Date
    FROM [Calendar]
)
SELECT
    [Date] AS Current_Date,
    Next_Date,
    DATEDIFF(DAY, [Date], Next_Date) AS Days_Between
FROM DateCheck
WHERE Next_Date IS NOT NULL
  AND DATEDIFF(DAY, [Date], Next_Date) <> 1;
```
  
A separate check was also used to identify missing date gaps:

```SQL
SELECT
    COUNT(*) AS Missing_Date_Gaps
FROM [Calendar] AS CalendarTable
WHERE NOT EXISTS
(
    SELECT 1
    FROM [Calendar] AS NextCalendarDate
    WHERE NextCalendarDate.[Date] =
          DATEADD(DAY, 1, CalendarTable.[Date])
)
AND CalendarTable.[Date] <
(
    SELECT MAX([Date])
    FROM [Calendar]
);
```


- Start-of-Year Validation

```SQL
SELECT COUNT(*) AS Incorrect_Start_of_Year
FROM [Calendar]
WHERE [Start_of_Year] <> DATEFROMPARTS(YEAR([Date]), 1, 1);
```

-	Start-of-Month Validation and Correction
  
The start-of-month field was checked against the actual first day of each month:

```SQL
SELECT COUNT(*) AS Incorrect_Start_of_Month
FROM [Calendar]
WHERE [Start_of_Month] <> DATEFROMPARTS(YEAR([Date]), MONTH([Date]), 1);
```

The field was then corrected using the appropriate date calculation:

```SQL
UPDATE [Calendar]
SET [Start_of_Month] = DATEFROMPARTS(YEAR([Date]), MONTH([Date]), 1);
```

The correction was subsequently validated:

```SQL
SELECT COUNT(*) AS Incorrect_Start_of_Month
FROM [Calendar]
WHERE [Start_of_Month] <> DATEFROMPARTS(YEAR([Date]), MONTH([Date]), 1);
```

- Start-of-Quarter Validation and Correction
  
The start-of-quarter field was also checked:

```SQL
SELECT COUNT(*) AS Incorrect_Start_of_Quarter
FROM [Calendar]
WHERE [Start_of_Quarter] <> DATEADD(
    QUARTER,
    DATEDIFF(QUARTER, 0, [Date]),
    0
);
```

The field was corrected using:

```SQL
UPDATE [Calendar]
SET [Start_of_Quarter] = DATEADD(
    QUARTER,
    DATEDIFF(QUARTER, 0, [Date]),
    0
);
```

The correction was then validated:

```SQL
SELECT COUNT(*) AS Incorrect_Start_of_Quarter
FROM [dbo].[Calendar]
WHERE [Start_of_Quarter] <> DATEADD(
    QUARTER,
    DATEDIFF(QUARTER, 0, [Date]),
    0
);
```

Finally, the completeness of the key calendar fields was checked:


```SQL
SELECT
    COUNT(*) AS Total_Rows,
    COUNT([Date]) AS Date_Count,
    COUNT([Start_of_Year]) AS Start_of_Year_Count,
    COUNT([Start_of_Quarter]) AS Start_of_Quarter_Count,
    COUNT([Start_of_Month]) AS Start_of_Month_Count
FROM [Calendar];
```


**8. Final Customer Flight Integrity Check**

After cleaning, the flight table was checked again for loyalty-number completeness and uniqueness:

```SQL
SELECT
    COUNT(*) AS Total_Rows,
    COUNT([LOYALTY_NUMBER]) AS Non_NULL_Loyalty_Numbers,
    SUM(CASE WHEN [LOYALTY_NUMBER] IS NULL THEN 1 ELSE 0 END) AS NULL_Loyalty_Numbers,
    COUNT(DISTINCT [LOYALTY_NUMBER]) AS Unique_Loyalty_Numbers
FROM [CUSTOMER_FLIGHT_CLEANED];
```

The relationship between the cleaned flight and customer loyalty tables was also checked to identify flight records whose loyalty numbers did not exist in the customer table:

```SQL
SELECT
    COUNT(DISTINCT Customer_Flight_Cleaned.[LOYALTY_NUMBER]) AS Unmatched_Loyalty_Numbers
FROM [CUSTOMER_FLIGHT_CLEANED] AS Customer_Flight_Cleaned
LEFT JOIN [CUSTOMER_LOYALTY_CLEANED] AS Customer_Loyalty_Cleaned
    ON CustomerFlightCleaned.[LOYALTY_NUMBER] =
       CustomerLoyaltyCleaned.[LOYALTY_NUMBER]
WHERE CustomerLoyaltyCleaned.[LOYALTY_NUMBER] IS NULL;
```


This final check ensured that the cleaned flight and customer loyalty tables were suitable for joining and subsequent analysis.

## Cleaning Outcome
The cleaning process produced the following analytical dataset:

-	CUSTOMER_FLIGHT: 392,936 original records reduced to 391,014 unique records after removing exact duplicate records.
-	CUSTOMER_LOYALTY: 16,737 unique loyalty members.
-	Postal Codes: 921 invalid postal-code records identified, with 15,816 valid postal-code records remaining.
-	CALENDAR: 2,557 records, with date fields reviewed and incorrect start-of-month and start-of-quarter values corrected.
-	Salary: Negative salary values were converted to NULL so that they would not be treated as valid salary values.
  
The cleaned tables were subsequently used for the business analysis of the 2018 promotional campaign, customer demographic adoption, loyalty membership, and summer 2018 flight activity.


##	Data Analysis and Insight

The objectives of this analysis is to the provide answers to the following questions:

1.	What impact did the campaign have on loyalty program memberships (gross / net)?
2.	Was the campaign adoption more successful for certain demographics of loyalty members?
3.	What impact did the campaign have on booked flights during summer?

**1.	What impact did the campaign have on loyalty program memberships (gross / net)?**

This question seeks to evaluate the impact of the 2018 promotional campaign on loyalty program membership by measuring the number of customers who enrolled during the campaign period and determining how many remained active after accounting for cancellations.
The analysis focuses on two key measures:

-	Gross Campaign Membership: The total number of customers who enrolled in the loyalty program through the campaign.
-	Net Campaign Membership: The number of campaign members remaining after subtracting customers who subsequently cancelled their membership.

Understanding gross and net membership growth helps evaluate the campaign's ability to attract new members and retain them after enrolment. A high gross enrolment indicates strong campaign reach, while a high net membership figure indicates that the campaign was also successful in retaining members.

##### SQL Analysis

The campaign membership was analyzed by identifying customers enrolled through the promotional campaign and comparing their membership status.

```SQL
SELECT
    [ENROLLMENT_TYPE],
    COUNT(*) AS Total_Members,
    SUM(
        CASE
            WHEN [CANCELLATION_YEAR] IS NOT NULL
            THEN 1
            ELSE 0
        END
    ) AS Cancelled_Members,
    SUM(
        CASE
            WHEN [CANCELLATION_YEAR] IS NULL
            THEN 1
            ELSE 0
        END
    ) AS Active_Members
FROM [CUSTOMER_LOYALTY_CLEANED]
GROUP BY [ENROLLMENT_TYPE]
ORDER BY Total_Members DESC;
```

The results were used to isolate the campaign members and determine their gross membership, cancellations, and remaining active members.

##### Results

| Membership Measure      | Campaign |
|-------------------------|----------|
| Gross Campaign Members  | 971      |
| Cancelled Members       | 115      |
| Net Active Members      | 856      |
| Retention Rate          | 88.16%   |
| Cancellation Rate       | 11.84%   |


The campaign attracted 971 loyalty program members. Of these, 115 members cancelled, leaving 856 active members. The campaign therefore achieved a net membership gain of 856 members after accounting for cancellations.

- Campaign Enrolment by Month
  
The campaign enrolment period covered February, March, and April 2018.

| Month    | Campaign Enrolments |
|----------|--------------------:|
| February | 295                 |
| March   | 330                 |
| April   | 346                 |
| **Total** | **971**            |



April recorded the highest number of campaign enrollments with 346 members, followed by March with 330 and February with 295.

##### Key Insights

-	Strong membership acquisition: The campaign attracted 971 new loyalty members, demonstrating that the promotion generated meaningful membership growth.
-	High retention: 856 members remained active, resulting in an 88.16% retention rate. This indicates that most customers acquired through the campaign continued their membership after enrollment.
-	Limited cancellation: Only 115 campaign members cancelled, representing an 11.84% cancellation rate.
-	Positive net membership impact: After accounting for cancellations, the campaign contributed 856 net active members to the loyalty program.
-	Enrollment increased throughout the campaign: Campaign enrollment rose from 295 members in February to 330 in March and 346 in April, with April producing the highest enrollment.
-	Campaign cancellation was slightly better than Standard membership: Campaign members recorded an 11.84% cancellation rate, compared with 12.38% among Standard members. This represents a 0.54 percentage-point lower cancellation rate for campaign members.
  

##### Conclusion

The 2018 promotional campaign had a positive impact on loyalty program membership. It generated 971 gross memberships and retained 856 members after cancellations, representing an 88.16% retention rate. The relatively low 11.84% campaign cancellation rate, compared with 12.38% for Standard members, suggests that campaign-acquired members were retained at a slightly better rate than Standard members. 
Overall, the campaign was effective in both attracting new loyalty members and maintaining a high proportion of those members, resulting in a meaningful net addition of 856 active members to the loyalty program.







**2.	Was the campaign adoption more successful for certain demographics of loyalty members?**
This question seeks to determine whether the 2018 promotional campaign was more successful among particular demographic groups within the loyalty program. Rather than looking only at the number of campaign members in each group, the analysis calculated campaign adoption rates by comparing campaign members with the total number of loyalty members in each demographic category. This provides a fairer comparison because demographic groups have different population sizes. The analysis considered gender, education, marital status, loyalty card type, salary, and customer lifetime value (CLV). Geographical adoption was analyzed separately using province and city.

##### SQL 

Campaign adoption was analyzed by grouping loyalty members according to each demographic characteristic and comparing campaign members with the total number of members.

```SQL
SELECT
    [GENDER],
    COUNT(*) AS Total_Customers,
    SUM(
        CASE
            WHEN [ENROLLMENT_TYPE] = 'Promotion'
            THEN 1
            ELSE 0
        END
    ) AS Campaign_Members,
    CAST(
        100.0 * SUM(
            CASE
                WHEN [ENROLLMENT_TYPE] = 'Promotion'
                THEN 1
                ELSE 0
            END
        ) / COUNT(*) AS DECIMAL(10,2)
    ) AS Adoption_Rate
FROM [CUSTOMER_LOYALTY_CLEANED]
GROUP BY [GENDER]
ORDER BY Adoption_Rate DESC;
```

The same analytical approach was applied to the other demographic variables to identify groups with relatively higher or lower campaign adoption.

#### Results

The analysis produced the following campaign adoption rates across the major demographic groups:


- Gender

  
| Gender | Campaign Members | Total Members | Adoption Rate |
|--------|-----------------:|--------------:|--------------:|
| Female | 494              | 8,410         | 5.87%         |
| Male   | 477              | 8,327         | 5.73%         |



Female members had a slightly higher campaign adoption rate than male members.


- Education


  
| Education            | Campaign Members | Total Members | Adoption Rate |
|----------------------|-----------------:|--------------:|--------------:|
| High School or Below | 50               | 782           | 6.39%         |
| Bachelor             | 632              | 10,475        | 6.03%         |
| College              | 238              | 4,238         | 5.62%         |
| Doctor               | 32               | 734           | 4.36%         |
| Master               | 19               | 508           | 3.74%         |


Education showed a clearer difference in campaign adoption than gender. Members with High School or Below education had the highest adoption rate at 6.39%, while members with a Master's degree had the lowest at 3.74%.



- Marital Status

  

| Marital Status | Campaign Members | Total Members | Adoption Rate |
|----------------|-----------------:|--------------:|--------------:|
| Divorced       | 155              | 2,518         | 6.16%         |
| Single         | 258              | 4,484         | 5.75%         |
| Married        | 558              | 9,735         | 5.73%         |




Divorced members recorded the highest adoption rate at 6.16%, although the difference between the groups was relatively small.


- Loyalty Card

  

| Loyalty Card | Campaign Members | Total Members | Adoption Rate |
|-------------|-----------------:|--------------:|--------------:|
| Aurora      | 208              | 3,429         | 6.07%         |
| Nova        | 330              | 5,671         | 5.82%         |
| Star        | 433              | 7,637         | 5.67%         |



Aurora card members had the highest adoption rate at 6.07%, while Star members had the lowest at 5.67%. The relatively narrow range indicates that loyalty card type was not a major differentiator in campaign adoption.


- Salary
  
Campaign adoption was also examined across salary bands:



| Salary Band       | Total Members | Campaign Members | Adoption Rate |
|-------------------|--------------:|-----------------:|--------------:|
| Low (< $40K)      | 98            | 86               | 87.76%        |
| Lower-Middle      | 3,202         | 202              | 6.31%         |
| Middle            | 4,387         | 211              | 4.81%         |
| Upper-Middle      | 3,271         | 146              | 4.46%         |
| High              | 5,779         | 326              | 5.64%         |



The Low salary group recorded an unusually high adoption rate of 87.76%. However, this group contained only 98 members, making it a much smaller population than the other salary bands. Therefore, this result should be interpreted cautiously. Among the larger salary groups, the Lower-Middle salary band had the highest adoption rate at 6.31%, while the Upper-Middle group recorded the lowest at 4.46%.


- Customer Lifetime Value (CLV)



| CLV Band       | Total Members | Campaign Members | Adoption Rate |
|----------------|--------------:|-----------------:|--------------:|
| Low            | 6,364         | 357              | 5.61%         |
| Lower-Middle   | 4,090         | 257              | 6.28%         |
| Middle         | 2,844         | 165              | 5.80%         |
| Upper-Middle   | 1,675         | 95               | 5.67%         |
| High           | 1,764         | 97               | 5.50%         |




The Lower-Middle CLV group recorded the highest adoption rate at 6.28%, while the High CLV group recorded 5.50%. The overall difference was relatively small, indicating that CLV was not a strong differentiator of campaign adoption.


##### Key Insights

-	Education was one of the stronger demographic differentiators. Adoption ranged from 6.39% among members with High School or Below education to 3.74% among members with Master's education.
-	Gender showed very little difference. Female members had a 5.87% adoption rate compared with 5.73% for males, a difference of only 0.14 percentage points.
-	Marital status showed modest variation. Divorced members had the highest adoption rate at 6.16%, compared with 5.75% for Single and 5.73% for Married members.
-	Loyalty card type was also a weak differentiator. Adoption ranged only from 5.67% to 6.07% across Star, Nova, and Aurora members.
-	Salary showed an unusual result in the Low salary group. Its 87.76% adoption rate was substantially higher than the other groups, but the result is based on only 98 members. It should therefore not be interpreted as evidence that low-income customers generally have dramatically higher campaign adoption.
-	CLV had limited influence on adoption. The difference between the highest and lowest CLV adoption rates was only 0.78 percentage points, suggesting that customer value was not a major factor distinguishing campaign adopters.

  
##### Conclusion

The analysis indicates that campaign adoption was more successful among certain demographic groups, but the strength of the difference varied considerably by demographic characteristic. Among the demographic variables analyzed, education showed one of the clearest differences in adoption, with rates ranging from 3.74% to 6.39%. Salary also produced a notable difference, although the exceptionally high rate for the Low salary group should be treated cautiously because of its small population. 
In contrast, gender, marital status, loyalty card type, and CLV showed relatively narrow differences in adoption rates. This suggests that these characteristics were less effective for distinguishing customers who were more likely to adopt the campaign.
Overall, the findings suggest that future campaign targeting could place greater emphasis on education and broader customer segmentation, while avoiding reliance on a single demographic characteristic. The results also highlight the importance of considering group size when interpreting unusually high adoption rates.



**3.	What impact did the campaign have on booked flights during summer?**

This analysis evaluates the relationship between the 2018 promotional campaign and customer flight activity during the summer period. Summer is defined as June, July, and August 2018. The analysis compares Promotion members with Standard members based on their total booked flights and average number of flights per member. Using the average flights per member provides a fairer comparison because the two enrollment groups have substantially different membership sizes.










