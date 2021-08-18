# Project 1: Data Modeling with Postgres

In order to run the files, on console, run craete_tables.py to drop and create the tables (this should be done each time). Then run etl.py to insert records into the tables. etl.ipynb is the test code for etl.py and teset.ipynb is used to validate that the code is woring as expected.

The goal is to create five main tables: songplays, users, artists, songs, and time. We are reading .json log files for each session where user played a song on an app, along with song files that contain information about the song. This data is combined to create the songplays facts table and the users, songs, artists and time dimension tables.
