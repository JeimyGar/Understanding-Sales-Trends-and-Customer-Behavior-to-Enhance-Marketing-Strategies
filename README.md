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
The objective of this data analysis to gain insight into cusotmer behavior and sales trends to engance marketing stratefies. This data set includes demographic informarion about the suctomre such as gender and age as well as their pruchasing habits dor varous electonics products. By analysizing this data, I intend to unvoer purchasing patters and trends for the customers throught the year. I also intedn to see how various factors, such as customer member loyalty staus and shipping type impact purchasing patterns. 
### Data Sources 

Electronic sales: The primary dataset used for this analysis is the "Customer purchase behavior - Electronic Sales Data" from Kaggle that can be found [here](https://www.kaggle.com/datasets/cameronseamons/electronic-sales-sep2023-sep2024/data). This data set contains sales transaction records for an electronics company. This data was collected over a one year period, starting in September 2023 and ending September 2024. It contains demographic information such as gender and age of buyers. It also contains information on the product types, which include various electronics like Smartphones, Laptops, Tablets and smartwatches. 

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
In Excel, I cleaned and transformed the data. I made sure that there were no nulls or outstanding numbers. I also made sure that the column titles were descriptive, short and accurate. In addition to this, I made picot charts to better undesand the data. The first pivot table I made was to see the distribution between male an female buyers which was almost equal. I then wanted to see how many customers opted to be loyal members. The distribution of this showed that aproximitly 22% of customers were not members as opposed to 78% who were memebrs. lastly I wanted to see the total amount purchased per electronic product and its corresponding amoutn purchased in add-ons. I added up all of total price of each product and the add_on total of each product to their corresponding pivor chart. The results of these are illustrated int he bar charts. We can see that the product with the most amount ot total transaction prices were smartphones. This corresponds with smartphones also having the most amount of add ons purchased. Headphones were the lease bought product and not surprisingly, they were also the product with the least amount of add_ons purchased. surprisingly, tablet add_on purchases surpased laptop and smartwatch add-on purchases, eventhough laptop and smartwatch transcation totals were both higher than ttablet transaction totals. 
