<img style="float: centre;"  src="https://www.erpcall.com/images/ecommerce.png" width="400"/>

# E-commerce Solutions - A Python approach
*Yazan Masarweh*

## Content
- [Project Description](#project-description)
- [Questions](#questions)
- [Dataset](#dataset)
- [Cleaning](#cleaning)
- [Analysis](#analysis)
- [Conclusions](#conclusions)
- [Future Work](#future-work)
- [Workflow](#workflow)
- [Repo structure](#repo-structure)

## Project Description
This project revolves around providing an A-Z Business Intelligence solution to an E-commerce company (applicable to any product/service providing company).

The idea is that our client, in this case an E-commerce company with headquarters in the United Kingdom, approached us in order to help them identify key drivers of growth and provide capacity management and planning based on their historical transactional data.

What we provide is a complete overview of the client's main revenue and overall growth drivers. The analyses are split into different overall themes:
- [x]  **Data cleaning**: A general study of the historical data available and cleaning the data for analysis
- [x] **Exploratory Data Analysis (EDA)**: Aims to appraoch the data from both a qualitative and a quantitative approach for main insights
- [x] **Monthly churn rate and Cohort Analysis**: Aims to identify monthly churn rates and performance measurement through customer cohort analysis on retention rates
- [x] **Customer segmentation with RFM and Machine Learning**: A look into the different customers to segment through RFM and K-Means to prioritise resrouces 
- [x] **Customer Lifetime Value calculation and prediction**: Trying to understand low to high value customers based on their lifetime value and attempting to predict any given customer CLTV based on a set timeframe

The purpose is to provide the E-commerce company with insights in resource management in order to retain existing customers and acquire new ones boosting growth and overall revenues.

## Questions
The purpose of this project is to go in depth into the company's transactions and revenues. This type of approach gives us a plethora of questions to tackle. These can be:

1. Where does your revenue come from?
2. Who is reponsible for the biggest amount of total revenue?
3. Who is responsible for the most number of orders?
4. Which customers are most valuable to your company's growth?
5. How to segment customers based on their historical transactions?
6. How are you performing when it comes to monthly churn rates?
7. How are you performing in your marketing and resource management by customer cohort?
8. Are new or existing customers what make up your revenues?
9. Is there any seasoanlity related transactions? Can they be monetised even further?

The application of the above questions is a generic one in the sense it can be applied over a number of varying company profiles. This is an obvious advantage as the answers to the above questions is something every company should aim to answer.

## Dataset
The dataset is acquired online through the use of [Kaggle](https://www.kaggle.com/).

The **raw** dataset comprises of:
- 541909 records and 8 columns
- The size of the dataset is approximately 46MB

Some of the important questions that cannot be answered are ones associated to cost and hence profit. Moreover, the historical data is only for a duration of ~1 year and therefore seasonality related questions are accompanied with assumptions to back them up.

The raw csv dataset can be found in my [github repo](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/datasets/e_commerce_raw.csv)

## Cleaning
[code](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/code/1_e_commerce_data_cleaning.ipynb)

The cleaning process starts off with having a look at the data types and records available in the dataset.
Data types are as follows:

field         | type
------------- | -------------
InvoiceNo     | object
StockCode     | object
Description   | object
Quantity      | int64
InvoiceDate   | object
UnitPrice     | float64
CustomerID    | float64
Country       | object

We should see if there are some missing values. But before that we rename the columns in a consistent manner.

Identifying null values:

field         | null_values
------------- | -------------
invoice_no    | 0
stock_code    | 0
description   | **1454**
quantity      | 0
invoice_date  | 0
unit_price    | 0
customer_id   | **135080**
country       | 0

Based on our proposed questions, identifying the customers behind a specific order is key and therefore dropping null value was the correct apporach.

field         | value_count
------------- | -------------
invoice_no    | 406829
stock_code    | 406829
description   | 406829
quantity      | 406829
invoice_date  | 406829
unit_price    | 406829
customer_id   | 406829
country       | 406829

Using the .describe() fucntion, we are to able to identify **negative quantities and unit prices equal to zero**. With no explanation on why these exist, we drop such records. This results in our dataset having a shape of **(397884, 8)**.

Moreover, we apply some data type changes such as:
- invoice_date :point_right: datetime
- customer_id :point_right: string

Concerning outliers, we keep all remaining records since we do want to include the outliers when it comes to total quantity or total unit price.

## Analysis
* Overview the general steps you went through to analyze your data in order to test your hypothesis.
* Document each step of your data exploration and analysis.
* Include charts to demonstrate the effect of your work.
* If you used Machine Learning in your final project, describe your feature selection process.


As per the project description, the work, after data cleaning, is divided as follows:
- [x] **Exploratory Data Analysis (EDA)**
- [x] **Monthly churn rate and Cohort Analysis**
- [x] **Customer segmentation with RFM and Machine Learning**
- [x] **Customer Lifetime Value calculation and prediction** 


### Exploratory Data Analysis (EDA)
[code](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/code/2_e_commerce_EDA.ipynb)

Exploratory Data Analysis refers to the critical process of performing initial investigations on data so as to discover patterns,to spot anomalies,to test hypothesis and to check assumptions with the help of summary statistics and graphical representations.

Here we aim to apply EDA to:
1. Maximize insight into a data set;
2. Uncover underlying structure;
3. Extract important variables;
4. Detect outliers and anomalies;
5. Test underlying assumptions

#### Transactions by country
Here we will have a more in depth look at orders and revenue by country. This, even though straight forward, gives us a clear starting point on where the efforts of the client should be directed or rather *redirected*.

We decide to include and exclude the United Kingdom in our EDA as the company's headquarters are in the United Kingdom and hence it will most probably provide the highest revenue and total order quantities.

##### Total order and revenue by country (Including the United Kingdom):

<img src="/images/charts/total_revenue_by_country.png" alt="total_revenue_by_country"/>

---- 

<img src="/images/charts/total_orders_by_country.png" alt="total_orders_by_country"/>

As expected, we can clearly see that there is a bias toward the United Kingdom given this retailer is based in the United Kingdom.

Here we see that the top five countries in terms of **revenue volumn** are:
1. United Kingdom
2. Netherlands
3. EIRE (Ireland)
4. Germany
5. France

Here we see that the top five countries in terms of **order volumn** are:
1. United Kingdom
2. Germany
3. France
4. EIRE
5. Spain

##### Total revenue by country (Excluding the United Kingdom):

<img src="/images/charts/total_revenue_by_country_exc_uk.png" alt="total_revenue_by_country_exc_uk"/>

---- 

<img src="/images/charts/total_orders_by_country_exc_uk.png" alt="total_orders_by_country_exc_uk"/>

This gives a better look at the countries outside of the UK where the client's main revenue comes from.
The top five countries in terms of **revenue volumn** are:
1. Netherlands
2. EIRE (Ireland)
3. Germany
4. France
5. Australia

---- 

#### A look into seasonality
Here we try and analyse if there are certain patterns when it comes to order and revenue over time.

##### Orders and Revenue by year_month:
We take a look at the absolute numbers of total orders and total revenue over the given timeframe in order to get a sense for the growth of the company in general. Are they making more revenue? Are they selling more units?

<img src="/images/charts/total_orders_by_year_month.png" alt="total_orders_by_year_month"/>

We can see from the above multi-line chart that overall, both total orders and revenue are increasing with time. There are some noticeable dips that we need to look into further such as 2011-04 to identify why this may be. Moreover, there are steeper growths after 2011-08 which should be also considered.

##### Orders and Revenue by day:

<img src="/images/charts/total_orders_by_day.png" alt="total_orders_by_day"/>

We can take two inputs from the above chart:
- The number of total orders and revenue tend to increase from Monday until Thursday
- There are no orders on Saturdays? Why is this? Potential increase in revenue stream

##### Orders and Revenue by hour:
We take a look at the absolute numbers of total orders and total revenue over the given timeframe by hour of the day in order to identify best times of the day where total orders and revenue come from.

This is quite important when it comes to capacity management of the company's resources.

<img src="/images/charts/total_orders_by_hour.png" alt="total_orders_by_hour"/>

It does not come to anyones surprise that total orders and revenie adopt a normal distribution throughout the day's cycle.

On the other hand it is important to note that the highest peak in both orders and revenue comes on 12:00 where all hands on deck should be available plus and minus 2 hours i.e. **10:00 - 14:00**.

---- 

#### A look into seasonality by country (Excluding the United Kingdom)
Taking incto account only the top five countries by total order as previously identified, we can dig a little deeper into their performance over time.

<img src="/images/charts/orders_by_country_by_year_month_exc_uk.png" alt="orders_by_country_by_time_exc_uk"/>

----

<img src="/images/charts/revenue_by_country_by_year_month_exc_uk.png" alt="revenue_by_country_by_time_exc_uk"/>

We tend to notice a growth in total orders in France, Germany, and Ireland while Spain and the Netherlands are stagnant with noticeable dips in total orders. These dips are further amplified when we look at revenue by said countries.

What happened to customers from the Netherlands in April and July?

From this we are able to allocate resources to the client's customer service team by country accordingly.

Looking at the same countries but switching our focus on hour of the day we get the following chart:

<img src="/images/charts/orders_by_country_by_hour_exc_uk.png" alt="orders_by_country_by_hour_exc_uk"/>

---- 

#### Growth Rates
After studying absolute numbers of revenue and orders we should direct our attention to percantage change over times i.e. growth rates.

##### Order and Revenue growth rate:

<img src="/images/charts/revenue_growth_rate.png" alt="revenue_growth_rate"/>

----

<img src="/images/charts/order_growth_rate.png" alt="order_growth_rate"/>


Overall, when it comes to growth rates we see a positive increase overall over the duration of our data but there are some considerable dips througout. 

Why is this?

Are the dips in revenue and total order growth related to number of active customers?

##### Active customer growth rate:
The total number of unique customer making purchases per month

<img src="/images/charts/customer_growth_rate.png" alt="customer_growth_rate"/>

As expected, dips in revenue and total orders are associated with dips in customer activity on the same months.

<img src="/images/charts/overall_growth_rate.png" alt="overall_growth_rate"/>

----

#### New vs. Existing customers
From the above metrics we can see that revenue growth was associated with number of active customers and their associated orders.

We can take a deeper look into those metrics by trying to separate customers into 'New' and 'Existing' in order to identify if the company is good in attracting new customers and retaining existing ones.

From this we can better understand where the marketing resources should be focused.

First we need to define what is a ***new customer*** and what is an ***existing customer***.

***NEW CUSTOMER***: A customer is classified as *new* if his minimum invoice_year_month date is equal to current invoice_year_month

***EXISTING CUSTOMER***: A customer is classified as *existing* if his minimum invoice_year_month date is less than the current invoice_year_month

##### Revenue by custmor type:
After applying dataframe manipulation based on the baove definitions we can plot revenue by said customer types:

<img src="/images/charts/revenue_by_customer_type.png" alt="revenue_by_customer_type"/>

We can clearly see that 'Existing' customers are growing positively with time unlike 'New' customers which sees a plateau in growth or even a small negative growth. Why?

Does the client need better marketing efforts to be put in place?

----

### Cohort analysis - Customer Retention and Average Revenue
[code](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/code/3_e_commerce_cohort_analysis_and_churn.ipynb)

One of the most important analyses any customer oriented company should consider is called *'Cohort Analaysis'*.

Cohort analysis overview:

A cohort is a group of people who share a common characteristic over a certain period of time.

In our case, our cohorts are going to be customers that purchased their first item within a given year_month i.e. we will group customers into cohorts based on their first purchase date.

Refer to this [article](https://medium.com/analytics-for-humans/a-beginners-guide-to-cohort-analysis-the-most-actionable-and-underrated-report-on-google-c0797d826bf4) for further reading

##### Cohort analysis on customer retention rate:
By manipulating our initial dataframe, please refer to the code [here](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/code/3_e_commerce_cohort_analysis_and_churn.ipynb), we are able to convert the dataframe into absolute customer retention over time and then into retention rates. Our cohort analysis that is spread over 13 periods (each of 1 month starting on period 2) looks as follows:

<img src="/images/charts/cohort_analysis_retention.png" alt="cohort_analysis_retention"/>

Approximately 50% of all customers from 2010-12 cohort return after 11 months (12 periods). This would mean that there needs to be an eye out for any changes the company might have implemented that caused such a spike in the rate.

Moreover, 2011-11 sees a sharp drop ~89% in period 2 which should be considered a red flag and must be investigated.

##### Cohort analysis on average revenue:
Similar to the above analysis, we apply cohort analysis on average revenue by period by cohort

<img src="/images/charts/cohort_analysis_revenue.png" alt="cohort_analysis_revenue"/>

We can see that there is a decline in sales as the heat map moves outward to a lighter color green. Moreover, there seems to be an anamoly on cohort 2011-05 period 8 that requires further investigation. Buik buyer? One off purchase?

This type of analyses offers great insights into the performance of the company with time and can be further tweaked to allow for filtering using countries of orders, by day of the week, by hours of the day and so on.

----

### Customer Segmentation with RFM and K-Means
[code](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/code/4_e_commerce_RFM_segmentation.ipynb)

Customer Segmentation comes as one of the most important actions companies should address when they deal with a large customer base. From what we saw earlier we deduced many inisghts about our customer base as a whole but there is still much more to be done.

Customers are not the same and therefore should not be treated the same especially when the company's precious resources are on the line.

One of the most popular customer segmentation methods is RFM.

#### RFM

RFM stands for:
- **Recency**: *When was the last time a customer purchased anything from us?*
- **Frequency**: *How often does a customer purchase from us?*
- **Monetary**: *How much money does a customer spend on us?*

##### Recency
How do we calculate a customer's *recency*?

Well, as per the definition above, we are looking for the last time a purchase was made from the most recent date we have which is 2011-12-09.

Therefore, we need to calculate the number of days of each purchase from this max date.

After this is down, we apply K-means to create a recency_cluster of customers.

<img src="/images/charts/recency_elbow_k_means.png" alt="recency_elbow_k_means"/>

From the elbow method graph, we can tel that the optimum number of clusters would be 3 (+-1). We choose 3.

Description of the recency clusters below:

<img src="/images/tables/recency_cluster_describe.png" alt="recency_cluster_describe"/>

##### Frequency & Monetary:
We follow the same idea as recency based on our definition with K-means we cluster to the following:

<img src="/images/tables/frequency_cluster_describe.png" alt="frequency_cluster_describe"/>

----

<img src="/images/tables/monetary_cluster_describe.png" alt="monetary_cluster_describe"/>

##### Main cluster based on highest cluster value:
We need to create one cluster based on the three different cluster types in order to give high/ value to customers.

High value would be a customer that has low recency, high frequency, and high monetary.

For this, our main cluster would be the sum of the cluster number based on the values mentioned above. The cluster numbers already denote the value associated with each.

<img src="/images/tables/main_cluster.png" alt="main_cluster"/>

We can see that cluster 15 has the most valuable customers while cluster 9 has the lowest value customers.

As per the distribution of customers based on the values of the main cluster above, we can simplify it by segmenting customers to low, medium, and high value.

##### Plot RFM segments:

<img src="/images/charts/recency_frequency_scatter.png" alt="recency_frequency_scatter"/>
<img src="/images/charts/recency_revenue_scatter.png" alt="recency_revenue_scatter"/>
<img src="/images/charts/frequency_revenue_scatter.png" alt="recency_frequency_scatter"/>

The scatter plots clearly differentiates the assigned customer segments and reinforces the used method to segment.

From here the company can leverage their strengths based on customer segments. For example, low value customers can be targeted to increase their frequency while medium to high value customers can be targeted to improve retention.

----

### Customer Lifetime Value (CLTV)
[code](https://github.com/Yazfm/Project-Week-8-Final-Project/blob/master/code/5_e_commerce_CLTV.ipynb)

Customer Lifetime Value (CLTV) is one of the most important metrics any company can obtain. In a nutshell, it represents the total amount of money a customer is expected to spend in your business, or on your products, during their lifetime. This is an important figure to know because it helps you make decisions about how much money to invest in acquiring new customers and retaining existing ones.

You can read more about CLTV in the following two links:
- [link_1](https://www.shopify.com/encyclopedia/customer-lifetime-value-clv) 
- [link_2](https://towardsdatascience.com/measuring-users-with-customer-lifetime-value-cltv-94fccb4e532e)

Over simplifying CLTV equation can be as follows:
- **TOTAL REVENUE** *minus* **TOTAL COSTS**

This has to be applied over a specific period of time tha we define in order to calculate. For example, we can asses the CLTV of a customer over a 6 month period in order to give us some historical data about a customer CLTV.

From there we could train a ML model to predict said customer's CLTV accordingly.

#### Feature identification
One, if not the most, important aspect of predicting our CLTV would be identifying the features that we should use to train and predict our model.

In our case, we have already segmented our customer baswed using RFM to shed light on thier associated values and therefore we are going to utilise them as our features.

According to this [article](https://towardsdatascience.com/data-driven-growth-with-python-part-3-customer-lifetime-value-prediction-6017802f2e0f) that helped pave the way for this calculation, we have to split our dataset into two parts:

- One dataframe that houses unique customer_ids and their associated clusters based on a 3 month period
- Another dataframe that houses the revenue of each customer over a 6 month period

One thing to keep in mind is that our data has to be chronological and therefore must be sorted accordingly.

From the dataframe we transformed with the same RFM segmentation before we get a dataframe of 3 months of transactions from 01-01-2011 to 01-04-2011

<img src="/images/tables/CLTV_dataframe.png" alt="CLTV_dataframe"/>


##### K-Means & CLTV
As mentioned earlier, CLTV involves cost calculations but in our dataset that is missing. Therefore we can use revenue as our LTV indicator.

We understand that CLTV should return a numerical value that represents, in this case, how much revenue a specific customer will contribute to the company. But since this porojects revolves around providing actionable intelligence in order to allocate resources and observe customer behaviour, we will resort to segmenting the CLTV using K-Means.

We use 3 clusters to simplify our approach.

<img src="/images/tables/CLTV_cluster_describe.png" alt="CLTV_cluster_describe"/>

We can see that CLTV cluster '0' has the lowest mean LTV and therefore would be our lowest priority while cluster '2' has the highest.

#### Feature engineering and correlation
By reveiwing the following [article](https://towardsdatascience.com/feature-engineering-for-machine-learning-3a5e293a5114) we can understand the great emphasis on correct feature engineering.

**One-hot encoding** will be our method of choice since our features are categorical.

According to the aforementioned article:

"*This method changes your categorical data, which is challenging to understand for algorithms, to a numerical format and enables you to group your categorical data without losing any information.*"


 We should try and understand which features correlate more with our CLTV_cluster.
 
 <img src="/images/charts/feature_correlation.png" alt="feature_correlation"/>
 
 #### Model: Random Forrest Regressor
This [article](https://www.kdd.org/kdd2016/papers/files/adf0755-vanderveldAbr.pdf) explains in detail the top level approach taken here.

 <img src="/images/tables/random_forrest.png" alt="random_forrest"/>

Referring to our mean r2_test scores we can see that we achieve an accuracy close to 83% which is quite high for what we are trying to achieve. This might seem to be a good model but we need to investigate a little further.

Looking at our CLTV cluster, we can see that around 99% of all our customers fall under cluster '0' which made our current model not a valid one.

----

## Conclusions

Conclusions can be segregated based on the structure proposed in the [project description].

EDA:
- The United Kingdom accounts for most revenue and total orders
- Outside of the United Kingdom, the Netherlands, Ireland, Germany, France, and Australia bring in the highest revenue respectively
- Absolute total orders and revenue see a positive growth overall peaking in 2011-11
- Weekdays with the highest absolute total orders and revenue are Thursdays while there are no orders on Saturdays
- Overall, distribution of all order and revenue over the day see a normal distribution between the hours of 06:00 and 20:00 peaking at around 12:00
- The Netherlands, bringing the most revenues, experienced *significant* dips in revenue in 2011-04 and 2011-07
- Total order and revenue growth rates (pct change over previous month) shows a decline (-ve growth) in 2011-04, and 2011-06 & 2011-07
- The client is monetising 'Existing' customers better thwn 'New' ones with revenues growth for the latter being slightly negative
- Cohort analysis on retention rates shows the overall performance to be somewhat lacking but there is a significant increase in retention rates of 50% of customer cohort 2010-12 in period 12 (12 months later). Better investigate marketing efforts
- Cohort analysis on avergae revenue shows the same behaviour as retention rates with a noticeable increase in period 8 of cohort 2011-05. This needs to be investigated as it might be either a boost in sales or a financial reporting error
- Segmenting customer with RFM and applying mean scores on recency, frequency and monetary we get the following:

main cluster | recency | frequency | revenue | segment      
------------ | ------- | --------- |-------- |--------
9            | 153     | 39        | 740     | low_value
10           | 292     | 25        | 483     | low_value
11           | 33      | 74        | 1564    | med_value
12           | 13      | 466       | 7710    | med_value
13           | 6       | 932       | 76327   | high_value
14           | 2       | 3400      | 145715  | high_value
15           | 0       | 5675      | 143825  | high_value

- From the above segment we can direct the client's resources based on customer value for example:
    - low_value: Increase frequency
    - med_value: Improve retention + Increase frequency
    - high_value: Improve retention

- CLTV calculation requires more data input and different model tryout. With costs information and more historical data we are confident on being able to calculate it with a high degree of accuracy

## Future Work
Address any questions you were unable to answer, or any next steps or future extensions to your project.

There are various missing information that could be very useful for any type of business intelligence on this datasets. 

Missing datapoints could be:
- More histroical data
- Product categories
- Associated costs of each product / category
- Finiacial statements to asses GEI

More country oriented analysis to develop different strategies based on country of origin and product categories.

Involve machine learning in the analytical process and client's resource allocation. These can range from:
- Dynamic pricing models based on customer attributes such as product ytypes, total orders, country of origin, transaction dates, etc.
- CLTV prediction based on various ML algorithms.
- Product recommndation models


## Workflow
Outline the workflow you used in your project. What were the steps?

First of, the idea was to apply and provide actionable Business Intelligence to an E-commerce / Saas company. Therefore the first step was to identify what kind of solutions we can provide by asking questions that every company (regardless e-commerce or Saas) would always want to answer or get insights on.

After that looking for suitable datasets proved to be a challenge as there ar not many publice data on sales and/or revenue of online retailers and/or Saas companies. Finally and thanks to [Kaggle](https://www.kaggle.com/) narrowed it down to a dataset of an online retailer based in the UK.

Data cleaning and then the structure proposed in the [project description](#project-description) followed. Referring to numerous articles online and with trial and error, charts and tables began to take shape and from the EDA insights were starting ot be compiled.

From there, cohort analysis and retention rates were the natural next step as they are the bread and butter of any retailer/Saas company when it comes to revenue growth and depolying resources effectively.

Segmentation using RFM was very informative as it can always give you a fast strategy of customer attention based on customer perceived value.

Last but not least, CLTV prediction which provied to be a challenge as the dataset did not provide a good prediction accuracy nor does it offer an advantage.

## Repo structure
What does your repository look like? Explain your folder and file structure.

My repo has the following folders and structure:
1. code:
    1. 1_e_commerce_data_cleaning.ipynb
    2. 2_e_commerce_EDA.ipynb
    3. 3_e_commerce_cohort_analysis_and_churn.ipynb
    4. 4_e_commerce_RFM_segmentation.ipynb
    5. 5_e_commerce_CLTV.ipynb
2. datasets:
    1. e_commerce_raw.csv *(original dataset from kaggle)*
    2. e_commerce_clean_non_null.csv *(cleaned dataset with no null values)*
    3. e_commerce_add_revenue.csv *(added revenue column to cleaned dataset)*
    4. e_commerce_add_customer_types.csv *(added customer type to cleaned dataset)*
    5. growth_rates_by_year_month.csv *(grouped growth rates and absolute totals by year_month)*
3. images:
    1. charts *(folder containing all charts)*
    2. tables *(folder containing all table screenshots)*
4. This README file
5. .gitignore file
  
