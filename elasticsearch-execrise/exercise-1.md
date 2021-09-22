Exercise 1

1. Create Opensearch(Elasticsearch) cluster with bellow spec
```
ES version: 7.10
Instance type: m4.large.search
EBS:10GB
Number of nodes:1
```
Set up [error logs](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createdomain-configure-slow-logs.html) for the cluster in the AWS ES console.


2. Download elasticsearch stress test script
```
sudo yum install git -y
```
```
git clone https://github.com/logzio/elasticsearch-stress-test.git
```
You should be running python 2.7+

```
sudo yum install python-pip -y
```
```
sudo pip install elasticsearch==7.13.1
```
You should use elasticsearch client < 7.14 as there is a version [break point](https://github.com/elastic/elasticsearch-ruby/issues/1429)

3. Run below command: This is just to push some documents to Elasticsearch cluster continuously. Please replace domain endpoint with your own domain endpoint.
```
for i in {0..10}; do python ~/elasticsearch-stress-test/elasticsearch-stress-test.py --es_address https://search-demo-cluster-1-765gtptpper6h3iajfukaj3yhy.us-east-1.es.amazonaws.com --indices 1 --documents 100 --clients 10 --seconds 600 --number-of-shards 1 --number-of-replicas 0 --bulk-size 5000 --max-fields-per-document 10 --max-size-per-field 700 --no-cleanup --stats-frequency 5 --not-green --no-verify; done;
```
Note: If cluster is yellow, you should specify --not-green in the command. Also, you may have to run the script multiple times to hit the free storage water mark.

1. Monitor cluster change with the help of K2 script and other ES APIs
   1. What's the difference between CW FreeStorageSpace and _cluster/stats and _cat/allocation APIs
1. Check when you are getting index_create_block_exception
1. How can you check cluster index write block using Elasticsearch APIs?
1. which log you will analyze to see the issue if you are the customer?

Note: The block may not be removed quickly

Clean up test index
```
DELETE *,-.kibana_1
```
