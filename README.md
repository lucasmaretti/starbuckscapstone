# starbuckscapstone
Capstone project for Udacity's Data Scientist Nanodegree
## <img src="https://images.unsplash.com/photo-1603361513137-219be38712ed?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1776&q=80" class="center" width="600"/>

Read the medium article for a more comprehensive view: https://lucasmaretti.medium.com/understanding-customers-preferences-through-data-a-starbucks-marketing-campaign-analysis-9f4d0c056144

# Starbucks promotional data analysis project

Link to Github repository: https://github.com/lucasmaretti/starbuckscapstone/


## Table of Contents

1. [Introduction](#introduction)
2. [Data description](#data)
3. [Problem statement and metrics](#statement)
4. [Data Wrangling](#wrangling)
5. [Conclusions](#conclusions)
6. [Licensing, Authors, and Acknowledgements](#licensing)

## Introductionn<a name="introduction"></a>

Starbucks is an American chain of coffeehouses originated in Seattle and has the accolade of being the worlds' largest in its niche market. The company is, as of November 2021, present in 80 countries with over 30 thousand stores spread across the globe. Being a company so big increases the challenges when developing marketing strategies and acquiring information about its users. In order to tackle these challenges the company released its own app, which is used to place orders, make payments and also send marketing-related promotional offers for the customers. All of this generates data for the company, that can use it to drive business data driven decisions.


## Data description <a name="data"></a>

The aim of this capstone project was to analyze the promotional offers and transaction data from the app , which were kindly provided by Starbucks. The data collected and generated from the interaction of the users with the app make up for the raw data used in this capstone project, which is comprised of 3 JSON files:
Profile.json - Contains users' age, gender, income, and date of membership
Portfolio.json  - Comprised of informations such as difficulty of the offers (meaning how much the user has to pay in order to complete it), channel used for communication, such as web, email, mobile or social media or a combination those, reward- how much the user gets for completing the offer- and classification of the offer, which can be one of three categories: Discount, Buy-one-get-one (BOGO) or Informational. Also, there is a total of 10 different offers.
Transcript.json -Records of interactions of users with the offers and amount spent (if any).

## Problem statement and metrics <a name="statement"></a>

Problem statement
The main goal of this project was to use this data to determine which demographic groups respond best to which offer type. For that goal to be achieved 2 approaches were used: visualizations through exploratory data analysis and clustering using the k-means algorithm. A possible outcome expected from the analysis would be something like: 'male customers of a certain age range and income tend to complete a certain type of offer more often.'

Metrics
For the k-means algorithm the fundamental step is to determine the optimal number of clusters into which the data may be clustered. The Elbow Method is one of the most popular methods to determine this optimal value of k. This approach is more qualitative and it was used combined with the the silhouette scored method, which is quantitative to determine the optimum number of clusters. By combining the 2 approaches, an optimal number of 4 clusters was defined.

### Data wrangling and Feature engineering <a name="wrangling"></a>
Data cleaning and wrangling was specially tricky in this project due to the fact that each offer could go one of 3 ways: it could be received, viewed and completed - in which case it would be classified as "offer_complete"; it could be received, viewed and not complete - then classified as "offer_ignored" or it could be received, not viewed and completed- the classification in this case was "accident_completion". This needed to be done for all 3 types of offers (BOGO, discount and informational) and each had its particularities that needed to be addressed. This part took around 80% of the amount of work in data preparation. After this was achieved, the 3 files were merged into one dataframe which is indexed by the customer_id - that is, each line in the final dataframe corresponds to a user (14825 observations or users in total). That way we have the amount offers completed by each type (as well as total) for each costumer, which in turn has its own demographic characteristics.
On the final dataframe feature engineering was done to aid the analysis of the demographic data of the customers by transforming the age and income variables (both of which spanned a wide range of values) into cohorts.
The age cohort was based on research [1] done on the fields of psychology and marketing based on the idea of generational cohorts, such as the 'baby boomers', generation X, Y and Z, and others. Based on the resources found, the following age stratification was used:

* 18–28 - Gen Z
* 29–39 - Gen Y
* 40–58 - Gen X
* 59–75 - Baby boomers
* 76+ - Post-War Cohort

Also income cohorts were generated in order to understand the different social classes that were present based on Equifax's definition:
* < 50k - Low income
* 50–75k - Moderate Income lower end
* 75–100k - Moderate Income upper end
* >100k - High Income

## Conclusions <a name="conclusions"></a>

The EDA along with the clustering analysis were able to provide a comprehensive understanding of Starbucks' customer behavior based on the data of the marketing campaign made available for this capstone project.
It should be noted first that the results obtained and observed are strongly dependent on the sample characteristics of the population of this dataset. As noted earlier, on the gender aspect there is a higher prevalence of males over females (about 30% more males); on the age distribution aspect, there is a much higher presence of individuals with age between 40 and 58. And on the income aspect, the majority of people have income in the range of 50k to 75k USD. The exercise is clear in mentioning that this is simulated data for the sake of testing the algorithms and data science skills, but it felt important to make this remark for the readers' information. As a data scientist, it is important to understand the data that one is working with.
Speaking about the results itself, it became clear that BOGO and Discount offers are two main drivers of when we speak about the customers with elevated rate of offers completed in general. Based on the EDA and clustering analysis, these customers that complete lots of offers can be divided into two main groups:
1) Males who belong in the generation X age cohort (40–58 years), with moderate income ranging from 50k to 75k USD and who prefer BOGO offers the most.
2) Females aged 40+ who prefer mainly discount offers.
Starbucks should keep sending promotional offers to this individuals, but focus on different strategies taking into account the demographic aspect.
The clustering analysis showed interesting trends and allowed for 2 other conclusions (one for each cluster)
First is that the younger portion of the sample - generations Y and Z (18–39 years of age) - were the age cohorts that completed offers the least. This can be explained partially by the fact this population is underrepresented on the moderate to high income strata.
Second, regarding accidental completion of offers, the demographics of the individuals who complete offers by accident the most is composed of elderly women of high income. So Starbucks should probably not send discounts to these individuals as they tend to purchase anyway.
Also, it is important to notice that the 3 offers with elevated accident completion have in common the fact that they did not use social media for marketing. Starbucks could perform an A/B test to understand the impact of social media marketing.

## Licensing and Acknowledgements<a name="licensing"></a>

Data provided by Starbucks

