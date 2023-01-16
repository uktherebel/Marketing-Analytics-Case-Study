# Marketing-Analytics-Case-Study
# Overview 
In this Marketing Analytics Case, we needed to generate necessary data points necessary to populate the template attached below for a fictional company, DVD Rental Co. 

The requirements were as follows: 
1. Top 2 Categories 
> For each customer, we need to identify the top 2 categories for each customer based off their past rental history. These top categories will drive marketing creative images as seen in the travel and sci-fi examples in the draft email.

2. Category Film Recommendations
> 3 most popular films for each customer’s top 2 categories. We cannot recommend a film which the customer has already viewed. If there are less than 3 films available - marketing is happy to show at least 1 film.

3. Individual Customer Insights
> How many total films have they watched in their top category?
> How many more films has the customer watched compared to the average DVD Rental Co customer?
> How does the customer rank in terms of the top X% compared to all other customers in this film category?

4. Second Ranking Category
> How many total films has the customer watched in this category?
> What proportion of each customer’s total films watched does

![Unknown](https://user-images.githubusercontent.com/55969501/212595517-b2f4d547-b1b4-4eca-b31a-912e0de1f0be.png)

# Key Learning Outcomes 

# Data Source 
This project was a part of the Serious SQL apprenticeship by Danny Ma. The data used is from the `dvd.rentals` schema in the `serious-sql` database.

# Entity Relationship Diagram
![Unknown-2](https://user-images.githubusercontent.com/55969501/212652223-81b393a6-88df-4591-b426-5d996ac2d5cd.png)

#### The ERD above was used to review all necessary raw datasets and understand the connections between the tables. 

# SQL Reverse Engineering 
The strategy used was to **reverse-engineer** the final solution. 

The approach starts with identifying the final outputs needed for the business requirements, and working backwards to identify the necessary data points and processing steps.

The final SQL output will have a single row for each customer and contain the necessary columns for the marketing team to execute their campaign. 

To sum, the approach is to start with the final output, and work backwards to identify the necessary data points and processing steps to generate the final output.

# Joining Multiple Tables 

### Plan of Attack 
#### 1. Defining Final State
    - Key columns needed need to generate data points at `customer_id` were identified: `category_name`, `rental_count`, `average_comparison`, `percentile`, and `category_percentage`.
> `category_name`: The name of the top 2 ranking categories  
`rental_count`: How many total films have they watched in this category  
`average_comparison`: How many more films has the customer watched compared to the average DVD Rental Co customer  
`percentile`: How does the customer rank in terms of the top X% compared to all other customers in this film category?  
`category_percentage`: What proportion of total films watched does this category make up?


#### 2. Reverse Engineering 
The `rental_count` was identified as the key value for the analysis, as it is used in all of the calculations. 

Removing all the dependent calculated columns: `category_ranking`, `average_comparison`, `percentile` and `category_percentage` would give us the following table: 

<img width="374" alt="Screenshot 2023-01-16 at 3 42 49 PM" src="https://user-images.githubusercontent.com/55969501/212659482-a8c43b33-92f7-4537-b13d-4d60d0a25e3f.png">

**Problem**: Generating a table with only the top 2 categories for each customer and their `rental_count` values meant we wouldn't be able to calculate the fields (`average_comparison`, `percentile`, and `category_percentage`) that need to be compared against all customers and categories. 

Therefore, to solve this problem, it was necessary to include all of the categories for each customer and not just the top 2.

#### 3. Identifying Key Columns and Start & End Points
To calculate the number of films that a customer has watched in a specific category, the key columns needed were `customer_id` and `category_name`. 

The analysis began with the `dvd_rentals.rental` table as it was the only place where the `customer_id` field existed and the only place where it was possible to identify how many films a customer has watched. 

However, the `dvd_rentals.rental` table did not include the `category_name` field, which was needed for the analysis. The only table that included the `category_name` field was the `dvd_rentals.category` table.  This marked the end point of the data joining journey. 

#### 4. Mapping the Joining Journey
Using the ERD analysis, it was deduced that a linear joining journey would be needed.

<img width="501" alt="Screenshot 2023-01-16 at 3 54 22 PM" src="https://user-images.githubusercontent.com/55969501/212661681-0c8ebe9a-2266-45b1-b0d9-b250c3d2f1ca.png">

### Framework for Analyzing Table Joins

The following framework was used to analyze table joins: 

1. What is the purpose of joining these two tables?  
a. What contextual hypotheses do we have about the data?  
b. How can we validate these assumptions?

2. What is the distribution of foreign keys within each table?

3. How many unique foreign key values exist in each table?
