Chicago Taxi Trips Analysis 🚖
Project Title: Analyzing Temporal and Spatial Trends in Chicago Taxi Trips

Project Description:
This project focuses on analyzing taxi trip data from the publicly available BigQuery dataset bigquery-public-data.chicago_taxi_trips.taxi_trips. The analysis aims to uncover temporal trends, payment preferences, spatial patterns, and company performance within the Chicago taxi service ecosystem. 

SQL was used to query and analyze the dataset.
BigQuery served as the primary platform for dataset querying and exploration.
Aggregation, grouping, and sorting techniques were utilized to extract meaningful insights.
Applications:
The results of this analysis can assist taxi service providers, urban planners, and policymakers in:

-- I selected all information from the table
SELECT *
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`


--I analyzed the Chicago taxi trips dataset to determine how many trips were paid for using cash. 
SELECT payment_type, COUNT(*) as count_cash
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type='Cash'
GROUP BY payment_type

--I analyzed the Chicago taxi trips dataset to determine how many trips were paid for using credit card.
SELECT payment_type,COUNT(*) as count_credit_card
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type = 'Credit Card'
GROUP BY payment_type

--I analyzed the hourly distribution of Chicago taxi trips based on the start time of the trips.
SELECT EXTRACT(HOUR FROM trip_start_timestamp) AS hour_of_day, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY hour_of_day
ORDER BY hour_of_day DESC

----I analyzed the hourly distribution of Chicago taxi trips based on the end time of the trips.
SELECT EXTRACT(HOUR FROM trip_end_timestamp) AS hour_of_day, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY hour_of_day
ORDER BY hour_of_day

--Day-of-week distribution of Chicago taxi trips based on the start time of the trips
SELECT EXTRACT(DAYOFWEEK FROM trip_start_timestamp) AS day_of_week, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY day_of_week
ORDER BY day_of_week

--Month distribution of Chicago taxi trips based on the start time of the trips

SELECT EXTRACT(MONTH FROM trip_start_timestamp) AS month, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY month
ORDER BY month

--top 10 community areas in Chicago with the highest number of taxi pickups
SELECT
   pickup_location AS community_area,
   COUNT(*) AS pickup_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE pickup_location IS NOT NULL
GROUP BY pickup_location
ORDER BY pickup_count DESC
LIMIT 10;

--top 10 pickup points in Chicago based on geographical coordinates
SELECT 
    FORMAT("POINT(%f %f)", pickup_longitude, pickup_latitude) AS pickup_location,
    COUNT(*) AS pickup_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE pickup_longitude IS NOT NULL AND pickup_latitude IS NOT NULL
GROUP BY pickup_location
ORDER BY pickup_count DESC
LIMIT 10;

--I calculated the average trip distance for taxi trips where the payment method was Credit Card
SELECT payment_type,AVG(trip_miles) AS average_trip_miles
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type = 'Credit Card'
GROUP BY payment_type

----I calculated the average trip distance for taxi trips where the payment method was cash

SELECT payment_type,AVG(trip_miles) AS average_trip_miles
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type = 'Cash'
GROUP BY payment_type

--tips in Chicago taxi trips
SELECT tips, COUNT(*) as count_tips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE 'tips' IS NOT NULL 
GROUP BY tips
ORDER BY count_tips ASC
LIMIT 1

--top 3 taxi companies in Chicago with the highest number of trips
SELECT company, COUNT(*) as count_company
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE 'company' IS NOT NULL 
GROUP BY company
ORDER BY count_company DESC
LIMIT 3

My insights:

1.More people paid with cash than with credit cards.
2.The highest number of taxi trips occurred at 6:00 PM and on Saturday.
3.The highest number of taxi trips took place in June.
4.The average trip distance paid by credit card was 4.36 miles.
5.The average trip distance paid by cash was 2.76 miles.
6.The two most popular companies were Taxi Affiliation Services and Flash Cab.

 

