1. COUNT(): 
2. GROUP BY():
3. **GROUP BY ... HAVING:** HAVING se usa en combinación con GROUP BY para ignorar los grupos que no cumplen con ciertos criterios.
```python
query="""
    SELECT Animal, COUNT(ID)
    FROM `bigquery-public-data.pet_records.pets`
    GROUP BY Animal
    HAVING COUNT(ID) > 1
"""
```
