# Python_Project_2
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

## Bivariate Analysis.

**1).** **Scatter plot** to show the relationship between **'Annual Income and 'Spending score'**.

- From the visualization, I observed that **the two variables have a non-linear realtionship**.

- **Code:** sns.scatterplot(data=df, x='Annual Income (k$)',y='Spending Score (1-100)' )

  ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/9d5bda2c-e642-49b5-9471-104dd44473e7)

**2)** **Pairplots** for the dataset variables.

- From the pairplots, I observed the type of relationship each variable has with each other.
  
- **Code:**

   df=df.drop('CustomerID',axis=1)

   sns.pairplot(df,hue='Gender')

  ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/9692e4de-3c75-491d-9561-2ac6946e6623)

**3)** **Correlation** between the variables.

- From the output, I observed that the **'Age' variable is negatively correlated to the 'Annual income' and 'Spending score' variables**.

- While the **'Annual income' is positively correlated to the 'Spending score'**.

- **Code:** df.corr()

- **Output:**

                        Age   	Annual Income (k$)	Spending Score (1-100)
  
                       Age	                     1.000000	-0.012398	-0.327227

                       Annual Income (k$)	    -0.012398	1.000000	0.009903

                       Spending Score (1-100)	-0.327227	0.009903	1.000000

**4).** **Mean values** of the numerical data variables,**grouped by gender.**

-  By observation, although the **male customers have an averagely higher income though they spend less** in comparision to the female customers.

- **Code:** df.groupby(['Gender'])['Age', 'Annual Income (k$)','Spending Score (1-100)'].mean()

- **Output:**

                      Age	       Annual Income (k$)	   Spending Score (1-100)

           Gender
   
           Female	38.098214	      59.250000	           51.526786

           Male	 39.806818	      62.227273	             48.511364

**5).** **Heatmap** to display the correlation between variables.

- To read the visualization, -1>x>0 indicates a negative correlatio between the variables while 0>x<1 indicates a positive correlation between the variables.

    ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/706a006c-e59f-4006-af22-11ee96df67a2)


## Univariate Clustering. 

**i)** For loop to **determine the intertia scores for  clusters** between the range of 1-11.

  - **Code:** 

       intertia_scores=[]

       for i in range(1,11):

        kmeans=KMeans(n_clusters=i)
    
        kmeans.fit(df[['Annual Income (k$)']])
    
        intertia_scores.append(kmeans.inertia_)

**ii)** **Plot the intertia scores** to obtain the most suitable cluster number,this is through the elbow method.

  - From the plot, I determined the **appropriate lot size to be 3**.

  - **Code:** plt.plot(range(1,11),intertia_scores)

  ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/8467b90a-442f-4704-ba80-60293f3558fc)

**iii)** **Initiate my algorithm**.

- **Code:** clustering1 = KMeans(n_clusters=3)

**iv)** **Fit my algorithm into the data**.

- **Code:** clustering1.fit(df[['Annual Income (k$)']])

**v)** **Add an 'Income Cluster'** column that contains clustered data values to the existing dataset.

- **Code 1:** df['Income Cluster'] = clustering1.labels and **Code 2:** df.head()

-  **Output:**  

       Gender	  Age	    Annual Income (k$)	Spending Score (1-100)	Income Cluster

      0	Male	         19	         15	                    39	                        0

      1	Male	         21	         15                    	81	                        0

      2	Female	       20	         16                    	6                          	0

      3	Female	        23	         16	                    77	                        0

      4	Female	        31	         17	                     40	                        0

**vi)** Obtain the **number of data values in each cluster**.

- **Code:** df['Income Cluster'].value_counts()

- **Output:**

      - The **'1' cluster** has the largest number of customers i.e **92**.
 
      - The **'0' cluster** has the second largest number of customers i.e **72**.
 
      - The **'2'** cluster has the least number of customers i.e **36**.
 
**vii)** **Summary statistics of the clusters** obtained.

 - The **income cluster 2 has the highest level of annual income** in addittion to the **highest spending score**.

- **Code:** df.groupby('Income Cluster')['Age', 'Annual Income (k$)','Spending Score (1-100)'].mean()   

- **Output:**

                      Age	Annual Income (k$)	Spending Score (1-100)
  
       Income Cluster

                     0	38.930556	33.027778	50.166667

                     1	39.184783	66.717391	50.054348

                      2	37.833333	99.888889	50.638889


## Bivariate Clustering. 

**i).** Initiate the KMeans clustering algorithm,fit the data values,label the obtained clusters, create new column,obtain dataset overview.

   - **Code:**
  
      clustering2 = KMeans(n_clusters=5)

      clustering2.fit(df[['Annual Income (k$)','Spending Score (1-100)']])

       df['Spending and Income Cluster'] =clustering2.labels_

       df.head()

   - **Output:**

           Gender	       Age	    Annual Income (k$)	  Spending Score (1-100)	Income Cluster	Spending and Income Cluster
    
         0	Male	        19	            15	                      39	               0	                       4

         1	Male	        21	             15	                      81	                0	                       3

         2	Female	      20	             16	                      6                  	0	                       4

         3	Female	      23	             16                       77                 	0	                        3

         4	Female	      31	             17                        40	                 0	                       4

**ii).** Obtain the appropriate number of clusters for the dataset using the elbow method.

 - From the plot,I was able to obtain that the **suitable number of clusters is 5**.

 - **Code:**   

    intertia_scores2=[]

    for i in range(1,11):

     kmeans2=KMeans(n_clusters=i)
  
     kmeans2.fit(df[['Annual Income (k$)','Spending Score (1-100)']])
  
    intertia_scores2.append(kmeans2.inertia_)
  
   plt.plot(range(1,11),intertia_scores2)

    ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/52e1459d-a3f7-4b22-a025-04d0c33d1f0e)

**iii).** **Scatter plot** to display the relationship between the 'Spending score' and 'Annual Income' in reference to clusters.

   - **Code 1:**

     centers =pd.DataFrame(clustering2.cluster_centers_)
  
     centers.columns = ['x','y']

  - **Code 2:**

    plt.figure(figsize=(10,8))
 
    plt.scatter(x=centers['x'],y=centers['y'],s=100,c='black',marker='*')

    sns.scatterplot(data=df, x ='Annual Income (k$)',y='Spending Score (1-100)',hue='Spending and Income Cluster',palette='tab10')

    plt.savefig('clustering_bivaraiate.png')


      ![image](https://github.com/MutheuTheAnalyst/Python_Projet_2/assets/92978069/ebba26b5-1e65-45fd-a6df-03feed95c646)

**iv)** Compare the male and female gender by the 'Spending and Income Cluster'.

- **Code:** pd.crosstab(df['Spending and Income Cluster'],df['Gender'],normalize='index')

- **Output:**

                      Gender	     Female       	Male
  
Spending and Income Cluster	

  	        0                       0.592593	      0.407407
         
            1	                     0.538462	      0.461538
          
            2	                     0.457143	      0.542857
          
            3	                     0.590909	      0.409091
          
            4	                     0.608696	      0.391304

**v).** **Group the variables** by the 'Spending and Income' Cluster.

- **Code:** df.groupby('Spending and Income Cluster')['Age', 'Annual Income (k$)','Spending Score (1-100)'].mean()

- **Output:**

                                          Age	         Annual Income (k$)	      Spending Score (1-100)
  
    Spending and Income Cluster	

              0	                        42.716049	         55.296296	                49.518519

              1	                        32.692308	          86.538462                	82.128205

              2	                         41.114286	        88.200000	                 17.114286

              3	                         25.272727	         25.727273	                79.363636

              4	                         45.217391	         26.304348	                 20.913043


## Reccommendations Obtained From The Project.

- The **aim** of the project is to **identify the best target customer group(s)** in order for the **marketing team  to plan the best optimal strategy** that ought to **increase the mall's product sales**.

- Following my analysis above,my reccommendations are as follows:

    **1).** The **best target customer group** is: **Cluster 1**.

    - This is because this cluster has both a high spending score and high income thus their able to purchase more products and at an often rate too.

    - 54% of cluster 1 customers are women.The marketing team could run a marketing campaign advertising items that particularly resonate with this sub-cluster.

    **2)** **Cluster 3** also **presents** an interesting **opportunity to  increase product sales**.

     - Although this cluster is in the low income range,it is suprisingly also in the high spending score category.

     - The customers could potentially be inclined to purchase more products when popular items are discounted.



  
    









          


 
   
 

      



    
  



              


  

