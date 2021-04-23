# Product_Recommendation_System

**Problem Statement**
The enterprise has a plan to increase its revenue by allocating various products to its existing customers. 

**Analysis: **
To target customers to recommend various products, the company has to work on the existing data and develop a solution where the customers are likely to use the recommended product. 
**
What is a recommender system?**
Recommender systems are information filtering systems that deal with information overload by filtering vital information fragment out of a large amount of dynamically generated information according to the user’s preferences, interest, or observed behavior about an item. The recommendation system can predict whether a particular user would prefer an item or not based on the user’s profile. Therefore, the need to use efficient and accurate recommendation techniques within a system that will provide relevant and dependable recommendations for users cannot be over-emphasized.

**Dataset:**
The dataset contained the list of the Customer IDs along with the number of services bought (from P1 to P9), ratios of services being used, number of services assigned, customer size, segment (S_1 to S_5), time since purchase and few unknown variables (Var1, Var2, etc.). The company’s revenue came only from the number of services being used. Hence, to increase revenue, we had to find customers who could use more services based on different data features present in the dataset.

**Data Preprocessing:** The data consists of 5949 companies with their usage for each product. The data consists of 15.61% missing values in most of the features. After removing those entries, the data now has 4974 rows. The products, namely “P7”, “P8”, “P9”, are removed because of insufficient data to get insights for those products. The feature “Purchase_date” is modified as “Year,” taking only the purchased year to make the data precise.
**
Negative Values**
Some of the companies have negative entries, which will mislead the results while performing machine learning techniques. Trimming these entries gives an advantage of improving the models.

**Limits: **
The features present in the data such as “P1_Ratio”, “P2_Ratio”, “P3_Ratio”, “P4_Ratio”, “P5_Ratio” and “P6_Ratio” has ratio values greater than 1 for some of the companies. Ideally, the maximum value of the ratio must be one and not less than zero. The data was modified that no entries have ratios greater than one and less than zero. 
The features depicting the companies license size and allocated licenses are “P1_Size”, “P1_E”, “P2_Size”, “P2_E”, “P3_Size”, “P3_E”, “P4_Size”, “P4_E”, “P5_Size”, “P5_E”, “P6_Size” and “P6_E”. Ideally, the value of the allocated licenses should not be greater than the companies actual license size. The data has been modified so that no allocated value is greater than its size.


**Action plan**
The percentile range with an increment of 0.05 range was adopted to analyze companies' percentage using the products.
 
A threshold value has to be considered to convert the continuous ratio variables into binary ratio variables. The advantage of converting them into binary is making it a classification problem and move further towards recommending products to the companies.
p1_limit=0.527474	p2_limit=0.200000	p3_limit=0.173738

p4_limit=0.150022	p5_limit=0.092294	p6_limit=0.411560
Table 1: Threshold values for six products

The above-described values are limits for each of the products given to get the binary values. Any ratio values below the limit are assigned to zero, and ratio values above the limit are assigned to one. 

**Data Mining Tasks**
The data has been modified into a classification problem. The data was split into train and test data to check the accuracy of the machine learning models. Feature selection has done using the ExtraTreesRegressor library to get the variables that are mostly affecting the dependent variable.  


Six machine learning algorithms are used: Classification and Regression tree (CART), Random Forest, Logistic Regression, XGBoost, AdaBoost and K Nearest Neighbours Regression. Ratio variables are taken as dependent variables (“P1_Ratio”, “P2_Ratio”, “P3_Ratio”, “P4_Ratio”, “P5_Ratio”and “P6_Ratio”) and variables obtained after feature selection are taken as independent features. After executing the listed algorithms, the corresponding confusion matrix is used to examine the “False Positive count.” 
When the actual outcome is zero and the predicted outcome is one, it is known as the False Positive rate. It plays a crucial role in recommending products to customers. Customers who are not using the product but are found to be using the product during our algorithms testing are taken as a subset to recommend the products.

**Methodology**
 We are targeting the companies falling under the misclassification of type False Positive. We expect that such companies are having an urge to use the product. But all the companies in this category are not equally likely to have the same magnitude of urge to use the product. Some companies are more likely to be interested in the product and some are less, depending on the nature of their business, size of customer, work area, etc. So, we quantify this magnitude of being a potential company by defining a coefficient which we call as Opportunity

where, opportunity=P_Size×deviation⁡(P_Ratio)
deviation⁡(P_Ratio)=  predicted⁡(P_Ratio)KNNRegressor -⁡〖P_Ratio〗

**Results** 
Each product can be recommended to a set of companies which we have obtained after the complete process. For each product, we extracted a list of companies which are most likely to be interested in using the product. This companies can either be a new user or regular user who wants to increase its usage significantly.


We found 100+ potential companies for product 1, 50+ potential companies for product 2, 300+ potential companies for b, 200+ potential companies for product 4, 50+ potential companies for product 5, 1500+ potential companies for product 6. 

**Conclusions**: 
This project deals with problem of evolving recommendation system. We used misclassification from 5 classifiers to locate the willingness to use the product. The false positive samples tend to jump from potential to optimized class. The error in recommendation is optimized by majority vote system after giving equal votes to each classifier. Then we used KNN Regressor to predict the expected value of product usage ratio which was key factor in estimating the coefficient of intensity of willingness. The coefficient is calculated by taking difference of predicted and actual usage ratio and then the product of this coefficient and size of license issued, gives the value of opportunity. Hence, we first extracted the most potential companies then we sort them by their opportunity values. This study reveals that Product 2 and Product 5 are getting the least number of recommendations and Product 6 is getting the maximum recommendations.  P1_Ratio is not affecting P4_Ratio, P5_Ratio and P6_Ratio significantly. All the ratios are very much depended on the Segment in which the companies fall. 
This can be further extended to make this process user-friendly by building an interactive dashboard which allows user to gain enough information about the products. It is found that some companies tend to stop using the product. This study can be slightly modified to analyze the customer retention factor also. 
