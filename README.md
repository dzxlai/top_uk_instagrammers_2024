
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
 3. Testing
 4. Analysis and Interpretations

 
<h2> Design </h2>

<h3> Dashboard plan </h3>

What should the dashboard contain based on requirements and how should it look like?
- In order to solve this, we need to break down the problem and figure out potential questions we'd like our dashboard to answer, such as:
- 
      1. Who are the top 'x' Instagram accounts with the most followers?
      2. Which 'x' Instagram accounts have uploaded the most posts?
      3. Which accounts have the highest following (i.e. engaging back to public accounts)?
      4. Which accounts have the most potential reach per post?
      5. Which channels have the highest average followers per post (i.e. engagement rate)?
      6. Which channels have the posts per followers gained? 

<h3> Dashboard mockup blueprint </h3>

![dashboard blueprint](https://github.com/user-attachments/assets/cc5cdea2-6707-41aa-90ce-3290f16df617)


<h3> Tools </h3>

| Tool | Purpose |
| --- | --- |
| Excel | Exploring the data |
| SQL (PostgreSQL) | Cleaning, transforming, testing, and analysing the data |
| Power BI | Visualising the data by creating compelling and informative plots |
| GitHub | Hosting the documentation of this project |










 
