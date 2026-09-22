# 🚚 Supply Chain Analytics – Delivery Performance & Risk Analysis

*Analyzing supply chain delivery performance, profitability, operational delays, and late-delivery risk using Python, SQL, Machine Learning, and Power BI.*

---

## 📌 Table of Contents

* <a href="#overview">Overview</a>
* <a href="#business-problem">Business Problem</a>
* <a href="#dataset">Dataset</a>
* <a href="#tools--technologies">Tools & Technologies</a>
* <a href="#project-structure">Project Structure</a>
* <a href="#data-cleaning--preparation">Data Cleaning & Preparation</a>
* <a href="#feature-engineering">Feature Engineering</a>
* <a href="#exploratory-data-analysis-eda">Exploratory Data Analysis (EDA)</a>
* <a href="#business-kpis">Business KPIs</a>
* <a href="#research-questions--key-findings">Research Questions & Key Findings</a>
* <a href="#profitability-analysis">Profitability Analysis</a>
* <a href="#delay-driver-analysis">Delay Driver Analysis</a>
* <a href="#machine-learning-model">Machine Learning Model</a>
* <a href="#model-evaluation">Model Evaluation</a>
* <a href="#dashboard">Dashboard</a>
* <a href="#how-to-run-this-project">How to Run This Project</a>
* <a href="#final-recommendations">Final Recommendations</a>
* <a href="#author--contact">Author & Contact</a>

---

<h2><a class="anchor" id="overview"></a>Overview</h2>

This project analyzes supply chain operations to identify delivery delays, profitability patterns, operational bottlenecks, and factors associated with late-delivery risk.

A complete analytics workflow was developed using **Python for data cleaning, exploratory analysis, visualization, and machine learning**, **SQL for business-oriented data analysis**, and **Power BI for interactive dashboard reporting**.

The project combines descriptive analytics and predictive analytics to help businesses monitor delivery performance and identify operational areas requiring further investigation.

---

<h2><a class="anchor" id="business-problem"></a>Business Problem</h2>

Efficient supply chain management is critical for maintaining customer satisfaction, controlling operational costs, and protecting profitability.

This project aims to:

* Measure overall delivery performance
* Identify late-delivery patterns
* Analyze the impact of delays on profitability
* Identify regions and operational factors associated with higher delay rates
* Analyze delay patterns by month, day, and hour
* Evaluate shipping-mode performance
* Identify profitability and loss-making orders
* Determine factors associated with late-delivery risk
* Build a machine learning model to predict late-delivery risk
* Provide data-driven insights for supply chain decision-making

---

<h2><a class="anchor" id="dataset"></a>Dataset</h2>

The project uses the **Supply Chain Dataset**, containing order-level information related to customers, products, shipping, delivery, sales, and profitability.

The dataset includes information such as:

* Order dates
* Shipping dates
* Shipping mode
* Customer segment
* Product category
* Department
* Order region
* Order status
* Scheduled shipping days
* Delivery status
* Order profit
* Late-delivery risk

The raw dataset is loaded from:

```text
DataCoSupplyChainDataset.csv
```

---

<h2><a class="anchor" id="tools--technologies"></a>Tools & Technologies</h2>

* **Python**

  * Pandas
  * NumPy
  * Matplotlib
  * Seaborn
  * SciPy
  * Scikit-learn
  * Imbalanced-learn

* **SQL**

  * SELECT
  * WHERE
  * GROUP BY
  * HAVING
  * CTEs
  * Window Functions
  * Aggregations

* **Machine Learning**

  * Train/Test Split
  * SMOTE
  * Random Forest Classifier
  * Classification Metrics

* **Power BI**

  * KPI Cards
  * Interactive Charts
  * Slicers
  * Trend Analysis
  * Regional Analysis

* **GitHub**

  * Project documentation
  * Version control
  * Portfolio presentation

---

<h2><a class="anchor" id="project-structure"></a>Project Structure</h2>

```text
supply-chain-analytics/
│
├── README.md
│
├── data/
│   └── Supply Chain Dataset.csv
│
├── notebooks/
│   ├── Supply Chain Analysis.ipynb
│
├── sql/
│   └── Research Based Question
│
├── dashboard/
│   └── supply_chain_dashboard.pbix
│
├── reports/
│   └── Supply_Chain_Performance_Report.pdf
│
└── images/
    └── dashboard.png
```

---

<h2><a class="anchor" id="data-cleaning--preparation"></a>Data Cleaning & Preparation</h2>

The raw dataset was cleaned and prepared before performing analysis.

### Data Cleaning Steps

* Inspected dataset dimensions and column structure
* Checked duplicate records
* Analyzed missing values
* Removed irrelevant and redundant columns
* Removed sensitive customer information
* Removed columns with no analytical value
* Removed cancelled shipping orders from delivery-time analysis
* Converted order and shipping dates into datetime format
* Checked categorical variables and their distributions

### Removed Columns

Examples of removed fields include:

* Customer Email
* Customer Password
* Customer Name
* Customer Address
* Customer Zipcode
* Customer ID
* Order ID
* Product IDs
* Product Image
* Latitude / Longitude
* Redundant discount and quantity fields
* Product Status
* Market
* Location fields not required for the analysis

---

<h2><a class="anchor" id="feature-engineering"></a>Feature Engineering</h2>

Several analytical features were created to measure operational performance.

### Order Processing Time

```python
df['Order Processing Time'] = (
    df['shipping date (DateOrders)']
    - df['order date (DateOrders)']
).dt.days
```

### Delivery Delay

```python
df['Delay'] = (
    df['Order Processing Time']
    - df['Days for shipment (scheduled)']
)
```

### Delayed Order Flag

```python
df['Is_Delayed'] = df['Delay'] > 0
```

### Time-Based Features

The following features were created:

* Order Month
* Order Day
* Order Hour

These features were used to identify temporal patterns in delivery delays.

---

<h2><a class="anchor" id="exploratory-data-analysis-eda"></a>Exploratory Data Analysis (EDA)</h2>

EDA was performed to understand supply chain performance and identify operational patterns.

### Key areas analyzed

* Delivery delay distribution
* Profitability distribution
* Delay percentage by region
* Delay percentage by customer segment
* Delay percentage by shipping mode
* Delay percentage by department
* Delay percentage by order status
* Monthly delivery delays
* Day-of-week delivery delays
* Hourly delivery delays
* Profit impact of delivery delays

### Example Profitability Classification

Orders were classified into three categories:

```text
Profit
Loss
Break-even
```

Based on:

```python
df['Order Profit Per Order']
```

---

<h2><a class="anchor" id="business-kpis"></a>Business KPIs</h2>

The project calculates important supply chain performance indicators.

| KPI                     | Description                                          |
| ----------------------- | ---------------------------------------------------- |
| Total Orders            | Total number of analyzed orders                      |
| Late Deliveries         | Number of orders delivered later than scheduled      |
| On-Time Delivery %      | Percentage of orders delivered within scheduled time |
| Late Delivery %         | Percentage of delayed orders                         |
| 90th Percentile Delay   | Delay level below which 90% of delays fall           |
| Total Profit            | Total positive order profit                          |
| Profit Impact of Delays | Profit associated with delayed orders                |

### KPI Calculations

**On-Time Delivery %**

```text
On-Time Delivery % =
(Total Orders - Late Deliveries) / Total Orders × 100
```

**Late Delivery %**

```text
Late Delivery % =
Late Deliveries / Total Orders × 100
```

---

<h2><a class="anchor" id="research-questions--key-findings"></a>Research Questions & Key Findings</h2>

The analysis investigates the following business questions:

### 1. What percentage of orders are delivered late?

Measures the overall delivery reliability of the supply chain.

### 2. Which regions have the highest delay rate?

Regional delay analysis helps identify geographical areas requiring operational investigation.

### 3. Which shipping mode has the highest delay rate?

Shipping modes are compared using total orders, delayed orders, and delay percentage.

### 4. Which customer segment experiences more delivery delays?

Customer segments are analyzed to identify differences in delivery performance.

### 5. Which departments contribute most to delivery delays?

Department-level analysis helps identify operational areas with higher delay rates.

### 6. How does delivery delay affect profitability?

Profitability is analyzed across different delay durations to understand the financial relationship between operational delays and order profit.

### 7. Which delay durations have the highest profit impact?

Orders are grouped by delay duration and evaluated using:

* Mean Profit
* Total Profit
* Order Count

### 8. Does delivery performance vary by month?

Monthly delay trends are analyzed to identify seasonal patterns.

### 9. Does delivery performance vary by day of the week?

Orders are grouped by weekday to compare delay percentages.

### 10. Does order time relate to delivery delays?

Hourly analysis is performed to identify variations in delay rates across the day.

---

<h2><a class="anchor" id="profitability-analysis"></a>Profitability Analysis</h2>

Orders are categorized based on **Order Profit Per Order**.

```python
df['Profitability Flag'] = np.where(
    df['Order Profit Per Order'] > 0,
    'Profit',
    np.where(
        df['Order Profit Per Order'] < 0,
        'Loss',
        'Break-even'
    )
)
```

### Profitability Categories

* **Profit** → Order Profit Per Order > 0
* **Loss** → Order Profit Per Order < 0
* **Break-even** → Order Profit Per Order = 0

The distribution of these categories is visualized using a percentage-based chart.

---

<h2><a class="anchor" id="delay-driver-analysis"></a>Delay Driver Analysis</h2>

Potential operational drivers of late delivery were analyzed across:

* Shipping Mode
* Customer Segment
* Department
* Product Type
* Order Status
* Order Region

For each category, the following metrics were calculated:

```text
Total Orders
Late Orders
Delay %
Average Delay
```

### Regional Driver Analysis

A regional driver analysis was also performed to identify the factors associated with higher delay percentages within a selected region.

Example:

```python
top_drivers_for_region('Central Africa')
```

This approach helps move from:

```text
"What region has delays?"
```

to:

```text
"What operational factors are associated with delays within that region?"
```

---

<h2><a class="anchor" id="machine-learning-model"></a>Machine Learning Model</h2>

A machine learning model was developed to predict **late-delivery risk**.

### Target Variable

```python
y = df['Late_delivery_risk']
```

### Features Used

The model uses operational and order-related variables including:

* Type
* Scheduled Shipment Days
* Category Name
* Customer Segment
* Department Name
* Order Region
* Shipping Mode
* Order Month
* Order Hour

### Encoding

Categorical variables are converted into numerical representations using frequency encoding.

```python
freq = X[col].value_counts(normalize=True)

X[f'{col}_freq'] = X[col].map(freq)
```

The original categorical columns are then removed before model training.

### Train/Test Split

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42,
    stratify=y
)
```

The dataset is divided into:

* **80% Training Data**
* **20% Testing Data**

---

<h2><a class="anchor" id="model-evaluation"></a>Model Evaluation</h2>

Because late-delivery prediction can involve class imbalance, **SMOTE (Synthetic Minority Oversampling Technique)** was applied to the training data.

```python
smote = SMOTE(random_state=42)

X_train_bal, y_train_bal = smote.fit_resample(
    X_train,
    y_train
)
```

### Model

A Random Forest Classifier was trained on the balanced training dataset.

```python
rf_model_balanced = RandomForestClassifier(
    random_state=42
)

rf_model_balanced.fit(
    X_train_bal,
    y_train_bal
)
```

### Evaluation Metrics

The model is evaluated using:

* Accuracy
* Precision
* Recall
* Classification Report

```python
accuracy_score()-
precision_score()
recall_score()
classification_report()
```

### Feature Importance

Feature importance can also be analyzed to identify which variables contribute most to the model's predictions.

```python
feature_importance = pd.DataFrame({
    'Feature': X_train.columns,
    'Importance': rf_model_balanced.feature_importances_
}).sort_values(
    'Importance',
    ascending=False
)
```

This helps connect the machine learning results with the business analysis.

---

<h2><a class="anchor" id="dashboard"></a>Dashboard</h2>

The Power BI dashboard is designed to provide an executive-level view of supply chain performance.

### Dashboard Components

#### KPI Cards

* Total Orders
* Late Deliveries
* On-Time Delivery %
* Late Delivery %
* Total Profit
* Average Delay

#### Delivery Analysis

* Delay by Region
* Delay by Shipping Mode
* Delay by Customer Segment
* Delay by Department

#### Time Analysis

* Monthly Delay Trend
* Day-of-Week Delay
* Hourly Delay Pattern

#### Profitability Analysis

* Profit vs Loss
* Profit by Delay
* Profitability Distribution

#### Risk Analysis

* Late Delivery Risk
* High-Risk Segments
* Operational Risk Factors

### Dashboard Preview

![Supply Chain Dashboard](images/dashboard.png)

---

<h2><a class="anchor" id="how-to-run-this-project"></a>How to Run This Project</h2>

### 1. Clone the repository

```bash
git clone https://github.com/SwastikAnalytics/supply-chain-analytics.git
```

### 2. Navigate to the project

```bash
cd supply-chain-analytics
```

### 3. Install required Python libraries

```bash
pip install -r requirements.txt
```

### 4. Place the dataset

Place:

```text
Supply Chain Dataset.csv
```

inside the:

```text
data/
```

folder.

### 5. Run the Python notebooks

Open:

```text
Supply Chain Analysis.ipynb
```

### 6. Run SQL analysis

Execute the SQL scripts located inside:

```text
sql/
```

### 7. Open the Power BI dashboard

Open:

```text
dashboard/supply_chain_dashboard.pbix
```

---

<h2><a class="anchor" id="final-recommendations"></a>Final Recommendations</h2>

Based on the analytical framework, the following areas can be considered for supply chain improvement:

* Monitor regions with consistently high delay percentages
* Investigate shipping modes associated with higher delay rates
* Track departments and product categories with recurring delivery issues
* Monitor delay duration and its relationship with profitability
* Establish regular delivery-performance monitoring
* Investigate seasonal and time-based delivery patterns
* Use late-delivery risk predictions as an additional operational monitoring signal
* Prioritize operational investigation using both historical analytics and model-driven risk indicators
* Continuously monitor profitability alongside delivery performance

---

<h2><a class="anchor" id="author--contact"></a>Author & Contact</h2>

**Swastik Kumar**
Data Analyst | MIS Analyst | Business Intelligence Enthusiast

📧 Email: [Your Email]

🔗 [LinkedIn](Your-LinkedIn-URL)

🔗 [GitHub](https://github.com/SwastikAnalytics)

---

## ⭐ Project Highlights

**Data Analytics:** Python, Pandas, NumPy, Matplotlib, Seaborn

**Database & Querying:** SQL, CTEs, Joins, Aggregations, Window Functions

**Business Intelligence:** Power BI, KPI Dashboards, Interactive Visualization

**Machine Learning:** Random Forest, SMOTE, Classification, Feature Importance

**Business Focus:** Supply Chain, Delivery Performance, Profitability, Operational Risk
