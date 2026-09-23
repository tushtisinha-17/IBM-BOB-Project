# Student Performance Analysis

A Python project that loads, cleans, analyses, and models a dataset of 1,000,000 student records to understand and predict academic performance.

---

## Project Structure

```
student_performance_project/
├── app.py                          # Streamlit web application
├── project.ipynb                   # End-to-end analysis notebook
├── requirements.txt                # Python dependencies
├── student_performance_dataset.csv # Dataset (1 M rows)
├── model_artifacts/
│   └── rf_model.joblib             # Trained Random Forest model
└── utils/
    ├── data_loader.py              # Load, inspect, and clean data
    ├── analysis.py                 # Descriptive statistics and insights
    ├── charts.py                   # Matplotlib / Seaborn chart helpers
    └── model.py                    # ML pipeline, training, evaluation, prediction
```

---

## Dataset
📥 **Source:** [Student Performance Dataset — Kaggle](https://www.kaggle.com/datasets/rabieelkharoua/students-performance-dataset)

The dataset is also included locally as `student_performance_dataset.csv` (1,000,000 rows, 9 columns).

| Column | Type | Description |
|---|---|---|
| `student_id` | int | Unique student identifier |
| `age` | int | Student age (18–24) |
| `gender` | str | Male / Female |
| `study_hours_per_day` | float | Daily study hours (0–8) |
| `attendance_percentage` | float | Class attendance % (60–100) |
| `sleep_hours` | float | Daily sleep hours |
| `internet_usage_hours` | float | Daily internet usage hours |
| `exam_score` | float | Final exam score (0–100) |
| `performance_level` | str | Poor / Average / Good / Excellent |

---

## Setup

```bash
# 1. Clone / download the project folder
cd student_performance_project

# 2. (Recommended) create a virtual environment
python -m venv .venv
.venv\Scripts\activate        # Windows
# source .venv/bin/activate   # macOS / Linux

# 3. Install dependencies
pip install -r requirements.txt
```

---

## Usage

### Streamlit App (interactive dashboard)

```bash
streamlit run app.py
```

Opens at **http://localhost:8501** with five pages:

| Page | Content |
|---|---|
| 📋 Dataset Overview | Shape, data types, missing values, descriptive statistics |
| 📊 Exploratory Analysis | Grouped tables, top/bottom students, gender breakdown, key insights |
| 📈 Visual Insights | 9 charts — pie, bar, scatter, heatmap, boxplot |
| 🤖 ML Model | Accuracy, F1, confusion matrix, feature importances, CV scores |
| 🔮 Predict Student | Enter student attributes → instant performance prediction |

### Jupyter Notebook (step-by-step analysis)

```bash
jupyter notebook project.ipynb
```

The notebook covers every stage end-to-end: data loading → cleaning → EDA → visualisation → model training → evaluation → insights.

---

## Machine Learning Model

- **Algorithm:** Random Forest Classifier (200 trees, `StandardScaler` pipeline)
- **Features:** age, study_hours_per_day, attendance_percentage, sleep_hours, internet_usage_hours, exam_score
- **Target:** performance_level (Poor / Average / Good / Excellent)
- **Split:** 80 % train / 20 % test, stratified
- **Validation:** 5-fold stratified cross-validation

| Metric | Score |
|---|---|
| Test Accuracy | 100 % |
| Weighted F1 | 1.00 |
| CV Mean F1 (5-fold) | 1.00 |

> The model achieves perfect scores because performance level is deterministically derived from exam score thresholds in this dataset. Study hours is the second-most important feature.

---

## Key Findings

- **Study hours** is the strongest predictor of exam score (correlation ~0.97).
- Students studying **6+ h/day** average ~80 points vs ~40 for those studying under 3 h/day.
- **Attendance** shows a positive but weaker effect (+8 points across the full range).
- **Sleep hours** and **internet usage** have minimal correlation with performance.
- **Gender** has no meaningful difference in outcomes.
- **32 %** of students are rated Poor; only **7.6 %** reach Excellent.

---

## Dependencies

| Package | Min version | Purpose |
|---|---|---|
| streamlit | 1.32 | Web application |
| pandas | 2.0 | Data manipulation |
| numpy | 1.26 | Numerical computing |
| scikit-learn | 1.4 | Machine learning |
| matplotlib | 3.8 | Plotting |
| seaborn | 0.13 | Statistical visualisation |
| joblib | 1.3 | Model persistence |
| notebook | 7.0 | Jupyter Notebook |
| ipykernel | 6.29 | Notebook kernel |
