### ssh tunnel

```bash
vim ~/.ssh/config

# add following to the config. Then you can type 'ssh gateway' to establish connection.
# use localhost:55439 to connect to the remote server remote_server_blah_blah.amazonaws.com:5439

Host gateway
HostName gateway.remote_server_blah_blah.com
User andrew
IdentityFile ~/.ssh/id_rsa
Compression yes
KeepAlive yes
ServerAliveInterval 60
ForwardAgent yes
LocalForward 55439 remote_server_blah_blah.amazonaws.com:5439
#ProxyCommand ssh andrew@gateway.remote_server_blah_blah.com nc %h %p 2> /dev/null
```

```bash
ssh gateway
```

```
ssh -L 8888:[host name]:80 andrxu@[jump box ip] -N
```

### sql dump

```bash
ssh andrew@mysql-box.com
mysqldump -h localhost --databases orders -u [username] -p[password] > ~/orders_dump.sql
exit
scp andrew@pmysql-box.com:~/orders_dump.sql ~/local_dump/
mysql -h localhost -uroot orders < ~/local_dump/orders_dump.sql

```

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

docker rm all containers
docker rmi all images

```


###   Misc

```bash

#cd ~/project/app/src/main/webapp/angular 
node ~/project/app/node_modules/gulp/bin/gulp
memcached -d -m 24 -p 11211
lsof -i:8080


```

### AWS keys

``` bash
# access redshift
ssh jump.your_company.com
psql --host=redshift.fdfdfsdfs.us-west-2.redshift.amazonaws.com --port=5439 --username=(your username) --dbname=(your dbname)

# access sql
ssh -t jump.your_company.com mysql -h [host server name] -u [your_username] -p[your_password] [database name]
```
### invoke REST api

``` bash
ssh -N -L 8443:production.api.your_company.com:443 jump.your_company.com &
And then you can access api via localhost:8443. Example:
curl -u USERNAME:PASSWORD  -k "https://localhost:8443/api/students/12345"

```

### svn
``` bash 
check out trunk and cd to it
make sure you have no diffs and that it is up to date
svn merge http://svn/SSC/feature-branch-path .
```

### sql dump
``` bash
mysqldump -h localhost --databases orders -u [username] -p[password] > ~/orders.sql  #create a dump
scp andrew@blah.your_company.net:~/order.sql .                                       #copy the dump    
mysql -h localhost -uroot -p orders < orders.sql                                     #import
```

### mvn
``` bash
mvn jetty:run -Dbranch=local -DredisUri=redis://localhost:32768 
``` 
