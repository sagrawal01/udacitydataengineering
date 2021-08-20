# Project Description: Data Modeling with Postgres


In this project, we are creating a Postgres database for a startup called Startify, which has collected data on songs and user activity in their music streaming app. We are pulling data from JSON files of user activity and songs to consolidate them for the analytics team. We have implented the database schema and ETL pipeline detailed below.

## There are five tables that have been created in this database.

1. songplays - facts table that contains information about the played songs
2. songs - dimensions table that contains the list of songs
3. users - dimensions table that contians the list of users
4. artists - dimensions table that contains the artist information
5. time - dimensions table that contains the timestamp broken down to an hourly level

The data model is a star schema and the structures of the tables is as follows:

<p>
    <img src="data_model_postgres.png" width="600" height="400" />
</p>

## ETL Process:

1. create_tables.py script is run to drop and create the database sparkifydb as well as the five tables detailed above. 
2. The files in the data/song_data directory are read and the first records are inserted into the songs and artists table via the `song_table_insert` and `artist_table_insert` queries in sql_queries.py. The process_data() function is used to read all the files in each of the directory.
3. The files in the data/log_data directory are read into a pandas dataframe and filtered to records where the page column is 'NextSong.' The start_time column is broken down until the hourly level and the data is inserted into the time table with the `time_table_insert` query in sql_queries.py. Similarly, the users data from the log file is inserted into the users table via the `user_table_insert` query. For the songplays table, the song_id and artist_id are extracted from the songs and artists table given the song title, artist name and song duration (as these ids are not present in the log files) and inserted into the songplays table via the `songplay_table_insert` query.
4. The database connection is closed once the tables have been inserted.

## Project Repository Files: 

1. create_tables.py is used to create and connect to the Sparkify database, as well as create and drop tables detailed in sql_queries.py.
2. sql_queries.py contains statements to create the five main tables in the database, drop the tables and select songs and artists based on song title, artist name and song duration (used to insert records into the songplays table). 
3. etl.py is used to do the following: 
    1. Process the list of songs in the data/song_data directory and insert the data into the songs and artists tables (process_song_files function). 
    2. Process the log files of user activity in the data/log_files directory and insert the data into the time, users and songplays tables (process_log_files function).
    3. Both steps 1 and 2 call the process_data function which iterates through each file in a given directory and processes it.
4. etl.ipynb is utilized to test and write functions that are in the etl.py file.
5. test.ipynb is utilized to validate that the tables were created and data has been inserted into those tables.

## Project Structure:
Project: Data Modeling with Postgres/          
├── data/                                         <- contains JSON files for log and song data
│   ├──log_data/                                  <- contains JSON files for logs of user activity
│   │   ├──2018
│   │   │   ├──11
│   │   │   │   ├──2018-11-01-events.json         <- log files of user activity(one for each day)
│   │   │   │   ├──...
│   ├──song_data/                                 <- contains JSON files for song data
│   │   ├──A
│   │   │   ├──A
│   │   │   │   │──A
│   │   │   │   │   │──TRAAAAW128F429D538.json    <- JSON files for song metadata
│   │   │   │   │──B
│   │   │   │   │   │──...
│   │   │   │   │──C
│   │   │   │   │   │──...
│   │   │   ├──B
│   │   │   │   │──...
│   │   │   ├──C
│   │   │   │   │──...
├── create_tables.py                              <- creates and drops the tables defined in the schema
├── data_model.png                                <- data model for the Sparkify Postgres database
├── etl.ipynb                                     <- Jupyter notebook for testing and writing functions for etl.py
├── etl.py                                        <- runs the ETL processes to load song and log data into database
├── README.md                                     <- explanation of project, code and schema
├── sql_queries.py                                <- script that contains the queries to create and drop tables 
├── test.ipynb                                    <- Jupyter notebook used to test table creation and data insertion


## How to Run the Project: 

In order to execute the code in this workspace, please open the terminal from the home diretory and run 'python3 create_tables.py' then 'python3 etl.py' and it will process the files, create tables and load the data into the tables. You can also navigate to https://github.com/sagrawal01/udacitydataengineering and go to Project: Data Modeling with Postgres directory to execute the code. Please clone the repository and set up a virtual environment or docker container to execute the code within your local machine. 


