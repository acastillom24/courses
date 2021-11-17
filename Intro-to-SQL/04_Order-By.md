1. Dates: El formato FECHA tiene primero el año, luego el mes y luego el día.

> YYYY-[M]M-[D]D
- YYYY: Four-digit year
- [M]M: One or two digit month
- [D]D: One or two digit day

2. EXTRACT
```python
query = """
  SELECT Name, EXTRACT(DAY from Date) as Day
  FROM `bigquery-public-data.pet_records.pets_with_date`
"""

query = """
  SELECT Name, EXTRACT(WEEK from Date) as Day
  FROM `bigquery-public-data.pet_records.pets_with_date`
"""

query = """
        SELECT COUNT(consecutive_number) AS num_accidents, 
               EXTRACT(DAYOFWEEK FROM timestamp_of_crash) AS day_of_week
        FROM `bigquery-public-data.nhtsa_traffic_fatalities.accident_2015`
        GROUP BY day_of_week
        ORDER BY num_accidents DESC
        """
```

> Nota: *DAYOFWEEK* devuelve "un número entero entre 1 (domingo) y 7 (sábado)"
