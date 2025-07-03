# 📊 Social Media Addiction vs Relationships – Data Analysis

This project explores a one-time survey dataset that examines the connection between students' social media usage and its effects on their **sleep**, **mental health**, **academic performance**, and **relationships**.

🔗 **Dataset Source**:  
[Social Media Addiction vs Relationships (Kaggle)](https://www.kaggle.com/datasets/adilshamim8/social-media-addiction-vs-relationships)
### **[View Interactive Dashboard](https://public.tableau.com/views/ocialMediaUseandItsImpactonRelationshipsWellbeing/Dashboard1?:language=en-GB&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**  
Explore platform preferences, screen time, relationship status, and mental health metrics across different age groups and genders.


---

## Objective

To analyze how social media addiction relates to:
- Daily usage and sleep patterns
- Mental health scores
- Conflict in relationships
- Academic performance
- Most used social platforms by age and gender
- Country distribution of respondents

---

## Tools Used

- Python 
- Pandas
- Seaborn
- Matplotlib
- Tableau

---

## Dataset Overview

- Age Range: 16–25
- Survey Participants: 705 students
- Academic Levels: High School, Undergraduate, Graduate
- Countries: Multiple

---

## Code

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
df = pd.read_csv('/Users/vernesapodrimaj/Downloads/Students Social Media Addiction.csv')

# Basic info
print('Dataset Information:')
df.info()

print('Dataset description:')
print(df.describe())

print('Check for Null Values:')
print(df.isnull().sum())

# Countries and respondent count
print('Unique Countries:', df['Country'].unique())
top_countries = df['Country'].value_counts().head(10)
top_countries.plot(kind='bar', figsize=(10,6), title='Top 10 Countries by Respondent Count')
plt.ylabel('Number of Respondents')
plt.xlabel('Country')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Relationship status count
df['Relationship_Status'].value_counts().plot(kind='bar', title='Relationship Status Count')
plt.ylabel('Number of Respondents')
plt.xlabel('Relationship Status')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Usage vs Sleep
sns.scatterplot(data=df, x='Avg_Daily_Usage_Hours', y='Sleep_Hours_Per_Night')
plt.title('Social Media Usage vs Sleep Hours')
plt.tight_layout()
plt.show()

# Most used platforms overall
df['Most_Used_Platform'].value_counts().plot(kind='bar', title='Most Used Social Media Platforms')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Most used platform by age group
df['Age_Group'] = pd.cut(df['Age'], bins=[15, 18, 21, 25], labels=['16-18', '19-21', '22-25'])

plt.figure(figsize=(10,6))
sns.countplot(data=df, x='Most_Used_Platform', hue='Age_Group')
plt.title("Most Used Platform by Age Group")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Most used platform by gender
sns.countplot(data=df, x='Most_Used_Platform', hue='Gender')
plt.title("Most Used Platform by Gender")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Usage vs Mental Health
sns.scatterplot(data=df, x='Avg_Daily_Usage_Hours', y='Mental_Health_Score')
plt.title('Daily Usage vs Mental Health Score')
plt.tight_layout()
plt.show()

# Conflict by relationship status
sns.boxplot(x='Relationship_Status', y='Conflicts_Over_Social_Media', data=df)
plt.title('Conflicts Over Social Media by Relationship Status')
plt.tight_layout()
plt.show()

# Correlation Heatmap
numeric_cols = df.select_dtypes(include='number')
sns.heatmap(numeric_cols.corr(), annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.tight_layout()
plt.show()
