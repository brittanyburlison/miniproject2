# miniproject2
EXECUTIVE SUMMARY 

For our project we wanted to identify which clients from XYZ Bank would subscribe for a term deposit. We were provided with a data set containing 20 columns and 41,188 rows. We began our work by doing some data preparation and cleaning to the provided data set. We did multiple data cleaning techniques such as renaming columns, imputing missing values and so on. We explain this in more detail in our data preparation segment. After we had cleaned and prepared our data we got to work on our modelling. We ran the following models: Logistic Regression, Gradient Tree Boosting, Random Forest and Decision Tree. We also looked at feature importance and K-Means clustering. After we had modelled and evaluated our data, we came to our conclusions that can be found in our evaluation section of this report.  

 

BUSINESS UNDERSTANDING 

XYZ Bank wants to identify which clients will subscribe for a term deposit. The Bank wants us to conduct Exploratory Data Analysis (EDA) to identify relationships, trends in data. Along with EDA, the Bank expects a predictive model to roll out for future use; explore different techniques and share findings about the approach and advantages of the best model identified. Make prescriptive recommendations if any. 

 

DATA UNDERSTANDING 

The data is about XYZ Bank’s direct marketing campaign. Marketing campaigns were driven by telephone calls. In many cases, more than one contact for the same client was required, in order to access if the product (deposit) would be ‘yes’ or ‘no’, subscribed. The dataset, XYZ_Bank_Deposit_Data_Classification.csv contains 20 columns and 41,188 rows.  

 

DATA PREPARATION / EDA 

The csv provided was cleaned and explored in pyspark. Our full code can be found in the appendix. We initially looked at the data in Notepad++, where we found that it actually is separated by semicolons, not commas. Additionally, several of the columns had periods in them, which cannot be read easily by pyspark, as the code interprets them as attempting a function. We renamed all columns containing periods to use underscores instead for ease of use.  

 

Text, table

Description automatically generated with medium confidenceSubsequently, we ran code to identify different variable types (integer, categorical, and double) in order to run summary statistics on the different types.  

 

We can see that duration, pdays, and previous all have zeros as their minimum, meaning they were missing. We replaced all zeros with null, and then imputed the missing values for all integer variables.  

 

We analyzed the distribution of numerical features in histograms and identified age, duration, campaign, and previous as needing transformations. We used log transformations to achieve a normal distribution for each of them. Below is the original duration value distribution alongside the log transformation value.  

 

Chart, histogram

Description automatically generated Chart, histogram

Description automatically generated 

 

For categorical variables, we used OneHotEncoder and a pipeline to make all categorical variables model-ready.  

We performed a correlation matrix plot to check for strong or weak correlations. The correlation matrix plot is below.  

 

 

MODELING  

The models tested were: Logistic Regression, Decision Tree, Gradient Boost Tree, and Random Forest. The target variable is y, a binary feature representing whether a customer will sign up or not. The ratio of the target variable is 7.88:1, because of this imbalance models were evaluated based on their ROC AUC score, they are displayed in the table below. All models were tuned using grid search and all scores are the mean of a 4-fold cross validation. 

Model 

ROC AUC Score 

Logistic Regression (LR) 

0.936 

Gradient Boosting Tree (GBT) 

0.946 

Random Forest (Forest) 

0.935 

Decision Tree (Tree) 

0.851 

 
The champion model is the Gradient Boosting Tree. This model provides the strongest predictions and feature importance scores.  

EVALUATION 

The feature importance is shown below of the top features. 

.Chart, bar chart

Description automatically generated 

The features importance scores show how helpful a feature is for the model to make a prediction. The Log of Duration being by far the strongest predictor. This may be self-fulfilling, because Duration indicates how long the previous phone call was, which calls where a customer subscribes to a term deposit are likely taking longer than a call where a customer is not subscribing. Granted this is referring to the previous call. For further insight we must look at the distribution of each feature to our target variable. Below is the mean duration value grouped by the target. 

Chart, bar chart

Description automatically generated 

We can conclude that a longer phone call is indicative of a customer subscribing because the mean is greater for target = yes and we know the feature is important in predicting. Below are Euribor 3 month and Log of Campaign to examine the direction of the relationship. 

Chart, bar chart

Description automatically generatedChart, bar chart

Description automatically generated  

We see here that a lower mean rate of Euribor is associated with term deposits, and less contacts during a campaign also is moving our prediction towards the customer enrolling. 

We recommend focusing campaign efforts while the Euribor 3-month average is less than 3. We also recommend implementing any strategies for maintaining the customer on the phone for a longer duration, for example if going into detail about the term deposits results in longer phone call duration then encourage associates to go into specific detail. Last, we recommend scaling back on campaigning after a certain threshold to not waste efforts and to not associate campaigns efforts from XYZ as something to be rejected out of hand. This seems to be the case based on the greater average Log Campaign length of customers who do not end up subscribing. 

K-MEANS CLUSTERING  

K-means clustering is one of the simplest and popular unsupervised machine learning algorithms.  

Silhouette analysis can be used to study the separation distance between the resulting clusters. The silhouette score measures how close each point in one cluster is to points in the neighboring clusters and thus provides a way to assess parameters like number of clusters. 
 
From the plot below we see that a cluster of 6 is ideal as K=6 is where a local maximum of Silhouette Score is observed.  

 Chart, line chart

Description automatically generated 

 

 

 
