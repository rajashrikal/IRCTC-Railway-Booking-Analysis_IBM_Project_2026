# IRCTC Railway Booking, Fare and Availability Analysis Using Python

### **IBM SkillsBuild Data Analytics with AI Academic Internship Program**
**Conducted by BharatCares in association with AICTE**

---

## Project Overview

This project presents an end-to-end data analytics, statistical investigation, and predictive modeling study on Indian Railways scheduling, passenger tariff structures, and seat availability dynamics. Utilizing empirical records from **326,643 pricing/booking observations** across **533 train services** and a schedule database of **3,292 train timetables**, this analysis uncovers critical operational bottlenecks, pricing yield variations across travel classes, and route congestion patterns across India's rail network.

---

## Problem Statement

Indian Railways operates one of the world's most extensive rail transit systems, handling millions of passenger journeys every day. However, managing passenger demand across varied travel classes (AC First, AC 2-Tier, AC 3-Tier, Sleeper, Chair Car, and Second Sitting) alongside distance-based tariff slabs creates operational challenges:
- **Acute Capacity Imbalances:** High demand on overnight long-distance routes leads to extreme waitlisting, while day-train seating services experience underutilized capacity.
- **Fare Breakdown Disparities:** Complex fare composition involving distance-tiered base fares, class-specific reservation fees, superfast levies, service tax/GST, and dynamic flexi-fares requires transparent modeling.
- **Route Bottlenecks:** Key junction terminuses face severe route concentration, impacting operational turnaround times.

This project provides an empirical, data-driven framework to analyze these operational challenges and build predictive machine learning models for fare estimation.

---

## Objectives

1. **Understand Dataset Architecture:** Inspect structural schemas, column types, and data completeness across pricing and scheduling datasets.
2. **Clean & Preprocess Data:** Identify and mathematically resolve scraping anomalies (e.g., negative duration wrap-arounds from midnight rollovers) and trim string data.
3. **Perform Feature Engineering:** Derive analytical features such as travel duration in hours, tariff yield per kilometer (`fare_per_km`), operating speed (`speed_kmh`), and standardized availability categories.
4. **Conduct Exploratory Data Analysis:** Visualize fare distributions, route congestion, availability pressure, and station hubs using publication-grade charts.
5. **Analyze Train & Route Operations:** Evaluate origin and destination concentration, route-level journey durations, and fleet classification.
6. **Benchmark Machine Learning Models:** Build and evaluate supervised regression models (Linear Regression vs. Random Forest Regressor) to predict passenger ticket fares.
7. **Deliver Actionable Recommendations:** Provide practical strategies for capacity rebalancing, dynamic pricing, and terminal decongestion.

---

## Dataset

- **Source:** Kaggle – Indian Railways Schedule-Prices-Availability Data (by Bhavyaraj Dev)
- **URL:** [https://www.kaggle.com/datasets/bhavyarajdev/indian-railways-schedule-prices-availability-data](https://www.kaggle.com/datasets/bhavyarajdev/indian-railways-schedule-prices-availability-data)
- **Files Used:**
  1. `price_data.csv`: 326,643 rows × 19 columns containing base fare, breakdown fees, seat availability strings, station codes, distance, and duration.
  2. `schedules.csv`: 3,292 rows × 13 columns containing train numbers, official names, terminal origin/destination stations, day-of-week operating flags, and intermediate station itineraries.

---

## Technologies Used

- **Programming Language:** Python 3.12
- **Data Manipulation & Computation:** Pandas (v3.0.2), NumPy (v2.4.4)
- **Data Visualization:** Matplotlib (v3.10.8), Seaborn (v0.13.2)
- **Machine Learning:** Scikit-learn (v1.8.0)
- **Document Generation:** Python-docx (v1.2.0)
- **Interactive Development:** Jupyter Notebook / IPython Kernel

---

## Project Structure

```
IRCTC Railway Booking Analysis/
├── price_data.csv                                     # Kaggle pricing and availability dataset
├── schedules.csv                                      # Kaggle train timetable and schedule dataset
├── RajashriKalshetti_IRCTC Railway Booking Analysis.ipynb  # Executed, 25-section Jupyter Notebook
├── requirements.txt                                   # Pinned Python package dependencies
├── RajashriKalshetti_ProjectReport.docx              # Academic internship project report (2.7 MB)
├── README.md                                          # Project documentation and summary
├── charts/                                            # 14 high-resolution exported figures
│   ├── 01_fare_distribution_by_class.png
│   ├── 02_fare_vs_distance_by_class.png
│   ├── 03_journey_duration_distribution.png
│   ├── 04_seat_availability_status.png
│   ├── 05_top_origin_stations.png
│   ├── 06_top_destination_stations.png
│   ├── 07_fare_per_km_by_class.png
│   ├── 08_availability_rate_by_class.png
│   ├── 09_train_types_distribution.png
│   ├── 10_distance_vs_duration_speed.png
│   ├── 11_fare_components_breakdown.png
│   ├── 12_correlation_matrix.png
│   ├── 13_ml_actual_vs_predicted.png
│   └── 14_ml_feature_importance.png
└── analysis_summary.json                              # Exact empirical audit metrics and results
```

---

## Installation

1. **Clone or Download the Repository:**
   ```bash
   git clone <repo-url>
   cd "IRCTC Railway Booking Analysis"
   ```

2. **Set up a Virtual Environment (Recommended):**
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On Linux/macOS:
   source venv/bin/activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

---

## How to Run

1. **Verify Datasets:** Ensure `price_data.csv` and `schedules.csv` are located in the project root directory.
2. **Launch Jupyter Notebook:**
   ```bash
   jupyter notebook "RajashriKalshetti_IRCTC Railway Booking Analysis.ipynb"
   ```
3. **Run All Cells:** Click **Kernel -> Restart & Run All** to reproduce all computations, tables, visual plots, and machine learning evaluations.

---

## Analysis Performed

1. **Data Quality Audit:** Complete verification of dataset shapes (326,643 × 19 and 3,292 × 13), 0 null values, 0 duplicate rows, and statistical percentiles.
2. **Data Cleaning & Anomaly Correction:** Corrected 189 negative duration records caused by midnight crossovers using a `+1440` minute modular adjustment, restoring valid transit times.
3. **Availability Parsing:** Extracted standardized booking statuses from embedded JSON strings into `Waitlist` (63.1%), `Available` (31.3%), `Regret` (2.0%), `Not Available` (1.6%), `RAC` (1.4%), and `Cancelled` (0.7%).
4. **Tariff Density & Class Benchmarking:** Evaluated per-kilometer yields ranging from ₹1.29/km in Second Sitting to ₹8.44/km in AC First Class.
5. **Fleet & Route Breakdown:** Classified trains into Express (74.2%), Superfast (8.8%), Special (5.1%), and premium categories across 74,615 distinct station pairs.
6. **Correlation Analysis:** Analyzed linear relationships confirming that base fare (\(r = 0.99\)), reservation charges (\(r = 0.69\)), and distance (\(r = 0.63\)) dictate total fare.

---

## Machine Learning

- **Task:** Supervised Regression (Passenger Total Fare Prediction)
- **Target Variable:** `totalFare` (INR ₹)
- **Features Used:** `distance`, `duration_clean`, `reservationCharge`, `superfastCharge`, `classCode` (One-Hot Encoded)
- **Dataset Split:** 80% Training (261,314 samples), 20% Testing (65,329 samples), `random_state=42`
- **Models Benchmarked:**
  1. **Linear Regression (Baseline)**
  2. **Random Forest Regressor (Ensemble)**

### Model Evaluation Results:

| Metric | Linear Regression | Random Forest Regressor | Performance Gain |
| :--- | :---: | :---: | :---: |
| **Mean Absolute Error (MAE)** | ₹224.60 | **₹41.75** | 81.4% Error Reduction |
| **Mean Squared Error (MSE)** | 111,835.64 | **12,265.60** | 89.0% Variance Reduction |
| **Root Mean Squared Error (RMSE)** | ₹334.42 | **₹110.75** | 66.9% Deviation Reduction |
| **Coefficient of Determination (\(R^2\))** | 0.8525 | **0.9838** | Explains 98.38% of Variance |

- **Feature Importance:** `reservationCharge` (44.6%) and `distance` (44.4%) represent the primary drivers of total passenger fares.

---

## Key Findings

1. **Severe Waitlisting on Budget Long-Hauls:** Sleeper (70.0%) and AC 3-Tier (66.5%) experience heavy waitlist concentration, signaling chronic capacity deficits.
2. **Underutilized Day Seating:** Second Sitting (78.0% confirmation) and Chair Car (68.5% confirmation) show surplus availability suitable for short-haul inter-city marketing.
3. **Cross-Subsidization Structure:** AC First Class yields ₹8.44/km, directly cross-subsidizing mass transit in Sleeper (₹1.51/km) and Second Sitting (₹1.29/km).
4. **Base Fare Predominance:** Base fare constitutes 89.0% (mean ₹890.1) of total passenger fare, with ancillary fees acting as minor increments.
5. **Predictable Deterministic Tariffs:** Random Forest accurately models railway tariff distance slabs with an \(R^2\) of 0.9838.

---

## Limitations

1. **Historical Snapshot Data:** The dataset is a point-in-time snapshot and does not capture dynamic seasonal spikes (e.g., Diwali or holiday travel surges).
2. **No Passenger Demographics:** Lacks individual passenger attributes such as age, gender, travel purpose, or booking channel.
3. **Absence of Final PNR Confirmations:** Cancellation logs and final cleared chart records are not tracked in the dataset.
4. **Tariff Focus:** Measures individual ticket fares rather than train-level or coach-level gross passenger revenue.

---

## Future Scope

1. **Dynamic PNR Confirmation Forecasting:** Training deep learning models on historical PNR clearing trajectories.
2. **Real-Time Punctuality & Delay Forecasting:** Integrating weather radar and live GPS tracking telemetry to predict delays.
3. **Interactive BI Dashboards:** Deploying Streamlit or Power BI apps for interactive route fare and availability queries.
4. **Rake Composition Optimization:** Applying mathematical linear programming to optimize rolling stock coach allocation based on route demand.

---

## Author

**Rajashri Kalshetti**  
Data Analytics Intern  
IBM SkillsBuild Data Analytics with AI Academic Internship Program  
Conducted by BharatCares in association with AICTE
