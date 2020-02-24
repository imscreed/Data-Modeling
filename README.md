## Data Modelling for Sparkify Music Streaming app

The main goal is to model and analyze the data containing all the songs and user activity of Sparkify's new streaming music application.

**Problem:**
There is no easy way to query the data since the data is completely unstructured and lives as JSON logs in the app.

**Prerequisites:**
Python 3.x, PostgreSQL, Jupyter Notebook.

**Project Description:**
This project focuses on data modeling with Postgres and building an ETL pipeline using Python. 

**Objectives:**
 -  Define fact and dimension tables for star schema
 - ETL pipeline to transfer data from JSON files in two local directories into these tables

## Datasets:
**Song Dataset**
Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.
```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json

```

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

```

# Log Dataset

Contains log files in JSON format based on the songs in the dataset above. 

The log files are partitioned by year and month. For example, see below:

```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json

```

## Schema for Song Play Analysis

STAR schema with the following tables

#### Fact Table

1.  **songplays**  - records in log data associated with song plays i.e. records with page  `NextSong`
    -   _songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent_

#### Dimension Tables

2.  **users**  - users in the app
    -   _user_id, first_name, last_name, gender, level_
3.  **songs**  - songs in music database
    -   _song_id, title, artist_id, year, duration_
4.  **artists**  - artists in music database
    -   _artist_id, name, location, latitude, longitude_
5.  **time**  - timestamps of records in  **songplays**  broken down into specific units
    -   _start_time, hour, day, week, month, year, weekday_

## Project Files & Instructions
 -  `test.ipynb`  displays the first few rows of each table to let you test your database.
 -  `create_tables.py`  drops and creates your tables. Run this file to reset your tables before each time you run your ETL scripts.
 -  `etl.ipynb`  reads and processes a single file from  `song_data`  and  `log_data`  and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.
 -  `etl.py`  reads and processes files from  `song_data`  and  `log_data`  and loads them into your tables. 
 -  `sql_queries.py`  contains all your sql queries, and is imported into the last three files above.

**Panda Library**
For manipulating the data and processing it we use the Panda library in Python. The imported data from JSON file is in the DataFrame format and we model the data using these dataframes. 

    df = pd.read_json(filepath, lines=True)

**Songplays Table:**
This table is the one that contains all the useful piece of information. i.e. The facts and metrics that are in structured form.

