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

#### Exploratory Analysis and Metrics
- Developed a measure table encompassing explicit measures for filter modification.
- Created critical measures using DAX for:
  - Total Revenue =
SUMX(
    'Sales Data',
    'Sales Data'[OrderQuantity] * RELATED('Product Lookup'[ProductPrice])
)

  - Total Returns =
COUNT('Returns Data'[ReturnQuantity])

  - Total Orders =
DISTINCTCOUNT('Sales Data'[OrderNumber])


  -  Total Profit =
[Total Revenue] - [Total Cost]

##### Total Customers:
The count of distinct customer keys provides insights into the customer base's size, which is fundamental in understanding market reach and potential growth opportunities.
```DAX
Total Customers = 
DISTINCTCOUNT(
    'Sales Data'[CustomerKey]
)


#### Target Metrics Establishment
- Derived targets for profit, returns, and revenue using DAX based on previous month performance.

— Revenue Target =
[Previous Month Revenue] * 1.1

Profit Target =
[Previous Month Profit] * 1.1


#### Additional Calculated Metrics and Their Significance

##### Average Revenue per Customer:
This metric measures the average revenue generated per customer, reflecting the effectiveness of revenue generation strategies tailored toward individual customers. It's calculated as follows:
```DAX
Average Revenue per Customer = 
DIVIDE(
    [Total Revenue], 
    [Total Customers]
)
```

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
- **Total Customers**
- **Revenue per Customer**

#### Map Visualization
The Map Visualization provides geographical insights and may contain location-based data showcasing sales distribution or customer concentration.

#### Product Details
This section offers a detailed breakdown of product-related metrics, featuring:
- **Year-to-Date (YTD) Weekly Revenue Line Chart:** Depicts revenue trends on a weekly basis and includes a trend line for forecasting future revenue.
- **Product Categories Order Distribution Var Chart:** Visualizes order distribution across various product categories.

#### Customer Details
The Customer Details section focuses on customer-centric data, incorporating:
- **Top Selling Table:** Highlights top-selling products based on specific criteria.
- **Selection Metric for Revenue, Total Profit, and Sales via Start of Week:** Enables user selection to view revenue, total profit, and sales metrics based on weekly data points.

#### Rationale for Visualization and Metrics Selection
- **Executive Dashboard:** Provides an at-a-glance overview of critical business metrics, aiding in quick decision-making.
- **YTD Weekly Revenue Line Chart:** Offers a temporal view of revenue trends, complemented by a forecast trend line, enabling future revenue prediction.
- **Product Categories Order Distribution Var Chart:** Illustrates the distribution of orders across different product categories for comprehensive product analysis.
- **Customer-Centric Metrics:** Empowers users to delve into customer-specific data, focusing on top-selling products and enabling flexible metric selection based on weekly data.

The inclusion of these visualization pages and key metrics enhances the overall analysis by offering varied perspectives on sales, product details, and customer-centric data, fostering informed decision-making and strategic planning.
You can interact with the visualization on 
![Alt text](total revenue.png)

