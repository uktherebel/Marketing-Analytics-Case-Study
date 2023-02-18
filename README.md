# Marketing-Analytics-Case-Study
# Overview 
In this Marketing Analytics Case, we needed to generate necessary data points necessary to populate the template attached below for a fictional company, DVD Rental Co. To generate the relevant data points, I reverse-engineered the problem. 

Skills Used: Data Wrangling, Statistical Distributions, ERD Analysis, Reverse Engineering, Window Functions, Hypotheses Validation

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

# Mapping the Joining Journey
Using the ERD analysis, it was deduced that a linear joining journey would be needed.

<img width="501" alt="Screenshot 2023-01-16 at 3 54 22 PM" src="https://user-images.githubusercontent.com/55969501/212661681-0c8ebe9a-2266-45b1-b0d9-b250c3d2f1ca.png">

