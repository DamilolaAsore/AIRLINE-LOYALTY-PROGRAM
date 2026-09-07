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

```SELECT COUNT(*) AS Total_Rows```

```FROM Calendar;```



SELECT COUNT(*) AS Total_Rows
FROM dbo.Calendar


