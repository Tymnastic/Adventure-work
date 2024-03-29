# Adventure-work


---

### Adventure Works Power BI Project Documentation

#### Overview of Adventure Works Dataset
The Adventure Works dataset forms the bedrock of this Power BI initiative. It encompasses diverse data sources, including sales transactions, product information, customer details, territorial insights, and a comprehensive return table.

#### Scope and Objectives
This project is designed to extract valuable insights from the expansive Adventure Works dataset. It involves:
- Analyzing sales trends over time
- Assessing revenue per customer
- Investigating order patterns
- Conducting a meticulous examination of product returns to discern factors impacting the success of top-selling products.

#### Components of the Dataset
The dataset comprises four primary components:
- **Sales Data:** Comprehensive details of sales transactions, encompassing order dates, product specifics, customer and territory keys.
- **Product Lookup Data:** Categorical information facilitating product classification and analysis based on categories.
- **Territory Lookup Data:** Geographical segmentation providing insights into sales territories across diverse regions and continents.
- **Return Data:** Detailed records of product returns, inclusive of customer IDs, return dates, product IDs, and territory IDs.

#### Objectives of Analysis
This analysis aims to:
- Uncover intricate patterns, trends, and correlations within sales data, deciphering customer behavior, product performance, and regional influences.
- Present actionable insights derived from the Adventure Works dataset to bolster data-driven decision-making.
- Provide a holistic view of business operations by synthesizing data across sales, products, customers, and territories.

#### Data Processing and Transformation
- Imported raw data (CSV) through Power BI's "Get Data" function.
- Data underwent meticulous cleaning and transformation via Power Query:
  - Elimination of extraneous columns (e.g., product descriptions).
  - Profiling and validation of data types.
  - Creation of a calculated column in the sales table computing total revenue using DAX.

#### Data Modeling Approach
- Implemented a snowflake schema for enhanced performance and efficient query processing by the DAX engine.
- Normalized the product category table using DAX's distinct function to extract subcategories.
- Established a one-to-many relationship between sales data and return data, forming the core of the fact tables.

![Data Model](https://github.com/Tymnastic/Adventure-work/blob/main/data%20modelling.png)


#### Exploratory Analysis and Metrics
- Developed a measure table encompassing explicit measures for filter modification.
- Created critical measures using DAX for:
  - Total Revenue =
SUMX(
    'Sales Data',
    'Sales Data'[OrderQuantity]
    *
    RELATED(
        'Product Lookup'[ProductPrice]
    )
)

  - Total Returns =
COUNT(
    'Returns Data'[ReturnQuantity]
)
  - Total Orders =
DISTINCTCOUNT(
    'Sales Data'[OrderNumber]
)

  -  Total Profit =
[Total Revenue] - [Total Cost]


### Total Customers
```DAX
Total Customers = 
    DISTINCTCOUNT(
        'Sales Data'[CustomerKey]
    )


##### Return Rate:
The return rate signifies the proportion of returned items concerning the total quantity sold. It provides insights into product quality, customer satisfaction, and potential operational inefficiencies. The formula used is:
```DAX
Return Rate = 
Return Rate = 
DIVIDE(
    [Quantity Returned],
    [Quantity Sold],
    "No Sales"
)
```

##### Year-to-Date (YTD) Revenue:
YTD revenue tracks the total revenue accumulated from the beginning of the calendar year up to the present date. It helps monitor revenue performance over specific time frames. The calculation involves:
```DAX
YTD Revenue = 
CALCULATE(
    [Total Revenue],
    DATESYTD(
        'Calendar Lookup'[Date]
    )
) 
```



### Visualization Pages and Key Metrics

#### Executive Dashboard
The Executive Dashboard encapsulates key business metrics, including:
- **Total Revenue**
- **Total Orders**
- **Returns Rate**
- **Profits**

- A line chart  was used to show the revenue trend over time  , bar chart was used to show the distributiion of product based on product categories. an 
-- A table matrix was developed  to show the top selling product .

![Executive Dashboard](https://github.com/Tymnastic/Adventure-work/blob/main/Executive%20dash.png)


#### Map Visualization
The Map Visualization provides geographical insights and may contain location-based data showcasing sales distribution or customer concentration.

#### Product Details
This section offers a detailed breakdown of product-related metrics, featuring:
- **Year-to-Date (YTD) Weekly Revenue Line Chart:** Depicts revenue trends on a weekly basis and includes a trend line for forecasting future revenue.
- **Product Categories Order Distribution Bar Chart:** Visualizes order distribution across various product categories.
--
   **Selection metrics** containing Revenue, profits, total Orders, total returns and return rate via weekly, monthly or yearly .so user can make selection based on metric preference to view the product with time

  ![product detail page](https://github.com/Tymnastic/Adventure-work/blob/main/product%20detail.png)


#### Customer Details
The Customer Details section focuses on customer-centric data, incorporating:
- **Top Purchasing Customers Table:** Highlights top-selling products based on specific criteria.
- **Selection Metric for Total Customers, and Average Revenue per Customer via Start of Week:** Enables user selection to view Average revenue, total Customer based on weekly data points.

- 
![Customer Detail Page](https://github.com/Tymnastic/Adventure-work/blob/main/Customer%20details.png)


#### Rationale for Visualization and Metrics Selection
- **Executive Dashboard:** Provides an at-a-glance overview of critical business metrics, aiding in quick decision-making.
- **YTD Weekly Revenue Line Chart:** Offers a temporal view of revenue trends, complemented by a forecast trend line, enabling future revenue prediction.
- **Product Categories Order Distribution Var Chart:** Illustrates the distribution of orders across different product categories for comprehensive product analysis.
- **Customer-Centric Metrics:** Empowers users to delve into customer-specific data, focusing on top-selling products and enabling flexible metric selection based on weekly data.

The inclusion of these visualization pages and key metrics enhances the overall analysis by offering varied perspectives on sales, product details, and customer-centric data, fostering informed decision-making and strategic planning.
You can interact with the visualization on 
![Alt text](total revenue.png)

