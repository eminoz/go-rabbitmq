# RabbitMQ

Docker image over [here](https://hub.docker.com/_/rabbitmq)
```
# run a standalone instance
docker network create rabbits
docker run -d --rm --net rabbits --hostname rabbit-1 --name rabbit-1 rabbitmq:3.8 

# how to grab existing erlang cookie
docker exec -it rabbit-1 cat /var/lib/rabbitmq/.erlang.cookie

# To run rubbitmq on docker
docker run -d --rm --net rabbits -p 8080:15672  --hostname rabbit-1 --name rabbit-1  rabbitmq:3.8 

# clean up
docker rm -f rabbit-1
```


# Message Publisher

```

cd messaging\rabbitmq\applications\publisher
docker build . -t eminoz/go-rabbitmq:latest 

docker run -it --rm --net rabbits -e RABBIT_HOST=rabbit-1 -e RABBIT_PORT=5672 -e RABBIT_USERNAME=guest -e RABBIT_PASSWORD=guest -p 80:80 eminoz/go-rabbitmq:latest 

```


# Message Consumer

```

docker build . -t aimvector/rabbitmq-consumer:v1.0.0
docker run -it --rm --net rabbits -e RABBIT_HOST=rabbit-1 -e RABBIT_PORT=5672 -e RABBIT_USERNAME=guest -e RABBIT_PASSWORD=guest aimvector/eminoz/go-rabbitmq-consumer:latest
```
