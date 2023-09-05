# MarketWatchDog

ssh -i "ameyakey.pem" ec2-user@ec2-3-145-20-135.us-east-2.compute.amazonaws.com

3.145.20.135

Secret Access Key IyJCDz+MOeUEfK0RALuIbOiuCG3ZecZ6SRqlbXWj

Access Key AKIAWIOX6JNDR5QPAFGD

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

A) 1st Terminal => Start Zoo-keeper:
-------------------------------
bin/zookeeper-server-start.sh config/zookeeper.properties

B) 2nd Terminal => Start Kafka-server:
-------------------------------
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
cd kafka_2.12-3.5.1 => add extra space for kafka server

bin/kafka-server-start.sh config/server.properties

C) 3rd Terminal => Create the topic:
-------------------------------
bin/kafka-topics.sh --create --topic demo_test --bootstrap-server {public EC2 IP address}:9092 --replication-factor 1 --partitions 1

D) 3th Terminal => Start Producer: (This is done in the same terminal as creating a topic)
-------------------------------
bin/kafka-console-producer.sh --topic demo_test --bootstrap-server {public EC2 IP address}:9092


E) 4th Terminal => Start Consumer:
-------------------------
bin/kafka-console-consumer.sh --topic demo_test --bootstrap-server {public EC2 IP address}:9092
