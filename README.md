# Climate-Twitter-Analysis-

# 🌍 Climate Change Sentiment Analysis (2006-2019)

## 📌 Project Overview

This project analyses over **15.79 million climate-related tweets** to understand how public sentiment and stance toward climate change have evolved over a 13-year period. It also identifies the key topics and regions driving **divisive and aggressive discourse**.

The analysis was conducted using **SQL for data processing** and **Power BI for visualization**, following a full end-to-end data analysis workflow.

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
* **GitHub (Documentation & Version Control)**

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

Data cleaning was performed using SQL to ensure accuracy and consistency:

* Removed duplicate records using CTEs
* Handled missing values (e.g., gender, topic, coordinates)
* Standardised text formatting using `INITCAP`
* Converted data types where necessary
* Created new columns such as **year (from timestamp)**

---

## 🔄 Data Transformation

To make the dataset suitable for analysis:

* Extracted **year** from timestamp for time-based analysis
* Created calculated fields such as:

  * Average sentiment
  * Aggression rate
* Structured data into analysis-ready tables and views

---

## 📈 Data Analysis (Exploratory)

Key trends identified:

* Total tweets analysed: **15.79 million**
* Peak activity occurred in **2018 (~6.25M tweets)**
* Sentiment fluctuates over time (positive → negative → unstable trends)

Topic insights:

* Some topics show **positive sentiment (~0.24)**
* Others show **negative sentiment (~-0.05)**
* Certain topics generate stronger emotional reactions

---

## 🔍 Diagnostic Analytics

Further analysis was conducted to understand *why* trends occur:

* **Divisiveness:**

  * Weather-related topics show highest variation (~0.44)

* **Aggression:**

  * Average aggression rate is **0.09** (moderate)

* **Engagement:**

  * Global stance has the highest engagement (~4.1M tweets)

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

### 🔗 Dashboard Link

👉 **(https://app.powerbi.com/view?r=eyJrIjoiOTk5NTU2YTAtN2I5NC00ODY2LWIxYmYtZjJmMTllNmVlZDE0IiwidCI6IjdhY2M3YWZiLWQ0ODMtNGMzOC1iYmU2LTRkYzQ5NmI1N2VhMiJ9)**

---

## 💡 Key Insights

* Public sentiment changes significantly over time
* Engagement peaked around **2018**
* Topic type strongly influences sentiment
* Some topics are highly divisive
* Aggressive discourse exists but is relatively moderate

---

## 🧠 Conclusion

The analysis shows that climate change discussions on social media are shaped by time, topic, and user engagement. Public opinion is dynamic and influenced by global events, with certain topics generating stronger disagreement and emotional intensity.

---

## 📌 Recommendations

* Focus communication on highly divisive topics
* Monitor aggressive discourse for misinformation risks
* Increase awareness in low-engagement areas
* Further investigate drivers of sentiment changes

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
 ┃ ┗ dashboard.pbix
 ┣ 📂 docs
 ┃ ┗ [climate twitter dataset report.pdf](https://github.com/user-attachments/files/27451830/climate.twitter.dataset.report.pdf)



---

## 👩‍💻 Author

**Adesewa Ajibade**

---


