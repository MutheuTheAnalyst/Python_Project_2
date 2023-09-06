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

**1).** For starters,I obtained the **descriptive statistics** of the dataset variables.

  - **Code:** df.describe().transpose()
 
  - **Output:**
                            count	   mean	    std	       min	    25%	   50%	   75%	    max
    
     CustomerID	            200.0	   100.50	  57.879185	  1.0	   50.75	 100.5	 150.25 	200.0

     Age	                  200.0	   38.85	  13.969007	  18.0	 28.75	 36.0	   49.00	  70.0

     Annual Income (k$)	    200.0	   60.56	  26.264721	 15.0 	 41.50	 61.5  	78.00	    137.0
 
     Spending Score (1-100)	200.0	   50.20	  25.823522	 1.0	   34.75	 50.0  	73.00	    99.0

 **2).** **Histogram plots** for each of the numerical variables.

- **Code:**

  columns=['CustomerID', 'Age', 'Annual Income (k$)']

  for i in columns:
  
  plt.figure()

  sns.distplot(df[i])

- **Insights**:

    - The 'CustomerID' Histogram confirms and displays that our **dataset contains 200 customers**.

       ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/775825bf-2926-4304-8a5d-b6718efdfd75)
    
    - From the 'Annual Income' Histogram, I observed that the **age range of the customers is between 18-69** whereby **most customers are in the age range 18-52**.

      ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/b9523c35-bf6a-4968-a350-74d98711bbdb)

  
    - From the 'Annual Income' Histogram,I observed that **most of the customers lie between the 50k-80k annual income range** while the **total range lies between 18k to 52k**.
    
     ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/91903eec-0a72-4361-ad99-d526593e80ff)

**3).** **KDE Plots** for each of the numerical  variables,categorized by gender.

- **Code:**

    columns = ['Age', 'Annual Income (k$)','Spending Score (1-100)']
    
    for i in columns:
    
    plt.figure()
    
    sns.kdeplot(df[i],shade=True,hue=df['Gender'])

- **Insights:**
 
   - From the Ist visualization, the **female customers are more in number within the age range of about 18 to 58**.In the **0-18 and 58-80 age ranges,the male gender customers are more in number**.

     ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/e518fd84-fd3c-4343-a240-4c08de9d8ba5)
     
 
   - In the 2nd visualization, the **female customers earn more annual income than the male customers within the income range 0-130k** while in the **130-150k range the male customers outshine the female customers**.
     
     ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/f97c0098-890c-4598-8b55-fa0341715a7a)
     
 
   - Generally, **female customers have a significantly higher spending score** as compared to their male counterparts.
   
     ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/6b7b64bd-fefb-4d8c-b0e9-e78389fa02e7)


**4).**  **Boxplots** for each numerical variable(categorized by gender).
 
- **Code:** 

    columns = ['Age', 'Annual Income (k$)','Spending Score (1-100)']

    for i in columns:

    plt.figure()
    
    sns.boxplot(data=df,x='Gender',y=df[i])

- From the boxplots,we can observe that there are **barely any outliers in the dataset variables**.

![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/d6e11967-eb3a-4e45-80b1-8e00792547b1)

![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/59d5ba86-f483-4100-98b5-81be92a8ea42)

![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/47f9a750-4ae9-4df0-8d40-108279982be7)

**5).** Number of male and female customers in % form.

- **Code:** df['Gender'].value_counts(normalize=True)

- It is clear to see that the **female customers outnumber the male customers by 12%**.

- **Output:**

  Female    0.56
  
  Male      0.44

  Name: Gender, dtype: float64




          


 
   
 

      



    
  



              


  

