# eth-data-pipeline

A data pipeline for enriching and summarizing ethereum token transfer data one day at a time powered by Infura API

1. Summatizing data from the public BigQuery table `bigquery-public-data.crypto_ethereum.token_transfers`.
  - Count the number of transactions for each `token_address` and save top 100
1. Enriching the data with information from the blockchain using the provided Infura node endpoint
  - Append token `name` and `symbol`
1. Processing one day at a time
1. Each execution of the pipeline triggered by running the Python function `run_batch_job` (see below)
1. Storing the result of each run in a BigQuery table 


| event_date | token_name | token_symbol | token_address | number_of_transfers |
|---|---|---|---|---|
| 2022-01-01 | USD Coin | USDC | 0x123... | 1000 | 
| 2022-01-01 | Aave | AAVE | 0x456... | 800 | 
| 2022-01-01 | Wrapped Ether | WETH | 0x789... | 600 | 

Extra:
 - The pipeline uses as few Infura lookups as possible
 - You may not use state in memory between pipeline runs (variables in Python)

for dates 2022-01-01 -> 2022-01-03 (three days)
