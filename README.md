# Udacity_code

Data Modeling with Apache Cassandra

Purpose

The purpose of this project is to create an Apache Cassandra database for a Music startup called Sparkify to query on song play data.
The raw data is in a directory of CSV files, and we will build a ETL pipeline to transform the raw data into the Apache Cassandra database.

Dataset

Ther is  one dataset: event_data. The directory of CSV files partitioned by date. The filepaths are given as event_data/<yyyy>-<mm>-<dd>-events.csv where <yyyy> indicates the year, <mm> indicates the month and <dd> indicates the year.

event_data/2018-11-08-events.csv
event_data/2018-11-09-events.csv

The fields of event_data file are:

artist (string)
auth (string)
firstName (string)
gender (char)
itemInSession (int)
lastName (string)
length (float)
level (string)
location (string)
method (string)
page (string)
registration (float)
sessionId (int)
song (string)
status (int)
ts (float)
userId (int)


Queries

For NoSQL databases, we design the schema based on the queries we already know we want to perform. For this Modelling project, we have three queries as below:

1) Find artist, song title and song length that was heard during sessionId=338, and itemInSession=4.
SELECT artist, song, length from artist_session_item WHERE sessionId=338 AND itemInSession=4

2) Find name of artist, song (sorted by itemInSession) and user (first and last name) for userid=10, sessionId=182.
SELECT artist, song, firstName, lastName FROM songinfo_user_session WHERE userId=10 and sessionId=182

3) Find every user name (first and last) who listened to the song 'All Hands Against His Own'.
SELECT firstName, lastName WHERE song='All Hands Againgst His Own'.


Schemas and Tables below created for the Project

For Query1:Table1:artist_session_item

Column 1 = sessionId
Column 2 = itemInSession
Column 3 = artist
Column 4 = song
Column 5 = length
Primary key = (sessionId, itemInSession)


For Query2:Table2:-songinfo_user_session

Column 1 = userId
Column 2 = sessionId
Column 3 = itemInSession
Column 4 = artist
Column 5 = song
Column 6 = firstName
Column 7 = lastName
Primary key = (userId, sessionId) with clustering column itemInSession


For Query3:Table3:-user_songs 


Column 1 = song
Column 2= userid
Column 3 = firstName
Column 4 = lastName
Primary key = (song, userId)


Created ETL Pipeline by following steps:-

1) There is a raw data csv files in events_data folder all 30 csv files.Used these  file to create a single event_datafile_full csv file that will be used to insert data into the # Apache Cassandra tables
2) For each row of the csv file file-event_datafile_full  , inserted the data in the appropriate columns as described in Schemas.
3) Ran the Select queries as described in the tables.


Build:

Run each segement of Project_1B_Project_Template.ipynb to get the desired results in the tables for all 3 queries.
