aws configure com valores = test
em vez de usar networking_mode host criar um network (windows)
invocar a lambda via interface localstack (problema de cors)
---
curl -XPOST -H "Content-Type: application/json" http://localhost:8083/connectors -d @connector-localstack.json

{"name":"example-lambda-connector-localstack","config":{"tasks.max":"1","connector.class":"com.nordstrom.kafka.connect.lambda.LambdaSinkConnector","topics":"example-stream","key.converter":"org.apache.kafka.connect.storage.StringConverter","value.converter":"org.apache.kafka.connect.storage.StringConverter","aws.region":"us-east-1","aws.lambda.function.arn":"arn:aws:lambda:us-east-1:000000000000:function:example-function","aws.lambda.invocation.timeout.ms":"60000","aws.lambda.invocation.mode":"SYNC","aws.lambda.batch.enabled":"false","localstack.enabled":"true","name":"example-lambda-connector-localstack"},"tasks":[],"type":"sink"}

-----
curl --request GET --url http://localhost:8083/connectors/example-lambda-connector-localstack/status 

{"name":"example-lambda-connector-localstack","connector":{"state":"RUNNING","worker_id":"127.0.0.1:8083"},"tasks":[{"id":0,"state":"RUNNING","worker_id":"127.0.0.1:8083"}],"type":"sink"}

