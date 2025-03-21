![Banner Image](./images/banner_image.png)
# 🍕 Pizza Mania Sales Analysis 🍕

 <a id="one"></a>
## **🌍 1. Introduction**
<a href=#cont>Back to Project Structure</a>

### 1.1 Project Overview 📝 
This project focuses on supporting Pizza Mania’s commitment to growth, operational excellence, and exceptional customer experience through data-driven decision-making. By analyzing business data, the goal is to uncover key insights, identify emerging trends, and highlight actionable opportunities to enhance performance, optimize operations, and drive strategic growth.

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


[Click here](./problem%20statement/Project_Statement(NorthwindTraders).docx) to download the full problem statement for this project.

---
An exploratory data analysis (EDA) of a world class pizza outlet called `Pizza Mania`.

This project provides a comprehensive analysis of a year's worth of sales from a pizza outlet. The dataset includes details on each order, such as date and time, pizza type, size, quantity, price, and ingredients. Using Power BI, I explored customer behavior, peak sales times, order trends, revenue, and potential areas for menu optimization and promotions.

## Project Overview 🌍 

The goal of this project is to uncover insights that can help improve sales and customer satisfaction at the pizza outlet. This analysis can guide business decisions, such as identifying peak hours, bestseller pizzas, and potential seasonal promotions. It also highlights data visualization techniques for deriving actionable insights from sales data.

## Dataset 📋 

The datasets contain a year's worth of order data detialed in the table below:

| Tables        | Features            | Description                                                                                                                                                                       |
|---------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| orders        | order_id         | Unique identifier for each order placed by a table                                                                                                                                |
|               | date             | Date the order was placed (entered into the system prior to cooking & serving)                                                                                                    |
|               | time             | Time the order was placed (entered into the system prior to cooking & serving)                                                                                                    |
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
|               | category         | Category that the pizza fall under in the menu (Classic, Chicken, Supreme, or Veggie)                                                                                             |
|               | ingredients      | Comma-delimited ingredients used in the pizza as shown in the menu (they all include Mozzarella Cheese, even if not specified; and they all include Tomato Sauce, unless specified) |

This data allows for a deep dive into customer behavior, order composition, and revenue generation over time.

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


## Exploratory Analysis 🔍

The following questions were addressed using the dataset:

1. **How many customers do we have each day?**
2. **Are there any peak hours?**
3. **How many pizzas are typically in an order?**
4. **Do we have any bestsellers?**
5. **How much money did we make this year?**
6. **Can we identify any seasonality in the sales?**
7. **Are there any pizzas we should take off the menu, or any promotions we could leverage?**


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
