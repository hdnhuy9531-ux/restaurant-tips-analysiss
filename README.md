# restaurant-tips-analysiss
Data analysis of restaurant tipping behavior using Jupyter Notebook
# Restaurant Tips Analysis
## Introduction
This project focuses on analyzing tipping behavior in a restaurant using a real-world dataset.
The analysis explores how factors such as total bill amount, day, time, and customer attributes influence tips.
## Dataset
- Source: "https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv".
- Description: The dataset contains information about restaurant bills, tips, customer gender, smoking status, day, and time.
- Access: The dataset is loaded directly within the Jupyter Notebook.
## Objectives
This project aims to analyze restaurant tipping behavior using a real-world dataset.
It explores how variables such as total bill, day, time, and customer characteristics influence tips
# Stage 1: Data import
- Import data:
- Input:
```python
#Import the libraries
import pandas as pd
import matplotlib.pyplot as plt

#Import the dataset into dataframe (df)
df = pd.read_csv("https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv")

# Display the first few rows of the dataset
print(df.head())
```
- Output

| id | total_bill | tip  | sex    | smoker | day | time   | size |
|----|------------|------|--------|--------|-----|--------|------|
| 0  | 16.99      | 1.01 | Female | No     | Sun | Dinner | 2    |
| 1  | 10.34      | 1.66 | Male   | No     | Sun | Dinner | 3    |
| 2  | 21.01      | 3.50 | Male   | No     | Sun | Dinner | 3    |
| 3  | 23.68      | 3.31 | Male   | No     | Sun | Dinner | 2    |
| 4  | 24.59      | 3.61 | Female | No     | Sun | Dinner | 4    |

### Show the columns of the dataframe and their types:
- Input:
```python
print(df.dtypes)
```
- Output:

| Column Name | Data Type |
|------------|-----------|
| id | int64 |
| total_bill | float64 |
| tip | float64 |
| sex | object |
| smoker | object |
| day | object |
| time | object |
| size | int64 |

The columns sex, smoker, day, and time are categorical variables currently stored as object. We will convert them to string type.
- Input:
```python
columns_to_convert = ['sex', 'smoker', 'day', 'time']
df[columns_to_convert] = df[columns_to_convert].astype(pd.StringDtype())
```
- Output:

| Column Name | Data Type |
|------------|-----------|
| id | int64 |
| total_bill | float64 |
| tip | float64 |
| sex | string |
| smoker | string |
| day | string |
| time | string |
| size | int64 |

###Basic descriptive statistics
- Input:
```python
df.describe()
```
- Output:

| Statistic | id | total_bill | tip | size |
|---------|------------|------------|------------|------------|
| count | 244.000000 | 244.000000 | 244.000000 | 244.000000 |
| mean | 121.500000 | 19.785943 | 2.998279 | 2.569672 |
| std | 70.580923 | 8.902412 | 1.383638 | 0.951100 |
| min | 0.000000 | 3.070000 | 1.000000 | 1.000000 |
| 25% | 60.750000 | 13.347500 | 2.000000 | 2.000000 |
| 50% | 121.500000 | 17.795000 | 2.900000 | 2.000000 |
| 75% | 182.250000 | 24.127500 | 3.562500 | 3.000000 |
| max | 243.000000 | 50.810000 | 10.000000 | 6.000000 |

# Stage 2:Hypothesis testing
## 🚬 Do people who smoke give more tips?
This analysis compares the measures of central tendency of tip amounts between smokers and non-smokers.
```python
#Create a new dataframe smokers_df containing only info about smokers.
smokers_df = df.query('smoker=="Yes"')

#Create a new dataframe non_smokers_df containing only non-smokers.
non_smokers_df = df.query('smoker=="No"')

#smokers_df measures of central tendency
smokers_tip_min = smokers_df['tip'].min()
smokers_tip_max = smokers_df['tip'].max()
smokers_tip_mean = smokers_df['tip'].mean()
smokers_tip_median = smokers_df['tip'].median()

#non_smokers_df measures of central tendency
non_smokers_tip_min = non_smokers_df['tip'].min()
non_smokers_tip_max = non_smokers_df['tip'].max()
non_smokers_tip_mean = non_smokers_df['tip'].mean()
non_smokers_tip_median = non_smokers_df['tip'].median()

#whole dataset df measures of central tendency
common_tip_min = df['tip'].min()
common_tip_max = df['tip'].max()
common_tip_mean = df['tip'].mean()
common_tip_median = df['tip'].median()

#Create table to compare
data_smoker_non_smoker = {
    "Common": [df["tip"].min(), df["tip"].max(), df["tip"].mean(), df["tip"].median()],
    "Smokers": [smokers_df["tip"].min(), smokers_df["tip"].max(), smokers_df["tip"].mean(), smokers_df["tip"].median()],
    "Non-Smokers": [non_smokers_df["tip"].min(), non_smokers_df["tip"].max(), non_smokers_df["tip"].mean(), non_smokers_df["tip"].median()]
} # Create a dictionary with the statistics
index_labels = ["Min", "Max", "Mean", "Median"] # Define row labels
smoking_compare_df = pd.DataFrame(ata_smoker_non_smoker, index=index_labels) # Create the DataFrame
smoking_compare_df
```
- Output

| Statistic | Common | Smokers | Non-smokers |
|---------|------------|------------|------------|
| Min | 1.000000 | 1.000000 | 1.000000 |
| Max | 10.000000 | 10.000000 | 9.000000 |
| Mean | 2.998279 | 3.008710 | 2.991854 |
| Median | 2.900000 | 3.000000 | 2.740000 |

### Histogram
- Input:
```python
figure, axis = plt.subplots(1,3,figsize=(20,5))
#Chart 1: Whole dataset tip values
axis[0].hist(df['tip'], bins = 10, color='#74b9ff')
axis[0].set_title('Whole dataset tip values')
#Chart 2: Smokers tip values
axis[1].hist(smokers_df['tip'], bins = 10, color='#ff7675')
axis[1].set_title('Smokers tip values')
#Chart 3: Non-smokers tip values
axis[2].hist(non_smokers_df['tip'], bins = 10, color='#55efc4')
axis[2].set_title('Non-smokers tip values')
```

- Output:

<img width="1597" height="451" alt="image" src="https://github.com/user-attachments/assets/4985cf50-0032-4622-a983-3ae1d45eabe0" />

### Insights and Conclusions on Tipping Behavior: Smokers vs. Non-Smokers
#### 🔍 Key Insights: Tipping Behavior by Smoking Status
- Smokers tend to tip slightly more than non-smokers.
Both the mean and median tip values are higher among smokers (mean ≈ 3.01, median 3.00) compared to non-smokers (mean ≈ 2.99, median 2.74), indicating a consistent but modest difference in tipping behavior.
- Higher tip variability is driven by smokers.
While minimum tip values are identical across groups, smokers reach higher maximum tip amounts, contributing more frequently to the upper end of the tip distribution. Non-smokers exhibit a slightly narrower range of tip values.
- Distribution patterns support numerical findings.
Histogram analysis shows similar tipping behavior at lower values for both groups, suggesting a common baseline. However, smokers display a higher concentration of larger tips, reinforcing the central tendency results.

#### 📌Conclusion
Overall, smokers demonstrate a marginally more generous tipping pattern than non-smokers. Although the difference is subtle, it is consistently observed across summary statistics and visual analysis. These insights highlight how customer segmentation can reveal behavioral nuances that may support more data-informed service and business decisions.

###👨👩 Do males give more tips?
In this section, the same analytical steps as in the previous question are applied. The data is split into male and female subsets, histograms are generated for each group, and the distributions are compared.
- Input:
```python
# Create new df for sex:
males_df = df.query('sex=="Male"')
females_df = df.query('sex=="Female"')
#Calculate central tendency:
males_tip_min = males_df['tip'].min()
males_tip_max = males_df['tip'].max()
males_tip_mean = males_df['tip'].mean()
males_tip_median = males_df['tip'].median()

females_tip_min = females_df['tip'].min()
females_tip_max = females_df['tip'].max()
females_tip_mean = females_df['tip'].mean()
females_tip_median = females_df['tip'].median()

#Create new data from for central tendency:
common_males_females_tip = {
    'Common': [common_tip_min, common_tip_max, common_tip_mean, common_tip_median],
    'Males': [males_tip_min, males_tip_max, males_tip_mean, males_tip_median],
    'Females': [females_tip_min, females_tip_max, females_tip_mean, females_tip_median]
}

index_labels = ["Min", "Max", "Mean", "Median"]
df_common_males_females_tip = pd.DataFrame(common_males_females_tip, index=index_labels)
#Create chart:
figure, axis = plt.subplots(1, 3, figsize=(45, 5))
# Chart 1: Whole dataset tip values
axis[0].hist(df['tip'], bins = 10, color='#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)
# Chart 2: Males tip values
axis[1].hist(males_df['tip'], bins = 10, color='#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Males tip values')
axis[1].grid(True)
# Chart 3: Females tip values
axis[2].hist(females_df['tip'],  bins = 10,color='#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Females tip values')
axis[2].grid(True)

plt.show()

#Print data frame
df_common_males_females_tip
```
- Output:

| Statistic | Common | Males | Females |
|-----------|--------|-------|---------|
| Min       | 1.000  | 1.000 | 1.000   |
| Max       | 10.000 | 10.000| 6.500   |
| Mean      | 2.998  | 3.090 | 2.833   |
| Median    | 2.900  | 3.000 | 2.750   |

<img width="4490" height="490" alt="image" src="https://github.com/user-attachments/assets/5d0a9101-0338-407e-bd51-7dc59514633c" />

### Insights and Conclusions on Tipping Behavior (Males vs. Females)

#### Insight 1: Males Tend to Tip Slightly More Than Females
- The **mean tip value** for males (3.090) is slightly higher than that for females (2.833).
- The **median tip value** for males (3.00) also exceeds that of females (2.75).
- Overall, this suggests that males tend to tip slightly more than females on average.

#### Insight 2: Tip Distribution Range
- The **tip range** (difference between maximum and minimum values) is the same for the overall dataset and for males, with a maximum tip of 10.000.
- For females, the maximum tip is lower (6.500), indicating a **narrower distribution of tip values**.
- Higher tip values are primarily contributed by male customers.

#### Histogram Observations
- The histogram for males shows a **higher frequency of larger tip values** compared to females.
- Both male and female distributions display a similar pattern at the lower end, suggesting a consistent minimum tipping behavior across genders.

#### General Conclusion
Males tend to tip slightly more than females, as reflected in both **mean and median tip values**. While the average difference is not large, males appear more frequently in the higher tip range. Visual analysis further supports this finding, showing a greater concentration of larger tips among males.

These insights can help businesses and service providers better understand tipping behavior and customer patterns, potentially informing service strategies and expectations.
