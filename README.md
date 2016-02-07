# Log-Feeding-into-Elasticsearch-using-Kafka
Step 1: Download from below link 
*********************************  
wget http://a.mbbsindia.com/kafka/0.8.2.2/kafka_2.11-0.8.2.2.tgz  
Instal Kafka  
Download the 0.9.0.0 release and un-tar it. 
tar -xzf kafka_2.11-0.8.2.2.tgz 
cd kafka_2.11-0.8.2.2.tgz  
Download Zookeeper  
wget http://a.mbbsindia.com/zookeeper/zookeeper-3.4.6.tar.gz  
Install Zookeeper  tar -xvf zookeeper-3.4.6.tar.gz  

Step 2: Start Zookeeper 
***********************  
sudo bin/zookeeper-server-start.sh config/zookeeper.properties  

Step 3: Start Kafka 
*******************  
sudo bin/kafka-server-start.sh config/server.properties  
Error while starting Kafka  INFO shutting down (kafka.server.KafkaServer)  
Resolution : Kafka instances are already running.Need to kill running services of Kafka and start Kafka again by following Step 3  

Step 4: Create a Topic 
**********************  
Create topic named "Test" with a single partition and one replica:  
> bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic Test  

Step 5: List topic 
******************  
> bin/kafka-topics.sh --list --zookeeper localhost:2181 Test  

Step 6: Send Message 
******************** 
Kafka comes with a command line client that will take input from a file or from standard input and send it out as messages to the Kafka 
cluster. By default each line will be sent as a separate message.  

Step 7: Run producer and send messages into the console 
*******************************************************  
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test  
Test Message 
Second Test Message: Send Message in Producer and check same in consumer Terminal  

Step 8: Start Consumer 
**********************  
Kafka also has a command line consumer that will dump out messages to standard output.  
> bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning 
Test Message 
Second Test Message: Send Message in Producer and check same in consumer Terminal  

Step 9: Start Connector 
***********************  
bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-source.properties config/connect-file-sink.properties     

Mention Log file which need to be input into Kafka in config file of Kafka i.e. connect-file-source.properties .  

Step 10 : Configure Logstash 
**************************** 
Run Logstash after doing changes in config file so that log file can be received from Kafka topic connect-test to Elasticsearch
