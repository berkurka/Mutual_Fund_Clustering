# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Mutual Fund Clustering

## Project Author
- Bernard Kurka | <u>[LinkedIn](https://www.linkedin.com/in/bernardkurka)</u> | <u>[Email](bkexcel2014@gmail.com)</u>


## [Presentation Slides](https://docs.google.com/presentation/d/1a9jGkPlWrMeTOaTl-t5zsYTpBsu5WPCP6Zb0eF-3wws/edit?usp=sharing)


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

I started the project using a database with 4,082 open-end Brazilian mutual funds destinated to Non-Institutional investors. I removed funds that where terminated or where recently created (last 24 months), the number went down to 1,300 funds.

I selected 42 features to fit in unsupervised clustering algorithms. Nearly half of the features are related to the fund qualitative characteristics such as classification, benchmark, management fee and so on. The other features are related to funds quantitative indicators such as fund assets under management, return, volatility and so forth.


I ran 4 different clustering models (Kmeans, Dbscan, Hierarchy and Agglomerative) using several hyperparameters combinations, analized the Inertia, Silhouette and cluster count distribution. The highest Silhouette scores models were ocorring with a lower number of centroids (k), and a highly concentrated cluster count, that means that a most of the observations have similar feature values hand full of funds with very different feature values.

I chose the xx model

 Model create X distinct clusters.
 - cluster 1: Limite
 - cluster 2: Moder
 - cluster 3: Hig
 - cluster 4: Highest .


We developed a Python Class that given a list of NYC Zipcodes or neighborhood names will access the API gather data for these neighborhoods and use a KNN model to predict wich cluster it belongs. The Class also has plot functions to compare the given Zipcodes with the 4 static clusters and there is also a option to print results in NYC map.

### The Data
##### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**zip**|*object*|KMeans Clustering|String for each of 278 ZIP codes across New York City boroughs|
|**location**|*object*|KNN Classifier|String of ZIP code or text location query parameter being classified with KNN model|
|**pr_1s**|*float*|KMeans Clustering, KNN Classifier|Floating point standardized ("s") value for number of \$ priced ("pr_1") establishments in top 100 best match for search location|
|**pr_2ws**|*float*|KMeans Clustering, KNN Classifier|Floating point standardized ("s") value for number of \$\$ priced ("pr_2") establishments in top 100 best match for search location, weighted ("w") by price level|
|**pr_3ws**|*float*|KMeans Clustering, KNN Classifier|Floating point standardized ("s") value for number of \$\$\$ priced ("pr_3") establishments in top 100 best match for search location, weighted ("w") by price level|
|**pr_4ws**|*float*|KMeans Clustering, KNN Classifier|Floating point standardized ("s") value for number of \$\$\$\$ priced ("pr_4") establishments in top 100 best match for search location, weighted ("w") by price level|
|**pr_totws**|*float*|KMeans Clustering, KNN Classifier|Floating point standardized ("s") value for total weighted price counts ("tot", "w") for top 100 best match for search location|

- [Notebook 02 - Yelp Fusion API](https://github.com/twludlow/ga_project_4/blob/master/notebooks/02%20-%20Yelp%20Fusion%20API.ipynb)
- [Notebook 03 - IRS Data](https://github.com/twludlow/ga_project_4/blob/master/notebooks/03%20-%20IRS_data_collection_and_cleaning.ipynb)
- [Notebook 04 - API Pull for Training Data](https://github.com/twludlow/ga_project_4/blob/master/notebooks/04%20-%20API%20Pull%20for%20Training%20Data.ipynb)
- Our data was acquired via Yelp's Fusion API `from yelpapi import YelpAPI`.We set our Yelp Fusion API Key and established an API connection. From there we stored the data we gathered into a `Pandas` DataFrame.
- The search criterias included all Yelp´s categories (shops, restaurants ..), filtered by Yelp´s "best mach" option.
- We gathered top 100 business prices and reviews from 278 NYC zipcodes.




### Analysis
- [Notebook 05 - Yelp Cluster Gridsearch](https://github.com/twludlow/ga_project_4/blob/master/notebooks/05%20-%20Yelp%20Cluster%20Grid%20Search%20-%20NYC.ipynb)
- [Notebook 06 - K-Means Modeling](https://github.com/twludlow/ga_project_4/blob/master/notebooks/06%20-%20Yelp%20K-Means%20Model%20-%20NYC.ipynb)
- intro sentence about our software requirements (e.g., `Pandas`, `Scikit-learn`)
- Used a Grid search through 3 different clustering models (K Means, Agglomerative and Hierarchical) and changing hiper parameters (n_clusters, inits, linkage_method, affinity...).
- Analizing Silhouette Score, Inertia Score and number of observations in each cluster, K Means yielded best results.
- Using the Elbow method n_clusters = 4 was found to be a good balanced choice.
- Final K means model used the default parameters except for init='random' and random_state=42.
- Using these models, we developed a class for use by our client: yelpaffluence_nyc.py class YelpAffluence_NYC
 - Methods for YelpAffluence_NYC object include tools to fit the model to NYC data, query Yelp API for list of locations, plot results in a bar graph by price level and plot results on NYC map.


### Conclusion
- [Notebook 01 - Yelp Affluence Demo](https://github.com/twludlow/ga_project_4/blob/master/notebooks/01%20-%20Yelp%20Affluence%20Demo%20190118.ipynb)
- [Notebook 07 - Yelp Class Development](https://github.com/twludlow/ga_project_4/blob/master/notebooks/07%20-%20Yelp%20Class%20Development.ipynb)
After optimizing our K-Means model, we deployed the K-Nearest Neighbors Classifier (n=15) to assign a label to our queried locations.  We found that the K-Means model sorted all NYC ZIP codes into 4 separate groups, which we have labeled "\$", "\$\$", "\$\$\$", and "\$\$\$\$" to match Yelp's existing pricing scale.

We noted that locations in each group shared distinct characteristics, and that our class designation presents a meaningful economic description for a particular location.

- \$ - Red
 - Limited economic activity across all price ranges (\$ - \$\$\$\$)

- \$\$ - Orange
 - Moderate economic activity in the \$ and \$\$ price levels
 - Limited activity in the \$\$\$ and \$\$\$\$ price categories

- \$\$\$ - Green
 - Highest activity in \$\$ price level
 - Increased activity in \$\$\$ and \$\$\$\$, but not highest

- \$\$\$\$ - Blue
 - Highest activity of all locations in \$\$\$ and \$\$\$\$ price establishments
 - High activity in \$\$ category

These trends are confirmed with inspection of the mean distribution of top-100 establishment price levels for each Yelp Affluence level.

##### Recommendations
- Feed other models with cluster results
 - This information can be useful as an economic rating variable in a predictive model

- Pay to use the Yelp Fusion VIP API
 - Will allow for commercial-scale queries

- Beware of ZIP query results
 - Yelp returned out of state results for some NYC-based zipcodes
 - e.g. 10015 returned results in Tucson, AZ

- Gathering and testing more data
 - Beyond the top 100, best match results

- Expanding class functionality
 - Enable collection of new training data
 - Automate model optimization

- Scaling the model
 - Train on other large metropolitan areas and check consistency of results
