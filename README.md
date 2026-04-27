# Data Manipulation & Visualization

> A concise guide for Data Engineering & Analysis students

---

## Table of Contents

- [What is Data Manipulation?](#what-is-data-manipulation)
- [Core Manipulation Tasks](#core-manipulation-tasks)
- [Main Tools](#main-tools)
- [What is Data Visualization?](#what-is-data-visualization)
- [Chart Types](#chart-types)
- [Visualization Tools](#visualization-tools)
- [Full Workflow](#full-workflow)
- [Python Example](#python-example)
- [Career Relevance](#career-relevance)

---

## What is Data Manipulation?

**Transforming raw data into a clean, useful format** before analysis or visualization.

> Think of it like cooking — raw ingredients (data) need to be cleaned, cut, and prepared before serving.

---

## Core Manipulation Tasks

### 1. 🧹 Cleaning

Fixing messy, incomplete, or incorrect data.

```python
df.dropna()            # remove missing values
df.fillna(0)           # fill missing with 0
df.drop_duplicates()   # remove duplicate rows
df['age'] = df['age'].astype(int)  # fix data types
```

---

### 2. 🔍 Filtering & Selecting

Getting only the data you need.

```python
df[df['age'] > 18]       # filter rows by condition
df[['name', 'age']]      # select specific columns
df.head(10)              # get first 10 rows
```

---

### 3. 🔄 Transforming

Changing format or creating new columns.

```python
df['salary_k'] = df['salary'] / 1000
df['full_name'] = df['first'] + ' ' + df['last']
df['score_scaled'] = (df['score'] - df['score'].min()) / (df['score'].max() - df['score'].min())
```

---

### 4. 📦 Aggregating & Grouping

Summarizing data by category.

```python
df.groupby('city')['sales'].sum()     # total sales per city
df.groupby('dept')['salary'].mean()   # average salary per dept
df.groupby('grade').agg({'score': ['min', 'max', 'mean']})
```

---

### 5. 🔗 Merging & Joining

Combining multiple tables — like SQL `JOIN`.

```python
pd.merge(df1, df2, on='id', how='inner')   # inner join
pd.merge(df1, df2, on='id', how='left')    # left join
pd.concat([df1, df2], ignore_index=True)   # stack rows
```

---

### 6. 🔢 Sorting & Ranking

```python
df.sort_values('score', ascending=False)
df['rank'] = df['score'].rank(ascending=False)
```

---

## Main Tools

| Tool | Language | Best For |
|------|----------|----------|
| **Pandas** | Python | General data manipulation |
| **NumPy** | Python | Numerical computation |
| **SQL** | SQL | Database querying |
| **PySpark** | Python | Big data processing |
| **dbt** | SQL | Data transformation pipelines |

---

## What is Data Visualization?

**Representing data visually** so patterns, trends, and insights are easy to understand.

> *"A picture is worth a thousand rows of data."*

Good visualization answers questions like:
- What is the trend over time?
- Which category performs best?
- Is there a relationship between two variables?

---

## Chart Types

| Chart Type | Use When | Example |
|------------|----------|---------|
| **Bar Chart** | Comparing categories | Sales by country |
| **Line Chart** | Showing trends over time | Revenue per month |
| **Pie / Donut** | Showing proportions | Market share % |
| **Scatter Plot** | Finding relationships | Age vs. Salary |
| **Histogram** | Distribution of values | Student score ranges |
| **Heatmap** | Correlation between variables | Feature correlation matrix |
| **Box Plot** | Spotting outliers | Salary range by department |
| **Area Chart** | Cumulative trends | Total users over time |

---

## Visualization Tools

### Python Libraries

```
Matplotlib   →  Basic, full control over every detail
Seaborn      →  Statistical plots, beautiful defaults
Plotly       →  Interactive, web-friendly charts
Pandas.plot  →  Quick and simple, built-in with Pandas
```

### BI Tools (No Code / Low Code)

```
Power BI   →  Microsoft ecosystem, great for business
Tableau    →  Drag & drop, very powerful dashboards
Looker     →  Cloud-based (Google), used in enterprises
Metabase   →  Open source, easy to set up
```

---

## Full Workflow

```
Raw Data
   │
   ▼
[Collect]      →  CSV, Database, API, Web Scraping
   │
   ▼
[Clean]        →  Handle nulls, fix types, remove duplicates
   │
   ▼
[Manipulate]   →  Filter, group, merge, transform
   │
   ▼
[Analyze]      →  Find patterns, statistics, trends
   │
   ▼
[Visualize]    →  Charts, dashboards, reports
   │
   ▼
[Insights]     →  Make decisions 💡
```

---

## Python Example

A complete end-to-end example combining manipulation and visualization.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# ── Load Data ──────────────────────────────────────────
df = pd.read_csv('students.csv')

# ── Manipulation ───────────────────────────────────────
df.dropna(inplace=True)                    # clean nulls
df = df[df['score'] >= 0]                  # filter valid scores

df['grade'] = df['score'].apply(           # transform → create grade
    lambda x: 'A' if x >= 90 else
              'B' if x >= 80 else
              'C' if x >= 70 else 'D'
)

avg_by_grade = (                           # aggregate
    df.groupby('grade')['score']
      .mean()
      .reset_index()
      .sort_values('grade')
)

# ── Visualization ──────────────────────────────────────
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Bar chart
sns.barplot(data=avg_by_grade, x='grade', y='score',
            palette='Blues_d', ax=axes[0])
axes[0].set_title('Average Score by Grade')
axes[0].set_xlabel('Grade')
axes[0].set_ylabel('Average Score')

# Distribution
sns.histplot(df['score'], bins=10, kde=True,
             color='steelblue', ax=axes[1])
axes[1].set_title('Score Distribution')
axes[1].set_xlabel('Score')

plt.tight_layout()
plt.show()
```

---

## Career Relevance

As a future **Data Engineer & Data Analyst**, here is how these skills apply:

| Role | Focus | Key Tools |
|------|-------|-----------|
| **Data Engineer** | Manipulation — pipelines, cleaning, transforming large datasets | SQL, Spark, dbt, Pandas |
| **Data Analyst** | Visualization — dashboards, reports, insights for business | Tableau, Power BI, Plotly |
| **Both Roles** | Need strong foundations in both ✅ | All of the above |

---

## Key Takeaway

| | Data Manipulation | Data Visualization |
|--|---|---|
| **Goal** | Make data clean & structured | Make data understandable |
| **Output** | Clean dataset / table | Charts / Dashboards |
| **Tools** | Pandas, SQL, Spark | Matplotlib, Tableau, Power BI |
| **Core Skill** | Logic & coding | Design & storytelling |

> Master both, and you become a powerful data professional. 💪

---

*Notes by RUPP — Data Science & Engineering, Generation 4*
