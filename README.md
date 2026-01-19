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
# 📥 Data import
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
