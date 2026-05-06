# Climate-Twitter-Analysis-

# 🌍 Climate Change Sentiment Analysis (2006-2019)

## 📌 Project Overview
This project analyses over 15.79 million climate-related tweets collected between 2006 and 2019 to examine how public sentiment and stance toward climate change have changed over time. The study also explores the major topics and regions contributing to divisive and aggressive online discourse surrounding climate-related discussions.

The analysis was carried out using SQL for data cleaning, transformation, and querying, while Power BI was used to develop interactive visualizations and dashboards. The project follows a complete end-to-end data analytics process, from raw data preparation to insight generation and reporting.

---

## 🎯 Objectives

* Analyse trends in public sentiment over time
* Examine how climate change stance has evolved
* Identify topics driving divisive and aggressive discussions
* Clean and transform raw data into an analysis-ready format
* Develop an interactive dashboard for decision-making insights

---

## 🛠️ Tools & Technologies

* **SQL (PostgreSQL )**
* **Power BI**
* 

---

## 📊 Dataset Description

The dataset contains over **15 million tweets (2008–2022)** with the following features:

* Timestamp (`created_at`)
* Sentiment score (numeric, including negatives)
* Climate stance (believer, neutral, etc.)
* Topic classification
* Gender
* Geolocation (latitude & longitude)
* Aggressiveness label

---

## 🧹 Data Preparation & Cleaning

Data cleaning and preparation were performed using SQL to improve data quality, accuracy, and consistency before analysis. Several preprocessing techniques were applied to ensure the dataset was suitable for reporting and visualization.

The cleaning process included:
	•	Removing duplicate records using Common Table Expressions (CTEs)
	•	Handling missing values in fields such as gender, topic, latitude, and longitude
	•	Standardising text formatting using the INITCAP function to maintain consistency
	•	Converting columns into appropriate data types where necessary
	•	Creating derived columns, including a year column extracted from the timestamp field for time-based analysis

These steps helped prepare the dataset for efficient querying, accurate analysis, and dashboard development in Power BI.
---

## 🔄 Data Transformation 
To prepare the dataset for effective analysis, several transformation processes were carried out using   
• A new year column was extracted from the timestamp field to support time-based trend analysis and reporting.

Additional calculated fields were also created to improve analytical depth, including metrics such as:
	•	Average sentiment scores
	•	Aggression rate indicators
The data was structured into analysis-ready tables and views to support efficient querying, dashboard integration, and visualization in Power BI. These transformations improved the usability of the dataset and enabled clearer insight generation.

## 📈 Data Analysis (Exploratory)

Exploratory analysis revealed several important trends within the dataset. 
A total of 15.79 million tweets were analysed, with the highest level of activity recorded in 2018, which accounted for approximately 6.25 million tweets. 
The analysis also showed that public sentiment toward climate change fluctuated over time, moving between positive and negative patterns rather than remaining stable.

Topic-based analysis further highlighted differences in public opinion across climate-related discussions. 
Some topics recorded relatively positive sentiment scores of approximately 0.24, while others showed more negative sentiment values close to -0.05. 
In addition, certain topics generated stronger emotional reactions and higher levels of engagement, indicating areas of increased public sensitivity and debate surrounding climate change issues.
---

## 🔍 Diagnostic Analytics

## 🔍 Diagnostic Analytics

### Diagnostic Insights (Why Trends Occur)

This section explains why some patterns appear in the data.

### Divisiveness
- Weather-related topics show the highest variation (~0.44)  
- This means people have very different opinions about extreme weather events  
- Some users are strongly affected by these events, while others are not, which creates disagreement  

### Aggression
- Average aggression rate is **0.09** (moderate)  
- This shows that most tweets are calm or neutral  
- Only a small number of tweets contain angry or harsh language  

### Engagement
- Global climate change discussions have the highest engagement (~4.1M tweets)  
- This means general climate topics attract more attention than specific issues  
- People are more likely to talk about overall climate change than niche topics  
---
## 📊 Power BI Dashboard

An interactive dashboard was developed to present insights clearly.

### 📄 Dashboard Structure

* **Page 1:** Sentiment & Stance Over Time

<img width="1457" height="853" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/91f7cede-21b3-45fa-839b-d80676c78aea" />

* **Page 2:** Topic & Aggression Analysis
   <img width="1416" height="841" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/df8abb18-2fb1-4f93-b127-05ba73d398ea" />
### 🎛️ Features

* Interactive slicers (Year, Topic, Gender, Stance)
* KPI cards (Total Tweets, Avg Sentiment)
* Line charts, bar charts, and gauge visuals
---
### 🔗 Dashboard Link

👉 **[Climate Twitter Dataset](https://app.powerbi.com/view?r=eyJrIjoiOTk5NTU2YTAtN2I5NC00ODY2LWIxYmYtZjJmMTllNmVlZDE0IiwidCI6IjdhY2M3YWZiLWQ0ODMtNGMzOC1iYmU2LTRkYzQ5NmI1N2VhMiJ9)**

---

## 💡 Key Insights

- Public sentiment toward climate change is not stable and shows significant variation over time, reflecting changing global conversations, events, and awareness levels.

- Engagement levels peaked around **2018**, indicating a period of heightened global attention and increased discussion activity around climate-related issues.

- The type of topic being discussed has a strong influence on sentiment polarity, meaning certain subjects consistently generate more positive or negative reactions than others.

- Some climate-related topics are highly divisive, with users expressing strongly opposing views, especially on issues linked to environmental impact and policy debates.

- Although aggressive discourse is present within the dataset, it remains relatively moderate overall (average aggression rate ≈ 0.09), suggesting that most discussions are still neutral or opinion-based rather than hostile.

- Overall, the findings highlight that climate change conversations on social media are shaped by both emotional response and topical sensitivity, rather than remaining consistent or uniform over time.

---
## 📌 Recommendations

- Focus communication on topics that people strongly disagree about, such as extreme weather and environmental policies, because they create the most debate.

- Monitor aggressive posts to help reduce misinformation and harmful messages about climate change.

- Increase awareness in areas and topics where there is low engagement so more people can join the conversation.

- Study what causes changes in public opinion over time, such as major events or climate news, to better understand why sentiment goes up or down.

- Create targeted messages for different topics and audiences to improve understanding and reduce disagreement in online discussions.

---
## 🧠 Conclusion

This analysis shows that climate change discussions on social media change over time and are influenced by different topics and levels of user engagement.

Public opinion is not fixed. It changes based on global events and ongoing discussions.

Some topics lead to stronger disagreement and more emotional responses, while others remain more neutral and balanced.

---

## 📁 Project Structure

```
📦 climate-sentiment-analysis
 ┣ 📂 SQL
 ┃ ┗ [
------------creating socialdata table-----------
CREATE TABLE social_data (
    created_at TIMESTAMP,
	 id BIGINT,
    lng DECIMAL(9,6),
    lat DECIMAL(9,6),
    topic VARCHAR(100),
    sentiment DECIMAL(10,8),
    stance VARCHAR(20),
    gender VARCHAR(10),
    temperature_avg DECIMAL(5,2),
    aggressiveness VARCHAR(20)
);
--------importing the climate twitter dataset into the social_table -------

copy social_data
FROM 'C:\Users\HP\Downloads\The Climate Change Twitter Dataset.csv'
WITH (FORMAT csv, HEADER);



--------data cleaning ---------
------handling missing / null values in social_data table -------

UPDATE social_data
SET temperature_avg = 0
WHERE temperature_avg IS NULL;

UPDATE social_data
SET lng = 0
WHERE lng IS NULL;

UPDATE social_data
SET lat = 0
WHERE lat IS NULL;




----------checking for duplicates---------

SELECT id , COUNT(*)
FROM public.social_data
GROUP BY id
HAVING COUNT(*) > 1;


---------- standardizing formats--------

UPDATE social_data
SET gender = initcap (gender);

UPDATE social_data
SET aggressiveness = initcap(aggressiveness);

UPDATE social_data
SET stance = initcap(stance);

--------removing inconsistent sentiment ranges------
DELETE FROM social_data
WHERE sentiment < -1 OR sentiment > 1;

-------data wrangling -------
-------Creating Derived Columns
--------Sentiment Category
ALTER TABLE social_data
ADD COLUMN sentiment_label VARCHAR(10);
-------- update sentiment label column -------
UPDATE social_data
SET sentiment_label =
CASE
    WHEN sentiment > 0 THEN 'Positive'
    WHEN sentiment < 0 THEN 'Negative'
    ELSE 'Neutral'
END;


------ Extracting Time Components ----------

ALTER TABLE social_data ADD COLUMN year INT;

UPDATE social_data
SET year = EXTRACT(YEAR FROM created_at);


----------Aggression Flag------------
ALTER TABLE social_data ADD COLUMN aggression_flag INT;

UPDATE social_data
SET aggression_flag =
CASE
    WHEN aggressiveness = 'Aggressive' THEN 1
    ELSE 0
END;
-----------DESCRIPTIVE ANALYTICS-----
--------TOTAL TWEETS-----
SELECT COUNT(*) AS total_tweets
FROM social_data;

------Average sentiment----------
SELECT AVG(sentiment) AS avg_sentiment
FROM social_data;

--------Aggressiveness breakdown----

SELECT aggressiveness, COUNT(*) 
FROM social_data
GROUP BY aggressiveness;
----tweets per year----

SELECT  year,
       COUNT(*) AS total_tweets
FROM social_data
GROUP BY year
ORDER BY year;

------------Topic-Based Sentiment Analysis-------
SELECT 
    topic,
    COUNT(*) AS total_tweets,
    AVG(sentiment) AS avg_sentiment
FROM social_data
GROUP BY topic
ORDER BY avg_sentiment DESC;

---------Aggregation Analysis (Trends Over Time)------

SELECT 
    EXTRACT(YEAR FROM created_at) AS year,
    COUNT(*) AS total_tweets,
    AVG(sentiment) AS avg_sentiment,
    AVG(CASE WHEN aggressiveness = 'aggressive' THEN 1 ELSE 0 END) AS aggression_rate
FROM social_data
GROUP BY EXTRACT(YEAR FROM created_at)
ORDER BY year;

Uploading stage 4.1.sql…]()

 ┣ 📂 PowerBI
 ┃ ┗ [Climate Twitter Dataset](https://app.powerbi.com/view?r=eyJrIjoiOTk5NTU2YTAtN2I5NC00ODY2LWIxYmYtZjJmMTllNmVlZDE0IiwidCI6IjdhY2M3YWZiLWQ0ODMtNGMzOC1iYmU2LTRkYzQ5NmI1N2VhMiJ9)

 ┣ 📂 docs
 ┃ ┗ [climate twitter dataset report.pdf](https://github.com/user-attachments/files/27451830/climate.twitter.dataset.report.pdf)



---

## 👩‍💻 Author

**Adesewa Ajibade**

---


