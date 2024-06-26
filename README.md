# Sales_Performance_Analysis_for_a_Telecom_Company_USA_1
A Data Analysis Project that Analysed  the sales performance of a Telecommunication  company Based in the United State. The company’s sales transaction data generated over the past years was used for the  analysis.

## Table of Content
- [Project overview](#project-overview)
- [Data Sources](#data-sources)
- [Data Analysis Tools Used](#data-analysis-tools-used)
- [Data Collection](#data-collection)
- [Data Cleaning and Formatting](#data-cleaning-and-formatting)
- [Loading Data into Power BI](#loading-data-into-power-bi)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Data Analysis](#data-analysis)
- [Results and Findings](#results-and-findings)
- [Recommendations](#recommendations)
  
## Project overview
This Data Analysis Project aims to provide  insights into the sales performance of a Telecommunication  company Based in the United State. 

__About the Company__
The Telecommunication Company operates a B2B business model and sells a wide variety of cell phones and devices, including __smartphones__, __tablets__, and __smartwatches__.  They offer devices from all of the major manufacturers, such as Apple, Samsung, Google, and Motorola.

Various aspects of the company’s sales transaction data generated over the past years was  analysed  to gain insights into their Customer Behaviour, Product Popularity, Top Performing  Channel of Marketing, Regional Performance  and Revenue Trends of the company since it began. 

We seek to identify Top performing customers, products, channels of sales , region , trends, and the overall performance of the company , to enable the company to make data-driven decisions/recommendations and to gain a deeper understanding of the company’s overall performance. 

__SALES PERFORMANCE BY CUSTOMERS (CUSTOMER BEHAVIOUR)__ <br> <br>


![customers_behaviour_ss](https://github.com/data-scholar-emma/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/162923747/df7f835f-85e1-44ab-90e3-350ef4ab0d81) <br> <br>



__SALES PERFORMANCE BY CHANNELS__ <br> <br>



![sales_by_channel_ss](https://github.com/data-scholar-emma/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/162923747/b6223cf6-c56f-44ab-b6c3-c7129cf33d45) <br> <br>



__SALES PERFORMANCE BY REGIONS OF BUSINESS OPERATIONS__ <br> <br>



![sales_by_region_ss](https://github.com/data-scholar-emma/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/162923747/f84f0c34-e8c0-4e56-8d45-3b170c39263a) <br> <br>



__SALES TREND OVER THE YEARS__ <br> <br>



![sales_trends_over_the_years](https://github.com/data-scholar-emma/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/162923747/291b54d4-85c9-4ffe-90c5-a2f1a19f7199) <br> <br>




## Data Sources
Sales Transaction Data : The primary dataset used for this data analysis project was sales transaction data, containing detailed information about each sales made by the company , and was extracted from the company’s database using SQL codes. 


Several SQL complex queries were written to the company’s database in order to extract the required data for this  data analysis project. 

Each SQL complex query was used to extract a particular aspect of the company’s sales data. 

The results were downloaded and saved as  the following csv files below:<br> <br> “customers_behaviour.csv” <br> <br>
“revenue_generated_by_channels_all_time.csv” <br> <br>
“revenue_generated_by_region_all_time.csv” <br> <br>
“revenue_trend_over_the_years.csv” <br> <br>

## Data Analysis Tools Used
#### - SQL (PostgreSQL)  
for Data Collection <br> <br>
for Data Cleaning <br> <br>
for Data Analysis

#### - Power BI 
for for Data Modelling <br> <br>
for for Data Analysis <br> <br>
for Data Visualization and <br> <br> 
for Creating an Interactive Report. 

## Data Collection: 
- Database Inspection : In the initial data collection phase , I  inspected the company’s database using SQL code  to check for missing data (NULL) in each of the tables in the company’s database.
- I extracted the  required data for the purpose of the data analysis project using SQL complex query and SQL data aggregation .  
## Data Cleaning and Formatting: 
- I used SQL codes to clean and format the data to conform to the required data format.
- I downloaded the result of my SQL Queries from the company’s database as a csv file to my PC.
  
## Loading Data into Power BI:
- I loaded the downloaded csv files into Power BI for the purpose of Data Visualization and Building interactive dashboard/report.

## Exploratory Data Analysis (EDA): 
EDA involves exploring the sales data in order to answer some key questions such as :
- Who are the top 10 customers of the company ?
- What particular products are the Top customers buying ?  
- What Is the Total quantity of items a particular customer has ever bought from the company ? 
- What is the Total revenue generated by the company from a particular customer ? 
- What is the top selling product ?
- What are the top performing channels of sales ? 
- What is the Total quantity of items sold through a particular channel ?
- What is the  Total Revenue generated  through a particular channel ?
- Which region is the best performing region ? 
- What is the Total quantity of items sold in a particular region ?
- What is the  Total Revenue generated  in a particular region?
- What is the peak sales period ? 
- What is the sales performance at a particular given time (year, month, day) ?  
- What is the sales trend between a particular period of time ? 
- What is the overall sales Trend of the company over the years ? 
- What is the overall sales performance of the company ? 

## Data Analysis
```SQL
/* QUERY 1: SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue generated by each customer  (CUSTOMERS BEHAVIOUR)  */
SELECT a.name AS customers_name,
       SUM(o.smartphones_qty),
       SUM(o.smartwatches_qty),
       SUM(o.tablets_qty),
       SUM(o.total) AS total_quantity,
       SUM(o.total_amt_usd) AS total_revenue_usd
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY customers_name
ORDER BY total_revenue_usd  DESC

/*  QUERY 2 : SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue generated by the company’s various channels of sales (SALES BY CHANNELS)  */

SELECT w.channel AS channel_name,
       SUM(total) AS total_quantity,
       SUM(total_amt_usd) AS total_revenue_usd
FROM  orders o
JOIN accounts a
ON o.account_id=a.id
JOIN web_events w
ON a.id=w.account_id
GROUP BY channel_name
ORDER BY total_revenue_usd DESC


/* QUERY 3 : SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue generated by the company’s various regions of operations (SALES BY REGIONS) */

SELECT r.name AS region_name,
       SUM(o.total) AS total_quantity,
       SUM(o.total_amt_usd)AS total_revenue_usd
FROM orders o
JOIN accounts a
ON a.id = o.account_id
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
GROUP BY region_name
ORDER BY total_revenue_usd DESC

/* QUERY 4 : SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue trend of the company over the years since inception (REVENUE TRENDS OVER THE YEARS)  */

SELECT DATE_TRUNC ('year', occurred_at) AS year,
       SUM(total) AS total_quantity,  
       SUM (total_amt_usd) AS total_revenue_usd
FROM orders
GROUP BY year  
ORDER BY year
```

##  Results and Findings
The Analysis Results is summarised as follows: 
1. The Company’s Top 3  Customers by ranking are : 
 -  1st: EOG Resources : Bought a total of 56,410 items and has generated a Total revenue of  $382,870
 -  2nd: Mosaic :  Bought a total of 49,246 items and has generated a Total revenue of $345,620
 -  3rd: IBM :    Bought a total of 47,506 items and has generated a Total revenue of $326,820
2. The top 10 customers are buying smartphones and smartwatches in almost the same proportion with a slightly higher preference for smartphones.
3. The Overall Top selling product is __smartphones__ , accounting for over __52%__ percent of total sales and Revenue. 
4. The top performing channel of sales is __Direct__ channel  accounting for over __61%__ percent of total total sales and Revenue.
5. The best performing region is the __Northeast__ Region , accounting for over __33%__ percent of total  Sales and Revenue.
6. The company’s sales have been steadily increasing over the past years  with a noticeable peak in the holiday season in  2016, followed by a sudden decline in sales from 2017.  
 
## Recommendations: 
Based on the findings/results of this  data analysis project, I strongly  recommend the following actions : 
1. The company should focus on expanding and promoting the __smartphones__ product category.
2. The company should invest in marketing and promotions during peak sales season to maximise revenue.
3. The company should implement a customer segmentation strategy to target __smartphones and smartwatches customers__ effectively.
4. The company should allocate more budget and resources to their __Direct__ sales channel to maximise revenue.
5. The company should invest more resources  in their __Northeast Region of operation__  to maximise revenue.
6. The Company should restrategize on how to tackle and mitigate the present decline in sales. 
   



