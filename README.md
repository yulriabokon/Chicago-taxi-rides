SELECT *
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
LIMIT 100


SELECT payment_type, COUNT(*) as count_cash
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type='Cash'
GROUP BY payment_type


SELECT payment_type,COUNT(*) as count_credit_card
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type = 'Credit Card'
GROUP BY payment_type


SELECT EXTRACT(HOUR FROM trip_start_timestamp) AS hour_of_day, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY hour_of_day
ORDER BY hour_of_day DESC


SELECT EXTRACT(HOUR FROM trip_end_timestamp) AS hour_of_day, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY hour_of_day
ORDER BY hour_of_day






SELECT EXTRACT(DAYOFWEEK FROM trip_start_timestamp) AS day_of_week, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY day_of_week
ORDER BY day_of_week


SELECT EXTRACT(MONTH FROM trip_start_timestamp) AS month, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY month
ORDER BY month


SELECT
   pickup_location AS community_area,
   COUNT(*) AS pickup_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE pickup_location IS NOT NULL
GROUP BY pickup_location
ORDER BY pickup_count DESC
LIMIT 10;






SELECT 
    FORMAT("POINT(%f %f)", pickup_longitude, pickup_latitude) AS pickup_location,
    COUNT(*) AS pickup_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE pickup_longitude IS NOT NULL AND pickup_latitude IS NOT NULL
GROUP BY pickup_location
ORDER BY pickup_count DESC
LIMIT 10;

SELECT payment_type,AVG(trip_miles) AS average_trip_miles
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type = 'Credit Card'
GROUP BY payment_type

SELECT payment_type,AVG(trip_miles) AS average_trip_miles
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type = 'Cash'
GROUP BY payment_type


SELECT tips, COUNT(*) as count_tips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE 'tips' IS NOT NULL 
GROUP BY tips
ORDER BY count_tips ASC
LIMIT 1


SELECT company, COUNT(*) as count_company
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE 'company' IS NOT NULL 
GROUP BY company
ORDER BY count_company DESC
LIMIT 3

SELECT payment_type,EXTRACT(HOUR FROM trip_end_timestamp) AS hour_of_day, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type='Cash'
GROUP BY hour_of_day,payment_type
ORDER BY trip_count DESC

SELECT payment_type,tips,EXTRACT(HOUR FROM trip_end_timestamp) AS hour_of_day, COUNT(*) AS trip_count
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE payment_type='Cash'
GROUP BY hour_of_day,payment_type,tips
ORDER BY tips DESC# Chicago-taxi-rides
