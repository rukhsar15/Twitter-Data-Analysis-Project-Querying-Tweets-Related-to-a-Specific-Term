
---

# **Twitter Data Analysis Project: Querying Tweets Related to a Specific Term**

## **Project Overview**

This project provides a detailed analysis of tweets using data from a Twitter dataset. It demonstrates my ability to ingest large datasets, query them using both Python and SQL, and provide insights in response to specific queries. The dataset focuses on tweets mentioning the term **“Britney”**, and the project allows for flexible querying of various metrics. 

This project was developed as part of a data analyst assessment for SIlverSpace INC and highlights my skills in:

- Data ingestion and handling large datasets.
- Writing complex queries in both **SQL** and **Python**.
- Implementing efficient, scalable querying systems.
- Documenting code and producing results that are easy to reproduce.

The project can be extended to support other types of data analysis tasks, including integration with a web API and Docker-based deployments.

---

## **Dataset Details**

The dataset used contains approximately **88,000** tweets with a variety of metadata fields, including:

- **Tweet content** (`text`), **language** (`lang`), and **author handle** (`author_handle`).
- **Engagement metrics** like **retweets**, **likes**, **replies**, and **quote counts**.
- **Timestamp** (`created_at`) and **location data** (`place_id`).
- **Sensitive content flags** and metadata about conversations.

This rich data allows us to generate insights and answer specific questions about user activity, tweet content, and engagement.

---

## **Key Features and Queries**

The project answers the following important questions about tweets containing a given search term (e.g., "Britney"):

1. **Number of tweets posted containing the term, broken down by day**:
   - This function counts the number of tweets posted each day that contain the search term.
   
2. **Number of unique users who posted tweets containing the term**:
   - This query returns how many distinct users tweeted about the search term.

3. **Average number of likes received by tweets containing the term**:
   - This gives insights into the engagement level (in terms of likes) on tweets about the search term.

4. **Location of the tweets (by place ID)**:
   - Identifies the geographic locations (place IDs) from where the tweets were posted.

5. **Times of day when tweets containing the term were posted**:
   - Shows the most active hours of the day based on the tweets containing the search term.

6. **Most active user posting tweets containing the term**:
   - Identifies the user who posted the most tweets containing the search term.

---

## **Technologies Used**

This project utilizes a combination of Python libraries and an SQLite database for efficient querying:

- **pandas**: For data manipulation and analysis.
- **SQLite**: To store and query the dataset efficiently.
- **Jupyter Notebook**: For developing, testing, and running code in an interactive environment.
- **Python's sqlite3**: To connect pandas with the SQLite database.
- **SQL**: For executing structured queries directly on the SQLite database.

---

## **Setup Instructions**

### **1. Environment Setup**

To run this project, you'll need the following installed:

- **Python 3.x**
- **pandas** library for data manipulation.
- **sqlite3** for SQL database integration.

You can install the required packages using pip:

```bash
pip install pandas sqlite3
```

### **2. Data Preparation**

1. Download the dataset (`correct_twitter_201904.tsv`) and place it in the project directory.
2. Load the dataset into a **pandas DataFrame** and ingest it into an **SQLite database** for querying.

### **3. Running the Project**

1. Open the Jupyter Notebook and ensure that it points to the correct dataset path.
2. Execute each code cell step-by-step, starting with the data ingestion and then proceeding to the queries.

---

## **Project Structure**

The project is divided into several key components, each playing a crucial role in data processing, querying, and analysis.

### **1. Data Ingestion**

The dataset is loaded into a **pandas DataFrame** and then ingested into an **SQLite database** to allow for efficient querying. Using SQLite allows us to scale the querying process for larger datasets.

**Code Example**:
```python
import pandas as pd
import sqlite3

# Load the dataset
df = pd.read_csv('correct_twitter_201904.tsv', sep='\t', encoding='utf-8')

# Ingest data into SQLite
conn = sqlite3.connect('tweets.db')
df.to_sql('tweets', conn, if_exists='replace', index=False)
```

### **2. Querying the Data**

Several query functions were built to retrieve insights about tweets containing a specific term. Each function uses **SQL** queries executed on the SQLite database and returns results in a **pandas DataFrame** for easy manipulation and visualization.

**Example Query Function (Tweets per Day)**:
```python
def tweets_per_day(term, conn):
    query = f"""
    SELECT substr(created_at, 1, 10) as date, COUNT(*) AS tweet_count
    FROM tweets
    WHERE text LIKE '%{term}%'
    GROUP BY date
    ORDER BY date;
    """
    return pd.read_sql(query, conn)
```

Other functions include:
- **Unique Users Posting the Term**
- **Average Likes on Tweets Containing the Term**
- **Tweet Locations (Place IDs)**
- **Time of Day for Tweet Posting**
- **Top User Tweeting the Term**

### **3. Running the Queries**

To run a query, call the function with a specific search term (e.g., "Britney") and the SQLite connection:

```python
term = 'Britney'

# Run query to get tweets per day
tweets_day = tweets_per_day(term, conn)

# Display results
print(tweets_day)
```

---

## **Results and Insights**

Here are some insights that were gathered from the sample analysis on tweets containing the term "Britney":

- **Number of Tweets Per Day**: A consistent increase in tweets during May 2019, with peaks on specific dates.
- **Unique Users**: Over 46,000 unique users tweeted about Britney.
- **Average Likes**: On average, tweets containing "Britney" received 6.73 likes.
- **Tweet Locations**: Tweets were posted from various geographical locations (place IDs).
- **Time of Day**: The busiest tweeting hours were between 14:00 and 17:00, with a peak at 16:00.
- **Most Active User**: The user `ricaricarica33` was the most active in posting tweets containing "Britney."

These results demonstrate how you can query, manipulate, and extract insights from the dataset.

---

## **Possible Extensions**

To make this project more robust and scalable, the following enhancements could be implemented:

1. **API Development**: Using **Flask** to turn the query functions into a web API that can be queried remotely.
2. **Dockerization**: Containerizing the entire project for easier deployment and environment consistency.
3. **Optimizations**: Exploring more complex query optimizations to improve performance for larger datasets.

---

## **Conclusion**

This project demonstrates my ability to work with large datasets, develop efficient querying systems using Python and SQL, and present insights in a structured way. The modular approach allows for easy extensions, such as API development or further optimization, and the thorough documentation ensures that others can easily replicate and understand the analysis.

---

## **Contact**

If you have any questions or require further clarification, please don't hesitate to contact me via email or GitHub.

---


