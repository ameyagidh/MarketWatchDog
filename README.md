# MarketWatchDog

#### login to the terminal create 4 terminals 
1. Zookeeper terminal
2. Kafka Cluster
3. Producer
4. Consumer

#### Steps 

1. Create EC2 instance on AWS, copy the public IP address, add security group and allow access from an IP address 

2. Install kafka on your EC2 instance :-
   wget https://downloads.apache.org/kafka/3.5.0/kafka_2.12-3.5.0.tgz
   tar -xvf kafka_2.12-3.5.0.tgz
   cd kafka_2.12-3.5.0

3. Install Java on the Ec2 Instance :- 
    sudo yum install java
   
4. Now add the public IPv4 address from your EC2 instance to the zookeeper
   sudo nano config/server.properties - change ADVERTISED_LISTENERS to public ip of the EC2 instance  
  
wget https://downloads.apache.org/kafka/3.5.1/kafka_2.12-3.5.1.tgz
tar -xvf kafka_2.12-3.5.1.tgz

-------------------------
### Step A: Start Zookeeper (1st Terminal) :

bin/zookeeper-server-start.sh config/zookeeper.properties

-------------------------
### Step B: Start Kafka-server (2nd Terminal):

export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
cd kafka_2.12-3.5.1 => add extra space for kafka server

bin/kafka-server-start.sh config/server.properties

 => Create the topic:
bin/kafka-topics.sh --create --topic demo_test --bootstrap-server {public EC2 IP address}:9092 --replication-factor 1 --partitions 1

-------------------------
### Step C: Start Producer (3rd Terminal) (This is done in the same terminal as creating a topic):

bin/kafka-console-producer.sh --topic demo_test --bootstrap-server {public EC2 IP address}:9092

-------------------------
### Step D: Start Consumer (4th Terminal):

bin/kafka-console-consumer.sh --topic demo_test --bootstrap-server {public EC2 IP address}:9092

-------------------------

