# Student Habits and Academic Performance Analysis

## Overview

This project is an exploratory data analysis (EDA) project that analyzes how student habits and lifestyle factors relate to academic performance. The analysis focuses on understanding patterns in study time, sleep duration, social media usage, Netflix consumption, attendance, part-time work, mental health, parental education level, and exam scores.

The project was developed as part of a data analysis portfolio to demonstrate data cleaning, exploratory analysis, visualization, and insight generation using Python.

## Objectives

The main objectives of this project are:

- Explore the structure and characteristics of the student performance dataset.
- Identify missing values, duplicate records, irrelevant categories, and potential outliers.
- Visualize the distribution of numerical and categorical variables.
- Analyze relationships between student habits and exam scores.
- Generate practical insights about factors that may influence academic performance.

## Dataset

The dataset used in this project is `student_habits_performance.csv`.

The dataset contains 1,000 student records with 16 variables, including:

| Column | Description |
|---|---|
| `student_id` | Unique student identifier |
| `age` | Student age |
| `gender` | Student gender |
| `study_hours_per_day` | Average daily study hours |
| `social_media_hours` | Average daily social media usage |
| `netflix_hours` | Average daily Netflix watching duration |
| `part_time_job` | Whether the student has a part-time job |
| `attendance_percentage` | Class attendance percentage |
| `sleep_hours` | Average sleep duration |
| `diet_quality` | Student diet quality |
| `exercise_frequency` | Exercise frequency |
| `parental_education_level` | Parents' education level |
| `internet_quality` | Internet quality |
| `mental_health_rating` | Mental health rating |
| `extracurricular_participation` | Whether the student participates in extracurricular activities |
| `exam_score` | Student exam score |

## Tools and Libraries

This project uses the following tools and libraries:

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Seaborn

## Project Workflow

### 1. Data Loading

The dataset is loaded from Google Drive using Google Colab.

```python
from google.colab import drive
drive.mount('/content/drive')

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv("/content/drive/MyDrive/MCI/student_habits_performance.csv")
```

### 2. Initial Data Exploration

The first step is to understand the dataset structure using:

- `data.info()`
- `data.describe()`
- `data.shape`
- `data.isnull().sum()`
- categorical value counts

This step helps identify data types, missing values, numerical summaries, and category distributions.

### 3. Data Cleaning

Several cleaning steps are performed before deeper analysis.

#### Missing Values

The `parental_education_level` column contains missing values. These values are filled with `Unknown` to preserve the records.

```python
data['parental_education_level'] = data['parental_education_level'].fillna('Unknown')
```

#### Irrelevant Category Handling

Rows with `gender = Other` are removed to simplify the gender-based analysis.

```python
data = data[data['gender'] != 'Other']
```

#### Outlier Treatment

Outliers in numerical columns are detected using the Interquartile Range (IQR) method. Then, winsorizing is applied by clipping values outside the lower and upper bounds.

```python
Q1 = data[col].quantile(0.25)
Q3 = data[col].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

data[col] = data[col].clip(lower=lower_bound, upper=upper_bound)
```

#### Duplicate Checking

The project checks for:

- Fully duplicated rows
- Duplicate `student_id` values

This step ensures that the dataset does not contain repeated student records that could bias the analysis.

## Exploratory Data Analysis

### Correlation Analysis

A correlation heatmap is used to examine relationships among numerical variables.

```python
corr = data.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
```

### Numerical Variable Distribution

Histograms are used to observe the distribution of numerical variables such as age, study hours, social media usage, Netflix hours, attendance, sleep hours, exercise frequency, mental health rating, and exam score.

### Categorical Variable Distribution

Count plots are created for categorical variables, including:

- Gender
- Part-time job status
- Extracurricular participation
- Parental education level
- Diet quality
- Internet quality

Each plot includes percentage labels to make category proportions easier to interpret.

## Key Analysis and Insights

### 1. Study Hours and Exam Score

A scatter plot is used to analyze the relationship between daily study hours and exam scores.

**Insight:**  
Students who study more than 5 hours per day tend to achieve exam scores above 80. This suggests that higher study duration is generally associated with better academic performance.

### 2. Sleep Hours and Exam Score

A line plot is used to observe the relationship between sleep duration and exam scores.

**Insight:**  
Students with very low sleep duration, especially below 5 hours per day, tend to have lower exam scores. Students who sleep around 6 to 8 hours show more stable academic performance. However, sleeping too long does not always lead to better results.

### 3. Social Media Usage and Exam Score

Social media usage is grouped into three levels:

- Low
- Medium
- High

A boxplot is used to compare exam scores across these groups.

**Insight:**  
Higher social media usage tends to be associated with lower exam scores. This indicates that excessive social media use may negatively affect academic performance.

### 4. Mental Health and Exam Score

A bar plot is used to analyze average exam scores based on mental health ratings.

**Insight:**  
Mental health appears to be an important factor related to academic performance. Students with better mental health ratings tend to show better academic outcomes.

### 5. Part-Time Job and Extracurricular Participation

A categorical bar plot is used to compare exam scores based on part-time job status and extracurricular participation.

**Insight:**  
This analysis helps evaluate whether academic performance differs between students who work part-time and those who participate in extracurricular activities.

### 6. Parental Education Level and Exam Score

A bar plot is used to compare average exam scores across different parental education levels.

**Insight:**  
Parental education level may have a relationship with student performance, although further statistical testing would be needed to confirm the strength of this relationship.

### 7. Netflix Hours and Exam Score

A line plot is used to analyze the relationship between Netflix watching duration and exam scores.

**Insight:**  
Students who spend more time watching Netflix tend to show lower exam scores on average. This suggests that excessive entertainment screen time may reduce study effectiveness or academic focus.

## Main Findings

Based on the exploratory analysis, several important patterns were identified:

- Higher study hours are generally associated with better exam scores.
- Adequate sleep duration, especially around 6 to 8 hours, supports more stable academic performance.
- Excessive social media usage may negatively affect exam scores.
- Higher Netflix consumption tends to be related to lower academic performance.
- Mental health, attendance, and lifestyle habits should be considered when analyzing student performance.
- Data cleaning is important before generating insights, especially for handling missing values, irrelevant categories, and outliers.

## How to Run the Project

1. Clone this repository.

```bash
git clone https://github.com/your-username/your-repository-name.git
```

2. Open the notebook in Google Colab or Jupyter Notebook.

```bash
FP_LAB_MCI.ipynb
```

3. Install or import the required libraries.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

4. Make sure the dataset path is correct.

```python
data = pd.read_csv("student_habits_performance.csv")
```

5. Run the notebook cells sequentially from data loading, cleaning, visualization, and analysis.

## Repository Structure

```text
.
├── FP_LAB_MCI.ipynb
├── student_habits_performance.csv
└── README.md
```

## Possible Improvements

Future improvements for this project include:

- Adding statistical hypothesis testing to validate relationships between variables.
- Building a machine learning model to predict student exam scores.
- Comparing several regression or classification models.
- Improving visualization design and adding more explanatory captions.
- Creating a dashboard using Streamlit, Tableau, Power BI, or Metabase.
- Adding feature importance analysis to identify the most influential factors.

## Conclusion

This project demonstrates a complete basic EDA workflow, starting from data loading, data inspection, data cleaning, outlier handling, visualization, and insight generation. The analysis shows that student academic performance is related to several behavioral and lifestyle factors, including study duration, sleep habits, social media usage, entertainment consumption, mental health, and attendance.

The project is suitable as a beginner-to-intermediate data analytics portfolio project because it highlights practical skills in Python-based data analysis and communicates findings in a clear and structured way.
