# Data Modeling with Casandra Apache Udacity project

## Goal of this project

The goal of this project is to create an ETL process to extract, transform and load data from existing CSV events files to Apache Casandra tables. This will simplify the whole process of analysing data for data analysts by simpliefied queries from created Apache Casandra tables. My personal goal in this project is to gain experience in building such ETL pipelines.

# Queries to perform 

In regard to build Apache Casandra tables, first it needs to be taken into consideration what queries will be required. This kind of approach of building tables is persisted in NOSQL DB, bacause we need to know which Partition Keys must be selected, which serve a minor role to distribute data among nodes.

1. Query 1: **Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4** 

> - CQL Statement: **SELECT * FROM songs_listened_history WHERE session_id = 338 AND item_in_session = 4**
> - Output: **Faithless Music Matters (Mark Knight Dub) 495.30731201171875**

2. Query 2: **Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182**

> - CQL Statement: **SELECT artist_name, song_title,first_name, last_name FROM users_listened_history WHERE user_id = 10 AND session_id = 182**
> - Output: **Down To The Bone Keep On Keepin' On Sylvie Cruz
              Three Drives Greece 2000 Sylvie Cruz
              Sebastien Tellier Kilometer Sylvie Cruz
              Lonnie Gordon Catch You Baby (Steve Pitron & Max Sanna Radio Edit) Sylvie Cruz**
              
3. Query 3: **Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'**

> - CQL Statement: **SELECT first_name, last_name FROM songs_listened_by_users WHERE song_title = 'All Hands Against His Own'**
> - Output: **Jacqueline Lynch
              Tegan Levine
              Sara Johnson**





# Tables structure and datatypes

There are 3 in total tabbles, which were composed regarding to required queries:

1. **songs_listened_by_users**
> - Columns created: **artist_name TEXT, song_title TEXT, length FLOAT, session_id INT, item_in_session INT, PRIMARY KEY (session_id,item_in_session )**

2. **users_listened_history**
> - Columns created: **user_id INT, session_id INT, item_in_session INT, artist_name TEXT, song_title TEXT, first_name TEXT, last_name TEXT,   PRIMARY KEY ((user_id, session_id), item_in_session ))**

3. **songs_listened_history**
> - Columns created: **song_title TEXT, user_id INT, first_name TEXT, last_name TEXT,   PRIMARY KEY (song_title, user_id )**