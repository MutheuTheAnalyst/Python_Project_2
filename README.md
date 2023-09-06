# Python_Projet_2
## Introduction

- In this project, a clean and transformed **'Mall_Customers Dataset'** obtained from a  shopping mall's database is presented.

- My aim is to **cluster the given dataset into distinct target market groups** and analyze the obtained target groups.This is in a bid to **gain insight on target markets that may potentially lead to increased product sales** at the mall when advertised to.

- I shall carry out my **analysis  using the 'Python Programming Language'** on the **Jupyter Notebook IDE**.

## Dataset Overview

- I first **imported libraries** that shall be useful in performing my analysis.

  - **Pandas** for data manipulation & data wrangling,**Seaborn** for statistical visualization,**matplotlib.pyplot** for data visualization,**sklearn.cluster** for clustering and **warnings** for removing py prompt warnings.

  - **Code:** import pandas as pd,import seaborn as sns,import matplotlib.pyplot as plt,from sklearn.cluster import KMeans,import warnings warnings.filterwarnings('ignore')

- I then proceeded to **import the Mall_Customers dataset(named it 'df')** and then confirmed that it loaded correctly by running a data overview query.

     - **Code 1:** df = pd.read_csv() and **Code 2:** df.head()
 
 - **Checked for null values** across all the columns.No column in this dataset contains null values **(no null values)**.

     - **Code:** pd.isnull(df).sum()

- Obtained **information about the dataset**.The dataset has a **total of 5 columns and 200 records**.In addittion, by running the code, I was able to know the column names and the data types of data values in each column.

    - **Code:** df.info()
      
    - **Output:**
      
    - Column                  Non-Null Count  Dtype

       0   CustomerID              200 non-null    int64 
 
       1   Gender                  200 non-null    object
 
       2   Age                     200 non-null    int64 
 
       3   Annual Income (k$)      200 non-null    int64 
 
       4   Spending Score (1-100)  200 non-null    int64 
 
       dtypes: int64(4), object(1)

## Univariate Analysis

- 
      



    
  



              


  

