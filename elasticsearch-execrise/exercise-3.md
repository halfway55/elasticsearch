Exercise 3: 

Create new Opensearch(Elasticsearch) cluster with bellow spec
```
ES version: 7.10
Instance type: m4.large.search
EBS:10GB
Number of nodes:3
```

1. Run below command to create an index "twitter" 
```
curl -H 'Content-Type: application/json' -XPUT 'https://search-timelion-test-vhe2bg7au5ueuuw2ff2w5b6d6m.us-east-1.es.amazonaws.com/twitter/' -d '{
    "settings" : {
        "index" : {
            "number_of_shards" : 3, 
            "number_of_replicas" : 0 
        }
    }
}' 
```

2. Run below command to ingest data into an index "twitter" 
```
for i in {1..1000}; do curl -H 'Content-Type: application/json' -XPOST 'https://search-timelion-test-vhe2bg7au5ueuuw2ff2w5b6d6m.us-east-1.es.amazonaws.com/twitter/_doc?routing=user1' -d '{
  "title": "This is a document"
}';  printf '\n\n'; done;

```



Analyze the cluster with Elasticsearch APIs and K2.
Cluster should turn red. Think why the cluster turned red?
