Exercise 2: 429, rejected_execution_exception:
*****************************************************
Please run below commands simultaneously from 3 EC2 machines(use bigger instance type minimum M4 to avoid OOM issues) and see how it is affecting the bulk queue of the cluster?

Use same cluster of exercise 1.

python elasticsearch-stress-test.py --es_address https://search-es51-wq5nykc2o2oxicrvxln6c2dmca.us-east-1.es.amazonaws.com --indices 1 --documents 1000 --clients 100 --seconds 300 --number-of-shards 100 --number-of-replicas 0 --bulk-size 10 --max-fields-per-document 10 --max-size-per-field 10 --no-cleanup --stats-frequency 15 --no-verify --not-green

Also, please create CloudWatch log groups to push your CloudTrail logs to the same Elasticsearch cluster.

Have you received rejected_execution_exception ? Please think about the reason and solutions.

Q: How you will monitor the bulk queue?

Note: We will get the rejected_execution_exception error in lambda logs.
