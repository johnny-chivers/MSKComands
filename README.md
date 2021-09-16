# MSK Comands For Creating a Cluster and Streaming Data

Install Java:
sudo yum install java-1.8.0

Get Kafka:wget https://archive.apache.org/dist/kafka/2.2.1/kafka_2.12-2.2.1.tgz

Extract Kafka:
tar -xzf kafka_2.12-2.2.1.tgz

Get Cluster ARN:
aws kafka describe-cluster  --region us-east-2 --cluster-arn "ClusterArn"
aws kafka describe-cluster  --region us-east-2 --cluster-arn arn:aws:kafka:us-east-2:159363735810:cluster/test-cluster-1/cc80ac7c-3edf-4c6d-95c7-bce68fd48023-7

Create Topic:
bin/kafka-topics.sh --create --zookeeper "ZookeeperConnectString" --replication-factor 2 --partitions 1 --topic AWSKafkaTutorialTopic

User the Trust store:
cp /usr/lib/jvm/JDKFolder/jre/lib/security/cacerts /tmp/kafka.client.truststore.jks

client.properties:
security.protocol=SSL
ssl.truststore.location=/tmp/kafka.client.truststore.jks

Get Brokers:
aws kafka get-bootstrap-brokers --cluster-arn ClusterArn --region

Producer:
./kafka-console-producer.sh --broker-list BootstrapBrokerStringTls --producer.config client.properties --topic AWSKafkaTutorialTopic

Consumer:
./kafka-console-consumer.sh --bootstrap-server BootstrapBrokerStringTls --consumer.config client.properties --topic AWSKafkaTutorialTopic --from-beginning
