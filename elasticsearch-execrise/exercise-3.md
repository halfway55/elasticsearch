Exercise 3: Red cluster
**************************
ES version: 1.x
Instance type: t2.micro
EBS:10GB
Number of nodes:1

Run below command on a 1.5 cluster and see what happens? Analyze the cluster with Elasticsearch APIs and K2.

curl -XPUT 'https://search-sajeev-test-7q52y2kv3vtjig3g4qq2hnwpyq.us-east-1.es.amazonaws.com/twitter2/' -d '{
    "settings" : {
        "index" : {
            "number_of_shards" : 1024, 
            "number_of_replicas" : 2 
        }
    }
}'



Cluster should turn red. Think why the cluster turned red?
