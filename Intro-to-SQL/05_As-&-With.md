# AS

# WITH ... AS

```python
# Query to select the number of transactions per date, sorted by date
query_with_CTE = """ 
                 WITH time AS 
                 (
                     SELECT DATE(block_timestamp) AS trans_date
                     FROM `bigquery-public-data.crypto_bitcoin.transactions`
                 )
                 SELECT COUNT(1) AS transactions,
                        trans_date
                 FROM time
                 GROUP BY trans_date
                 ORDER BY trans_date
                 """

# Set up the query (cancel the query if it would use too much of 
# your quota, with the limit set to 10 GB)
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
query_job = client.query(query_with_CTE, job_config=safe_config)

# API request - run the query, and convert the results to a pandas DataFrame
transactions_by_date = query_job.to_dataframe()

# Print the first five rows
transactions_by_date.head()

transactions_by_date.set_index('trans_date').plot()

```
![](https://www.kaggleusercontent.com/kf/79126389/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..VrK7vbI1TUqEKqVM7XdjbA.D2YpMafyLBZ5TrnRLr9tcoXqDnpuEWD7dzeoViE4Ld2wR24u-sXB4odkqz2n1illOveNJVESZqESt0_XV1niG2JZ3CoOZagcH6HCknbDVIQ39MMpn5LCb7jxYA6zpuSOGcjJ6Ztcgxl4tWIQRGSfhBg1M-0YzMXXV_wAUXioA6HtdHv1INVAFcnIojAIM86q6vwuT7Dz4klGxkuJ5R6zuaEb-x6IULhFor9y6YaePeL5Nb33dpgf6Rpm1oT5TZXoc_B8cqFLmMcJmFWUkM9IM_ehbtSAIxPGVEJKeBUzdVxHwc9sy_CfR28NdOYKITnEbscBBnKJlQrrUboqOpf_FmzgB0PCUIIs1xmX-fL77rKM89Ia8RFiCQEo_czAtyyzkt_jlpzDXuch1FonhwJcxoAiljGmpS7M0NYYDTueM4xztBJXJzrXSE3e1Vlmsd7fMnLc_-z4VRN_jrr2rF_4SENyHFyhxEQ226-iDbs5_06bz5apeWlj3_nSPi5ZSAOEwBYNHkzFQ7_iRv528DfO5qvK2QqydiziO29Slud1Zw95DUTfBj1OWRPO6hWhYO6SuLN3h6UV4EDHWRflgBwd12cewHCyVED28JaAp-gu1kqabWRkQfkfsfrMe8qilwoehz_oPTptd-xkp-UAjAnDug.GjpHRTvy4_3E-ukgkCG1Hg/__results___files/__results___6_1.png)
