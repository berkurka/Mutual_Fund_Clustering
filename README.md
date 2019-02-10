# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Mutual Fund Clustering

## Project Author
- Bernard Kurka | <u>[LinkedIn](https://www.linkedin.com/in/bernardkurka)</u> | <u>[Email](bkexcel2014@gmail.com)</u>


## [Presentation Slides](https://docs.google.com/presentation/d/1fzJ11Je7FM09U-_RrLRmNs7IHrcWNF0Ny9ZS_LW_qIg/edit?usp=sharing)


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
In 2017 the number of [open-end funds](https://www.investopedia.com/ask/answers/042315/what-are-primary-differences-between-closed-end-investment-and-open-end-investment.asp) worldwide reached [114,131](https://www.statista.com/topics/1441/mutual-funds/). Choosing a mutual fund can be overwhelming, since  there are thousands of choices and many ways to compare, in the United States there where [9,356 mutual funds in 2017](https://www.statista.com/topics/1441/mutual-funds/). The goal of this project is to use unsupervised machine learning clustering algorithms to leverage and simplify fund selection.

I´ve used a Brazilian mutual fund data, since U.S. mutual fund data is not easily available. After cleaning, filtering and feature engineering the final data consisted of 1,300 funds with 56 features (30 numeric and 26 dummy).

Nearly half of the features selected were related to the fund qualitative characteristics such as classification, benchmark, management fee and so on and the other half were related to funds quantitative indicators such as fund assets under management, return, volatility and so forth.

I ran 4 different clustering models (Kmeans, Dbscan, Hierarchy, and Agglomerative) using several hyperparameters combinations, analyzed the Inertia, Silhouette and cluster count distribution. The highest Silhouette scores models were occurring with a lower number of centroids (k), and a highly concentrated cluster count, that means that a most of the observations have similar feature values hand full of funds with very different feature values.

To get a good balance between interpretability and clustering scores I selected the Kmeans model with 5 clusters. Since there are 42 features it can be difficult to grasp the intuition behind different clusters. In order to find the most significant features used for the clustering algorithm, I´ve built a Random Forest Classifier model, to predict which cluster any given row belongs. The Random Forest accuracy score was 99%, 98% and 98% in training, cross-validation and testing data respectively.

 Model created 5 distinct clusters
 - Cluster 0: Contains 91% balanced funds with low volatility, low returns, medium range age of funds high management fee.

 - Cluster 1: Contains 100% fixed income with lowest volatility, lowest returns, largest size funds.

 - Cluster 2: Very similar than cluster 1, contains 94% fixed income funds with low volatility, low returns but these funds are younger and smaller compared to cluster 1 funds.

 - Cluster 3: Contains 95% of equity funds with highest volatility, highest returns and highest management fee. Also contains 5% balanced funds.

 - Cluster 4: Contains 97% of currency funds with medium volatility, highest age of funds and medium management fee.


### The Data

- [Notebook 01 Data Cleaning and Feature Engineering](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Data%20Cleaning.ipynb)

##### Data Source

- Data was acquired using [Quantum Axis](https://www.quantumaxis.com.br/webaxis/), wich is a online platform with all Brazilian finantial data, provided by [Quantum Finance](http://www.quantumfinance.com.br/eng/). In the platform I selected all open-end funds and exported it to a 2 excel files, 1 with qualitative features and other with quantitative features. The data was imported into a `Pandas` DataFrame using `pandas.read_excel`.

##### Data Cleaning


- I started the project using a database with 4,082 open-end Brazilian mutual funds destinated to Non-Institutional investors. I removed funds that were terminated or where recently created (last 24 months), or had null row values the number went down to 1,300 funds. Also dropped 47 columns qualitative columns.

##### Feature Engineering
- Created dummy columns for category features.
- Created column with fund age in months.
- There where more than 90 different fund managers, insted of converting it into dummy columns I´ve created column with number of funds managed by fund manager and other column with the sum of all assets under management for each manager.


##### Data Dictionary

|Label|Type|Description|
|---|---|---|
|Name|String|Fund Name|
|CNPJ|String|Unique code per fund|
|ManagementFee|Float|Fee charged to pay for management costs.|
|MinimumInvestment|String|Minimum investment accepted by the fund in Brazilian Reais.|
|PerformanceFee|Float|Fund performance Fee charged if fund exceeds its benchmark|
|PortfolioManager|String|Name of fund manager|
|LiquidityRatios|String|Number of days after redemption order the fund will take to transfer back money to investors acount.|
|age_months|Integer|Number of months since funds start date.|
|CVMCategory_FixedIncome|Integer|1 if fund category is Fixed income, 0 otherwise|
|CVMCategory_Multimarket|Integer|1 if fund category is Balanced, 0 otherwise|
|CVMCategory_Equities|Integer|1 if fund category is Equity, 0 otherwise|
|CVMCategory_FX|Integer|1 if fund category is Currency, 0 otherwise|
|TaxClassification_Exempt|Integer|1 if fund exempt from income tax, 0 otherwise|
|TaxClassification_LongTerm|Integer|1 if the fund has short term income tax rates, 0 otherwise|
|TaxClassification_ShortTerm|Integer|1 if the fund has short long income tax rates, 0 otherwise|
|PrivateCreditAnbima_Notapplicable|Integer|1 if the fund is not elegible for this classification, 0 otherwise.|
|PrivateCreditAnbima_Yes|Integer|1 if the fund invests 50% or more in private bonds, 0 otherwise.|
|LeveragedAnbima_Yes|Integer|1 if the fund is authorized to make leveraged operations. |
|PerformanceFeeReferenceIndex_100%doIBX|Integer|1 if performance reference index equals 100 IBX, 0 otherwise|
|PerformanceFeeReferenceIndex_100%doIbovespa|Integer|1 if performance reference index equals 100 of Ibovespa, 0 otherwise|
|PerformanceFeeReferenceIndex_Other_performance_fee|Integer|1 if performance reference index is other, 0 otherwise|
|PerformanceFeeReferenceIndex_Thereisnot|Integer|1 if does not charge performance fee, 0 otherwise|
|Benchmark_Dollar|Integer|1 if fund benchmark is Dollar vs Brazilian Reais (USD/BRL), 0 otherwise|
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
|Excess_Return_-_Dollar_6m|Float|Return that exceeded Dollar vs Brazilian Reais (USD/BRL) Benchmark, over 6 month period.|
|Excess_Return_-_Dollar_12m|Float|Return that exceeded Dollar vs Brazilian Reais (USD/BRL) Benchmark, over 12 month period.|
|Excess_Return_-_Dollar_24m|Float|Return that exceeded Dollar vs Brazilian Reais (USD/BRL) Benchmark, over 24 month period.|
|#_Funds_managed|Float|Count of how many different funds are managed by the same manager. Considering only funds within the sample.|
|Manager_avg_Assets|Float|Sum of assets under management for the fund manager. Considering only funds within the sample|


### Analysis
- <u>[Notebook 02 Data Exploration](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/EDA.ipynb)</u>
- <u>[Notebook 03 Data Modeling](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Notebooks/Building%20Models.ipynb)</u>
- The libraries used for modeling (e.g., `Pandas`,`numpy`, `Scikit-learn`)
- Used a Grid search through 4 different clustering models (K Means, Dbscan Agglomerative and Hierarchical) and changing hiper parameters (n_clusters, inits, linkage_method, affinity...).
- Analyzing  Silhouette Score, Inertia Score and number of observations in each cluster, K Means yielded the best results.
- Using the Elbow method to pick k indicates a high score variation depending on the number of clusters in the mode. In order to make interpretability more comprehensible, I found that 5 clusters was a well balanced choice.
- Final K means model used the default parameters except for `init = random` and `random_state=42`.
- Using the optimal model, I created a prediction column with the predicted cluster.
 - In order to facilitate model interpretability I used a `RandomForestClassifier` model to predict which cluster a row should be assigned to. The model had xxxx scores. The model´s most relevant coefficients where used to find build a table with different characteristics of each cluster.

#### Insert table
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
- Using unsupervised machine learning K-means clustering model a group of 1,300 was split into 5 different clusters with different characteristics.
- Using a supervised Random Forest Classifier to analyze the clusters the most important features used to select the cluster were which
  - Fund type (Fixed Income, Balanced, Equity ...)
  - Fund volatility
  - Fund Excess return compared Brazil risk free interest rate returns.
  - Fund size (assets under management)
- The framework used in this can be used to classify new fund in one of the clusters and understand differences among funds.



##### Recommendations
- Separate problem in 2 steps
 - Step 1: Cluster only quantitative features, analyize the results.
 - Step 2: Cluster only quantitative features, analyize the results.


- Try using different clustering methods
 - Spectral Clustering, MeanShift, AffinityPropagation.


- Test clustering with different feature combinations
 - Some of the features have a high correlation, perhaps using fewer features may achieve the same results.
