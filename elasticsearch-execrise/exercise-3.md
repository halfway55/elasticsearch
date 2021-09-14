Exercise 3: 

Create new Opensearch(Elasticsearch) cluster with bellow spec
```
ES version: 7.1
Instance type: m4.large.search
EBS:10GB
Number of nodes:3
```

Run below commands from a EC2 machines(use bigger instance type minimum M4 to avoid OOM issues) to create an index "shakespeare". Please replace domain endpoint with your own domain endpoint.

```
curl -H 'Content-Type: application/json' -XPUT 'https://search-timelion-test-vhe2bg7au5ueuuw2ff2w5b6d6m.us-east-1.es.amazonaws.com/shakespeare/' -d '{
    "settings" : {
        "index" : {
            "number_of_shards" : 3
        }
    }
}' 
```

Download sample file:
```
curl https://download.elastic.co/demos/kibana/gettingstarted/shakespeare_6.0.json -O 

```
Open file shakespeare_6.0.json and remove _id by 
```
ESC
:%s/,"_id":\w\+/
ESC
:wq
```
Now run bellow command to ingest data to the index
```
for i in {0..100};
do curl -H 'Content-Type: application/x-ndjson' -XPOST 'https://search-timelion-test-vhe2bg7au5ueuuw2ff2w5b6d6m.us-east-1.es.amazonaws.com/shakespeare/_bulk?routing=user1' --data-binary @shakespeare_6.0.json;  
printf '\n\n'; 
done;
```

Check shard allocation using API and K2 script
```
GET _cat/shards/shakespeare?v
```

* Explain the result 
* What problem may arise
* How to mitigate this issue

