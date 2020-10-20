# Project-3-Data-Warehouse
Data modelling - Data Warehouse with RedShift

# This repo contains the Code for create an IaC with Redshift cluster, S3 and IAM Roles, used to create the ingestion based on the files that come on the S3 bucket, and the code to load the files to the Redshift tables.

Let's get started with this code

## Table of Contents

1. [Quick start](#quick-start)
1. [Song Dataset](#Song-Dataset)
1. [Log Dataset](#Log-Dataset)
1. [Prepare the environment](#Prepare-the-environment)
1. [Clean the environment](#Clean-env)


## Quick start

1. The purpose here, is to load some songs data, thinking in a self service architecture, to build a Data Warehouse based on the data loaded before.

Notes:

We have 2 datasets here:

## Song Dataset
The first dataset is a subset of real data from the https://labrosa.ee.columbia.edu/millionsong/. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```

## Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.


```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json
```


And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.


| artist | auth | firstName | gender | itemInSession | lastName | length | level | location | method | page | registration | sessionId | song | status | ts | userAgent | userId |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                                                                         |

```
Sydney Youngblood Logged In Jacob M 53 Klein 238.07955 paid Tampa-St. Petersburg-Clearwater, FL PUT NextSong 1.540558e+12 954 Ain't No Sunshine 200 1543449657796 "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4... 73 1 Gang Starr Logged In Layla F 88 Griffin 151.92771 paid Lake Havasu City-Kingman, AZ PUT NextSong 1.541057e+12 984 My Advice 2 You (Explicit) 200 1543449690796 "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebK... 24 2 3OH!3 Logged In Layla F 89 Griffin 192.52200 paid Lake Havasu City-Kingman, AZ PUT NextSong 1.541057e+12 984 My First Kiss (Feat. Ke$ha) [Album Version] 200 1543449841796 "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebK... 24 3 RÃ�Â¶yksopp Logged In Jacob M 54 Klein 369.81506 paid Tampa-St. Petersburg-Clearwater, FL PUT NextSong 1.540558e+12 954 The Girl and The Robot 200 1543449895796 "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4... 73 4 Kajagoogoo Logged In Layla F 90 Griffin 223.55546 paid Lake Havasu City-Kingman, AZ PUT NextSong 1.541057e+12 984 Too Shy 200 1543450033796 "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebK... 24

```

The code here, will build an architecture, to create and load the data inside a Redshift cluster.

So, to run the code, you will need to follow these steps:
1) To create the redshift cluster, and the IAM roles and config the dwh.cfg file
    $ %run create_structure_IaC.py
2) To drop/create the tables inside the Redshift cluster
    $ %run create_tables.py
3)  To load the tables based on the files on the S3 bucket (JSON)
    $ %run etl.py
    
# If you have some problems with the execution, install the following requirements:

## Prepare the environment

```
$ pip install boto3 && pip install psycopg2
```

## Clean the environment

At the end of the process

```
Follow the comments inside the main function, and uncomment the clean line, and comment the others, in the create_stucture_IaC.py file

    #clean_redshift_cluster()
    #clean_iam_roles()
    
    
And after you comment the other lines, run it again:

    $ %run create_structure_IaC.py
    
```

##End of README

