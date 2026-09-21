# 🗽 NYC 311 Service Requests Analysis

## 📌 Project Overview

This project analyzes **NYC 311 Service Requests** to discover patterns in public service requests based on **complaint type, agency, time, location, borough, and resolution duration**.

The project follows a practical Data Science workflow, starting from raw data cleaning and exploration, followed by feature engineering, visualization, advanced EDA, and preparation of the dataset for future Machine Learning applications.

---

## 🎯 Objectives

The main objectives of this project are to:

* Clean and prepare NYC 311 service-request data.
* Explore patterns in complaint types and service demand.
* Analyze requests across NYC boroughs and geographic locations.
* Investigate request volume by time and day.
* Analyze service-request resolution duration.
* Engineer useful time, geographic, and operational features.
* Identify patterns between complaint types, boroughs, and agencies.
* Prepare numerical and categorical features for future Machine Learning models.

---

## 📊 Dataset

The analysis uses the **NYC 311 Service Requests** dataset provided through the NYC Open Data platform.

For this project, a sample of **100,000 service requests** was used.

### Main features used

| Category            | Features                                                       |
| ------------------- | -------------------------------------------------------------- |
| Request Information | `unique_key`, `complaint_type`, `descriptor`, `location_type`  |
| Agency              | `agency`, `agency_name`                                        |
| Time                | `created_date`, `closed_date`                                  |
| Geography           | `borough`, `incident_zip`, `latitude`, `longitude`, `location` |
| Status              | `status`, `resolution_description`                             |
| Channel             | `open_data_channel_type`                                       |

---

## 🛠️ Technologies & Libraries

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**
* **Jupyter Notebook**

### Machine Learning preprocessing

* `StandardScaler`
* `OneHotEncoder`
* `ColumnTransformer`

---

## 🔄 Project Workflow

### 1. Data Loading

The NYC 311 dataset was loaded from the NYC Open Data API using Pandas.

```python
url = "https://data.cityofnewyork.us/resource/erm2-nwe9.csv?$limit=100000"
df = pd.read_csv(url)
```

---

### 2. Data Understanding

The dataset was investigated using:

* Dataset shape
* Data types
* Statistical summaries
* Missing-value analysis
* Duplicate checking
* Numerical and categorical feature identification

---

### 3. Data Cleaning

Several preprocessing steps were performed:

* Selected relevant columns for the analysis.
* Converted date columns to datetime format.
* Investigated missing values.
* Checked duplicate records.
* Handled missing categorical values using `"Unknown"`.
* Applied median imputation to numerical geographic features.
* Validated latitude and longitude values.
* Identified invalid geographic coordinates without automatically deleting the corresponding service requests.

Approximately **98.1% of records contained valid geographic coordinates**.

---

## ⚙️ Feature Engineering

Several new features were created to make the dataset more useful for analysis and future Machine Learning applications.

### Time Features

* Request year
* Request month
* Request hour
* Day of week
* Quarter
* Weekend indicator
* Season

### Geographic Features

* Valid-location indicator
* Borough
* ZIP code
* Latitude
* Longitude

### Resolution Feature

A new feature called:

```text
request_duration_days
```

was created from the difference between `closed_date` and `created_date`.

Negative durations were treated as invalid and replaced with missing values.

---

## 📈 Exploratory Data Analysis

The project includes several visual and statistical analyses.

### Complaint Types

The analysis found that **Illegal Parking** was the most common complaint type in the analyzed sample, with **15,294 requests**.

### Agencies

The **NYPD** accounted for approximately half of the analyzed requests, showing that a relatively small number of agencies represent a large portion of the overall request volume.

### Borough Analysis

**Brooklyn** had the highest number of service requests in the analyzed sample, with **32,035 records**.

However, request volume alone does not necessarily indicate worse conditions because factors such as population size and reporting behavior can influence the number of requests.

### Location Type

**Street/Sidewalk** was the most common location type, indicating that public spaces and infrastructure represent an important source of service requests.

---

## 🌎 Geographic Analysis

Geographic patterns were explored using:

* Latitude and longitude
* Borough
* ZIP code
* Geographic scatter plots
* Complaint type by borough

The analysis showed that requests are distributed across NYC rather than being concentrated in a single location.

The ZIP-code analysis also identified areas with substantially higher request volumes, with **11226** having the highest request volume in the analyzed sample.

---

## ⏱️ Request Resolution Time

The `request_duration_days` feature was used to investigate how long requests take to close.

The analysis showed:

* **Median resolution time:** approximately `0.08 days`
* **Mean resolution time:** approximately `0.54 days`

The difference between the median and mean indicates a **right-skewed distribution**.

Most requests are resolved relatively quickly, while a smaller number of requests take considerably longer.

The analysis also compared resolution time across:

* Agencies
* Complaint types

For agencies with sufficient request volume, **HPD** had the highest average resolution time in the analyzed sample.

Housing-related complaint types also showed relatively longer average resolution times.

---

## 🔍 Advanced EDA

The project includes additional analysis of relationships between different variables.

### Complaint Type × Borough

Complaint patterns vary across boroughs.

For example:

* Illegal Parking is particularly concentrated in **Brooklyn and Queens**.
* Noise – Street/Sidewalk complaints are particularly high in **the Bronx and Manhattan**.

### Agency × Resolution Time

Average and median request resolution times were compared across agencies while filtering out agencies with fewer than 100 requests.

### Complaint Type × Resolution Time

Complaint types were compared based on their average and median resolution durations.

### Weekend × Complaint Type

The analysis also examined how complaint patterns differ between weekdays and weekends.

Noise complaints were relatively more common on weekends.

---

## 🤖 Machine Learning Preparation

Although this project is primarily an **EDA and Data Analysis project**, the dataset was also prepared for future Machine Learning applications.

### Numerical Features

Numerical variables were standardized using:

```python
StandardScaler()
```

### Categorical Features

Categorical variables were transformed using:

```python
OneHotEncoder(handle_unknown="ignore")
```

Both transformations were combined using:

```python
ColumnTransformer()
```

This produced a machine-learning-ready representation of the dataset.

---

## 💡 Key Insights

1. **Illegal Parking** was the most common complaint category in the analyzed sample.
2. A relatively small number of agencies, particularly the **NYPD**, account for a large portion of request volume.
3. **Brooklyn** had the highest number of service requests in the analyzed sample.
4. **Street/Sidewalk** was the most common location type.
5. Service requests show meaningful geographic variation across NYC.
6. Most requests are resolved quickly, while a smaller number take considerably longer.
7. Resolution time varies across agencies and complaint categories.
8. Complaint patterns differ across boroughs.
9. Geographic data is highly usable, with approximately **98.1%** of records containing valid coordinates.
10. Time, geographic, complaint, and agency features can provide useful inputs for future predictive analysis.

---

## 📌 Business Recommendations

Based on the analysis, possible areas for further investigation include:

* Prioritizing high-volume complaint categories such as Illegal Parking.
* Identifying geographic hotspots and investigating the complaints driving those areas.
* Adjusting staffing based on demand by hour, day, and season.
* Investigating long-duration requests to understand the agencies and complaint types associated with slower resolution.
* Comparing request volume with population data before making resource-allocation decisions.

---

## 📁 Project Structure

```text
NYC-311-Service-Requests/
│
├── NYC_311_Service_Requests.ipynb
├── Images/
│   ├── Request_Duration_Distribution.jpg
│   ├── Borough_Analysis.jpg
│   ├── Geographic_Distribution.jpg
│   ├── Top_Complaint_Types_Borough.jpg
│   ├── Request_Resolution_Time_Agency.jpg
│   └── Complaint_Types_Resolution_Time.jpg
│
└── README.md
```

---

## 🚀 Future Improvements

Possible next steps for this project include:

* Analyze a larger portion of the NYC 311 dataset.
* Build an interactive dashboard using **Plotly** or **Power BI**.
* Normalize request volume by population.
* Perform deeper spatial analysis using geospatial libraries.
* Build a model to predict request resolution time.
* Predict complaint categories.
* Apply clustering to identify similar service-request patterns.
* Perform time-series analysis to forecast service demand.

---

## 📚 Skills Demonstrated

**Data Analysis**

* Data Cleaning
* Exploratory Data Analysis
* Missing Value Analysis
* Data Aggregation
* Statistical Analysis

**Feature Engineering**

* Date/Time Features
* Resolution Duration
* Geographic Features
* Categorical Features

**Data Visualization**

* Bar Charts
* Histograms
* Heatmaps
* Scatter Plots
* Geographic Visualizations

**Machine Learning Preparation**

* Feature Selection
* Standardization
* One-Hot Encoding
* ColumnTransformer

---

## 👩‍💻 Author

**Sama Tarek**

Computer Science & AI Student
AI Department — Benha University

Interested in **Data Science, Machine Learning, Data Analysis, and practical real-world projects**.
