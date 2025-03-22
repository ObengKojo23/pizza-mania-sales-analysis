![Banner Image](./images/banner_image.png)
# 🍕 Pizza Mania Sales Analysis 🍕
---
<a id="cont"></a>

### **Project Structure**

<a href=#one>1. Introduction</a>

<a href=#two>2. Data Collection & Extraction</a>

<a href=#three>3. Loading, Cleaning & Transformation of Data (ETL Process)</a>

<a href=#four>4. Data Modelling</a>

<a href=#five>5. Project Details</a>

---
 <a id="one"></a>
## **🌍 1. Introduction**
<a href=#cont>Back to Project Structure</a>

### 1.1 Project Overview 📝 
This project focuses on supporting Pizza Mania’s commitment to growth, operational excellence, and exceptional customer experience through data-driven decision-making. This project provides a comprehensive exploratory data analysis (EDA) of a year's sales from `Pizza Mania`. By analyzing business data, the goal is to uncover key insights, identify emerging trends, and highlight actionable opportunities to enhance performance, optimize operations, and drive strategic growth. The dataset for the project includes details on each order, such as date and time, pizza type, size, quantity, price, and ingredients. Using Power BI, I explored customer behaviour, peak sales times, order trends, revenue, and potential areas for menu optimization and promotions.

### 1.2 Problem Statement ⚠️

#### 1.2.1 Project Objective 🎯
This project seeks to analyze our business data in order to optimize performance, maximize revenue, and refine our customer experience. Your task is to deliver a comprehensive analysis and an interactive dashboard that will enable leadership to make well-informed decisions.

#### 1.2.3 Key Deliverables 🔑
- - An interactive dashboard (Power BI or Tableau) covering:
  - Daily customer trends
  - Peak hour visuals
  - Average order size
  - Bestsellers and underperformers
  - Revenue breakdowns
  - Seasonality charts
  - Promotion recommendations
-	An executive summary document (1–2 pages) highlighting the most important insights and strategic recommendations.


[Click here](./problem_statement/Mania_Pizza_Project_Statement.docx) to download the full problem statement for this project.

---
<a id="two"></a>
## **📋 2.  Data Collection & Extraction**
<a href=#cont>Back to Project Structure</a>

The datasets for this project contain a year's worth of pizza sales orders from `Pizza Mania`. The extracted datasets came in four separate `CSV` formats, which are detailed in the table below:

To access all four datasets for the project, [Click here](./Datasets) to download. 

All four original datasets were downloaded from [Maven Analytics](https://www.mavenanalytics.io/data-playground?dataStructure=Multiple%20tables&order=date_added%2Cdesc&page=4&pageSize=5).

| Datasets        | Features            | Description                                                                                                                                                                       |
|---------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| orders        | order_id         | Unique identifier for each order placed by a table                                                                                                                                |
|               | date             | Date the order was placed (entered into the system before cooking & serving)                                                                                                    |
|               | time             | Time the order was placed (entered into the system before cooking & serving)                                                                                                    |
| order_details | order_details_id | Unique identifier for each pizza placed within each order (pizzas of the same type and size are kept in the same row, and the quantity increases)                                 |
|               | order_id         | Foreign key that ties the details in each order to the order itself                                                                                                               |
|               | pizza_id         | Foreign key that ties the pizza ordered to its details, like size and price                                                                                                       |
|               | quantity         | Quantity ordered for each pizza of the same type and size                                                                                                                         |
| pizzas        | pizza_id         | Unique identifier for each pizza (constituted by its type and size)                                                                                                               |
|               | pizza_type_id    | Foreign key that ties each pizza to its broader pizza type                                                                                                                        |
|               | size             | Size of the pizza (Small, Medium, Large, X Large, or XX Large)                                                                                                                    |
|               | price            | Price of the pizza in USD                                                                                                                                                         |
| pizza_types   | pizza_type_id    | Unique identifier for each pizza type                                                                                                                                             |
|               | name             | Name of the pizza as shown in the menu                                                                                                                                            |
|               | category         | Category that the pizza falls under in the menu (Classic, Chicken, Supreme, or Veggie)                                                                                             |
|               | ingredients      | Comma-delimited ingredients used in the pizza as shown in the menu (they all include Mozzarella Cheese, even if not specified; and they all include Tomato Sauce, unless specified) |

This data allows for a deep dive into customer behaviour, order composition, and revenue generation over time.


---

<a id="three"></a>
## **🔍 3.  Loading, Cleaning & Transformation of Data (ETL Process)**
<a href=#cont>Back to Project Structure</a>

### 3.1 Promote Row Headers 📝
Promoting headers means ensuring that the column names of a dataset are recognized as the first row instead of data values.
- During loading the four datasets, the `pizza_type table` had its header row as a data value and, therefore, had to be promoted as a row header before loading it.

### 3.2 Rename Tables and Columns 📝 
After loading each table, checks were made on the table and column naming format. 

- The observation was that both table and column names were in the `Snake Case` format (e.g., orders_table, order_details). I, therefore, renamed each of them to follow the standard and my preferred format for dashboard projects. For example, `orders_table` was renamed `Orders Table`, `order_details` --> `Order Details`.

### 3.3 Standardize Data Formats 📝
After loading data into Power BI, standardising data formats is crucial to ensure accuracy, consistency, and compatibility for analysis and visualization. This ensures that Power BI does not misclassify data types (e.g., treating dates as text), facilitates accurate data modelling, enables reliable sorting and filtering, and ensures data consistency across the report.

- Each column was inspected to ensure the right data format. Fortunately, exploration indicated that all columns were in the right format.

### 3.4 Handling Null Values  📝
Checking for null values in Power BI is crucial as it ensures data completeness, prevents calculation errors, maintains accurate relationships, and improves visualization reliability.
- The data quality (`Valid, Error and Empty`) was inspected under transform data mode.
- The observation indicated no null values in the dataset as all `Valid` values were `100%`.

---

<a id="four"></a>
## **🔍 4.  Data Modelling**
<a href=#cont>Back to Project Structure</a>

Data modelling is the process of organizing data into tables and creating linked relationships or connecting them so that each table can easily communicate for analysis and report creation.

### 4.1 Creating Table Relationships 🔗 
- I used the snowflake schema by organizing the data into `Fact` and `Dimension` tables. The fact table contains the key metrics or performance data, while the dimension tables store descriptive attributes related to those metrics. This structure helps optimize query performance and improves the clarity of relationships between data points, ensuring efficient analysis and reporting.

  The table below shows the `Fact` and `Dimension` Tables.

  | Fact Table     | Dimension Tables   |
  |----------------|--------------------|
  | Order Detials  | Pizza Type         | 
  |                | Orders             |
  |                | Pizzas             |

- I created a new `Date Table` (Calender Table) to the schema. This new Date table is important for more efficient and flexible time-based analysis during the analysis. 

  The below DAX formula was used to create the new Date Table.
  ```sql
  
  Date = 
  ADDCOLUMNS(
      CALENDAR(MIN(Orders[Order Date]), MAX(Orders[Order Date])),
      "Year", YEAR([Date]),
      "Month", FORMAT([Date], "mmm"),
      "Month No", MONTH([Date]),
      "Quarter", FORMAT([Date], "\QQ"),
      "Day", FORMAT([Date], "ddd"),
      "Day No", WEEKDAY([Date])
  )
 
  ```
  A screenshot of the final Table Relationship
  ![Data Modelling View](./images/data_modelling.png) 

### 4.2 Creating Calculated Measures and Columns ➗
The decision to create calculated measures and columns stems from the questions to be answered and the insights to be uncovered. 
- I first created a measures table. I plan to store all my measures under this table for better organisation and easy accessibility.
- All measures were created based on the under-listed questions
  1. **How many customers do we have each day?**
  3. **Are there any peak hours?**
  4. **How many pizzas are typically in an order?**
  5. **Do we have any bestsellers?**
  6. **How much money did we make this year?**
  7. **Can we identify any seasonality in the sales?**
  8. **Are there any pizzas we should take off the menu or any promotions we could leverage?**
- Below is the list of all calculated measures and columns created
  
  1. Number of Customers (calculated measure)
  ```sql
   Number of Customers = DISTINCTCOUNT(Order_Details[Order ID])
   ```
  Since the dataset does not include a customer table, counting the distinct orders from the order_details table would be the best way to answer the first question, `How many customers do we have each day?`.

  2. Number of Customers (calculated column)
   ```sql
    Number of Customers = DISTINCTCOUNT(Order_Details[Order ID])
    ```
   Inspecting the tables indicates a `Time Column` in the `Orders Table`. Further inspection shows that the `Minimum Time` = 9:52:21 and `Maximum Time` = 23:05:52, which means that I can create a time interval slot from 9 AM to 12 PM to answer the question, `Are there any peak hours?` This will help sort varied timeframes for peak hours analysis.
  
  
  2. Total Sales (calculated measure)

  ```sql
  
  Total Sales = 
  SUMX(
      'Order_Details',
      'Order_Details'[Order Quantity] * RELATED(Pizzas[Pizza Price])
      )
 
  ```
  1. Number of Customers (calculated measure)
  ```sql
   Number of Customers = DISTINCTCOUNT(Order_Details[Order ID])
   ```
  Since the dataset does not include a customer table, counting the distinct orders from the order_details table would be the best way to answer the first question, `How many customers do we have each day?`.
 
 
  

## Key Performance Indicators (KPIs) 🔑 

The following KPIs were identified to measure the performance and trends in sales at Pizza Mania. These KPIs help uncover insights into customer behavior and sales patterns:

- **`Daily Order Count:`** Tracks the number of customers each day, helping to identify busy and slow days.

- **`Daily Sales:`** Analyzes sales by days to identify peak times, guiding staffing and operational planning.

- **`Average Order Size:`** Measures the typical number of pizzas in each order, giving insight into customer ordering patterns (e.g., whether they often order in groups or as individuals).

- **`Bestselling Pizzas:`** Identifies the most popular pizza types and sizes, helping in inventory planning and promotion targeting.

- **`Total Sales:`** Calculates total income generated within the year, providing a high-level view of business performance.

- **`Revenue by Pizza Type:`** Breaks down revenue by each type of pizza (Classic, Supreme, Veggie, and Chicken), revealing which categories are the most profitable.

- **`Seasonal Revenue Trends:`** Shows revenue by months, weeks, and days of the week, helping to identify sales cycles and potential seasonal promotions.

- **`Menu Optimization Opportunities:`** Identifies low-performing pizzas that may need to be discontinued or adjusted, and suggests potential promotions to increase sales of specific items.

- **`Average Order Value (AOV):`** Measures the average revenue per order, useful for setting targets for up-selling or cross-selling.

- **`Sales Margin by Pizza Type:`** Tracks the margin of each pizza type, supporting decisions on pricing adjustments or cost-cutting.


These KPIs were selected to provide a comprehensive view of the pizza mania’s sales dynamics, customer preferences, and overall performance. They guide decision-making to optimize sales, enhance customer satisfaction, and increase profitability.

## Conclusion 📝

This project offers valuable insights into the pizza outlet's sales dynamics, helping to inform business decisions on menu design, promotion strategies, and operational efficiency. The analysis is also a showcase of Power BI’s potential for transforming raw data into actionable insights, a skillset valuable in various industries.

---
### How to Run This Project 🚀 

1. **Clone the Repository**  
   Run the following command to clone the repository to your local machine:
   ```bash
   git clone https://github.com/ObengKojo23/pizza-sales-analysis.git
2. **Download Power BI Desktop**  
   You can download Power BI Desktop from the official Microsoft website: [Download Power BI Desktop](https://powerbi.microsoft.com/desktop/).
3. **Load the dataset**
   Load all the dataset into Power BI to explore the interactive dashboard.

## Tools and Technologies Used 🛠 

- **Power BI Desktop**: The primary tool for data visualization and analysis.
- **DAX (Data Analysis Expressions)**: Used for calculations and data manipulation.
- **Power Query**: For data transformation and cleansing.
- **Power BI Service**: For sharing reports and dashboards.
- **GitHub**: For version control and collaboration on project files, including sharing the Power BI reports and documentation.
- **Data Sources**: Excel spreadsheets.
- **Visualization Types**: Bar charts, line graphs, pie charts, tables, and cards.

## File Structure 💾

- `Data/`: Contains the datasets for analysis.
- `Dashboard/`: Power BI file for the dashboard.
- `README.md`: Project overview and documentation.
- `LICENSE`: The project is licensed under the Apache License 2.0.

## Acknowledgments 👏
- **Maven Analytics** for providing the [Pizza Sales dataset](https://www.mavenanalytics.io/data-playground?dataStructure=Multiple%20tables&order=date_added%2Cdesc&page=4&pageSize=5).
- **Power BI Community** for visualization inspiration and dashboarding techniques.
- **Pizza Icons**: Pizza icon used in the project was created by [Freepik - Flaticon](https://www.flaticon.com/free-icons/pizza).
