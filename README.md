![Screenshot at Sep 01 12-11-18](https://github.com/user-attachments/assets/ab181bca-52c7-4d1a-a5ee-8210a19885a0)

<h1> Top Performing UK Instagram Accounts 2024: Excel -> SQL -> Python Project </h1>

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


<h3> Creating SQL view for data testing </h3>

```sql
/*
# 1. Creating a SQL view to store the transformed refined dataset.
# 2. Selecting only the required columns from the top_uk_instagrammers_2024 dataset SQL table.
*/

CREATE VIEW view_uk_instagrammers_2024 AS

SELECT 
    initcap(regexp_replace(CAST(SUBSTRING(name, 1, POSITION('@' IN name) - 1) AS VARCHAR(100)), '[^A-Za-z\s]', '', 'g')) as full_name,
    total_followers AS followers,
    total_following AS following,
    total_posts AS posts,
    CAST(SUBSTRING(engagement_rate, 1, 4) AS float8) AS engagement_rate_percent,
    CAST(TRIM('M' FROM potential_reach) AS float8) AS potential_reach_per_million
FROM top_uk_instagrammers_2024;
```


<h2> Testing the data </h2>

Here, are a series of data quality checks.

What is 'high-quality' data?
- Data that is complete and accurate.
  - Ideally we don't want:
    - empty records
    - duplicate records
    - inaccurate figures
    - bad characters
   

<h3> Data Quality Tests </h3>

1. data needs to be 100 records of instagram accounts (row count test)
2. completes columns (6 fields) - (column count test)
3. account names must be string format, total_followers + total_following + total_posts must be whole number format (data type test)
4. each record must be unique (duplicate count test)
    
<b> Goal: </b> make sure actual data is equivalent to expeceted data
   

<h3> Row Count Test </h3>

- Count the total number of rows (records) are in the our SQL dataset view

```sql

SELECT
    COUNT(*) AS no_of_rows
FROM
    view_uk_instagrammers_2024;

```
![row_count_test](https://github.com/user-attachments/assets/16531641-5fd3-495b-bf71-53e39d13b81a)


<h3> Column Count Test </h3>

- Count the total number of columns (features/fields) in our SQL view
- Using information_schema, a meta database that holds sets of views (information) about database objects

```sql

SELECT * 
FROM information_schema.columns
WHERE table_name = 'view_uk_instagrammers_2024';

SELECT COUNT(*) AS no_of_columns 
FROM information_schema.columns
WHERE table_name = 'view_uk_instagrammers_2024';

```
![column_count_test](https://github.com/user-attachments/assets/193fef4f-1ec7-472e-accc-7f63cc9099dd)


<h3> Data Type Test </h3>

- Check the data type of each column, using the information schema database

```sql

SELECT ordinal_position, column_name, data_type 
FROM information_schema.columns
WHERE table_name = 'view_uk_instagrammers_2024'
ORDER BY ordinal_position;

```
![data_type_test](https://github.com/user-attachments/assets/08ab69d3-67e8-4e52-b90a-945003b1ef4e)


<h3> Duplicate Count Test </h3>

- Using HAVING function, to filter to records that are greater than 1, i.e. identifying duplicates

```sql

SELECT full_name, COUNT(*) AS duplicate_count
FROM view_uk_instagrammers_2024
GROUP BY full_name
HAVING COUNT(*) > 1

```
![duplicate_count_test](https://github.com/user-attachments/assets/837e2413-4be1-4e40-bf7f-d8cb80b0b828)

- No records returned, implying no duplicate records where located.


<h2> Account Engagement Ratios </h2>

<h3> Potential Reach Per Post </h3>

```Python

sum_of_potential_reach_per_m = df['potential_reach_per_million'].sum()
sum_of_posts = df['posts'].sum()

print("sum of potential reach (M) = " + str(sum_of_potential_reach_per_m) + ' M')
print("sum of posts = " + str(sum_of_posts))

print("\n")

avg_potential_reach_m_per_post = sum_of_potential_reach_per_m / sum_of_posts
print("average potential reach (M) per post = " + str(avg_potential_reach_m_per_post) + ' M')

avg_potential_reach_per_post = avg_potential_reach_m_per_post * 1000000
avg_potential_reach_per_post = avg_potential_reach_per_post.round()
print("average potential reach per post = " + str(avg_potential_reach_per_post) + ' people')

```

![potential_reach_per_post_results](https://github.com/user-attachments/assets/d6c41a85-4dbd-4082-a963-845254f5bdf3)

<h3> Follower Engagement Rate </h3>

- Engagement Rate = The level of interaction the influencer's content receives from users on social media platforms, expressed as a percentage.

```Python

# follower engagement rate
# average followers per post

sum_of_followers = df['followers'].sum()
sum_of_posts = df['posts'].sum()

print("sum of followers = " + str(sum_of_followers))
print("sum of posts = " + str(sum_of_posts))

print("\n")

avg_follower_engagement_rate = sum_of_followers / sum_of_posts
avg_follower_engagement_rate = avg_follower_engagement_rate.round()
print("average followers gained per post or 'Engagement Rate' = " + str(avg_follower_engagement_rate) + ' people')

```

![engagement_rate_results](https://github.com/user-attachments/assets/e6e00550-4bfc-4c75-bc8d-5f1a9961c843)

<h3> Posts per Followers </h3>

- On average, instagram post rate per followers gained

```Python

sum_of_posts = df['posts'].sum()
sum_of_followers = df['followers'].sum()

print("sum of posts = " + str(sum_of_posts))
print("sum of followers = " + str(sum_of_followers))

sum_of_followers_m = sum_of_followers / 1000000
print("sum of followers (M) = " + str(sum_of_followers_m) + ' M')

print("\n")

avg_posts_per_million_followers = sum_of_posts / sum_of_followers_m
avg_posts_per_million_followers = avg_posts_per_million_followers.round()
print("average no. of posts per million followers = " + str(avg_posts_per_million_followers) + ' posts')

```

![posts_per_followers_results](https://github.com/user-attachments/assets/f8764018-4773-4680-95b2-845f63f4187e)


<h2> Data Visualisation </h2>

<h3> Dashboard Results </h3>


![top_uk_instagrammers_2024_dashboard](https://github.com/user-attachments/assets/99c7305b-10ef-4b3b-97e1-073fdb68e046)



<h2> Analysis </h2>

<h3> Findings/Results </h3>

<h3> 1. Who are the top 10 Instagram accounts with the most followers? </h3>

| Rank | Name         | Followers (M) |
|------|----------------------|-----------------|
| 1    | David Beckham    | 88.35           |
| 2    | Emma Watson               | 74.32           |
| 3    | Tom Holland           | 65.11           |
| 4    | Millie Bobby Brown            | 63.46           |
| 5    | Adele           | 57.58           |
| 6    | Zayn Malik                  | 51.87           |
| 7    | Ed Sheeran                | 47.89           |
| 8    | Liverpool Football Club             | 45.63           |
| 9    | Jason Statham              | 42.39           |
| 10   | Cara Delevingne                | 41.33           |

<h3> 2. Which 5 accounts have uploaded the most posts? </h3>

| Rank | Name    | Posts Uploaded |
|------|-----------------|-----------------|
| 1    | Liverpool Football Club       | 28157          |
| 2    | Tottenham Hotspur | 21013           |
| 3    | Arsenal        | 19306           |
| 4    | Mercedes-AMG Petronas F Team        | 15585           |
| 5    | Vicky Pattinson        | 10785           |

<h3> 3. Which 5 accounts have the most potential reach per post </h3>

| Rank | Name | Potential Reach (M) |
|------|--------------|-----------------|
| 1    | David Beckham       | 26.1           |
| 2    | Emma Watson   | 22.6           |
| 3    | Tom Holland   | 19.9           |
| 4    | Millie Bobby Brown  | 19           |
| 5    | Adele   | 16.8           |

<h3> 4. Which 5 accounts have the highest engagement rate? </h3>

| Rank | Name       | Follower Engagement Rate (%)        |
|------|-----------------   |---------------------------- |
| 1    | Kit Connor          | 28.6                     |
| 2    | One Direction        | 17.9                     |
| 3    | Harry Styles HQ   | 14.5                     |
| 4    | The UK Rider   | 13.9                     |
| 5    | Mason Mount   | 13.7                     |

<h3> 5. Which 5 accounts are most active in posting per followers gained? </h3>

| Rank | Name       | Posts per Followers (M) gained        |
|------|-----------------   |---------------------------- |
| 1    | Vicky Pattinson          | 1953                     |
| 2    | Tottenham Hotspur        | 1229                     |
| 3    | Mercedes-AMG Petronas F Team   | 1150                     |
| 4    | Sean Garnier   | 944                    |
| 5    | Adnan Alkateb   | 838                     |


<h2> Discovery </h2>

We discovered that:

1. David Beckham, Emma Watson and Tom Holland are the Instagram accounts with the most followers in the UK.
2. Liverpool Football Club, Tottenham Hotspur and Arsenal are the accounts with the most posts uploaded.
3. Disregarding company/organisation accounts, individual accounts with the most followers; Cara Delevinge, Ed Sheeran and David Beckham are the accounts with the most posts uploaded.
4. Zayn Malik, Tom Holland and Adele have the highest follower engagement rates for the top followed accounts regarding most followers vs potential reach.

<h3> Recommendations </h3>

What can we recommend based on the insights gathered?

1. David Beckham is the best Instagram account to collaborate with if we want to maximise and push visibility. This is because he has the most followers on Instagram in the UK, and consequently has the highest potential reach.
2. Liverpool Football Club, Tottenham Hotspur and Arsenal have the most posts, which means they have the most activity on the platform. However, as they are huge company sports clubs, it may be worth considering whether there are better options with other Instagram accounts, as it would require a lot more money and effort, with return on investments being significantly lower compared to others.
3. Zayn Malik, Tom Holland and Adele can also be highly considered to form collaborations with. These 3 accounts have the highest followers in correlation to  potential reach. In addition to this, they are the top 3 accounts with the largest engagement rates, meaning they have the highest level of interactions with followers and therefore these 3 accounts would potentially have the highest return on investment going forward with the campaign.



