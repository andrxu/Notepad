### docker commands

```bash
docker ps

docker images

docker-machine create --driver virtualbox --virtualbox-cpu-count 2 --virtualbox-memory 2048 {your virtual machine name}

docker-machine ip {your virtual machine name}

docker-machine ls  // list virtual machine

docker-machiine help

// connect the virtual machine

eval $(docker-machine env {virtual machine name}

docker ps

docker run -d -p 3000:3000 {image name}



