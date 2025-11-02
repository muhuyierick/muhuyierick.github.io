---
layout: post
title: "Titanic Exploratory Data Analysis - Uncovering Survival Patterns using Python"
date: 2025-10-10
categories: [data-analysis, python, exploratory-data-analysis, titanic]
author: Muhuyi Erick
---

# Titanic Exploratory Data Analysis - Uncovering Survival Patterns

## Project Overview

As a Data and AI student at Cyber Shujaa, I conducted a comprehensive Exploratory Data Analysis (EDA) on the famous Titanic dataset. This project was designed to help me understand how to systematically examine data, identify patterns, and extract meaningful insights that could explain what factors influenced passenger survival during the tragic Titanic disaster.

## My Step-by-Step Analysis Process

### Step 1: Required Packages and Initial Data Exploration

- I began by importing essential Python libraries, including Pandas for data manipulation, NumPy for numerical computations, and Matplotlib/Seaborn for visualization. I loaded the Titanic dataset and performed initial exploration to understand its structure.
- I used `pd.read_csv()` to load the data, `df.head()` to preview the first rows, `df.shape` to check dimensions (891 passengers, 12 features), `df.info()` to examine data types, and `df.describe()` for statistical summaries. I also checked for duplicates and unique values in each column.
- The dataset contained passenger information, including age, gender, ticket class, fare, and survival status - perfect for understanding what factors influenced survival rates.

### Step 2: Handling Missing Values and Outliers

- I identified and addressed data quality issues, including missing values in the Age (177 missing), Cabin (687 missing), and Embarked (2 missing) columns.
- For Age, I used median imputation (`df['Age'].fillna(df['Age'].median()`) as it's robust to outliers. I dropped the Cabin column due to excessive missing data. For Embarked, I used mode imputation. I detected outliers using boxplots and IQR method, then capped extreme fare values using quantile-based clipping.
- The Challenge I Overcame: Deciding how to handle missing age data was crucial since it represented 20% of the dataset. Median imputation preserved the overall distribution without being skewed by outliers.

### Step 3: Univariate Analysis - Understanding Individual Variables

- I analyzed each variable individually to understand its distribution using histograms, KDE plots, count plots, and pie charts.
- I created histograms with KDE for Age distribution, KDE plots for Fare distribution, count plots for Embarked locations, and pie charts for Gender distribution. I also examined value counts for Passenger Class.
- Key Insights: Most passengers were aged 20-40 years, fare distribution was right-skewed (most paid lower fares), there were more male passengers, and third class was the most common passenger class.

### Step 4: Bivariate Analysis - Exploring Relationships Between Variables

- I examined relationships between two variables to understand how different factors interacted with each other and with survival.
- I created correlation heatmaps for numerical variables, box plots for Fare by Passenger Class, violin plots for Age by Survival, count plots for Survival by Embarked port, and mosaic plots for Pclass vs Survival relationships.
- Key Findings: Higher passenger classes paid significantly more for tickets. Younger passengers had better survival chances. Embarkation port influenced survival rates, with Cherbourg passengers having higher survival.

### Step 5: Multivariate Analysis - Complex Pattern Discovery

- I combined multiple variables to uncover more complex patterns and interactions using advanced visualization techniques.
- Used pair plots with survival hue to see multiple variable interactions simultaneously. Created FacetGrids for Age distribution across Survival and Pclass combinations. Generated 3D scatter plots using Plotly to visualize Age, Fare, and Survival relationships with Pclass coloring.
- Complex Patterns Revealed: The analysis showed that survival wasn't determined by single factors alone. First-class females had the best survival chances, while third-class males had the worst, showing how class, gender, and age interacted complexly.

### Step 6: Target Variable Exploration - Deep Dive into Survival

- I focused specifically on the survival variable, examining its distribution and relationships with key demographic factors.
- Created count plots for overall survival distribution, grouped bar plots for survival by Gender and Class combinations, and analyzed the dataset imbalance (62% non-survivors vs 38% survivors).
- Critical Insight: The "women and children first" protocol was strongly evidenced in the data, with females having 74% survival rate versus 19% for males, and clear class-based survival disparities.

## Key Findings and Insights

### 1. "Women and Children First" Was Real

- The data strongly support the historical accounts of "women and children first" evacuation procedures. Female passengers had a 74% survival rate compared to only 19% for males. Children, particularly those in first and second class, had significantly higher survival rates.

### 2. Economic Class Determined Survival Chances

- The passenger class was one of the strongest predictors of survival. First-class passengers had a 63% survival rate, compared to 47% for second class and only 24% for third class. This suggests that access to lifeboats and evacuation procedures favored wealthier passengers.

### 3. Complex Interactions Between Factors

- The analysis revealed that survival wasn't determined by a single factor alone. A first-class male had better survival chances than a third-class female in some cases, showing how class, gender, and age interacted in complex ways during the disaster.

## Technical Skills I Developed

### Data Cleaning and Preparation

- Handling missing values using appropriate imputation methods
- Identifying and treating outliers that could skew the analysis
- Making informed decisions about data retention and removal

### Statistical Analysis

- Understanding distributions and central tendencies
- Calculating and interpreting correlation coefficients
- Recognizing skewed distributions and their implications

### Data Visualization

- Creating informative plots using Seaborn and Matplotlib
- Designing multi-panel visualizations for comparative analysis
- Using color and layout effectively to communicate insights

### Critical Thinking

- Asking the right questions of the data
- Testing hypotheses about relationships between variables
- Drawing meaningful conclusions from statistical patterns

## Challenges I Overcame

### Missing Data Management

- Learning when to impute values versus when to remove variables was challenging. I had to consider the percentage of missing data and the importance of each variable to the analysis.

### Visualization Selection

- Choosing the right type of plot for each analysis question required careful thought. I learned that box plots are great for comparisons, violin plots show distribution shapes well, and heatmaps effectively display correlation patterns.

### Interpretation Complexity

- Understanding that correlation doesn't imply causation was crucial. I had to consider historical context and external factors when interpreting the survival patterns.

## Lessons Learned

### 1. Data Quality is Fundamental

- I learned that thorough data cleaning is essential before any meaningful analysis can begin. Missing values and outliers can dramatically affect results if not handled properly.

### 2. Visualization Tells the Story

- Creating clear, well-labeled visualizations helped me understand complex relationships and communicate my findings effectively to others.

### 3. Context Matters

- Understanding the historical context of the Titanic disaster was crucial for interpreting the data correctly. The "women and children first" protocol explained many of the survival patterns I observed.

### 4. Iterative Analysis Process

- I discovered that data analysis is rarely linear. I often had to return to earlier steps, create new visualizations, and reconsider my approach as new patterns emerged.

### 5. Business Implications

- This project taught me how data analysis can reveal important insights that could inform safety protocols and emergency procedures in modern transportation.

## Project Resources

### 🔗 Interactive Python Notebook
[View Full Analysis on Kaggle](https://www.kaggle.com/code/muhuyierick/muhuyi-erick-cs-da02-25088-exploratorydataanalysis)

### 📈 Sample Insights

- Survival rate by gender and class combinations
- Age distribution of survivors vs non-survivors
- Fare price correlations with survival chances

## Tools & Technologies Used

- **Python 3.x** - Primary programming language
- **Pandas** - Data manipulation and analysis
- **Seaborn & Matplotlib** - Data visualization
- **NumPy** - Numerical computations
- **Jupyter Notebook** - Interactive coding environment
- **Kaggle** - Platform for dataset and notebook hosting

## Conclusion

- This Titanic exploratory data analysis project provided me with invaluable hands-on experience in the complete data analysis lifecycle. From initial data loading and cleaning to sophisticated multi-variable analysis and insight generation, I developed practical skills that I can apply to real-world data challenges. The project reinforced the importance of methodical, curious, and context-aware analysis in uncovering meaningful patterns in data.
- The most rewarding aspect was seeing how data could tell a compelling human story about one of history's most famous maritime disasters, while simultaneously teaching me technical skills that are directly applicable to modern data analysis roles.

---

*This project was completed as part of the Data and AI course assignment under Cyber Shujaa, demonstrating comprehensive exploratory data analysis skills and the ability to derive meaningful insights from complex datasets. The analysis showcases practical application of data cleaning, visualization, and statistical analysis techniques using Python and popular data science libraries.*
