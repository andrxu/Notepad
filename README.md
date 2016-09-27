### docker commands

```bash

docker-machine create --driver virtualbox --virtualbox-cpu-count 2 --virtualbox-memory 2048 {your virtual machine name}

docker-machine ip {your virtual machine name}

docker-machine ls  # list virtual machine

docker-machine help

# connect the virtual machine

eval $(docker-machine env {virtual machine name}

docker ps -a 

docker images

docker run -d -p 3000:3000 {image name}

# start Zookeeper 
docker run -d -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper confluent/zookeeper 

# start kafka
docker run -d -p 9092:9092 -e KAFKA_ADVERTISED_HOST_NAME=`docker-machine ip {your virtual machine name}` -e KAFKA_ADVERTISED_PORT=9092 --name kafka --link zookeeper:zookeeper confluent/kafka 

# down load Zookeeper CLI
cd zookeeper/bin
./zkcli.sh -server localhost:2181
./zkCli.sh -server {virtual machine ip}:2181

ls /brokers/topics # check topics 

# down load Kafaka CLI
./kafka-topics.sh --list --zookeeper 192.168.99.100

docker exec -it kafaka bash  # go into the container 

# down load cassandra CLI
./cqlsh `docker-machine ip biddata` 9042

>CREATE KEYSPACE “stock” WITH replication = {'class': 'SimpleStrategy', 'replication_factor':1} AND durable_writes = 'true';
>USE stock;
>DESCRIBE KEYSPACE;
>CREATE TABLE user ( first_name text, last_name text, PRIMARY KEY (first_name));
>DESCRIBE TABLE user;

docker exec -it cassandra bash
cd /var/lib/cassandra
ls




