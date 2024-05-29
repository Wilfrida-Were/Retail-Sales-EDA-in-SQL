# Retail Sales Exploratory Data Analysis in SQL

This **[Retail Sales Dataset](https://www.kaggle.com/datasets/mohammadtalib786/retail-sales-dataset/data)** is a snapshot of a fictional retail landscape, capturing essential attributes that drive retail operations and customer interactions. It includes key details such as `Transaction ID`, `Date`, `Customer ID`, `Gender`, `Age`, `Product Category`, `Quantity`, `Price per Unit`, and `Total Amount`.

Check out the full code in this **[Kaggle Notebook](https://www.kaggle.com/code/wilfridawere/retail-sales-eda-in-sql)**

These are the analyses I will perform:

* Analysis 1: Customer`Age`, `Gender`, and Purchasing Behaviour
* Analysis 2: Top `Product Category` for each `Age` and `Gender`
* Analysis 3: Customer Purchases by `Quantity`, `Age`, `Gender`, and `Product Category`
* Analysis 4: `Price per Unit` Comparison by `Product Category`

# Data Cleaning
​
The dataset has **1000 rows and 9 columns**

Since this particular dataset has **No Missing values**, I will confirm if there are unexpected values by checking for *unique values* in each column and identifying potential *outliers*

Yes, the analyses will eventually be performed using ***SQL commands***. To me, Data Cleaning is easier in Python. Please reach out if you have any cheat sheet or effective ways to clean data using SQL

* There are 1000 distinct Transaction IDs and 1000 distinct Customers (Customer ID)s
* Since there are only 345 unique dates, some customers likely made purchases on the same dates
* The Product categories are only *Beauty*, *Clothing* and *Electronics*

# Connect to a Database and convert the Cleaned Dataframe to a Table

This SQL Exploratory Data Analysis (EDA) utilizes Python's `sqlite3` library to connect to a SQLite database file. This is how I use it. At the very end of the notebook, I will **close** the connection to the database.

```sql
import sqlite3

conn = sqlite3.connect('retail_data.db')  # replace ('retail_data.db') with ('your_database_name.db')

# Create 'retail' table
cursor = conn.cursor()
cursor.execute("SELECT name FROM sqlite_master WHERE type='table' AND name='retail'")
table_exists = len(cursor.fetchall()) > 0

if not table_exists:
  # Load data to 'retail' table only if it doesn't exist
  df.to_sql('retail', conn, index=False)
  print("Table 'retail' created and data loaded successfully.")
else:
  print("Table 'retail' already exists. Skipping data loading.")
```

# Analysis 1: Customer Age, Gender, and Purchasing Behaviour

# Total spending for each combination of Age and Gender

| Age | Female | Male |
|---|---|---|
| 18 | 7940 | 3275 |
| 19 | 7335 | 7535 |
| 20 | 5175 | 3470 |
| 21 | 5400 | 7185 |
| 22 | 5425 | 8275 |
| 23 | 2895 | 5325 |
| 24 | 1750 | 3665 |
| 25 | 3550 | 6350 |
| 26 | 10375 | 3605 |
| 27 | 4280 | 5105 |
| 28 | 5400 | 3270 |
| 29 | 4000 | 2570 |
| 30 | 6285 | 3505 |
| 31 | 2020 | 8200 |
| 32 | 1850 | 3700 |
| 33 | 2040 | 4200 |
| 34 | 12050 | 4735 |
| 35 | 6815 | 4475 |
| 36 | 3080 | 6025 |
| 37 | 5730 | 5920 |
| 38 | 6020 | 5080 |
| 39 | 3355 | 1240 |
| 40 | 7630 | 1785 |
| 41 | 1195 | 4455 |
| 42 | 5290 | 3210 |
| 43 | 10260 | 7710 |
| 44 | 3590 | 3970 |
| 45 | 585 | 5740 |
| 46 | 5380 | 7710 |
| 47 | 6315 | 6190 |
| 48 | 5410 | 1830 |
| 49 | 2650 | 2460 |
| 50 | 4300 | 5545 |
| 51 | 7270 | 8795 |
| 52 | 4270 | 2770 |
| 53 | 4890 | 4620 |
| 54 | 5755 | 4750 |
| 55 | 7070 | 2710 |
| 56 | 6025 | 3415 |
| 57 | 3630 | 5660 |
| 58 | 3680 | 3715 |
| 59 | 3785 | 5685 |
| 60 | 7660 | 3930 |
| 61 | 2840 | 3890 |
| 62 | 3060 | 5060 |
| 63 | 1205 | 8045 |
| 64 | 6325 | 2800 |

# Insights from Analysis 1
​
Analysis 1 shows how Total spending varies with `Age` and `Gender`

​
For example: For 20 year olds, Females collectively spent **more** than Males. The opposite is shown for 63 year olds, and so on.

​
From the Barplot below, you see that **39 year olds** collectively spent the **least** while **43 year olds** spent the **most**

# Barplot of Total Spending by Age and Gender

![Alt text](./Barplot%20of%20Total%20Spending%20by%20Age%20and%20Gender.png)  

# Analysis 2: Top Product Categories for each Age and Gender

The table shows from **Age 18 - Age 25**, and **Age 35 - Age 45**. See the **FULL** output **[Here](https://www.kaggle.com/code/wilfridawere/retail-sales-eda-in-sql)**

| Product_Category | Beauty | Clothing | Electronics |
|---|---|---|---|
| Age Gender       |        |        |        |
| 18 Female         | 3195.0 | 2575.0  | 2170.0  |       
| 18 Male           | 1765.0 | 1510.0  | NaN      |
| 19 Female         | 2225.0 | 1200.0  | 3910.0  |
| 19 Male           | 2140.0 | 1530.0  | 3865.0  |
| 20 Female         |  365.0 |   80.0  | 4730.0  |
| 20 Male           | 2160.0 |  360.0  |  950.0  |
| 21 Female         | 3300.0 | 1200.0  |  900.0  |
| 21 Male           | 4700.0 | 1885.0  |  600.0  |
| 22 Female         | 1300.0 | 3275.0  |  850.0  |
| 22 Male           | 4230.0 | 2075.0  | 1970.0  |
| 23 Female         |  475.0 | 1270.0  | 1150.0  |
| 23 Male           |  165.0 | 3050.0  | 2110.0  |
| 24 Female         | 1575.0 |   25.0  |  150.0  |
| 24 Male           | 1310.0 | 2125.0  |  230.0  |
| 25 Female         | 1000.0 | 2200.0  |  350.0  |
| 25 Male           | 1375.0 | 2150.0  | 2825.0  |
| 35 Female        | 3000.0    | 1545.0  | 2270.0  |
| 35 Male          | 2075.0    | 1140.0  | 1260.0  |
| 36 Female        | 1300.0    | 1310.0  |  470.0  |
| 36 Male          | 2025.0    | 1900.0  | 2100.0  |
| 37 Female           | NaN      | 3270.0  | 2460.0  |
| 37 Male          | 1620.0    | 2200.0  | 2100.0  |
| 38 Female        | 2100.0    |  300.0  | 3620.0  |
| 38 Male          | 1200.0    |  790.0  | 3090.0  |
| 39 Female        | 3100.0    |   75.0  |  180.0  |
| 39 Male          | 920.0     |  160.0  |  160.0  |
| 40 Female        | 3700.0    | 2295.0  | 1635.0  |
| 40 Male            | 50.0     | 1135.0  |  600.0  |
| 41 Female           | NaN      | 1045.0  |  150.0  |
| 41 Male          | 1550.0    | 1340.0  | 1565.0  |
| 42 Female        | 2380.0    |  730.0  | 2180.0  |
| 42 Male          | 1780.0    |  275.0  | 1155.0  |
| 43 Female        | 2425.0    | 4175.0  | 3660.0  |
| 43 Male           | 120.0     | 2240.0  | 5350.0  |
| 44 Female          | 75.0     | 2890.0  |  625.0  |
| 44 Male            | 30.0     | 2110.0  | 1830.0  |
| 45 Female         | 190.0     |  310.0  |   85.0  |
| 45 Male          | 3840.0    | 1000.0  |  900.0  |

# Insights from Analysis 2

Analysis 2 helps to identify **Trends in Customer Spending behaviour** based on `Age`, `Gender`, and `Product Category`

The insights:

* Age Preferences: Spending habits change with Age for certain Product Categories
* Gender Differences: There are significant differences in spending patterns between Genders for specific Product Categories

For a larger Real-life dataset, using such analysis can help to refine the **Target Audience for Marketing Campaigns**. Specific Age groups and Genders have a higher propensity to spend on certain Product Categories

# Analysis 3: Customer Purchases by Quantity

Customer Purchases by Quantity is grouped by ***Age***, ***Gender***, and ***Product Category***

| Product_Category | Beauty | Clothing | Electronics |
|---|---|---|---|
| Age Gender       |        |        |        |
| 18 Female        | 3.0     | 3.0      | 1.0       |
| 18 Male          | 2.0     | 2.0      | NaN       |
| 19 Female        | 1.0     | 4.0      | 2.0       |
| 19 Male          | 3.0     | 3.0      | 2.0       |
| 20 Female        | 1.0     | 1.0      | 4.0       |
| 20 Male          | 2.0     | 2.0      | 3.0       |
| 21 Female        | 2.0     | 4.0      | 3.0       |
| 21 Male          | 4.0     | 3.0      | 2.0       |
| 22 Female        | 4.0     | 1.0      | 2.0       |
| 22 Male          | 4.0     | 3.0      | 3.0       |
| 23 Female        | 1.0     | 1.0      | 2.0       |
| 23 Male          | 2.0     | 2.0      | 1.0       |
| 24 Female        | 3.0     | 1.0      | 4.0       |
| 24 Male          | 2.0     | 1.0      | 1.0       |
| 60 Female        | 3.0     | 3.0      | 2.0       |
| 60 Male          | 1.0     | 2.0      | 4.0       |
| 61 Female        | NaN     | 1.0      | 2.0       |
| 61 Male          | 4.0     | 1.0      | 2.0       |
| 62 Female        | 4.0     | 2.0      | 2.0       |
| 62 Male          | 4.0     | 1.0      | 4.0       |
| 63 Female        | 1.0     | 3.0      | 2.0       |
| 63 Male          | 1.0     | 4.0      | 2.0       |
| 64 Female        | 1.0     | 2.0      | 4.0       |
| 64 Male          | 2.0     | 4.0      | 4.0       |

# Insights from Analysis 3

Analysis 3 can help answer these questions:

* Purchase Patterns by Age and Gender: For example, are there any Age groups or Genders that consistently purchase more of a  particular Product category?
* Popular Product Categories: You can identify which Product Categories are generally purchased the most across different Age and Gender groups.
* Variations in Purchases: You can see if there are any significant variations in purchase quantities for the same Product Category across different Age and Gender groups. For instance, does the purchase of Electronics increase or decrease with Age for a particular Gender?

**Actionable insights**:

Imagine the analysis reveals that young females (18-24) consistently purchase more beauty products than other demographics *(this is an example)*. This can inform several decisions:

* Inventory: The store can stock a wider variety of beauty products and maintain higher inventory levels for this category.
* Promotions: They can run targeted promotions or offer loyalty rewards for beauty product purchases.
* Store Layout: Beauty products could be placed in a prominent location on the first floor, readily accessible to young female customers.

By leveraging the insights from purchase quantity analysis, retail companies can make data-driven decisions that **Optimize Inventory management**, **Product Development**, **Marketing strategies**, and ultimately, increase sales and customer satisfaction.

# Analysis 4: Price per Unit Comparison by Product Category

| Product_Category | Average_Price | Min_Price | Max_Price |
|---|---|---|---|
| Beauty         | 184.06            | 25        | 500       |
| Clothing         | 174.29              | 25        | 500       |
| Electronics         | 181.90              | 25        | 500       |

# Insights from Analysis 4

Analysis 4 helps understand the **Average Price, and Price Range for each Product Category**

This helps inform decisions based on:

* Pricing Strategies: When setting prices for new products, retailers can consider the average price point of the category to ensure their products are competitively priced. In this case, Beauty products have the highest Average price.
* Product Assortment: The significant difference between the minimum and maximum prices for each category (e.g., Electronics: 25 - 500) implies that the retailer offers a variety of products within each category at different price points. This allows customers to choose based on their needs and budget.

Finally, when the analyses are done, ***Close the connection*** to the Database using:

```sql
conn.commit()`  # Save changes (if any)
conn.close()`
```

I use the same dataset from these analyses, to perform **[Retail Sales EDA in Python](https://www.kaggle.com/code/wilfridawere/retail-sales-eda-in-python)**

Feel free to Contact me for any changes and feedback

***Explore and be teachable***
