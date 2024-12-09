# Understanding Sales Trends and Customer Behavior to Enhance Marketing Strategies
## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](data-cleaning)
- [Exploratory Data Analysis](exploratory-data-analysis)
- [Data Analysis](data-analysis)
- [Results/Findings](results/findings)
- [Recommendations](recommendations)

Understanding customer behavior and sales trends to make data_driven decisions to enhance marketing strategy. 

### Project Overview
The objective of this data analysis project is to gain insight into customer behavior and sales trends to enhance marketing strategies. This dataset includes demographic information about customers, such as gender and age, as well as their purchasing habits for various electronic products. By analyzing this data, I aim to uncover purchasing patterns and trends throughout the year. Additionally, intend to examine how various factors, such as customer member loyalty status and shipping type, impact purchasing patterns.
### Data Sources 

The primary dataset used for this analysis is the "Customer purchase behavior - Electronic Sales Data" dataset from Kaggle, which can be found here. This data set contains sales transaction records for an electronics company, collected over a one-year period from September 2023 to 2024. It includes demographic information such as gender and age of buyers, as well as details on product types, which encompass various electronics like Smartphones, Laptops, Tablets and smartwatches. 


### Tools

- Excel - Data Cleaning, Pivot Chart 
- SQL Bigquery - Data Analysis
- Tableau - Creating Reports

### Data Cleaning 
In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection. 
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis
EDA involved exploring the sales data to answer key questions, such as:
- What is the trend in total sales over the year?
- How do purchasing patterns vary between loyalty members and non-members?
- What age groups spend the most on electronic products?
- What gender spends the most on electronic products?
- Which electronic products are the most and least purchased? 

### Data Analysis

The Data analysis was done in excel and SQL 

#### Excel
In Excel, I cleaned and transformed the data, ensuring there were no null or outliers.  I also made sure that the column titles were descriptive, concise, and accurate. Additionally, I made pivot tables to better understand the data. The first pivot table I made displayed the distribution between male and female buyers, which was almost equal. Next, I analyzed how many customers opted to be loyal members. The distribution of this showed that approximately 22% of customers were members while 78% were not members. Lastly, I reviewed the total amount of purchased electronic products and the corresponding amount of instances an add-on was purchased. I summarized the total purchases and add-ons in a pivot chart. The results of these are illustrated in the bar charts below. The bar chart illustrates the product with the most purchases were smartphones, which also had the most instances of add-ons purchased. Headphones were the least bought product and, unsurprisingly, they were also the product with the least amount of add_ons purchased. 
<img width="367" alt="member count" src="https://github.com/user-attachments/assets/93b7a356-9535-4d3d-979c-d13faa19b552">
<img width="471" alt="Add-ons " src="https://github.com/user-attachments/assets/ee5cafe0-7ea9-4bcd-a283-578ae8f4929b">

### SQL 
After I cleaned the data in excel, I uploaded the Electronic Sales data into bigquery to do explorataroy data analysis. 

The first query I made was to see the total quantity of each product type purchased by male and female customers. I started off by selecting the product_type to select the type of product from the table. Then I used a CASE statement to sum the quatitiy of entries if the is 'Male'. I did the same for women. I used GROUP BY product type to group the the results byt the product type. This made sure that the aggregated operations were performed seperately for each product type. I finally sorted this result alphabetically by the product type. This provided important insight into what types of electronics each gender is most and least likely to spend their money on.

``` SQL
SELECT
    product_type,
    SUM(CASE WHEN gender = 'Male' THEN quantity ELSE 0 END) AS Male_Purchases,
    SUM(CASE WHEN gender = 'Female' THEN quantity ELSE 0 END) AS Female_Purchases
FROM
    stunning-lambda-442403-k6.sales_data.digital_sales_date
GROUP BY
    product_type
ORDER BY
    product_type;
```
This next query is to see the units purchsed per age group. I started by using a CASE WHEN categorize the customers age into groups based on their age. The age groups I made were for teens, 20-29, 30-39, 40-49, 50-59, 60-69, 70-80. SUM(quantity) was used to sum the total quantity of units purchased per age group. This was then given the alias of 'Units-Purchased'. I then counted the number of custumers in each age group by counting the number of times a customer_id showed up and using Distinct to only count each number once. After that, I calculated the average total price of purchases for each age group and used ROUND to round two decimal points. Lastly, I counted the number instances when add-ons were purchased by each age group and aliased this as "Add-ons_purchased". I used Group by to group the first column, which was age. 

```SQL
SELECT CASE 
WHEN age <20 THEN 'Teens'
WHEN age >= 20 AND age < 30 THEN '20_Year_olds'
WHEN age >= 30 AND age < 40 THEN '30_Year_olds'
WHEN age >= 40 AND age < 50 THEN '40_Year_olds'
WHEN age >= 50 AND age < 60 THEN '50_Year_olds'
WHEN age >= 60 AND age < 70 THEN '60_Year_olds'
WHEN age >= 70 AND age <= 80 THEN '70_Year_olds'
END AS Age, SUM(quantity) AS Units_Purchased, COUNT(DISTINCT customer_id) AS total_customers, ROUND(AVG(Total_price),2) AS Average_Purchased_Price, COUNT(Add_ons_Purchased) AS Add_ons_Purchased
FROM stunning-lambda-442403-k6.sales_data.digital_sales_date
GROUP BY 1
ORDER BY 1;
```
I then wanted to analyze the total sales data per month to identiy peak sales periods. I first need to extract the month from the purchase date and and assign a month name to each eow based on the month value. I did this using CASE WHEN EXTRACT and named this column 'month-name. Then I used SUM(quanity) to sum the quanityt of units purchased. To get total price of transactions foe each month I  summed the total price and rounded 2 decimal places. This was then given the alias of 'Total_transaction_sum'. Lastly, i calculated the average total prive of the total price of transactions and rounded it two decimal points. Using GROUP BY to group the month-name, I was able to group the results by the month column. This query helped me understand the sales trends on a monthly basis. 

``` SQL
SELECT 
    CASE 
      WHEN EXTRACT(Month FROM purchase_date) = 1 THEN 'January'
      WHEN EXTRACT(Month FROM purchase_date) = 2 THEN 'February'
      WHEN EXTRACT(Month FROM purchase_date) = 3 THEN 'March'
      WHEN EXTRACT(Month FROM purchase_date) = 4 THEN 'April'
      WHEN EXTRACT(Month FROM purchase_date) = 5 THEN 'May'
      WHEN EXTRACT(Month FROM purchase_date) = 6 THEN 'June'
      WHEN EXTRACT(Month FROM purchase_date) = 7 THEN 'July'
      WHEN EXTRACT(Month FROM purchase_date) = 8 THEN 'August'
      WHEN EXTRACT(Month FROM purchase_date) = 9 THEN 'September'
      WHEN EXTRACT(Month FROM purchase_date) = 10 THEN 'October'
      WHEN EXTRACT(Month FROM purchase_date) = 11 THEN 'November'
      WHEN EXTRACT(Month FROM purchase_date) = 12 THEN 'December'
      ELSE 'Unknown'
    END AS month_name, SUM(quantity) AS Total_Number_units_purchased, Round(SUM(Total_price),2) AS Total_Transaction_Sum, Round(AVG(total_price),2) AS Average_Transaction_Price
FROM stunning-lambda-442403-k6.sales_data.digital_sales_date
GROUP BY 1
ORDER BY 1;
```
Lastly, I wanted to see the quantity of purchases each electronic type had per month. I first made a CTE so we can refrence the month names, which were extracted from the purchase date, and given the correponding month name. In the main query, I selected the month name and gave it the alias 'Month'. Then I calculated the total quantity for each product type. For example, in "SUM(CASE WHEN product-type = 'Smartphone' THEN quantity ELSE 0 END) AS smartphone" I used SUM to sum the quantity of smartphones sold if the product type was 'smartphone'. I did the same for the rest of the electronic products. I used GROUP BY to aggreated the quantites for each product type within each month. This query provided me with a clear view of the quantity of products sold each month for each product type, alloqing me to analyze sales trends over time for each product.  
``` SQL
WITH Months AS (
  SELECT 
    EXTRACT(Month FROM purchase_date) AS month_num,
    CASE 
      WHEN EXTRACT(Month FROM purchase_date) = 1 THEN 'January'
      WHEN EXTRACT(Month FROM purchase_date) = 2 THEN 'February'
      WHEN EXTRACT(Month FROM purchase_date) = 3 THEN 'March'
      WHEN EXTRACT(Month FROM purchase_date) = 4 THEN 'April'
      WHEN EXTRACT(Month FROM purchase_date) = 5 THEN 'May'
      WHEN EXTRACT(Month FROM purchase_date) = 6 THEN 'June'
      WHEN EXTRACT(Month FROM purchase_date) = 7 THEN 'July'
      WHEN EXTRACT(Month FROM purchase_date) = 8 THEN 'August'
      WHEN EXTRACT(Month FROM purchase_date) = 9 THEN 'September'
      WHEN EXTRACT(Month FROM purchase_date) = 10 THEN 'October'
      WHEN EXTRACT(Month FROM purchase_date) = 11 THEN 'November'
      WHEN EXTRACT(Month FROM purchase_date) = 12 THEN 'December'
      ELSE 'Unknown'
    END AS month_name,
    product_type,
    quantity
  FROM stunning-lambda-442403-k6.sales_data.digital_sales_date
)
SELECT 
  month_name AS Months,
  SUM(CASE WHEN product_type = 'Smartphone' THEN quantity ELSE 0 END) AS Smartphone, 
  SUM(CASE WHEN product_type = 'Smartwatch' THEN quantity ELSE 0 END) AS Smartwatch,
  SUM(CASE WHEN product_type = 'Tablet' THEN quantity ELSE 0 END) AS Tablet,
  SUM(CASE WHEN product_type = 'Laptop' THEN quantity ELSE 0 END) AS Laptop,
  SUM(CASE WHEN product_type = 'Headphones' THEN quantity ELSE 0 END) AS Headphones
FROM Months
GROUP BY month_num, month_name
ORDER BY month_num;
```
### Results/Findings

The analysis results are summarized as follows:
1. In this bar chart, we can see the quantiy of each product bought by each gender. First, I wanted to see the distribution of genders. By counting the total number of male and female customers, I was able to make a pie chart showing the distribution. We can see in the pie chart labled "Gender" that there are slighly more males than males, but the difference is very small. With this in mind I made the bar chart titled "Quantity of Prdicts Bought by Gender". We can see that the Y-axis list the numerical number of products bought. The Y axis relays the product type and the purchase made by each gender. We can see that males have consistily bought more quantities of each product. This can be explained by the slightly higher number of male customers. It is clear that men and women in this database have similar purchasing habits. The most popular product bough are smartphones and the least popular electronic are headphones for both genders.
<img width="400" alt="Electronic_1" src="https://github.com/user-attachments/assets/49b44136-4339-470c-b458-f5315040b9d7">
<img width="305" alt="gender" src="https://github.com/user-attachments/assets/fc7849e8-d8d1-491c-95fe-cd91049bf4a7">

2. The "Total Units Purchased per Age Group" bar cahrt dispalays the units purchased per customers grouped by age group. As previously stated, the age groups are teens, 20-29, 30-39, 40-49, 50-59, 60-69, 70-80. In this distribution we can see the teens bar is drastically shorter than the rest of the age groups. This can be explained because the teens age group starts at 18 years old and only includes 18 and 19 year olds. This means that there are significanly less custumers for this age range. We can also see the bar with the most units purchased is the 70s age group. One thing we have to keep in mind for this age group is that it includes 1 additional age that the other age groups do not have. This is because the age group starts at 70 and includes 80 instead of it stopping at 79. Even though we have slighly more customers in this age group, the difference between it and the other bars is not huge. We can rule out any age group from being significant outliers in the number of units purchased. 
<img width="798" alt="Electronic_2" src="https://github.com/user-attachments/assets/5a19eea2-9bea-44be-96e8-37ba04a15bde">

3. In the "Total Dollar Amount Purchased per Month chart" I analyzed the total transaction amount in dollars per month. We can we that there is a very clear dip in the total transaction amount for the last quarter of the month, starting in slighly dipping in September and plummeting in October. This downturn stays consistent from October to December. Since the time period for this data is from September 2023 to September 2024, we know the January bar immediatly precedes the December data. This means that there is an unexpected and drastic increase of transaction activity from one month to the other. The downturn of activity from October to December is also very odd and unexpected. These months are consistenly associated with higher spending due to holidays like Christmas and events like black Friday. Apart from this there seem to be no other significant outliers in the total transaction amount per month in this dataset.
<img width="403" alt="Electronic_3" src="https://github.com/user-attachments/assets/1944511f-f255-4062-aaa7-18591e593505">

4. The last graph I made in Tableau was the "Quantity of Electronics Purchased per Month". This graph is useful to determine product sales performace over time. The bar graph covers all 12 month of the sales data starting in January. For each month it also list each product type and the total units sold for that product in that month. We can see that smartphones are the best selling product for each month and headphones have the least amount of sales consistently. With headphones, we can also see that there is a very sharp decline in the quantity sold starting in october. This decline can be seen for the rest of the product types as well, but not as drastic as with headphones. Headphone sales essentailly stop in the last quarter of the month. Although headphones have the most drasctic change, we can see there is a significant drop in sales for the other products as well. I intially thought this change could be caused by faulty products and poor customer satisfaction. I decided to take a look at the rating for each of these products. When I graphed the average star rating for these products I saw that apart from smartphone having the highest rating, all other rating were the same. If there had been a sudden decline in the quality of the product, I would expect to see this in the rating. I specially would expect to see the rating for headphones to go since no sales were made in 3 months. This tells me it was not an issue with the customer satisfaction of the product. Next I suspected that the problem might lay in problems that come up after equipment is purchased. I graphed the completed and implete orders in the chart labeled "Cpm[leted and Canceled Order per Month". I suspected that there would be an increase in imcomplete orders for the last quarter of the year. Althouth order quantitiy decreased, as expected, the completed and incomplete order ration stayed the same. It is not clear why this plummet in sales is so sudden but it could do with supply chain issues.
<img width="353" alt="rating" src="https://github.com/user-attachments/assets/e651fd45-ad47-456c-9ef0-46d002ce23c0">
<img width="987" alt="Electronic_4" src="https://github.com/user-attachments/assets/5a28bf7e-0125-4267-99a9-d463a2937198">
<img width="707" alt="completed orders" src="https://github.com/user-attachments/assets/6daf0b99-b7d5-4640-9a57-8fe755a00e85">

### Recommendations 
Based on the results/ findings there are a few things that stand out.

- Age-Based insights: One thing we can try to add are age based ads and promotions. An example of these promotions are ads for student discounts for teens and young adults. This would increase the amount purchased by teens and people in their 20s. Another age based promotions is a senior discount. We can also promote certain products for certain age groups. This can look like promoting cell phones for older adults so that they can communicate with friends and family and tablets to help with school work for teens and yound adults
- Monthly sales: Since it looks like there are less than desired sales in the last quarter of the month, we can run promotions to encourage shopping. These limited time discounts can center around black friday, christmas and new years to boost sales during these typically high spending months.
      - It is also important to investigate and address the reason there are low sales in the last quarter. Based on the the current data we are given, there is no clear reason as to why sales would be so low. This could be do to supply chain issues. This would need to be resolved to ensure popular products are well stocked during this peak shopping period.
- Product Specific Strategies: Another thing we can implement is targeted campaigns highlighting low performing products. For example, we can highlihgt the unique and usefule feaures our headphones would provide. We can also consider making bundles with more popular items or offering discounts to promote sales. 
    




