Exercise 2: 

Use same cluster of exercise 1.

1. Please run below commands simultaneously from 3 EC2 machines(use bigger instance type minimum M4 to avoid OOM issues) and see how it is affecting the bulk queue of the cluster?

```
python ~/elasticsearch-stress-test/elasticsearch-stress-test.py --es_address https://search-demo-cluster-1-765gtptpper6h3iajfukaj3yhy.us-east-1.es.amazonaws.com --indices 1 --documents 1000 --clients 1000 --seconds 600 --number-of-shards 100 --number-of-replicas 0 --bulk-size 10 --max-fields-per-document 10 --max-size-per-field 10 --no-cleanup --stats-frequency 15 --no-verify --not-green
```

2. Please run below commands on another EC2 machines and see have you received rejected_execution_exception ? Please think about the reason and solutions.

```
while true; do curl -XPOST  'https://search-demo-cluster-1-765gtptpper6h3iajfukaj3yhy.us-east-1.es.amazonaws.com/movies/_doc' -d '{"director": "Burton, Tim", "genre": ["Comedy","Sci-Fi"], "year": 1996, "actor": ["Jack Nicholson","Pierce Brosnan","Sarah Jessica Parker"], "title": "Mars Attacks!"}' -H 'Content-Type: application/json';printf '\n\n';sleep 1; done;
```

Q: How you will monitor the bulk queue
Q: What API can help us check the thredpool
Q: What suggestion will you give base on this

