# Project Overview

This project explores the Data Science job market in India using Python. The analysis focuses on understanding job market trends, salary distributions, and the skills employers are looking for across different data-related roles.

The goal is to identify which skills are most in demand, which skills offer higher salaries, and what skills are worth learning for someone pursuing a career in data analytics.

### Objectives

- Identify the top 5 most in-demand skills for Data Analysts, Data Engineers, and Data Scientists.
- Analyze and compare median salaries across these three job roles.
- Explore the highest-paying and most frequently requested skills for Data Analysts.
- Identify optimal skills by comparing salary potential with job demand.

### Tools & Technologies

- **Python** – Programming language
- **Pandas** – Data cleaning and manipulation
- **Matplotlib** – Data visualization
- **Seaborn** – Statistical data visualization
- **Jupyter Notebook** – Data analysis and exploration

### Dataset

The project uses the [Data Jobs Dataset](https://huggingface.co/datasets/lukebarousse/data_jobs), containing job titles, salaries, locations, work arrangements, and required skills.
# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View  My notebook with detailed steps here:
View my notebook with detailed steps here:

[2. Skills Count Analysis](2_Skills_Count.ipynb)
### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc
        ['job_title_short'] == job_title].head(5)[::-1]

    sns.barplot(
        data=df_plot,
        x='skill_percent',
        y='job_skills',
        ax=ax[i],
        hue='skill_count',
        palette='dark:b_r'
    )

plt.show()
```

### Results

### Results

![Visualization of Top Skills for Data Roles](images/skill_demand_all_dateroles.png)
### Insights

💡

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).

- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).

# The Analysis

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python
from matplotlib.ticker import PercentFormatter

df_plot = df_DA_India_percent.iloc[:, :5]

sns.lineplot(
    data=df_plot,
    dashes=False,
    legend='full',
    palette='tab10'
)

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```


### Results



![Trending Top Skills for Data Analysts in India](images/skill_trend.png)

*Bar graph visualizing the trending top skills for data analysts in India in 2023.*

### Insights:

- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.
- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

# The Analysis


## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

### Visualize Data

```python
sns.boxplot(
    data=df_India_top6,
    x='salary_year_avg',
    y='job_title_short',
    order=job_order
)

ticks_x = plt.FuncFormatter(lambda y, pos: f'₹{int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
### Results

![Salary Distributions in India](images/salary_box_plot.png)

*Box plot visualizing the salary distributions for the top 6 data job titles in India.*

#### Insights

- There's a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to ₹600K, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

💡

- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.
# The Analysis

### 3. How well do jobs and skills pay for Data Analysts?

### Highest Paid & Most Demanded Skills for Data Analysts in India

### Visualize Data

```python
fig, ax = plt.subplots(2, 1)

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(
    data=df_DA_top_pay,
    x='median',
    y=df_DA_top_pay.index,
    hue='median',
    ax=ax[0],
    palette='dark:b_r'
)
ax[0].legend().remove()

# Original code:
# df_DA_top_pay[::-1].plot(kind='barh', y='median', ax=ax[0], legend=False)

ax[0].set_title('Top 10 Highest Paid Skills for Data Analysts in India')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(
    plt.FuncFormatter(lambda x, _: f'₹{int(x/1000)}K')
)

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(
    data=df_DA_skills,
    x='median',
    y=df_DA_skills.index,
    hue='median',
    ax=ax[1],
    palette='light:b'
)
ax[1].legend().remove()

# Original code:
# df_DA_skills[::-1].plot(kind='barh', y='median', ax=ax[1], legend=False)

ax[1].set_title('Top 10 Most In-Demand Skills for Data Analysts in India')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (INR)')

# Set the same x-axis limits as the first plot
ax[1].set_xlim(ax[0].get_xlim())

ax[1].xaxis.set_major_formatter(
    plt.FuncFormatter(lambda x, _: f'₹{int(x/1000)}K')
)

plt.tight_layout()
plt.show()
```
### Results

![Highest Paid and Most In-Demand Skills for Data Analysts in India](images/HighestPaid%20and%20Most_In_demand_skills_for_data_analysts%20_In%20_the_India.png)

*Two bar graphs visualizing the highest-paid and most in-demand skills for Data Analysts in India.*
### Insights

- The top graph shows specialized technical skills like `dplyr`, `Bitbucket`, and `GitLab` are associated with higher salaries, some reaching up to ₹200K, suggesting that advanced technical proficiency can increase earning potential.

- The bottom graph highlights that foundational skills like `Excel`, `PowerPoint`, and `SQL` are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data Analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.
# The Analysis

## 4. What is the most optimal skill to learn for Data Analysts?

### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(
    df_DA_skills_high_demand['skill_percent'],
    df_DA_skills_high_demand['median_salary']
)

plt.show()
```


### Results



![Most Optimal Skills for Data Analysts in India](./images/Most_Optimal_Skills_for_Data_Analysts_in_India.png)

*A scatter plot visualizing the most optimal skills (high-paying and high-demand) for data analysts in India.*
### Insights

- The scatter plot shows that most of the `programming` skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the data analytics field.

- Analyst tools (colored green), including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

- The database skills (colored orange), such as Oracle and SQL Server, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data management and manipulation expertise in the industry.