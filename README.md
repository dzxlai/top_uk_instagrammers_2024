
![Screenshot at Sep 01 12-11-18](https://github.com/user-attachments/assets/ab181bca-52c7-4d1a-a5ee-8210a19885a0)

<h1> top_uk_instagrammers_2024: Excel -> SQL -> Python Project </h1>

<h2> Description </h2>
Exploring and identifying the top performing UK instagram accounts to form marketing collaborations with.

</br>
</br>

<b> Project Architecture </b>

- <b> Excel </b>
  - Using Excel, I will explore the data. Scanning through the Excel dataset file, checking the data, fields (column features), records, properties of the data, errors, inconsistencies and bad characters. This will give me a general idea of how we want to clean the data.

- <b> SQL </b>
  - I will then pass the dataset through to SQL for the data cleansing process. By setting up a database and table in SQL, I can then pass the dataset as a .csv file and import it into the table ready for data cleansing. Here I am defining cleaning steps and transforming the data to the required structure.
     - Within SQL, I will also test the data by performing a series of data quality checks to ensure 'high-quality' data (i.e. data that is complete and accurate)

- <b> Python </b>
  - In the next phase of this project, I will leverage Python and its powerful libraries, such as Matplotlib and Seaborn, to create compelling and informative data visualizations. These plots and charts will present key statistics in an easy-to-read manner, allowing for quick insights and clear understanding of important trends.
  - After generating individual visualizations, I will combine them into a comprehensive dashboard, which will bring together all these insights in a cohesive and interactive format. This dashboard will serve as a platform for analyzing and exploring the data effectively.


<h2> Table of Contents </h2>


<h2> Objectives </h2>

- Key Point / Main Objective
Stakeholders and head of departments have come to me and want to know who are the top Instagrammers in 2024. They want us to help them use data-driven support in order to decide on which Instagrammers would be the best to collaborate and run marketing campaigns with.

- Solution?
  - To create a comprehensive and compelling dashboard that will inclue key information and statistics, allowing the marketing team to conduct informed decisions about taking further steps forward, and therefore maximise how effective each campaign is.


<h2> Data Source </h2>

 Where is this data coming from?
   - For this project we used a .csv dataset sourced from [Kaggle](https://www.kaggle.com/datasets/bhavyadhingra00020/top-100-social-media-influencers-2024-countrywise?resource=download)
   - Here we were able to extract information about the top 100 social media influencers 2024, including the top users for Instagram.
   - Some features included:
      - Rank
      - Name
      - Follower Count
      - Engagement Rate
      - Potential Reach
    
However, after loooking at the dataset, I wanted extra data and features. Some social media platforms have an API that holds meta-information about their users, granting extra information that would be very useful for analysis. Unfortunately, Instagram is not one that has their own. 
  - In order to go around this, I used a 3rd-party Python library, [instaloader](https://instaloader.github.io/), a tool, that allows me to download public profile statistics from instagram.
  - Extra features such as:
      - Following Count
      - Post Count


<h2> Steps </h2>

      1. Design and implementation
      
      2. Development and prepraring
       - Get the data
       - Explore the data in MS Excel
       - Clean the data in SQL
       
      3. Testing
       - Test the data in SQL, a series of quality checks to see how robust the data is
       
      4. Analysis and Interpretations
       - Visualise the data using powerful Python libraries
       - Conclude findings using insights gained


<h2> Design </h2>

<h3> Dashboard Plan </h3>

What should the dashboard contain based on requirements and how should it look like?
- In order to solve this, we need to break down the problem and figure out potential questions we'd like our dashboard to answer, such as:
  
      1. Who are the top 'x' Instagram accounts with the most followers?
      2. Which 'x' Instagram accounts have uploaded the most posts?
      3. Which accounts have the highest following (i.e. engaging back to public accounts)?
      4. Which accounts have the most potential reach per post?
      5. Which channels have the highest average followers per post (i.e. engagement rate)?
      6. Which channels have the posts per followers gained? 

<h3> Dashboard mockup blueprint </h3>

![dashboard blueprint](https://github.com/user-attachments/assets/cc5cdea2-6707-41aa-90ce-3290f16df617)


<h2> Tools </h2>

| Tool | Purpose |
| --- | --- |
| Excel | Exploring the data |
| SQL (PostgreSQL) | Cleaning, transforming, testing, and analysing the data |
| Python | Visualising the data by creating compelling and informative plots, using powerful Python libraries |
| GitHub | Hosting the documentation of this project |



<h2> Data Exploration Notes </h2>

In this step, I scanned through the raw data looking at the values, columns/features and rows to make sure I understood the data. 
These are the initial observations, i.e. what grabs my attention at first glance? Taking note of things such as errors, inconsistencies, empty or duplicated values, or bad/'corrupted' characters.

1. There are a few columns that contain the useful data needed for analysis.
2. The first column, 'NAME' contains both the names of the account, as well their account names, separated by an '@' symbol.
3. A lot of messy symbols in certain columns that require cleaning.
4. 'FOLLOWERS' column in the format '87M', need to change this to numerical format
5. There are more columns than required for this data exploration, so it would be appropriate to remove column features we don't need.


<h2> Data Cleaning </h2>

To begin the data cleansing process, I first created a database in SQL, as well as a new table which I can use to input my dataset into, making sure I create each column feature with the appropriate corresponding data type.

The aim is to refine the dataset to ensure it is concise and ready for analysis. Poor standardisation, data errors, etc. can cause inaccuracies and bias' towards the results of our analysis, therefore it is a crucial step.

We want:
- All data types should be appropriate for the contents of columns.
- Extracting names from 'NAME' column.
- Removing duplicated and null values.
- Keeping only the columns we need for analysis.
- If needed, rename columns using aliases.


<h3> Outling dataframe shape of cleaned dataset: </h3>

  | Property | Description |
| --- | --- |
| Number of Rows | 100 |
| Number of Columns | 6 |


<h3> Outling column data types cleaned dataset: </h3>

| Column Name | Data Type |
| --- | --- |
| full_name | VARCHAR |
| followers | INTEGER |
| following | INTEGER |
| posts | INTEGER |
| engagement_rate_percent | FLOAT |
| potential_reach_million | FLOAT |


<h3> Transforming the data </h3>

```sql
/*
# 1. Select the required columns
# 2. Extract names from 'NAME' column
# 3. Removing 'messy/bad' symbols from 'NAME' column, using regexp_replace, used to replace substrings within a string that match a regular expression with specified replacement substring.
# 4. Using initcap to standardise formatting of names.
# 5. CAST on certain columns to appropriately convert their data types to FLOATS
*/

SELECT 
    initcap(regexp_replace(CAST(SUBSTRING(name, 1, POSITION('@' IN name) - 1) AS VARCHAR(100)), '[^A-Za-z\s]', '', 'g')) as full_name,
    total_followers AS followers,
    total_following AS following,
    total_posts AS posts,
    CAST(SUBSTRING(engagement_rate, 1, 4) AS float8) AS engagement_rate_percent,
    CAST(TRIM('M' FROM potential_reach) AS float8) AS potential_reach_per_million
FROM top_uk_instagrammers_2024;
```













