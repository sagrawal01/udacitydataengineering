# Project Description: Data Modeling with Apache Cassandra

In this project, we are creating an ETL pipeline for a startup, Sparkify, that reads data from a directory of csv files and loads the data into an Apache Cassandra to understand which songs the users are listening. The data is processed from the raw events csv file, consolidated in one file, loaded into Apache Cassandra and tested with a few queries to ensure that it was properly loaded.

## There are three tables that have been created in this database:

1. song_sessions - table that contains information about sessions and songs
2. user_sessions - table that contains information about user sessions and the song in that session
3. user_song_history - table that contains information about the songs that a user has listened to

## ETL Process:

1. The files in event_data directory are processed into one csv data file: event_datafile_new.csv
2. The Apache Cassandra keyspace song_data is created and the three tables listed above are created and loaded with data from the event_datafile_new.csv
3. Queries are used to check that the data was inserted.
4. The tables are dropped and the database connection is closed
