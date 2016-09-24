### docker commands

```bash

docker-machine create --driver virtualbox --virtualbox-cpu-count 2 --virtualbox-memory 2048 {your virtual machine name}

docker-machine ip {your virtual machine name}

docker-machine ls  # list virtual machine

docker-machiine help

// connect the virtual machine

eval $(docker-machine env {virtual machine name}

docker ps -a 

docker images

docker run -d -p 3000:3000 {image name}

// start Zookeeper 
docker run -d -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper confluent/zookeeper 

// start kafka
docker run -d -p 9092:9092 -e KAFKA_ADVERTISED_HOST_NAME=`docker-machine ip {your virtual machine name}` -e KAFKA_ADVERTISED_PORT=9092 --name kafka --link zookeeper:zookeeper confluent/kafka 

// down load Zookeeper CLI
cd zookeeper/bin
./zkcli.sh -server localhost:2181
./zkCli.sh -server {virtual machine ip}:2181

ls /brokers/topics // check topics 

// down load Kafaka CLI
./kafka-topics.sh --list --zookeeper 192.168.99.100

docker exec -it kafaka bash  // go into the container 





