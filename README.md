# Healthcare Appointment No-Show Prediction

A comprehensive data analytics project that predicts patient no-shows for medical appointments using machine learning and visualizes insights through an interactive Power BI dashboard.

![Power BI Dashboard](dashboard_preview.png)

## 📊 Project Overview

This project analyzes healthcare appointment data to predict patient no-shows and identify key factors contributing to missed appointments. By leveraging **machine learning** (Python) and **business intelligence** (Power BI), healthcare facilities can optimize scheduling, reduce resource waste, and improve patient care.

### Key Objectives
- Predict the likelihood of patient no-shows
- Identify risk factors associated with missed appointments
- Provide actionable insights through interactive dashboards
- Enable data-driven decision-making for healthcare operations

---

## 📈 Dataset Information

- **Source**: Healthcare appointment scheduling system
- **Size**: 106,987 appointments across 60,270 unique patients
- **Time Period**: April - June 2016
- **Target Variable**: `Showed_up` (True/False)

### Dataset Features

| Feature | Description | Type |
|---------|-------------|------|
| PatientId | Unique patient identifier | Numeric |
| AppointmentID | Unique appointment identifier | Numeric |
| Gender | Patient gender (M/F) | Categorical |
| ScheduledDay | Date when appointment was scheduled | Date |
| AppointmentDay | Actual appointment date | Date |
| Age | Patient age in years | Numeric |
| Neighbourhood | Patient's neighborhood | Categorical |
| Scholarship | Whether patient is enrolled in Bolsa Família welfare program | Boolean |
| Hypertension | Whether patient has hypertension | Boolean |
| Diabetes | Whether patient has diabetes | Boolean |
| Alcoholism | Whether patient has alcoholism | Boolean |
| Handicap | Whether patient has Handicap | Boolean |
| SMS_received | Whether SMS reminder was sent | Boolean |
| Showed_up | Whether patient attended appointment (target) | Boolean |

---

## 🔧 Technical Implementation

### Technologies Used

**Data Analysis & Machine Learning:**
- Python 3.x
- pandas - Data manipulation and analysis
- NumPy - Numerical computing
- scikit-learn - Machine learning algorithms
- Matplotlib & Seaborn - Data visualization

**Business Intelligence:**
- Microsoft Power BI - Interactive dashboard creation
- DAX - Data modeling and calculations

### Machine Learning Pipeline

#### 1. Data Preprocessing
```python
# Key preprocessing steps implemented:
- Missing value check (no missing values found)
- Boolean conversion to numeric (0/1)
- Date feature engineering
- Outlier detection and removal (negative Date.diff values)
```

#### 2. Feature Engineering

**Temporal Features:**
- `AppointmentWeekday` - Day of week (0-6)
- `AppointmentMonth` - Month number
- `ScheduledHour` - Hour when appointment was scheduled
- `Date.diff` - Days between scheduling and appointment

**Categorical Features:**
- `Gender_Encoded` - Gender encoding (F=0, M=1)
- `AgeGroup` - Age categories (0-18, 19-30, 31-45, 46-60, 60+)

**Historical Features:**
- `TotalAppointments` - Patient's total appointments
- `TotalShow_ups` - Patient's total show-ups
- `Show_Up_Rate` - Patient's historical show-up rate

**Risk Segmentation:**
- `Date_diff_Group` - Appointment lead time categories
- `RiskCategory` - Patient risk classification (Low/Medium/High)

#### 3. Model Development

**Algorithm**: Decision Tree Classifier

**Hyperparameters:**
```python
DecisionTreeClassifier(
    max_depth=8,
    min_samples_split=100,
    min_samples_leaf=50,
    random_state=42
)
```

**Training Configuration:**
- Train-test split: 80-20
- Random state: 42 (for reproducibility)

**Model Output:**
- `Predicted_Show_up` - Binary prediction (0/1)
- `Show_up_Probability` - Probability score (0-1)
- `RiskCategory` - Risk classification based on probability thresholds

---

## 📊 Key Findings

### Overall Statistics
- **Average Show-up Rate**: 79.77%
- **Average No-Show Rate**: 20.23%
- **Total Appointments**: 106,987
- **Unique Patients**: 60,270

### Critical Insights

#### 1. SMS Reminders Paradox
- **No-Show Rate WITH SMS**: 27.67%
- **No-Show Rate WITHOUT SMS**: 16.73%
- **Interpretation**: SMS reminders were likely sent to high-risk patients, not randomly distributed

#### 2. Age Distribution
The dataset shows variation in show-up probability across age groups:
- Children (0-18): Lower show-up rates (dependent on parent schedules)
- Young Adults (19-30): Moderate show-up rates
- Middle Age (31-60): Higher show-up rates
- Seniors (60+): Highest show-up rates

#### 3. Appointment Lead Time
- **Same-day appointments**: Highest show-up rates
- **1-7 days**: Moderate no-show risk
- **8-30 days**: Increased no-show risk
- **31+ days**: Highest no-show risk

#### 4. Risk Categories Distribution
- **Low Risk** (>80% show-up probability): ~68% of appointments
- **Medium Risk** (50-80% probability): ~27% of appointments
- **High Risk** (<50% probability): ~5% of appointments

#### 5. Day of Week Patterns
Weekday appointments show different patterns, with specific days having higher no-show rates (visible in dashboard)

---

## 📊 Power BI Dashboard

### Dashboard Components

#### KPI Cards
1. **Average Show-up Probability**: 79.77%
2. **No-Show Rate with SMS**: 27.67%
3. **No-Show Rate without SMS**: 16.73%

#### Visualizations

**1. Sum of Showed_up by Risk Category (Donut Chart)**
- Breakdown of show-ups across Low, Medium, and High Risk categories
- Percentage distribution with count values

**2. Count of Age Group by Age Group (Donut Chart)**
- Patient distribution across age segments
- Visual representation of demographic composition

**3. Average Show_up Probability by Age (Scatter Plot)**
- Correlation between patient age and show-up likelihood
- Identifies age-related patterns in attendance

**4. Show-up Probability and Total Appointments by Weekday (Combo Chart)**
- Dual-axis visualization showing:
  - Show-up probability percentage (bars by gender)
  - Total appointments count (line chart)
- Day-of-week analysis for scheduling optimization

**5. Sum of Showed_up by Month and Age Group (Area Chart)**
- Temporal trends across different age segments
- Monthly patterns in appointment attendance

### Interactive Features
- Cross-filtering across all visuals
- Dynamic tooltips with detailed metrics
- Gender-based segmentation
- Time-based filtering

---

## 🚀 Getting Started

### Prerequisites

```bash
Python 3.8+
Jupyter Notebook or JupyterLab
Microsoft Power BI Desktop (for dashboard)

```
- pandas>=1.5.0
- numpy>=1.23.0
- scikit-learn>=1.1.0
- matplotlib>=3.5.0
- seaborn>=0.12.0
- jupyter>=1.0.0

## 💡 Use Cases

### Healthcare Administrators
- **Optimize scheduling**: Reduce appointment slots for high-risk patients
- **Resource allocation**: Better staff and facility planning
- **Reminder systems**: Target SMS reminders to high-risk patients

### Data Analysts
- **Pattern identification**: Discover hidden trends in no-show behavior
- **Predictive insights**: Forecast no-show rates for planning
- **Performance monitoring**: Track metrics over time

### Healthcare Providers
- **Patient engagement**: Identify patients needing additional support
- **Revenue optimization**: Reduce losses from no-shows
- **Quality improvement**: Better patient care through improved attendance

---

## 🔍 Model Performance Insights

The Decision Tree model provides:
- **Interpretability**: Easy to understand decision rules
- **Feature importance**: Identifies key predictive factors
- **Probability scores**: Enables risk-based segmentation
- **Actionable outputs**: Direct integration with operational systems

### Key Predictive Features
1. Historical show-up rate (`Show_Up_Rate`)
2. Appointment lead time (`Date.diff`)
3. Age and age group
4. SMS reminder status
5. Day of week and month
6. Patient demographics

---

## 📋 Future Enhancements

### Potential Improvements
- [ ] **Advanced ML models**: XGBoost, Random Forest, Neural Networks
- [ ] **Hyperparameter tuning**: Grid search for optimal parameters
- [ ] **Real-time predictions**: API deployment for live scoring
- [ ] **A/B testing framework**: Test intervention strategies
- [ ] **Geographical analysis**: Neighborhood-level insights
- [ ] **Cost-benefit analysis**: ROI calculation for interventions
- [ ] **Automated reporting**: Scheduled dashboard refreshes
- [ ] **Mobile app integration**: Patient reminder system

