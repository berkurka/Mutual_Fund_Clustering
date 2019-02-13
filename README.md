# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Mutual Fund Clustering

## Project Author
- Bernard Kurka | <u>[LinkedIn](https://www.linkedin.com/in/bernardkurka)</u> | <u>[Email](bkexcel2014@gmail.com)</u>


## [Presentation Slides](https://docs.google.com/presentation/d/1fzJ11Je7FM09U-_RrLRmNs7IHrcWNF0Ny9ZS_LW_qIg/edit?usp=sharing)

## Finantial concepts used in project:
- Some terms used in the project are specific to finance this file will provide some useful explanation. <u>[Finance concepts explained]()</u>

## Notebooks
- <u>[01 Data Cleaning](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Data%20Cleaning.ipynb)</u>
- <u>[02 Data Exploration](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/EDA.ipynb)</u>
- <u>[03 Data Modeling](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Building%20Models.ipynb)</u>
- <u>[04 Interactive Demo](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Interactive_display_demo.ipynb)</u>

## Table of contents
- <u>[Executive Summary](#header)</u>
- <u>[The Data](#header)</u>

- <u>[Analysis](#header)</u>
- <u>[Conclusion](#header)</u>

### Executive Summary
In 2017 the number of [open-end funds](https://www.investopedia.com/ask/answers/042315/what-are-primary-differences-between-closed-end-investment-and-open-end-investment.asp) worldwide reached [114,131](https://www.statista.com/topics/1441/mutual-funds/). In the United States there were [9,356 mutual funds in 2017](https://www.statista.com/topics/1441/mutual-funds/). Choosing a mutual fund can be overwhelming, since  there are thousands of choices and many ways to compare. The goal of this project is to use unsupervised machine learning clustering algorithms to leverage and simplify fund selection.

I´ve used Brazilian mutual fund data, since U.S. mutual fund data is not easily available. After cleaning, filtering and feature engineering the final data consisted of 1,376 funds with 49 features (29 numeric and 20 dummy).

Nearly half of the features selected were related to the fund characteristics such as classification, benchmark, management fee and so on and the other half were related to funds technical indicators such as fund assets under management, return, volatility and so forth.

I ran 4 different clustering models (K-means, DBSCAN, Hierarchy, and Agglomerative) using several hyperparameters combinations, analyzed the inertia, silhouette and cluster count distribution.
Models with fewer centroids (i.e. low K) resulted in the highest silhouette scores and unbalanced clusters (e.g. for K = 2, one DBSCAN cluster had 1,373 observations, while the other hand only 3 observations.)


To get a good balance between interpretability and clustering scores I selected the Kmeans model with 5 clusters. Since there are 42 features it can be difficult to grasp the intuition behind different clusters. In order to find the most significant features in the clustering algorithm, I´ve built a Random Forest Classifier model, to predict which cluster any given observation. The Random Forest accuracy score was 99%, 98% and 98% in training, cross-validation and testing data respectively.

I selected the K-means model since the scores were similar then the Hierarchy and Agglomerative and DBCSCAN.
The K-means model guarantees that all observations are classified, it also allows inertia score calculation, to measure the density in each cluster.
The downside of this model is that it can be impacted by outliers.

 Model created 5 distinct clusters
 - Cluster 0: Contains 91% balanced funds with low volatility, low returns, medium range age of funds high management fee.

 - Cluster 1: Contains 100% fixed income with lowest volatility, lowest returns, largest size funds.

 - Cluster 2: Very similar than cluster 1, contains 94% fixed income funds with low volatility, low returns but these funds are younger and smaller compared to cluster 1 funds.

 - Cluster 3: Contains 95% of equity funds with highest volatility, highest returns and highest management fee. Also contains 5% balanced funds.

 - Cluster 4: Contains 97% of currency funds with medium volatility, highest age of funds and medium management fee.


### The Data

[Notebook 01 Data Cleaning and Feature Engineering](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Data%20Cleaning.ipynb)

##### Data Source

- Data was acquired using [Quantum Axis](https://www.quantumaxis.com.br/webaxis/), which is an online platform with all Brazilian financial data, provided by [Quantum Finance](http://www.quantumfinance.com.br/eng/). In the platform I selected all open-end funds and exported into two excel files, the first one with characteristics and second with technical indicators. The data was imported into a `Pandas` DataFrame using `pandas.read_excel`.

##### Data Cleaning


- I started the project using a database with 4,082 open-end Brazilian mutual funds intended to non-institutional investors. I removed funds that were terminated or were recently created (last 24 months), or had null row values. After cleaning, the number went down to 1,376 funds. I also dropped 47 columns pertaining to fund characteristics.

##### Feature Engineering
- Created dummy columns for categorical features.
- Created a column with fund age in months.
- Since there were more than 90 different fund managers, instead of one-hot encoding them, I created a column with number of funds managed by the primary fund manager and another column with the sum of all assets under management for that manager.


##### Data Dictionary

|Label|Type|Description|
|---|---|---|
|Name|String|Fund Name|
|CNPJ|String|Unique code per fund|
|ManagementFee|Float|Fee charged to pay for management costs.|
|MinimumInvestment|Integer|Minimum investment accepted by the fund in Brazilian Real.|
|PerformanceFee|Float|Fee charged if fund returns exceed its benchmark's|
|PortfolioManager|String|Name of primary fund manager|
|redemption_delay|Integer|Number of days after redemption order the fund will take to transfer back money to investors acount.|
|age_months|Integer|Number of months since fund's start date.|
|CVMCategory_FixedIncome|Integer|1 if fund category is Fixed income, 0 otherwise|
|CVMCategory_Multimarket|Integer|1 if fund category is Balanced, 0 otherwise|
|CVMCategory_Equities|Integer|1 if fund category is Equity, 0 otherwise|
|CVMCategory_FX|Integer|1 if fund category is Currency, 0 otherwise|
|TaxClassification_Exempt|Integer|1 if fund exempt from income tax, 0 otherwise|
|TaxClassification_LongTerm|Integer|1 if the fund has long term income tax rates, 0 otherwise|
|TaxClassification_ShortTerm|Integer|1 if the fund has short term income tax rates, 0 otherwise|
|PrivateCreditAnbima_Notapplicable|Integer|1 if the fund is not eligible for this classification ******, 0 otherwise.|
|PrivateCreditAnbima_Yes|Integer|1 if the fund invests 50% or more in private bonds, 0 otherwise.|
|LeveragedAnbima_Yes|Integer|1 if the fund is authorized to make leveraged operations. |
|PerformanceFeeReferenceIndex_100%doIBX|Integer|1 if performance reference index equals 100 IBX, 0 otherwise|
|PerformanceFeeReferenceIndex_100%doIbovespa|Integer|1 if performance reference index equals 100 of Ibovespa, 0 otherwise|
|PerformanceFeeReferenceIndex_Other_performance_fee|Integer|1 if performance reference index is other, 0 otherwise|
|PerformanceFeeReferenceIndex_Thereisnot|Integer|1 if does not charge performance fee, 0 otherwise|
|Benchmark_Dollar|Integer|1 if fund benchmark is Dollar vs Brazilian Reals (USD/BRL), 0 otherwise|
|Benchmark_IBX|Integer|1 if fund benchmark is IBX, 0 otherwise|
|Benchmark_IMA-B|Integer|1 if fund benchmark is IMA-B, 0 otherwise|
|Benchmark_Ibovespa|Integer|1 if fund benchmark is Ibovespa, 0 otherwise|
|Benchmark_NotInformed|Integer|1 if fund benchmark is not informed, 0 otherwise|
|Benchmark_Other_Benchmark|Integer|1 if fund benchmark is another type, 0 otherwise|
|Last_Assets|Float|Fund most recent total asset under management|
|Assets_Flow_6m|Float|Fund net asset flow in last 6 months|
|Assets_Flow_12m|Float|Fund net asset flow in last 12 months|
|Assets_Flow_24m|Float|Fund net asset flow in last 24 months|
|Average_Assets_6m|Float|Average asset under management in the last 6 months.|
|Average_Assets_12m|Float|Average asset under management in the last 12 months.|
|Average_Assets_24m|Float|Average asset under management in the last 24 months.|
|Return_6m|Float|Fund return, over a 6 month period.|
|Return_12m|Float|Fund return, over a 12 month period.|
|Return_24m|Float|Fund return, over a 24 month period.|
|Volatility_6m|Float|Fund volatility, over a 6 month period.|
|Volatility_12m|Float|Fund volatility, over a 12 month period.|
|Volatility_24m|Float|Fund volatility, over a 24 month period.|
|Excess_Return_-_CDI_Opening_6m|Float|Return that exceeded CDI Benchmark, over 6 month period.|
|Excess_Return_-_CDI_Opening_12m|Float|Return that exceeded CDI Benchmark, over 12 month period.|
|Excess_Return_-_CDI_Opening_24m|Float|Return that exceeded CDI Benchmark, over 24 month period.|
|Excess_Return_-_Ibovespa_6m|Float|Return that exceeded Ibovespa Benchmark, over 6 month period.|
|Excess_Return_-_Ibovespa_12m|Float|Return that exceeded Ibovespa Benchmark, over 12 month period.|
|Excess_Return_-_Ibovespa_24m|Float|Return that exceeded Ibovespa Benchmark, over 24 month period.|
|Excess_Return_-_Dollar_6m|Float|Return that exceeded Dollar vs Brazilian Real (USD/BRL) Benchmark, over 6 month period.|
|Excess_Return_-_Dollar_12m|Float|Return that exceeded Dollar vs Brazilian Real (USD/BRL) Benchmark, over 12 month period.|
|Excess_Return_-_Dollar_24m|Float|Return that exceeded Dollar vs Brazilian Real (USD/BRL) Benchmark, over 24 month period.|
|#_Funds_managed|Integer|Count of how many different funds are managed by the same manager. Considering only funds within the sample.|
|Manager_avg_Assets|Float|Sum of assets under management for the fund manager. Considering only funds within the sample|


### Analysis
<u>[Notebook 02 Data Exploration](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/EDA.ipynb)</u>
<u>[Notebook 03 Data Modeling](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Building%20Models.ipynb)</u>

The libraries used for modeling (e.g., `Pandas`,`numpy`, `Scikit-learn`).

I compared silhouette, inertia score and cluster balance from 610 different models. These models were created using 4 different clustering models (K- Means, DBSCAN Agglomerative and Hierarchical) and changing hyperparameters (n_clusters, inits, linkage_method, affinity...).

I selected the K-means model since there DBSCAN would not classify all observations and the other 2 models did present superior results. I used the plot's to analyze the change in silhouette and inertia score when increasing the number of clusters. There was not a clear number of clusters to chose using the Elbow method. In order to make interpretability more comprehensible, I found that 5 clusters was a well balanced choice.

Final K-means model used the default parameters except for `init = random` and `random_state=42`.
- Using the optimal model, I created a prediction column with the predicted cluster.
 - In order to facilitate model interpretability I used a `RandomForestClassifier` model to predict which cluster an observation should be assigned to. The Random Forest accuracy score was 99%, 98% and 98% in training, cross-validation and testing data respectively. The model´s most relevant coefficients were used to build a table with different characteristics of each cluster.

Most Important coefficients for predicting cluster

|Feature name|Random Forest Coefficient|
|---|---|
|CVM Category_Fixed Income|0.296|
|CVM Category_Multimarket|0.157|
|Excess_Return_-_CDI_Opening_6m|0.106|
|Excess_Return_-_Dollar_6m|0.072|
|Excess_Return_-_Ibovespa_6m|0.056|
|Volatility_12m|0.041|
|CVM Category_Equities|0.039|
|Volatility_6m|0.038|
|Last_Assets|0.032|
|Leveraged Anbima_Yes|0.026|


### Conclusion
The most important feature used in K-means clustering was the fund's category. Volatility was also one of the most relevant features used in the clustering. The fund's category and volatility are the most relevant information when searching for similar funds.

Several fund recommender systems use fund category and volatility, as the backbones of their decision process, the project results are similar then the industry practice.  

### Recommendations
1. Build a fund recommender system using cluster classifications
  - The system will receive as input information about risk, fund category, minimum amount invested and redemption delay.
2. To improve the recommender system
  - Build 2 different clusters, first using characteristics features and second using technical features.
  - Try different clustering methods such as Spectral Clustering, MeanShift, AffinityPropagation.
  - Test clustering with different feature combinations
