# Assignment

## Brief

Write the SQL DML statements for the following questions.

## Instructions

Paste the answer as SQL in the answer code section below each question.

### Question 1

Select the minimum and maximum price per sqm of all the flats.

```sql

```SELECT 
    claim.id, 
    claim.claim_date, 
    claim.travel_time, 
    claim.claim_amt,
    car.car_type, 
    car.car_use
FROM claim
JOIN car ON claim.car_id = car.id;

```

### Question 2

Select the average price per sqm for flats in each town.

```sql
SELECT 
    c.id,
    c.car_id,
    c.travel_time,
    SUM(c.travel_time) OVER (PARTITION BY c.car_id ORDER BY c.id) AS running_total
FROM claim c;

```

### Question 3

Categorize flats into price ranges and count how many flats fall into each category:

- Under $400,000: 'Budget'
- $400,000 to $700,000: 'Mid-Range'
- Above $700,000: 'Premium'
  Show the counts in descending order.

```sql
WITH CarResaleValues AS (
    SELECT 
        car_use,
        resale_value
    FROM car
),
AverageResale AS (
    SELECT 
        car_use,
        AVG(resale_value) AS avg_resale_value
    FROM CarResaleValues
    GROUP BY car_use
)
SELECT 
    c.id,
    c.resale_value,
    c.car_use
FROM car c
JOIN AverageResale a ON c.car_use = a.car_use
WHERE c.resale_value < a.avg_resale_value;

```

### Question 4

Count the number of flats sold in each town during the first quarter of 2017 (January to March).

```sql
SELECT 
    town,
    COUNT(*) AS flats_sold
FROM flats_sale
WHERE sale_date >= '2017-01-01' AND sale_date <= '2017-03-31'
GROUP BY town;
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
