# Demand Forecasting Model – Online Retail

##  Project Overview

This project focuses on building a **demand forecasting model** to predict the **quantity of products sold** using historical online retail sales data. The goal is to help the **Sales & Operations Planning (S&OP)** team make better decisions related to inventory planning, promotions, and supply chain management.

By using machine learning (Random Forest Regression) and time-based features, the model estimates future demand patterns and evaluates performance using **Mean Absolute Error (MAE)**.



##  Business Problem

E-commerce companies face uncertainty in customer demand, especially during peak seasons. Poor forecasting can lead to:

* Stockouts
* Overstocking
* Increased operational costs
* Delayed deliveries

This project helps forecast product demand so that the company can:

* Maintain optimal inventory levels
* Plan promotions effectively
* Improve customer satisfaction


##  Dataset Description

**File:** `Online Retail.csv`

### Columns

| Column Name | Description                       |
| ----------- | --------------------------------- |
| InvoiceNo   | Unique 6-digit transaction number |
| StockCode   | Unique product identifier         |
| Description | Product description               |
| Quantity    | Number of items sold              |
| UnitPrice   | Price per unit                    |
| CustomerID  | Unique customer identifier        |
| Country     | Customer country                  |
| InvoiceDate | Date & time of transaction        |
| Year        | Transaction year                  |
| Month       | Transaction month                 |
| Week        | Week number (1–52)                |
| Day         | Day of month                      |
| DayOfWeek   | Day of week (0=Monday, 6=Sunday)  |


## Technologies Used

* **Python**
* **Apache Spark (PySpark)**
* **Spark MLlib**
* **Random Forest Regressor**
* **Pandas**


##  Data Preprocessing

1. Load CSV data using Spark
2. Convert `InvoiceDate` to proper date format
3. Aggregate transactions at **daily level** by:

   * Country
   * StockCode
   * InvoiceDate
4. Sum daily quantities and average unit price


##  Train-Test Split

The dataset is split using a **time-based split**:

* **Training Data:** All records up to and including `2011-09-25`
* **Testing Data:** All records after `2011-09-25`

This ensures no data leakage and simulates real-world forecasting.

A pandas DataFrame named **`pd_daily_train_data`** is created containing:

* Country
* StockCode
* InvoiceDate
* Quantity


##  Feature Engineering

### Categorical Encoding

* `Country` → `CountryIndex`
* `StockCode` → `StockCodeIndex`

### Numerical Features Used

* Year
* Month
* Week
* Day
* DayOfWeek

All features are combined using **VectorAssembler**.


##  Model Building

* **Algorithm:** Random Forest Regressor
* **Target Variable:** Quantity
* **Reason for choice:**

  * Handles non-linearity well
  * Robust to noise
  * Works well with mixed features

The entire workflow is implemented using a **Spark ML Pipeline**.


##  Model Evaluation

The model is evaluated on the test dataset using:

### Metric

* **Mean Absolute Error (MAE)**

MAE measures the average absolute difference between actual and predicted quantities.

The final MAE value is stored as a float variable:

```python
mae
```



##  Sales Forecasting Output

### Weekly Sales Forecast

Predicted daily quantities are aggregated at weekly level.

### Business Question Answered

**How many units are expected to be sold in Week 39 of 2011?**

The total predicted quantity for Week 39 is stored as:

```python
quantity_sold_w39
```



##  Future Forecasting Capability

Although the dataset only contains data until 2011, the trained model can:

* Predict future demand for any date
* Forecast upcoming weeks or months

By creating future date features (Year, Month, Week, etc.), the model can estimate **expected sales** even for current or future years.



## Key Outcomes

* Built a scalable demand forecasting model using PySpark
* Successfully evaluated forecasting accuracy using MAE
* Generated actionable weekly sales predictions
* Created a model useful for inventory and promotion planning
