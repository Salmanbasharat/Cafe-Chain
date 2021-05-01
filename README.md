# **Cafe Chain Analysis**

## **Segment 4 of the project :-**

## **Presentation**
The presentation [can be reached here]( https://1drv.ms/p/s!AkVDqlS3Ei2agpo9MclSiN3mLx4cQA?e=pUWede)

In this project presentation, I have addressed the following:
### **Selection of Topic**
This is the analysis of a *Cafe chain* business which wants to understand its customers.

### **Reason of selection of This Topic**

Understanding of the customer base is one of the most important aspects of any business and same is true for a retail chain running coffee shops across the country. If the management has deep understanding of its business, they can take correct decisions to expand their business and make it profitable. The major reasons why I selected this data are:

* Real Life Example​
* Large Scale Business​
* Can be used for Machine Learning​
* Helpful for Data Visualizations​
* Data driven decision making in business​
* Understanding the Core Customer​

### **Description of The Data**

This is a real-life data collected by the management of "Our Cafe"" (Not the actual name for confidentiality reasons)- a  cafe chain business running their outlets across the country. It contains transaction‐level data from eight "Our Cafe" locations in a recent year. For each store, we have a random sample of daily transactions for 10 randomly selected days of each month. Each observation in the data represents a transaction and includes information on the specific items purchased and the prices and caloric content of those items. The data are limited to transactions that involve at most one drink and one food item — the vast majority of all transactions fall into this category. In addition,there is information about the demographic characteristics of the customer as well as the customer’s responses to three survey questions. 

Finally, there are features that indicate whether "Our Cafe" location at which the transaction took place, competes directly with a *medium size retail chain*, a *big retail chain* and an independent coffee shop. The precise variable definitions are below:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/cafe_data_features.png)

### **Questions to Answer**

There are many pertinent business questions a business might want to address to scale it's revenue and expansion. In the current analysis, I look forward to address the following questions :

* **Prediction of repeat customers (Machine Learning)**
* **Recommendation of Food/ Drink items for the customer based upon their demographics and answers to 3 survey questions related to their preference of Taste/ Calories/ Price in making their purchase (Machine Learning)**
* Identification of Customer Preferences (Taste/Price/ Calorie)​
* Core Customer of “Our Café”​
* Repeat Customers & Store Wise Distribution​
* Highest Revenue Stores​
* Popular Food / Drink Items  & Demand over the year​
* Customer Demographics​
* Customer Spending Habits​
* Survey Answers Vs Actual Purchases​

### **Data Exploration phase**
In this phase, we are working on following:
* Data visualizations​
* Customer Demographics data​
* Stores and their order variations​
* Food and drink items​
* Store Performance​
* Repeat Customers & trends​
* Data set division as per machine learning model requirement​

Here are few images of Data exploration at this stage:
### **Customer Responses**
![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/cust_preference.png)

### **Popular Food/Drink Across All Shops**
![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/food_items.png)

### **Repeat Customer Orders**
![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/repeat_cust_orders.png)

## **Database Formation**
The project data has been stored in "postgreSQL" and being queried using SQLAlchemy and Flask.

I have initial dataset named: cafe_data.csv, which stores static data, as below:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/cafe_data_csv.png)

Dataset has been connected with **pgAdmin** in a Database named **cafe_db** with the help of following connection code in the Python scripts, for the interface:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/database_connection.png)

After having created tables customer_info, order_info and competitors from my original dataset cafe_data.csv and a complete table named cafe_original_data, in my database cafe_db,  to organize the data, I established relationship between all the tables using the following snippet:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/relationship_between_tables.png)

Entity Relationship Diagram from the established relationship is as presented below:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/ERD.png)

Below is the code snippet to present the usage of SQL joins:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/joins.png)

## **Data Analysis phase**
In the analysis of the data, I have performed the following to prepare machine learning model for recommending Food & Drink Items, as per their Demographics & Preferences, and identification & prediction for the Repeat Customer​ for "Our Cafe":

* checked statistical validity of our data
* checked for nulls and deleted as required
* checked datatypes and took out wrong datatype values and re-transformed datatypes
* dropped or excluded irrelevant columns
* visualized our data
* binned data where appropriate
* checked columns for unique values
* split data into training and testing datasets
* created calculated conditions for our scripts for machine learning model
* supervised and unsupervised learning, dimensionality reduction
* rescaling data



## **Machine Learning Model**
I'm analyzing the dataset with different machine learning models to predict the following as explained briefly below:​​
### **Identifying & Predicting the Repeat Customer​**

#### **Description of preliminary data preprocessing:**

- I have a customer_info table with features which includes information about demographics of customers such as gender, age, cust_income. In addition, I have answers from the customers for three survey questions. These questions are about customer preferences towards taste, calories and price. I have order information of customers with calories and price.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/database_and_tables_in_postgresql.png)

- I joined customer_info and order_info tables after establishing connection with database cafe_db using SQL join for postgreSQL.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/preprocessing_repeat_cust.png)
#### **Description of preliminary feature engineering and preliminary feature selection, including their decision-making process:**
- From the joined table I have picked every column in cust_info table and total_spend features from orders_info table to define regular customer dataframe named reg_cust_df. By using these features, I have determined the number of visits by every customer based upon the cust_ID. 
- I dropped the null values from the reg_cust_df dataframe which I made in the above step.
- I created some income ranges and used them as bins to use them in features instead of customers' specific income values.  
- In this table, I further filtered regular customers on the basis of a condition where every customer who has visited more than or equal to five times is considered as a regular customer
- Next, I created features by dropping cust_ID, cust_income and reg_cust column 
I selected regular customer as target 

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/prelim_features_repeat_cust.png)
#### **Description of how data was split into training and testing sets**
- I used **sklearn** training_ test_split method to split my data into training and testing sets.	
- Used **Standard scaler** to scale our training and testing data by fitting the scaler on training data set and use that transformed training and testing datasets for my machine learning model
#### **Explanation of model choice, including limitations and benefits**
- To perform my machine learning predictions I used SVM,  EasyEnsemble, Neural Networks and Random Forest Classifier (RFC). Out of all these algorithms, RFC was able to give the predictions with most accuracy of **78%** .

- Also, this model gave me respectable scores for classification .
	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/repeat_cust.png)

- According to the classification report, the precision of prediction of repeat customers is 73% , which means if this model predicts someone to be repeat customer, there is a 73% chance that this prediction is correct. The recall for this prediction is 68% that means if someone is repeat customer, there is 68% chance that this model will predict them as repeat customer.

- At the end I saved the model and the standard scaler to use it in the flask app for our dashboard. 

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/sav_model_repeat_cust.png)
	
 

### **Recommending Food & Drink Items as per their Demographics and Preferences​**

**A: Machine learning model for FOOD items clustering and recommendation prediction**
-	After establishing connection with my database ‘café_db’, where I already have all the tables from my **Database Formation** phase, I joined customer_info table and order_info table using SQL join query to select required data.

From the resultant table , I dropped null values in **cust_ income** and 'food_type' columns, removed columns related to the **drink** and **total_spend**, as I don't need them in the model to predict the recommendation of food items. 

	
- #### **Description of preliminary feature engineering and preliminary feature selection, including their decision-making process:**

	- I used unsupervised machine learning model to cluster food items based upon the food_calories and food_price.
	

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/preprocessing_food.png)

	
	Further, the **elbow curve** method was used to determine the option value for number of clusters for **KMeans algorithm**, which I came up as 3 clusters as below:

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/elbow_curve_food.png)
	
	Then I used KMeans algorithm with 3 clusters to predict the classes of the food items mentioned . I created a dataframe clustered _df using the clusters from KMeans algorithm to have all the unique food items with their classes and food_type.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/food_items_cluster.png)
	
	- Created food_class dataframe for sending it to a csv file to use it later in flask app.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/food_items_to_csv.png)

	- Next I use the supervised machine learning to predict the class of the food items, for the customer based upon their gender, age, preference of taste, calories_importance, price_importance and the current month.
	- Created ranges for calories and price by specifying required conditions

	-  Defined features and target for supervised machine learning

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/features_and_target_food_items.png)
- #### **Description of how data was split into training and testing sets**
	- I used **sklearn** training_ test_split method to split our data into training and testing sets.	
	- Used **Standard scaler** to scale our training and testing data by fitting the scaler on training data set and use that transformed training and testing datasets for our machine learning model

- #### **Explanation of model choice, including limitations and benefits:**

	- To perform my machine learning predictions I used SVM,  EasyEnsemble, Neural Networks and Random Forest Classifier (RFC). Out of all these algorithms, RFC was able to give the predictions with most accuracy of **92%**.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/rfc_food.png)

	- Also, this model gave me respectable scores for classification .
	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/food_cluster.png)

	- At the end I saved the model and the standard scaler to use it in the flask app for our dashboard. 

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/sav_model_food.png)

**B: Machine learning model for DRINK items clustering and recommendation prediction**

- #### **Description of preliminary data preprocessing:**

	After establishing connection with my database ‘café_db’, where I already have all the tables from our **Database Formation** phase, I joined customer_info table and order_info table using SQL join query to select required data.

	From the resultant table , I dropped null values in **cust_ income** column, columns related to the **food** and **total_spend**, as I don't need them in the model to predict the recommendation of drink items. 
	Also I dropped the null values in the **drink_type** column .

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/preprocessing_drinks.png)
- #### **Description of preliminary feature engineering and preliminary feature selection, including their decision-making process:**

	- Replaced null values in the 'drink_milk' column with a space white space character 
	- Joined the 'drink_size', 'drink_type' and 'drink_milk' columns to create a new column 'Drink_Type'

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/feature_eng_drink.png)

	- I used unsupervised machine learning model to cluster drink items based upon the drink_calories and drink_price.
		
	Further, the **elbow curve** method was used to determine the option value for number of clusters for **KMeans algorithm**, which I came up as 5 clusters as below:

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/elbow_curve_drinks.png)
	
	Then I used KMeans algorithm with 5 clusters to predict the classes of the drink items mentioned . I created a dataframe clustered _df using the clusters from KMeans algorithm to have all the unique drink items with their classes and Drink_Type.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/drink_items_cluster.png)
	
	- Created drink_class dataframe for sending it to a csv file to use it later in flask app.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/drink_items_to_csv.png)

	- Next I used the supervised machine learning to predict the class of the drink items, for the customer based upon their gender, age, preference of taste, calories, price and the current month.
	- Created ranges for calories and price by specifying required conditions
	-  Defined features and target for supervised machine learning

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/features_and_target_drink_items.png)
- #### **Description of how data was split into training and testing sets**
	- I used **sklearn** training_ test_split method to split our data into training and testing sets.	
	- Used **Standard scaler** to scale our training and testing data by fitting the scaler on training data set and use that transformed training and testing datasets for my machine learning model

- #### **Explanation of model choice, including limitations and benefits:**

	- To perform my machine learning predictions I used SVM,  EasyEnsemble, Neural Networks and Random Forest Classifier (RFC). Out of all these algorithms, RFC was able to give the predictions with most accuracy of **92%**.

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/rfc_drinks.png)

	- Also, this model gave me respectable scores for classification .
	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/drink_cluster.png)

	- At the end I saved the model and the standard scaler to use it in the flask app for our dashboard. 

	![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/sav_model_drinks.png)
## **Dashboard Preparation**
I'm using *Tableau* for our data visualizations. The interactive elements on the story board are the filters I have used on all the pages of the story board. Using these filters, I can explore the trends in data for my questions as described above.

Below is a glimpse of our Tableau Storyboard.

### **Tableau Storyboard**

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/main/Resources/Tableau_storyboard_blueprint.png)


My **Tableau dashboard** for the detailed Visualizations [can be reached here](https://public.tableau.com/profile/kirti.bhandari#!/vizhome/Coffee_Cafe_Chain_Project/Story1?publish=yes)

 To present my Machine Learning model, I have prepared an interactive *Web Application* (using Flask, HTML, JavaScript) to display the options to the Cafe management to predict **Repeat Customers'** and the customers to **Recommend Food/Drink items** based upon their demographics and preferences.
### **Machine Learning Dashboard**

I have developed an interactive Web Application to help Management of the Cafe chain to identify a repeat customer. 

A glimpse of this app is as below:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/machine_learning_model_dashboard.png)

Through this dashboard of Machine Learning, I can:
* **Predict Repeat Customer**
* **Recommend Food/Drink Items** on the basis of customer preferences.

When I click on our first button **Predict Repeat Customer**, on the dash board, a form opens up to fill up the details about the customer such as customer's gender, age, income range, preferences taste, price and calories and total spend by the customer for current order.
![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/predict.png)

Once I hit **Submit** button, I'm able to predict likelihood of whether this customer will be a **REPEAT  CUSTOMER**, using my machine learning model at the backend.

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/predict_repeat_cust.png)


In the same manner, when I click on **Recommend Food/Drink items to Customer** button, there opens up another form to provide customer's details as below:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/recommend_food.png)

After I submit the details, I'm able to predict the **FOOD/DRINK** items based upon customer's preferences and related information, as below:

![](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Kirti/Resources/recommended.png)

A **VIDEO CAPTURE** may be downloaded from this [LINK](https://github.com/UTOR-VIRT-DATA-PT-10-2020-U-B-TEAM-5-FP/Final_Project/blob/Ehsan/Flask_video.mov?raw=true) here and can be run on one's system like a video clip, to review the Web Application's functionality.
## **Summary of analysis**
* Accuracy of my Machine Learning model to predict repeat customer is **78%** 
* Prediction of FOOD items is done accurately by **92%**
* DRINK items are recommended by out Machine Learning Model with **92%** accuracy.
* Most important feature on which **Core Customers** of **Our Cafe** depend is their **Age**.
* **Highest Revenue Store** is **Store 568**
* I have **23.51%** repeat customers.
* Store which has **Most Repeat Customers** is **Store 511**
* Most of our customers are of **Age group : 30-40** and **Income Group : 50K to 75K**
* Customers **Preferred TASTE** above calories and price respectively.
* Most **Popular Food Item** is **Blueberry Scone**
* Most **Popular Drink Item** is **Drip Coffee**

## **Recommendation for future analysis**
* More data points(transactions) could be made to avail for the analysis as it is only for 10 days data out of 30 days of a month, it will help in improving the prediction accuracy even further.
* More data points will also help in suggesting the new store locations.
* Locations of stores may be provided to analyze data from the perspective that how location impacts revenue of a store.
* Budget information for marketing campaign may be gathered.
* Data about competitors sales to have comparison of performance and help in strategizing new customer acquisitions.
